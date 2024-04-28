# Why even bother doing this?

Once upon a time, there were video game consoles that output composite video natively and thus the games were appropriately designed with composite
video and shitty consumer grade NTSC CRT TVs in mind. Then emulation happened and suddenly people thought, "hey, this thing looks better on my computer
than it does on my TV". Thus everything was ruined forever and CRT technicians were cursed with the worst kind of customer: the RGB Retro Gamer.

The RGB Retro Gamer is the CRT repairman's equivalent of an audiophile: a moron who insists on having his retro consoles look exactly like they do in an emulator.
He is a fool who is very easily parted from his money, which was a major reason why I decided to make this. He demands that his TV have RGB inputs (normally only
used on professional-grade equipment and arcade monitors) so that he can get as clear a picture as possible from consumer-grade equipment. This is why he insists
that technicians install the worst connector of all time to his TV. It is a single syllable that strikes fear into the hearts of sane people.
Yes, we have to talk about SCART.

SCART is as big of a French fuckup as existentialism, the auteur theory, the Magniot line, wine tasting, the SECAM color system, Marcel Duchamp, King Louis XVI,
and France itself. Yet it is the only widely accepted consumer-grade 15 kHz RGB video standard because nobody bothered to come up with a better one. In particular,
RGB Retro Gamers insist on using SCART because virtually all console RGB cables use it. If I were to use BNC like a sane person (it's what the PVM users do, anyway),
the RGB Retro Gamer would scowl at me and I wouldn't be able to make money. So, unfortunately, I must appease the fascists and design a circuit centered around
a cumbersome connector that is not widely available in civilized parts of the world and instead must be ordered from companies named Shenzhen Bongfong Precision Electronic Co. Ltd.
and arrive ten months later having been routed through Estonia of all places.

The majority of SCART mods you see online involve weird muxers, hardwired switches and all sorts of crap that I didn't want to bother with. I was more interested
in adding the SCART port to TVs in such a way that the SCART port functions exactly like a normal port on the TV. Unfortunately, this adds a ton of logic, and I'm
a noob at electronics, so the resulting circuit is convoluted, but it at least works with the TVs I've tried it on, which is why I'm releasing it.

# Prior (f)Art

RGB mods have been around for a while. They typically take on one of the following forms:

* **Switch of Shame**: A switch is used to force SCART blanking on so that RGB coming into the TV is always displayed. This may or may not
  cause problems with the OSD, which is why most installs typically use...
* **Passive mux**: Diodes and resistors are used to mix signals together, allowing the OSD to be used while RGB is being injected. While
  it's still better than the Switch of Shame mod, the OSD blanking signal is merely mixed with the RGB blanking signal, resulting normally
  black backgrounds in menus being filled in with the background RGB video. Any installer worth a damn usually uses the passive mux mod.
* **Active mux**: Similar to the passive mux, only a video switch IC does the work. The OSD takes priority, so if the MICOM blanking signal
  goes active, the injected RGB signal is blocked.

So what do these all lack?

* **Simple-as-possible installation**: Unfortunately, RGB mods will always be difficult to do. There's too many factors involved for it to be a straight
  up easy job. However, certain bits could be simplified, particularly not having to pick random resistors, diodes and capacitors.
* **RGB signal interfering with other video inputs**: Modders like to assume that your TV will never leave the RGB input, or that you'll
  nicely switch off your RGB device before switching back to RF or to another composite/component input. This will obviously cause interference
  when you do, because the RGB video will keep being fed into the TV, but not synced correctly.
* **Input protection**: So many of these RGB mux mods lack critical overvoltage/overcurrent/ESD protection on their inputs, leaving the TV
  exposed to danger.

The TV Desecrator attempts to solve these problems, and probably fails at doing so. Guess it's the thought that counts.

