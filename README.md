# Sonic Stick

A mini implementation of some concepts of Laurie Spiegel's [Music Mouse](https://en.wikipedia.org/wiki/Music_Mouse), for C64.

This was primarily a learning exercise (LLM-assisted) to become more familiar with 6502 assembly, the SID chip, and the design of the early versions of Music Mouse. It's a combination of how I thought Music Mouse worked, how it actually worked, and a couple C64 specific things like a filter, chording via arpeggio, a noise voice and a scale derived from Stockhausen's Studie II, in case you don't like music that sounds nice.

Currently uses joystick, which gives no way to detect speed. As such, chords are played sequentially across the grid instead of Music Mouse's intuitive jumps. Koala Pad and 1351 support may be added if I end up getting one.

## Controls

### Joystick (Port 2)

| Input    | Action                              |
|----------|-------------------------------------|
| Stick    | Move cursor through pitch space     |
| Fire     | Hold to mute, release to resume     |

### Keyboard

| Key         | Action                               |
|-------------|--------------------------------------|
| Space       | Toggle sound on/off                  |
| S           | Cycle scale                          |
| W           | Cycle waveform                       |
| < / >       | Octave down / up (all voices)        |
| , / .       | Filter cutoff down / up              |
| F           | Toggle filter                        |
| R           | Toggle envelope retrigger            |
| C           | Toggle contrary motion               |
| F1          | Rhythm: chord (all voices together)  |
| F3          | Rhythm: arpeggiate (rapid cycling)   |
| F5          | Rhythm: line (one voice per beat)    |
| F7          | Rhythm: improvise (random voices)    |
| + / -       | Tempo faster / slower                |

### Scales

Cycled with S: chromatic, major, minor, pentatonic, wholetone, dorian, minor pentatonic, studie ii.

### Waveforms

Cycled with W: triangle, sawtooth, pulse, noise.

### Voices

The screen is a 2D pitch space. Three SID voices plus one fake one are harmonically linked:

| Voice | Pitch source                                    |
|-------|-------------------------------------------------|
| V1    | X position                                      |
| V2    | Y position (inverted: up = higher pitch)        |
| V3    | Y + scale-degree offset (a fifth)               |
| V4    | Y + scale-degree offset (a third), via arpeggio |

With **contrary motion** (C key), V2 reverses its pitch direction while V3/V4 stay normal, causing voices to diverge.

### Rhythmic Treatments

Inspired by Music Mouse's four temporal distributions of a chord:

| Mode       | Key | Behavior                                              |
|------------|-----|-------------------------------------------------------|
| Chord      | F1  | All voices sound simultaneously (default)             |
| Arpeggiate | F3  | Voices cycle one at a time, tempo subdivided by 3     |
| Line       | F5  | One voice per full beat at current tempo              |
| Improvise  | F7  | Random subsets of voices on each beat                 |

Tempo is adjustable with `+` (faster) and `-` (slower). The current mode is shown at the top-right corner of the screen (CHR/ARP/LIN/IMP).

## Build

Built with [64tass](https://tass64.sourceforge.net):

```
64tass --cbm-prg -o sstick.prg sstick.tass
```
