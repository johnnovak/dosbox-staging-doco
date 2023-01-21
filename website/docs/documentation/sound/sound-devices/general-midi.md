# General MIDI synthesisers

General MIDI isn't a specific piece of hardware so much as a standard that has
been supported by various sound cards (and other devices such as mixers,
instruments, lighting control panels, etc...) throughout computing history.
DOSBox is able to emulate MIDI in either regular or uart modes.

Since MIDI support is still common on computers, DOSBox passes MIDI data along
to any MIDI synthesizer installed on your system rather than trying to emulate
a particular device. General MIDI in DOSBox sounds exactly like any other
program on your host computer that plays MIDI files because it is generating
its output through the same device. You can think of the General MIDI as more
a pass-though interface than a piece of emulated hardware.

General MIDI is configured under the midi category. There are several options,
which are explained briefly in the comments in the configuration file and at
greater length in the README file. Owners of Yamaha MIDI Synthesizers and
other external synthesizers may find this guide useful, while those without
may want to use the guide to software emulation of MIDI instead.


## FluidSynth


## External MIDI devices


