---
date: 17. Juli 2025
tags:
  - blink
  - LED
  - Robotik
  - Raspberry Pi Pico
---
# Blink the built-in LED on a Raspberry Pi Pico

Here is a simple code snippet that will let you blink the built-in LED on a Raspberry Pi Pico using MicroPython.

The pin number 25 is lined to the onboard LED (pin 8 on ESP32).
`while True` will run forever, the value passed to `time.sleep()` is the delay in seconds.

```python
import machine
import time

LED = machine.Pin(25, machine.Pin.OUT)  # GPIO Pin 25 controls the onboard LED (GPIO Pin 8 on ESP32)

while True:
    LED.off()
    time.sleep(0.2)
    LED.on()
    time.sleep(0.2)
```

