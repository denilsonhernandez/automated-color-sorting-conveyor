# automated-color-sorting-conveyor
Arduino-based automated conveyor system designed to detect objects by color and automatically route them to the corresponding container.
![Color Sorting Conveyor](images/prototype.jpg)

## Overview

The objective of this project was to design and build an automated sorting system capable of transporting objects, identifying their color, and separating them into different containers.

The prototype integrates sensors, servo motors, a stepper motor, and embedded software to create a complete automated material-handling process.

The system identifies three colors:

- Red
- Green
- Blue

Depending on the detected color, the Arduino controls the corresponding sorting mechanism.

## Key Features

- Automated conveyor system
- RGB color detection
- Red, green, and blue object classification
- Servo-controlled sorting mechanisms
- Stepper motor conveyor drive
- Ultrasonic object detection
- Object-flow control
- Arduino C/C++ programming
- Mechanical and electronic prototyping

## System Architecture

```text
                    Object
                      |
                      v
                Conveyor Belt
                      |
                      v
                 Color Sensor
                      |
                      v
                 +---------+
                 | Arduino |
                 +----+----+
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
      Red Servo   Green Servo   Direct Path
          |           |           |
          v           v           v
       Red Bin     Green Bin    Blue Bin
          |           |           |
          v           v           v
      Ultrasonic  Ultrasonic  Ultrasonic
        Sensor      Sensor      Sensor
```

## Hardware

- Arduino
- Color sensor
- NEMA 17 stepper motor
- A4988 stepper motor driver
- Servo motors
- Ultrasonic sensors
- Breadboard
- Jumper wires
- Bearings
- MDF structure
- Custom conveyor mechanism

## How It Works

### 1. Object Entry

The conveyor transports an object into the sorting area.

A servo-controlled gate regulates the flow so that only one object enters the classification stage at a time.

### 2. Color Detection

The color sensor measures the reflected light from the object.

The Arduino reads the red, green, and blue frequency components and compares them with calibrated threshold values.

```text
Read Red
   |
   v
Read Green
   |
   v
Read Blue
   |
   v
Compare Thresholds
   |
+--+-------+--+
|          |  |
v          v  v
Red      Green Blue
```

### 3. Sorting

Depending on the detected color:

```text
RED   -> Activate red sorting servo
GREEN -> Activate green sorting servo
BLUE  -> Continue toward the final container
```

### 4. Object Confirmation

Ultrasonic sensors detect when the object reaches its corresponding container.

After detection:

- The sorting servo returns to its initial position
- The entry gate opens
- The next object is allowed into the system

## Conveyor Motor Control

The conveyor belt is driven by a NEMA 17 stepper motor controlled through an A4988 driver.

The Arduino generates STEP signals to move the motor and control the conveyor.

## Control Sequence

```text
START
  |
  v
Start Conveyor
  |
  v
Allow Object Into Sorting Area
  |
  v
Read Color Sensor
  |
  +---- Red -----> Activate Red Servo
  |
  +---- Green ---> Activate Green Servo
  |
  +---- Blue ----> Continue Forward
  |
  v
Confirm Object Arrival
  |
  v
Reset Sorting Mechanism
  |
  v
Allow Next Object
```

## Electronic Design

![Electronic Diagram](images/electronic-diagram.png)

## Mechanical Design

![Mechanical Design](images/mechanical-design.png)

## Demo

![Conveyor Demo](images/demo.gif)

## Software

The control software was implemented using Arduino C/C++.

The firmware includes:

- Stepper motor control
- RGB color measurement
- Color classification
- Servo positioning
- Ultrasonic distance measurement
- Object-flow sequencing

## Results

The prototype successfully integrated sensing, actuation, mechanical movement, and embedded control into an automated color-sorting system.

## Skills Demonstrated

- Arduino
- C/C++
- Sensors and actuators
- Stepper motor control
- Servo motor control
- Color sensing
- Ultrasonic sensing
- Automation logic
- Mechanical prototyping
- Hardware/software integration
- Troubleshooting

## Academic Context

Developed as an academic automation project at the Universidad Autónoma de Nuevo León (UANL), Faculty of Mechanical and Electrical Engineering.
