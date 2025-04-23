# twsu-arcade-coder-pcb

An open source repository for replicating the board schematics and layout of Tech Will Save Us's ESP32-powered Arcade Coder RGB input matrix.

This project is viewable in KiCad 9.0+

I am not an electrical engineer, this is my best guess at replicating the schematics and layout of the board.  

## Community

Following [a very generous sharing of dozens of Arcade Coders](https://www.reddit.com/r/LinusTechTips/comments/1jgk9cr/how_can_i_stop_all_of_this_from_becoming_ewaste/), there is now a community of developers working on developing software for this board on [Discord](https://discord.gg/QWCUWKAqts) (if this URL does not work please message someone in the reddit thread who has joined).
If you join the community please make an effort to share your discoveries in a public space for future preservation.

## How it works

- 9 daisy chained HC595 chips are daisy-chained and used to control 24 RGB LEDs (two of the twelve rows) from 3 ESP32 pins
- 6 multiplexing channels are used to control the rows which the HC595s are in control of, this is done with an IC2012 (LS138) which requires 3 pins; the other 2 channels uses are unknown
- buttons on matrix are partially handled by 6 GPIO pins which are grouped in correspondence with the multiplexed LED channels (seemingly also partially handled by values being distorted by red LEDs)
- 2 status LEDs on the rear of the device are directly controlled by a GPIO pin each, as is the home button on the side
- accelerometer which I have not tested

### Pinout

HC595:
- Data: GPIO5
- Clock: GPIO17
- Latch: GPIO16
- OE: GPIO4 

ICN2012 (LS138, controls multiplexing to allow control of all 144 RGB LEDs):
- A0: GPIO19
- A1: GPIO18
- A2: GPIO21
- E1: 3.3v
- E2: GND (after a chain of resistors)

Button inputs (tracks if any button in row is pressed):
- 6 and 12: GPIO32
- 5 and 11: GPIO33
- 4 and 10: GPIO34
- 3 and 9: GPIO35
- 2 and 8: GPIO36
- 1 and 7: GPIO39

Other:
- LED1: GPIO22
- LED2: GPIO23
- Home: GPIO2 (seems unreliable)
- Motion sensor: GPIO27/GPIO26 for possible accelerometer in middle of board

Note: Usage of GPIO4 may impact ability to use Wifi from what I can see, will need to verify and see if it can be worked around.

## Errata

The project is currently schematics only, and currently only has the LED matrix and logic chips. I am working on figuring out the wiring of the button matrix, but that is more complicated as it uses some kind of resister ladder.
