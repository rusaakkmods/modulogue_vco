### **Pulse Wave with PWM Control: Step-by-Step Schematic Routing**

The **Pulse Wave Generator with PWM (Pulse Width Modulation) Control** allows the width of the pulse wave to be adjusted in real time, giving a rich variety of timbral changes. Here is a detailed step-by-step guide to create a pulse wave generator with PWM control:

#### **1. Key Components**
- **Op-Amp (U5A - TL072 or similar)**
- **Comparator** for PWM control
- **Triangle Wave Input** for creating the pulse wave
- **PWM Input Signal** (for modulating the pulse width)
- **Potentiometer (RV5)** for manual PWM adjustment
- **Resistors and capacitors** for feedback and signal control

#### **Step-by-Step Schematic Routing**

##### **1. Triangle Wave Input to Comparator**
- **Input Signal**:
  - Use a **triangle waveform** from the previous oscillator stage.
  - Connect the **triangle wave input** to the **inverting input (-)** of the **comparator op-amp (U5A)** through a **resistor R11 (10kΩ)**. This signal acts as the reference for comparison and sets the waveform’s symmetry.

##### **2. Pulse Width Control via Potentiometer (RV5)**
- **PWM Control Potentiometer**:
  - Add a **potentiometer (RV5, 10kΩ - 50kΩ)** to adjust the **pulse width manually**.
  - **One terminal** of **RV5** should be connected to a **reference voltage**, typically derived from a stable supply like **+5V**.
  - The **other terminal** of **RV5** should be connected to **ground**.
  - The **wiper** of **RV5** should be connected to the **non-inverting input (+)** of the comparator op-amp (U5A).
  - This configuration allows you to manually control the threshold level, thus adjusting the pulse width.

##### **3. Adding PWM Modulation**
- **Modulation Input (PWM)**:
  - You can add an external modulation signal to change the **pulse width** automatically.
  - Connect the **PWM modulation input** to the **non-inverting input (+)** of **U5A** through a **resistor R12 (10kΩ)**.
  - This modulation signal could come from an LFO (Low-Frequency Oscillator), an envelope generator, or any other modulation source. This will provide dynamic control over the pulse width.

##### **4. Comparator Output for Pulse Wave**
- **Comparator Output**:
  - The **output of U5A (pin 1)** will produce the **pulse wave**.
  - The comparator will compare the triangle wave to the PWM control voltage, outputting a **high** or **low** signal depending on whether the triangle input is above or below the threshold set by the PWM control. This produces the **pulse wave**.
  - **Output Resistor (R13, 1kΩ)**: Add **R13** at the output of **U5A** to limit the current.

##### **5. Feedback and Stability**
- **Hysteresis Resistor for Stability**:
  - To add **hysteresis** (which prevents the comparator from rapidly switching due to noise), connect a **resistor (R14, 1MΩ)** between the **output (pin 1)** of **U5A** and the **non-inverting input (+)**.
  - This feedback introduces a small amount of positive feedback, making the output more stable and reducing unwanted oscillation around the switching point.

##### **6. Power Supply for Op-Amp (U5A)**
- **Power Supply**:
  - Ensure **pin 8** of **U5A** is connected to **+12V**, and **pin 4** is connected to **-12V**.
- **Decoupling Capacitors**:
  - Place **decoupling capacitors (C8, C9 - 100nF each)** between **+12V and ground** and **-12V and ground** to filter any supply noise.

#### **Summary of Connections**
1. **Triangle Wave Input**:
   - Connect to the **inverting input (-)** of the comparator through **R11 (10kΩ)**.
2. **Manual PWM Control (RV5)**:
   - Connect **RV5** between **+5V** and **ground**.
   - The **wiper** goes to the **non-inverting input (+)** of **U5A**.
3. **Modulation Input**:
   - Connect the **PWM modulation signal** to the **non-inverting input (+)** through **R12 (10kΩ)**.
4. **Comparator Output**:
   - **U5A output (pin 1)** generates the **pulse wave**.
   - Add **R13 (1kΩ)** to limit output current.
5. **Hysteresis Feedback**:
   - Connect **R14 (1MΩ)** between the **output** and the **non-inverting input (+)** of **U5A**.
6. **Power Supply and Decoupling**:
   - **+12V** to **pin 8**, **-12V** to **pin 4**.
   - **C8 and C9 (100nF)** for decoupling between **power pins** and **ground**.

This configuration will give you a **pulse wave output** with adjustable **PWM** through both manual control and external modulation, making it versatile for different synthesis applications.

### **Bill of Materials (BOM)**

| Part Description                     | Reference | Value         | Suggested Part Number | Quantity |
|--------------------------------------|-----------|---------------|-----------------------|----------|
| Potentiometer (Manual PWM Control)   | RV5       | 10kΩ - 50kΩ  | Linear Taper          | 1        |
| Op-Amp                               | U5A       | TL072         | TL072CN               | 1        |
| Input Resistor (Triangle Wave)       | R11       | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| Input Resistor (PWM Modulation)      | R12       | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| Output Resistor                      | R13       | 1kΩ           | 1/4W, 1% Tolerance    | 1        |
| Hysteresis Resistor                  | R14       | 1MΩ           | 1/4W, 1% Tolerance    | 1        |
| Decoupling Capacitors                | C8, C9    | 100nF         | Ceramic               | 2        |

This BOM lists the components needed for the pulse wave generation with PWM control, including resistors, capacitors, potentiometers, and an op-amp. Feel free to ask if you need more details or further assistance with the design!

