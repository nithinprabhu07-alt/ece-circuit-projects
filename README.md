# ECE circuit projects

Two analog circuit projects from ECE 2001 at UConn, Fall 2026. This repository
keeps the LTspice drafts alongside a short explanation of each design and the
checks needed to reproduce the work.

| Project | Focus | Files |
|---|---|---|
| [Temperature and light indicators](sensor-indicators/) | Sensor voltage dividers, reference levels, and op-amp comparators | Original `Draft1.asc` and design notes |
| [Two-way optical audio link](optical-audio-link/) | Audio conditioning, optical transmission, amplification, and level indicators | Original `Draft2.asc` and design notes |

## Current status

The original schematics are included unchanged. Documentation has been checked
against the project descriptions and the contents of the uploaded files.
LTspice execution, measured performance, and final hardware results have not
been independently verified in this repository. The notes distinguish design
targets from results; no waveform images or measurement data are included yet.

The two drafts use LTspice's **OP07** symbol. That is the model actually present
in these files; it should not be confused with a UA741 used in a hardware build.
Model choice, supply wiring, and output-drive limits need checking when comparing
simulation with the breadboard circuits.

## Open the schematics

1. Download or clone the repository.
2. Open the `.asc` file inside the selected project's `ltspice` folder.
3. Read that project's README before running it. Some draft parameters need
   attention, so opening successfully is not the same as a validated simulation.
4. Keep experimental edits in a separate copy until they have been checked.

LTspice must have the referenced OP07 symbol and model available. No custom
model files were supplied with the drafts. Simulation outputs such as `.raw`
and `.log` files are excluded by `.gitignore`; selected plots and concise
measurement tables can be added later.

## What to add next

- Circuit screenshots exported from LTspice.
- Breadboard photos with useful labels.
- Actual simulation traces and test conditions.
- A short account of design changes and troubleshooting.
- Measured results with units, equipment, and limitations.

## Documentation

The READMEs summarize the course design briefs rather than reproducing the
assignment handouts. The circuit files are the uploaded student drafts.
Repository organization and explanatory documentation were prepared with
ChatGPT assistance. Claims about hardware performance should be supported by
the corresponding test records before being added.
