/*
This sketch uses an attiny85 to control two small DC motors via
PWM. To make manual speed calibration easier I added two 10 K ohm trimpots
that are read by analog pins A1 and A2. 

One button connected to pin A3 starts a timer so the motors run
for a defined number of milliseconds.

The circuit:
  - Attiny85 chip running with internal 1 MHZ clock
  - Powered by a 12v 300 mA wall wart
  - Regulated by an L7805 voltage regulator with electrolitic capacitors
    - 10 uF on the input
    - 47 uF on the output
  - Each motor control switches 12 v using
    - TIP112 transistor
    - 1N4001 Diode
    - 270 Ohm resistor
  - Trim pots are 10 K ohm outside legs connected to 5v and Ground, 
    middle leg to pins A1 and A2 respectively
  - Switch uses a pull down 10 k resistor connected to ground and
    the other leg to 5v

Resources:
  - Motor circuit and code (TIP112 instead of N2222:  https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors/
  - Motor transistor circuit: https://www.arduino.cc/en/Tutorial/TransistorMotorControl
  - Button circuit and code: https://www.arduino.cc/en/Tutorial/Button
  - Reading a Potentiometer: https://www.arduino.cc/en/tutorial/potentiometer
  - Timer function takes hints from the debounce example: https://www.arduino.cc/en/Tutorial/Debounce
  - Use hints for attiny85: https://learn.sparkfun.com/tutorials/tiny-avr-programmer-hookup-guide/attiny85-use-hints


Federico
https://wolfcatworkshop.com
more about this project at https://wolfcatworkshop.com/index.php/portfolio/drill-powered-flipbook-animation/
  
 */


//variables
int motorPin0    = 0;  //Motor 
int motorPin1    = 1;  //Motor 
int analogInPin1 = A1; //Analog Pin 1 for 10 k pot
int analogInPin2 = A2; //Analog Pin 2 for 10 k pot
int buttonPin    = A3; //Button 

int analogIn1;  //stores readings from A1
int analogIn2;  //stores readings from A2

int buttonState;    //reading for the button, either HIGH or LOW
int motorState;     //Motors ON or OFF (0 or 1)


long seconds = 8000;  //See note below about changing the PWM frequency and its effect on delay and millis
//Using unsigned longs for milliseconds because the number gets larger than
//what can be stored in an int
unsigned long lastTime = seconds * 60;       // the last time the button pin was toggled
unsigned long timerDelay = seconds * 60;    // how long until next read



void setup() {

//set up all the pins  
    pinMode(motorPin0,    OUTPUT);
    pinMode(motorPin1,    OUTPUT);
    pinMode(analogInPin1, INPUT);
    pinMode(analogInPin2, INPUT);
    pinMode(buttonPin,    INPUT);

/* Change the PWM frequency to avoid buzzing, more at http://forum.arduino.cc/index.php?topic=174349.0
This setting affects delay and millis() https://playground.arduino.cc/Main/TimerPWMCheatsheet 
On the attiny85 this line affects both PMW pins
One second: 8000 millis with 0x02 (which is divisor 8 of the frequency)
*/
    TCCR0B = TCCR0B & 0b11111000 | 0x02; //see comment above
}


void loop() {
  
int analogIn1 = analogRead(analogInPin1); // Read analog voltage on pin A1
int analogIn2 = analogRead(analogInPin2); // Read analog voltage on pin A2  

/*  This turns the motors ON or OFF depending on the value of motorState
    analogRead returns a value between 0 and 1023, dividing this by four turns
    it into a value between 0 and 255 which is the range analogWrite can use
*/
  if (motorState == 1){
    analogWrite(motorPin0, analogIn1/4); 
    analogWrite(motorPin1, analogIn2/4);
  }
  else {
    analogWrite(motorPin0, 0);
    analogWrite(motorPin1, 0);
    };


/*
The timer takes hints from the Debaounce example on the arduino website
Only cares about the state of the button pin if the current time - the last time is
bigger than the specified delay. 

*/
buttonState = digitalRead(buttonPin);  // larger than delay they read the button  

if (millis() - lastTime > timerDelay){   //if current time minus last time is 
    
     if (buttonState == HIGH){     //if the button is pressed
      lastTime = millis();          //reset the time
      motorState = 1;              //and turn on the motors
      }
     else{
      motorState = 0;              //motors OFF if nothing happens
      }

        };
  

  
    
}
  
  


  

