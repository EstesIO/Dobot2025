
# OTA and MQTT Setup for Robot Panel

## ESPHome OTA Flashing

1. Install ESPHome on your system:
   ```bash
   pip install esphome
   ```

2. Connect ESP32 via USB, then run:
   ```bash
   esphome run esphome.yaml
   ```

3. After first flash, OTA will be available wirelessly.

## MQTT Setup on Windows

1. Install Mosquitto from https://mosquitto.org/download/
2. Edit `mosquitto.conf` to set listener and auth:
   ```
   listener 1883
   allow_anonymous false
   password_file passwords.txt
   ```

3. Create a password file:
   ```bash
   mosquitto_passwd -c passwords.txt mqtt_user
   ```

4. Start the broker:
   ```bash
   mosquitto -c mosquitto.conf
   ```

## Node-RED

1. Add `mqtt in` nodes for:
   - `robot/start`
   - `robot/stop`
   - `robot/manual`
   - `robot/estop`

2. Connect to Mosquitto broker with correct credentials.

3. Use `debug` or `exec` nodes to control your robot.
