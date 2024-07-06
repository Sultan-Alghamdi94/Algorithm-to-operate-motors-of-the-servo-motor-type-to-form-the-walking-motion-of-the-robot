#include <Servo.h>

Servo hip_ServoLeft;
Servo kne_ServoLeft;
Servo ank_ServoLeft;
Servo hip_ServoRight;
Servo kne_ServoRight;
Servo ank_ServoRight;

int Current_Position = 1500;
int lift_Position = 1400;
int forward_Position = 1300;
int weightShift_Position = 1600;

void setup() {
 
  hip_ServoLeft.attach(9);     
  kne_ServoLeft.attach(10);
  ank_ServoLeft.attach(11);
  hip_ServoRight.attach(6);
  kne_ServoRight.attach(7);
  ank_ServoRight.attach(8);

  initializeServos();
}

void loop() {
  walk();
}

void initializeServos() {
  hip_ServoLeft.writeMicroseconds(Current_Position);
  kne_ServoLeft.writeMicroseconds(Current_Position);
  ank_ServoLeft.writeMicroseconds(Current_Position);
  hip_ServoRight.writeMicroseconds(Current_Position);
  kne_ServoRight.writeMicroseconds(Current_Position);
  ank_ServoRight.writeMicroseconds(Current_Position);
}

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

void moveLegForward(char leg) {
  if (leg == 'L') {
    hip_ServoLeft.writeMicroseconds(forward_Position);
  } else {
    hip_ServoRight.writeMicroseconds(forward_Position);
  }
}

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

void shiftWeightToLeg(char leg) {
  if (leg == 'L') {
    hip_ServoRight.writeMicroseconds(weightShift_Position);
  } else {
    hip_ServoLeft.writeMicroseconds(weightShift_Position);
  }
}

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
