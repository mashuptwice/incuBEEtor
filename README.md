# incuBEEtor bee queen incubator
ESP32 based temperature and humidity control for a bee queen incubator

## PARTS LIST
- ESP32 Dev Board
- 12V power supply
- 4 channel relais module
- 12V silent fan
- 2 heating mats
- rotary encoder
- SSD1306 OLED display
- wires 'n' stuff


## ESP32 PIN REFERENCE
- Heater upper    12
- Heater lower    13
- Fan             14
- Encoder Button  27
- Encoder DT      26
- Encoder CLK     25
- SSD1306 SDA     21
- SSD1306 SCK     22
- HDC1080 SDA     21 
- HDC1080 SCK     22

### additional project info

Both heaters are reptile heating mats, connected via relays to 230V. They put out 14W of power each. I got rid of the in-line thermostats and connected them directly as the whole point of this project was to provide better, more accurate temperature control.

The fan is a small 12V 500mA one, also connected via relays to the 12V PSU.

The encoder got some hardware debouncing as described [here](https://cdn-reichelt.de/documents/datenblatt/F100/402097STEC12E08.PDF) on page 11. I’ve also added some software debounce as the chosen PSU was pretty shi**y.

I’ve got some problems with strange inteference on the display, which I've traced back to a shitty, ripplesome 12V PSU. 


Another thing is that the set temperature gets written to EEPROM immediately, which provides conveniant restore of the last set temp & humid values after a power loss. Keep in mind that the ESP32's (and every other) EEPROM can only take a few thousand write cycles before it breaks down. This decision was made as the incubator won't need to be set on a different temperature very often but it should be failsafe immediately after setting the temperature to not risk the live of the bee larva. If you can think of a better solution, saving both the technical and biological ressources, feel free to create a pull request.
