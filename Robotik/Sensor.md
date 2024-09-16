---
date: 15. September 2024
tags:
  - Sensor
  - Robotik
---

# Sensors Library

```Python
# This code goes to 'sensors.py'

from machine import Pin, time_pulse_us
import time

class Ultrasound:

    def __init__(self, trig_pin, echo_pin):
        self.trig = Pin(trig_pin, Pin.OUT)
        self.echo = Pin(echo_pin, Pin.IN)

    def send_pulse(self):
        self.trig.low()
        time.sleep_us(2)
        self.trig.high()
        time.sleep_us(10)
        self.trig.low()

    def get_distance(self):
        self.send_pulse()
        duration = time_pulse_us(self.echo, 1)
        # Calculate distance in cm
        distance = duration / 58.275
        return distance
```
## Using the Library:
```Python

from sensors import Ultrasound  # from the file sensors.py

sensor = Ultrasound(trig_pin=15, echo_pin=16)

while True:
    dist = sensor.get_distance()
    print("Distance: {:.2f} cm".format(dist))
    time.sleep(0.2)

