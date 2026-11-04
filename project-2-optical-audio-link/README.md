# Two-way optical audio link

This project combines analog audio processing with optical communication.
The design goal is a board that can receive audio, drive a speaker, and send
a combined audio signal through a modulated laser to another board.

## Design goals

The course brief calls for three inputs: an external audio device, an optical
receiver such as a photodiode or solar cell, and a microphone. Each input needs
independent adjustment. The receiver should reproduce the external and optical
audio inputs at a speaker; the transmitter should combine the three inputs
and send the result optically. Four-level indicators are specified for each
input channel.

Baseline targets include a link distance of at least 20 feet and 1 W of speaker
output, with a separate sound-level criterion. The longer 100-foot and 200-foot
distances in the assignment are bonus targets. None of these distances or
output levels is a verified result in the uploaded draft.

## Included schematic

`ltspice/Draft2.asc` is the original draft. It contains eight OP07 symbols,
coupling capacitors, resistor networks, diode branches, a microphone annotation,
and a resistor named `speaker`. The file does not by itself establish a complete
optical channel or a demonstrated two-way link.

| Item | What is in the file |
|---|---|
| Op-amps | 8 OP07 symbols |
| Supply/source values | Five voltage sources entered as 4.5 V |
| Speaker approximation | A 7.5 Ω resistor named `speaker` |
| C1 and C3 | `1µ` in the original file's character encoding |
| C2 | `1` with no unit prefix: SPICE interprets this as 1 F |
| Analysis directive | `.tran 5` |
| Output devices | Generic diodes rather than explicitly identified LEDs |

The original file uses a legacy text encoding for the micro symbol. Keep its
bytes intact when uploading; if an editor corrupts that symbol, a working
copy can use the unambiguous ASCII value `1u` after confirming the intended units.

## Signal-chain concepts

- **Input conditioning:** coupling capacitors and resistors can remove DC bias
  and set a high-pass cutoff. Their values must suit the desired audio band.
- **Gain and mixing:** op-amp stages can amplify and combine signals, but their
  precise gain depends on feedback connections and source impedances.
- **Optical channel:** a transmitter must modulate optical output, while a receiver
  converts received light back into an electrical signal. Alignment, ambient
  light, bandwidth, and noise affect the recovered signal.
- **Output drive:** a voltage-amplifier stage and a speaker-power stage have
  different current requirements. Check the device's output-current capability.
- **Indicators:** threshold stages can show signal level, but LED model, polarity,
  current limiting, and signal dynamics still need checking.

## Speaker-power calculation

For a sine wave into the assignment's idealized 8 Ω resistive load:

```text
P = Vrms² / R
Vrms = sqrt(1 W * 8 Ω) = 2.828 V
Vpeak = sqrt(2) * Vrms = 4.000 V
Irms = Vrms / R = 0.354 A
Ipeak = Vpeak / R = 0.500 A
```

A 3 V peak sine wave into 8 Ω is only 0.5625 W. The brief's approximate
3 V amplitude and 1 W target therefore need a clearly defined amplitude
convention and an actual power measurement. Do not infer 1 W from peak voltage
alone. The saved draft uses 7.5 Ω, so substitute that value when analyzing it.
An OP07 should not be assumed capable of supplying half an ampere to a speaker;
a suitable output stage and its supply headroom need explicit verification.

## Checks before running

1. Confirm whether C2 was intended as 1 F or a prefixed capacitance such as 1 µF.
   Do not change it without recording the intended design value.
2. R12 and R13 lack explicit saved `SYMATTR Value` entries; set intended values
   in the working copy before simulation.
3. Check OP07 rails, common-mode limits, output swing, feedback, and loading.
4. Define the test signal. The saved voltage-source values are DC 4.5 V; no
   sine-wave stimulus is recorded in those source values.
5. Identify the actual microphone, optical receiver, and laser-driver models.
   A text annotation or diode symbol does not establish the optical transfer path.
6. Confirm how every required channel's gain and four-level indication are
   implemented. The draft does not demonstrate all required channel indicators.
7. After selecting a test frequency, choose a transient duration and maximum
   timestep suitable for waveform inspection rather than relying only on `.tran 5`.
8. Check output voltage and current together; calculate average load power over
   steady-state cycles and inspect clipping.

## What to document from actual tests

For each test, record input source and amplitude, frequency, supply rails,
gain setting, load, received waveform, noise or clipping, and LED behavior.
For the optical link, record measured separation, alignment, ambient conditions,
and whether communication was one-way or simultaneous two-way.

Breadboard photos, oscilloscope traces, link-distance measurements, and output-
power measurements have not been supplied here. Add them before reporting
those quantities as achieved performance.
