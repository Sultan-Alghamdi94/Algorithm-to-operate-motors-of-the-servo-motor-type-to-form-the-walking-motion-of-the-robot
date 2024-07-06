# Algorithm-to-operate-servo-motor-type-motors-to-move-the-robot's-legs

Intoduction:

This code controls a bipedal walking robot using six servo motors, three for each leg (hip, knee, and ankle). The robot performs a simple walking motion by lifting, moving forward, and placing down each leg in sequence. The code utilizes the Servo library to manage the servo motors, which are connected to an Arduino microcontroller. Below is a detailed description of the code, including its initialization, walking algorithm, and detailed function descriptions.

Description:

The code is structured into several functions to manage the walking motion of the robot. It includes the setup and loop functions, which are standard in Arduino sketches, as well as custom functions to initialize servos, lift legs, move legs forward, place legs down, and shift weight between legs.

Libraries and Servo Objects:

#include <Servo.h>

Servo hip_ServoLeft;
Servo kne_ServoLeft;
Servo ank_ServoLeft;
Servo hip_ServoRight;
Servo kne_ServoRight;
Servo ank_ServoRight;

The Servo library is included to control the servo motors.
Six Servo objects are declared to represent the hip, knee, and ankle servos for both the left and right legs.

Position Constants:
int Current_Position = 1500;
int lift_Position = 1400;
int forward_Position = 1300;
int weightShift_Position = 1600;

These constants define the positions for the servos in microseconds, representing different movements (initial, lift, forward, and weight shift positions).

Setup Function:

void setup() {
  hip_ServoLeft.attach(9);
  kne_ServoLeft.attach(10);
  ank_ServoLeft.attach(11);
  hip_ServoRight.attach(6);
  kne_ServoRight.attach(7);
  ank_ServoRight.attach(8);
  
  initializeServos();
}

The setup function attaches each servo to a specific pin on the Arduino.
It then calls initializeServos to set all servos to their initial positions.

Loop Function:

void loop() {
  walk();
}
The loop function continuously calls the walk function to keep the robot walking.

Initialize Servos Function:

void initializeServos() {
  hip_ServoLeft.writeMicroseconds(Current_Position);
  kne_ServoLeft.writeMicroseconds(Current_Position);
  ank_ServoLeft.writeMicroseconds(Current_Position);
  hip_ServoRight.writeMicroseconds(Current_Position);
  kne_ServoRight.writeMicroseconds(Current_Position);
  ank_ServoRight.writeMicroseconds(Current_Position);
}
This function sets all servos to the initial standing position (Current_Position).

Lift Leg Function:

void liftLeg(char leg) {
  if (leg == 'L') {
    hip_ServoLeft.writeMicroseconds(lift_Position);
    kne_ServoLeft.writeMicroseconds(lift_Position);
    ank_ServoLeft.writeMicroseconds(lift_Position);
  } else {
    hip_ServoRight.writeMicroseconds(lift_Position);
    kne_ServoRight.writeMicroseconds(lift_Position);
    ank_ServoRight.writeMicroseconds(lift_Position);
  }
}
This function lifts the specified leg by adjusting the hip, knee, and ankle servos to the lift_Position.

Move Leg Forward Function:

void moveLegForward(char leg) {
  if (leg == 'L') {
    hip_ServoLeft.writeMicroseconds(forward_Position);
  } else {
    hip_ServoRight.writeMicroseconds(forward_Position);
  }
}
This function moves the specified leg forward by adjusting the hip servo to the forward_position.

Place Leg Down Function:

void placeLegDown(char leg) {
  if (leg == 'L') {
    hip_ServoLeft.writeMicroseconds(Current_Position);
    kne_ServoLeft.writeMicroseconds(Current_Position);
    ank_ServoLeft.writeMicroseconds(Current_Position);
  } else {
    hip_ServoRight.writeMicroseconds(Current_Position);
    kne_ServoRight.writeMicroseconds(Current_Position);
    ank_ServoRight.writeMicroseconds(Current_Position);
  }
}

This function places the specified leg down by returning the hip, knee, and ankle servos to the Current_Position.

Shift Weight Function:

void shiftWeightToLeg(char leg) {
  if (leg == 'L') {
    hip_ServoRight.writeMicroseconds(weightShift_Position);
  } else {
    hip_ServoLeft.writeMicroseconds(weightShift_Position);
  }
}

This function shifts the robot's weight to the specified leg by adjusting the opposite hip servo to the weightShift_Position.

Walk Function:

void walk() {
  liftLeg('L');
  delay(500);
  moveLegForward('L');
  delay(500);
  placeLegDown('L');
  delay(500);
  shiftWeightToLeg('L');
  delay(500);

  liftLeg('R');
  delay(500);
  moveLegForward('R');
  delay(500);
  placeLegDown('R');
  delay(500);
  shiftWeightToLeg('R');
  delay(500);
}

The walk function coordinates the walking cycle by calling the lift, move, place, and weight shift functions for each leg in sequence.
Delays are used to provide time for the servos to move to their new positions.
