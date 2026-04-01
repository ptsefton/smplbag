# Smplbag

A browser-based "**non-looping looper**" which is one-shot sampler songwriting and live performance.

This tool is designed to be driven primarily by an external MIDI sequencer (for example a Dirtywave M8), while still being playable from the web UI or a keyboard controller.

The name comes from "Sample Bag", but if you read that as "simple" that's OK, that's a design goal. 

(A sample bag AKA Show Bag, in Australian English was a thing you used to get at an agricultural show (you know, like a fair). When we went to the Royal Easter Show in Sydney, every time my would tell me they used to be free, and contain, you know *samples* but I didn't really believe him. When I was a kid you had to *buy* them and you still do - they were typically full of some kind of food like licorice or chocolate or bread with some kind of toy or something but now they sometimes contain just toys. Anyway this smplbag's free!)

## What it is

This is not a traditional loop station with overdub layers, though it has plenty of tracks to put down multiple layers that are independent of each other.

It is a **16-pad, one-shot clip recorder/player** where each pad can:
- arm/disarm,
- record from a selected audio input,
- stop recording on note release (or on a new note event),
- replay captured audio from the start,
- route playback to a chosen hardware output channel.

The workflow is meant for **fast song-structure capture**: verse, chorus, bridge, transitions, etc using a sequencer to lay out the structure that you can then play in to.

## Core idea

Use sequenced MIDI notes as section triggers.

Example:
- `C1` (MIDI note 0) held for 16 bars records Pad 1 (bottom-left) if armed.
- `C#1` (MIDI 1) can target the next section (for example chorus).
- `D1` (MIDI 2) can target bridge.

You can pre-program a structure in your sequencer, then capture and trigger parts in performance with minimal manual interaction. 

On the M8 - the plan is then get the 


## Features

- 4×4 pad grid (16 pads*) 
- Fixed note mapping* starting at MIDI 0 (`C1` display convention)
- Per-pad arm toggle
- Per-pad output channel selection
- MIDI channel filtering (or all channels)
- MIDI monitor in UI
- Adjustable trigger offset if you have latency issues (ms)
- Input device selection and refresh
- Stop / clear controls per pad
- Output channel test tone tool to help work out where stuff is going in your USB interface. (Eg in the Tascam Model 12 in 10*12 mode tracks 1&2 go to 9&10 and 3-8 go to tho 3-8)

* Current 4x4 layout and midi mapping might made configurable

## TODO (maybe)

- Customize number of clips
- Customize midi behaviour
- Resampling features like play all (populated) clips so they can be sampled and sliced
- Allow for different takes on a note/sample that can be switched in the UI or via midi CC
- Export a zip 
- Save clips to browser storage
- Import?


## MIDI behavior (current)

For a pad’s trigger note:
- **Note ON**
  - If pad empty and armed: start recording
  - If already recording: stop recording, then play captured clip
  - If clip exists: play/retrigger from start
- **Note OFF**
  - If recording: stop recording

Arm toggling can be done from dedicated arm notes (`trigger note + 24 semitones`) or in the UI.

## Typical setup

1. Open `index.html` in a Chromium-based browser with Web MIDI support.
2. Select the audio input device.
3. Enable MIDI.
4. Arm the pads you want to capture.
5. Assign output channels per pad (to your mixer/interface routing).
6. Run your sequencer pattern and capture sections as notes are triggered.

## Intended use cases

- Songwriting with pre-defined section structure
- Live arrangement capture
- Performance transitions between recorded sections
- Hardware-sequencer-driven clip launching

## Notes and limits

- Browser audio device behaviour depends on OS + browser + interface drivers.
- Multi-output routing may require mixer/interface routing configuration.
- This app records and plays clips; it does not implement DAW-style timeline editing and it has no internal sequencer or loop triggering (yet).
