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


