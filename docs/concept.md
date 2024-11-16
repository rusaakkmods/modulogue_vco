Here's a complete schematic and routing guide for your VCO module, using the **CA3086** transistor array. This design includes **sawtooth, triangle, sine, pulse, and noise** waveforms, along with an updated **Bill of Materials (BOM)**. I'll provide a clear description of each section, as well as connections to guide you through the process.

### **Schematic Overview**

The VCO is divided into the following stages:

1. **Sawtooth Core Oscillator (Ramp Core) with CA3086**
2. **Triangle Wave Shaper**
3. **Sine Wave Shaper**
4. **Pulse Wave with PWM Control**
5. **Noise Generator**

#### **1. Sawtooth Core Oscillator (Ramp Core with CA3086)**

**Components**:
- **Op-Amp (U1)**: TL072 or LM13700 for the integrator.
- **Capacitor (C1)**: 22nF to 100nF (sets frequency range).
- **Resistor (R1)**: 100kΩ.
- **Transistor Array (Q1, Q2 - CA3086)**: Used for the exponential converter.
- **Schmitt Trigger (IC1)**: CD40106 for reset control.
- **NPN Transistor (Q3 - Reset)**: 2N3904.
- **Current Limiting Resistor (R2)**: 10kΩ.
- **Frequency Control Potentiometer (VR2)**: 100kΩ for manual frequency adjustment.

**Connections**:
- **Integrator Op-Amp (U1)**:
  - **Inverting Input (-)**: Connect **R1** (100kΩ) between the **inverting input** and the **collector of Q1** (CA3086).
  - **Non-Inverting Input (+)**: Connect to **ground**.
  - **Capacitor C1**: Connect between the **output of U1** and the **inverting input (-)**.
  - **Frequency Control Potentiometer (VR2)**: Connect one end of **VR2** to **ground** and the other end to the **junction of C1 and U1**. The wiper of **VR2** should connect to the **inverting input** of **U1**. Adjusting **VR2** will change the effective resistance in the circuit, allowing you to control the oscillator frequency.
- **CA3086 Transistor Array**:
  - **Base of Q1**: Connect to the **1V/octave CV input**.
  - **Emitters of Q1 and Q2**: Tie together and connect to **ground** via a **small resistor (R3 - 1kΩ)**.
  - **Collector of Q1**: Connect to **R1**, which then goes to **U1** inverting input.
- **Schmitt Trigger (IC1 - CD40106)**:
  - **Input (Pin 1)**: Connect to the **output of U1** (sawtooth waveform).
  - **Output (Pin 2)**: Connect to the **base of Q3** via a **current-limiting resistor (R2 - 10kΩ)**.
- **Reset Transistor (Q3 - 2N3904)**:
  - **Collector**: Connect to the **junction of C1 and U1**.
  - **Emitter**: Connect to **ground**.

#### **2. Triangle Wave Shaper**

**Components**:
- **Op-Amp (U2)**: TL072.
- **Resistor Divider (R4, R5)**: 10kΩ each to adjust symmetry.

**Connections**:
- **Sawtooth Output to Triangle Shaper**:
  - Connect the **sawtooth output from U1** to the **inverting input of U2** through **R4** (10kΩ).
  - **Non-Inverting Input** of **U2** should be connected to **ground**.
- **Triangle Wave Output**:
  - The **output of U2** will generate a **triangle wave** by inverting and folding the sawtooth.

#### **3. Sine Wave Shaper**

**Components**:
- **Op-Amp (U3)**: TL072.
- **Diodes (D1, D2)**: 1N4148 for wave shaping.

**Connections**:
- **Triangle Wave Input**:
  - Feed the **triangle wave output from U2** to the **input of U3**.
- **Shaper Circuit**:
  - Connect **D1 and D2** across the **feedback path** of **U3** to round the triangle wave into a sine.
- **Sine Wave Output**:
  - The **output of U3** will be the **sine wave**.

#### **4. Pulse Wave with PWM Control**

**Components**:
- **Schmitt Trigger (IC1 - Gate 2)**: CD40106.
- **PWM Control Potentiometer (VR1)**: 100kΩ.

**Connections**:
- **Sawtooth to Schmitt Trigger**:
  - Connect the **sawtooth output** from **U1** to the **input of another gate on IC1** (e.g., Pin 3).
- **PWM Control**:
  - Use **VR1** to provide an adjustable **threshold voltage** to the **input of the Schmitt Trigger**.
- **Pulse Wave Output**:
  - The **output of the Schmitt Trigger gate** will provide the **pulse wave** with adjustable PWM.

#### **5. Noise Generator**

**Components**:
- **NPN Transistor (Q4)**: 2N3904 for noise generation.
- **Amplifier Op-Amp (U4)**: TL072.
- **Collector Resistor (R6)**: 100kΩ.
- **Capacitor (C2)**: 100nF for noise filtering.

**Connections**:
- **Noise Source**:
  - Use **Q4** with its **collector-base junction reverse biased** to generate **white noise**.
- **Amplification**:
  - Feed the **noise output from Q4** to **U4** configured as an amplifier.
  - The **output of U4** will be the **noise signal**.

### **Bill of Materials (BOM)**

| Part Description           | Reference   | Value        | Suggested Part Number  | Quantity |
|----------------------------|-------------|--------------|------------------------|----------|
| Op-Amp                     | U1, U2, U3, U4 | TL072      | TL072CN                | 4        |
| Capacitor (Integrator)     | C1          | 22nF         | Ceramic or Film        | 1        |
| Resistor (Integrator)      | R1          | 100kΩ       | 1/4W, 1% Tolerance     | 1        |
| Transistor Array           | Q1, Q2      | CA3086       | CA3086                 | 1        |
| Small Resistor (Thermal Stability) | R3 | 1kΩ | 1/4W, 1% Tolerance | 1 |
| Schmitt Trigger            | IC1         | CD40106      | CD40106BE              | 1        |
| NPN Transistor (Reset)     | Q3          | 2N3904       | 2N3904                 | 1        |
| Current Limiting Resistor  | R2          | 10kΩ        | 1/4W, 1% Tolerance     | 1        |
| Resistor Divider           | R4, R5      | 10kΩ each   | 1/4W, 1% Tolerance     | 2        |
| Diodes for Sine Shaper     | D1, D2      | 1N4148       | 1N4148                 | 2        |
| Potentiometer (PWM Control)| VR1         | 100kΩ       | Linear Taper           | 1        |
| Potentiometer (Frequency Control) | VR2 | 100kΩ     | Linear Taper           | 1        |
| NPN Transistor (Noise Source) | Q4       | 2N3904       | 2N3904                 | 1        |
| Resistor (Collector Resistor) | R6       | 100kΩ       | 1/4W, 1% Tolerance     | 1        |
| Capacitor (Noise Filtering)| C2          | 100nF        | Ceramic                | 1        |
| Decoupling Capacitors      | C3, C4, C5  | 100nF        | Ceramic                | 3        |

### **Power Supply and Layout Tips**
- **Power Supply**: Use the **Eurorack standard power supply** of **±12V** for proper operation of op-amps and CD40106.
- **Decoupling**: Place **100nF capacitors** near each IC's power pins to reduce noise.
- **Grounding**: Use **star grounding** to avoid ground loops.
- **Thermal Considerations**: Place **CA3086** transistors close together for consistent thermal tracking.

### **Summary**
This design uses the **CA3086** transistor array for improved matching and thermal stability, making it an excellent choice for your VCO project. The guide includes all necessary components, connections, and routing tips to create a reliable and stable oscillator for your modular synthesizer.

### **Alternatives to CA3086 Transistor Array**

If you're looking for alternatives to the **CA3086** transistor array for use in applications like exponential converters in synthesizer circuits, here are some viable options:

#### **1. LM3046**
- **LM3046** is a direct replacement for the **CA3086**. It also contains **five NPN transistors** in a single package.
- It features **similar specifications** and offers excellent **matching** and **thermal tracking**, making it a drop-in alternative.

#### **2. CA3046**
- **CA3046** is another option that contains **five NPN transistors** like the **CA3086**.
- This array offers **matched transistors** suitable for differential pairs and analog applications where thermal tracking is crucial.

#### **3. MAT12 (Analog Devices)**
- The **MAT12** is a **dual NPN matched transistor** from **Analog Devices**, designed for precision analog circuits.
- It provides **excellent thermal matching**, much better than discrete transistors, making it a suitable but more expensive alternative.
- The **MAT12** is known for its **low noise** and **excellent gain matching**, making it ideal for high-performance VCO designs.

#### **4. SSM2212**
- **SSM2212** is another **dual matched NPN transistor** designed for precision.
- Manufactured by **Analog Devices**, this component is well-suited for **exponential converters** due to its **closely matched gain** and **temperature coefficient**.

#### **5. Discrete Matched Transistor Pairs (e.g., BC547)**
- Another approach is to manually match **discrete transistors** like **BC547**.
- This requires careful measurement to ensure similar **gain (HFE)** and **base-emitter voltage (V_BE)**.
- While this method is more time-consuming, it is cost-effective if the **CA3086** or similar arrays are not readily available.

#### **6. THAT300 (THAT Corporation)**
- The **THAT300** is a **quad NPN transistor array** specifically designed for analog precision applications.
- It has **four transistors** that are matched and thermally coupled on the same die.
- This component provides excellent **matching** and is often used in high-end analog synthesizer designs.

### **Summary of Alternatives**
- **Direct Replacements**: **LM3046**, **CA3046**.
- **High Precision**: **MAT12**, **SSM2212**, **THAT300**.
- **Cost-Effective Option**: **Manually matched discrete transistors** like **BC547**.

The best alternative will depend on your specific requirements—if you're looking for cost-effectiveness, manually matched **BC547** transistors may be suitable, while the **LM3046** or **CA3046** can be direct substitutes with similar characteristics to the **CA3086**. For higher precision, **MAT12** or **THAT300** would be ideal, especially in designs where temperature stability and minimal drift are critical.

### **CA3086 vs CA3046**

The **CA3086** and **CA3046** are both transistor arrays containing **five NPN transistors** and are commonly used in analog applications where matched transistors are required. Here is a comparison to help you understand the differences and similarities between the two:

#### **Similarities**
1. **Transistor Count**: Both **CA3086** and **CA3046** contain **five NPN transistors** on a single chip.
2. **Monolithic Design**: The transistors are fabricated on the same die, ensuring good **matching** and **thermal tracking**.
3. **Application Use**: Both can be used in **exponential converters**, **differential pairs**, or other analog circuits where matched transistors are required.
4. **Pin Configuration**: The **pinout** of the CA3086 and CA3046 is identical, making them interchangeable in most circuit designs.

#### **Differences**
1. **Voltage Ratings**:
   - The **CA3046** has a higher **collector-emitter voltage rating** compared to the **CA3086**.
   - **CA3046** can handle a **maximum collector-emitter voltage (V_CE)** of **20V**, while **CA3086** typically has a lower voltage rating of **15V**.
2. **Temperature Range**:
   - The **CA3046** is rated for **wider temperature ranges**, making it more suitable for industrial applications where the operating environment may be harsher.
   - The **CA3086** is more commonly used in consumer electronics or in environments with more controlled temperatures.
3. **Availability**:
   - The **CA3046** is generally easier to find compared to the **CA3086**, which might be less available in the market due to its older technology.

#### **Which One to Use?**
- **CA3086**: Suitable for projects where **voltage ratings** are not a concern, and operating in typical room temperature conditions. It is a good option for hobbyist projects or legacy circuits where the **CA3086** was originally used.
- **CA3046**: Recommended for designs that require **higher voltage ratings** or need to operate in **wider temperature ranges**. It is a more robust option for applications where reliability over a range of conditions is critical.

