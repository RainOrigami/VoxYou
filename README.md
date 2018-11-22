# VoxYou

Lightweight VST host application for VoiceMeeter with MIDI support.

Use VST effect plugins with VoiceMeeter without having to install a DAW like Canterbile or LiveProfessor. Use your MIDI input device to control your effects and VoiceMeeter at the same time.

## Table of content

- [Installation](#installation)
- [First time setup](#first-time-setup)
- [Usage](#usage)
- [Why](#why)

## Installation

### Prerequisites

- Windows 10
- .NET Framework 4.6.1+
- [virtualMIDI driver](http://www.tobias-erichsen.de/software/virtualmidi.html)
- VoiceMeeter

The virtualMIDI driver is only required if you're using a MIDI device for controlling the VST plugins. It is bundled with [loopMidi](http://www.tobias-erichsen.de/software/loopmidi.html) or [rtpMIDI](http://www.tobias-erichsen.de/software/rtpmidi.html). If you're not sure which one you need, install loopMIDI. Running loopMIDI or starting loopMIDI with Windows is not required.

## First time setup

### VoiceMeeter setup

VoiceMeeter needs to be setup to use patch inserts.  
Go to VoiceMeeter `Menu` -> `System Settings / Options` and enable the patch inserts at the bottom for any channel that you want to apply VST effects on.

![Patch Inserts](https://i.imgur.com/fnyzcPx.png)

If you're using a MIDI device, go to VoiceMeeter `Menu` -> `M.I.D.I. Mapping` and select `- No Midi -` for now to free your MIDI device.

![MIDI Mapping](https://i.imgur.com/8EspBT4.png)

### VoxYou audio setup

When you start VoxYou for the first time you will be prompted to select an ASIO device. Select `VoiceMeeter [Version] Insert Virtual ASIO` and confirm. Make sure to use the correct one that corresponds to the VoiceMeeter version that you are using.

![Select ASIO device](https://i.imgur.com/w3vDD25.png)

Next, setup your inputs, outputs and plugins. To do this, go to `File` -> `Add cable` and use the provided dialog to setup the cable.

![Cable setup](https://i.imgur.com/SLsErLm.png)

In `Input` select the first (eg. left) channel of your input and specify how many channels you're using (mono, stereo, ...). If you're not sure, keep the default value of 2. The corresponding input channels will be listed in the box below.

In `VST Effects` use the `+` button to add all effects you want to use and, if necessary, use the up and down buttons to change their position. Audio is sent to the selected plugins from the top to the bottom.

In `Output` select the first (eg. left) channel of your primary output. If you're not sure, select the same name that you selected for `Input`. The corresponding output channels will be listed in the box on the right.

Click `OK` to add the cable. It will show up in the VoxYou main window.

![A cable is shown](https://i.imgur.com/yOVVDEA.png)

To show and setup your plugins double click their name and the plugin will be displayed.

When you have finished setting up all cables and plugins, click `File` -> `Save` to save these settings.

### VoxYou MIDI setup

If you're not using a MIDI device or don't want to setup any keyboard shortcuts, you can skip this step.

Setup your MIDI triggers for your VST plugins by opening `MIDI Device` -> `MIDI Mapping`.

Check all the MIDI devices that you want to use. Any checked device will receive a virtual MIDI device called `{MidiDeviceName} VoxYou Forward` for use in VoiceMeeter.

![MIDI Mapping](https://i.imgur.com/Gv1EKiy.png)

Press a button or move a slider on your MIDI device or press a key combination on your keyboard. The input will appear in the `MIDI signals` list. Select the input that you want to use.

Select the plugin from the `VST Plugin control` dropdown and select the parameter you want to control from the list below.

Depending on the input signal that you selected you can input a value to set or use toggle to switch between On (1) or Off (0). If you selected a slider or knob it will use its positional value.

Press `Add` to add and enable the trigger. You can bind the same input to multiple plugin parameters.

### VoiceMeeter MIDI setup

If you're not using a MIDI device, you can skip this step.

In VoiceMeeter go to `Menu` -> `M.I.D.I. Mapping` and select the `VoxYou MIDI Forward` input device.

![VoiceMeeter MIDI input](https://i.imgur.com/fljk55G.png)

## Usage

### Cables (Inputs->VST->Outputs)

Cables in VoxYou will route one ASIO input through a selected list of VST plugins to one or multiple ASIO outputs.  
The selected amount of channels will be applied to input and output channels to combine into the same cable.

When selecting multiple output channels, the first output channel in the list is the primary output, any additional output channels will be mirrored to.

The order of VST plugins from top to bottom dictates the order in which the plugins will receive audio data.

### MIDI triggers

`ControlChange` events will apply the value of the control to the plugin parameter in a `0.0` to `1.0` range.

All other events can be assigned to toggle a switch (for example `Bypass plugin` or a switch on the plugin) or set a specific value. Valid values usually range between `0.0` and `1.0`, some plugins may accept larger values (for example to use +125% gain).

The `VoxYou MIDI Forward` device is capable of two-way data traffic and can be used to control the MIDI device from VoiceMeeter (for example to set LED colors on the MIDI device from VoiceMeeters MacroButtons).

If you want to send data to your MIDI controller when a trigger fires, for example to set LED colors, program them in VoiceMeeters MacroButtons, you can assign the same MIDI event in both VoxYou and VoiceMeeter.

### Automatic startup

VoxYou will automatically start with Windows. You can disable this in your Task Manager.

![Don't start with windows](https://i.imgur.com/ODFtnsC.png)

### Saving

To get VoxYou to automatically load whatever you have configured, be it cables, plugins or MIDI triggers, you have to save using `File` -> `Save`, otherwise VoxYou will discard any unsaved changes on the next restart. This way you can reset your changes to the last saved configuration by restarting VoxYou and you can experiment without having to worry about overwriting your current settings.

## Why

When you Google `VoiceMeeter effects` the most recommended way of using any effects with VoiceMeeter is to use Cantabile Lite, a Digital Audio Workstation that contains a ton of features for live performance and doesn't run in the background. It supports playback, instruments and all the snazz you need for your average music session, a lot of stuff that you don't need for just applying a noise filter to you microphone in VoiceMeeter.

![Cantabile Lite](https://i.imgur.com/goiIO8x.png)

*I didn't know that I needed a metronome and a piano to filter noise from my mic to stream on Twitch... Or a metronome. Or tempo. Or instruments. Or...*

The next alternatives are other DAWs like Ableton or LiveProfessor. Programs that are way too bloated and inconvenient to use when you're just streaming games. Usually these DAWs are fine if you're okay with the features in the free versions, or are able to pay $60+ for a full version and running a whole DAW in the background doesn't bother you. Except when you're using a MIDI device, like an AKAI APC Mini, to control your audio environment.

![AKAI APC Mini](https://i.imgur.com/i5QRDMB.jpg)

*It's got more buttons than free keyboard shortcuts and flashing LEDs to tell you you're muted and faders to control your stuff more precisely and generally MacroDeck has got nothing on it!*

VoiceMeeter supports MIDI devices so you can control most VoiceMeeter features from your device and even control your device from VoiceMeeter, for example to light up LEDs to show that you're muted.

The problem arises when you're trying to use your MIDI device in VoiceMeeter and to control parameters of your effects in your DAW. Windows doesn't let you use the same MIDI device in multiple programs at the same time, so you can either control plugins in your DAW, or control VoiceMeeter, but not both at once. Then of course you can install loopMIDI and setup four virtual devices and use MIDI-OX to route the signals, but make sure not to cross the streams or they trigger themselves and...

![MIDI messs](https://i.imgur.com/VB8MOe8.png)

*Send help...*

If you tried to work around all the issues that arise when using MIDI and VST effects with VoiceMeeter you would end up with three additional programs you'd have to keep in your autostart, and one of those usually can not be minimized to the system tray and occupies valuable real-estate in your taskbar and starts maximized with Windows.

For this reason VoxYou was born. It combines the ASIO patching from VoiceMeeter with a super lightweight VST host that does nothing except for running VST effects, and a virtual MIDI device to use your MIDI controller in VoiceMeeter too. And its got a tray icon to stay out of your way.

## Special thanks to

- [un4seen](http://www.un4seen.com/) for a great audio library that does ASIO, VST and MIDI all in one
- [Mathew Sachin](https://github.com/MathewSachin) for the wrapper
- [Tobias Erichsen](http://www.tobias-erichsen.de/software/virtualmidi.html) for an easy to use virtual midi driver
- [vb-audio](https://www.vb-audio.com/Voicemeeter/) for not implementing VST capabilities into VoiceMeeter
