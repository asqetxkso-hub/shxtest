# ☄️ SHX Tester v3.00 Pro — Liquid Glass Edition

**The Ultimate Free & Open-Source Laptop Hardware, Peripherals & Buyer Inspection Suite for Windows (100% Portable Single-File EXE)**  
**الأداة الشاملة المجانية ومفتوحة المصدر لفحص اللابتوب المستعمل والجديد بالكامل على نظام ويندوز — تعمل بملف واحد محمول حتى على نسخ الويندوز الخام الجديدة بدون أي برامج خارجية**

---

## 🌟 Highlights & What's New in v3.00 Pro / أبرز مميزات الإصدار 3.00 Pro

- **🎨 Liquid Glass Pro UI & Smooth Micro-Animations:**
  Modern frosted-glass dark interface with glowing radial health gauges, live area sparklines, neon emerald `PASS ✓` and crimson `FAIL ✕` status pills, floating quick-action dock, and studio-grade spatial UI sound effects (`SFX`).
- **📦 100% Zero-Dependency Portable Single-File EXE (Works on Fresh Windows Installs):**
  Bundles the **.NET 8 Desktop Runtime**, **VC++ Runtime DLLs**, **Portable WebView2 Fixed Runtime (`v157.0`)**, 1080p calibration videos/photos, and studio stereo voice WAVs inside a single standalone `SHXTester.exe`. Automatically detects or extracts its built-in engine on brand-new or stripped Windows 10/11 installations offline.
- **⚡ Dynamic Multi-Browser Battery, CPU & RAM Stress Test + Floating Top-Right HUD:**
  - Live **CPU Usage (`%` & `°C`)** and **RAM Consumption (`%` & `Used / Total GB`)** meters inside the Battery Test and on the always-on-top **Floating HUD Bar**.
  - Interactive **Target CPU Load Slider (`10%` – `100%`)**: As you increase the percentage, the test automatically opens **up to 5 real browser windows simultaneously** (`YouTube 4K`, `Wikipedia Live Scroll`, `GitHub Explore`, `YouTube 60FPS`, and `Office 25,000-Cell Live Spreadsheet`) plus multi-threaded CPU/RAM load; as you decrease the percentage (from the slider, presets, or `[ − ] / [ + ]` HUD buttons), it automatically closes excess browsers live.
- **💥 BSOD & Crash History Inspector (`كاشف الشاشات الزرقاء وسجل الأعطال`):**
  Scans Windows Event Logs (`Kernel-Power 41`, `BugCheck 1001`, `EventID 6008`, `WHEA-Logger`, Disk Controller Errors) and `C:\Windows\Minidump` to uncover hidden Blue Screens and sudden shutdowns before buying a used laptop.
- **👆 10-Finger Touchscreen Multi-Touch & Dead-Zone Tester (`اختبار شاشات اللمس المتعدد`):**
  Tracks up to 10 simultaneous touch points with a 24-zone perimeter & dead-zone sweep grid (included in `Full Test`).
- **⌨️ 104-Key Mechanical & Chatter Keyboard Diagnostic Matrix:**
  Full-size visual keyboard layout with live **Key Chatter / Switch Bounce Detection (`< 35 ms`)**, minimum interval telemetry (`ms`), rollover count, and stuck-key warning.
- **📶 Separate Dedicated Wi-Fi & Bluetooth Diagnostic Suites:**
  - **Wi-Fi & Ethernet Suite:** Adapter link speed, live nearby SSID signal scanner, ping latency, and real download bandwidth test.
  - **Bluetooth Suite:** Independent Bluetooth radio controller inspection, paired/linked peripherals audit, Wi-Fi/BT coexistence check, and wireless audio latency test.
- **🖥️ True Fullscreen 3-Suite Display & Dead-Pixel Inspector:**
  Covers 100% of monitor bounds (over the Windows Taskbar) with **Suite 1 (9 Pure Solid Colors)**, **Suite 2 (1080p H.264 Calibration Videos, HDR/SMPTE Reference Photos & Live UFO FPS Tracker)**, and **Suite 3 (Dead-Pixel Flasher, Grid Scanner & Backlight Bleed Maps)**.
- **🔊 Hardware-Isolated Stereo Voice Test & Smart Welcome Greeting (`LOGS`):**
  - Strictly isolated Left (`R=0`), Right (`L=0`), and Center studio voice WAVs in Arabic & English, plus frequency sweep and polarity tests.
  - Automatically logs every tested machine in `LOGS/SHX_Device_Logs.txt` and greets you by voice indicating whether this is a **Brand-New Device (`Launch #1`)** or a **Returning Previously-Tested Device (`Launch #N`)**.
- **📜 Verified Buyer Certificate + Offline QR Code & Export (`PDF / HTML / JSON`):**
  Generates an instant inspection certificate with a scannable offline QR code, executive pass-rate summary, and optional Serial Number masking.

---

## 🛠️ Complete Diagnostic Modules / جميع اختبارات الفحص (25+ اختبار)

| Category | Modules Included |
| :--- | :--- |
| **System & Authenticity** | Hardware Overview, Anti-Fake Detection (WMI vs. SMBIOS/Registry/EDID), BIOS & Security Locks, Windows License & Activation |
| **Stability & Storage** | BSOD & Crash History Inspector, S.M.A.R.T. SSD/NVMe Health & Sequential Read/Write Speed Benchmark, Driver & Startup Audit |
| **Power & Thermals** | Multi-Browser Battery Stress & Drain Estimator, Charger Wattage & Voltage Stability, CPU/GPU Thermal Stress & Throttling |
| **Display & Input** | 3-Suite Fullscreen Display & Dead-Pixel Tester, 10-Finger Touchscreen Multi-Touch Grid, 104-Key Keyboard Chatter Matrix, Touchpad Canvas |
| **Audio, Camera & Ports** | Stereo Voice & Frequency Speaker Test, Microphone Waveform & Recording, Webcam Live Preview, USB Controller & Hot-Plug Monitor, Dedicated Wi-Fi Test, Dedicated Bluetooth Test, Physical Inspection Checklist |

---

## 🚀 Getting Started / طريقة التشغيل

1. Run **`SHXTester.exe`** directly from a USB drive or desktop (requests Administrator privileges so WMI/SMBIOS, S.M.A.R.T., `powercfg`, and Windows Event Logs work with full accuracy).
2. Works out-of-the-box on **Windows 10 & Windows 11 (64-bit)** — including fresh offline Windows installations (automatically uses or extracts its embedded portable WebView2 runtime on first launch).

---

## 📄 License / الرخصة

Released under the **MIT License** — 100% Free & Open Source.
