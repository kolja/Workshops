Control a DC Motor with a L298N Motor Driver
```Python
from machine import Pin

# Define the GPIO pins for IN1 and IN2
IN1 = Pin(17, Pin.OUT)
IN2 = Pin(18, Pin.OUT)

def control_motor(direction):
    """
    Controls the motor direction.

    :param direction: 1 for clockwise, 0 for stop, -1 for counter-clockwise
    """
    if direction == 1:
        # Clockwise rotation: IN1 high, IN2 low
        IN1.value(1)
        IN2.value(0)
    elif direction == 0:
        # Stop: both IN1 and IN2 low
        IN1.value(0)
        IN2.value(0)
    elif direction == -1:
        # Counter-clockwise rotation: IN1 low, IN2 high
        IN1.value(0)
        IN2.value(1)
    else:
        raise ValueError("Invalid direction: Must be 1, 0, or -1")

# Example usage:
# Start motor clockwise
control_motor(1)

# Stop motor
control_motor(0)

# Start motor counter-clockwise
control_motor(-1)
```
