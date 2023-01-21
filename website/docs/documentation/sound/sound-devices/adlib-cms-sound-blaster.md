# AdLib, CM/S & Sound Blaster

## Overview

For many who owned a gaming PC in the 1990s, the name **Sound Blaster** is a
synonym for "sound card"---and rightly so, as the Sound Blaster family of
cards by Creative Technology was the de facto standard for DOS gaming. The
first Sound Blaster was released in 1989, and it quickly became the
best-selling expansion card for the PC. Virtually all games from 1990 onwards
had Sound Blaster support in some shape or form, and this remained unchanged
for the rest of the DOS-era until the late 90s.

DOSBox can emulate all major revisions of the Sound Blaster family. One of the
most common models was the [Sound Blaster 16](#sound-blaster-16) which has
good (but not perfect) backwards-compatibility with earlier cards. This is the
sound card DOSBox emulates by default to ensure the widest possible
compatibility with games,

Most games that support the AdLib or Sound Blaster work fine with the DOSBox
defaults, and don't require you to load any DOS drivers. A small percentage of
games, however---especially from the early Sound Blaster days---only work with
a specific model, or require a driver to be loaded. Please refer to the [List
of games that require a sound driver](#){ external } on the wiki for more
details.


### On-board synthesisers

In addition to their digital sound playback capabilities (also referred to as
**PCM sound**), all Sound Blaster models feature at least one on-board
synthesiser for the generation of music and sound effects. The most important
of these is the [AdLib](#adlib-music-synthesizer-card) that is present on all
Sound Blaster cards. The AdLib is also referred to as **OPL sound** (after the
Yamaha OPL range of chips responsible for the "AdLib sound"), or **FM sound**
(after the OPL chip's FM sound synthesis capabilities). DOSBox uses the highly
accurate NukedOPL library to achieve a nearly bit-perfect emulation of the OPL
chips.

The other less common synthesiser is the [Creative Music
System](#creative-music-system-cms) (also referred to as **CM/S**, or
**CMS**) which is only present on the earliest Sound Blaster models.

Because the history and even the emulation of these synthesisers are so
closely entwined with those of the Sound Blaster, we are going to discuss them
together.


### Emulated Sound Blaster models

The below table lists all Sound Blaster models emulated by DOSBox, along with
their main capabilities:

| Model | `sbtype` | Digital sound | Synthesiser |
| ----- | -------- | ------------- | ----------- |
| [Game Blaster](#creative-music-system-cms-game-blaster) | `gb` | N/A | CMS (stereo)
| [Sound Blaster 1.0](#sound-blaster-10) | `sb1` | 8-bit mono 22kHz | OPL2 (mono)<br>CMS (stereo)
| [Sound Blaster 2.0](#sound-blaster-20) | `sb2` | 8-bit mono 22kHz | OPL2 (mono)<br>CMS (stereo, optional)
| [Sound Blaster Pro](#sound-blaster-pro) | `sbpro1` | 8-bit mono 44kHz<br>8-bit stereo 22kHz | Dual OPL2 (stereo)
| [Sound&nbsp;Blaster&nbsp;Pro&nbsp;2.0](#sound-blaster-pro-20) | `sbpro2` | 8-bit stereo 44.1kHz | OPL3 (stereo)
| [Sound Blaster 16](#sound-blaster-16) | `sb16` | 16-bit stereo 44kHz | OPL3 (stereo)


### Mixer channels

The digital sound of the Sound Blaster is output to the **`SB`** mixer channel,
while the AdLib (OPL) synthesiser has its own dedicated **`OPL`** channel. Both
channels can be either mono or stereo, depending on the particular Sound
Blaster model being emulated.

The Creative Music System synthesiser has its own dedicated **`CMS`** channel,
which is always stereo.

The upshot of this is that the digital sound and synthesiser volumes can be
adjusted independently via the DOSBox mixer (e.g. in games that use
digital sound for speech and sound effects, and the synthesiser for music).

!!! note

    Starting with the Sound Blaster Pro, programs can adjust the volume of the
    digital sound, OPL, and CD Audio channels via the Sound Blaster software
    mixer. By default, DOSBox forwards these adjustments to the DOSBox mixer,
    allowing programs to change the volumes of these channels. This can
    potentially result in your manually set volumes being overridden. To
    prevent this from happening, set the [`sbmixer`](#sbmixer) configuration
    setting to `off`.


### Default settings

The default Sound Blaster settings shown below have been selected for the
widest possible compatibility with games. Most games can auto-detect the
presence of a Sound Blaster card and these settings, but in case they need a
little help, here are the values to use:

<div class="compact" markdown>

| Setting                                | Config setting    | Default value |
| -------------------------------------- | ----------------- | ------------- |
| Base address (or I/O address, or port) | [sbbase](#sbbase) | 220
| IRQ (or interrupt)                     | [irq](#irq)       | 7
| DMA (or low DMA)                       | [dma](#dma)       | 1
| High DMA (or HDMA)                     | [hdma](#hdma)     | 5

</div>

If you have configured a game for Sound Blaster speech and music but can't
hear both or maybe there is no sound at all, or if the game hangs or crashes,
first double check that the above settings have been set in the game's
configuration. Many games don't let you to set all of them manually and just
assume some common fixed values instead. Please refer to the detailed
description of the config settings for troubleshooting tips.


### Selecting the best Sound Blaster model for a game

The default lowest common denominator settings will serve you well if you just
want to play some games with minimum hassle. In that case, you might as well
stop reading this chapter now, and only come back to it if you've encountered
issues with certain titles, or if you want to further your understanding of
the subtler differences between the various Sound Blaster models.

For the ones who are still with us (or who have come back to learn more!),
here's the thing: if you want to coax the best sound out of a particular game,
often you'll need to select a specific Sound Blaster model the game was primarily
developed for. The reason for this lies in Creative's own failure to provide
accurate backwards compatibility with their earlier cards.



Stereo bug
:   Games with stereo digital sound written for the Sound Blaster Pro 1.0 or
    2.0 output mono sound only in the backwards-compatibility mode of the Sound
    Blaster 16.

Different analog low-pass output filters
:   Sound Blaster cards before the Sound Blaster 16 have a fixed frequency
    low-pass filter on the output to reduce the effects of aliasing which sounds
    like metallic overtones when playing digital audio at low sample rates.

    This fixed filter was changed to a variable-frequency design on the Sound
    Blaster 16, and the character of the filter was also altered. The old
    filter let a good amount of the metallic overtones through, resulting in a
    characteristic gritty, crunchy sound, while the new variable brick-wall
    filter was much more effective at reducing these overtones.

    The result is that low sample rate digital audio typical to earlier DOS games
    sounds overly muffled on the Sound Blaster 16 compared to earlier models.

Dual OPL2 support
:   The Sound Blaster Pro 1.0 is capable of stereo **Dual OPL2** operation
    thanks to its two on-board OPL2 chips. This is the only Sound Blaster
    model with a dual OPL2 configuration. Previous models feature a single
    OPL2 chip, capable of mono operation only, and while later
    cards have the improved OPL3 which *can* output stereo sound, programs written
    for dual OPL2 won't work produce stereo sound on OPL3, and vice versa.




To provide a good out-of-the-box experience that works well enough with most
games without tinkering, DOSBox defaults to the imaginary `modern` [filter
setting](#sb_filter) on all Sound Blaster models. This implements simple
linear-interpolation instead of accurately emulating the analog output
filter---this makes most games sound decent regardless of the Sound Blaster
model in use, but it's not authentic.

For the best authentic results, you need to set the most appropriate Sound
Blaster model for each game via the [sb_type](#sb-type) configuration
setting. Additionally, you need to set the [sb_filter](#sb_filter) setting to `auto`
to let DOSBox select the output filter appropriate to the emulated model.

For example, use the following settings to enable authentic Sound Blaster Pro
1.0 emulation with Dual OPL2 support, suitable for games from the early 90s:

``` ini
[sblaster]
sbtype = sbpro1
sb_filter = auto
```

Determining the best Sound Blaster model for a game can be tricky as the
different cards were released close to each other, so simply looking at the
game's release date often doesn't help much. In some cases both the Sound
Blaster 16 and earlier models can be selected in the game's configuration, yet
the Sound Blaster 16 is not the best option. Ultimately, you'll need to do a
little bit of research, experiment, and trust your ears.


---

## AdLib Music Synthesizer Card

The **AdLib Music Synthesizer Card** (typically simply referred to as
**AdLib**) was released by Ad Lib in 1987. It was the first popular sound card
for IBM PC compatibles, capable of producing multitimbral FM music and sound
effects via its Yamaha OPL2 synthesizer chip. Digital audio is not supported
on the card.

Being such a huge step up from the PC speaker, the AdLib was an instant
success. As it quickly became a de facto standard, many competing sound card
manufacturers started including full AdLib compatibility on their cards. The
result of this is that virtually all DOS games from 1988 onwards support the
AdLib, at least as a fallback option.

Use the following settings to enable AdLib (OPL2) emulation:

``` ini
[sblaster]
sbtype = none
oplmode = opl2
```

It was still possible, however, to output PCM sound with software by
modulating the playback volume at an audio rate, as was done, for example, in
the MicroProse game F-15 Strike Eagle II[5] and the multi-channel music editor
Sound Club for MS-DOS.[6]

!!! note

    When [oplmode](#oplmode) is set to `opl2`, C/MS emulation is always
    enabled as well. This is a historical shortcoming of DOSBox and will be
    addressed in a future version.


## Creative Music System (C/MS) / Game Blaster

Originally named the Creative Music System (CMS), but the year after rebranded as the Game Blaster.

The Creative Music System was Creatives first sound card released in 1987, and were later rebranded as Game Blaster.

The **Creative Music System** (also referred to as **C/MS** or **CMS**) was
released in August 1987 by Creative Technology. The card featured two Philips
SAA-1099 chips, allowing multitimbral stereo sound via FM synthesis. It
sounded like a much simpler variant of the AdLib card and it did not sell that
well.

Use the following settings to enable Game Blaster emulation:

``` ini
[sblaster]
sbtype = gb
```


## Sound Blaster 1.0

The original **Sound Blaster 1.0** was released by Creative Technology in 1989
as the successor of their Game Blaster card. It was the first sound card on
the market to have digital sample playback capability; it could play back
1-channel 8-bit digital audio at up to 22kHz sample rate. It was also 100%
C/MS and AdLib (Yamaha OPL2) compatible, making the card live up to its
"Killer Kard" code name. In less than a year, the Sound Blaster became the
best-selling expansion card for the PC.

This transformed DOS gaming, as sampled sound effects could be used while simultaneously playing music via the OPL2 or CMS synthesiser chips.

Use the following settings to enable Sound Blaster 1.0 emulation:

``` ini
[sblaster]
sbtype = sb1
```

Only uses DMA 1 and IRQ 7

## Sound Blaster 2.0

The **Sound Blaster 2.0** was released by Creative Technology in October 1991.
Similarly to Sound Blaster 1.0, it can play back 1-channel 8-bit digital
audio, but the maximum sample rate is increased to 44.1 kHz.

The card retains the perfect AdLib (OPL2) compatibility, but C/MS support was
optional.

Some early games specifically written for Sound Blaster 1.0 have problems with
this or later cards.

Use the following settings to enable Sound Blaster 2.0 emulation:

``` ini
[sblaster]
sbtype = sb2
```

Only uses DMA 1 and IRQ 7


## Sound Blaster Pro

The **Sound Blaster Pro** (or **Sound Blaster Pro 1.0**) was released by
Creative Technology in May 1991. It is backward-compatible with the earlier
models, but it can also output stereo digital audio up to 22 kHz sample rates,
and it features a pair of Yamaha OPL2 chips instead of just one for stereo FM
sound.

This is the only card supported by the known OEM releases of Microsoft Windows
3.0a with Multimedia Extensions.

Use the following settings to enable Sound Blaster Pro emulation:

``` ini
[sblaster]
sbtype = sbpro1
```

!!! important

    Software specifically written for the dual OPL2 chips of the Sound Blaster
    Pro 1.0 will not produce stereo audio on any other Sound Blaster models
    (including the Sound Blaster Pro 2.0). Therefore, it is important to set
    the correct Sound Blaster model for such software by specifying `sbtype =
    sbpro1` in the configuration.



## Sound Blaster Pro 2.0

The **Sound Blaster Pro 2.0** was released by Creative Technology in 1991,
quickly replacing its predecessor, the Sound Blaster Pro.

It is functionally the same as the earlier Sound Blaster Pro with one key difference:
instead of the dual OPL2 chips, it uses a single Yamaha OPL3 chip for stereo
FM sound.

Use the following settings to enable Sound Blaster Pro 2.0 emulation:

``` ini
[sblaster]
sbtype = sbpro2
```

!!! important

    Software specifically written for the dual OPL2 chips of the Sound Blaster
    Pro 1.0 will not produce stereo audio on the Sound Blaster Pro 2.0, but
    will revert to the default mono OPL2 compatibility mode of the OPL3 chip.
    Therefore, it is important to set the correct Sound Blaster model for such
    software by specifying `sbtype = sbpro1` in the configuration.

    Likewise, software targeting the OPL3 specifically will only work
    correctly on Sound Blaster Pro 2.0 and later models that feature the
    OPL3 chip.


## Sound Blaster 16

The **Sound Blaster 16** was released by Creative Technology in June 1992.
This is the first Sound Blaster card to support CD-quality sound (stereo
16-bit digital audio at 44.1 kHz sample rate). The card features the Yahama
OPL3 chip that has perfect backward-compatibility with OPL2, and supports
stereo operation in a single chip.

The Sound Blaster 16 has less than perfect compatiblity with earlier models.
Due to a design flaw, Sound Blaster Pro compatibility mode works in mono only,
and the analog output filter behaviour of previous models is not replicated,
making earlier games sound different and subjectively wrong to many.

In its early stages, Sound Blaster 16 retained the Yamaha OPL3 chip for FM
music synthesis, so was still backward-compatible with the original Sound
Blaster.

Some key features of the SB 16

- "noisy" audio

Sound Blaster 16 emulation is enabled by default, and can be enabled by
setting sbtype=sb16 in the [sblaster] section of the DOSBox-X config file.

Use the following settings to enable Sound Blaster 16 emulation:

``` ini
[sblaster]
sbtype = sb16
```


## AdLib Gold 1000

The **AdLib Gold 1000** was released in 1992. It is backward compatible with
the earlier AdLib Music Synthesizer Card, but not with the Sound Blaster
cards.

Use the following settings to enable AdLib Gold 1000 emulation, including the
surround module add-on:

``` ini
[sblaster]
oplmode = opl3gold
```


## Configuration settings

All Creative Music System, Sound Blaster and AdLib related settings are to be
configured in the `[sblaster]` section.

### Sound Blaster

##### sbtype

:   Sound Blaster model to emulate.

    Possible values:

    <div class="compact" markdown>

    - `none` -- Disable Sound Blaster emulation.
    - `gb` -- [Creative Music System (C/MS) Game Blaster](#creative-music-system-cms-game-blaster)
    - `sb1` -- [Sound Blaster 1.0](#sound-blaster-10)
    - `sb2` -- [Sound Blaster 2.0](#sound-blaster-20)
    - `sbpro1` -- [Sound Blaster Pro](#sound-blaster-pro)
    - `sbpro2` -- [Sound Blaster Pro 2.0](#sound-blaster-pro-20)
    - `sbpro16` *default*{ .default } -- [Sound Blaster 16](#sound-blaster-16)

    </div>

    Please refer to the [Emulated Sound Blaster
    models](#emulated-sound-blaster-models) section for an overview of the
    capabilities of the different models.


##### sbbase

:   The base address (also referred to as I/O address, or port) of the Game
    Blaster / Sound Blaster.

    Possible values: `220` *default*{ .default }, `240`, `260`, `280`, `2a0`, `2c0`, `2e0`, `300`.

    You can typically only choose between `220`, `240` and `260` on real cards.

    !!! important

        Virtually all games with Game Blaster / Creative Music System (CM/S)
        support only work with the base address set to `220`. A significant
        number of early 90s games with Sound Blaster support also assume a
        base address of `220` and do not let the user the change it, making
        this the most compatible setting.


##### irq

:   The IRQ (interrupt) number of the Game Blaster / Sound Blaster.

    Possible values: `3`, `5`, `7` *default*{ .default }, `9`, `10`, `11`, `12`.

    You can typically only choose between `5` and `7` on real cards.

    !!! important

        Cards up until the Sound Blaster Pro 1.0 defaulted to IRQ 7. From
        the Sound Blaster Pro 2.0 onwards, the default had been changed to
        IRQ 5. Some earlier games assume IRQ 7 and do not let the user to change
        it. Games assuming IRQ 5 is less of a problem, making `7` the overall
        most compatible setting.


##### dma

:   The DMA (also referred to as low DMA) channel used for 8-bit
    transfers of the Sound Blaster.

    Possible values: `0`, `1` *default*{ .default }, `3`, `5`, `6`, `7`.

    You can typically only choose between `0`, `1` and `3` on real cards.

    !!! important

        Many earlier games assume DMA 1 and do not let the user to change
        it, making it the most compatible setting.


##### hdma

:   The high DMA channel used for 16-bit transfers of the Sound Blaster.

    Possible values: `0`, `1`, `3`, `5` *default*{ .default }, `6`, `7`.

    You can typically only choose between `5` and `7` on real cards.

    High DMA is only used on the Sound Blaster 16 for 16-bit digital audio.


##### sbmixer

:   Allow the Sound Blaster mixer to modify the DOSBox mixer.

    Possible values: `on`, `off` *default*{ .default }

    Starting with the Sound Blaster Pro, programs can adjust the volume of the
    digital sound, OPL, and CD Audio channels via the Sound Blaster software
    mixer. By default, DOSBox forwards these adjustments to the DOSBox mixer
    which can potentially result in your manually set volumes being
    overridden. To prevent this from happening, set the [`sbmixer`](#sbmixer)
    configuration setting to `off` to retain full manual control over the
    mixer channels.


##### sbwarmup

:   Silence initial DMA audio after card power-on, in milliseconds.

    Default value: `100`

    This mitigates pops heard when starting many Sound Blaster based games.
    Reduce this if you notice intial playback is missing audio.


##### sb_filter

:   Type of filter to emulate for the Sound Blaster digital sound output:

    - `auto` -- Use the appropriate filter determined by [sbtype](#sbtype).
    - `sb1`, `sb2`, `sbpro1`, `sbpro2`, `sb16` -- Use the filter of this Sound Blaster model.
    - `modern` *default*{ .default } -- Use linear interpolation upsampling that acts as a low-pass filter; this is the legacy DOSBox behaviour.
    - `off` -- Don't filter the output.
    - `<custom>` -- Specify a custom filter; see [Custom filter settings](../analog-output-filter/#custom-filter-settings) for details.


##### sb_filter_always_on

:   Force the Sound Blaster filter to be always on (disallow programs from
    turning the filter off).

    Possible values: `on`, `off` *default*{ .default }


### OPL

##### oplmode

:   OPL mode to emulate.

    Possible values:

      - `none` -- Disable OPL emulation.

      - `auto` *default*{ .default } -- Automaticaly select the appropriate OPL
        mode for the emulated Sound Blaster card, based on the value of the
        [sbtype](#sbtype) setting (see [Emulated Sound Blaster
        models](#emulated-sound-blaster-models) for an overview).

      - `cms` -- Two Philips SAA1099 chips as used in the Creative Music
        System / Game Blaster (not OPL compatible).

      - `opl2` -- Yamaha YM3812 (OPL2) as found on the original AdLib Music
        Synthesiser and early Sound Blaster cards.

      - `dualopl2` -- Two Yamaha OPL2 chips in a stereo configuration as
         found on the Sound Blaster Pro 1.0.

      - `opl3` -- Yamaha YMF262 (OPL3) as found on the Sound Blaster Pro 2.0
        and later cards.

      - `opl3gold` -- Yamaha OPL3 as found on the AdLib Gold. Also enables the
        emulation of the on-board Philips TDA8425 Hi-fi Stereo Audio
        Processor and the Yamaha YM7128 Surround Processor found on the
        optional surround module.

    !!! note

        When `oplmode` is set to `opl2`, C/MS emulation is always enabled as
        well. Likewise, C/MS emulation should have its own config setting as
        it has nothing to do with OPL. Both issues are historical shortcoming
        of the original DOSBox and will be addressed in a future version of
        DOSBox Staging.


##### opl_filter

:   Type of filter to emulate for the Sound Blaster OPL output:

    - `auto` *default*{ .default } -- Use the appropriate filter determined by [sbtype](#sbtype).
    - `sb1`, `sb2`, `sbpro1`, `sbpro2`, `sb16` -- Use the filter of this Sound Blaster model.
    - `off` -- Don't filter the output.
    - `<custom>` -- Custom filter definition; see [sb_filter](#sb_filter) for details.


### CMS

##### cms_filter

:   Filter for the Sound Blaster CMS output:

    - `on` *default*{ .default } -- Filter the output.
    - `off` -- Don't filter the output.
    - `<custom>` -- Custom filter definition; see `sb_filter` for details.

