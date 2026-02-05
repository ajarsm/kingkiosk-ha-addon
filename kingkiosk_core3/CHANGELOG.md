# Changelog

All notable changes to the KingKiosk Feature Server Home Assistant Add-on will be documented in this file.

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
