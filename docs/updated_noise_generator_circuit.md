### **Updated Complete Schematic for Noise Circuit with Voltage-Controlled Blending and Mixer Using CD40106**

This updated schematic integrates the noise circuit with the voltage-controlled blending functionality, utilizing **2N5457 JFETs** as voltage-controlled amplifiers (VCAs). Additionally, the remaining inverters in the **CD40106** are used to create independent buffered noise outputs for each waveform. Each waveform (sawtooth, triangle, sine, pulse) controls the noise level individually, creating dynamic, modulated noise effects for each output.

#### **Key Sections of the Schematic**

1. **Noise Generation and Amplification**:
   - **Noise Source**: The noise is generated using **BC547 (Q1)**, with the **collector** connected to **+12V** via **R15 (100kΩ)**, and the **emitter** connected to **ground**. The **base** is left floating to produce thermal noise.
   - **Amplification Stage**: The noise signal is then coupled through **C8 (10μF)** to the **non-inverting input (+)** of **op-amp U5A (TL072)** for amplification.
     - **R16 (1MΩ)** sets a reference for the **non-inverting input (+)**.
     - **R17 (470kΩ)** and **R18 (10kΩ)** set the gain for the op-amp.
   - The amplified noise output is available at **pin 1** of **U5A**.

2. **Noise Buffering Using CD40106**:
   - The **amplified noise output** from **U5A** is routed to the **inputs of 5 separate inverters** in the **CD40106** (e.g., pins 1, 3, 5, 9, and 11).
   - Each inverter provides a buffered version of the noise signal, ensuring isolated noise distribution for blending with each waveform.

3. **Envelope Follower for Waveform Control Signal**:
   - Each waveform output (sawtooth, triangle, sine, pulse) is connected to an **envelope follower** circuit consisting of a **diode (1N4148)** and **capacitor (10μF)**.
   - The **diode (D1, D2, D3, D4)** and **capacitor (C14, C15, C16, C17)** create a control voltage proportional to the waveform's amplitude, which is then used to control the noise level.

4. **JFET-Based Voltage-Controlled Amplifier (VCA)**:
   - **JFETs (2N5457)** are used as VCAs to control the amplitude of the noise signal for each waveform.
   - The **drain** of each JFET (Q2, Q3, Q4, Q5) is connected to the respective **buffered noise output** from the **CD40106**.
   - The **gate** of each JFET receives the control voltage from the corresponding envelope follower (D1, C14, etc.).
   - The **source** of each JFET is connected to the respective waveform blending stage.

5. **Summing Mixer for Blended Output**:
   - After passing through the JFET VCA, the noise signal is summed with the respective waveform using an **op-amp summing mixer** (U7A, U7B - TL072).
   - Each waveform output is connected to the **non-inverting input (+)** of the op-amp.
   - The noise signal (after blending) is connected to the **inverting input (-)** of the op-amp through a **mixing resistor (R21, R22, R23, R24 - 100kΩ)**.
   - **Feedback resistors (R25, R26, R27, R28 - 100kΩ)** are used to set the gain for each summing stage, ensuring the correct blend of noise and waveform.

6. **Power Supply and Decoupling**:
   - Ensure **+12V** and **-12V** are properly connected to the power pins of all op-amps (pins **8** and **4** respectively for TL072).
   - Use **decoupling capacitors (C12, C13 - 100nF)** between **+12V** and **ground**, and **-12V** and **ground** to filter any power supply noise.

#### **Summary of Connections**

1. **Noise Source and Amplification**:
   - **BC547 (Q1)**: Collector to **+12V** via **R15 (100kΩ)**, emitter to **ground**.
   - **Amplified Noise**: Coupled through **C8 (10μF)** to **U5A** (TL072) for amplification.
2. **Noise Buffering Using CD40106**:
   - **Amplified Noise Output**: Connect the amplified noise output from **U5A** to the **inputs of 5 inverters** in **CD40106** (pins 1, 3, 5, 9, and 11).
   - **Buffered Noise Outputs**: Available at pins **2, 4, 6, 10, and 12** of the **CD40106**.
3. **Envelope Followers**:
   - **Waveform Outputs**: Connect each waveform output to an envelope follower (diode and capacitor) to generate a control voltage.
4. **JFET VCAs**:
   - **2N5457 (Q2, Q3, Q4, Q5)**: Drain connected to buffered noise from **CD40106**, gate receives control voltage from envelope follower, source to blending stage.
5. **Summing Mixer**:
   - **Op-Amps (U7A, U7B - TL072)**: Used to mix the original waveform and the noise signal for each waveform.
6. **Power Supply**:
   - **Decoupling Capacitors**: Place **C12, C13 (100nF)** close to the power pins of all op-amps.

#### **Bill of Materials (BOM) Update**

| Part Description                     | Reference       | Value         | Suggested Part Number | Quantity |
|--------------------------------------|-----------------|---------------|-----------------------|----------|
| NPN Transistor                       | Q1              | BC547         | BC547                 | 1        |
| Collector Resistor                   | R15             | 100kΩ         | 1/4W, 1% Tolerance    | 1        |
| Coupling Capacitor                   | C8              | 10μF          | Electrolytic          | 1        |
| Amplification Reference Resistor     | R16             | 1MΩ           | 1/4W, 1% Tolerance    | 1        |
| Feedback Resistor (U5A)              | R17             | 470kΩ         | 1/4W, 1% Tolerance    | 1        |
| Inverting Input Resistor (U5A)       | R18             | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| High-Pass Filter Capacitor           | C10             | 100nF         | Ceramic               | 1        |
| High-Pass Filter Potentiometer       | RV7             | 50kΩ          | Linear Taper          | 1        |
| Low-Pass Filter Capacitor            | C9              | 10nF          | Ceramic               | 1        |
| Low-Pass Filter Potentiometer        | RV6             | 50kΩ          | Linear Taper          | 1        |
| Resistor for Low-Pass Wiper          | R19             | 10kΩ          | 1/4W, 1% Tolerance    | 1        |
| Mixer Op-Amp                         | U5B, U7A, U7B   | TL072         | TL072CN               | 3        |
| Mixing Resistors                     | R20, R21, R22, R23, R24 | 100kΩ | 1/4W, 1% Tolerance | 5        |
| Blend Control Potentiometers         | RV8 (x4)        | 50kΩ          | Linear Taper          | 4        |
| Mixer Feedback Resistor              | R25, R26, R27, R28 | 100kΩ       | 1/4W, 1% Tolerance    | 4        |
| Decoupling Capacitors                | C12, C13        | 100nF         | Ceramic               | 2        |
| Inverter Buffer (Noise Distribution) | CD40106         | -             | CD40106               | 1        |
| JFET                                 | Q2, Q3, Q4, Q5  | 2N5457        | 2N5457                | 4        |
| Diode for Envelope Follower          | D1, D2, D3, D4  | 1N4148        | 1N4148                | 4        |
| Capacitor for Envelope Follower      | C14, C15, C16, C17 | 10μF       | Electrolytic          | 4        |
| Resistors for VCA                    | R26, R27, R28, R29 | 100kΩ       | 1/4W, 1% Tolerance    | 4        |

#### **Step-by-Step Routing Guide**

1. **Noise Source and Amplification**:
   - Connect the **collector** of **Q1 (BC547)** to **+12V** via **R15 (100kΩ)**. Connect the **emitter** of **Q1** to **ground**. Leave the **base** of **Q1** floating to generate thermal noise.
   - Couple the noise through **C8 (10μF)** to the **non-inverting input (+)** of **U5A (TL072)**. Connect **R16 (1MΩ)** between the **non-inverting input (+)** and **ground**.
   - Set the gain of **U5A** using **R17 (470kΩ)** and **R18 (10kΩ)**. The amplified noise output is available at **pin 1** of **U5A**.

2. **Noise Buffering with CD40106**:
   - Connect the amplified noise output from **U5A** to the **inputs of 5 inverters** in **CD40106** (pins 1, 3, 5, 9, and 11).
   - The **buffered noise outputs** are available at **pins 2, 4, 6, 10, and 12**.

3. **Envelope Followers**:
   - Connect each waveform output (sawtooth, triangle, sine, pulse) to an **envelope follower** circuit (diode and capacitor).
   - Connect **diodes (D1, D2, D3, D4)** in series with **capacitors (C14, C15, C16, C17 - 10μF)** to generate control voltages proportional to waveform amplitudes.

4. **JFET VCAs**:
   - Connect the **drain** of each **JFET (2N5457 - Q2, Q3, Q4, Q5)** to the respective **buffered noise output** from **CD40106**.
   - Connect the **gate** of each JFET to the control voltage from the corresponding envelope follower.
   - Connect the **source** of each JFET to the respective waveform blending stage.

5. **Summing Mixer**:
   - Use **op-amps (U7A, U7B - TL072)** to mix the original waveform and noise for each waveform.
   - Connect the original waveform to the **non-inverting input (+)** and the noise signal (via blending resistor) to the **inverting input (-)** of the op-amp.
   - Use **feedback resistors (R25, R26, R27, R28 - 100kΩ)** to set the appropriate gain for each summing stage.

6. **Power Supply and Decoupling**:
   - Connect **+12V** and **-12V** to the power pins (**8** and **4** respectively) of each op-amp.
   - Place **decoupling capacitors (C12, C13 - 100nF)** between **+12V** and **ground**, and **-12V** and **ground** to filter power supply noise.

This configuration allows each waveform output to dynamically control the noise level using a JFET-based VCA, with the **CD40106** providing buffered noise signals for each path, resulting in a unique blended output for each waveform that varies according to its amplitude. Let me know if you need more details on any part of this updated schematic or further assistance!

