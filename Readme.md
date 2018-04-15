#ESP32 I2S MEMS Microphone Arduino IDE Example
This repository holds some samples for connecting a I2S MEMS microphone to an ESP32 board.

At first I thought hooking up an I2S microphone would be straight forward, but it seems that I2S is a somewhat new or neglected interface. The examples distributed by adafruit only apply for Feather M0; the generic I2S example from the ESP32 examples is not directly applicable. Hence this repository.

## Components used in this example
I am using these components:
* [adafruit-huzzah32-esp32-feather](https://www.adafruit.com/product/3405)
* [adafruit-i2s-mems-microphone-breakout](https://www.adafruit.com/product/3421)

## How to connect the components?
There are no dedicated I2S pins on the ESP32. Instead, you will have to configure/enable the pins in your code. 
Eventually, I connected I2S-MEMS pins to the following ESP32 pins:
* SEL is unconnected, i.e. only one channel, apparently left
* LRCL to #15
* DOUT to #32
* BCKL to #14
* GND to GND
* 3V to 3V

Don't try to connect them to the similar sounding SCL/SCA/SCK, they're for the incompatible I2C interface.

## How to use the examples?
You can open each of the examples as a sketch in the Arduino IDE. I've commonly used a baudrate of `115200`, you will need to configure this in your serial monitor, otherwise it'll display rubbish.

## Noteworthy
* Either the `SEL` config is wrong, or the ESP32 I2S channel handling.
  * I had to use `I2S_CHANNEL_FMT_ONLY_RIGHT` whenever `SEL` pin was unconnected/ground, and `I2S_CHANNEL_FMT_ONLY_RIGHT` when `SEL` is high.
* I could only get it to work with 32 bit sampling.
  * I don't know if this is a limitation of either hardware, or a configuration mistake on my side.
* Although the setup seems to react nicely to noise.
  * I do not know if the recorded data is actually a valid sound.
  * There might be some bit-juggling still to be done.

## Credits
Credits go to Adafruit for the easy-to-use hardware and the nice guide (even if it is not fully applicable here, it's still a great place for starters) and the [espressif examples](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2s).