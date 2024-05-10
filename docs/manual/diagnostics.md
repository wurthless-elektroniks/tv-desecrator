# Diagnostics and troubleshooting

## Blinkenlights

There are four blinkenlights on the TV Desecrator board. Here is what they mean.

* Red: +5V present. Board is receiving power. The board should only power on when the TV is "on" (i.e., not in standby).
* Blue: SCART RGB blanking signal detected.
* Yellow: MICOM blanking signal active. This must turn on or blink when the TV's OSD is active.
* Green: SCART RGB injection signal active.

Intended operation:

* Red only means the board is powered.
* Yellow and Green should never light unless Blue is lit.
* Yellow and Green should never light at the same time, except when the OSD is active.

## Troubleshooting

Here are some problems I've encountered and their causes.

### No power (red light stays off)

The TV Desecrator needs a 6-12 volt power source. The jungle chip is usually supplied with approximately 7 volts.

There is no reverse polarity protection on this circuit, by the way. You'll destroy it, and possibly your equipment,
if you don't feed a positive voltage to VIN.

### Picture looks exactly like composite

That's probably because it is. The TV Desecrator falls back to composite over SCART if it sees no RGB blanking signal.
Make sure the blue and green diagnostic lights toggle.

### SCART RGB signal detected but RGB never injects

RGB_SELECTED isn't going active. Green diagnostic light should be toggling. Logic chips might be bad.

### RGB injects all the time

Immediately disconnect power and check for bridged solder joints.

### Ghosting

You're missing pulldown resistors on the RGB lines.

Missing pulldowns on the input result in extensive ghosting. This will happen on the output side too, but not quite as messy.

### Inverted colors

Probably swapped wires somewhere. RGB lines are often creatively routed on the chassis, so it's not often clear which lines are which.
Check schematics and try again.

### Screen is yellow and blue

Red/green lines are shorted

### Screen is too dark

This can be caused by resistance or capacitance anywhere on the inputs and outputs.

Capacitance on the output side will result in video that is too dark but slowly fades in after a while. If this happens, CC1/CC2/CC3
all need to be changed. They are 0.47uF by default; use a lower value if you want.

Any resistance on the input can cause the signal to be weakened because of the 75 ohm pulldowns. This is why there's an RGB amp on
the board in the first place: the signal is bound to be attenuated by the protection circuitry, particularly the thermistors.

### Dark screen with dotted highlights

Unwelcome pulldown on output side

### Screen is way too bright

RGB line voltage is too high. Put resistors inline to darken the picture.

**TTL-level RGB is the kiss of death for your TV chassis.** The TV Desecrator attempts to prevent you from frying your TV, but it will
likely sacrifice itself in the process. Some overvoltage/overcurrent protection is there, but it's only there to prevent
bozos from feeding anything into the TV that is way out of spec.

### OSD has missing colors or backgrounds

I've found in testing that the blanking signal from the MICOM can be a little finicky.

My JVC has an odd blanking circuit where the blanking signal is routed in parallel between a 47pF capacitor
and a 1800 ohm resistor. Replacing this with a single 1k resistor caused issues. The OSD no longer showed
red or yellow colors (whites were fine), and the black backgrounds of menus/volume controls no longer displayed.
If I can fix this in the future, I'll document it here.

### No picture on Nintendo 64 even though RGB is being injected

The N64 needs to be modded to support RGB. Install the mod and try again.

This will also happen if your SCART cable has the RGB blanking signal active but your console doesn't output RGB.
All SCART cables are "dumb" in that they will always signal that they are RGB cables without actually checking if
RGB video is present.

### Unwelcome video noise

There are several possible causes:

- Composite video causing background interference. Try a sync stripper.
- Your SCART cabling sucks. Try other consoles, cables, etc. to isolate the problem.
  Lots of Chinese-made SCART cables tend to be cheapo.
- RGB wiring inside your TV is capacitively coupling to something else. TV chassis cause a lot of noise.
  Try decoupling the wires to ground somehow (twisted pair, shielded wiring, etc.).

### MICOM asserts blanking when RGB present and keeps blanking asserted until reset

This is a known issue on some chassis of which the cause currently isn't clear.
The TV Desecrator always gives the OSD priority over the injected RGB picture,
but it doesn't explain why the MICOM keeps the blanking signal asserted.

The workaround is to switch the MICOM blanking signal off when RGB is on.

### Injected RGB picture off-center

This is normal. The OSD is calibrated at the factory to display only at a certain position.
If it bothers you, change settings in service mode (if possible).
