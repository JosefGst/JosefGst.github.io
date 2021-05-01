# Oven upgrade


1. TOC
{:toc}

# Problem

With this very cheap and simple oven there is no direct way to regulate the temperature. The only way to adjust the temperature is by switching between upper, lower or all heating tubes. The problem here is that the inbuild temp-sensor will turn off the heating elements if the chamber reaches a specific temp. However that is usually too low to bake something like a chicken. 

![](/Oven/images/oven.jpg "Oven")

# Temperature Sensor 

Since there's no way to adjust the temp-senor, I ended up disconecting it.

![](/Oven/images/circuite.jpg)

# Clock

It's a timer, which will turn off the oven after the set time is elapsed.

# Switch for Heating Tubes

This funcition is quite useless and we have never touched it, since the oven does not reach very high temperatures even with all heating elements turned on.

# A look into the Heating Plate

![](/Oven/images/heatplate.jpg)
![](/Oven/images/heat_plate_regulator.jpg "heat regulator in electric plate")

The heating plate uses a bi metal to regulate the power consumed. When it heats up it will open the switch and the currentflow is disconnected. It will cool down after a while and connect again. It is like a very slow PWM but works fine for very sluggish systems.  

![](/Oven/images/regulator.PNG)



# Solution

I want to use the bi metal heat regulator in the oven to controll the power input -> temperature.

The power goes into the clock, so I can still set a desiret period of time and forther to the heat regulator to be able to set the temperature. Then the output of the regulator is connected to the heating elements and the lamp. This way the lamp only flashes when the heting elements are fed with electricity, so I know when it is heating and when it is off.

![](/Oven/images/circuite2.jpg)