# PY32_RF_I2C_SSR_ControllerBoard
<img src="https://github.com/TomatoCube18/PY32_RF_I2C_SSR_ControllerBoard/blob/main/images/PY32_RF_I2C_SSR_Controller.jpg"  width="400" height="auto" />

## Description
The **Educational RF & I2C Single-Channel SSR Controller Board** allows students to safely control AC devices via a Solid State Relay (SSR). It features a PY32 ARM-based MCU, on-board AC to DC power supply, 433MHz ASK RF receiver, I2C Grove connectors (5v & 3v3), on-board speaker, RGB LED expansion, manual override switch, and an opto-isolated input. Reprogrammable via popular embedded programming tools such as Keil or Arduino, this provides hands-on learning in embedded systems, wireless control, and AC power switching with safety in mind.

<br>

## Board Features
<img src="https://github.com/TomatoCube18/PY32_RF_I2C_SSR_ControllerBoard/blob/main/images/PY32_RF_I2C_SSR_Controller_Top.jpg"  width="400" height="auto" /> <img src="https://github.com/TomatoCube18/PY32_RF_I2C_SSR_ControllerBoard/blob/main/images/PY32_RF_I2C_SSR_Controller_Bottom.jpg"  width="400" height="auto" />
- Main Processor: PY32F002AW15S Arm M0 Processor

- On-Board peripherals: 
  - 1x Power LED
  - 1x LED (PB0)
  - 1x 5v SSR output with LED Indicator (PB1)
  - 2x I2C Grove Connector, 5v & 3v3 (SDA-PF0, SCL-PF1)
  - 1x On-Board Speaker (PA9)
  - 1x RF Receiver (PA0)
  
- External Interface (2x4 IDC connector)
  - 1x RGB LED Output (PA2, PA6, PA7)
  
  - 1x External Switch Input (PA1)
  
  - 1x Opto-isolated Input (PA3)
  
    

External Interface (2x4 IDC Connector) Pinout:
```text
+----------------------------------+
|                                  |
|    R      B     SW     Ext_GND   |
|   VCC     G     GND    Ext_IN	   |
|           +==========+           |
+------------          ------------+
```
- Common Anode RGB LED -> VCC(Anode), R, G, B (Cathode)
- External Switch -> SW & GND (Active Low)
- Opto-isolated Input -> Ext_IN & Ext_GND (3v - 5v)


<br>

## Instruction
##### Arduino Instruction:
1. [Download and install the Arduino IDE](https://www.arduino.cc/en/Main/Software) (Personally prefer Legacy IDE)
2. Start the Arduino IDE
3. Go into Preferences
4. Put a Check on "compilation" under "show verbose output during:"
5. Add https://github.com/PY32Duino/Arduino-pack-json-ci/releases/download/Nightly/package_py32_index.json as an "Additional Board Manager URL"
6. Open the Boards Manager from the Tools -> Board menu and install "PY32 Arduino"
7. Select your PY32 board from the Tools -> Board menu



##### Arduino Blink Instruction:

1. Choose File > Examples > 01.Basics > Blink
2. Replace "LED_BUILTIN" with "PB0"
3. Hit on Compile ✅ (not Upload ➡️)
4. Pay close attention to the Console Log; towards the end of the log file, Arduino will show you the path to the compiled output ELF file. "Blink.ino.elf"



##### Programming the firmware:

1. We will be using a DAPLink adapter & PYOCD software to burn the firmware into the MCU.
2. Connect the DAPLink to the programming pins (VCC, DIO, CLK, RST & GND)
3. Download and Install Python3 
4. Open up the Terminal/Command Prompt with the proper PATH configured for Python3 & Install the PYOCD software with Pip, `$ pip3 install pyocd`
5. Unzip the PY32_ocd_Configuration.zip file in your working folder.
6. From your working folder, Use PYOCD to burn your "Blink.ino.elf" into the MCU. `$ pyocd flash -t PY32F002Ax5  --config ./Misc/pyocd.yaml [PATH]/Blink.ino.elf`
7. (Optional) Whenever you wish to erase the program flash on the MCU `$ pyocd erase -t PY32F002Ax5 --chip --config ./Misc/pyocd.yaml`
