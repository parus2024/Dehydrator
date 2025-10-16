# ESPHome Dehydrator

This project provides an ESPHome configuration for managing a dehydrator (a device for drying food) based on ESP8266 (ESP-01). The dehydrator uses a DS18B20 temperature sensor, a heater with PWM control, and a variable-speed fan for automatic food drying in a safe mode.

## Description

The dehydrator automatically controls temperature, preventing overheating and ensuring even drying. Key features include:
- **Temperature Monitoring**: Regular temperature readings from the Dallas sensor (update every 5 seconds).
- **Safety**: Automatic heater shutdown if the emergency temperature is exceeded or if the fan is turned off.
- **Automatic Mode**: Scheduled on/off for the heater and fan based on time of day.
- **Customizable Parameters**: Heating level (0-100%), emergency temperature, PWM frequency, fan speed (1-3 levels), on/off times.
- **State Recovery**: The device retains settings after reboot.

The project is based on ESPHome and integrates with Home Assistant via native API for convenient control and monitoring.

## Features

- **Temperature Sensor**: DS18B20 on GPIO1 (OneWire).
- **Heater**: PWM control on GPIO12 with adjustable frequency (1-100 Hz) and power level.
- **Fan**: Speed-controlled fan on GPIO2 with 3 speed levels.
- **Automation**:
  - On/off times (default 00:01 - 07:00).
  - Time range check every 10 seconds in automatic mode.
  - Heater shutdown if fan is off or temperature exceeds limits.
- **HA Settings**: Template components for control (number, select, switch, datetime).
- **Logging**: Detailed logs for debugging in automatic mode.

## Requirements

- **Hardware**:
  - ESP8266 (ESP-01 with 1M flash memory).
  - DS18B20 temperature sensor.
  - Heater and fan with PWM control.
  - Triac BTA-41-600 or another capable of operating with appropriate cooling or without cooling (as in the project).
  - Pins: GPIO1 (sensor), GPIO2 (fan), GPIO12 (heater).
- **Software**:
  - ESPHome (version compatible with the config).
  - Home Assistant for integration.
- **Dependencies**: Included via includes (common.yaml, packages, etc.).

## Installation

1. **Clone the repository** or copy the YAML configuration.
2. **Configure substitutions** (if needed to change IP, pins, etc.):
   - `device_ip`: Device IP address.
   - `name`, `friendly_name`: Names for HA and ESPHome.
3. **Upload the configuration to ESPHome Dashboard**:
   - Create a new project in ESPHome.
   - Paste the YAML and compile/upload to the device.
4. **Integrate into Home Assistant**:
   - Ensure native API is enabled (via `api.yaml`).
   - Restart HA for automatic device discovery.

## Configuration

The main logic is in `dehydrator.yaml`. Key sections:
- **Sensor**: Temperature with filters and safety conditions.
- **Light**: Heater with checks (does not turn on without fan).
- **Number**: Settings for heating level, emergency temperature, PWM frequency.
- **Fan**: Fan with 3 speeds, turns off heater when disabled.
- **Datetime**: On/off times in automatic mode.
- **Switch/Select**: Auto mode toggle and fan speed selection.
- **Interval**: Periodic time check for automation.

For customization, edit the YAML in ESPHome Dashboard and recompile.

## Safety and Debugging

- **Safety**: Heater does not turn on if fan is off or temperature > emergency.
- **Logs**: Debug mode enabled (`logger/debug.yaml`). View logs in ESPHome Dashboard for diagnostics.

## 📊 Screenshots and Videos

*(Add screenshots of the display, HA dashboard, or demonstration videos here)*

- [Firmware yaml file](dehydrator.yaml)
- [Appearance](dehydrator.png)

---

## 📄 License

This project is distributed under the MIT License. Use at your own risk.

---

## Additional Information Sources

Telegram channel https://t.me/parus_smart

---
## 🙏 Acknowledgments

- ESPHome community for the excellent framework.
- Home Assistant for integration.
- You for using it! If the project is helpful, give it a ⭐ on GitHub.

---

*Created with ❤️ ParusSmartHome. Version: 15.10.2025*
