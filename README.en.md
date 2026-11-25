# Baiqin LAN Remote Control (LAN Remote Control Web Service)

#### Description

A LAN remote control tool that runs on Windows. Once the service is started on
the controlled machine, no client software is needed on the controller side —
just open a browser on any phone, tablet, or PC and navigate to the controlled
machine's IP to screen-share, control mouse/keyboard, transfer files, and launch
programs remotely.

- Author: Personal Studio
- License: Non-commercial personal use only
- Platform: Windows 10 / 11 x64
- Default console port: 7281

#### Software Architecture

The launcher starts a set of child processes:

| Module | Role |
|---|---|
| LANRemoteControlWebService.exe | Main web backend, serves the browser console |
| LANFileShareSvc.exe | File sharing service (upload / download / search) |
| BaiqinLANRemoteControlMaster2.exe | Tray GUI on the controlled machine |
| BaiqinDynamicImageLibrary.exe | Screen capture and JPEG encoding |
| BaiqinProcessManagement.exe | Process list and kill |
| BaiqinKeyboardLogger.exe | Keystroke log (can be disabled in settings) |
| LANRemoteWallpaperServer.exe | Remote wallpaper setter |
| BaiqinMacroRecord.dll | Keyboard/macro recorder (with audio sample) |
| BaiqinRegeditPage.dll | Remote registry editor |

Feature modules are shipped as plugin DLLs, each exposing Init / GetPage / Api,
and are mounted by the main web service as separate web routes.

#### Installation

1. Download `LANRemoteControlWebServiceSetupVx.xx.exe` from [Releases](releases)
2. Run the installer on the controlled Windows 10/11 x64 machine and follow the prompts
3. Start "局域网远控神器" and click **Start Service**
4. Once the log shows "service started", note the machine's LAN IP (e.g. 192.168.1.3)

> If your antivirus flags it, add the install folder to the whitelist.

#### Instructions

1. On any device in the same LAN, open `http://<controlled-IP>:7281/`
2. The home screen shows the live desktop; use the on-screen virtual mouse/keys to control it
3. File manager: open `http://<controlled-IP>:7283/` to upload, download, or search files
4. Use the "Run EXE" page to launch programs remotely; use the process page to kill tasks
5. The Settings page lets you change ports, JPEG quality, frame rate, and upload limits

#### Features

- Real-time screen streaming (JPEG, ~20 fps)
- Remote mouse / keyboard, clipboard sync
- File upload (chunked), download, full-disk search
- Remote EXE launch, remote process kill
- Remote registry editing, remote wallpaper change
- Macro recording and playback, controlled-side audio playback
- Session popup notifications, one-click suspend protection

#### Default Ports

| Port | Purpose |
|---|---|
| 7281 | Web console |
| 7283 | File sharing |
| 7299 | Control channel |

#### Security Notes

- The service binds to 0.0.0.0 with **no access password** by default; use only on a trusted LAN
- Do **not** expose ports 7281 / 7283 / 7299 to the public internet
- Keystroke logging and remote execution are on by default; disable them in Settings if not needed
- Only deploy on machines you own or are explicitly authorized to manage

#### Contribution

1. Fork the repository
2. Create a Feat_xxx branch
3. Commit your changes
4. Open a Pull Request
