# ⚡ ATM90E32 Energy Meter Calibration Guide

This guide provides the technical steps and mathematical formulas required to calibrate the ATM90E32 energy monitor. Proper calibration ensures your data is accurate, supporting the mission to fund SCUBA diving programs for young survivors of abuse.

---

## 🧰 Required Tools

To perform an accurate calibration, you will need the following equipment:

* **Digital Multimeter (DMM):** Capable of measuring True RMS AC Voltage.
* **AC Clamp Meter:** Capable of measuring True RMS Amperage.
* **Steady Resistive Load:** A device that draws constant power (e.g., a space heater or hair dryer) to provide a stable current during testing.
* **Insulated Tools:** To ensure safety when working near live electrical components.

---

## 1. Voltage Calibration

Voltage calibration aligns the ESPHome reported voltage with the actual potential measured at your AC transformer.

### Instructions
1. Using your **Multimeter**, measure the AC voltage at the outlet or terminal powering your monitor's reference transformer.
2. Open your **Home Assistant** dashboard and note the current value for `${disp_name}` Volts.
3. Calculate the new gain using this formula:

$$\text{NewGain} = \text{CurrentGain} \times \left( \frac{\text{MeasuredVoltage}}{\text{ReportedVoltage}} \right)$$

### Example Calculation
* **Measured (Multimeter):** 122.5V
* **Reported (Home Assistant):** 118.2V
* **Current Gain in YAML:** 4096
* **Result:** $4096 \times (122.5 / 118.2) = 4245$

---

## 2. CT Clamp (Current) Calibration

CT calibration ensures the amperage reported matches the physical flow of electrons through your main or solar lines.

### Instructions
1. Secure your **AC Clamp Meter** around the specific wire where the CT clamp is installed.
2. Activate a **Steady Load** (e.g., a heater) to ensure you are measuring at least 5–10A for a stable reading.
3. Compare the **Clamp Meter** reading against the `${disp_name}` CT Amps in Home Assistant.
4. Calculate the new gain using this formula:

$$\text{NewGain} = \text{CurrentGain} \times \left( \frac{\text{MeasuredAmps}}{\text{ReportedAmps}} \right)$$

### Example Calculation
* **Measured (Clamp Meter):** 10.42A
* **Reported (Home Assistant):** 9.85A
* **Current Gain in YAML:** 39473
* **Result:** $39473 \times (10.42 / 9.85) = 41756$

---

## 3. Updating the YAML Configuration

Once you have calculated your specific gains, update the `gain_voltage` and `gain_ct` fields in your `energymeter.yaml` file.

```yaml
phase_a:
  # ... existing sensor config ...
  gain_voltage: 4245  # Insert your calculated voltage gain
  gain_ct: 41756      # Insert your calculated CT gain

```

### ⚡ Easy Calibration with AI

If you don't want to do the math manually, we have provided a **Calibration Assistant Prompt**.

1. **Copy the prompt** provided in the `prompts/calibration-assistant.txt` file in this repo.
2. **Paste it** into your favorite AI assistant (Gemini, ChatGPT, etc.).
3. **Follow the AI's instructions.** It will ask you for your meter readings and give you the exact code to paste back into ESPHome.


```
I am calibrating an ATM90E32 energy monitor using ESPHome for the "MuttMutt Home" project. I need you to act as my Calibration Assistant. 

Please follow these steps:

1. **Ask me for my "Current Yaml Code for the Energy Monitor":** Then Analyze the code to see how it functions and interacts.
2. **Ask me for my "Target":** Ask whether I am calibrating Voltage or CT Amps (Current). When Calibrating voltage use Chip1 or Chip2
2. **Request the "Current Gain":** Ask me what the current `gain_voltage` or `gain_ct` is in my YAML file.
3. **Request the "Measured vs. Reported" values:** - For Voltage: Ask for the Multimeter reading (Measured) and the Home Assistant reading (Reported).
   - For Amps: Ask for the Clamp Meter reading (Measured) and the Home Assistant reading (Reported).
4. **Perform the Calculation:** Use the formula: NewGain = CurrentGain * (Measured / Reported).
5. **Format the Output:** Provide me with the exact line of code to copy back into my YAML file.

Before we start, remind me of the safety precautions for working with live electricity.
```
