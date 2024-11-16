### **Modification for Adjustable Triangle Wave Symmetry**

To add **adjustable symmetry control** for the triangle wave in your VCO design, you can modify the circuit to include a **potentiometer** that allows you to tweak the balance of the **resistor divider**. Here’s how to implement it:

#### **Step-by-Step Modification for Adjustable Triangle Wave Symmetry**

1. **Replace Resistor Divider with Potentiometer**:
   - Instead of using fixed resistors **R4** and **R5** for the voltage divider, replace them with a **single potentiometer (VR1)**.
   - Use a **10kΩ potentiometer (VR1)**, which will allow you to vary the resistance on either side of the divider and thus control the symmetry of the triangle wave.

2. **Wiring the Potentiometer**:
   - Connect the **middle wiper** of the potentiometer (VR1) to the **inverting input (-)** of **U2**.
   - Connect one of the **outer terminals** of VR1 to the **sawtooth input** (coming from the output of **U1A** through **R4**).
   - Connect the other **outer terminal** of VR1 to **ground**.

3. **Adjusting Symmetry**:
   - By adjusting the position of the **wiper** of the potentiometer, you can change the ratio between the resistance to the sawtooth input and the resistance to ground.
   - This adjustment changes how the op-amp processes the sawtooth input, allowing you to control the **linearity** of the triangle waveform.
   - When the wiper is in the center, the resistances are equal, resulting in a symmetric triangle wave. Moving the wiper in either direction will adjust the up-slope and down-slope, thus changing the symmetry.

4. **Adding Fixed Resistor for Range Control** (Optional):
   - You could add **fixed resistors (e.g., 1kΩ)** in series with each side of the potentiometer to limit the range of adjustment, preventing the wave from becoming too distorted.

#### **Revised Schematic Routing**

- **Sawtooth Wave Input**:
  - Connect the **sawtooth waveform** from the output of **U1A** to one of the **outer terminals** of the potentiometer **(VR1)**.
  - The other **outer terminal** of **VR1** should be connected to **ground**.
- **Inverting Input of U2**:
  - Connect the **middle wiper** of the potentiometer **(VR1)** to the **inverting input (-)** of the op-amp **U2**.
  - The **feedback resistor (R6)** should remain between the **output of U2** and the **inverting input (-)**.

#### **Operational Notes**

- **Adjusting the potentiometer** allows you to change the symmetry of the triangle wave.
- This provides flexibility to achieve different harmonic content in the waveform, which can be useful in sound design.

#### **Summary**

- Replacing the fixed resistor divider (R4, R5) with a **10kΩ potentiometer** allows you to **manually adjust the symmetry** of the triangle wave.
- This modification provides more control over the waveform shape, making your VCO more versatile for different sonic characteristics.

Using this approach will enhance the versatility of your **Triangle Wave Shaper** by allowing for real-time control over the waveform symmetry, adding expressiveness to your synthesizer.

#### **Bill of Materials (BOM)**

| Part Description                  | Reference | Value     | Suggested Part Number | Quantity |
|-----------------------------------|-----------|-----------|-----------------------|----------|
| Op-Amp                            | U2        | TL072     | TL072CN               | 1        |
| Potentiometer (Symmetry Control)  | VR1       | 10kΩ      | Linear Taper          | 1        |
| Fixed Resistors (Optional)        | R4, R5    | 1kΩ       | 1/4W, 1% Tolerance    | 2        |
| Feedback Resistor                 | R6        | 10kΩ      | 1/4W, 1% Tolerance    | 1        |


### **Detailed Step-by-Step Connection Routing for Triangle Wave Shaper**

This step-by-step guide explains how to modify the **Triangle Wave Shaper** by adding a potentiometer to adjust the symmetry of the triangle waveform.

#### **Step-by-Step Routing**:

1. **Connecting the Sawtooth Wave Input**:
   - **Sawtooth Output from Integrator (U1A)**:
     - Locate the **output pin of U1A** (the previous integrator op-amp stage) where the **sawtooth waveform** is generated.
     - Connect this sawtooth output to **one of the outer terminals** of the **potentiometer (VR1, 10kΩ)**. This terminal will provide the varying input voltage to help shape the triangle wave.

2. **Grounding the Potentiometer**:
   - **Ground Connection for VR1**:
     - Connect the **other outer terminal** of **VR1** to **ground**. This sets a reference point for adjusting the symmetry, which will allow for changes in the linearity of the triangle waveform.

3. **Connecting the Potentiometer Wiper**:
   - **Middle Wiper of Potentiometer (VR1)**:
     - Connect the **middle wiper** of the potentiometer to the **inverting input (-)** of **op-amp U2**. This input will receive a variable voltage depending on the wiper's position, which influences how U2 shapes the input waveform.
     - The wiper acts as a variable resistor, altering the relative resistance between the sawtooth signal and ground.

4. **Adding Feedback Resistor to U2**:
   - **Feedback Resistor (R6)**:
     - Place a **10kΩ feedback resistor (R6)** between the **output of U2** and the **inverting input (-)**.
     - This feedback resistor helps determine the gain of the op-amp, ensuring that the output triangle waveform is correctly shaped based on the input and feedback configuration.

5. **Connecting Power to the Op-Amp (U2)**:
   - Ensure that the **op-amp U2 (TL072)** is powered correctly:
     - Connect **pin 8** of **U2** to the **+12V supply**.
     - Connect **pin 4** of **U2** to the **-12V supply**.
   - This provides the necessary bipolar power for the op-amp to handle the full range of the input signal.

6. **Output Triangle Wave**:
   - The **output of U2** will generate the **triangle waveform**.
   - You can take this output to the next stage, such as a **sine wave shaper**, or use it as a standalone output for further synthesis.

7. **Optional Fixed Resistors for Range Control**:
   - If you wish to **limit the range** of symmetry adjustment:
     - Place **1kΩ fixed resistors** in series with **each of the outer terminals** of the potentiometer.
     - These resistors will prevent the potentiometer from adjusting the symmetry too far, which could lead to distortion or unwanted wave characteristics.

#### **Summary of Connections**:

- **Sawtooth Input to VR1**: Connect the sawtooth waveform output from **U1A** to **one outer terminal** of the potentiometer (VR1).
- **Ground VR1**: Connect the **other outer terminal** of **VR1** to **ground**.
- **Potentiometer Wiper to U2**: Connect the **middle wiper** of the potentiometer to the **inverting input (-)** of the **op-amp U2**.
- **Feedback Resistor**: Connect a **10kΩ resistor (R6)** between the **output of U2** and the **inverting input (-)**.
- **Power U2**: Connect **+12V** to pin **8** and **-12V** to pin **4** of **U2**.

This routing guide ensures that the triangle wave can be adjusted for symmetry, giving you more flexibility in shaping the waveform and producing richer harmonic content. Let me know if you need further details or additional modifications!

