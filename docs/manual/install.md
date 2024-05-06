# Installation

## Identifying a RGB-capable set

Find a CRT TV matching these specifications:
- Manufacture date in the 1990s or 2000s
- Must have composite video input, **preferably only one video input**
- Must have on-screen display
- Sets with component and composite on the same video input are of particular interest (I'll explain why)

Once you have found your TV of choice, open it up and study the circuitry. You are looking for the following:
- MICOM chip: a microcontroller looking thingy near the front panel controls.
  It receives power in standby (typically +5V) and will have an integrated RGB video output.
  Near the MICOM, you will find...
- TTL to 0.7V (1Vpp) RGB conversion circuit, which is usually nothing more than three voltage dividers
  for each of the RGB channels. Usually identifiable by a trio of 4.7k resistors close to the MICOM.
- The blanking control circuit, which the MICOM chip uses to take priority over the NTSC output.
  This is typically +5V at the source, but is often knocked down to a lower voltage.
- The RGB in-line capacitors. There will be three of them, and they will all be the same value.
  In many cases they will be surface mount caps right next to the inputs on the jungle chip.
  However it's common for these caps to be electrolytics.
- And, most importantly, the jungle chip, which is an all-in-one chip that decodes NTSC signals,
  overlays the OSD, and drives the RGB signals on the CRT itself.

The TV Desecrator is NOT compatible with the following types of TV chassis:
- All-in-one MICOM/jungle chip with no external RGB inputs
- MICOM logic operating at 3.3VDC (the TV Desecrator assumes 5VDC)
- Jungle chips that use "digital" RGB inputs, or any RGB signal that isn't 0.7V

**TVs from the 1980s and earlier will NEVER be supported.** Their circuitry is all analog, the picture they
produce is inferior to the more modern sets, and they have massive retro and collector appeal that will be
dashed the second you graft a SCART connector onto them. Plus which, RGB video can't be used to drive
the electron guns directly. Leave those sets for the collectors and restoration guys. They'll thank you for it.

Note that some TVs have composite and component signals coming in on the same video input (Toshiba sets call
the input "COLOR STREAM"). The jungle chip on those sets *might* have a pin that toggles the component lines
between YPbPr and RGB. **These sets aren't supported by this mod, but I might tackle them as a separate project one day.**

And, most importantly, **test your TV in full before modding it!** That way you'll know how it's supposed to work.

## Testing procedure

Before you hack apart your TV, you'll need to test it in full. If you have the remote control, that's great news because you'll be
able to go into service menus if your set has any.

Connect as many video sources as possible to see how the set behaves with a given input. Play around with some games to try
to get the image to distort. Make notes on how every OSD screen behaves. Take pictures and video if need be.

Also check how audio input is handled with RCA stereo connections. When you have only the left channel plugged in, does it play
over both speakers? If you connect a dummy input to the right channel input, does the right channel mute?

**Remember: All of the information you gather before even opening the set will help you in the long run.**

## Forming the plan of attack

By the time your TV is in pieces on the floor of your studio apartment and you've gotten to this sentence,
you have without a doubt have read the schematics. Thus you will know that **the TV Desecrator sits between the
MICOM and jungle chips, allowing RGB in from a SCART video source when it is allowed**. This provides the
challenge that you now face during the installation.

The general installation procedure is:

- The **TTL-level (+5V) blanking signal** must be rerouted to the TV Desecrator, and the TV Desecrator's mixed blanking
  signal must be returned in its place. There is typically a resistor limiting current from the MICOM's blanking pin
  to the jungle chip's input, usually around 1.5k to 2k. Measure this resistor, then put an equivalent resistor in line
  from the TV Desecrator's blanking output. Failure to do this will cause problems, such as OSD colors/black levels being
  incorrect.
- The **0.7V-level RGB signals prior to the capacitors** must be rerouted to the TV Desecrator, and the TV Desecrator's
  multiplexed RGB signals must be returned to the opposite end of where the capacitors formerly sat.
- A suitable DC power source must be located to power the 5 volt voltage regulator on board the TV Desecrator. Though many
  sets have a +5V power source, it's designed only to run the MICOM and is on all the time (i.e., in standby).

The TV Desecrator does not carry composite video or audio, but you'll have to get them out of the SCART connector and route
them as follows:
- The composite video signal must go to the composite video input. This is trivial. I don't even know why it was worth mentioning.
- The audio inputs must go to the... well, the audio inputs. If your set is mono, mix the two guys together with resistors.
  If your set stays in mono mode no matter what you do, it's because the RCA jacks have an internal switch that is toggled when
  you stick something in there. You might need to hack the RCA connectors to get around this limitation.

This is difficult already, but now you have to deal with the most annoying thing of all...

## Knowing when to inject RGB

Also called "why every RGB modder just uses a switch".

RGB_SELECTED is a signal that, when active, will get the TV Desecrator injecting RGB video. It can be set as
active high (jump HI) or as active low (jump LO); the input is always pulled low via a 10k resistor.

Recall that RGB video is injected if and only if:
- 1. the SCART blanking signal has been detected,
- 2. the MICOM is not displaying anything (MICOM_BLANKING is low), and
- 3. RGB_SELECTED is active (somehow)

Or, in boolean terms:

    RGB_IS_ACTIVE = !RGB_INHIBIT = !(SCART_BLANKING && !MICOM_BLANKING && RGB_SELECTED)

So how do you find the RGB_SELECTED signal? Here are some ideas.

### Trivial difficulty: Always on

Jump LO and let RGB_SELECTED float. Pulldown resistors will do their job. RGB will always be injected
as long as conditions 1. and 2. are met. And that will obviously cause interference when you switch video inputs.

In short, this makes the TV Desecrator behave like a normal diode mux mod. 

### Easy difficulty: The Switch of Shame

To defeat the purpose of this being a switchless mod, or to force RGB off, you may add a switch somewhere.
How you choose to do it is up to you:

- Switching the SCART blanking signal (with a switch on the breakout board or somewhere inbetween)
- Switching RGB_SELECTED between +5V and ground

This will still cause problems when you switch video inputs, but at least you have slightly more control over
when the thing injects RGB.

You're also free to add a three-setting toggle switch with ON, AUTO and OFF positions that allows you to force RGB on (pulled up)
or off (pulled to ground), or to fallback to automatic mode (using the SCART blanking signal received at the SCART connector).
**Just be careful that the SCART blanking signal you feed to the TV Desecrator stays within 1-3VDC!**

### Medium difficulty: Sync signal comparison

Jungle chips typically have a composite video output signal either because there's a video output on the
back of the TV, or the signal needs to be routed to the MICOM so that it can display closed captions.
Using two sync strippers and a microcontroller, you can easily match up the sync pulses on the composite
signals and generate the RGB_SELECTED signal as appropriate.

### Hard difficulty: MICOM I/O pins

Some TV manufacturers had the decency to have their MICOM programs output a status indicator on the GPIOs.
If you can find an active high or active low signal that reliably indicates when the video input of your
choice is selected, you can use that. Schematics, and occasionally 74-series logic chips, will be your
best friend here.

### Nightmare difficulty: I2C bus schenanigans

Virtually all CRT TVs use the I2C protocol for communications between the MICOM and other components, including the jungle
chip and RF tuner. Pick a suitable I2C target, study its protocol, and write a simple microcontroller program to produce
RGB_SELECTED. You can then have the MCU sit on the bus as a sniffer, or to act as an intermediary.

This, however, is far easier said than done. The I2C bus is extremely fragile and tampering with it will cause you
far more headaches than it's worth. It's a mission critical part of the TV set and if it isn't working correctly you
will cause major problems.

Examples of what can happen when you tamper with the I2C bus:
* TV won't even turn on
* MICOM locks up and the TV becomes totally unresponsive
* MICOM runs normally but the RGB drives are totally dead

I2C is ancient technology from the 1980s, it's too susceptible to noise and interference, and if you're missing a pullup
somewhere it will shit the bed. So don't play with it unless you want to spend day after day cursing at an ancient TV set.

### Impossible difficulty: Hacking the MICOM program

All MICOMs you'll find in CRT TVs will use mask ROMs. However, it's likely that the same ROM is shared between different models
of TV, with the EEPROM containing model-specific configuration loaded at startup. Nefarious hackers could try to modify the program
such that normally unused I/O lines on the MICOM could be made to output the RGB_SELECTED signal. This is hugely ad hoc-y though
and I doubt it's even possible to do because MICOM documentation is hard to find.

## Recalibration

Once you've powered your TV on and made sure everything works, you'll need to recalibrate colors.
You must do this for both composite video and for RGB video.

Typical recalibration involves the following:
- Generate a test pattern somehow. If you're a cheapskate, you can just use one of the OSD menus.
- Set SCREEN to minimum on flyback, then, with RGB active, start increasing until your test pattern is nice and bright.
- If you can get into the service menus, recalibrate RGB gain and cutoffs. Older sets have these as potentiometers on the boards.
- Switch over to composite and begin tweaking brightness, contrast and hue settings. The jungle chip usually won't apply any
  of these to the RGB signal, they're for NTSC only.

Now all you need to do is install the breakout board and you're done. I won't cover that, obviously, because that's a lot
of work with Dremels and screws and whatnot.
