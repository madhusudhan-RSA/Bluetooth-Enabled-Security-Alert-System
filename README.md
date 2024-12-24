# Bluetooth-Enabled-Security-Alert-System

This project is an AVR-based door monitoring system that uses an IR sensor and a buzzer. The system allows remote control through Bluetooth communication, enabling or disabling monitoring based on received commands.

## Features
- **IR Sensor Monitoring**: Detects the state of a door (open/closed).
- **Buzzer Alert**: Activates a buzzer when the door is open (if monitoring is enabled).
- **Bluetooth Control**: Commands to toggle monitoring on and off using a Bluetooth device.
- **Asynchronous Communication**: Uses UART interrupt service routine (ISR) for efficient data handling.

## Hardware Requirements
- **ATmega328P** microcontroller (or compatible AVR microcontroller).
- **IR Sensor**: Connected to `PB2` (Pin 10 on Arduino Uno).
- **Buzzer**: Connected to `PB5` (Pin 13 on Arduino Uno).
- **Bluetooth Module**: Connected to UART pins (`RX` and `TX`) of the microcontroller.
- Supporting components (resistors, capacitors, etc.) for proper operation.

## Software Requirements
- AVR-GCC (for compiling the code).
- AVRDUDE (for uploading the code to the microcontroller).
- `UART.h` and `bluetooth.h` libraries (ensure these files are available in your project).

## Circuit Diagram
1. **IR Sensor**: Connect the signal pin of the IR sensor to `PB2`.
2. **Buzzer**: Connect the positive terminal of the buzzer to `PB5` through a resistor.
3. **Bluetooth Module**:
   - `RX` of the Bluetooth module to `TX` of the microcontroller.
   - `TX` of the Bluetooth module to `RX` of the microcontroller.
4. Ensure proper grounding and power connections for all components.

## Installation
1. Clone this repository:
   ```bash
   git clone <repository-url>
   ```
2. Open the project folder and compile the code using AVR-GCC:
   ```bash
   avr-gcc -mmcu=atmega328p -DF_CPU=16000000UL -o main.elf main.c
   ```
3. Upload the code to your microcontroller using AVRDUDE:
   ```bash
   avrdude -c <programmer> -p atmega328p -U flash:w:main.elf
   ```

## Usage
1. Power on the system.
2. Connect to the Bluetooth module from your device.
3. Send the following commands via Bluetooth:
   - `E`: Enable door monitoring.
   - `D`: Disable door monitoring.
4. When monitoring is enabled, the buzzer will activate if the door is open (IR sensor triggered).

## Code Overview
The program runs the following steps:
1. **Initialization**:
   - Sets up UART for Bluetooth communication.
   - Configures `PB5` as an output (for the buzzer) and `PB2` as an input (for the IR sensor).
2. **Main Loop**:
   - Checks for UART data and updates the monitoring state (`monitor_door`).
   - Monitors the IR sensor and controls the buzzer based on the monitoring state.
3. **Interrupt Service Routine**:
   - Captures UART data and processes commands asynchronously.

## Customization
- Modify `#define BUZZER` and `#define IR_SENSOR` to change the pins used for the buzzer and IR sensor.
- Update `set_bluetooth_name("RSA")` to change the Bluetooth device name.

## License
This project is licensed under the MIT License.

## Acknowledgments
This project was developed for monitoring door states and alerts with user control over Bluetooth.

---

For more details, contact the project maintainer.
