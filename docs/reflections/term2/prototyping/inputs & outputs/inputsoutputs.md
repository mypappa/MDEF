so far in mdef we have been using some basic inputs, like microphones and outputs, such as led lights and buzzers.  

for this task which once again was in collaboration with my roommate Korbi, we experimented with two ESP feather boards at home. 

we divided the task into the following steps: first, we set a board with a led light and a button controlling the led. Then we set another board with a light sensor reading light levels in realtime. then it was time to make a manual morse code transmitter..  

## button   
<img src="../button.gif" alt="drawing" width="450" />   



<details> 

```cpp
/*
  Debounce

  Each time the input pin goes from LOW to HIGH (e.g. because of a push-button
  press), the output pin is toggled from LOW to HIGH or HIGH to LOW. There's a
  minimum delay between toggles to debounce the circuit (i.e. to ignore noise).

  The circuit:
  - LED attached from pin 13 to ground
  - pushbutton attached from pin 2 to +5V
  - 10 kilohm resistor attached from pin 2 to ground

  - Note: On most Arduino boards, there is already an LED on the board connected
    to pin 13, so you don't need any extra components for this example.

  created 21 Nov 2006
  by David A. Mellis
  modified 30 Aug 2011
  by Limor Fried
  modified 28 Dec 2012
  by Mike Walters
  modified 30 Aug 2016
  by Arturo Guadalupi

  This example code is in the public domain.

  http://www.arduino.cc/en/Tutorial/Debounce
*/

// constants won't change. They're used here to set pin numbers:
const int buttonPin = 12;    // the number of the pushbutton pin
const int ledPin = 13;      // the number of the LED pin

// Variables will change:
int ledState = HIGH;         // the current state of the output pin
int buttonState;             // the current reading from the input pin
int lastButtonState = LOW;   // the previous reading from the input pin

// the following variables are unsigned longs because the time, measured in
// milliseconds, will quickly become a bigger number than can be stored in an int.
unsigned long lastDebounceTime = 0;  // the last time the output pin was toggled
unsigned long debounceDelay = 50;    // the debounce time; increase if the output flickers

void setup() {
  pinMode(buttonPin, INPUT);
  pinMode(ledPin, OUTPUT);

  // set initial LED state
  digitalWrite(ledPin, ledState);
}

void loop() {
  // read the state of the switch into a local variable:
  int reading = digitalRead(buttonPin);

  // check to see if you just pressed the button
  // (i.e. the input went from LOW to HIGH), and you've waited long enough
  // since the last press to ignore any noise:

  // If the switch changed, due to noise or pressing:
  if (reading != lastButtonState) {
    // reset the debouncing timer
    lastDebounceTime = millis();
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    // whatever the reading is at, it's been there for longer than the debounce
    // delay, so take it as the actual current state:

    // if the button state has changed:
    if (reading != buttonState) {
      buttonState = reading;

      // only toggle the LED if the new button state is HIGH
      if (buttonState == HIGH) {
        ledState = !ledState;
      }
    }
  }

  // set the LED:
  digitalWrite(ledPin, ledState);

  // save the reading. Next time through the loop, it'll be the lastButtonState:
  lastButtonState = reading;
}
```
</details>

## light sensor   

next step: connect the light sensor and print a light graph on the serial plotter  

<img src="../light sensor.gif" alt="drawing" width="450" /> 
<img src="../light graph.gif" alt="drawing" width="450" />   

<details>

```cpp
int R2 = 10000;
float VIN = 3.0;

void setup() {
  Serial.begin(9600);
}

void loop() {

  // read the input on analog pin 0:
  int sensorValue = analogRead(A3);

  // Convert the analog reading (which goes from 0 - 1023) to a voltage (0 - 5V):
  float voltage = sensorValue * (3.0 / 1023.0);

  // Get the value of R1
  int ldr = ((R2 * VIN) / voltage) - R2;

  // print out the value you read:
  Serial.println(sensorValue);
  Serial.print("voltage: ");
  Serial.println(voltage);
  Serial.print("LDR value: ");
  Serial.println(ldr);
}
```
</details>

## morse code   

<img src="../morse.gif" alt="drawing" width="450" />   

last and most challenging part: encoding different types of messages given by the light to a binary 'morse' type with "longs" and "shorts".
we have two boards that we need to bring together: one with the light sensor that prints graphs and another with a button and a led light. we need to make the sensor 'read' the led light (controlled by us) and print messages accordingly. 
since the sensor is too sensitive for the average luminosity of our workspace (kitchen), in order to make it work we had to turn off the lights. and this was our first message. once we shut the lights off, we get a congratulating message that we did a good job so far.. much needed to go on. then, time for the led to shine! we push the button that controls the led and here we have two possible outputs: for a duration longer than a second (1000ms) we have a long and for less than a second, a short. sounds easy and simple, but explaining the notion of 'time' to arduino was surprisingly challenging.   

check our final code below :)  
<details> 

```cpp
int R2 = 10000;
float VIN = 3.0;

unsigned long startTime = 0;
unsigned long endTime = 0;
unsigned long interval = 0;

int ledState = 0;

void setup() {
  Serial.begin(9600);
}



void loop() {

  // read the input on analog pin 0:
  int sensorValue = analogRead(A3);

  if (sensorValue > 1000) {
    Serial.println("turn off the lights!");
    delay(1000);
  }

  else {
    Serial.println("lights off, checking for LED...");
    if (sensorValue > 100 && ledState == 0)  //if the led turns on
    {
      ledState = 1;
      Serial.println("the led turned on, I think!");
      startTime = millis();
      Serial.println("start time:");
      Serial.println(startTime);

      if (sensorValue < 100) {
        endTime = millis();
        Serial.println("end time: ");
        Serial.println(endTime);
        interval = endTime - startTime;
        Serial.println("interval: ");
        Serial.println(interval);

        Serial.println("The LED is back off, I think!");
        ledState = 0;
        delay(1000);

        if (interval < 1000) {
          Serial.println("SHORT");
          delay(1000);
          interval = 0;
        }

        else {
          Serial.println("LONG");
          delay(1000);
          interval = 0;
        }
      }
    }
    // Convert the analog reading (which goes from 0 - 1023) to a voltage (0 - 5V):
    //float voltage = sensorValue * (3.0 / 1023.0);

    // Get the value of R1
    //int ldr = ((R2 * VIN) / voltage) - R2;

    // print out the value you read:
    //Serial.println(sensorValue);
    //Serial.print("voltage: ");
    //Serial.println(voltage);
    //Serial.print("LDR value: ");
    //Serial.println(ldr);
  }
}

```
</details>
