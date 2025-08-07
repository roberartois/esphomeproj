# ESP32C3sm TestBoard Boiler Controller

## English

### Overview
This project turns an ESP32-C3 Super Mini board into a smart water-heater controller using ESPHome. It provides:
- Dallas temperature sensing (DS18B20) on GPIO7  
- Dual-relay control (GPIO5 & GPIO6)  
- Two buttons for menu navigation and parameter adjustment (GPIO4 & GPIO3)  
- 128×32 OLED display with multiple pages and automatic dimming  
- Global settings for target and one-heater temperatures  
- Heater logic script for automatic relay switching  
- MQTT integration with Home Assistant discovery, birth/will messages, logs  
- Dual OTA support (ESPHome API + web_server)  
- Wi-Fi captive portal fallback

### Features
- Temperature reading every 120 s  
- Menu-driven UI:  
  - Page 1: Current temp + relay status  
  - Page 2: Target temperature  
  - Page 3: One-heater temperature threshold  
  - Info page on switch toggle  
- Buttons:  
  - **NEXT** (GPIO4): Cycle display pages or wake display from dimmed state  
  - **UP** (GPIO3):  
    - Page 0: Toggle Heating switch  
    - Page 1: Increment target temp (25–85 °C step 5)  
    - Page 2: Increment one-heater temp (25–85 °C step 5)  
- Scripts:  
  - `heater_control_script`: Automatic relay control based on current, target, one-heater temps  
  - `show_info_page_script`: Temporarily show the info page, then return
- Automatic display dimming after 30 s inactivity and clear after 60 s  
- MQTT topics under customizable prefix (default via `secrets.yaml`)  
- Home Assistant MQTT Discovery

### Hardware & Pinout

| Signal                   | ESP32-C3 GPIO |
|--------------------------|--------------:|
| Button NEXT              | GPIO4         |
| Button UP                | GPIO3         |
| I²C SDA                  | GPIO8         |
| I²C SCL                  | GPIO9         |
| 1-Wire (DS18B20)         | GPIO7         |
| Relay 1 & 2              | GPIO6         |
| Relay 3 & 4              | GPIO5         |

### Installation

1. Install ESPHome (CLI or Dashboard).  
2. Clone this repository.  
3. Create `secrets.yaml` in the same folder:
   ```yaml
   mqtt_broker: "192.168.1.100"
   mqtt_port: 1883
   mqtt_user: "esp_boiler"
   mqtt_pwd: "your_mqtt_password"
   ota_password: "your_ota_password"
   wifi_ssid: "YourSSID"
   wifi_password: "YourWiFiPass"
   ```
4. Adjust `esphome/esp32c3sm-testboard.yaml` if needed.  
5. Compile & upload via USB:
   ```
   esphome run esp32c3sm-testboard.yaml
   ```
6. Upon boot, captive portal will start if Wi-Fi fails.  

### MQTT Integration

- **Discovery prefix**: `homeassistant` (configurable)  
- **Birth/will**:  
  - `myavailability/topic`: `online` / `offline`  
- **Auto-discovered entities**:  
  - Sensor: `water_heater_temperature`  
  - Switches: `relay_3_4`, `relay_1_2`, `heating_on_off`  
  - Numbers: `wanted_temperature`, `one_heater_temperature`  
  - Buttons: `restart_board`  
- **Logs**: published to `homeassistant/<device>/log`  

### Usage

- Use Home Assistant UI or MQTT to toggle heating, adjust temps, read sensor.  
- Display cycles pages via NEXT button; UP button edits values.  
- Automatic dimming conserves power.

---

## Українською

### Опис
Проєкт перетворює ESP32-C3 Super Mini на «розумний» контролер бойлера з ESPHome. Особливості:
- Датчик температури Dallas (DS18B20) на GPIO7  
- Керування двома реле (GPIO5 та GPIO6)  
- Дві кнопки для навігації меню й налаштувань (GPIO4 та GPIO3)  
- OLED-дисплей 128×32 з кількома сторінками та автоматичним затемненням  
- Глобальні змінні для цільової температури та порогу для одного нагрівача  
- Логіка скрипту для автоматичного вмикання/вимикання реле  
- Інтеграція з MQTT та Home Assistant Discovery, повідомлення про народження/смерть, логи  
- Два способи OTA (ESPHome API та web_server)  
- Резервна точка доступу (captive portal)

### Можливості
- Зняття температури кожні 120 с  
- UI-меню:  
  - Сторінка 1: Поточна температура + статус реле  
  - Сторінка 2: Цільова температура  
  - Сторінка 3: Температура одного нагрівача  
  - Інфо-сторінка на перемиканні  
- Кнопки:  
  - **NEXT** (GPIO4): Перемикає сторінки дисплея або повертає з затемненого стану  
  - **UP** (GPIO3):  
    - При позиції 0: перемикає Heating On/Off  
    - При позиції 1: циклічно збільшує цільову температуру (25–85 °C крок 5)  
    - При позиції 2: циклічно збільшує температуру одного нагрівача (25–85 °C крок 5)  
- Скрипти:  
  - `heater_control_script`: Автоматичне керування реле за температурою  
  - `show_info_page_script`: Тимчасове відображення інфо-сторінки  
- Дисплей затемнюється через 30 с без активності та очищується через 60 с  
- MQTT підключення з гнучкою настройкою через `secrets.yaml`  
- Автоматичне виявлення у Home Assistant (Discovery)

### Апаратура та розводка

| Сигнал                   | ESP32-C3 GPIO |
|--------------------------|--------------:|
| Button NEXT              | GPIO4         |
| Button UP                | GPIO3         |
| I²C SDA                  | GPIO8         |
| I²C SCL                  | GPIO9         |
| 1-Wire (DS18B20)         | GPIO7         |
| Relay 1 & 2              | GPIO6         |
| Relay 3 & 4              | GPIO5         |

### Встановлення

1. Встановіть ESPHome (CLI або Dashboard).  
2. Клонуйте репозиторій.  
3. Створіть `secrets.yaml` поруч з `esp32c3sm-testboard.yaml`:
   ```yaml
   mqtt_broker: "192.168.1.100"
   mqtt_port: 1883
   mqtt_user: "esp_boiler"
   mqtt_pwd: "your_mqtt_password"
   ota_password: "your_ota_password"
   wifi_ssid: "YourSSID"
   wifi_password: "YourWiFiPass"
   ```
4. За потреби відредагуйте `esp32c3sm-testboard.yaml`.  
5. Скомпілюйте й завантажте прошивку через USB:
   ```
   esphome run esp32c3sm-testboard.yaml
   ```
6. При помилці Wi-Fi активується точка доступу для налаштування.

### Інтеграція MQTT

- **Discovery prefix**: `homeassistant` (за замовчуванням)  
- **Повідомлення про статус**:  
  - `myavailability/topic`: `online` / `offline`  
- **Автоматично створювані сутності**:  
  - Сенсор: `water_heater_temperature`  
  - Реле: `relay_3_4`, `relay_1_2`, `heating_on_off`  
  - Числові регулятори: `wanted_temperature`, `one_heater_temperature`  
  - Кнопка: `restart_board`  
- **Логи**: публікуються в `homeassistant/<device>/log`  

### Використання

- Керуйте нагрівом, корегуйте температуру в Home Assistant або через MQTT.  
- Кнопками змінюйте сторінки дисплея й налаштовуйте параметри.  
- Дисплей автоматично затемнюється для економії енергії.  

---

© 2025 Ievgen Gubareni. License: MIT.
