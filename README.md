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
>`[include leds_user.cfg]`
>`[include leds_core.cfg]`
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
