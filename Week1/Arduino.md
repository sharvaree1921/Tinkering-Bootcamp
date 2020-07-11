## Arduino
### Introduction
- Arduino = Hardware project + Arduino IDE + Arduino code (known as sketch). 
- Various types such as UNO,Mega,Nano,etc.
- Has Atmega328 microcontroller board.
- 16 Mhz ceramic resonator
- USB connection,power supply,ICSP Header,and a reset button
- GPIO(General purpose input - output pins):14 Digital pins(0 to 13) and 6 Analog pins(A0 to A5).
- Has 4 LEDs mounted on board - 2(Tx and Rx),1(Reset) , 1(on or off)

![Arduino](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/arduino.png)

- Two types of communication:(serial:one bit at a time,parallel:all bits at a simultaneously passed)
- Tx:transmitter,Rx:Receiver pins for Serial communication
- Where '~' sign is there ,they are PWM pins.
- Baud rate: Rate at which data is transferred through serial/parallel communication.

### How to write Arduino IDE code (Sketch) ?

Sketch is primarily based on C language and has its own syntax.It has by default two functions:

- void setup() : To initialize variables ,pins and setup serial monitor if needed.(Serial monitor is a window which displays our data or output).
- void loop() : Our main execution of code is done in this loop.Since it is a loop,it executes multiple times.

![Sketch](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/sketch.png)

Various functions used are listed below:
- pinMode(pin_no. , input/ouput) :Ex- pinMode(3,OUTPUT) which implies pin no. 3 gives us output.
- digitalWrite(pin_no. , high/low) :Ex-digitalWrite(13,HIGH) which implies arduino gives output as HIGH to pin 13.
- digitalRead(pin_no.) :Ex-digitalRead(13) which implies arduino reads the pin as high/low
- analogWrite(A5) :Outputs the analog value to A5 pin.
- analogRead(A0) : Read the analog value from A0.
- delay(t) :ex-delay(1000)implies stop or delay the execution of code by 1 sec.'t' is in millisecond.
- Serial.begin(9600) : setup the serial monitor,9600 is the baud rate,it can be any other value also.
- Serial.println("qwerty") : To print something on serial monitor

### PWM(Pulse Width Modulation)
PWM(Pulse Width Modulation) or PDM(Pulse Duration Modulation) is a method of reducing the avg power delivered by an electrical signal by effectively chopping it up
into discrete parts.

More simply,what if we want our LED to blink upto its 50% of highest intensity? This tweaking and tuning of intensity through digital pins is done by PWM pins.
- Duty_cycle = T_on/(T_on + T_off)
- Vout = Vmax * Duty_cycle
- analogWrite() function is used to give output to PWM pins(as we are deciding value somewhere between 0 and 1)
- A call to analogWrite() is on a scale of 0 to 255. 0 means 0 and 255 means 1.
- Ex: analogWrite(127) is 50% Duty cycle.

![pwm](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/pwm.png)

For writing arduino codes, a simulator is available known as tinkercad.

### Photoresistors
We know that ,when light falls on metal,electrons jump from valence band to conduction band,thus increasing conductivity or decreasing resistivity.
Similarly in photoresistors - Light_Intensity is inversly proportional to resistivity.

![photoresistor](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/photoresistor.png)

**Code for blinking of LED**

``` c++
int ledpin=8;
void setup()
{
 pinMode(ledpin,OUTPUT);
}
void loop()
{
 digitalWrite(ledpin,HIGH);
 delay(1000);
 digitalWrite(ledpin,LOW);
 delay(1000);
}
```
**Using PWM pins:**
```c++
byte pwmvalue=0;
void setup()
{
 pinMode(9,OUTPUT);
}
void loop()
{
 analogWrite(9,pwmvalue);
 delay(1000);
 pwmvalue++;
}

```
**Using Photoresistor**(click and move the slider to change the intensity of photoresistor)
```c++
void setup()
{
pinMode(A0,INPUT)
Serial.begin();
}
void loop()
{
Serial.println()analogRead(A0);
delay(10);
}
```
![Code](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/photoresistor-arduino.jpg)






