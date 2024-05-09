# So why don't TVs have RGB connectors (or that they do)?

Long story short: analog television standards. Televisions were never meant to do anything other than receive programs. 
This only really changed because the market did.

Color TV tubes have worked on the RGB color space from the very beginning, but the problem is that sending RGB signals
over the air is not feasible, and it especially wasn't back in the 1950s when the NTSC standard was adopted. NTSC
set the tone for all analog color standards after, in that the signal needed to be compatible with monochrome sets
and needed to transmit color in the most bandwidth-efficient way possible.

RGB only really became relevant on the consumer end for two reasons:
1. Digitally-generated signals, as from computers and video game consoles
2. France (those fuckers again)

A lot of early home computers generated RGB directly but were forced to output composite video because it turns out that
the average consumer didn't want to buy an expensive monitor just to use their shiny new Apple II. Televisions were never
intended to be computer monitors; they ended up being repurposed.

It was around this time that the SCART standard came onto the scene, not just because of all these devices outputting
native RGB, but because the French were so proud of themselves that they went with the SECAM standard while the rest
of Europe went with PAL. If someone from France bought a PAL video game console, they'd find it was incompatible with
their SECAM TV. So they'd either have to buy an inferior SECAM version (if one was even available) or find a PAL converter.
It's the same case with VHS: PAL videotapes aren't compatible with SECAM TVs, even though both standards are 50 Hz.

Having RGB on the SCART connector killed both of these issues with one stone. Consoles could simply output RGB to a
French TV without having to deal with different encoding schemes, and PAL/RGB conversion (or even NTSC/RGB conversion)
could easily be done on a single chip.

So why, after all this, did we end up with S-Video and YPbPr?
- S-Video was a videotape standard (and thus limited by videotape bandwidth)
- YPbPr was three signals as opposed to analog RGB, which usually requires four (R/G/B/CSYNC) or five (R/G/B/HSYNC/VSYNC)

Analog video sucked and that's why HDMI replaced it. All these incompatible standards were replaced with a single one
and nobody had to worry about this bullshit ever again. Except if they're retro gamers or anyone dealing with CRTs,
in which case this shit will never end.
