# flipbox-animation

Althought this is not a full how-to, you can find design files here in case you want to replicate this project. 
Read the full story [here](https://wolfcatworkshop.com/index.php/portfolio/drill-powered-flipbook-animation/) or go directly to a [video](https://vimeo.com/235196914) of the project in action.  


<p align="center"> 
<img src="https://github.com/wolfcatworkshop/flipbox-animation/blob/master/images/flipbox-featured.jpeg">
</p>

![flipbox](https://github.com/wolfcatworkshop/flipbox-animation/blob/master/images/flipbox-featured.jpeg)

## Box Construction
![box schematic](https://github.com/wolfcatworkshop/flipbox-animation/blob/master/images/flipBox-box.jpg)

* All faces in a single file in the following formats: [DXF](/vector-files/all-box-faces.dxf), [AI](/vector-files/all-box-faces.ai), [SVG](/vector-files/all-box-faces.svg)
* Additional 1" box for electronics in the following formats: [DXF](/vector-files/bottom-box-faces.dxf), [AI](/vector-files/bottom-box-faces.ai), [SVG](/vector-files/bottom-box-faces.svg)

## Additional parts
* Frame holding wheel: [DXF](/vector-files/wheel.dxf), [AI](/vector-files/wheel.ai), [SVG](/vector-files/wheel.svg) and [STL](/stl-files/wheel.stl)(since this part is suitable for 3D printing).
* Small DC motor mount: [DXF](/vector-files/motor-mount.dxf), [SVG](/vector-files/motor-mount.svg) and [STL](/stl-files/motor-mount.stl)

## Electronics
This project can be replicated with any number of Arduino compatible boards, in my case, for space saving purpuses I used an Attiny85.

* The speed of each motor is controlled via Pulse Width Modulation, because the microcontroller has a current and voltage limit, the switching is done by a transistor (see the [Transistor Motor Control](https://www.arduino.cc/en/Tutorial/TransistorMotorControl) example on the Arduino website).
* A small potentiometer serves as a physical interface to adjust the speed of each motor (see the [Reading a potentiometer](https://www.arduino.cc/en/tutorial/potentiometer) example).
* There is a single button to start the operation and start the timer, so every time you press the button the animation plays for 1 minute and then stops (see [Button Tutorial](https://www.arduino.cc/en/Tutorial/Button) and [Debounce Tutorial](https://www.arduino.cc/en/Tutorial/Debounce)).

The specifics of my final circuit are as follows:
* Attiny85 chip running with internal 1 MHZ clock
* Powered by a 12v, 300 mA wall wart
* Power is regulated by an L7805 voltage regulator with two electrolytic capacitors
   * 10 uF on the input
   * 47 uF on the output
* Each motor control switches 12 v using:
   * TIP112 transistor
   * 1N4001 Diode
   * 270 Ohm resistor
* Trimpots are 10 K ohm outside legs connected to 5v and Ground, middle leg to pins A1 and A2 respectively
* Switch uses a pull-down 10 k resistor connected to ground and the other leg to 5v
* Arduino [Code](/code/arduino-Sketch.ino)

Note that in the above code the analog pins are referenced as A1, A2, and A3 which works with the Attiny85 microcontroller but not with other boards. Also, I changed the PWM frequency on line 75 to get rid of the motor buzzing at low speeds but this affects the delay() and millis() functions. Read more about compesanting for this at https://playground.arduino.cc/Main/TimerPWMCheatsheet





