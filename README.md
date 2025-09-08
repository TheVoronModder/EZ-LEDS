# EZ-LEDS
Easy LED control NO Python or added installations

2 config files! Thats it!

Now, NEVER EVER EVER EVER EVER EVER Touch the leds_core.cfg 

I will not be able to help you due to #1, I do not have the time... SORRY!

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

>[!WARNING]
>add the folder to your klipper files section (drag and drop)
>
>within printer.cfg under your includes section add this:
>
>`[include leds_user.cfg] # you edit this one` 
>`[include leds_core.cfg] # engine (NEVER TOUCH THIS)`
>
>



>[!NOTE]
>How to use
>
This mini system lets you run different colors/effects on five LED groups:
L = Left frame

R = Right frame

CL = Chain-Left (drag-chain/side)

CR = Chain-Right

TH = Toolhead

All logic is pure Klipper macros/Jinja. No additional Python modules or led_effect plugin needed.


>[!NOTE]
>features
>
>Two files only: a user file you edit, and a core engine you don’t.
>
>Zones or whole strips per group (map any group to a subrange or a whole [neopixel]).
>
>Simple API per group: LED_*, LED_OFF_*, LED_BRIGHT_*, LED_EFFECT_*.
>
>Effects: pulse, chase, progress (based on print progress), or off.
>
>One ticker updates all active effects and sleeps when nothing animates.

