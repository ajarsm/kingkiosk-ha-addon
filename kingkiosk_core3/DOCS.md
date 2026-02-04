# KingKiosk Core 3 - Home Assistant Add-on

KingKiosk Core 3 is a high-performance media kiosk platform providing WebRTC media streaming, remote browser control, and AI-powered quality monitoring.

## Features

- **WebRTC Media Server** - Real-time audio/video communication via mediasoup
- **Remote Browser Control** - Control headless Chromium sessions via CDP
- **AI Analysis** - Object detection, speech-to-text, quality monitoring
- **Home Assistant Integration** - MQTT discovery, entity exposure

## Configuration

### Basic Options

| Option | Description | Default |
|--------|-------------|---------|
| `log_level` | Logging verbosity (trace/debug/info/warn/error) | `info` |
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

## WebSocket API

Connect to `ws://<host>:4000/ws` for signaling. The API follows the same protocol as KingKiosk Core 2 (Node.js version).

### Example: Create Browser Session

```json
{
  "request": "createBrowserSession",
  "id": "req-123",
  "data": {
    "url": "https://example.com",
    "width": 1280,
    "height": 720
  }
}
```

## Ingress

The add-on supports Home Assistant Ingress. Access the web interface directly from the sidebar.

## Troubleshooting

### Browser sessions not working

1. Check Xvfb is running: Look for "Starting Xvfb" in logs
2. Ensure `browser_enabled` is `true`
3. Check available memory (each session needs ~200MB)

### WebRTC not connecting

1. Set `announced_ip` to your server's public IP
2. Ensure RTP port range (40000-40100) is open in your firewall
3. Check for NAT/port forwarding issues

### ML models not loading

1. Place model files in `/share/kingkiosk/models/`
2. Check file permissions
3. Ensure `ml_quality_detection` is enabled

### MQTT not connecting

1. Verify Mosquitto add-on is running
2. Check MQTT discovery is working
3. Review logs for connection errors

## Support

- [GitHub Issues](https://github.com/anthropics/kingkiosk-core3/issues)
- [Documentation](https://github.com/anthropics/kingkiosk-core3)
