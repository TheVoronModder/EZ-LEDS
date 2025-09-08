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
Folder-Based NeoPixel Control for Klipper

L/R/CL/CR/TH groups • solid colors • pulse • chase • progress • zero Python extras

This mini system lets you run different colors/effects on five LED groups:

L = Left frame

R = Right frame

CL = Chain-Left (drag-chain/side)

CR = Chain-Right

TH = Toolhead

All logic is pure Klipper macros/Jinja. No additional Python modules or led_effect plugin needed.

✨ Features

Two files only: a user file you edit, and a core engine you don’t.

Zones or whole strips per group (map any group to a subrange or a whole [neopixel]).

Simple API per group: LED_*, LED_OFF_*, LED_BRIGHT_*, LED_EFFECT_*.

Effects: pulse, chase, progress (based on print progress), or off.

One ticker updates all active effects and sleeps when nothing animates.

📦 Install

Add these includes to your printer.cfg:

[include leds_user.cfg]   # you edit this one
[include leds_core.cfg]   # engine (do not edit)


Place both files next to printer.cfg.

You only edit leds_user.cfg for your pins, LED counts, and group mapping.

⚙️ Configure (leds_user.cfg)
1) Declare your hardware

Add one or more [neopixel ...] blocks for each physical device:

[neopixel main_strip]
pin: PB0
chain_count: 60
color_order: GRB
initial_RED: 0
initial_GREEN: 0
initial_BLUE: 0

[neopixel toolhead_strip]
pin: PB1
chain_count: 8
color_order: GRB
initial_RED: 0
initial_GREEN: 0
initial_BLUE: 0

2) Map groups to strips or zones

At the top of leds_user.cfg you’ll see:

[gcode_macro LED_GROUPS]
# type: "strip" = whole device, "zone" = index range on device
# led:  name of your [neopixel ...]
# from/to: 1-based index range (only used when type="zone")

# LEFT frame (first 15 LEDs on main strip)
variable_L_type: "zone"
variable_L_led:  "main_strip"
variable_L_from: 1
variable_L_to:   15

# RIGHT frame (last 15 LEDs)
variable_R_type: "zone"
variable_R_led:  "main_strip"
variable_R_from: 46
variable_R_to:   60

# CHAIN-LEFT
variable_CL_type: "zone"
variable_CL_led:  "main_strip"
variable_CL_from: 16
variable_CL_to:   30

# CHAIN-RIGHT
variable_CR_type: "zone"
variable_CR_led:  "main_strip"
variable_CR_from: 31
variable_CR_to:   45

# TOOLHEAD (dedicated ring/strip = whole device)
variable_TH_type: "strip"
variable_TH_led:  "toolhead_strip"
variable_TH_from: 1
variable_TH_to:   99999   # ignored for type="strip"

# Defaults (optional)
variable_brightness_L: 0.30
variable_brightness_R: 0.30
variable_brightness_CL: 0.30
variable_brightness_CR: 0.30
variable_brightness_TH: 0.30
variable_tick_fast: 0.05    # pulse/chase speed
variable_tick_slow: 0.25    # progress update
gcode:
  # holder


Tip: If you have completely separate left/right/chain strips on their own pins, set that group’s *_type to "strip" and point *_led to the device name. from/to will be ignored.

🚀 Reload

Restart Klipper (UI “Restart Firmware” or RESTART). The defaults above are applied on boot.

🎮 Commands

All commands accept either 0–255 or 0–1 color inputs.

Solid color
LED_L  R=0   G=64  B=255     ; Left: blue
LED_R  R=255 G=160 B=64      ; Right: warm
LED_CL R=0   G=255 B=120     ; Chain-L: teal
LED_CR R=255 G=0   B=90      ; Chain-R: magenta
LED_TH R=255 G=255 B=255     ; Toolhead: white

Turn off a group
LED_OFF_L
LED_OFF_R
LED_OFF_CL
LED_OFF_CR
LED_OFF_TH

Brightness per group (0..1)
LED_BRIGHT_L  B=0.20
LED_BRIGHT_R  B=0.40
LED_BRIGHT_CL B=0.35
LED_BRIGHT_CR B=0.35
LED_BRIGHT_TH B=0.60


If a group is in solid mode, changing brightness re-applies its color automatically.

Effects per group
LED_EFFECT_L  MODE=pulse
LED_EFFECT_R  MODE=chase
LED_EFFECT_CL MODE=progress
LED_EFFECT_CR MODE=off
LED_EFFECT_TH MODE=pulse


pulse – breathing brightness of the current color

chase – moving bright “dot” with a dim trail

progress – fills based on print progress (0–100%)

off – disables the effect for that group (solid/off colors stay as set)

🧩 Example setups
One frame strip + toolhead ring

Map L/CL/CR/R to zones on main_strip

Map TH to toolhead_strip with type="strip"

Two independent frame strips

Declare:

[neopixel left_frame]  pin: PB2 chain_count: 30 color_order: GRB
[neopixel right_frame] pin: PB3 chain_count: 30 color_order: GRB


Then set:

variable_L_type: "strip"
variable_L_led:  "left_frame"
variable_R_type: "strip"
variable_R_led:  "right_frame"


Keep CL/CR as zones (or give them their own strips).

🔁 Hook into your print macros (optional)
[gcode_macro PRINT_START]
gcode:
  ; Warm “heating” glow with pulse
  LED_L  R=255 G=80  B=0
  LED_R  R=255 G=80  B=0
  LED_EFFECT_L  MODE=pulse
  LED_EFFECT_R  MODE=pulse

  ; ... your heating/homing ...

  ; Solid “printing” color
  LED_EFFECT_L  MODE=off
  LED_EFFECT_R  MODE=off
  LED_L  R=0 G=64 B=255
  LED_R  R=0 G=64 B=255

[gcode_macro PAUSE]
rename_existing: PAUSE_BASE
gcode:
  PAUSE_BASE
  LED_TH R=255 G=255 B=0
  LED_EFFECT_TH MODE=pulse

[gcode_macro RESUME]
rename_existing: RESUME_BASE
gcode:
  RESUME_BASE
  LED_EFFECT_TH MODE=off
  LED_TH R=255 G=255 B=255

🛠️ Troubleshooting

Nothing lights up
Check pin, chain_count, and color_order in your [neopixel ...]. Then RESTART.

Wrong section lights
Your physical order may differ—adjust the from/to ranges in LED_GROUPS.

Zone commands don’t do anything
Zones use 1-based indices. Make sure your ranges fall within the device’s chain_count.

High CPU / flicker
Increase variable_tick_fast from 0.05 → 0.08 (lower refresh rate), or avoid running multiple effects simultaneously on many LEDs.

📁 File layout (for reference)
printer.cfg
leds_user.cfg   # <-- you edit this one
leds_core.cfg   # <-- engine (do not edit)

✅ Notes

100% Klipper/Jinja macros: no external Python extras.

One engine ticker updates all groups and sleeps when no effects are active.

Safe batching with TRANSMIT minimizes SPI/PIO spam.
