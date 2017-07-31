# Extrudrboard2
Proposed revision of [Printrbot] [Extrudrboard] for
multi-color/multimaterial printing

Thing tracker at
https://cscott.github.io/thing-tracker/#/thing/737eb982-b77f-43e0-ae38-4fc30f3e3170

## Description

The latest revision of the [Printrboard] (REV F6) is mildly incompatible
with the original [Extrudrboard],
since the HOTEND A signal used by the Extrudrboard was disconnected
and used to provide an extruder fan output.

Also, multimaterial printing doesn't actually need all of the extra
hotend and thermistor inputs.

This repo contains a proposed "Extrudrboard2" which is compatible with
Printrboard REV F6 and provides up to four additional stepper outputs,
used for multimaterial bowden extruders.  The original Printrboard
extruder stepper is used for the direct drive just before the hotend,
and these additional Extrudrboard outputs are multiplexed and used for
the individual filament options.

As a bonus, I've thrown in a FAN2 output for owners of REV F5 and
earlier Printrboards, which adds an extruder fan output which works
identically to that on the REV F6 Printrboard.

The multiplexing scheme here is inspired by the "[Super Switch]" of
Prusa, and in fact basically the same [Marlin] code (`MK2_MULTIPLEXER`)
can be used.  One wrinkle is that the Printrboard extruder output
(we'll call it E0) wants to be a [Gear Head Extruder] with 127
steps/mm, while the individual bowden drivers (E1-E4, driven by the
Extrudrboard2) may be the lower cost 96 steps/mm [Alu Extruder]s --
or even the short-lived injection-molded plastic extruder.  So some
software cleverness is needed to allow multiplexing different
extruders with potentially different steps/mm rates.

There are two versions of the board here.  The [`Extrudrboard2-thunk.sch`]
files are an initial
prototype that allows you to connect two original Extrudrboards to the
Printrboard using the new multiplexing signal scheme.  It uses some
random logic ICs for the multiplexer that I just happened to have in
my toolbox.  There was a three-unit minimum order, so I've got a couple extra.  You
could also order this from [OSH Park] as shared project
[wLrvnUeh](https://oshpark.com/shared_projects/wLrvnUeh) -- warning,
boards are not yet tested!

If Printrbot decided to actually adopt this "project" as a "product",
they'd want something more like [`Extrudrboard2.sch`], which integrates the
four stepper drivers from the two old extrudrboards into a single new
board.  I actually reused as much as possible of the original
Extrudrboard schematic, components, and component packages, so this
should be highly compatible with whatever manufacturing process
Printrbot had for the original Extrudrboard.

## Instructions

### Choose your build

If you have existing [Extrudrboard]s you wish to upgrade to the new
Extrudrboard2 functionality, use [`Extrudrboard2-thunk.sch`] with 1 or
2 original Extrudrboards connected.  If you are making new boards from
scratch, use [`Extrudrboard2.sch`].

### Assembling `Extrudrboard2-thunk`
### Wiring `Extrudrboard2-thunk`
### Assembling `Extrudrboard2`
### Wiring `Extrudrboard2`

## Related

* [Forum discussion for this project](http://forum.monstercafe.net/topic5.html)
* [Multimaterial project](https://github.com/cscott/3d-multimaterial)
* [Repo for original Printrboard/Extruderboard](https://github.com/Printrbot/printrboard)

## License

These designs are released under the
[Creative Commons Attribution Share Alike 3.0] license, like the
original [Extrudrboard](https://github.com/Printrbot/printrboard#printrboard).

[Printrbot]: http://printrbot.com
[Printrboard]: http://reprap.org/wiki/Printrboard
[Extrudrboard]: http://reprap.org/wiki/Adding_more_extruders#RAMPS_using_ExtrudrBoard
[Marlin]: http://www.marlinfw.org/
[Super Switch]: https://github.com/prusa3d/Original-Prusa-i3/issues/29
[Gear Head Extruder]: https://printrbot.com/shop/gear-head-extruder-v2/
[Alu Extruder]: https://printrbot.com/shop/printrbot-alu-extruder-v2/
[`Extrudrboard2.sch`]: ./Extrudrboard2.sch.pdf
[`Extrudrboard2-thunk.sch`]: ./Extrudrboard2-thunk.sch.pdf
[OSH Park]: https://oshpark.com
[Creative Commons Attribution Share Alike 3.0]: https://spdx.org/licenses/CC-BY-SA-3.0.html
