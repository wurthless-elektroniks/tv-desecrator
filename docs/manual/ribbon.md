## Ribbon connector

The TV Desecrator connects to the input device via a 14 pin ribbon connector (2x7 2.54mm).
Though designed mainly with SCART inputs in mind, the ribbon connector can just as easily accept
video from a BNC input (with the appropriate circuitry in place, of course!).

The pinout is as follows:

| Fcn        | Pin | Pin | Fcn            |
| ---------: | --: | :-- | :------------- |
|        +5V |   1 | 2   | +5V            |
|        GND |   3 | 4   | GND            |
|        GND |   5 | 6   | RED            |
|        GND |   7 | 8   | GREEN          |
|        GND |   9 | 10  | BLUE           |
|        GND |  11 | 12  | GND            |
| RGB IN USE |  13 | 14  | SCART BLANKING |

where:

* +5V is 5VDC from the TV Desecrator's 5 volt regulator
* GND is chassis ground
* RED/GREEN/BLUE are 0.7 Vpp, 75-ohm terminated RGB video signals
* RGB IN USE is a 5 volt TTL signal, active high, indicating that the TV Desecrator is pulling RGB video from this connector. This signal will
  toggle when the OSD is running, so any logic relying on this pin should have a timeout mechanism so that it stays active.
* SCART BLANKING is exactly what it says on the tin. This is a 75-ohm terminated input, and once the pulldown has been applied, the TV Desecrator
  needs to see a certain voltage (ideally 1VDC) present on this pin before it can inject RGB. **Do NOT directly supply 5V to this pin** -- use a 470 ohm
  resistor.

This connector was formerly 16 pins and carried composite video and audio signals with it. However, they were left off the board as the TV Desecrator
didn't do anything with them. It's up to the breakout board to handle those things. We're only the RGB injector.

Notice also how most of those connections are ground. That's done in an attempt to prevent parasitic capacitance from interfering with the RGB signal
on its way to the TV Desecrator. You can also use twisted-pair ribbon cable here if you feel like it.