---
draft: false 
date: 2021-03-01
links:
  - Github: https://github.com/JosefGst/autorace
categories:
  - Robotics
---


# :red_car: Autonomous RC-car race (first place) :trophy:

[![rc-car race](gifs/rc_car.gif)](https://github.com/JosefGst/autorace)


In this competition organized at HKUST I trained the [Jetson-racer](https://github.com/NVIDIA-AI-IOT/jetracer) to drive autonomously, avoid obstacles and overtake other cars. Basically I drove along the race course and recorded images with the corresponding throttle and steering values. This data is fed into the a ML model and let it train. It was much fun and I resliced what machine learning is capable of but also it's limitations. 

<!-- more -->

## :pencil: My takeaways:

- Most of the time I kept driving without recording any data but just training myself to drive fast and without crashes. Because if you provide bad data to the model it will learn your bad driving skills as well. If you drive slow the car will crash if you speed up the autonomous controller.
- Lightning condition had a strong influence. It could work perfectly fine in the morning but at a cloudy afternoon the light from the windows changed the perception and the car reacted strangely. Therefore changing the camera settings from RGB to HSV made the images more tolerant to various lightning.
- All Participants used the default resnet18 model. Only I invested the time to experiment with other models and decided to use Squeeznet. Even though resnet18 had a better accuracy but could only handle 4 fps. With Squeeznet the accuracy was lower meaning sometimes the predicted control values did not match so well with the test data. However with this model I reached up to 15 fps. Which made the car react much quicker to obstacles, turns and other cars. Finally gotten rid of the sluggish agent the rc car could drive much faster as anyone else.
