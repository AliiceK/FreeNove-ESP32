# FreeNove-ESP32
Documenting my learning of Embedded Systems

Day 1 4/17 :

Documentation day one : I will learn programming an ESP32 ( it's the chip ) microcontroller . I will use the Arduino framework - easiest way for me to learn how to program microcontrollers . My code will run on the hardware. I will ( maybe ) in the future switch to ESP - IDF ( which is the professional way to program ESP32 ).

The board is made by FreeNove and this tutorial will include the steps listed on their website.
- Component List : Prepare material for the experiment
- Component Knowledge : to understand the electronic modules or components
- Circuits : to learn circuits obv
- Code : guess what it is.

Remember we are using ESP32-Wrover, which has extra features built in, also has extra RAM. The board has an antenna printed into it ( like a phone's internal antenna to connect to bluetooth and wifi ).

Let's explain the hardware parts : Here's a pic for reference 

<img width="1123" height="538" alt="image" src="https://github.com/user-attachments/assets/40c32890-84ae-40bd-b7ec-d1232847b7a7" />

<img width="1034" height="360" alt="image" src="https://github.com/user-attachments/assets/1a70bb0a-ddd7-4e11-ab6b-a0a3729cc235" />

GPIO pins : basically the holes / pins you plug your wires and sensors into
LED indicator : A tiny light to tell you the board is on
Camera interface : plus in camera module 
Reset button : like resetting your computer 
Boot Mode : Used when flashing new code onto the board
USB port : how to connect with your laptop

You might also see thi very confusing table 

<img width="479" height="776" alt="image" src="https://github.com/user-attachments/assets/a65b4c4a-2948-419f-baaf-fe1c1a1ea56c" />

This is called a pinout table . It will list most importantly the type of the pin ( I = Input only, O = Output only, I/O = both, P = Power ) and everything the pin can do . For example look at pin IO2 ( i included a picture of my own board ) 

<img width="474" height="771" alt="image" src="https://github.com/user-attachments/assets/cd8896d1-faea-4320-8144-8945b2911d8b" /> you see the 2 at the bottom on the right side of the label strip ( between  0 & 15 ) --> that's IO2. One of its functions is GPIO — blinking LEDs, reading buttons. No need to memorize these btw.

The extension board has 3 main jobs:
- Spread out the GPIO pins into the breadboard so you can easily plug wires in .
- Provide power to your components (sensors, LEDs, etc.)
- Allow external power if USB isn't enough

Don't try to draw too much power from those pins. If you connect too many power-hungry components at once, you could damage your board. So I will plug in via USB and use the 3.3V pins to power small sensors.

So now what is the next step ? 
- Installing the driver that lets your computer talk to your ESP32 board

  What is CH340 ? Your ESP32 communicates with your laptop over USB. But your laptop doesn't automatically know how to interpret those signals. The CH340 is a chip on your board that translates between USB and the ESP32's language. The driver is software that tells your laptop how to work with that chip.

  There are steps listed on the website, ill be posting my own pics here

  I have a Windows 11, I downloaded CH341SER.EXE.

  Next I downloaded the Arduino Software.

  <img width="629" height="443" alt="image" src="https://github.com/user-attachments/assets/7ca6d6e5-5a58-4fef-844f-7006401a0958" />

  Once finished downloading, some explanation on the Arduino interface :
- Sketch : Just their word for "program" — don't overthink it.ino.
- file : The file extension, like .py for Python or .java for Java.
- Console : Where error messages and output appear — like a terminal.
- Serial Monitor : How you print text from your ESP32 to your laptop screen.
- Verify : Compiles your code — checks for errors without uploading.
- Upload : Sends your code to the ESP32.

  I downloaded the esp32 3.3.8 version since the 3.0.7 version timed out

4/20 :

  The first piece of code is the LEB Blink Code which is teh following :
#define LED_BUILTIN 2
  void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

This runs one time when the board powers on or resets. It tells pin 2 to act as an output (sending power out), not an input (reading a signal).

Then we hace the second piece of code :

loop() — runs forever in a cycle
  void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // LED OFF
  delay(1000);                      // wait 1 second
  digitalWrite(LED_BUILTIN, LOW);   // LED ON
  delay(1000);                      // wait 1 second
}
What happens :digitalWrite(HIGH) Sends voltage to pin 2 → LED turns OFF
              delay(1000)Waits 1 second
              digitalWrite(LOW) Cuts voltage to pin 2 → LED turns ON
              delay(1000) Waits 1 second
              
It was a little confusing at me first why if digital Write is High, the LED truns off, and when LOW it turns ON. This is when Current Flows comes in : Current ONLY flows when there is a voltage difference between 3 points - from high to low.

How this specific circuit is wired (Active Low):
3.3V (always on) → Resistor → LED → GPIO Pin 2
The LED sits between a constant 3.3V source and GPIO pin 2.

When GPIO is HIGH (3.3V):
3.3V ----LED---- 3.3V (GPIO)
Both sides are at the same voltage → no difference → no current flows → LED OFF

When GPIO is LOW (0V):
3.3V ----LED---- 0V (GPIO)
Different voltages → current flows from 3.3V through the LED down to 0V → LED ON

I wasnt really understanding how it is all coming together, so I asked AI to do a power chain map : 

USB (5V)
   ↓
Voltage Regulator
   ↓
3.3V → powers everything including:
         ├── The 3.3V supply pin (for your circuit)
         └── The GPIO pins (so when HIGH, they output 3.3V)

Chapter 0 Finished !

Onto Chapter 1 : LED 

LED is a diode meaning current can only flow through it one way ( one way street )
It has two pins : + ( Anode - Longer Pin - connects 3.3V ) & - Cathode ( Shorter Pin - Ground ( GND ) )  ).
It has a voltage range 1.9V to 3.4V - 3.3V is safe .

WHY A RESISTOR MUST BE USED ! too much current rushes through LED and destroys it ! An analogy can be like Voltage is the Water pressure but the Current is the Water Flow Rate.

<img width="624" height="199" alt="image" src="https://github.com/user-attachments/assets/21891a7d-b5ae-4d9c-85c2-b2957df17f76" />

A resistor is a passive component that limits the current flow in a circuit. It just resists ( doesnt generate or store anything ) . Those colored stripes on the physical resistor are a code that tells you its resistance value in Ohms. For example a 330Ω resistor has specific color bands

OHM'S LAW : 
I = V / R
Current = Voltage ÷ Resistance.

Keep in mind that :

If voltage is fixed (3.3V always), then:
More resistance → less current → dimmer LED
Less resistance → more current → brighter LED (but risk of burnout)

<img width="436" height="193" alt="image" src="https://github.com/user-attachments/assets/63323d96-0365-457d-9673-9afec8a21537" />

The ESP32-WROVER needs 5V to operate. It gets it from the USB cable.

Never let + and - touch each other without something in between (a resistor, LED, sensor etc.) 

Normal:
3.3V → Resistor → LED → GND
(resistance limits current = safe ✅)

Short circuit:
3.3V → GND directly (nothing in between)
(no resistance = unlimited current = 💀)

<img width="869" height="338" alt="image" src="https://github.com/user-attachments/assets/54720893-cfc2-4227-9b77-01bb707e238b" />




  












