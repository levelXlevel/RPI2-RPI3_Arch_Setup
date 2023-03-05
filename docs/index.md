# ARCH Linux on PI2B/3B

How I setup ARCH Linux on my RPi2 & RPi3.

## Why

You might be asking; In 2023 why maintain these resource constrained devices?
Answer; They're good enough for data collection and reporting.

1. Prometheus; Anything with an exporter gets routed to these devices for collection.
2. Grafan; Because what's the point of collecting data if you can't visualize it?
3. Dabble in other things.

## Hardware

### RPi2

1. Version 1.1
2. 1GB RAM
3. 52Pi Raspberry Pi Fan Expansion Board w/ 0.91 OLED V1.0
4. SD Card
5. 32GB USB Drive
6. UCtronics POE splitter

### RPi3B

1. Version 1.2
2. 1GB RAM
3. 52Pi Raspberry Pi Fan Expansion Board w/ 0.91 OLED V1.0
4. SD Card
5. 32GB USB Drive
6. UCtronics POE splitter

## Getting started

This is just an outline of steps. There are a few ways to perform the first step and everyone has their preferred way. The seconds step is performed by [PINN](https://github.com/procount/pinn) , leaving little of consequence for the user to setup.

1. Install [PINN](https://github.com/procount/pinn) on the SD card.
2. Install ARCH from the PINN UI onto the USB drive.
3. Reboot
4. Enjoy
