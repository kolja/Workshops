---
tags: [Ultrasound, sensor]
---

# The Ultrasound sensor and the Speed of Sound

We have an Ultrasound sensor, and we want to measure the distance to an obstacle. However, the sensor does not measure the distance directly. It measures the time it takes for a sound to travel from the sensor to the obstacle and back.

Here is some code that uses the ultrasound sensor (HC-SR04) to do this:

```Python
from machine import Pin, time_pulse_us
import time

# Pin Definitions
TRIG = Pin(15, Pin.OUT)
ECHO = Pin(16, Pin.IN)
LED = Pin(17, Pin.OUT)

def send_pulse():
    TRIG.low()
    time.sleep_us(2)
    TRIG.high()
    time.sleep_us(10)
    TRIG.low()

def measure_distance():
    send_pulse()
    duration = time_pulse_us(ECHO, 1)
    return duration / 58.275

while True:
    dist = measure_distance()

    if dist < 20:
        LED.high()  # Turn on LED
    else:
        LED.low()   # Turn off LED

    time.sleep(0.2)
```
The speed of sound is approximately 343,2 m/s (or 34320 cm/s)
We have a measurement in microseconds (μs) but for our calculations, we would like to use seconds and centimeters:

`time in seconds = our measurement in microseconds / 1000000`

To calculate the distance traveled within the time we measured,
we can do:

`total distance (cm) = speed of sound (cm/s) * time in seconds`

`total distance (cm) = 34320 * (duration / 1000000)`

But we are not interested in the total distance the sound wave traveled. We only need half of that distance, because the sound travels to the obstacle and back to the sensor.

`distance (cm) = 34320 * (duration / 1000000) * 1/2`

or:

`distance (cm) = 34320 * duration / 2000000`

or:

`distance (cm) = 34320 / 2000000 * duration`

or:

`distance (cm) = 0.01716 * duration`

Which can also be expressed as:

`distance (cm) = duration / 58.275`

