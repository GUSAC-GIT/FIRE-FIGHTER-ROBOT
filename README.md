# FIRE-FIGHTER ROBOT

![](https://github.com/GUSAC-GIT/FIRE-FIGHTER-ROBOT/blob/master/images/fighter1.jpg)


> FIRE FIGHTER ROBOT

---

### Contents


- [Components](#components)
- [Description](#description)
- [Code](#code)
- [Team Info](#team-info)

---

## Components

- Arduino UNO
- Fire sensor or Flame sensor (3 Nos)
- Servo Motor (SG90)
- L293D motor Driver module
- Mini DC Submersible Pump
- Small Breadboard
- Robot chassis with motors (2) and wheels(2) (any type)
- A small can
- Connecting wires

[Back To The Top](#fire-fighter-robot)


## Description

According to National Crime Records Bureau (NCRB), it is estimated that more than 1.2 lakh deaths have been caused because of fire accidents in India from 2010-2014. Even though there are a lot of precautions taken for Fire accidents, these natural/man-made disasters do occur now and then. In the event of a fire breakout, to rescue people and to put out the fire we are forced to use human resources which are not safe. With the advancement of technology especially in Robotics it is very much possible to replace humans with robots for fighting the fire. This would improve the efficiency of firefighters and would also prevent them from risking human lives. Today we are going to build a Fire Fighting Robot using Arduino, which will automatically sense the fire and start the water pump
In this project, we will learn how to build a simple robot using Arduino that could move towards the fire and pump out water around it to put down the fire. It is a very simple robot that would teach us the underlying concept of robotics

We detect the direction of the fire we can use the motors to move near the fire by driving our motors through the L293D module. When near a fire we have to put it out using water. Using a small container we can carry water, a 5V pump is also placed in the container and the whole container is placed on top of a servo motor so that we can control the direction in which the water has to be sprayed. 

An IR Receiver (Photodiode) which is used to detect the fire. How is this possible? When fire burns it emits a small amount of Infra-red light, this light will be received by the IR receiver on the sensor module. Then we use an Op-Amp to check for change in voltage across the IR Receiver, so that if a fire is detected the output  pin (DO) will give 0V(LOW) and if the is no fire the output pin will be 5V(HIGH).



[Back To The Top](#fire-fighter-robot)

---


## Code

```
#include <Servo.h>
Servo myservo;
 
int pos = 0;    
boolean fire = false;
 
/*-------defining Inputs------*/
#define Left_S 9      // left sensor
#define Right_S 10      // right sensor
#define Forward_S 8 //forward sensor
 
/*-------defining Outputs------*/
#define LM1 2       // left motor
#define LM2 3       // left motor
#define RM1 4       // right motor
#define RM2 5       // right motor
#define pump 6
 
void setup()
{
  pinMode(Left_S, INPUT);
  pinMode(Right_S, INPUT);
  pinMode(Forward_S, INPUT);
  pinMode(LM1, OUTPUT);
  pinMode(LM2, OUTPUT);
  pinMode(RM1, OUTPUT);
  pinMode(RM2, OUTPUT);
  pinMode(pump, OUTPUT);
 
  myservo.attach(11);
  myservo.write(90); 
}
 
void put_off_fire()
{
    delay (500);
 
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, HIGH);
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, HIGH);
    
   digitalWrite(pump, HIGH); delay(500);
    
    for (pos = 50; pos <= 130; pos += 1) { 
    myservo.write(pos); 
    delay(10);  
  }
  for (pos = 130; pos >= 50; pos -= 1) { 
    myservo.write(pos); 
    delay(10);
  }
  
  digitalWrite(pump,LOW);
  myservo.write(90);
  
  fire=false;
}
 
void loop()
{
   myservo.write(90); //Sweep_Servo();  
 
    if (digitalRead(Left_S) ==1 && digitalRead(Right_S)==1 && digitalRead(Forward_S) ==1) //If Fire not detected all sensors are zero
    {
    //Do not move the robot
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, HIGH);
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, HIGH);
    }
    
    else if (digitalRead(Forward_S) ==0) //If Fire is straight ahead
    {
    //Move the robot forward
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, LOW);
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, LOW);
    fire = true;
    }
    
    else if (digitalRead(Left_S) ==0) //If Fire is to the left
    {
    //Move the robot left
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, LOW);
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, HIGH);
    }
    
    else if (digitalRead(Right_S) ==0) //If Fire is to the right
    {
    //Move the robot right
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, HIGH);
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, LOW);
    }
    
delay(300); //Slow down the speed of robot
 
     while (fire == true)
     {
      put_off_fire();
     }
}

```
[Back To The Top](#fire-fighter-robot)

---


---

## Team Info

Gusac Projects Team

[Back To The Top](#fire-fighter-robot)
