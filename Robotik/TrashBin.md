---
date: 17. Juli 2025
tags:
  - Sensor
  - Servo
  - Robotik
---

# Trash bin robot
## with ultrasonic sensor and servo motor

This code illustrates how to use an ultrasonic sensor with

```python
from machine import Pin, PWM, time_pulse_us
import time

# Pin Definitions
TRIG = Pin(15, Pin.OUT)
ECHO = Pin(16, Pin.IN)
SERVO = PWM(Pin(17))

SERVO.freq(50)  # 50Hz PWM

def send_pulse():
    TRIG.low()
    time.sleep_us(2)
    TRIG.high()
    time.sleep_us(10)  # Send a 10-microsecond HIGH pulse
    TRIG.low()

def measure_distance():
    send_pulse()
    duration = time_pulse_us(ECHO, 1)
    return duration / 58.275

# Sets the servo to a specific angle (0 to 180 degrees).
def set_servo_angle(angle):
    """
    Pulse width varies approximately from 0.5 ms (0°) to 2.5 ms (180°).
    Convert angle to duty cycle for the 50 Hz signal (20 ms period).
    """
    pulse_width_ms = 0.5 + (angle / 180) * 2.0  # Pulse width in milliseconds
    duty = int((pulse_width_ms / 20) * 65535)  # Scale to 16-bit integer for PWM
    SERVO.duty_u16(duty)

while True:
    dist = measure_distance()

    if dist < 20:
        set_servo_angle(90)
        time.sleep(1)  # delay for the servo to move smoothly
        set_servo_angle(0)
    else:
        set_servo_angle(0)  # No object detected

    time.sleep(0.2)  # Delay before measuring again
