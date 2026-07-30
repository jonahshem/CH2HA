# Crestron Home for Home Assistant

A custom Home Assistant integration for Crestron Home OS processors, plus optional support for Crestron PC-350V series PDUs (power distribution units).

Every endpoint, field name, and command in this integration was verified against real captured traffic (curl tests against the official REST API, and browser DevTools captures of WebSocket traffic for the PDU) rather than assumed from documentation alone, since Crestron's public docs and actual firmware behavior frequently disagree.

## Features

**Crestron Home processor:**
- Lights (dimmers)
- Shades/covers
- Thermostats (climate)
- Door locks
- Scenes
- Relay/gate/generic I/O controls (exposed as buttons)
- Occupancy, motion, door, and window sensors (binary sensors)
- Media room status (read-only)
- Automatic Home Assistant Area creation matching your Crestron rooms

**PC-350 PDU (optional, supports multiple units):**
- Per-outlet on/off switches (only for outlets configured with full control)
- Per-outlet power cycle buttons (available on all outlets, including "power cycle only" configured outlets)
- Reset Voltage Protection, Reboot, and combined Reset & Reboot buttons
- Live push-based state updates over WebSocket (no polling)
- Automatic reconnection with backoff if the connection drops
- Over/under voltage, over current, wiring fault, and surge protection binary sensors

## Installation

### Via HACS (recommended)
1. HACS → Integrations → ⋮ (top right) → Custom repositories
2. Add this repository's URL, category: Integration
3. Search for "Crestron Home" in HACS and install
4. Restart Home Assistant

### Manual
1. Copy `custom_components/crestron_home/` into your Home Assistant `config/custom_components/` folder
2. Restart Home Assistant

## Configuration

Settings → Devices & Services → Add Integration → Crestron Home

You'll need:
- Your Crestron Home processor's IP address
- A Crestron Home API token (generated via the Crestron Home Setup app)

PDUs are optional and configured afterward via the integration's "Configure" menu, which supports adding/removing any number of PDUs.

## Known limitations

- `alarm_control_panel.py` is present but **unverified** - it was written against a system with no security panel attached (`GET /securitydevices` always returned empty), so the endpoint/field names have never been tested against a real panel. Verify before relying on it.
- Media room control is read-only. A write endpoint may exist but was never found in Crestron's public API documentation.

## Disclaimer

This is an unofficial, community-built integration. It is not affiliated with or endorsed by Crestron Electronics, Inc.
