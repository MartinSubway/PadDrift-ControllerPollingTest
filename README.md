<p align="center">
  <img src="https://i.postimg.cc/ZnDSCJtB/banner.png" alt="PadDrift Controller & Mouse Polling Tester — Stick Drift, Circularity & Hz Analyzer" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Gamepad%20%26%20Mouse%20Tester-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-paddrift--test--v1.3-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# PadDrift Controller & Mouse Polling Tester — Stick Drift, Circularity & Hz Analyzer

**Character slowly walking on its own from analog stick drift? Bought a new 4000 Hz or 8000 Hz gaming mouse and want to verify its real USB polling rate and jitter? Test DualSense, Xbox, 8BitDo controllers and gaming mice locally in one portable app.**

PadDrift Controller & Mouse Polling Tester provides raw, unfiltered HID and XInput telemetry on Windows: **visualizing resting stick deadzone drift, outer-ring circularity error percentage, L2/R2 trigger linearity, rumble motor response, and live mouse USB polling rate stability**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) PC gamers** testing new or used controllers (Xbox, PlayStation DualSense/DualShock 4, 8BitDo, Hall Effect pads) and high-polling-rate mice.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Camera or character drifts when thumbs are off the sticks | Worn potentiometer carbon tracks or uncalibrated Hall Effect center | Measure exact resting X/Y axis offset percentage to set deadzones |
| Diagonal movement feels slower than cardinal directions | Squarish outer stick gate causing high circularity error | Run a 360° outer-ring sweep to measure average circularity error % |
| 8000 Hz / 4000 Hz gaming mouse feels inconsistent in-game | USB hub bottleneck or slow hand movement failing to saturate polling | Move mouse rapidly in circles to measure peak and average polling Hz |
| Need to verify a used controller before buying | Sticky face buttons, weak rumble motors, or half-pressing triggers | Test every button, trigger 0–255 range, and left/right vibration motors |

## Download for Windows

[**Download PadDriftTest.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/PadDriftTest.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `PadDriftTest.exe`? (Key features)

- Supports Xbox (XInput), PlayStation DualSense / DualShock 4, Switch Pro, and generic DirectInput/HID pads.
- Displays real-time X/Y coordinates (`-1.000` to `+1.000`), resting drift percentage, and 360° circularity error.
- Tests L2/R2 analog trigger travel (`0%` to `100%`) and triggers low/high-frequency rumble motors.
- Measures live mouse USB polling rate (`125 Hz` to `8000 Hz`) and interval jitter in milliseconds.

### Sample Output

```text
[PadDriftTest] Detected Input Devices on Windows HID / XInput...
[OK]   Controller [0]   : Sony DualSense Wireless Controller (USB Wired)
[INFO] Left Stick Rest  : X = +0.012, Y = -0.008 (1.4% drift — Healthy)
[INFO] Circularity Avg  : 6.8% average outer-ring error
[OK]   Gaming Mouse     : Peak Polling Rate = 3984 Hz (Configured: 4000 Hz | Jitter: 0.04 ms)
```

The release ZIP is named `PadDriftTest.zip`; the Windows executable inside is named `PadDriftTest.exe`.

1. Close PadDrift Test before updating or replacing executable files.
2. Click **Download PadDriftTest.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `PadDriftTest.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit) with USB or Bluetooth controllers / mice connected.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `PadDriftTest.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Knowing exact deadzone values to set in Steam Input or games

Seeing that your left stick rests at `3.2%` offset lets you set a `5%` deadzone instead of a sluggish `15%` default.

### Verifying Hall Effect and TMR stick replacements

Circularity testing confirms whether replacement thumbsticks reach full diagonal corners cleanly.

### Diagnosing USB port bottlenecks on 4K/8K mice

Plugging an 8000 Hz dongle into a front-panel case hub often caps polling at 1000 Hz; live Hz graphs reveal the drop immediately.

### Zero browser throttling

Web-based mouse testers are capped by browser event loops; a native Windows app reads raw `WM_INPUT` HID packets accurately.

## Default folders and configuration paths

PadDrift Test runs as a standalone portable executable with zero installation or drivers:

```text
Portable (No AppData files required)
```

Typical directory layout:

```text
PadDriftTest.exe
├── Controller Tab : Live Stick Radar + Circularity % + Trigger Bars + Rumble
└── Mouse Tab      : Raw WM_INPUT Polling Rate (Hz) + Interval Jitter Graph
```

For accurate 4000 Hz / 8000 Hz mouse readings, move the mouse continuously in wide circles so the sensor generates maximum report packets.

## Quick start guide

Follow these steps to get started:

1. **Extract `PadDriftTest.zip` and launch `PadDriftTest.exe`.** Connect your controller via USB or Bluetooth.
2. **Leave both thumbsticks untouched for 3 seconds to read resting drift.** Note the X/Y percentage offset.
3. **Rotate each thumbstick smoothly around the outer edge.** Review the circularity error percentage.
4. **Switch to the **Mouse Polling** tab and move your mouse in circles.** Verify your mouse reaches its rated 1000 / 4000 / 8000 Hz.

### Data safety note

PadDrift Test reads raw Windows HID/XInput state in read-only mode without installing virtual drivers.

## What the status summary shows

PadDrift Test displays **controller model, X/Y resting drift %, circularity error %, trigger range, and mouse peak/average polling Hz**.

## FAQ

**Why do browser polling rate testers cap at 1000 Hz or 2000 Hz?**

Web browsers throttle mousemove events to the display refresh rate or sandbox timers; native Windows Raw Input (`WM_INPUT`) reads true 4000–8000 Hz USB packets.

**Does PadDrift Test work with PlayStation DualSense controllers?**

Yes—it reads both XInput (Xbox) and HID (DualSense, DualShock 4, 8BitDo) controllers.

**What is a good circularity error percentage?**

Stock Xbox/PS5 controllers typically score 7%–11%, while calibrated Hall Effect sticks score under 5%.

## Useful reading

- [Microsoft Docs — Raw Input (WM_INPUT) Overview](https://learn.microsoft.com/en-us/windows/win32/inputdev/raw-input)

## More Windows Desktop Utilities

- [WinTimer-LatencyDoctor](../WinTimer-LatencyDoctor) — Windows gaming latency, Ultimate Performance & timer check
- [AudioSwitch-HotkeyToggle](../AudioSwitch-HotkeyToggle) — One-key headphones, speakers & microphone switcher
- [SoundDeck-MicSoundboard](../SoundDeck-MicSoundboard) — Lightweight virtual-mic soundboard for Discord, OBS & voice chat
- [Win11-GamingDebloatGuard](../Win11-GamingDebloatGuard) — Windows 11 gaming optimizer & background process cleaner

*Independent open-source desktop utility for Windows.*
