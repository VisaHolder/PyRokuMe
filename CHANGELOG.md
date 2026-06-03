# Changelog

All notable changes to PyRokuMe are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] - 2026-06-03

### Fixed
- **"Show window" from the already-running prompt spawned a phantom white box with its own taskbar button.** Surfacing the existing instance used raw Win32 `ShowWindow` on *every* top-level window owned by that process, which also revealed Tk's hidden helper window (it has no `WS_EX_TOOLWINDOW`, so it grabbed a taskbar button and rendered as an undrawn white rectangle). The second launch now drops a small signal file and the running instance restores *itself* through Tk, keeping Tk and Win32 in sync — no phantom window, no stray taskbar button.
- **Double-clicking the tray icon would hide the window instead of reopening it.** The tray handler fired the show/hide toggle on both `WM_LBUTTONUP` and `WM_LBUTTONDBLCLK`, so a normal double-click toggled an even number of times and ended up back hidden. The toggle is now debounced and a tray click reliably surfaces the window.

### Changed
- Restoring the window (from the tray or a second launch) now re-stamps `WS_EX_TOOLWINDOW` so the remote stays out of the taskbar and Alt+Tab after being shown.
- The `show` signal file is cleared on startup and on quit so no stale request is left behind.

## [1.0.0]

### Added
- Initial release: single-file Roku remote with SSDP + IP-range auto-discovery, full button layout, remappable keyboard shortcuts, app launcher, input switcher, send-text, Wake-on-LAN, now-playing status, system tray, multi-device quick-switch, 6 themes, opacity, always-on-top, auto-reconnect, and portable/standard config modes.

[1.0.1]: https://github.com/reaprrr/PyRokuMe/releases/tag/v1.0.1
[1.0.0]: https://github.com/reaprrr/PyRokuMe/releases/tag/v1.0.0
