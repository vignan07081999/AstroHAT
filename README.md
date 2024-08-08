# AstroHAT
## Introduction




## Theory
### PART 1 (What is the HAT spec?)
Raspberry Pi HAT modules are a great open standard for adding functionality to a Pi that either needs additional hardware, or a better way to connect with the rest of the world. The Pi Foundation has a pretty good spec for what is needed to make a board officially HAT compatible, but it takes a little bit of reading and parsing. This page on the design guidelines has all of the specifics of what you need to consider when designing your HAT.
From the main page:
A board can only be called a HAT if:
It conforms to the basic add-on board requirements
It has a valid ID EEPROM (including vendor info, GPIO map and valid device tree information).
It has a full size 40W GPIO connector.
It follows the HAT mechanical specification
It uses a GPIO connector that spaces the HAT between 10mm and 12mm from the Pi (i.e. uses spacers between 10mm and 12mm).
If back powering via the GPIO connector the HAT must be able to supply a minimum of 1.3A continuously to the Pi (but ability to supply 2A continuously recommended).
Other details you need to know:
There are specific GPIO sequencing that you need to be mindful of. By default, some pins are active at boot, so that can have unexpected results if there is no current limiting on whatever is connected to them.
On pins 27 and 28, do not connect anything other than an EEPROM that is to the defined spec. You can leave off the EEPROM, but that is no longer officially a HAT. As long as you don't connect anything to those pins, the Pi Foundation would still probably be supportive, but you can't say it is a HAT.
If you are back powering the Pi via the HAT, you need to not connect the 3.3V supply from the HAT to the Pi, and you need to put in protective components to prevent 5V via USB causing conflicting power issues.
So, that seems to be the lot of it, the Pi Foundation really tried to leave the rest as wide open as possible to let you be as clever as you want.

### PART 2 (OK, so how do you design a HAT?)
Well, knowing the basics of what things you need to call your design a HAT is only a small part of it. The best resource I found for the details of what each pin is capable of is https://pinout.xyz/ If you check their GitHub you can find good resource files with all the functions defined in YAML format. Here is a good image based version of the same info.I know everyone may have their own way to approach this part of the design. Some people might start with a schematic with all the bits and then just start making connections, but what I have found is that doing this in a spreadsheet helps to both make it easier to parse all the options and to do some checking to see what is available and if the function you assigned to a particular pin is valid. You can find a spreadsheet version of this pinout in this project files here.

After some consideration, the final system level design is to use the Raspberry Pi 40-pin header to interface to a small MCU that is directly controlling 2 IO modules. The size of the official HAT hardware makes it pretty much a requirement for the IO module connectors to be mounted directly on it instead of making it an adapter to the Controller slot on our backplanes.
![image](https://github.com/user-attachments/assets/b05a53b3-b160-46a5-b6d9-55726269feac)



## 5v Powered HAT Protection
![image](https://github.com/user-attachments/assets/0f211d5c-0f3d-45c7-a3df-35fe8f7c172f)





