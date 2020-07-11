## ESP32 / NodeMCU
- Very strong microcontroller compared to Arduino as it has inbuilt Wifi connection.
- 2 Dual Cores
- Wifi : 2.4 GHz(this is bandwidth that provides coverage at linger range but transmits data at slower speeds) upto 150 Mbps
- Bluetooth : BLE and legacy Bluetooth
- Architecture : 32 bits
- Clock Frequency : 240 MHz
- RAM : 512 kB

![esp](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/esp.jpg)

**ESP32s-DEVKIT v1-DOIT**
- 18 ADC channels :8 ADC1 channels + 10 ADC2 channels
- 3 SPI Interfaces
- 2 'I2C' interfaces
- 16 PWM output channels
- 2 'I2S' interfaces
- 2 DAC channels
- 10 capacitive sensing GPIO pins (all pins except 3.3 V)

![esp1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/esp1.png)

**More about ESP**

- Arduino has so much limitations on number of PWM and ADC pins.
- Arduino's assigned value is from 0V to 5V whereas for ESP it is from 0V to 3.3V.
- Resolution for Arduino is upto 10 bits(0 to 1023) whereas for ESP it is upto 12 bits(0 to 4095).The voltage measured is then assigned to value between 0 and 4095
  where 0 is 0V and 4095 is 3.3V.
- Input only pins are ranked higher.
- UART pins are for transferring and receiving data.
- SPI pins are used for serial monitor functions.
- Max current through GPIO pins is 40mA.

**More about ADC channels**

![adc](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/adc.png)

- This behavior means that your ESP32 is not able to distinguish 3.3 V from 3.2 V. You’ll get the same value for both voltages: 4095.
- The same happens for very low voltage values: for 0 V and 0.1 V you’ll get the same value: 0. You need to keep this in mind when using the ESP32 ADC pins.

**More about GPIO pins**
1. Input only pins : GPIOs 34 to 39 (4 pins)
2. SPI flash (not recommended for use) : GPIOs 6 to 11 (6 pins)
3. DAC : DAC1 - GPIO 25
       : DAC2 - GPIO 26
4. PWM : 16 independent channels
       : All pins can be used except for 34 to 39(Input only pins).

### Programming ESP32 with Arduino IDE

#### 1. Glowing a LED:
- By ESP32 ,we can control LED via Wifi.
- Wifi helps our system to connect from anywhere in the world as it gives us access to the internet facility.
- For writing code,we have to import some libraries into Arduino IDE.
- Code same as Arduino(just change the pin no.).
- Make sure that you have changed the board name and port no. in Arduino IDE. 

![esp2](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/ESP32_LED.png)

```c++
int Led = 21; // you have to use pin number written after D in your board

void setup() {
  pinMode(Led,OUTPUT); // setting up your pin in output mode
}

// loop code runs again and again and makes your led blinks

void loop() {
  digitalWrite(Led,HIGH);   // turning on the led
  delay(1000);   // glows led for 1 sec
  digitalWrite(Led,LOW);   // turing off the led
  delay(1000);  //  turns off your led for one sec
}

```

#### 2. Code for Fetching data from internet via ESP module :

```c++
#include<Wifi.h>
#include<WifiClient.h>     //importing required libraries
#include<WebServer.h>
#include<HTTPClient.h>

WebServer server ( 80 );  // creating a variable for our webserver.Here 80 is the port number(this is by default) that we are using to ensure that no mismatching occurs

const char* ssid     = "Aniket";   // wifi name
const char* password = "123456712"; // wifi password

int LEDPIN = 21;   // led pin number


void setup() 
{

  pinMode(LEDPIN, OUTPUT);     // setting led as output
  digitalWrite(LEDPIN, LOW);   // initializing led as low
  Serial.begin(9600);   // setting up serial monitor


  connectToWifi();   //calling the function connectToWifi()

}

void connectToWifi()
{
  WiFi.enableSTA(true);   // enabling wifi port
  
  delay(2000);   //y=this is imp as wifi requires some time to setup

  WiFi.begin(ssid, password);   // connnecting to wifi
  
  while (WiFi.status() != WL_CONNECTED) { 
        delay(500);
        Serial.print(".");   // printing "." till wifi is not connected
    }
  Serial.println("");
  Serial.println("WiFi connected");   
  Serial.println("IP address: ");  
  Serial.println(WiFi.localIP());  // wifi connected and printing it's IP address
}



void loop(){
  if(WiFi.status() == WL_CONNECTED){
     digitalWrite(LEDPIN, HIGH);  // glowing the led if wifi is connected
     HTTPClient http;   // making a variable for interacting to any webpage
     http.begin("https://api.thingspeak.com/apps/thinghttp/send_request?api_key=T9IX646NPLSLF9QK");  // connecting with this webpage.For this thingspeak url see youtube video of TL
     int httpCode = http.GET(); // get function sends the request to access the url and if the permission is given,then it returns some positive value.
     if(httpCode>0){ // condition written is if connected
      String confirmedCases = http.getString();   // storing confirmed cases
      confirmedCases = confirmedCases.substring(4,10);  // triming it
      Serial.print("Confirmed Cases in Bihar - ");
      Serial.println(confirmedCases); // printing on serial monitor
           }
  }
  else{ /// if wifi gets disconnected the whole  wifi will be again connected by the same process
     digitalWrite(LEDPIN, LOW);
     WiFi.begin(ssid, password);
     while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
     }
    Serial.println("");
    Serial.println("WiFi connected");
    Serial.println("IP address: ");
    Serial.println(WiFi.localIP());
  }
}


```

#### 3.Using ESP 32 as a server.

```c++
#include <WiFi.h>
#include <WiFiClient.h>
#include <WebServer.h>
#include <Esp32WifiManager.h>
// libraries used


// this is the webpage we are going to create
const char MAIN_page[] PROGMEM = R"=====(
<!DOCTYPE html>
<html lang=en-EN><head><meta http-equiv='refresh' content='60'/>
<head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">
<body>
 
<h2>Tinkerers' Laboratory<h2>
<h3>Webpage Esp32</h3>
 
<form action="/action_page">
  <ul><li>LED

  <INPUT type='radio' name='LED' value='1'>ON
  <INPUT type='radio' name='LED' value='0'>OFF</li></ul>
  <input type="submit" value="Submit">
</form> 
 
</body>
</html>
)=====";

// form action is the action taken place when any action is given by the user


int LEDPIN = 21;   // led pin number
WebServer server(80);  // creating a variable for our webserver


// handleroot initializes the webpage
void handleRoot() {
  String s = MAIN_page;
  server.send(200, "text/html", s);
}


// handleform handles the action by the user
void handleForm() {
  String LEDValue;
  LEDValue = server.arg("LED"); // value given by user on selecting the radio button
  Serial.println("Set GPIO "); 
  Serial.println(LEDValue);
  
  if ( LEDValue == "1" ) {
    digitalWrite(LEDPIN, HIGH); // if value is 1 turn on the led
    String s = MAIN_page;  // again setting the webpage
    server.send ( 200, "text/html", s );
  }
  else if( LEDValue == "0" ) 
  {
    digitalWrite(LEDPIN, LOW); // if value is 0 turn off the led
    String s = MAIN_page;  // again setting the webpage
    server.send ( 200, "text/html", s );
  } else 
  {
    Serial.println("Error Led Value");  // in any other case if some error happened
  }
}
void setup(void){
  Serial.begin(9600);  // setting up serial monitor
  pinMode(LEDPIN, OUTPUT);   // setting led as output
  digitalWrite(LEDPIN, LOW);   // initializing led as low
 
  Serial.println("Setting WiFi .... ");
  boolean result = WiFi.softAP("ESP32", "12345678");   // creating a wifi
  if(result == true)
  {
    Serial.println("Ready");  // if wifi is created
  }
  else
  {
    Serial.println("Failed!");  // if wifi is not created
  }
 
  server.on("/", handleRoot);    // initializes handleRoot() function
  server.on("/action_page", handleForm);  // initalizes handleForm() function
 
  server.begin();   // starting the server
  Serial.println("HTTP server started");
}
void loop(void){
  server.handleClient();   // giving the server access to handle the user
}

```

#### 4.Capacitive demo (using capacitive touch pins)

```c++
// set pin numbers
const int touchPin = 4; 
const int ledPin = 21;

// change with your threshold value
const int threshold = 20;
// variable for storing the touch pin value 
int touchValue;

void setup()
{
  Serial.begin(115200);
  delay(1000); // give me time to bring up serial monitor
  // initialize the LED pin as an output:
  pinMode (ledPin, OUTPUT);
}
void loop(){
  // read the state of the pushbutton value:
  touchValue = touchRead(touchPin);
  Serial.print(touchValue);
  // check if the touchValue is below the threshold
  // if it is, set ledPin to HIGH
  if(touchValue < threshold){
    // turn LED on
    digitalWrite(ledPin, HIGH);
    Serial.println(" - LED on");
  }
  else{
    // turn LED off
    digitalWrite(ledPin, LOW);
    Serial.println(" - LED off"); setup(){
  S
  }
  delay(500);
}
```

### Other References
- [intro to ESP32](https://randomnerdtutorials.com/getting-started-with-esp32/)
- [Pinout reference](https://randomnerdtutorials.com/esp32-pinout-reference-gpios/)
- [ESP32 ADC](https://randomnerdtutorials.com/esp32-adc-analog-read-arduino-ide/)
- [Installing ESP32 library](https://www.youtube.com/watch?v=1XjwH4Gckpk)
- [Capacitive touch demo](https://youtu.be/40tyJfvpcxw)
- [Full session by TL](https://www.youtube.com/watch?v=9pgmtAK7dYA&feature=youtu.be )


