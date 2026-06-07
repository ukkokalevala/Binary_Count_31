201 views  May 15, 2025
This project can be used for ESP or Arduino-compatible microcontroller to display a counting sequence from 0 to 31 in both decimal and binary formats. The binary representation is shown using 5 LEDs and an OLED display. Here's a breakdown of how it works:
Libraries and Setup
1. Libraries:
o Wire.h: Enables I2C communication for the OLED display.
o Adafruit_GFX and Adafruit_SSD1306: Drive the SSD1306 OLED display.
2. Display Configuration:
o A 128x64 pixel OLED display is initialized with I2C address 0x3C.
o Uses software-based reset (no physical reset pin).
3. LED Configuration:
o 5 LEDs are connected to pins D8, D7, D6, D5, D0 (common on ESP8266 boards).
o All LEDs start in the OFF state.
________________________________________
Key Functions
setup()
• Initializes LEDs as outputs and sets them to LOW (off).
• Initializes the OLED display with text size 3 and white color.
loop()
1. Count from 0 to 31:
o The loop iterates through values 0 to 31 (32 total values).
o Each iteration updates the LEDs and OLED display.
2. LED Control:
o Converts the current count to its 5-bit binary form.
o Each bit controls an LED:
 Bit 0 (LSB): Controls D8.
 Bit 4 (MSB): Controls D0.
o Example: For count = 3 (binary 00011), D8 and D7 light up.
3. OLED Display:
o Shows the decimal value (e.g., 3) at the top.
o Shows the 5-bit binary value (e.g., 00011) below it.
o Bits are displayed from MSB (left) to LSB (right).
4. Timing:
o Each value is displayed for 3 seconds (delay(3000)).
________________________________________
Hardware Mapping
Least Significant Bit (LSB):
Bit 0 is the least significant bit because it has the smallest positional weight in a binary number. In a binary number like 1010, the rightmost bit "0" is the LSB

Bit Position LED Pin Binary Weight
Bit 0 (LSB) D8 1 (2⁰)
Bit 1 D7 2 (2¹)
Bit 2 D6 4 (2²)
Bit 3 D5 8 (2³)
Bit 4 (MSB) D0 16 (2⁴)
________________________________________
Behavior
• The sequence increments every 3 seconds.
• At count = 31, all LEDs light up (binary 11111), and the system restarts from 0.
________________________________________
