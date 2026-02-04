# KingKiosk Feature Server - Home Assistant Add-on

KingKiosk Feature Server is a high-performance media kiosk platform providing WebRTC media streaming, remote browser control, and AI-powered quality monitoring.

## Features

- **WebRTC Media Server** - Real-time audio/video communication
- **Remote Browser Control** - Control remote browser sessions
- **AI Analysis** - Object detection, speech-to-text, quality monitoring
- **Home Assistant Integration** - MQTT discovery, entity exposure

## Configuration

### Basic Options

| Option | Description | Default |
|--------|-------------|---------|
| `server_port` | HTTP/WebSocket port | `4000` |

### MQTT Options

| Option | Description | Default |
|--------|-------------|---------|
| `mqtt_enabled` | Enable MQTT integration | `true` |
| `mqtt_discovery_prefix` | Home Assistant discovery prefix | `homeassistant` |

MQTT broker connection is automatically discovered from Home Assistant.

### Media Options

| Option | Description | Default |
|--------|-------------|---------|
| `announced_ip` | Public IP for WebRTC media (leave empty for auto) | `` |
| `go2rtc_url` | go2rtc RTSP base URL for RTSP export (e.g. `rtsp://192.168.0.199:8554`) | `` |
| `go2rtc_api_url` | go2rtc HTTP API base URL (e.g. `http://192.168.0.199:1984`) | `` |

Set this to your server's public IP if clients are connecting from outside your local network.

### Browser Options

| Option | Description | Default |
|--------|-------------|---------|
| `browser_enabled` | Enable browser sessions | `true` |
| `browser_max_sessions` | Maximum concurrent browser sessions | `5` |

### ML Options

| Option | Description | Default |
|--------|-------------|---------|
| `ml_quality_detection` | Enable ML quality monitoring and detection | `false` |

**Note:** ML models must be placed in `/share/kingkiosk/models/` before enabling. Includes video/audio quality analysis and object detection.

### Home Assistant Bridge

| Option | Description | Default |
|--------|-------------|---------|
| `ha_bridge_enabled` | Enable HA entity bridge via MQTT | `true` |

## Network Configuration

The add-on uses **host networking** for WebRTC RTP traffic. Ensure the following ports are available:

| Port | Protocol | Purpose |
|------|----------|---------|
| 4000 | TCP | HTTP/WebSocket |
| 8554 | TCP | RTSP streaming |
| 40000-40100 | UDP | RTP media |

## Hardware Acceleration

The add-on automatically detects and uses available hardware video encoding:

- **Intel** - VAAPI with Intel Media Driver
- **AMD** - VAAPI with Mesa drivers
- **NVIDIA** - NVENC (requires nvidia-container-toolkit on host)

Ensure `/dev/dri` is available for GPU acceleration.

## Data Storage

| Path | Purpose |
|------|---------|
| `/data/kingkiosk/` | Add-on persistent data |
| `/share/kingkiosk/recordings/` | Video recordings |
| `/share/kingkiosk/models/` | AI model files |

## Ingress

The add-on supports Home Assistant Ingress. Access the web interface directly from the sidebar.

## Support

- [GitHub Issues](https://github.com/ajarsm/kingkiosk-ha-addon/issues)
