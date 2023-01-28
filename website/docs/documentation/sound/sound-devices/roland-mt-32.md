# Roland MT-32

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



!!! note

    Roland MT-32 support might be referred to as **Roland MT-100**, **LAPC-I**
    (sometimes mispelled as **LAPC-1**), **CM-32L**, or **CM-64** in the
    game's setup program. All these refer to the same thing; you only need to
    research which ROM version is recommended for the game and set it
    accordingly.

    Some games offer a **Roland MT-32 with Sound Blaster** option which should
    be generally preferred to the plain Roland MT-32 option as it might enable 
    additional digital music to be played on the Sound Blaster.


With the arrival of the Roland MT-32 in 1987 you would have needed to drop almost $700 USD to get one. Since this was out of reach for most of us, we instead purchased a much cheaper sound card or in the early days we just put up with the PC speaker! 

Its intended audience was for amateur musicians rather than computer users. The MT-32 came with a built-in library of 128 synth and 30 rhythm sounds, playable on 8 melody channels and 1 rhythm channel, plus it had a digital reverb effect.

 It actually could produce much better sounds than the stock library if you used a computer-based editor to create and upload your own sound samples. The better game soundtracks did just that, and used the full capability of the MT-32 to produce very realistic custom instruments and sound effects not found in its default samples.


It was common for PC games released from 1988 to 1992 to support the Roland MT-32. During this era, the MT-32 was followed by the MT-100 which was an MT-32 'new' combined with a Roland PR-100 sequencer. A little later, Roland introduced their "Computer Music" series: the CM-32L and CM-64, both released in 1989.



Roland also produced the LAPC-I, often incorrectly labelled LAPC-1, which was an entire CM-32L and MPU-401 interface on a single ISA expansion card - these are very rare and hence expensive to buy. 



Earlier DOS games that provide a Roland MT-32 sound option frequently use Normal mode during initialisation, or when communicating with the card. Most later games including those that support General MIDI typically only use the more basic UART mode. This mode is much simpler to implement, so almost all hardware that claims to be MPU-401 compatible will have this mode as standard. The Sound Blaster 16 and up only support MPU-401 UART mode, making them unsuitable as a reliable interface for older DOS games with MT-32 support. The older Sound Blasters do not support MPU-401 at all (the game port's pinouts are not MPU-401 compatible). 



Was the MT line worth the money? In many respects yes. Based on Linear Arithmatic synthesis, the MT-32 combined partial, 16-bit samples of actual instruments with subtractive synthesis techniques that could fill-in for the unsampled parts of the tone. This was quite a clever combination, as the use of real samples allowed the sound patches on the MT-32 to sound much more realistic than those produced by via FM, while the synthesiser functions meant that composers were free to manipulate the stock samples in order to create custom sounds. It may perhaps have been slightly weaker than the FM-based competition when it came to delivering purely weird and synthetic tones, but at the time it was absolutely unparalleled when it came to emulating acoustic instruments. In 1987 the MT-32 was the closest a PC game composer could get to creating a CD quality soundtrack.


History of MT-32 and inseparablySierra intertwined

Despite its original purpose as a companion to other professional MIDI equipment, the MT-32 became one of several de facto standards for PC computer game publishers. Sierra On-Line, a leading PC game publisher of the time, took an interest in the sound-design of its PC games. Sierra secured a distribution deal to sell the MT-32 in the US, and invested heavily in giving its game titles (at the time) state-of-the-art sound by hiring professional composers to write in-game music. King's Quest IV, released in 1988, was the first Sierra title with a complete musical soundtrack scored on the MT-32.

For a time, it was described as providing "the most realistic sound available in computer gaming today".[12]



DOSBox supports the MPU-401 (MIDI Processing Unit) interface created in 1984 by the Japanese audio company Roland to enable customers to connect MIDI-compatible devices to their home computers. Initially, this interface support was through standalone cards, but partial support was later incorporated into many third-party sound and joystick add-on cards.

The Roland MT-32 Multi-Timbre Sound Module from 1987 was a programmable synthesiser that supported up to 32 notes played at once using a 16-bit DAC at a sample rate of 32000 HZ. This standalone device required an MPU-401 interface installed on the host machine to connect to and use on a PC.


Also, in 1989 Roland released the first of a series of CM (Computer Module) sound modules. Some of which improved but were also mostly compatible with the MT32 module. Models included the CM-32L, an improved MT-32 with 33 added sound-effect samples. And the CM-64 was a more expensive model of the CM32L with extra functionality geared toward computer musicians.

To complicate things, MPU-401 has two modes, ‘intelligent’ and ‘UART,’ otherwise called dumb mode. Many ‘MPU-401 compatible’ cards and devices only support UART mode. In UART mode, the attached MPU-401 component acts as a dumb playback device.

While the intelligent mode, the attached device handles part of the audio processing. This more complex mode allows computers with the slowest generation of Intel PC CPUs (such as the 8086 and 8088) to handle MIDI playback. But intelligent mode had become redundant when support for these CPUs was abandoned in favour of faster chips that could handle the audio processing.





Part of the Munt project, mt32emu is a multi-platform software synthesizer emulating Roland's MT-32, CM-32L, CM-64 and LAPC-I modules. It is not endorsed by or affiliated with the Roland Corporation.

DOSBox Staging now comes with mt32emu built-in by default. Yet to use that synthesizer, you will have to provide a set of valid ROM files dumped from the hardware. The mt32emu configuration section below will help you with the details.




Tip: using the layering approach of DOSBox configuration files, you can pick one specific MT-32 model per game.






[mt32emu] support for DOSBox Staging is now built-in by default and can be configured by editing your [`dosbox-staging.conf`] file (or any local `.conf` you may have) as follows:

``` ini
[midi]
mididevice = mt32

[mt32]
model  = auto
romdir = /path/to/mt32-roms
```

**Tip**: using the layering approach of DOSBox [configuration files], you can pick one specific MT-32 model per game.


## Roland ROM images

The Roland MT-32 and CM-32L ROM images are copyrighted by Roland Corporation
and *are not distributable*. The ROMs contain PCM samples and are required to
get any sound out of the MT-32 device selected.

These ROMs can be stored anywhere as long as the `romdir =` parameter is
pointing to the correct location. The directory can be absolute or relative,
or you may leave it blank to use the `mt32-roms` directory in your DOSBox
Staging [configuration directory]. 

DOSBox Staging supports the loading of both _versioned_ and _unversioned_ ROMs
(more details below) for the CM-32L, LAPC-I, MT-32 "new", and MT-32 "old"
models. Depending on which ROMs are available, DOSBox Staging's default
setting (`model = auto`) will attempt to load ROMs for **CM-32L** first, then
**MT-32 "old"**, and finally **MT-32 "new"**. 

Although the vast majority of games are best served by the CM-32L model, there
are many games that rely on the older MT-32 models (eg. Dune 2). Feel free to
refer to the table listing the [MT-32-compatible games] as well as the list on
[Wikipedia](https://en.wikipedia.org/wiki/List_of_MT-32-compatible_computer_games)
to know which model works best.


### Unversioned ROMs

Unversioned ROMs must be named as follows:

<div class="compact" markdown>

- `CM32L_CONTROL.ROM`
- `CM32L_PCM.ROM`
- `MT32_CONTROL.ROM`
- `MT32_PCM.ROM`

</div>

### Versioned ROMs

Versioned ROMs are part of the MAME video game preservation project. Learn
more by searching for _"mt32 mame roms"_ and _"cm32l mame roms"_. These ROM
sets support the following models:

<div class="compact" markdown>

| Model               | `model` value            | Control ROM filename                               |
| ------------------- | ------------------------ | -------------------------------------------------- |
| CM-32L/LAPC-I v1.02 | `cm32l_102`              | `cm32l_control.rom`                                |
| CM-32L/LAPC-I  1.00 | `cm32l_100`              | `lapc-i.v1.0.0.ic3.bin`                            |
| MT-32 v2.04 ("new") | `mt32_204` or `mt32_new` | `mt32_2.0.4.ic28.bin`                              |
| MT-32 v1.07 ("old") | `mt32_107` or `mt32_old` | `mt32_1.0.7.ic26.bin`<br>`mt32_1.0.7.ic27.bin`     |
| MT-32 v1.06         | `mt32_106`               | `mt32_1.0.6.ic26.bin`<br>`mt32_1.0.6.ic27.bin`     |
| MT-32 v1.05         | `mt32_105`               | `mt32_1.0.5.ic26.bin`<br>`mt32_1.0.5.ic27.bin`     |
| MT-32 v1.04         | `mt32_104`               | `mt32_1.0.4.ic26.bin`<br>`mt32_1.0.4.ic27.bin`     |
| MT-32 BlueRidge     | `mt32_bluer`             | `blue_ridge__mt32a.bin`<br>`blue_ridge__mt32b.bin` |

| Model                 | PCM ROM filename                                                     |
| --------------------- | -------------------------------------------------------------------- |
| MT-32 (all versions)  | `r15449121.ic37.bin`<br>`r15179844.ic21.bin`<br>`r15179845.ic22.bin` |
| CM-32L (all versions) | `r15179945.ic8.bin`                                                  |

</div>


### Listing the installed ROMs

In DOSBox Staging you'll be able to run the command `MIXER /LISTMIDI` to check
which ROMs are being detected and currently used. This should translate into:

<p align="center">
  <img src="https://user-images.githubusercontent.com/1557255/113753268-c0f47480-96c2-11eb-892e-b3107e475bb4.png">
</p>

In the screen above, `mt32_107` is the user's selected model. The green
highlighted **'y'** additionally indicates which directory will be used during
the actual loading.

Note that *both* the control and PCM ROMs need to be present for a given
model. If some model could not be detected, or you're getting `Failed to find
ROMs for model <model_name>` error at startup, make sure that both ROM sets
have been copied to your ROM directory for that model.

