# DFRobot LTR390 UV Sensor Micropython library

This micropython library is aimed at the DFRobot's LTR390 UV sensor, product code SEN0540.

I bought this device thinking it would be easy to use their existing library, but I
just couldn't get their Python library to work. I also found a couple of other libraries
out there for the LTR390, but they didn't work either!

In the end I wrote this myself, using a combination of the DFRobot C library and the
LTR390 data sheet.

It works for me on an ESP32 controller, with both UV and regular light modes.

I hope you find this useful.

## Usage

```
import ltr390
from machine import Pin, I2C

sensor_i2c = I2C(0, scl=Pin(39), sda=Pin(40), freq=100_000)
ltr = ltr390.LTR390(sensor_i2c)
ltr.set_uvs()
ltr.set_gain(ltr390.eGain6)
ltr.set_measure_rate(ltr390.e18bit, ltr390.e200ms)

while True:
    v = ltr.uvs()
    print(f"V: {v}")
    utime.sleep_ms(500)
```

