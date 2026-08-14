# automated-color-sorting-conveyor
Arduino-based automated conveyor system designed to detect objects by color and automatically route them to the corresponding container.

<p align="center">
  <img src="images/prototype.jpg" width="700">
</p>

## Overview

The objective of this project was to design and build an automated sorting system capable of transporting objects, identifying their color, and separating them into different containers.

The prototype integrates sensors, servo motors, a stepper motor, mechanical components, and embedded software to create a complete automated material-handling process.

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
- Automatic object-flow control
- Arduino C/C++ programming
- Mechanical prototyping
- Hardware/software integration

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

## Mechanical Design

The conveyor structure was designed to transport individual objects through a color-detection area and toward three separate output containers.

Servo-actuated mechanisms were positioned along the conveyor to redirect red and green objects.

Blue objects continued through the conveyor toward the final container.

<p align="center">
  <img src="images/mechanical-design.png" width="800">
</p>

## How It Works

### 1. Conveyor Motion

A NEMA 17 stepper motor drives the conveyor belt.

The motor is controlled using an A4988 stepper driver.

The Arduino generates STEP pulses that control the movement of the motor.

### 2. Object Entry

A servo-controlled gate regulates the flow of objects so that only one object enters the sorting area at a time.

This prevents multiple objects from reaching the color sensor simultaneously.

### 3. Color Detection

The color sensor measures the reflected light from each object.

The firmware reads the red, green, and blue frequency components.

```text
Read Red Frequency
        |
        v
Read Green Frequency
        |
        v
Read Blue Frequency
        |
        v
Compare Calibrated Thresholds
        |
   +----+----+
   |    |    |
   v    v    v
  Red Green Blue
```

The measured values are compared against calibrated thresholds to determine the detected color.

## Sorting Logic

Depending on the detected color:

```text
RED   -> Activate Red Servo
GREEN -> Activate Green Servo
BLUE  -> Continue Forward
```

When a red or green object is detected, the corresponding sorting servo redirects the object toward its container.

Blue objects continue directly toward the final container.

## Object Confirmation

Ultrasonic sensors are installed near the output containers.

They confirm that the object successfully reached its destination.

Once an object is detected:

```text
Object detected in container
          |
          v
Reset sorting servo
          |
          v
Open entry gate
          |
          v
Allow next object
```

This creates a sequential sorting process and prevents multiple objects from interfering with each other.

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
Wait for Ultrasonic Detection
  |
  v
Confirm Object Arrival
  |
  v
Reset Sorting Mechanism
  |
  v
Allow Next Object
  |
  +-------------> Repeat
```

## Flowchart

<p align="center">
  <img src="images/flowchart.png" width="700">
</p>

## Electronic Design

The electronic system integrates the Arduino controller with the servo motors, color sensor, ultrasonic sensors, stepper motor, and motor driver.

<p align="center">
  <img src="images/electronic-diagram.png" width="800">
</p>

## Software

The control software was implemented using Arduino C/C++.

The firmware performs several main tasks:

- Stepper motor control
- RGB color measurement
- Color classification
- Servo positioning
- Ultrasonic distance measurement
- Object-flow sequencing

### Color Detection

The firmware reads each color channel separately.

```cpp
digitalWrite(S2, LOW);
digitalWrite(S3, LOW);
Rojo_Frec = pulseIn(sensorSalida, LOW);

digitalWrite(S2, HIGH);
digitalWrite(S3, HIGH);
Verde_Frec = pulseIn(sensorSalida, LOW);

digitalWrite(S2, LOW);
digitalWrite(S3, HIGH);
Azul_Frec = pulseIn(sensorSalida, LOW);
```

The measured values are then compared with threshold values to determine the detected color.

## Demo

The following demonstration shows the conveyor identifying and sorting colored objects.

<p align="center">
  <img src="images/demo.gif" width="700">
</p>

## Results

The prototype successfully integrated sensing, actuation, mechanical movement, and embedded control into an automated color-sorting system.

Objects were transported through the conveyor, identified according to color, and directed toward their corresponding output area.

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
- System troubleshooting

## Academic Context

Developed as an academic Automation project at the Universidad Autónoma de Nuevo León (UANL), Faculty of Mechanical and Electrical Engineering.
