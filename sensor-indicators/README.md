# Temperature and light indicators

This project explores how resistance changes from thermal and optical sensors
can be translated into visible indicators using voltage dividers, reference
voltages, and op-amp comparator stages.

## Design goals

The temperature channel is intended to light one through eight LEDs as the
thermistor warms, with sensitivity adjusted using one control. The light
channel has a different goal: identify the flashlight's position using one
of eight LEDs, with only one LED lit at a time. A cumulative temperature
display and a one-hot light-position display are not equivalent behaviors.

The course brief specifies split supplies of ±4.5 V, with up to ±6 V allowed.
These are requirements, not a record of a completed demonstration.

## Included schematic

`ltspice/Draft1.asc` contains two eight-stage OP07 comparator banks, resistor
reference ladders, diode output branches, and parameterized input resistors.
The sensor behavior is represented through resistance values rather than a
calibrated physical sensor model. The original filename and bytes are retained.

Features visible in the draft:

| Item | What is in the file |
|---|---|
| Op-amps | 16 OP07 symbols |
| Output devices | 16 generic diode symbols; LED models are not specified |
| Supplies | Four sources, each entered as 4.5 V |
| Sensor representation | R17 and R36 use `{R2}`; R18 and R37 are 100 kΩ |
| Output resistors | 500 Ω branches |
| Sweep text | Two copies of `.step param R2 100k 70k 1k` |

These observations describe the saved draft, not proof that it meets the
light-position or temperature-display requirements.

## How the circuit is intended to work

A divider turns a sensor resistance into a voltage. A comparator then compares
that voltage with a reference. For an ideal comparator, the output goes high
when the non-inverting input exceeds the inverting input, and low when the
opposite is true. Several references allow different stages to switch at
different input levels.

For a divider with a sensor above a fixed resistor:

```text
V_sensor = V_low + (V_high - V_low) * R_fixed / (R_sensor + R_fixed)
```

Swapping the sensor and fixed resistor reverses how the divider voltage changes
with sensor resistance. Use the actual connection order when deriving thresholds.
The formula does not establish a temperature calibration without sensor data.

## Checks before running

1. **Sweep direction:** the saved sweep runs from 100 kΩ down to 70 kΩ with a
   positive 1 kΩ increment. In a working copy, use a correctly directed sweep,
   such as `.step param R2 100k 70k -1k`, or an explicit list.
2. **Duplicate directive:** both banks share the same parameter and duplicate
   sweep text. Decide whether both should vary together, then retain a single
   intended directive rather than an accidental nested or duplicate sweep.
3. **Analysis command:** no `.op`, `.dc`, or `.tran` command appears in the
   uploaded draft. For static threshold inspection, add a suitable operating-
   point analysis to the working copy.
4. **Component values:** R13, R15, R32, and R34 lack an explicit saved
   `SYMATTR Value`. Confirm intended values before running.
5. **Models and rails:** verify diode models, OP07 supply connections, allowable
   input common-mode range, output swing, and LED-current limits.
6. **One-hot light behavior:** verify the logic or analog arrangement that turns
   off the previous light indicator. A basic reference ladder alone does not
   establish one-hot operation or encode flashlight position.

The originals have not been silently repaired; edits should be made in a copy
and documented after their intended behavior is confirmed.

## Useful validation records

Record sensor resistance, sensed voltage, comparator reference voltages, and
which outputs switch for each input condition. For a physical build, include
sensor arrangement, supply voltages, LED currents, and oscilloscope observations.
Add a separate temperature calibration only if actual temperatures are measured.

No completed validation table is included because those measurements were not
provided with the schematic.
