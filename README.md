# [TITLE] - flute and live electronics

A Max/MSP project for solo flute with live electronics.

**Author:** Alessandro De Iturbe  
**License:** [MIT License](LICENSE)

---

## Overview

This is the live electronic part of my composition for solo flute and live electronics for **AltreVoci Ensamble**. The patch handles real-time audio processing, routing, effects, and cue-based event playback during performance.

## Requirements

- [Max/MSP](https://cycling74.com/) 8 or later
- Node for Max (included with Max)

## Getting Started

Open `altrevoci_2027_flauto.maxproj` in Max. The project window will organize all dependencies automatically.

## Project Structure

```
altrevoci_2027_flauto/
├── patchers/
│   ├── main.maxpat                      # Main patcher — entry point
│   ├── cue_manager.maxpat               # UI and logic for cue recall
│   ├── csi.cues_manager_general.maxpat  # General cue management abstraction
│   ├── reverb.poly.maxpat               # Polyphonic convolution reverb
│   ├── water_effect.maxpat              # Water texture effect
│   └── prime.maxpat                     # Prime number generator/detector
├── code/
│   └── csi.cues_manager_node.js         # Node for Max: cue engine backend
├── data/
│   ├── cues.json                        # Active cue list
│   └── project_presets.json             # Saved mixer/routing presets (pattrstorage)
├── media/
│   ├── ir_glass_1.wav                   # Impulse response for convolution reverb
│   └── water_drop.mp3                   # Sample for water effect
└── other/
    └── LICENSE
```

## Cue System

The cue engine is based on [csi_cue_manager](https://github.com/albertobarberis/csi_cue_manager) by Alberto Barberis, adapted for this project. It runs in Node for Max (`csi.cues_manager_node.js`) and provides sequential, typed event storage for performance control.

**Max messages:**

| Message                         | Description                                 |
| ------------------------------- | ------------------------------------------- |
| `add <cue> <type> <data>`       | Add or update an event in a cue             |
| `insertCue <cue> <type> <data>` | Insert a cue at a position, shifting others |
| `deleteCue <cue>`               | Delete a cue and renumber subsequent ones   |
| `deleteEvent <cue> <type>`      | Remove a specific event from a cue          |
| `getCue <cue>`                  | Recall and output all events in a cue       |
| `copyEvent <src> <type> <dst>`  | Copy an event between cues                  |
| `moveEvent <src> <type> <dst>`  | Move an event between cues                  |
| `import <filename>`             | Load a cue list from a JSON file            |
| `export <filename>`             | Save the current cue list to JSON           |
| `printAll`                      | Print all cues to the Max console           |

Backups are written automatically to `data/BACKUP.*.json` after `add` and `move` operations.



| Branch        | Purpose                    |
| ------------- | -------------------------- |
| `main`        | Stable performance version |
| `development` | Work in progress           |
