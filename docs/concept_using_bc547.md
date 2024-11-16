Here's a complete schematic and routing guide for your VCO module, using **matched BC547 transistors** instead of the **CA3086** transistor array. This design includes **sawtooth, triangle, sine, pulse, and noise** waveforms, along with an updated **Bill of Materials (BOM)**. I'll provide a clear description of each section, as well as connections to guide you through the process.

### **Schematic Overview**

The VCO is divided into the following stages:

1. **Sawtooth Core Oscillator (Ramp Core with Matched BC547 Transistors)**
2. **Triangle Wave Shaper**
3. **Sine Wave Shaper**
4. **Pulse Wave with PWM Control**
5. **Noise Generator**

#### **1. Sawtooth Core Oscillator (Ramp Core with Matched BC547 Transistors)**

**Components**:
- **Op-Amp (U1)**: TL072 or LM13700 for the integrator.
- **Capacitor (C1)**: 22nF to 100nF (sets frequency range).
- **Resistor (R1)**: 100kΩ.
- **Matched Transistors (Q1, Q2 - BC547)**: Used for the exponential converter.
- **Schmitt Trigger (IC1)**: CD40106 for reset control.
- **NPN Transistor (Q3 - Reset)**: 2N3904.
- **Current Limiting Resistor (R2)**: 10kΩ.
- **Frequency Control Potentiometer (VR2)**: 100kΩ for manual frequency adjustment.

**Connections**:
- **Integrator Op-Amp (U1)**:
  - **Inverting Input (-)**: Connect **R1** (100kΩ) between the **inverting input** and the **collector of Q1** (BC547).
  - **Non-Inverting Input (+)**: Connect to **ground**.
  - **Capacitor C1**: Connect between the **output of U1** and the **inverting input (-)**.
  - **Frequency Control Potentiometer (VR2)**: Connect one end of **VR2** to **ground** and the other end to the **junction of C1 and U1**. The wiper of **VR2** should connect to the **inverting input** of **U1**. Adjusting **VR2** will change the effective resistance in the circuit, allowing you to control the oscillator frequency.
- **Matched Transistors (Q1, Q2 - BC547)**:
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
| Matched Transistors        | Q1, Q2      | BC547        | Hand-matched BC547     | 2        |
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
- **Thermal Considerations**: Place **Q1 and Q2** (BC547) close together and consider using thermal compound or adhesive to improve thermal tracking.

### **Summary**
This design uses **matched BC547 transistors** for the exponential converter instead of the **CA3086** array. Careful matching of the transistors is important to achieve good temperature stability. The guide includes all necessary components, connections, and routing tips to create a reliable and stable oscillator for your modular synthesizer.


### **Guide to Manual Matching of Transistors**

Manual matching of transistors is an important process for circuits like **exponential converters** in VCOs, where precise performance and temperature stability are crucial. Here's a step-by-step guide to manually match transistors, particularly for **BC547** transistors.

#### **Goal of Matching Transistors**
For circuits like **exponential converters** in a VCO, it is important to match transistors for the following characteristics:
1. **Current Gain (HFE)** - The ratio of collector current to base current.
2. **Base-Emitter Voltage (V_BE)** - The voltage drop from base to emitter when conducting.

Closely matching these parameters helps improve the **accuracy** and **temperature stability** of your circuit.

#### **Equipment Needed**
1. **Multimeter with HFE Measurement** (preferable).
2. **Breadboard and Power Supply** (optional if you prefer building a test circuit).
3. **Test Circuit Components** - Resistors, battery, wires (optional if you need to measure with a test setup).

#### **Step-by-Step Guide to Manually Match Transistors**

##### **Method 1: Using a Multimeter with HFE Measurement**

1. **Set the Multimeter to HFE Mode**:
   - Most multimeters have a setting for measuring the **HFE** of transistors. Set your multimeter to this mode.

2. **Identify the Pins**:
   - The **BC547** is a standard NPN transistor with the pinout: **Collector (C)**, **Base (B)**, **Emitter (E)**.
   - Identify these pins on the transistor using the datasheet or reference image (typically, if looking at the flat face of the transistor, from left to right: **C**, **B**, **E**).

3. **Insert the Transistor**:
   - Insert the **collector, base, and emitter** pins of the transistor into the corresponding slots in the **HFE socket** of the multimeter (often labeled for NPN and PNP transistors).

4. **Record the HFE Value**:
   - Read the **HFE** value displayed on the multimeter and note it down.
   - Repeat this process for all the transistors you want to match, and write down each **HFE** value.

5. **Match Transistors**:
   - Compare the **HFE values** of all the transistors.
   - Find two transistors that have nearly identical **HFE values**. Ideally, they should be within **5%** of each other for good matching in a VCO application.

##### **Method 2: Using a Test Circuit on a Breadboard**

If your multimeter does not have an **HFE measurement mode**, you can use a simple test circuit to measure **V_BE** and **HFE**.

1. **Test Circuit Setup**:
   - Use a **breadboard** to set up a simple circuit to measure **HFE** and **V_BE**.
   - You’ll need:
     - **Power Supply** (e.g., a **9V battery** or a **DC power supply** set to 9-12V).
     - **Resistor** (1kΩ and 10kΩ).

2. **Circuit Description**:
   - Connect a **1kΩ resistor** between the **base** and the **positive supply**.
   - Connect a **10kΩ resistor** between the **collector** and the **positive supply**.
   - Connect the **emitter** to **ground**.

3. **Measure Collector Current (I_C)**:
   - Measure the **voltage across the 10kΩ collector resistor** using the multimeter.
   - **Calculate the collector current (I_C)** using **Ohm’s Law**: \( I_C = rac{V_R}{R} \), where \( V_R \) is the voltage across the resistor and \( R \) is the resistor value (10kΩ).
   
4. **Calculate Base Current (I_B)**:
   - Measure the **voltage across the 1kΩ base resistor**.
   - **Calculate the base current (I_B)** similarly: \( I_B = rac{V_R}{R} \), where \( V_R \) is the voltage across the 1kΩ resistor.

5. **Calculate HFE**:
   - Use the formula: \( HFE = rac{I_C}{I_B} \).
   - Record this value for each transistor.

6. **Measure V_BE**:
   - Measure the **voltage drop between the base and emitter (V_BE)**.
   - Note that **V_BE** should ideally be close, preferably within **5mV** for well-matched transistors.

7. **Select Matched Pairs**:
   - Compare the **HFE** values and **V_BE** values of all transistors.
   - Select transistors that have similar **HFE** and **V_BE** values.

#### **Tips for Manual Matching**

1. **Thermal Matching**:
   - Perform measurements under consistent temperature conditions. Small changes in temperature can affect **HFE** and **V_BE** significantly.
   - If possible, keep the transistors close together or even attach them with a thermally conductive adhesive when assembling the final circuit to minimize differences due to temperature variations.

2. **Batch Measurement**:
   - It’s a good idea to buy more transistors than needed and measure them all to find the closest match.
   - Transistors from the **same batch** are more likely to have similar characteristics due to the consistency of manufacturing.

3. **Target Matching Accuracy**:
   - For most analog synthesizer VCO applications, aim for **matching within 5%** for **HFE** and **within 5-10mV** for **V_BE**.
   - Better matching will result in **more accurate pitch tracking** and **less drift** with temperature changes.

#### **Summary**
- Use a **multimeter with HFE measurement** if available—this is the easiest and quickest way to match transistors.
- Alternatively, build a **test circuit** to measure **HFE** and **V_BE** if a dedicated HFE meter is not available.
- Look for **matched HFE and V_BE** values to ensure stability, especially for the **exponential converter** stage in a **VCO**.

Using well-matched transistors will provide the **temperature stability** and **precision** necessary for reliable musical tuning and pitch tracking in your synthesizer project.

### **Methods to Improve Thermal Tracking for BC547 Transistors**

Thermal tracking is critical in circuits like **exponential converters** used in **VCOs** to ensure consistent performance and minimal pitch drift. For **BC547 transistors**, here are effective methods to improve thermal tracking:

#### **1. Thermal Adhesive Compound**
- Apply a **thermal adhesive compound** between the two matched transistors (e.g., **Q1 and Q2** in your VCO circuit).
- This ensures that both transistors are in **direct thermal contact**, allowing them to heat up and cool down at the same rate.
- By maintaining a similar temperature, the **gain (HFE)** and **V_BE** remain more consistent, improving stability.

#### **2. Heat Shrink Tubing**
- Use a piece of **heat shrink tubing** to encase both transistors together.
- This method holds the transistors in tight physical contact, improving thermal equilibrium between them.
- The heat shrink tubing helps them share heat effectively, reducing any thermal gradient that might cause drift.

#### **3. Copper Foil or Heatsink**
- Wrap both transistors with **copper foil tape** to increase their thermal conductivity.
- Copper is highly thermally conductive, and wrapping it around the transistors will help distribute heat evenly between them.
- Alternatively, use a small **metal heatsink** that is in contact with both transistors to stabilize their temperature.

#### **4. Mounting on the Same PCB Pad**
- Place both transistors on the same **thermal pad** or closely spaced **PCB area**.
- The shared **copper pad** helps to maintain an even temperature between the transistors, as it acts as a heat spreader.
- Make sure to avoid excessive spacing between the transistors, as proximity is key for effective thermal coupling.

#### **Summary**
- **Thermal Adhesive Compound** and **heat shrink tubing** are the simplest methods for improving thermal tracking of **BC547 transistors**.
- Using **copper foil tape** or a **heatsink** further enhances thermal contact and helps maintain temperature consistency.
- **PCB layout considerations**, such as mounting both transistors on the same pad, also play a crucial role in ensuring they track each other's temperature closely.

These methods will help minimize temperature-induced variations in the **exponential converter** circuit, leading to improved stability and pitch accuracy for your VCO.

