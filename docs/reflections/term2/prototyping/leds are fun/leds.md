here we go, finally playing with our arduino boards again. We were all hapoy to start this class straight away hands-on. the 'real-time' presentation and application feels much more efficient and productive and fun, as it is a collective experience.  

we started by the simplest tast of *turning on a led light*, which we have already done numerous times, starting from the precourse. Yet still, I always get something wrong and ask for help because somehow i can never find if I mixed some pins, if I didn't connect to the right board on arduino interface, if, if, if...   

however, i collaborated with my friend Korbi for this task so this made the process faster.  



## message to the led  

after succeeding to make arduino understand that we were giving them messages, we wrote 3 different messages that would trigger the led to blink in 3 different rythms: 
- blink once  
- blink slowly  
- blink panic  

the notes in the code with the  '//' symbol actually help a lot....

![](slow fast.gif)  

```cpp
#include <jled.h>

#define LED 14

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  //pinMode(LED, OUTPUT); //this breaks the breathing - so you need to do everything in jled.
  Serial.begin(9600);
}

//defining the kled object
JLed led = JLed(LED);

//blinking in the narrow sense: only once.
void blink () {
 digitalWrite(LED, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(500);                      // wait for a second
  digitalWrite(LED, LOW);   // turn the LED off by making the voltage LOW
  delay(500);  
}

//slowly blinking for 10 seconds (might actually be 11 seconds ;) )
void blinkTenSecSlowly () {

  for (int i=0; i<5; i++) {
    digitalWrite(LED, HIGH);  // turn the LED on (HIGH is the voltage level)
    delay(1000);                      // wait for a second
    digitalWrite(LED, LOW);   // turn the LED off by making the voltage LOW
    delay(1000);  
  }

}

//blinking for ten (or maybe eleven) seconds, but much faster - PANIC MODE
void blinkTenSecPANIC () {

  for (int i=0; i<20; i++) {
    digitalWrite(LED, HIGH);  // turn the LED on (HIGH is the voltage level)
    delay(250);                      // wait for a second
    digitalWrite(LED, LOW);   // turn the LED off by making the voltage LOW
    delay(250);  
  }

}

// Smooth breathing
void breathe() {
  led.Breathe(1000).Repeat(4);
}

// the loop function runs over and over again forever
void loop() {

 if (Serial.available()) {

    String newMsg = Serial.readString();
    newMsg.trim();
    Serial.print("Got new message!: ");
    Serial.println(newMsg);

    // blink once if we tell it to!
    if (newMsg.equals("blink")){
      blink();
    }


    //blink slowly
    if (newMsg.equals("blink slowly")){
      blinkTenSecSlowly();
    }

   //blink panic
    if (newMsg.equals("blink panic")){
      blinkTenSecPANIC();
    }

    //breathe smooth
    if (newMsg.equals("breathe")){
      breathe();
  }

  // Do not remove this line! 
  led.Update();

}
}
```

## breathe   
the 'breathing' effect of the led seemed quite impressive so even though we were given the code already written by [jandelgaclo](github.com/jandelgaclo/jled), we wanted to understand how it is actually made. Soon we realised that it is much more complicated than we imagined so not much messing around could happen on our side. Most of the interesting part was 'hidden' in the jled library we installed anyway.  
<img src="../breathe_cheat_sheet.jpeg" alt="drawing" width="600" />   

At least we tried to understand the code  and add notes to make it a bit more understandable.  

```cpp
#include "Arduino.h"
#include "jled.h"
#define LED_PIN 14


// Jled object.
// More information here: https://github.com/jandelgado/jled#usage
auto led = JLed(LED_PIN);

// the setup function runs once when you press reset or power the board
void setup() {
  Serial.begin(9600);
}

// Basic blink
void blink () {
  led.Blink(1000, 600).Repeat(3);
}

// Smooth breathing
void breathe() {
  led.Breathe(2000).Repeat(10);
}

// the loop function runs over and over again forever
void loop() {

  if (Serial.available()) {
    // Read the string and clean it up
    String newMsg = Serial.readString();
    newMsg.trim();

    // For debugging purposes, print it
    Serial.print("Got new message!: ");
    Serial.println(newMsg);

    // Blink if we tell it to!
    if (newMsg.equals("blink")){
      blink();
    // Or breathe!
    } else if (newMsg.equals("breathe")) {
      breathe();
    }
  }

  // Do not remove this line!
  led.Update();
}
```

## synced burn  
