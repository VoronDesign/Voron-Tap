# Voron Tap

![Voron-Tap3](images/Voron-Tap.gif)

> Animated image courtesy of [Maple Leaf Makers](https://github.com/MapleLeafMakers) , see the whole video at https://www.youtube.com/watch?v=mz5qcOZgXhI

Tap is a nozzle-based z-probe for the V2 and Trident printer designs. The entire toolhead moves to trigger an optical switch. Tap offers many advantages:

* Extreme precision 0.4μm (0.0004mm)
* Any build surface and easily change at will
* Durability via optical sensor (millions of probe cycles)
* High temperature reliability (70C to 100C)
* Simplified probe mechanics (no dock/undock macros)
* No separate Z-endstop required
* Crash protection

## Requirements

* Bed must be stable for probing force of 500-800 grams
  * Switchwire, V1.8, Legacy, V0 beds are NOT rigid enough
* Mounts to MGN-12H X-axis
* Front mounted extruder (Clockwork2, LGX, Galileo)
* Accuracy depends on good mechanical condition
* Must have 5V at toolhead or special 24V sensor PCB

## Instructions

Comprehensive assembly details are available in the [Manual](Manual/Assembly_Manual_Tap.pdf)

## Post-Install Setup

1. Update your `printer.cfg` as recommended in [Tap Klipper Instructions](config/tap_klipper_instructions.md)
2. Test virtual Z endstop by lifting tool-head and using the `M119` or `query_probe` commands
3. Home Z.
4. Heat soak your machine and run a couple `probe_accuracy samples=100` to "break-in" your probe and check there's no significant trend in the result
5. Run a few more `probe_accuracy` checks (default of 10 probes)

### Diagnosing problems

For well-built machines you can expect to see between 0.0000 and 0.0008 standard deviation. Where probe accuracy trends notably up/down over 100 samples, or standard deviation is outside the desired range, check that:
- Sampling is taking place at a constant temperature (cooling/heating of any part will result in drift)
- Z belts are tightened correctly and uniformly
- The magnets on your tap have been adjusted to mate correctly when Tap is in the down position ([see the adjustment step in Nero3D's build guide](https://youtu.be/mJNCn72lQpU?t=751))
- The rail is well greased, the balls are correctly seated and there's no swarf in the guides (eg from the manufacture)
- The StealthBurner is firmly attached onto the Tap carriage
  - A common mistake is that the tabs on the body of the SB are pushed up under the alignment screws on the carriage to seat it in place, but then not tightened - make sure to tighten these firmly!
- The `speed` parameter in the `[probe]` section of your `printer.cfg` is appropriate (try `speed=3` with `lift_speed=10`)

While originally intended for the klicky probe, the following [probe accuracy tests](https://github.com/sporkus/probe_accuracy_tests) may assist in further diagnosis.

## FAQs

* Will Tap hurt my print surface? No, probing temp is restricted to 150C. The team recommends spray coated spring steel. Users of smooth PEI may find minor burnish marks if continously probing the same spot.
* Will the hartk 2-piece PCB work with Tap? Yes, but it requires a slight modification. See discord pin.
* Can I use an optical sensor not specified in the BOM? Not recommended, the team spent considerable time validating sensors in [BOM](BOM.md).
* Can I use micro-switch instead? Not recommended, but check here for more details: [Unklicky Tap](https://github.com/majarspeed/Unklicky/tree/main/Unklicky_TAP)
* Can I use Tap with kinematic bed mounts? Yes, if your bed is rigid up to 800 grams of force.
* Doesn't this add a lot of weight? The team explored many designs and landed on ~50 extra grams as good trade-off between rigidity and weight.
* Why do I need this if my induction probe works fine? Tap enables a far better user experience as it eliminates most baby-stepping needed due to thermal expansion, nozzle & bed surface changes.
* Is Tap noticably more accurate than klicky? Yes.

## (Bonus Points) Data Science

Tap engineering is backed by data science. If you want to dive deeper check out the following resources:

* [Voron:LIVE! Voron Tap announcement stream](https://www.youtube.com/watch?v=JLUDLJQXZeU)
* [Probe accuracy across thermal envelope](https://github.com/KiloQubit/probe_accuracy)
* [Repeatability at individual corners](https://github.com/sporkus/probe_accuracy_tests)




