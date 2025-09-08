# EZ-LEDS
Easy LED control NO Python or added installations

>[!IMPORTANT]
>
>You must create a FOLDER in Klipper called "leds"
>
>like this:
>~/printer_data/config/leds/
>
>then, in your printer.cfg add this under your "includes" section:
>
>```[include leds/*.cfg]```
>
>within the `leds` folder we need to add some info
>

How to use

Reload: RESTART

Set different functions:

Left shows progress bar: LED_L R=0 G=64 B=255 then LED_EFFECT_L MODE=progress

Right pulses warm white: LED_R R=255 G=180 B=64 then LED_EFFECT_R MODE=pulse

Turn one side off: LED_OFF_L or LED_OFF_R

Per-side brightness: LED_BRIGHT_L B=0.2, LED_BRIGHT_R B=0.4

Adjust zone split: edit left_to/right_from in LED_ZONES.
