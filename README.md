# SmoothBus T2A

An adaptation of the [SmoothBus project](https://github.com/PegorK/SmoothBus/tree/main) for the early VW bay window bus (Type 2A). Replaces the original fuel gauge mechanism with a servo-driven needle controlled by an ATTiny85 microcontroller, providing smooth movement and a low-fuel LED warning.

## Features

- Smooth servo motion — moves in 1° steps with a moving average filter (35-sample window) to eliminate sender noise
- Low-fuel LED warning when the sender reads in the reserve range
- Boot sweep sequence (empty → full → empty) to verify servo operation
- Compact PCB (~32mm × 14mm) designed to fit within the original gauge enclosure
- 3D-printable enclosure included

## How It Works

The ATTiny85 reads the fuel sender resistance via a voltage divider, applies a running average to smooth noisy readings, and drives a servo to the corresponding needle position. Calibration values are sourced from the [TheSamba forum](https://www.thesamba.com/vw/forum/viewtopic.php?t=693930) and tuned for the T2A sender:

| Sender (Ω) | Level   | Servo angle |
|-----------|---------|-------------|
| 10        | Full    | 10°         |
| 40        | Half    | 53°         |
| 55        | Quarter | 71°         |
| 70        | Reserve | 81°         |
| 79        | Empty   | 98°         |

## Repository Layout

```
SmoothBus-T2A/
├── src/SmoothBus/SmoothBus.ino   # ATTiny85 firmware (Arduino)
├── hardware/
│   ├── SmoothBusT2A.kicad_sch    # Schematic
│   ├── SmoothBusT2A.kicad_pcb    # PCB layout
│   ├── SmoothBusT2A.pdf          # Schematic PDF
│   ├── gerbers.zip               # Gerber files for PCB fabrication
│   ├── bom/ibom.html             # Interactive BOM
│   └── 3D Parts/body.stl         # 3D-printable enclosure
└── pictures/                     # Assembly and finished photos
```

## Resources

- [Interactive BOM](https://htmlpreview.github.io/?https://github.com/theHeathLee/SmoothBus-T2A/blob/main/hardware/bom/ibom.html)
- [Schematic PDF](https://github.com/theHeathLee/SmoothBus-T2A/blob/main/hardware/SmoothBusT2A.pdf)
- [Firmware README](src/README.md) — flashing instructions (Arduino Mega as ISP + ATTinyCore)

## Photos

![Exploded view render](https://github.com/theHeathLee/SmoothBus-T2A/blob/main/pictures/explodeddiagramrender.png?raw=true)

![Face removed](https://github.com/theHeathLee/SmoothBus-T2A/blob/main/pictures/faceremoved.jpg?raw=true)

![Illuminated](https://github.com/theHeathLee/SmoothBus-T2A/blob/main/pictures/iluminated.jpg?raw=true)

![Paper layout](https://github.com/theHeathLee/SmoothBus-T2A/blob/main/pictures/paperlayout.jpg?raw=true)

## Credits

Original SmoothBus design by [Pegor Karoglanian](https://github.com/PegorK/SmoothBus/tree/main).
