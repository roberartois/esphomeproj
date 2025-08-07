# ESP8266 Water Heater Controller

## 🇬🇧 English

### 🔧 Features
- Dual relay control for heating stages (GPIO16 & GPIO12)
- Temperature monitoring via DS18B20 on GPIO14
- OLED display with multiple pages and auto-dimming
- Two physical buttons for menu navigation and temperature adjustment
- Configurable target and one-heater temperature thresholds
- Automatic heater logic based on current temperature
- OTA updates via ESPHome
- Home Assistant API integration
- Free heap memory monitoring

---

### 🔌 Wiring Overview

| Function                  | GPIO | Notes                                 |
|---------------------------|------|----------------------------------------|
| Relay 1 & 2               | 16   | Active HIGH at boot                   |
| Relay 3 & 4               | 12   |                                        |
| DS18B20 (1-Wire)          | 14   |                                        |
| Button NEXT               | 2    | INPUT_PULLUP, boot-sensitive          |
| Button UP                 | 0    | INPUT_PULLUP, boot-sensitive          |
| OLED SDA                  | 4    | I²C                                    |
| OLED SCL                  | 5    | I²C                                    |

---

### 📦 Installation

1. Install [ESPHome](https://esphome.io/) via CLI or Dashboard.
2. Clone this repository and place the YAML file in your ESPHome config directory.
3. Create a `secrets.yaml` file with your credentials:
   ```yaml
   wifi_ssid: "YourSSID"
   wifi_password: "YourPassword"
   ota_password_esp8266-water-heater: "YourOTAPassword"
   ```
4. Flash the firmware via USB:
   ```
   esphome run esp8266-water-heater.yaml
   ```
5. After boot, the device will connect to Wi-Fi and be available at `esp8266-water-heater.local`.

---

### ⚙️ Components

- **Sensor**: DS18B20 temperature sensor
- **Switches**: Two GPIO-controlled relays
- **Buttons**: NEXT and UP for UI navigation
- **Display**: SSD1306 128×32 OLED via I²C
- **Globals**: Stores temperature thresholds and UI state
- **Scripts**:
  - `heater_control_script`: Controls relays based on temperature
  - `show_info_page_script`: Displays heating status briefly
- **Numbers**: Home Assistant entities for temperature adjustment
- **Intervals**: Periodic updates and display dimming logic

---

### 🧠 How It Works

- The device reads water temperature every 120 seconds.
- The OLED shows:
  - Page 1: Current temperature + relay status
  - Page 2: Target temperature
  - Page 3: One-heater threshold
  - Info page: Heating ON/OFF status
- Buttons allow page switching and temperature adjustment.
- Heating logic:
  - If temp > target → both relays OFF
  - If temp between one-heater and target → relay 3&4 ON
  - If temp ≤ one-heater → both relays ON
- Display dims after 30s inactivity, clears after 60s.

---

## 🇺🇦 Українською

### 🔧 Можливості
- Керування двома реле для ступеневого нагріву (GPIO16 та GPIO12)
- Вимірювання температури через DS18B20 (GPIO14)
- OLED-дисплей з кількома сторінками та автоматичним затемненням
- Дві фізичні кнопки для навігації та зміни параметрів
- Налаштовувані пороги температури
- Автоматична логіка нагріву залежно від температури
- OTA-оновлення через ESPHome
- Інтеграція з Home Assistant API
- Моніторинг вільної пам’яті

---

### 🔌 Схема підключення

| Функція                   | GPIO | Примітки                              |
|---------------------------|------|----------------------------------------|
| Реле 1 та 2               | 16   | Активний HIGH при завантаженні        |
| Реле 3 та 4               | 12   |                                        |
| DS18B20 (1-Wire)          | 14   |                                        |
| Кнопка NEXT               | 2    | INPUT_PULLUP, чутлива до BOOT         |
| Кнопка UP                 | 0    | INPUT_PULLUP, чутлива до BOOT         |
| OLED SDA                  | 4    | I²C                                    |
| OLED SCL                  | 5    | I²C                                    |

---

### 📦 Інсталяція

1. Встановіть [ESPHome](https://esphome.io/) через CLI або Dashboard.
2. Клонуйте репозиторій і помістіть YAML-файл у конфігураційну директорію ESPHome.
3. Створіть файл `secrets.yaml` з вашими даними:
   ```yaml
   wifi_ssid: "ВашSSID"
   wifi_password: "ВашПароль"
   ota_password_esp8266-water-heater: "ВашOTAпароль"
   ```
4. Прошивка через USB:
   ```
   esphome run esp8266-water-heater.yaml
   ```
5. Після завантаження пристрій підключиться до Wi-Fi і буде доступний за адресою `esp8266-water-heater.local`.

---

### ⚙️ Складові

- **Сенсор**: DS18B20
- **Реле**: GPIO-керовані виходи
- **Кнопки**: NEXT і UP для навігації
- **Дисплей**: SSD1306 OLED 128×32 через I²C
- **Глобальні змінні**: зберігають пороги температури та стан UI
- **Скрипти**:
  - `heater_control_script`: керує реле залежно від температури
  - `show_info_page_script`: коротке відображення статусу нагріву
- **Числові регулятори**: сутності Home Assistant для налаштування температури
- **Інтервали**: періодичне оновлення та логіка затемнення дисплея

---

### 🧠 Основні принципи роботи

- Пристрій зчитує температуру води кожні 120 секунд.
- OLED-дисплей показує:
  - Сторінка 1: поточна температура + статус реле
  - Сторінка 2: цільова температура
  - Сторінка 3: поріг одного нагрівача
  - Інфо-сторінка: статус нагріву ON/OFF
- Кнопки дозволяють перемикати сторінки та змінювати параметри.
- Логіка нагріву:
  - Якщо температура > цільової → обидва реле вимкнено
  - Якщо температура між порогом і цільовою → реле 3&4 увімкнено
  - Якщо температура ≤ порогу → обидва реле увімкнено
- Дисплей затемнюється після 30 с бездіяльності, очищується через 60 с.

---

© 2025 Ievgen Gubareni. License: MIT.
