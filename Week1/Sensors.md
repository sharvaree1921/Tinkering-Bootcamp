## Sensors

### IR Sensor
InfraRed(IR) sensor helps us to detect whether there is an object in front of it or not. It has builtin IR transmitter and IR receiver that sends out IR energy 
and looks for reflected IR energy to detect the presence of any obstacle in front of the sensor module. The module has an on board potentiometer that lets
the user adjust detection range. The sensor has very good and stable response even in ambient light or in complete darkness.

![IR](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/IR.png)

**Code for IR Sensor**
```c++
int irObstaclePin = 2;   // This is our input pin
int Obstacle = HIGH;     // HIGH MEANS NO OBSTACLE
void setup() 
{
 pinMode(irObstaclePin, INPUT);   // Initializing Input pin
 Serial.begin(9600);       // Initializing serial monitor
}
void loop() 
{
 Obstacle = digitalRead(irObstaclePin);  //This reads the input
 if (Obstacle == LOW)
 {
   // If the input is low it means there is an obstacle
   Serial.println("OBSTACLE!!, OBSTACLE!!");  
 }
 else
 {
   // else there is no obstacle
   Serial.println("clear");
 }
 delay(200); 
}

```
![IR1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/Connection%20Diagram.png)

Link for video tutorials-
1. [Tutorial 1](https://youtu.be/zq51oZMzyP0)
2. [Tutorial 2](https://youtu.be/tUTr58fq308)

### PIR Sensor

Passive InfraRed (PIR) sensors are widely used in daily life. They are a key component in motion detection and can be used for security systems, automatic doors,
or automatic light control. They are commonly used to detect humans. For example, when someone is detected in a specified area an alarm may be triggered or
a specific room may be lit. 

![pir](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/pir.jpg)

When an object, such as a person, passes in front of the background, such as a wall, the temperature at that point in the sensor's field of view will rise from 
room temperature to body temperature, and then back again. The sensor converts the resulting change in the incoming infrared radiation into a change in the
output voltage, and this triggers the detection. Objects of similar temperature but different surface characteristics may also have a different infrared emission 
pattern, and thus moving them with respect to the background may trigger the detector as well.

![pir1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/pircomp.jpg)

_More about PIR Sensor_
- It has inbuilt pyroelectric sensor which genertes energy when exposed to heat i.e. when humans will get in the range of sensor
[P.S. Humans radiate heat energy in form of infrared radiations],it will detect infrared radiations.
- The word 'Passive' is used as it doesn't directly detect any object but it detects radiations.

**PIR Sensor Code**
```c++
int calibrationTime = 30; //the time when the sensor outputs a low impulse
long unsigned int lowIn;
//the amount of milliseconds the sensor has to be low
//before we assume all motion has stopped
long unsigned int pause = 5000;
boolean lockLow = true;
boolean takeLowTime;
int pirPin = 12;    //the digital pin connected to the PIR sensor's output
int ledPin = 13;
////
//SETUP
void setup(){
  Serial.begin(9600);
  pinMode(pirPin, INPUT);
  pinMode(ledPin, OUTPUT);
  digitalWrite(pirPin, LOW); //give the sensor some time to calibrate
  Serial.print("calibrating sensor ");
  for(int i = 0; i < calibrationTime; i++)
  {
  Serial.print(".");
  delay(1000);
  }
  Serial.println(" done");
  Serial.println("SENSOR ACTIVE");
  delay(50);
}
//LOOP
void loop(){
  if(digitalRead(pirPin) == HIGH)
  {
   digitalWrite(ledPin, HIGH);   //the led visualizes the sensors output pin state
   if(lockLow)
   {
    lockLow = false;
    Serial.println("---");
    Serial.print("motion detected at ");
    Serial.print(millis()/1000);
    Serial.println(" sec");
    delay(50);
   }
  takeLowTime = true;
  }
if(digitalRead(pirPin) == LOW)
{
  digitalWrite(ledPin, LOW);  //the led visualizes the sensors output pin state
  if(takeLowTime)
  {
   lowIn = millis();          //save the time of the transition from high to LOW
   takeLowTime = false;       
  }
//if the sensor is low for more than the given pause,
//we assume that no more motion is going to happen
  if(!lockLow && millis() - lowIn > pause){
//makes sure this block of code is only executed again after
//a new motion sequence has been detected
   lockLow = true;
   Serial.print("motion ended at ");      //output
   Serial.print((millis() - pause)/1000);
   Serial.println(" sec");
   delay(50);
}
}
}

```

**Resources**
1. [Principle and components of PIR sensor]( https://www.youtube.com/watch?v=6Fdrr_1guok)
2. [Code and connection with arduino]( https://create.arduino.cc/projecthub/Raushancpr/arduino-with-pir-0eab77)

### Active Buzzer Module
Active Buzzer module is an electromechanical audio signaling device which is used to produce a fixed when high input is given by an arduino.
As a type of electronic buzzer with integrated structure, buzzers are widely used in computers, printers, photocopiers, alarms, electronic toys, automotive 
electronic devices, telephones, timers and other electronic products for voice devices.
For example, you may use it as an alarm when the pir sensor detects  a signal and sends it to the arduino.

![abm](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/buzzercircuit.jpg)

```c++
int buzzPin = 12;   // This is our output pin
void setup() 
{
 pinMode(buzzPin, OUTPUT);   // Initializing output pin
}
void loop() 
{
 digitalWrite(buzzPin, LOW); // Beeping ON
 delay(1000);
 digitalWrite(buzzPin, HIGH); // Beeping OFF
 delay(1000);
}
```
Try out all of these modules and sensors as it is very basic and useful for tinkering in day-to-day life. You can try making different tones by changing the
delay time, and also can make it beep upon change in signal from other sensors.You can also read and try out other modules as well as sensors.

[Video tutorial](https://www.youtube.com/watch?v=UepyY4jF0qg)

### Servo Motors
- Servo motors are great devices that can turn to a specified position.Usually, they have a servo arm that can turn 180 degrees.
- Servos are clever devices. Using just one input pin, they receive the position from the Arduino and they go there. 
- Internally, they have a motor driver and a feedback circuit that makes sure that the servo arm reaches the desired position. 
- But what kind of signal do they receive on the input pin?It is a square wave similar to PWM. Each cycle in the signal lasts for 20 milliseconds and for most of    the time, the value is LOW.
- At the beginning of each cycle, the signal is HIGH for a time between 1 and 2 milliseconds. At 1 millisecond it represents 0 degrees and at 2 milliseconds it represents 180 degrees. In between, it represents the value from 0–180. This is a very good and reliable method. The graphic makes it a little easier to understand.

![servo1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/servo1.jpg)

![servo](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/servo.jpg)

**Code for rotating servo 180 degrees back and forth

```c++
#include <Servo.h>  //this library is necessary to 
                //Include in your code    
int pos = 0;
Servo servo_9;     //creating the object of the servo
void setup()
{
  servo_9.attach(9); //To which pin is the signal wire      
}               //attached to arduino pin
void loop()
{
 // sweep the servo from 0 to 180 degrees in steps of 1 degrees
or (pos = 0; pos <= 180; pos += 1) {
    // tell servo to go to position in variable 'pos'
    servo_9.write(pos);
    // wait 15 ms for servo to reach the position
    delay(15); // Wait for 15 millisecond(s)
  }
  for (pos = 180; pos >= 0; pos -= 1) {
    // tell servo to go to position in variable 'pos'
    servo_9.write(pos);
    // wait 15 ms for servo to reach the position
    delay(15); // Wait for 15 millisecond(s)
  }
}
```
[Video tutorial](https://www.youtube.com/watch?v=aFHu65LiFok&list=PLGs0VKk2DiYw-L-RibttcvK-WBZm8WLEP&index=31&t=0s )

### Ultrasonic Sensor

 It is a sensor used to detect distances using the principle of reflection of sound waves. It converts electrical energy into acoustic waves and vice versa. It has 4 pins:-
 
 1. Vcc:Powers the sensor,typically +5V.
 2. Trigger:Input Pin.Trigger pin is usually to be kept high for 10 microseconds to initialize measurement by sending US wave.
 3. Echo:Output pin.This pin goes high for a period of time which will be equal to the time taken for the US wave to return back to the sensor.
 4. Gnd:0V
 
 ![ultrasonic](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/Ultrasonic-sensor-pinout.png)
 
 _Working_
 - The microcontroller sends a trigger signal to the ultrasonic sensor. The duty cycle of this trigger signal is 10µS for the HC-SR04 ultrasonic sensor.
 - When triggered, the ultrasonic sensor generates eight acoustic (ultrasonic) wave bursts and initiates a time counter. 
 - As soon as the reflected (echo) signal is received, the timer stops.
 - The output of the ultrasonic sensor is a high pulse with the same duration as the time difference between transmitted ultrasonic bursts and the received echo signal.
 
 P.S.-Arduino's output means Sensor's input
 
 ![ultrasonic1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/ultrasonic.jpg)
 
 **Code for ultrasonic sensor**
 ```c++
Int trigpin=11;                     //defining trigger pin
int echopin=10;        //defining echopin

void setup()
{
  pinMode(11,OUTPUT);  //trigger pin is output pins
  pinMode(10,INPUT);     //echopin is input pin
  Serial.begin(9600);     //setting up serial monitor
}

void loop()
{
  digitalWrite(trigpin,LOW); 
  delayMicroseconds(10);
  digitalWrite(trigpin,HIGH);    //creates US bursts
  delayMicroseconds(10);
  digitalWrite(trigpin,LOW);
  int time=pulseIn(echopin,HIGH); //measuring time
  Serial.println(time*0.0165); //look below
  delay(10); //delay for 10 milliseconds
}

// The pulseIn measures time duration in microseconds hence we need to multiply 10-6 but we need to measure the distance in cm hence we need to multiply by 102 and we have traversed twice the distance hence we need to divide by 2.
We are taking the speed of sound approximately equal to 330m/s. Hence we get the factor of 0.0165.

 ```
 [Ultrasonic Sensor](https://www.youtube.com/watch?v=M-UKXCUI0rE&list=PLGs0VKk2DiYw-L-RibttcvK-WBZm8WLEP&index=54&t=0s)
