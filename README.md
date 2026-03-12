# Manic Mouse

A mini implementation of Laurie Spiegel's [Music Mouse](https: //en.wikipedia.org/wiki/Music_Mouse) for C64. Primarily a learning exercise (largely LLM-assisted) for myself to become more familiar with 6502 assembly and the SID chip.

Notes:

* Limited to 3 voices, but may add dual SID support for the C64U.
* Currently uses joystick, which gives no way to detect speed. As such, chords are played sequentially across the grid instead of Music Mouse's intuitive jumps. Koala Pad and 1351 support may be added.

## Build

Built with [64tass](https://tass64.sourceforge.net):

```
64tass --cbm-prg -o mm.prg mm_annotated.tass
```
