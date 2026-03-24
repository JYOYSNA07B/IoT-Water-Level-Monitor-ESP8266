# IoT Water Level Monitoring System with AI

An automated smart water tank management system built on the **NodeMCU ESP8266** that monitors water levels in real time using an ultrasonic sensor, automatically controls a water pump, and streams live data to the **Blynk** mobile app — all without human intervention.

---

## 📌 Features

- 📡 Real-time water level monitoring via ultrasonic sensor
- 🔁 Automatic pump ON/OFF based on water level thresholds
- 📱 Remote monitoring through the Blynk 2.0 mobile app
- 💡 LED indicator for pump status (Virtual Pin V2)
- 📊 Live distance/level data pushed to Blynk gauge (Virtual Pin V1)
- ☁️ Cloud-connected via Wi-Fi using ESP8266

---

## 🧰 Hardware Requirements

| Component              | Quantity | Approx. Price (₹) |
|------------------------|----------|-------------------|
| NodeMCU ESP8266        | 1        | ₹330              |
| Ultrasonic Sensor HC-SR04 | 1     | ₹90               |
| Breadboard             | 1        | ₹90               |
| Connecting Wires       | —        | ₹40               |
| Mini LED               | 1        | ₹20               |
| **Total**              |          | **₹570**          |

> A 5V relay module is recommended if you wish to control an actual water pump.

---

## 💻 Software Requirements

- [Arduino IDE](https://www.arduino.cc/)
- [Blynk 2.0](https://blynk.io/)
- ESP8266 Board Package for Arduino IDE
- Libraries: `ESP8266WiFi.h`, `BlynkSimpleEsp8266.h`

---

## 🔌 Pin Configuration

| NodeMCU Pin | Connected To         |
|-------------|----------------------|
| D4          | Motor / Relay IN     |
| D5          | Ultrasonic TRIG      |
| D6          | Ultrasonic ECHO      |
| V1 (Virtual)| Blynk Gauge (Level)  |
| V2 (Virtual)| Blynk LED Indicator  |

---

## ⚙️ How It Works

1. The ultrasonic sensor emits a pulse and measures the echo return time.
2. Distance to the water surface is calculated using:
   ```
   distance = 0.0343 × (timedelay / 2)
   ```
3. Water level = `tank_height (30 cm) - measured_distance`
4. **If water level < 5 cm** → Pump turns **ON**, LED turns **ON**
5. **If water level > 25 cm** → Pump turns **OFF**, LED turns **OFF**
6. Level data is continuously sent to the Blynk app via Virtual Pin V1.

---

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/IoT-Water-Level-Monitor-ESP8266.git
cd IoT-Water-Level-Monitor-ESP8266
```

### 2. Configure Credentials

Open `water_level_monitor.ino` and update the following:

```cpp
#define BLYNK_TEMPLATE_ID   "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "YOUR_TEMPLATE_NAME"
#define BLYNK_AUTH_TOKEN    "YOUR_AUTH_TOKEN"

char ssid[] = "YOUR_WIFI_SSID";
char pass[] = "YOUR_WIFI_PASSWORD";
```

> ⚠️ **Never commit real credentials to a public repository.** Use environment variables or a `secrets.h` file added to `.gitignore`.

### 3. Install Libraries

In Arduino IDE, go to **Sketch → Include Library → Manage Libraries** and install:
- `Blynk` by Volodymyr Shymanskyy
- `ESP8266WiFi` (included with the ESP8266 board package)

### 4. Upload the Code

- Select board: **NodeMCU 1.0 (ESP-12E Module)**
- Select the correct COM port
- Click **Upload**

### 5. Set Up Blynk Dashboard

In your Blynk project, add:
- **Gauge widget** → Virtual Pin **V1** (Water Level in cm)
- **LED widget** → Virtual Pin **V2** (Pump Status)

---

## 📱 Blynk App Preview

| Motor ON (Low Water Level) | Motor OFF (Tank Full) |
|----------------------------|-----------------------|
| LED indicator ON, pump running | LED indicator OFF, pump stopped |

---

## 📐 System Diagram

```
[Ultrasonic Sensor] ──► [NodeMCU ESP8266] ──► [Relay / Motor]
                               │
                          [Wi-Fi Cloud]
                               │
                         [Blynk Mobile App]
```

---

## Future Enhancements

- Add SMS/email alerts when tank is critically low or full
- Integrate with voice assistants (Alexa / Google Home)
- Support multiple tanks with a single dashboard
- Add water flow sensor for leak detection
- Enable scheduled pump operation timers
- Use deep sleep mode to improve energy efficiency

---

## 📚 References

- Jeswin, C., Marimuthu, B., & Chithra, K. (2017). *Ultrasonic water level indicator and controller using AVR microcontroller*. ICICES 2017. https://doi.org/10.1109/ICICES.2017.8070773
- Sachio, S., Noertjahyana, A., & Lim, R. (2019). *IoT Based Water Level Control System*. TIMES-iCON 2018. https://doi.org/10.1109/TIMES-iCON.2018.8621630
- [IoT Based Water Level Control & Monitoring with ESP8266 – how2electronics.com](https://how2electronics.com/iot-based-water-level-control-monitoring-with-esp8266/)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

> Built with using NodeMCU ESP8266, Arduino IDE, and Blynk 2.0.
