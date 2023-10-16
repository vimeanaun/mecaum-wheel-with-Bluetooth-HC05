# mecaum-wheel-with-Bluetooth-HC05
https://youtu.be/J_mIawP_2Z4

#include<SoftwareSerial.h>
#include<AFMotor.h>

SoftwareSerial BT(0,1); // pin of TX and RX connection between Arduino and Bluetooth HC05 ( connect opposite pin );
char text;
int speed=255; // speed of the DCMotor; 

AF_DCMotor motor1(1, MOTOR12_1KHZ); 
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);

void setup(){
  Serial.begin(9600);
  BT.begin(9600);
  motor1.setSpeed(speed);
  motor2.setSpeed(speed);
  motor3.setSpeed(speed);
  motor4.setSpeed(speed);
}

void loop(){
  while (BT.available()>0){
      text=BT.read();
      Serial.println(text);

    if (text == '1'){
      turnleftbackward();
    }
    else if (text =='2'){
      backward();
    }
    else if (text == '3'){
      turnrightbackward();
    }
    else if (text == '4'){
      turnleft();
    }
    else if (text == '5'){
      stop();
    }
    else if (text == '6'){
      turnright();
    }
    else if (text == '7'){
      turnleftforward();
    }
    else if (text == '8'){
      forward();
    }
    else if (text == '9'){
      turnrightforward();
    }
    else if (text == 'e'){
      rotateright();
    }
    else if (text == 'q'){
      rotateleft();
    }
  }
    motor1.setSpeed(speed);
    motor2.setSpeed(speed);
    motor3.setSpeed(speed);
    motor4.setSpeed(speed);
}

void forward(){ //8
  motor1.run(FORWARD);
  motor2.run(FORWARD);
  motor3.run(FORWARD);
  motor4.run(FORWARD);
}

void backward(){ //2
  motor1.run(BACKWARD);
  motor2.run(BACKWARD);
  motor3.run(BACKWARD);
  motor4.run(BACKWARD);
}

void turnleft(){ //4
  motor1.run(FORWARD);
  motor2.run(BACKWARD);
  motor3.run(FORWARD);
  motor4.run(BACKWARD);
}

void turnright(){ //6
  motor1.run(BACKWARD);
  motor2.run(FORWARD);
  motor3.run(BACKWARD);
  motor4.run(FORWARD);
}

void stop(){ //5
  motor1.run(RELEASE);
  motor2.run(RELEASE);
  motor3.run(RELEASE);
  motor4.run(RELEASE);
}

void turnrightbackward(){ //3
  motor1.run(BACKWARD);
  motor2.run(RELEASE);
  motor3.run(BACKWARD);
  motor4.run(RELEASE);
}

void turnleftbackward(){ //1
  motor1.run(RELEASE);
  motor2.run(BACKWARD);
  motor3.run(RELEASE);
  motor4.run(BACKWARD);
}

void rotateleft(){ //q
  motor1.run(BACKWARD);
  motor2.run(FORWARD);
  motor3.run(FORWARD);
  motor4.run(BACKWARD);
}

void rotateright(){ //e
  motor1.run(FORWARD);
  motor2.run(BACKWARD);
  motor3.run(BACKWARD);
  motor4.run(FORWARD);
}

void turnleftforward(){ //7
  motor1.run(FORWARD);
  motor2.run(RELEASE);
  motor3.run(FORWARD);
  motor4.run(RELEASE);
}

void turnrightforward(){ //9
  motor1.run(RELEASE);
  motor2.run(FORWARD);
  motor3.run(RELEASE);
  motor4.run(FORWARD);
}
