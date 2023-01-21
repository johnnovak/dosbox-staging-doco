# Roland MIDI synthesisers

The Roland synthesizers, particularly the MT-32, are worth mentioning
separately. Many DOS games included separate support for the MT-32 (or the
MT-100, LAPC-I, CM-32L, or CM-64) in addition to basic General MIDI support.
People who have a real Roland MT-32 or a software synthesizer that emulates
one can take advantage of this support. Since DOSBox only passes along MIDI
data to your synthesizer without looking at it, simply route DOSBox's General
MIDI to your Roland and configure your DOS software to use Roland mode.

A Roland MT-32 can be connected to the PC using a USB to MIDI adapter. The
MT-32 output can be connected to the line-in on a sound card. Dosbox can be
configured to use the MT-32 for music when it is connected this way. At the
Dosbox command prompt, type mixer /listmidi to get a list of the midi devices
attached to the machine. Locate the USB midi adapter in the list and note the
number that it is associated with. Change Dosbox.conf's midiconfig = id of
MIDI device to the ID of the USB midi device (e.g. midiconfig=0) Once that is
done, the MT-32 should operate.


