---
title: Light Sensor
tags:
    - Robotik
    - Pico
    - Pankow
    - Python
---

```python
from machine import Pin
import time

light_sensor = Pin(16, Pin.IN)
LED = Pin(17, Pin.OUT)

while True:
    if (light_sensor.value() == 0):
        LED.high()
    else:
        LED.low()

    time.sleep(0.5)
```
