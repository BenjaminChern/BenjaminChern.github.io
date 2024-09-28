---
layout: post
title: Self Playing Piano
subtitle: A project 2.5 years in the making
author: Benjamin Chern
youtubeId: pbvPtyYYVq0
---

## Demo:

{% include youtubePlayer.html id=page.youtubeId %}


## Capabilities
  - Individual control of 88 keys
  - 255 Levels of volume modulation using PWM
  - Converts MIDI to compact bitset to increase data transmission speed
  - Cascading series of Queues to ensure notes are timed properly

## Background

Like any good asian child, me and my sister played the piano since we were young at the insistence of our parents. Unlike my sister though, I stopped lessons at the end of elementary school and my skills have slowly declined since. Now she is head and shoulders ahead of me and this project is my attempt at leveling the field. Of course, mechanical hands can never match human ones, but I have put in effort to make the gap as small as possible.

## Planning

Since I am most comfortable with robotics, I started development by laying out the broad strokes concerning mechanisms and control hardware. Solenoids were the easy choice to press the piano keys but they were not without downsides. Solenoids are fast, powerful and the linear motion suits the project well. However solenoids also are power hungry, heavy, produce a loud clicking noise when bottoming out, and are expensive to buy. Regardless, the speed and lack of rotational motion were too important to pass on so a lot of this project became about mitigating the downsides of using solenoids. 

An obvious problem arises, how do you control 88 solenoids at once? An arduino/raspberry pi has around 16 output pins so wiring them directly is out of the question. I also want to drive the solenoids using PWM to control volume which further narrows the set of options available. After considerable thought, I believe the solution lies in either a shift register or I2C GPIO expander. Either approach would have worked fine, however I chose the I2C expander option due to a familiarity with the I2C protocol. 

Mounting the device to the piano also merits a bit of planning which I did not initially do. Since I focused upon the electronics heavily, the chassis was neglected more than it should have been, leading to the ugly wooden spacer in version 1 found [here](https://www.youtube.com/watch?v=qJCV7lqjcMM). When I revisited the project for V2, I added an additional aluminum bar for strength and combined with formal 3D modeling classes, the body was much more efficient than before. 

## Custom PCB Work

There are pre-existing I2C GPIO expanders on the market in the form of neat little development boards which would suit most purposes. However the solenoids produce a noticeable buzzing noise when driven by PWM with the frequency of the operating frequency of the PWM generating chip. For example, common GPIO expanders like [this one](https://www.adafruit.com/product/815) use the PCA9685 chipset with a PWM frequency of 1.6kHz, producing a 1.6kHz whine while the device is operational. This whine is not ideal and is what led me to proceed with a chipset from the same family (PCA9635) which offers up to 97kHz frequency which is far outside human hearing. With the help from online resources and an invaluable mentor from an online community, I was able to learn the design software EAGLE and send a design to JLCPCB which did much of the component assembly for me.

## Electrical System

The heart of this project is an Arduino Mega doing all the scheduling and coordination. In hindsight this should have been on my local machine (laptop) but what's done is done. Each custom PCB is daisy chained on the I2C bus with different addresses starting at 0x40 and ending at 0x47. A 24V, 20A power supply powers the solenoids through a distribution bus while a buck-boost converter drops the voltage down to 12 to power the logic and relay. In the future, I want to use the arduino to control a set of linear actuators for the pedal mechanism but that is outside of the time constraints for now. Currently the relay is used to hold power from the solenoids until after the PCBs have finished initializing so the solenoids don't fire before logic is initialized. 

## Code

Although I have little formal software engineering experience, I am quite proud of what I wrote for this project. The software is split into two parts, one half on my local machine and the other on the onboard arduino. A library (documentation found [here](https://www.fourmilab.ch/webtools/midicsv/) is used to convert the MIDI to a CSV file which is then parsed through using Python to extract the important information: state, note, volume, time. The note value falls from 1-88, meaning it fits within 1 byte. Volume is from 0-255 meaning it is just outside 1 byte. State is binary, either an "on" event or "off" event, allowing it to be 1 bit. For the sake of ease though, I sent state as a byte, wasting some space. Since all events were bytes, they could be converted to an ASCII char and sent over USB serial to the arduino. A "noteEvent" would therefore look something like: !E~0

Upon 

## Local URLs in project sites {#local-urls}

When hosting a *project site* on GitHub Pages (for example, `https://USERNAME.github.io/MyProject`), URLs that begin with `/` and refer to local files may not work correctly due to how the root URL (`/`) is interpreted by GitHub Pages. You can read more about it [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). To demonstrate the issue, the following local image will be broken **if your site is a project site:**

![Crepe](/assets/img/crepe.jpg)

If the above image is broken, then you'll need to follow the instructions [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). Here is proof that it can be fixed:

![Crepe]({{ '/assets/img/crepe.jpg' | relative_url }})
