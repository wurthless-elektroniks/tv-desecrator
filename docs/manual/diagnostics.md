## Diagnostics and troubleshooting

### Blinkenlights

There are four blinkenlights on the TV Desecrator board. Here is what they mean.

* Red: +5V present. Board is receiving power. The board should only power on when the TV is "on" (i.e., not in standby).
* Blue: SCART RGB blanking signal detected.
* Yellow: MICOM blanking signal active. This must turn on or blink when the TV's OSD is active.
* Green: SCART RGB injection signal active.

Intended operation:

* Red only means the board is powered.
* Yellow and Green should never light unless Blue is lit.
* Yellow and Green should never light at the same time, except when the OSD is active.

### Troubleshooting

Here are some problems I've encountered and their causes.

#### Picture looks exactly like composite

That's probably because it is. The TV Desecrator falls back to composite over SCART if it sees no RGB blanking signal.
Make sure the blue and green diagnostic lights toggle.

#### SCART RGB signal detected but RGB never injects

RGB_SELECTED isn't going active. Green diagnostic light should be toggling. Logic chips might be bad.

#### RGB injects all the time

Bridged solder joints somewhere. Can also cause major thermal stress on the NAND gate.

#### Ghosting

You're missing pulldown resistors on the RGB lines.

Missing pulldowns on the input result in extensive ghosting. This will happen on the output side too, but not quite as messy.

#### Inverted colors

Probably swapped wires somewhere. RGB lines are often creatively routed on the chassis, so it's not often clear which lines are which.
Check schematics and try again.

#### Screen is yellow and blue

Red/green lines are shorted

#### Screen is too dark

Capacitance on the output is probably too high. Change CC1, CC2, CC3 to a different capacitance value (they are 0.47uF by default).

#### Dark screen with dotted highlights

Unwelcome pulldown on output side

#### Screen is way too bright

RGB line voltage is too high. Put resistors inline to darken the picture.

**TTL-level RGB is the kiss of death for your TV chassis.** The TV Desecrator attempts to prevent you from frying your TV, but it will
likely sacrifice itself in the process. Some overvoltage/overcurrent protection is there, but it's only there to prevent
bozos from feeding anything into the TV that is way out of spec.

#### OSD has missing colors or backgrounds

I've found in testing that the blanking signal from the MICOM can be a little finicky.
My JVC has an odd blanking circuit that I'll replicate here:

(You can ignore the inductor because it's a jumper on the chassis.)

That 47pF capacitor across the 1800 ohm resistor seems unimportant, but removing it caused issues
with the blanking signal. The OSD no longer showed red or yellow colors (whites were fine),
and the black backgrounds of menus/volume controls no longer displayed.

#### No picture on Nintendo 64 even though RGB is being injected

The N64 needs to be modded to support RGB. Install the mod and try again.

#### Unwelcome video noise

There are several possible causes:

- Composite video causing background interference. Try a sync stripper.
- Your SCART cabling sucks. Try other consoles, cables, etc. to isolate the problem.
  Lots of Chinese-made SCART cables tend to be cheapo.
- RGB wiring inside your TV is capacitively coupling to something else. TV chassis cause a lot of noise.
  Try decoupling the wires to ground somehow (twisted pair, shielded wiring, etc.).


#### Picture off-center

This is normal. If it bothers you, change settings in service mode (if possible).