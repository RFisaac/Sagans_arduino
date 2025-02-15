# Raspberry Pi Pico Learning Kit

## Overview
I wanted to put together an electronics kit for my cute love that would hopefully let her make nifty stuff but also give her a headstart on some grasshopper concepts. That way once she starts learning grasshopper she can do extra cool stuff with it. The ai tells me that grasshopper scripts use c#, so a lot of concepts should be transferrable.

Most tutorials and information online for the pico is for micropython or circuit python. So any googling or llm help will have to specifically be for the arduino sdk or C++. 

## Setup Instructions
According to people on the internet Earle Philhower's Arduino-Pico core, is heavily superior to the native Arduino SDK. The core allows you to program the Pico using C++ while maintaining the simplicity of the Arduino framework.

Installation and setup instructions can be found here:  
https://github.com/earlephilhower/arduino-pico

## Core Components
1. Raspberry Pi Pico W (2x)
   - RP2040 Microcontroller
   - Dual ARM Cortex-M0+ @ 133MHz
   - 264KB RAM
   - 2MB Flash Storage
   - 2.4GHz WiFi
   - Operating Voltage: 3.3V (5V input)
   - GPIO: 26 multi-function pins

## Additional Components & Specifications

### Display Modules
1. 0.96" OLED Display (SSD1306)
   - Resolution: 128x64 pixels
   - Interface: I2C
   - Operating Voltage: 3.3V/5V
   - Default I2C Address: 0x3C

2. 0.91" OLED Display (SSD1306)
   - Resolution: 128x32 pixels
   - Interface: I2C
   - Operating Voltage: 3.3V/5V
   - Default I2C Address: 0x3C

### LED Components
1. Standard LEDs
   - Operating Voltage: ~2V (varies by color)
   - Recommended Current: 20mA
   - Included Resistors: 330Ω (for 5V operation)
   
   Common LED Forward Voltages:
   | Color  | Forward Voltage | Current Limiting Resistor (5V) |
   |--------|----------------|-------------------------------|
   | Red    | 1.8-2.0V      | 220-330Ω                     |
   | Green  | 2.0-2.2V      | 220-330Ω                     |
   | Blue   | 3.0-3.3V      | 150-220Ω                     |
   | White  | 3.0-3.3V      | 150-220Ω                     |

2. NeoPixel Components
   a. LED Strips (WS2812B)
      - 8 pixels per strip (2 strips)
      - Operating Voltage: 5V
      - Data Input: 3.3-5V
      - Current Draw: ~60mA per pixel at full white
      - Data Protocol: Serial, 800kHz
   
   b. 24 LED NeoPixel Ring
      - Operating Voltage: 5V
      - Data Input: 3.3-5V
      - Current Draw: ~60mA per pixel at full white
      - Data Protocol: Serial, 800kHz
      - Total max current: ~1.44A at full white

### Input Devices
1. KY-040 Rotary Encoders (2x)
   - Operating Voltage: 5V
   - Output: Digital (2 phase)
   - Built-in Pushbutton
   - Infinite Rotation

2. 2-Axis Joystick
   - Potentiometer Value: 50kΩ (502F+)
   - Operating Voltage: 5V
   - Analog Output: 0-5V per axis

3. Momentary Buttons (14x)
   - Type: SPST (Single Pole, Single Throw)
   - Recommended Circuit: Pull-down resistor (10kΩ)

### Motor Control
1. L298N Motor Driver Modules (2x)
   - Operating Voltage: 5-35V
   - Logic Voltage: 5V
   - Maximum Current: 2A per channel
   - Channels: 2 per module

2. SG90 9g Micro Servos (2x)
   - Operating Voltage: 4.8-6V
   - Rotation Range: 180°
   - Speed: 0.1 sec/60° at 4.8V
   - Torque: 1.8 kg⋅cm at 4.8V

### Power Control
MOSFET Switch Modules (2x)
- Voltage Range: 5-36V
- Maximum Current: 15A (30A peak)
- PWM Frequency: 0-20kHz
- Logic Level: 3.3/5V compatible

### Environmental Sensors
DHT11 Temperature/Humidity Sensor
- Temperature Range: 0-50°C ±2°C
- Humidity Range: 20-80% ±5%
- Operating Voltage: 3.3-5.5V
- Sampling Rate: 1Hz (max)

### Power Monitoring
INA219 Current/Power Sensor
- Voltage Measurement: 0-26V
- Current Measurement: ±3.2A
- Resolution: 0.8mA
- Interface: I2C
- Default I2C Address: 0x40
- Power Measurement: High-side current sensing
- Bus/Shunt ADC Resolution: 12-bit

### Prototyping Materials
1. Mini Breadboards (2x)
2. Perfboard
   - For permanent circuit assembly
   - Requires soldering
3. Pico Breakout Board
   - Screw terminals for secure connections
   - Requires soldering for assembly
4. Jumper Wires (Male-to-Male, Male-to-Female)
5. Various Resistors

## Common Circuit Configurations

### Button Circuit
```
5V ----[Button]----+----[10kΩ]----GND
                   |
                   +----[GPIO Pin]
```

### LED Circuit
```
5V ----[220-330Ω]----[LED]----GND
```

### Servo Connection
```
Red   -> 5V
Brown -> GND
Orange/Yellow -> GPIO Pin
```

### I2C OLED Display
```
VCC -> 3.3V/5V
GND -> GND
SDA -> GPIO4 (Default I2C0 SDA)
SCL -> GPIO5 (Default I2C0 SCL)
```

### Power Management
1. TP4056 Type-C Battery Charger Modules (2x)
   - Input: USB Type-C 5V
   - Charging Current: 1A
   - Compatible Battery: 18650 Li-ion
   - Protection: Overcharge, over-discharge, short circuit
   - Status LEDs: Red (charging), Blue (full)

2. LM2596 Buck Converter Modules (2x)
   - Input Voltage: 4.5-40V
   - Output Voltage: 1.25-37V (adjustable)
   - Maximum Current: 3A
   - Efficiency: Up to 92%
   - Output ripple: <30mV

### INA219 Current Sensor
```
VCC    -> 3.3V
GND    -> GND
SDA    -> GPIO4 (Default I2C0 SDA)
SCL    -> GPIO5 (Default I2C0 SCL)
V+     -> Power Source (+)
V-     -> Load (+)
        -> Load (-)    -> Power Source (-)

Note: V+ and V- connect in series with the load's positive wire
      for high-side current measurement
```

## Power Requirements
- Total maximum current draw with all components:
  - NeoPixels: ~2.88A (48 pixels at full white)
  - OLED Displays: ~20mA each
  - Servos: ~250mA each under load
  - Other components: ~200mA combined
  - Recommended power supply: 5V 2A minimum

## Safety Notes
1. Always verify voltage levels before connecting components
2. Use appropriate current-limiting resistors with LEDs
3. Be careful not to exceed maximum current ratings of the Pico's GPIO pins (12mA per pin)
4. When using multiple servos or NeoPixels, consider using external power supply
5. Double-check I2C addresses if using both OLED displays simultaneously