# TV Desecrator: A universal-as-I-can-make-it RGB SCART circuit for non-SCART TVs

Hey, you! Are you an idiot who wishes to ruin a perfectly good TV? Then build yourself a TV Desecrator! It's a reliable way of adding a SCART connector to a TV that doesn't normally support it.

There are plenty of takes on RGB mods already, but I wanted to do one with seamless operation and simpler installation. In other words, I wanted the SCART connector to behave as if it was part
of the TV set rather than a bolt-on feature. A hell of a challenge for someone with next to no knowledge of electronics, but totally worth it in the end as long as I get to stick it to the other
modders and hopefully make a few bucks while I'm at it.

This is all discrete logic so you only get the Gerbers.

The TV Desecrator is part of the wider Jänkermeister's CRT Toolkit project, which also includes:
* The [G1 Crymax](https://github.com/wurthless-elektroniks/g1crymax)
* The [simple SCART breakout board](https://github.com/wurthless-elektroniks/scart-breakout)
* ...and possibly others

# WARNING - STILL UNDER CONSTRUCTION

TV Desecrator v6 is still undergoing testing and is not guaranteed to work correctly. Think of this as an open betatest with nobody participating (except for me).
If you order your own boards and find it doesn't work, then you forgot to read this caveat emptor.

# Features

* SCART port can function exactly like a normal input; totally switchless operation
* RGB injection that doesn't interfere with OSD and other input modes
* Safe and reliable SCART RGB blanking detection: no need to worry about 10 volt signals wrecking shit
* THS7374 video amp so the final injected signal comes in loud and clear
* Diagnostic blinkenlights to tell you where you fucked up
* Modular design so you can easily pull the TV case apart when things inevitably explode
* Modular design also means you can use BNC like a civilized person

# **BEFORE YOU INSTALL THIS, ASK YOURSELF: "DO I REALLY NEED RGB?"**

Chances are you don't. People often use RGB to compensate for poorly tuned equipment. You can get a great picture without ever having to use RGB.
To do so, perform some combination of the following steps:

* Recap entire set, particularly anything related to the power supply, horizontal/vertical deflection circuits, RGB drives, and most importantly the NTSC decode circuitry
* Recalibrate colors, drives and cutoffs if possible
* Drop G1 pin to a negative voltage and recalibrate SCREEN and FOCUS to get a sharper picture and better contrast (*this is a must on larger sets!*)
* Use component or S-Video if available (they don't suffer from composite color artifacts)
* Use a console that outputs better quality video than others in its class (in Sega Genesis terms, throw your Model 2 in the garbage and get a Model 1)

Other options for RGB gaming, besides modding old TVs, include:
* Computer monitors that support 15 kHz natively
* The usual 15 kHz to whatever-standard-you-please converters (shitty GBS converters, SCART to component, OSSC, etc.)
* If you want to live dangerously, an arcade monitor with an amp and sync stripper. (Some oldschool consoles output TTL RGB natively, you just need to know how to tap it.)

Remember: **DO NOT RGB MOD A TV SET UNLESS YOU REALLY NEED TO** <sup><sub>(or just want to scam idiot retro gamers)</sub></sup>

# Schematic

![](schematic.png)

There are two major parts of the circuit. The first is logic circuitry that determines when the RGB signal coming in from the SCART connector should
be sent to the TV; if not allowed, it selects the MICOM inputs. The second is a switcher and amplification circuit that allows the TV Desecrator
to appear to the TV as if it were a normal, everyday MICOM. The rest is all boring and not worth explaining here.

Please read the extensive documentation to learn about how this thing works, how to install it, and known issues.

## License

Public domain
