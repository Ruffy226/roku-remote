# ESPHome Roku Remote

A physical remote control for Roku devices using ESP32-S3 with a 2.4" TFT touchscreen.

## Hardware

- **MCU**: ESP32-S3 N16R8 (16MB flash, 8MB PSRAM)
- **Display**: 2.4" TFT LCD Shield with ST7789V driver (240x320)
- **Touch**: XPT2046 resistive touchscreen (integrated with display shield)
- **Target**: Roku device via ECP API (network)

## Features

- D-pad navigation (Up, Down, Left, Right, Select)
- Home, Back, Play/Pause, Power buttons
- Volume Up/Down (via Home Assistant buttons)
- Touch-responsive UI
- Status LED for connectivity feedback
- Optional deep sleep for battery power

## Wiring (ESP32-S3 DevKitC-1)

| Pin | Function |
|-----|----------|
| GPIO18 | SPI CLK |
| GPIO23 | SPI MOSI |
| GPIO19 | SPI MISO |
| GPIO5  | Display CS |
| GPIO4  | Display DC |
| GPIO22 | Display Reset |
| GPIO21 | Touch CS |
| GPIO27 | Touch IRQ |
| GPIO48 | Status LED (built-in, inverted) |

## Setup

1. Copy `secrets.yaml.example` to `secrets.yaml` and fill in your credentials
2. Update the `roku_ip` substitution to match your Roku device
3. Compile and flash via ESPHome dashboard or CLI:
   ```bash
   esphome run roku-remote.yaml
   ```

## Roku ECP API

This remote uses Roku's External Control Protocol (ECP) which allows HTTP POST requests to control the device:

```
POST http://<roku-ip>:8060/keypress/<button>
```

No authentication required — just need the Roku's IP address.

## Home Assistant Integration

The device exposes all buttons as native ESPHome entities, so once added to Home Assistant you can:
- Automate button presses
- Create scripts combining multiple actions
- Use volume buttons that aren't on the touchscreen UI

## License

MIT
