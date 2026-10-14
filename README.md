# Automated Powder & Fluid Dispenser

An Arduino-controlled machine that fills test tubes automatically. A conveyor brings each tube under the dispensers, an IR sensor detects it, a servo gate releases powder, and a pump adds liquid.

## How it works

The sketch (`CodeASF.ino`) runs one cycle each time the start button is pressed:

1. **Start:** wait for the push button (pulled low when pressed).
2. **Conveyor:** run the DC motor forward until the IR sensor sees a test tube.
3. **Stop:** halt the conveyor with the tube in position.
4. **Powder:** swing the servo gate 45° open, wait 5 seconds while powder flows, then close it.
5. **Fluid:** run the pump at full speed for 5 seconds.
6. **Count:** increment the tube counter and print it over serial. The loop is meant to stop after 5 tubes.

Progress is logged over serial at 9600 baud. The IR sensor reads `0` when an object is present and `1` when nothing is there.

## Hardware

| Component | Connection |
| --- | --- |
| Arduino board with Adafruit Motor Shield V1 | Shield stacked on the board |
| Conveyor DC motor | Motor shield port M1 |
| Liquid pump | Motor shield port M4 |
| Servo (powder gate) | Pin 9 |
| IR sensor | A0 |
| Start button | A1 (internal pull-up) |
| Status LED | A4 |
| Emergency stop button | A2 (planned, see Status) |

Mechanical parts were designed in SolidWorks.

## Software setup

1. Install the Arduino IDE.
2. Install the **Adafruit Motor Shield V1** library (provides `AFMotor.h`). `Servo.h` is included with the IDE.
3. Open `CodeASF.ino`, select your board and port, then upload.
