# Updating your Klipper config for Tap

There are some changes you'll need to make to get Tap working properly.

1. import all the cfg files and include `tap_settings.cfg` into your `printer.cfg`.

2. add the activate and deactivate gcode found at the bottom of the `tap_settings.cfg` to the `[probe]` section in your `printer.cfg`.

3. add `[save_variables]` to your config.

4. replace any instance of `BED_MESH_CALIBRATE` with `BED_MESH_CALIBRATE_PROPER`, this is largely for KAMP compatibility.

After that, you can configure the Z acceleration when probing, the homing position; and the speed multiplier thereof, and turn on the z tilt and QGL macros so that `NOZZLE_BRUSH` works properly. One thing you need to put in as a copy of your config is the default Z acceleration.

## Note make sure to run `SET_PROBE_TEMP` at least once. This sets the minimum probe temp for your print surface and saves it to the variables file. This varies by print surface but there are some general values below

|Surface|Temp range(C)|
|--|--|
|PEI (any)|150-155|
|Polyploplene|100-110|
|Galorite (G10)|130-150|
|Borosilicate Glass|200-230|
