Whenever the Ultrasonic sensor(placed on top of the servo motor to rotate in 360 degrees) detects the distance , the buzzer beeps!

![radar bot](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/radar%20bot.jpg)

**Code for the Radar bot is as follows**
```c++
#include<Servo.h>
Servo s;

int pos;
int trigpin=13;
int echopin=12;
double d;

double findDistance() //creating 
{                  // function
  digitalWrite(13,LOW);
  delayMicroseconds(10);
  digitalWrite(13,HIGH);
  delayMicroseconds(10);
  digitalWrite(13,LOW);
  int time=pulseIn(echopin,HIGH);
  double distance=(0.0165*time);
  return(distance);
  }
void setup()
{
s.attach(7);
  Serial.begin(9600);
  pinMode(trigpin,OUTPUT);
  pinMode(echopin,INPUT);
}
void loop()
{
 for(pos=0;pos<=180;pos++)
 {
  s.write(pos);
  delay(15);
  d=findDistance();
   Serial.println(d);
   if(d<100)
   {
     tone(8,2000,15);
   }}
for(pos=180;pos>=0;pos--)
  {
    s.write(pos);
    delay(15);
    d=findDistance();
    Serial.println(d);
    if(d<100)
    {
      tone(8,2000,15);
    }
  }
  
}
```
