# Sound overview

DOSBox is capable of emulating several sound devices. By emulating the
hardware the user can utilize whatever audio device they have installed in
their PC, while the DOS Game or Application believes it is running on the
emulated hardware.

Sound was sometimes difficult to set up in the DOS era. Unlike Windows, DOS
did not keep a list of the system's sound devices, nor did it expose generic
drivers for them. Software had to include separate support for each sound
device it wanted to give the users the option of using. If a game did not
support a user's audio hardware, no sound was possible. And the game had to be
configured with the memory addresses of the hardware by hand. Also, different
devices supported different features, resulting in games that could sound very
different (maybe high-quality music on one card, but voice-acting on another)
depending on the hardware available. Thankfully, DOSBox can emulate all the
most popular sound systems of the DOS era, so one can usually find something
that sounds good.

Most of the sound devices are capable of existing inside the same computer at
the same time, so when configuring DOSBox sound you need to think of them as
separate devices that can be enabled or disabled. Sound devices that are not
in use do not use many resources, so you don't gain much in the way of
performance by reducing the number of sound devices enabled. A game will
likely only use a single device at a time anyway. (The one notable exception
being routing music and sound effects through different devices, which was
common for people with both a Sound Blaster and a separate MIDI device.)
DOSBox also makes sure the appropriate environment variables are defined for
each device, so game audio device auto-detection usually works, if the game
attempts it.

DOSBox's output to your real computer's sound system is configured under the
mixer category. Each emulatable device has its own configuration section. Note
that almost all sound devices have a configuration setting to enable or
disable them, as well as one for the sample rate of the emulation. The sample
rate of a device must never exceed the rate setting under the mixer heading,
as this will cause undefined behavior.

DOSBox can emulate the following devices. Although the sound quality you will
get depends heavily on your configuration and what the software you are
running supports, they are listed here in roughly ascending order of audio
processing power.
