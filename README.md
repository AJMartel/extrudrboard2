# extrudrboard2
Hardware for a proposed revision of the Extrudrboard for
multi-color/multimaterial printing

The latest revision of the Printrboard (REV F6) is mildly incompatible
with the original
[Extrudrboard](http://reprap.org/wiki/Adding_more_extruders#RAMPS_using_ExtrudrBoard),
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

The multiplexing scheme here is inspired by the "Super Switch" of
Prusa, and in fact basically the same Marlin code (`MK2_MULTIPLEXER`)
can be used.  One wrinkle is that the Printrboard extruder output
(we'll call it E0) wants to be a [Gear Head
Extruder](https://printrbot.com/shop/gear-head-extruder-v2/) with 127
steps/mm, while the individual bowden drivers (E1-E4, driven by the
Extrudrboard2) may be the lower cost 96 steps/mm [Alu
Extruders](https://printrbot.com/shop/printrbot-alu-extruder-v2/) --
or even the short-lived injection-molded plastic extruder.  So some
software cleverness is needed to allow multiplexing different
extruders with potentially different steps/mm rates.

There are two versions of the board here.  The
[`Extrudrboard2.sch`](./Extrudrboard2.sch.pdf) files are an initial
prototype that allows you to connect two original Extrudrboards to the
Printrboard using the new multiplexing signal scheme.  It uses some
random logic ICs for the multiplexer that I just happened to have in
my toolbox.  I had to make three, so I've got a couple extra.  You
could also order this from [OSH
Park](https://oshpark.com/shared_projects/wLrvnUeh) -- warning,
untested!

If Printrbot decided to actually adopt this "project" as a "product",
they'd want something more like
[`Extrudrboard.sch`](./Extrudrboard.sch.pdf), which integrates the
four stepper drivers from the two old extrudrboard into a single new
board.  I actually reused as much as possible of the original
Extrudrboard schematic, components, and component packages, so this
should be highly compatible with whatever manufacturing process
Printrbot had for the original Extrudrboard.

-- C. Scott Ananian <cscott@cscott.net>
   Printrbot owner since Christmas 2014
