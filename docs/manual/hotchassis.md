# The perils of hot chassis

This is a must-read for anyone attempting to modify any CRT TV or display, as it's important
for health and safety.

The TV Desecrator was designed only for television sets that are properly isolated from the mains.
I didn't really know about the hazards of hot chassis at the time, but now that I do, and have made
a very expensive computer (a Mac Studio) explode as part of this lesson, I'm writing this document to advise all
prospective modders about hot chassis, how to identify them, and the dangers of modifying them.

**The tl;dr is: NEVER attempt to modify a hot chassis. You will kill your expensive equipment and
potentially yourself.**

## What's a hot chassis?

A hot chassis is any CRT chassis where the low voltage side is directly referenced to the mains.
These tend to be seen on older or "budget" designs, where proper isolation is not required and they
assume you won't be fiddling around inside of the set.

## Identifying a hot chassis

Here are some ways of identifying a hot chassis.

1. **No transformer besides the flyback**: This is the easiest way of detecting a hot chassis.
   Trace the low voltage power supply back as far as you can go. If you don't see that it's connected
   to a switching power supply, or that there's a dropper resistor or similar knocking the voltage down
   to something the low voltage regulators can handle, then it's a hot chassis.

2. **RF-only sets**: Not always a sign you're dealing with a hot chassis but a good indicator. RF-only
   sets only need to expose one piece of metal (the RF jack) so the designs aren't concerned at all with
   safely isolating the chassis. **The tell-tale sign is whether the tuner directly terminates with a
   coax connector.** If the coaxial connector is on its own box, then that's a sign the RF input is using
   a balun to isolate the coax lead from the chassis.

3. **Chassis "ground" connected to AC neutral**: Usually on a hot chassis a resistor is all that separates chassis "ground"
   from AC neutral. Check what resistance there is between ground and the AC neutral connection; there shouldn't
   be any. On one Orion set I tested, the resistor separating chassis "ground" and neutral was approximately 16k ohms.

Note that on switching power supplies, there may be class Y capacitors tying the supposedly isolated side
with the mains. This is normal. 

## Hazards

If you attempt to modify or otherwise play with a hot chassis, you run the risk of the following:

* Any equipment you connect, including your treasured and very expensive electronics or test equipment, will likely explode
* Electrical shock and possible electrocution
* Smoke and fire

## What if I want to make a hot chassis safe?

That's not worth the cost. You'll need to isolate pretty much every input from the SCART connector, so that's
4 video signals plus two audio signals. Combine that with the fact you need specialist baluns for isolation
and you'll have a sizeable bill.

This is also the reason why you shouldn't try modifying a RF-only chassis to support RCA inputs. I had to give
up on that dream when I realized it wasn't feasible compared to SCART modding.

Save yourself the headache and find a properly isolated set.

**If, however, you ever need to work on a hot chassis as part of a repair job, an isolation transformer and
battery-operated equipment will limit the risk of zaps, ouchies and kabooms.**