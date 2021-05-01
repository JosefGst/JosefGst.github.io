# Oven upgrade
![](/Oven/images/screenshots/oven.jpg "Oven")

1. TOC
{:toc}

# Problem

With this very cheap and simple oven there is no direct way to regulate the temperature. The only way to dajust the temperature is by switching between upper, lower or all heating tubes. The problem here was that the inbuild temp-sensor will turn off the heating elements if the chamber reaches a specific temp. However that is sometimes too low to bake some bigger like a chicken. 

# Temperature Sensor 

![](/Oven/images/screenshots/circuite.jpg)

Since there's no way to adjust the temp-senor, I ended up disconecting it

# Clock

It's a timer, which will turn off the oven after the set time is elapsed.

# Switch for Heating Tubes

This funcition is quite useless and we have never touched it, since the oven does not reach very high temperatures even with all heating elements turned on.

# Heating Plate

![](/Oven/images/screenshots/heatplate.jpg)

The heating plate uses a bi metal to regulate the power consumed. When it heats up it will open the switch and the currentflow is disconnected. It will cool down after a while and connect again. It is like a very slow PWM but works fine for very sluggish systems.  

![](/Oven/images/screenshots/regulator.PNG)

![](/Oven/images/screenshots/heat_plate_regulator.jpg "heat regulator in electric plate")

# Solution

I want to use the bi metal heat regulator in the oven to controll the power input -> temperature.

![](/Oven/images/screenshots/circuite2.jpg)

The power goes into the clock, so I can still set a desiret period of time and forther to the heat regulator. Then the output of the regulator is connected to the heating elements and the lamp. This way the lamp only flashes when the heting elements are fed with electricity.