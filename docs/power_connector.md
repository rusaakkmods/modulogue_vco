### **Eurorack Power Connector Improvement**

#### **Schematic for Power Connector Improvement**
1. **Connector (J9)**:
   - 16-pin Eurorack power connector.
   - Pins are distributed as follows:
     - Pins 1, 2: **-12V**
     - Pins 3, 4, 5, 6, 7, 8: **GND**
     - Pins 9, 10: **+12V**
     - Pins 11, 12: **+5V**
     - Pins 13, 14: **CV IN (Optional)**
     - Pins 15, 16: **GATE (Optional)**

2. **Reverse Polarity Protection Diode**:
   - Use a **Schottky diode (D1)** such as **1N5819** in series with each voltage rail (+12V and -12V). This will protect against incorrect connection.
   - Connect the **anode** of the diode to the incoming power supply line and the **cathode** to the power rail input to the module.

3. **Filtering Capacitors**:
   - Add the following capacitors near the power pins of the connector:
     - **100nF ceramic capacitors (C1, C2)** between **+12V** and **GND**, and between **-12V** and **GND** for high-frequency filtering.
     - **47μF electrolytic capacitors (C3, C4)** between **+12V** and **GND**, and between **-12V** and **GND** for bulk decoupling to reduce power ripple.

4. **Pin Duplication**:
   - Multiple **GND pins** (pins 3 to 8) should be connected together to ensure proper grounding.
   - **+12V** and **-12V** pins (pins 1, 2, 9, 10) should also be duplicated for robust power distribution.
   - Ensure the **+5V**, **CV IN**, and **GATE** signals are clearly marked and routed for optional use.

#### **Bill of Materials (BOM)**

| Part Number | Description                                    | Quantity |
|-------------|------------------------------------------------|----------|
| J9          | 16-Pin Eurorack Power Connector               | 1        |
| D1, D2      | Schottky Diodes (1N5819 or equivalent)        | 2        |
| C1, C2      | 100nF Ceramic Capacitors                      | 2        |
| C3, C4      | 47μF Electrolytic Capacitors                 | 2        |
| Wires       | For Pin Connections                           | As needed|

#### **Detailed Guide of Pin Routing**
1. **Pins 1, 2 - -12V**:
   - Route both pins to the **-12V** power rail.
   - Connect a **Schottky diode (D1)** in series with the power line.
   - After the diode, add **C1 (100nF ceramic)** and **C3 (47μF electrolytic)** capacitors between **-12V** and **GND**.

2. **Pins 3, 4, 5, 6, 7, 8 - GND**:
   - Connect all GND pins together for a solid ground plane.
   - Ensure that **C1, C2, C3, C4** are all connected to this common GND plane.

3. **Pins 9, 10 - +12V**:
   - Route both pins to the **+12V** power rail.
   - Connect a **Schottky diode (D2)** in series with the power line.
   - After the diode, add **C2 (100nF ceramic)** and **C4 (47μF electrolytic)** capacitors between **+12V** and **GND**.

4. **Pins 11, 12 - +5V**:
   - Ensure proper decoupling with a **100nF capacitor** close to the +5V line.

5. **Pins 13, 14 - CV IN (Optional)**:
   - Route these pins to a **CV input** if applicable in your circuit.

6. **Pins 15, 16 - GATE (Optional)**:
   - Route these pins to the **Gate input** for any triggering function needed.

#### **Summary**
- Use **Schottky diodes** for reverse polarity protection on the power rails.
- Add **100nF ceramic** and **47μF electrolytic** capacitors for proper power filtering.
- Duplicate **GND**, **+12V**, and **-12V** pins for robustness and to reduce potential issues due to poor connections.
- Ensure proper routing for optional signals like **+5V, CV IN, and GATE** to provide flexibility for future modifications.

These improvements will help make your Eurorack module more reliable, with reduced power noise and greater resilience to accidental misconnection.

### **Eurorack Power Connector Improvement with Single LED Indicator**

#### **Schematic for Power Connector Improvement**
1. **Connector (J9)**:
   - 16-pin Eurorack power connector.
   - Pins are distributed as follows:
     - Pins 1, 2: **-12V**
     - Pins 3, 4, 5, 6, 7, 8: **GND**
     - Pins 9, 10: **+12V**
     - Pins 11, 12: **+5V**
     - Pins 13, 14: **CV IN (Optional)**
     - Pins 15, 16: **GATE (Optional)**

2. **Reverse Polarity Protection Diode**:
   - Use a **Schottky diode (D1)** such as **1N5819** in series with each voltage rail (+12V and -12V). This will protect against incorrect connection.
   - Connect the **anode** of the diode to the incoming power supply line and the **cathode** to the power rail input to the module.

3. **Filtering Capacitors**:
   - Add the following capacitors near the power pins of the connector:
     - **100nF ceramic capacitors (C1, C2)** between **+12V** and **GND**, and between **-12V** and **GND** for high-frequency filtering.
     - **47μF electrolytic capacitors (C3, C4)** between **+12V** and **GND**, and between **-12V** and **GND** for bulk decoupling to reduce power ripple.

4. **Pin Duplication**:
   - Multiple **GND pins** (pins 3 to 8) should be connected together to ensure proper grounding.
   - **+12V** and **-12V** pins (pins 1, 2, 9, 10) should also be duplicated for robust power distribution.
   - Ensure the **+5V**, **CV IN**, and **GATE** signals are clearly marked and routed for optional use.

5. **Power LED Indicator**:
   - Add a single **LED (LED1)** with a series resistor for power indication.
   - Connect **LED1** in series with a **1kΩ resistor (R1)** between the **+5V** power rail and GND to indicate power status.

#### **Bill of Materials (BOM)**

| Part Number | Description                                    | Quantity |
|-------------|------------------------------------------------|----------|
| J9          | 16-Pin Eurorack Power Connector               | 1        |
| D1, D2      | Schottky Diodes (1N5819 or equivalent)        | 2        |
| C1, C2      | 100nF Ceramic Capacitors                      | 2        |
| C3, C4      | 47μF Electrolytic Capacitors                 | 2        |
| LED1        | Power Indicator LED (+5V)                    | 1        |
| R1          | 1kΩ Resistor for LED current limiting        | 1        |
| Wires       | For Pin Connections                           | As needed|

#### **Detailed Guide of Pin Routing**
1. **Pins 1, 2 - -12V**:
   - Route both pins to the **-12V** power rail.
   - Connect a **Schottky diode (D1)** in series with the power line.
   - After the diode, add **C1 (100nF ceramic)** and **C3 (47μF electrolytic)** capacitors between **-12V** and **GND**.

2. **Pins 3, 4, 5, 6, 7, 8 - GND**:
   - Connect all GND pins together for a solid ground plane.
   - Ensure that **C1, C2, C3, C4** are all connected to this common GND plane.

3. **Pins 9, 10 - +12V**:
   - Route both pins to the **+12V** power rail.
   - Connect a **Schottky diode (D2)** in series with the power line.
   - After the diode, add **C2 (100nF ceramic)** and **C4 (47μF electrolytic)** capacitors between **+12V** and **GND**.

4. **Pins 11, 12 - +5V**:
   - Ensure proper decoupling with a **100nF capacitor** close to the +5V line.

5. **Pins 13, 14 - CV IN (Optional)**:
   - Route these pins to a **CV input** if applicable in your circuit.

6. **Pins 15, 16 - GATE (Optional)**:
   - Route these pins to the **Gate input** for any triggering function needed.

7. **Power LED Indicator**:
   - **+5V Indicator**: Connect **LED1** in series with **R1 (1kΩ resistor)** between **+5V** and **GND**.

#### **Summary**
- Use **Schottky diodes** for reverse polarity protection on the power rails.
- Add **100nF ceramic** and **47μF electrolytic** capacitors for proper power filtering.
- Duplicate **GND**, **+12V**, and **-12V** pins for robustness and to reduce potential issues due to poor connections.
- Ensure proper routing for optional signals like **+5V, CV IN, and GATE** to provide flexibility for future modifications.

These improvements will help make your Eurorack module more reliable, with reduced power noise and greater resilience to accidental misconnection.

