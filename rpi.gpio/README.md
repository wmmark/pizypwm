PiZyPwm (RPi.GPIO flavor)
=========================

PiZyPwm, for Raspberry (Pi) Ea(zy) PWM, is an easy way to implement PWM (Pulse Width Modulation) output on a Raspberry Pi using Python language.

* [Project's website](http://goddess-gate.com/projects/en/raspi/pizypwm)
* [PiZyPwm in action](http://www.youtube.com/watch?v=1X_FYJ5x6Wo)
* [PiZyPwm with a digital oscilloscope](http://www.youtube.com/watch?v=aP1F67PtaVc)


Warning
-------

Due to the non real-time capacities of Python language, do not expect PWM to be very accurate. Pulses will never exactly last the theorical duration. But PiZyPwm will be enough if you don't need a great accuracy.


Running example.py
------------------

To run this example code, you'll need the assembly you'll find [here](http://goddess-gate.com/projects/en/raspi/raspiledmeter)

Requirements
------------

* First of all : a Raspberry Pi
* Python (with Debian / Raspbian : packages “python” and “python-dev”)
* RPi.GPIO library (0.4.0a or newer). On Raspbian, install package “python-rpi.gpio”.


Example usage
-------------

    import RPi.GPIO as GPIO
    
    from pizypwm import *
  
    # Set GPIO pin #7 as PWM output with a frequency of 100 Hz
    pwm = PiZyPwm(100, 7, GPIO.BOARD)
    
    # Start PWM output with a duty cycle of 20%. The pulse (HIGH state) will have a duration of
    # (1 / 100) * (20 / 100) = 0.002 seconds, followed by a low state with a duration of
    # (1 / 100) * ((100 - 20) / 100) = 0.008 seconds.
    # If a LED is plugged to with GPIO pin, it will shine at 20% of its capacity.
    pwm.start(20)
    
    # Change duty cycle to 6%. The pulse (HIGH state) will now have a duration of
    # (1 / 100) * (6 / 100) = 0.0006 seconds, followed by a low state with a duration of
    # (1 / 100) * ((100 - 6) / 100) = 0.0094 seconds.
    # If a LED is plugged to with GPIO pin, it will shine at 6% of its capacity.
    pwm.changeDutyCycle(6)
    
    # Change the frequency of the PWM pattern. The pulse (HIGH state) will now have a duration of
    # (1 / 10) * (6 / 100) = 0.006 seconds, followed by a low state with a duration of
    # (1 / 10) * ((100 - 6) / 100) = 0.094 seconds.
    # If a LED is plugged to with GPIO pin, it will shine at 6% of its capacity, but you may
    # notice flickering.
    pwm.changeFrequency(10)
    
    # Stop PWM output
    pwm.stop()

