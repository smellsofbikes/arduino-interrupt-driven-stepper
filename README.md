# arduino-interrupt-driven-stepper
Stepper driver using timer2 to schedule steps, adc for speed, with display
This targets an Uno R3.  LCD on pins 2-7, pins 8-11 provide raw half-step signals for something like an L298 dual H-bridge,
and ADC5 reads a potentiometer that determines the speed.
Operation: ADC set up as free-running, sampling the pot.  Timer2 is set up to interrupt on overflow.  In the Timer2 overflow 
ISR, the number of overflows is compared to the requested speed.  On match/exceed, a single step is driven in the desired
direction.  Drive is via PORTB rather than digitalWrite for speed.  Display shows speed (relative, not absolute), direction,
and off/on status.
Pullup pins on D12 and D13 control rotation direction and off/on, through toggle variables with a subtractive 
millis()-based debounce.
Hardware is tested and works.
If the stepper is run at higher speeds (with this setup max is about 100rpm) this will need acceleration/deceleration 
profiles for reversing and off/on.
