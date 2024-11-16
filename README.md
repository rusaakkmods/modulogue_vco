### **Summary of Modular Synthesizer Project**

#### **Project Overview**
This modular synthesizer project involved designing and building multiple waveform generation and blending circuits, aimed at creating a versatile and adjustable synthesizer module. The primary goals were to implement various waveforms, include a noise source, and blend all the generated signals into a single output. The project also included specific modifications, such as fine-tuning, power supply design, and signal buffering to ensure stability and reliability.

#### **Key Components and Stages**

1. **Oscillator Core (Ramp Core)**
   - A ramp core oscillator was designed using a **TL072** operational amplifier as the integrator, along with a **2N3904** transistor and **CA3086** transistor array for current mirroring.
   - The integrator frequency is controlled by **RV1**, with an additional fine-tuning **trimmer (R36)**, allowing precise frequency adjustment.
   - **CD40106 Schmitt Trigger** inverters were used for signal buffering, ensuring the stability of the output signal.

2. **Waveform Generation and Blending**
   - The circuit generates several basic waveforms: **sawtooth, triangle, sine, and pulse**.
   - Each waveform output is blended with an adjustable amount of noise using **JFETs (2N5457)** as voltage-controlled amplifiers (VCAs).
   - The blend output of each waveform was further processed through a buffering stage using **TL072** operational amplifiers.

3. **Noise Source and Filtering**
   - A **white noise generator** was implemented using a **BC547** transistor, with the noise amplified by a **TL072** operational amplifier.
   - Adjustable filtering was added to shape the noise characteristics, providing both **high-pass** and **low-pass** controls, implemented with **RV7** and **RV6**.
   - The filtered noise was further buffered to ensure clean blending with the other waveforms.

4. **Signal Mixing**
   - The blended outputs of the sawtooth, triangle, sine, and pulse waveforms were mixed into a final output using a **TL072** operational amplifier configured as a summing amplifier.
   - **Mix Out** provides a composite audio signal with all waveforms mixed with noise, with individual blending for each waveform.

5. **Power Supply Design**
   - A **Eurorack power connector (J9)** was used for powering the module, providing **±12V, +5V, CV, and Gate** signals.
   - **Protection diodes (1N5819)** were added to each power line, followed by capacitors for decoupling and stability (±12V and +5V).
   - A **single power-on LED indicator** was added to the +5V line, indicating when the module is powered.

#### **Challenges and Improvements**
- **Thermal Coupling**: The **CA3086/3046** transistor array was used for better thermal coupling of the transistors, which helped reduce frequency drift and improved pitch stability.
- **Signal Buffering**: The use of **CD40106** Schmitt Trigger inverters for buffering was initially a concern due to their threshold nature. This was addressed by careful selection of the threshold voltage levels, ensuring proper signal integrity.
- **Component Selection**: The decision to use **TL072** for all operational amplifier needs was made due to its wide availability, cost-effectiveness, and adequate performance characteristics for audio signal processing.

#### **Outcome**
- A fully functional modular synthesizer module was designed, capable of generating sawtooth, triangle, sine, and pulse waveforms, each of which can be blended with an adjustable amount of noise.
- The project successfully addressed all the initial design goals, providing flexibility in waveform generation and blending, along with a stable power supply and efficient signal buffering.

This modular synthesizer is now ready for integration into a Eurorack system, providing unique sonic possibilities through its noise blending and waveform generation features.

### **Comprehensive Review of Synthesizer Schematics**

#### **Project Overview**
The goal of our project was to create a versatile analog synthesizer module capable of generating multiple waveform outputs, including sawtooth, triangle, sine, pulse, and noise. We also aimed for flexibility in signal blending, along with a reliable power section for consistent operation. The design uses commonly available components, ensuring it can be built with minimal specialized parts while providing a high level of functionality.

Below is a detailed review of the individual sections of the schematics, and how they align with our goals:

#### **1. Ramp Core Oscillator**
- **Schematic (01_ramp_core.png)**: The ramp core oscillator is at the heart of this synthesizer. It utilizes a **TL072 op-amp** to generate a stable ramp waveform, which serves as the basis for shaping other waveforms.
- **Components & Design Considerations**:
  - **CA3086/3046** transistor array forms a **current mirror**, which is key for controlling the ramp's linearity and stability.
  - **RV1 (100kΩ)** is used for frequency control, with **R36 (10kΩ)** added to ensure finer tuning.
  - The use of **Q2 (2N3904)** as a current sink and the **Schmitt trigger (CD40106)** for buffering ensures a sharp and well-defined ramp reset.
- **Conclusion**: This section effectively creates the ramp waveform with control over its frequency and reset characteristics. The fine-tuning and thermal coupling of transistors enhance pitch stability, meeting our goal of producing a precise core waveform.

#### **2. Triangle Wave Shaper**
- **Schematic (02_triangle_wave.png)**: The ramp waveform is shaped into a triangle wave using a **TL072** op-amp and a pair of **diodes (1N4148)**.
- **Symmetry Control**:
  - **RV4 (10kΩ)** allows for symmetry adjustments, ensuring a balanced triangle wave. Proper alignment of diodes helps achieve a linear slope on both halves of the triangle.
- **Conclusion**: The triangle wave is a fundamental waveform in many synthesis processes, and the use of a symmetry adjustment meets our goal of ensuring waveform accuracy.

#### **3. Sine Wave Shaper**
- **Schematic (03_sine_wave.png)**: The triangle waveform is converted into a sine wave through a feedback network using **capacitor C4** and **TL072**.
- **Shaping and Adjustment**:
  - The trimmer **RV2 (10kΩ)** is critical for reducing harmonic distortion and shaping the sine wave properly.
- **Conclusion**: The sine wave shaping circuit effectively smooths the triangle waveform, creating a sine with adjustable harmonic content. This fulfills our goal of generating a clean, adjustable sine output.

#### **4. Pulse Wave Shaper**
- **Schematic (04_pulse_wave.png)**: The **TL072 (U4B)** op-amp shapes the input from the triangle waveform and LFO into a pulse waveform.
- **Pulse Width Control**:
  - **RV5 (10kΩ)** allows manual control of the pulse width, while the **LFO** input modulates the pulse width, adding versatility for different modulation scenarios.
- **Conclusion**: The pulse width modulation capability, along with manual control, provides the desired flexibility in sound design, meeting our project objectives for waveform variety.

#### **5. Noise Generator**
- **Schematic (05_noise_generator_v2.png)**: Noise is generated using a **CA3086/3046 transistor** and amplified with a **TL072 (U5A)**.
- **Filtering**:
  - **RV7** and **RV8** are used to control the high-pass filter characteristics, allowing adjustments in the coloration of the noise output.
- **Conclusion**: Noise generation with adjustable filtering is useful for creating diverse sound textures, aligning well with our goal of a versatile noise section.

#### **6. Waveform Blending and Summing**
- **Schematic (06_mixed_out.png)**: Each waveform output is blended using a **summing amplifier (TL072, U10B)**.
- **Mixing Control**:
  - Equal resistances (**100kΩ**) for each input ensure that all waveforms are summed evenly, providing a balanced mixed output.
- **Conclusion**: This blending stage achieves the goal of providing a single output that contains a mix of all generated waveforms, offering a comprehensive signal suitable for various applications.

#### **7. Power Supply and Distribution**
- **Schematic (07_power_connector.png)**: The power section delivers **+12V, -12V, and +5V** to the different parts of the circuit.
- **Power Integrity**:
  - **Diodes (1N5819)** protect against reverse polarity, and capacitors ensure proper decoupling.
  - The addition of an LED indicator for the **+5V** line serves as a power-on visual indicator.
- **Conclusion**: The power section is robust, ensuring stable operation across the synthesizer. Proper decoupling and visual status indication align with the goal of reliability.

#### **8. Output Connections**
- **Schematic (08_outputs.png)**: Each generated waveform, including the mixed output, is connected to individual output jacks.
- **Labelling and Accessibility**:
  - Proper labeling of outputs ensures that each waveform can be accessed easily, making the synthesizer user-friendly.
- **Conclusion**: The output interface meets our objective of making all waveforms accessible for external use, fulfilling the goal of usability.

### **Overall Assessment**
The project successfully meets the outlined objectives:
- **Versatility**: The synthesizer offers a wide range of waveforms—sawtooth, triangle, sine, pulse, and noise—each with adjustable parameters, providing a rich palette for sound design.
- **Stability and Control**: The use of **thermal coupling**, **fine-tuning trimmers**, and **proper filtering** ensures the oscillator remains stable, while the power section guarantees reliable operation.
- **User-Friendly Design**: The interface, including labeled outputs and the power-on indicator, makes the synthesizer easy to operate.

Overall, the design is well-executed, with each section effectively contributing to the synthesizer's versatility and reliability. The schematics illustrate a thoughtful and methodical approach to achieving a high-quality analog synthesizer module.

#### **Complete Bill of Materials (BOM)**

| No | Reference                                                                                           | Value       | Qty |
| -- | --------------------------------------------------------------------------------------------------- | ----------- | --- |
| 1  | C1                                                                                                  | 22nF        | 1   |
| 2  | C2, C3, C5, C6, C10, C11, C12, C17, C18, C19, C20, C21, C22, C23, C24, C25, C26, C27, C28, C29, C32 | 100nF       | 21  |
| 3  | C4, C7                                                                                              | 10pF ~ 33pF | 2   |
| 4  | C8, C13, C14, C15, C16                                                                              | 10uF        | 5   |
| 5  | C9                                                                                                  | 10nF        | 1   |
| 6  | C30, C31, C33                                                                                       | 47uF        | 3   |
| 7  | D1, D2                                                                                              | 1N4148      | 2   |
| 8  | D3, D4, D5, D6                                                                                      | 1N4148      | 4   |
| 9  | D7, D8, D9                                                                                          | 1N5819      | 3   |
| 10 | D10                                                                                                 | POWER ON    | 1   |
| 11 | J1                                                                                                  | SAWTOOTH    | 1   |
| 12 | J2                                                                                                  | TRIANGLE    | 1   |
| 13 | J3                                                                                                  | SINE        | 1   |
| 14 | J4                                                                                                  | PULSE       | 1   |
| 15 | J5                                                                                                  | MIX OUT     | 1   |
| 16 | J6                                                                                                  | NOISE       | 1   |
| 17 | J7                                                                                                  | HP NOISE    | 1   |
| 18 | J9                                                                                                  | POWER       | 1   |
| 19 | J10                                                                                                 | CV IN       | 1   |
| 20 | Q2                                                                                                  | 2N3904      | 1   |
| 21 | Q3, Q4, Q5, Q6                                                                                      | 2N5457      | 4   |
| 22 | R1, R15, R20, R21, R22, R23, R24, R25, R26, R27, R28, R29, R30, R31, R32, R33, R34, RV1             | 100K        | 18  |
| 23 | R2, R6, R9, R10, R11, R12, R18, R19, R36, RV2, RV4, RV5                                             | 10K         | 12  |
| 24 | R3, R4, R5, R7, R8, R13, R35                                                                        | 1K          | 7   |
| 25 | R14, R16                                                                                            | 1M          | 2   |
| 26 | R17                                                                                                 | 470K        | 1   |
| 27 | RV3, RV6, RV7, RV8                                                                                  | 50K         | 4   |
| 28 | U1, U4, U5, U6, U7, U8, U9, U10                                                                     | TL072       | 8   |
| 29 | U2                                                                                                  | CD40106     | 1   |
| 30 | U3                                                                                                  | CA3086/3046 | 1   |