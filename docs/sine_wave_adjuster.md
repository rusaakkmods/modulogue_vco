### **Sine Wave Shaper: Complete Schematic Guide with Amplitude Control and Triangle Corner Shaping**

This guide explains how to design the **Sine Wave Shaper** with **amplitude control** and **triangle corner shaping** for better sine conversion, including a complete schematic routing, a Bill of Materials, and an operational overview.

#### **Step-by-Step Schematic Routing**

##### **1. Triangle Wave Input to Sine Shaper**
- **Input Signal**:
  - Connect the **triangle wave output** from the previous stage (triangle wave shaper) to the **inverting input (-)** of the op-amp **U3 (TL072)** through **resistor R9 (10kΩ)**. This resistor helps control the input signal.

##### **2. Diode Shaping Network for Sine Wave Conversion**
- **Diodes (D1, D2)**:
  - Use two **1N4148 diodes (D1 and D2)** to clip the triangle waveform, converting it to a sine wave.
  - Connect **D1** and **D2** in opposite directions, with their cathodes and anodes meeting at the **inverting input (-)** of **U3**. Connect the **other junction** (the free ends) of **D1 and D2** to **ground**. This forms a symmetric clipping point around ground, shaping the input triangle wave into a sine wave.
- **Triangle Corner Shaping Potentiometer (RV4)**:
  - Replace the fixed resistors in the shaping network with a **potentiometer (RV4, 10kΩ)** to control the clipping level.
  - Connect **one outer terminal** of **RV4** in series with **D1** and **D2**.
  - Connect the **middle wiper** of **RV4** to the **junction point** between **D1, D2**, and the **inverting input (-)** of **U3**. Adjusting **RV4** will allow you to fine-tune how much of the triangle wave is clipped, resulting in different sine wave characteristics.

##### **3. Feedback Network for Gain Control**
- **Feedback Resistor (R10)**:
  - Connect a **resistor (R10, 10kΩ)** between the **output of U3 (pin 1)** and the **inverting input (-) (pin 2)**. This resistor defines the gain and ensures proper feedback for sine shaping.
- **Optional Capacitor for Smoothing (C4)**:
  - You can add a **small capacitor (10pF to 33pF)** in parallel with **R10** to reduce high-frequency oscillations and smooth out the sine wave.

##### **4. Amplitude Control Potentiometer (RV3)**
- **Output of the Op-Amp**:
  - Connect the **output of the sine wave shaping op-amp** (U3) to one of the **outer terminals** of the potentiometer **(RV3, 10kΩ - 50kΩ)**.
- **Ground Connection**:
  - Connect the **other outer terminal** of **RV3** to **ground**.
- **Middle Wiper as Adjustable Output**:
  - The **middle wiper** will act as the **adjustable amplitude output**. This allows you to adjust the amplitude of the sine wave output to match other waveform levels or provide a desired output range.

##### **5. Power Supply for Op-Amp (U3)**
- **Op-Amp Power Supply**:
  - Connect **pin 8** of **U3** to the **+12V supply**.
  - Connect **pin 4** of **U3** to the **-12V supply**.
- **Decoupling Capacitors (C2, C3)**:
  - Place **100nF capacitors** between the **+12V and ground** and **-12V and ground** to stabilize the power supply and reduce noise.

### **Bill of Materials (BOM)**

| Part Description                      | Reference | Value         | Suggested Part Number | Quantity |
|---------------------------------------|-----------|---------------|-----------------------|----------|
| Potentiometer (Amplitude Control)     | RV3       | 10kΩ - 50kΩ  | Linear Taper          | 1        |
| Potentiometer (Corner Shaping)        | RV4       | 10kΩ          | Linear Taper          | 1        |
| Diodes for Sine Shaping               | D1, D2    | 1N4148        | 1N4148                | 2        |
| Op-Amp                                | U3        | TL072         | TL072CN               | 1        |
| Feedback Resistor                     | R10       | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| Input Resistor                        | R9        | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| Resistors (Optional for Limiting)     | R7, R8    | 1kΩ           | 1/4W, 1% Tolerance    | 2        |
| Capacitors (Decoupling)               | C2, C3    | 100nF         | Ceramic               | 2        |
| Capacitor for Smoothing (Optional)    | C4        | 10pF - 33pF   | Ceramic               | 1        |

### **Operational Overview**

- **Amplitude Control**: By adjusting **RV3**, you control the final **output level** of the sine wave. This helps match its amplitude to the other waveforms or provides a customizable output level.
- **Shaping Adjustment**: **RV4** allows you to control how much the **triangle corners are rounded** by adjusting the diode clipping point. This gives you a way to tune how close the waveform resembles an ideal sine wave—adjusting between more of a triangle or a smoothly rounded sine shape.

### **Summary of Changes**

- Add a **potentiometer (RV3)** at the output to control the **amplitude** of the sine wave.
- Replace the fixed resistors in the **diode shaping network** with a **potentiometer (RV4)** to adjust the curvature and **symmetry** of the sine wave.
- Add a **feedback resistor (R10)** to define gain, with an optional capacitor (C4) to smooth the sine wave output.

These changes provide more flexibility and control over both the **waveform's shape** and its **amplitude**, making the sine wave more versatile for use in different applications. Let me know if you need any more information or guidance on implementing these changes!

