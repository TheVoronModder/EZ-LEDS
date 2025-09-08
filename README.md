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
>00_hw.cfg
```# === Hardware: declare a NeoPixel strip ===
[neopixel rear_strip]
pin: <mcu_pin_here>      # e.g. PB0 or gpio26
chain_count: 30
color_order: GRB
initial_RED: 0
initial_GREEN: 0
initial_BLUE: 0
```

