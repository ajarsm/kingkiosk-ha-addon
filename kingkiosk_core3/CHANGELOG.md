# Changelog

All notable changes to the KingKiosk Feature Server Home Assistant Add-on will be documented in this file.

## [1.0.110] - 2026-02-10

### Changed

- Published updated amd64 and aarch64 images for release `1.0.110`.
- Completed distributed build from the same pinned commit for both architectures and republished GHCR `latest` tags.

## [1.0.109] - 2026-02-09

### Changed

- Published updated amd64 and aarch64 images for release `1.0.109`.
- Switched distributed release publish flow to keep Intel on native amd64 and avoid accidental emulated aarch64 remote builds.
- Added release cleanup guidance for pruning old distributed artifacts and Docker builder/image caches on both machines.

## [1.0.107] - 2026-02-09

### Changed

- Published updated amd64 and aarch64 images for release `1.0.107`.
- Updated distributed build flow to enforce bundled King Admin UI for both architectures.
- Added distributed build cleanup hooks to reclaim Docker/image disk space after artifact collection.

## [1.0.106] - 2026-02-09

### Changed

- Published updated amd64 and aarch64 images for release `1.0.106`.
- Bumped add-on metadata version so Home Assistant can surface the upgrade.

## [1.0.105] - 2026-02-08

### Added

- Offline license validation and management support.
- Face recognition and named-person event support for AI detections.
- Add-on documentation for available Piper voices.

### Changed

- Updated Home Assistant ingress and text-to-speech integration flow.
- Improved add-on packaging to prebuild King Admin web assets once and reuse them across both architectures.
- Refreshed the dual-architecture publish runbook and release steps.
- Tuned remote object and face detection cadence for steadier updates.

### Fixed

- Stream ingest changes now apply cleanly without requiring a manual add-on restart.
- Improved health endpoint behavior and startup robustness.
- Removed invalid service wiring from the add-on image to reduce startup errors.
- Improved ARM full-feature build compatibility.

## [1.0.90] - 2026-02-06

### Fixed

- Resolved remote-browser right-edge clipping by enforcing Chromium window sizing to match the Xvfb capture viewport.
- Published updated images for both amd64 and aarch64 with the browser sizing fix.

## [1.0.89] - 2026-02-05

### Changed

- Version now tracks the git build number (`MAJOR.MINOR.<git commit count>`) and matches the GHCR image tags.
- Published updated images for both amd64 and aarch64.

## [1.0.0] - 2025-01-28

### Added

- Initial Home Assistant Add-on release
- WebRTC media server
- Remote browser control
- SIP/VoIP gateway support
- AI features (object detection, transcription, quality monitoring)
- Home Assistant MQTT discovery
- Ingress support for web UI
- Hardware video acceleration (Intel VAAPI, AMD, NVIDIA NVENC)
- Multi-architecture support (amd64, aarch64)

### Configuration Options

- Basic server settings (port, logging)
- MQTT integration with auto-discovery
- WebRTC media settings
- Browser session limits
- SIP gateway configuration
- AI model paths and toggles
- Home Assistant bridge settings
