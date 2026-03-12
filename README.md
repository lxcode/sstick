# Manic Mouse

A mini implementation of the concepts pioneered by Laurie Spiegel's [Music Mouse](https: //en.wikipedia.org/wiki/Music_Mouse), for C64. Primarily a learning exercise (largely LLM-assisted) for myself to become more familiar with 6502 assembly, the SID chip, and the design of the early versions of Music Mouse.

Notes:

* Constrained to 3 voices with an optional 4th via arpeggio, but may add dual SID support for the C64U.
* Currently uses joystick, which gives no way to detect speed. As such, chords are played sequentially across the grid instead of Music Mouse's intuitive jumps. Koala Pad and 1351 support may be added.

## Controls

### Joystick (Port 2)

| Input    | Action                              |
|----------|-------------------------------------|
| Stick    | Move cursor through pitch space     |
| Fire     | Hold to mute, release to resume     |

### Keyboard

| Key   | Action                               |
|-------|--------------------------------------|
| Space | Toggle sound on/off                  |
| 1-7   | Select scale                         |
| W     | Cycle waveform                       |
| Q / E | Voice 3 octave down / up             |
| , / . | Filter cutoff down / up              |
| F     | Toggle filter                        |
| R     | Toggle envelope retrigger            |
| A     | Toggle 4th voice arpeggio            |
| C     | Toggle contrary motion               |

### Scales

| Key | Scale          |
|-----|----------------|
| 1   | Chromatic      |
| 2   | Major          |
| 3   | Minor          |
| 4   | Pentatonic     |
| 5   | Wholetone      |
| 6   | Dorian         |
| 7   | Minor Penta    |

### Waveforms

Cycled with W: triangle, sawtooth, pulse, noise.

### Voices

The screen is a 2D pitch space. Three SID voices are harmonically linked:

| Voice | Pitch source                                    |
|-------|-------------------------------------------------|
| V1    | X position                                      |
| V2    | Y position (inverted: up = higher pitch)        |
| V3    | Y + scale-degree offset (a fifth)               |
| V4    | Y + scale-degree offset (a third), via arpeggio |

With **contrary motion** (D key), V2/V3/V4 move in the same direction as Y instead of inverting it.

## Build

Built with [64tass](https://tass64.sourceforge.net):

```
64tass --cbm-prg -o mm.prg mm.tass
```
