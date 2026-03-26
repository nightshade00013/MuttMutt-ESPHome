# 🌊 MuttMutt Home - ESPHome Builder Configuration Files

Welcome to the official repository for **MuttMutt Home** smart home configurations. These files are designed to provide high-precision monitoring for water and energy usage as well as help with other devices that you may be using.  This repository will be growing over the coming months and should help you setup many devices that are supported by ESPHome Builder and HomeAssistant

## 🎗️ Our Mission

I am MuttMutt, the founder of the **DogHouse Diving Foundation**

I am a geek, a SCUBA Diver, and a survivor of childhood abuse.

I want to help others with the knowledge I have freely so I host a lot of tutorials and other things at www.muttmutt.us and in my repositories on Github

The core mission of the **DogHouse Diving Foundation** is to provide children and young adults who have survived mental, physical, and/or sexual abuse the opportunity to experience the healing power of the underwater world through SCUBA diving—completely free of charge.  By subscribing to our channel, watching video's, and making purchases using our affiliate links you are helping to fund those activities.

#### You can show your thanks for this and help the foundation by heading over to:
#### https://www.muttmutt.us/your-welcome-here-is-how-you-can-say-thank-you/

---

## 🚀 Build Requirements & Compatibility

* **ESPHome Version:** 2026.1.0 or Higher
* **Optimization:** These configurations are optimized for the latest standards in the ESPHome ecosystem.

### The ESP-IDF Framework
Starting with the 2026.1.0 release, all ESP32 devices in this repository (such as the Energy Meter) are configured to use the **ESP-IDF framework** rather than the older Arduino framework.

* **Benefits:** Faster compile times, smaller binaries, and superior SPI stability for the ATM90E32 chips.
* **Note:** The ESP8266 devices (like the Water Meter) continue to use the standard `esp8266` framework.

---

## 🛠️ Included Configurations

* Note:  Some of the devices are DIY those devices will have pages located at www.muttmutt.us

| File | Device | Hardware | Purpose |
| :--- | :--- | :--- | :--- |
| `base-config.yaml` | Core Package | Shared | Centralized WiFi, API, and OTA management. |
| `Example-Secrets.yaml` | Core Package | Shared | Centralized Secrets file. |
| `4ChannelEnergyMeter.yaml` | Energy Meter | ESP32 + ATM90E32 | Real-time Grid & Solar monitoring (CT Clamps). |
| `PulseOutputWaterMeter.yaml` | Water Meter | ESP8266 + DAE AS200U-75P | Real-time flow and persistent lifetime totals. |
| `DIYElectricWaterHeaterController.yaml` | Water Heater | ESP8266 + DS18B20 | Dual-element temperature monitoring and relay control. |
| `TempAndHumidity.yaml` | Temp and Humidity | ESP8266 + DHT Sensor | Simple Temperature and Humidity Sensor. |

---

## 📋 Installation & Setup

1.  **Prerequisites:** Ensure you have ESPHome 2026.1.0+ installed.
2.  **Base Configuration:** Update `base-config.yaml` with your local WiFi credentials and API keys.
3.  **Secrets Configuration:** Make sure that your `secrets.yaml` file is properly configured and populated.
4.  **Static IPs:** Each YAML file is configured with a either a generic static IP or DHCP. Ensure these do not conflict with your network's IP pool.
5.  **Calibration:**
    * **Energy Meter:** Refer to `energy-meter-calibration-guide.md` to calculate your specific voltage and CT gains.
    * **Water Meter:** Set your `initial_value` in the `globals` section to match your physical meter dial.

## 🌡️ Water Heater Controller (DIY)
The `DIYElectricWaterHeaterController.yaml` is designed for high-current electric water heaters. It monitors three critical points to provide a complete picture of your thermal efficiency:

* **Top Temperature:** Monitors the upper heating element zone.
* **Bottom Temperature:** Monitors the lower heating element zone.
* **Output Temperature:** Monitors the water temperature as it leaves the tank for the house.

### **Safety First**
* **Restore Mode:** The relay is set to `ALWAYS_OFF`. If the ESP8266 reboots or loses power, the heating element will not turn on automatically until commanded by Home Assistant.
* **Inverted Logic:** Configured for standard active-low relay boards (common in DIY electronics).

### **Hardware Pinout**
* **GPIO04:** One-Wire Data Bus (requires a 4.7kΩ pull-up resistor).
* **GPIO05:** Relay Control Output.
---

## 🎨 Dashboard Integration

All sensors come pre-configured with **MDI (Material Design Icons)** and proper `device_class` settings. They will automatically appear in Home Assistant with appropriate units (**Gallons, Volts, Watts, kWh**) and are fully compatible with the **Home Assistant Energy Dashboard**.

---

## 🤝 Contributing & Support

If you encounter issues or wish to suggest an optimization, please open an issue or pull request. 

Your contributions help grow the channel and expand the reach of the DogHouse Diving Foundation.

* **Website:** [muttmutt.us](https://muttmutt.us)
* **Foundation:** [doghousediving.org](https://doghousediving.org)

