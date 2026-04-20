# 4-Bit Binary Counter with Arduino

This project uses an Arduino to create a visual 4-bit binary counter using four LEDs. It counts from 0 to 15 (0000 to 1111 in binary) and then resets.

🛠 Hardware Needed

* 1 x Arduino (Uno, Nano, or similar)
* 4 x LEDs
* 4 x 220Ω Resistors
* Jumper wires & Breadboard

🔌 Wiring Diagram

Connect the LEDs to the following Digital Pins:
* LED 1 (MSB): Pin 2
* LED 2: Pin 3
* LED 3: Pin 4
* LED 4 (LSB): Pin 5
* GND: Connect all LED cathodes to the Arduino Ground via resistors.

🚀 How it Works

The code manually toggles the HIGH and LOW states of four pins to represent binary numbers.
* 0000 (0): All LEDs OFF
* 0001 (1): LED 4 ON
* ...
* 1111 (15): All LEDs ON
The variable wait is set to 2000ms, meaning the counter updates every 2 seconds.

💻 Installation

1. Open the Arduino IDE.
2. Copy and paste the code from counter.ino into a new sketch.
3. Connect your Arduino via USB.
4. Select your Board and Port under Tools.
5. Click Upload.


More efficient version of the code using a loop:


Using a for loop and some bitwise math makes the code much shorter and easier to manage. Instead of writing out every single number, we can just count from 0 to 15 and let the Arduino figure out which LED should be on.

// Define pins in an array (from Most Significant Bit to Least Significant Bit)
int ledPins[] = {2, 3, 4, 5}; 

void setup() {
  for (int i = 0; i < 4; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // Count from 0 to 15
  for (int i = 0; i <= 15; i++) {
    displayBinary(i);
    delay(2000);
  }
}

void displayBinary(int num) {
  for (int j = 0; j < 4; j++) {
    // Check the state of each bit using bitwise shift and AND
    // This looks at the bits from right to left
    int bitState = (num >> (3 - j)) & 1;
    digitalWrite(ledPins[j], bitState);
  }
}


* If you want to add a 5th LED, you just add one pin to the array and change the 15 to 31.


