# AI & Open-Source Developer Guide — SHX Tester v3.00

> Free & Open Source (**MIT License**) — Built to be clean, dependency-light, and straightforward for both human developers and AI coding assistants to extend.

---

## 1. Architecture Overview

`SHXTester` is a single-file-publishable **C# (.NET 8 WPF + Microsoft Edge WebView2)** desktop application.
All frontend assets and offline 1080p/WAV media live inside `src/SHXTester/wwwroot/` and are embedded directly inside `SHXTester.exe` via `.csproj`:

```xml
<EmbeddedResource Include="wwwroot\**\*" LogicalName="wwwroot/%(RecursiveDir)%(Filename)%(Extension)" />
```

On startup (`MainWindow.xaml.cs`), the app extracts embedded UI & media assets into `%TEMP%\SHXTester_UI_v3` (skipping intact `media\` files whose size matches to keep repeat launches instant) and maps them to `https://shx.app/` using `SetVirtualHostNameToFolderMapping`.

### Key Files
| File | Purpose |
|------|---------|
| `src/SHXTester/SHXTester.csproj` | .NET 8 `net8.0-windows` WPF project (`v3.0.0`, `WebView2`, `System.Management`, single-file config) |
| `src/SHXTester/app.manifest` | Requests `requireAdministrator` so low-level WMI/ACPI/SMBIOS/powercfg queries succeed |
| `src/SHXTester/MainWindow.xaml` | Borderless dark chrome host window (`Title="SHX Tester v3.00"`) |
| `src/SHXTester/MainWindow.xaml.cs` | Smart cached asset extractor, Win32 true monitor-bounds fullscreen, JSON-RPC router & stress session lifecycle |
| `src/SHXTester/BatteryStressWindow.cs` | Automated WebView2 stress browser (YouTube + Web + Office + Offline video fallback) + floating Top-Right WPF HUD (`Elapsed`, `Battery %`, `Est. Shutdown`, `STOP`) |
| `src/SHXTester/HardwareService.cs` | Native WMI, SMBIOS/Registry fallback, EDID, `netsh`, scaled `ToggleCpuStress(start, loadPercent, includeRam)`, `AutoConfigureBatteryPreTest()`, speed test & SAPI stereo WAV TTS |
| `src/SHXTester/wwwroot/index.html` | Titlebar shell, sub-navigation workflow bar, modals, display overlay (`canvas` + `img` + `video`) |
| `src/SHXTester/wwwroot/styles.css` | Base structural styles & component grids |
| `src/SHXTester/wwwroot/liquid-glass.css` | Eye-Comfort Liquid Glass theme, `body.shx-display-fullscreen` chrome hiding, battery controls & `@media print` A4 PDF CSS |
| `src/SHXTester/wwwroot/qr.js` | Offline zero-dependency ISO/IEC 18004 QR Code SVG generator (Versions 1–5, ECC Level L) |
| `src/SHXTester/wwwroot/app.js` | Single-file state machine (`App`), i18n (`en`/`ar`), workflows, 3-suite display test, bilingual speaker test, automated battery UI, QR Certificate & exports |
| `src/SHXTester/wwwroot/media/` | Embedded `audio/{ar,en}_{left,center,right}.wav`, `photos/*.png`, `videos/*.mp4`, `deadpixel/*.{png,mp4}` |

---

## 2. JS ↔ C# Bridge Protocol

Messages flow over `window.chrome.webview.postMessage(JSON.stringify({ cmd, reqId, ...args }))` and resolve asynchronously via `Bridge.call(cmd, payload)`. Host push events emit `{ eventType, payload }` dispatched on `window` as `'shx-event'`.

### Registered `cmd` Handlers (`MainWindow.xaml.cs`)
- `window.minimize` / `window.maximize` / `window.close` / `window.fullscreen` (`enter: bool` — toggles Win32 `rcMonitor` `HWND_TOPMOST` covering Windows Taskbar)
- `hw.overview` → `HardwareService.GetFullSystemOverview()`
- `hw.antifake` → `HardwareService.RunAntiFakeScan()` (7-check WMI vs Kernel/Registry/SMBIOS/BIOS-Date/EDID)
- `hw.drivers` / `hw.startup` / `hw.license` / `hw.usb` / `hw.peripherals`
- `hw.netbt` / `hw.net.speed`
- `hw.speak` (`text`, `channel`, `lang`) → fallback SAPI PCM stereo WAV generator (primary voice uses embedded `wwwroot/media/audio/{lang}_{channel}.wav`)
- `hw.temp` / `hw.stress` (`start`, `loadPercent`, `includeRam`) → `HardwareService.ToggleCpuStress()`
- `hw.battery` / `hw.battery.autoconfig` (`powercfg` DC timeouts + WMI 75% brightness)
- `hw.battery.stress.start` (`mode`, `cpuLoadPercent`, `stressCpu`, `stressRam`, `useYouTube`, `useWeb`, `useOffice`, `lang`) → starts `BatteryStressSession`
- `hw.battery.stress.stop` → stops `BatteryStressSession` and pushes `battery.stress.stopped` event with summary telemetry
- `hw.storage.list` / `hw.storage.speed` / `hw.benchmark`
- `report.export` (`format: "html" | "pdf" | "json"`, `content`, `filename`)
- `history.load` / `history.save` (`%LocalAppData%\SHXTester\history.json`)

---

## 3. Build & Self-Contained Publish Commands

```powershell
# Standard Release build
dotnet build src\SHXTester\SHXTester.csproj -c Release

# Self-contained single-file executable (bundles .NET 8 Runtime + all 1080p/WAV media)
dotnet publish src\SHXTester\SHXTester.csproj -c Release -r win-x64 --self-contained true `
  -p:PublishSingleFile=true -p:IncludeAllContentForSelfExtract=true `
  -p:IncludeNativeLibrariesForSelfExtract=true -p:DebugType=None -p:DebugSymbols=false
```

Output executable path:
`src\SHXTester\bin\Release\net8.0-windows\win-x64\publish\SHXTester.exe`

---

## 4. Conventions for Contributors

- Keep dependencies minimal (no external JS/npm build step; embedded WebView2 UI runs 100% offline).
- Keep Display Suites 1 (`colors`), 2 (`media`), and 3 (`deadpixel`) strictly separate without overlapping media files.
- Always test audio channel isolation (`left = L only, R = 0`, `right = R only, L = 0`) and stop stress/HUD timers deterministically inside `BatteryStressSession.Stop()`.
