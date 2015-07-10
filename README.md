# standuino-arduino

Arduino code to measure distance and send it over a serial port.

See https://github.com/b-ryan/standuino for the companion Python code to read
the data.

## Prerequisites

The following are used to build the Arduino code and load it onto the Arduino.

```
apt-get install arduino-core picocom
```

Use the python library [ino](https://github.com/amperka/ino) to build and load
the code. It can be installed with

```
pip install ino
```

## Hardware

Check out the sketch
[here](http://arduinobasics.blogspot.com/2012/11/arduinobasics-hc-sr04-ultrasonic-sensor.html).

To give a brief rundown, the ultrasonic sensor needs four connections. You will
see labels for each pin on the front of the sensor. These are named

* `VCC` for voltage
* `Trig` for trigger
* `Echo`
* `GND` for ground

Connect `VCC` pin to 5V power. Connect ground to ground. Connect 7 to `Echo`
and connect 8 to `Trig`.

Finally, plug the Arduino into a USB port.

## Code

Getting the code running is easy:

```
ino build
ino upload
```

If you get errors due to permissions on the serial port, you can give yourself
permission to read/write on the serial port in use. In the output of the upload
command you should see something like this:

> Guessing serial port ... /dev/ttyACM0

You can use that to figure out which permissions you need. See
[this](http://unix.stackexchange.com/a/14363) stack overflow question with
details. In my case, this works:

```
sudo usermod -a -G dialout buck
```

You might need to log out and back in for this to take effect.

## Test

To confirm things are working, you can open a serial monitor with

```
ino serial
```

This will read the data coming from the Arduino. It will look like:

```json
{"distance_cm": 24}
```

If the distance is 0, then something isn't working correctly. Try making
sure the connections are set up properly.

To quit the serial monitor, use `<C-a><C-q>`.
