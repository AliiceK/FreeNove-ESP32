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












