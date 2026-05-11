# DonutzSwitchModePlugin

This SimHub plugin transforms a simple rotary encoder into a mode switch.
Depending on the selected mode, a second encoder can trigger different Control Mapper roles in SimHub — multiplying your button functionality.

---

## 🚀 Features

- Multiple **independent mode switches** (configurable count)
- Each switch can control a **configurable number of Control Mapper roles**
- **Custom Mode Mappings** – define named mode profiles and reuse them
- **Advanced Mode Mappings** – automatically switch profiles based on game, car, or car class
- **Exclusive mode** for precise, conflict-free button behavior
- **Custom commands** to extend what a button press can do:
  - 🎮 **GROUPED** – chain multiple Control Mapper roles, waits, and keystrokes into a single macro sequence
  - 🔄 **PROPERTY** – cycle a custom SimHub property through a list of values with every press
  - 💬 **IRCHAT** – send iRacing chat messages or pit commands directly from your wheel

---

## 🛠️ Setup Guide

### 1. Keybindings

Bind your physical controls to the plugin actions in SimHub:

- **Increase / Decrease Switch N Mode** — for relative rotary encoders (one detent = next/previous mode)
- **Switch N Mode 1–12** — for absolute encoders (each position jumps directly to a mode slot)
- **Trigger Mapper Role 1–N** — bind these to your steering wheel buttons to fire the active mode's actions

### 2. Mode Settings

Define your modes and assign Control Mapper roles to each one.

- Each mode has a **name** and up to N **Mapper Role** slots
- The mode name can contain multiple values separated by `;` — useful for displaying sub-labels on a dash
- When a mode becomes active, its assigned roles fire automatically
- Use **Reload Roles** after adding new roles in SimHub's Control Mapper
- **Trigger Duration** controls how long (in ms) a role is held when fired (default: 50 ms)

### 3. Mode Mapping

Define which modes are available per switch — and optionally per game or car.

Use the `[Switch1Modes][Switch2Modes]…` format:

| Example | Meaning |
|---------|----------|
| `[1,2,3]` | Switch 1 cycles through modes 1, 2, 3 |
| `[1,2][4,5]` | Switch 1: modes 1+2 · Switch 2: modes 4+5 |
| `[1,2][4,5][1,6]` | three switches, each with their own mode set |

Add profiles per game (`iRacing`) or per game+car (`iRacing_GT3 AMG`). Jump into a session and use **Add game** or **Add game+car** — the current values are filled in automatically.

### 4. Advanced Mode Mappings *(optional)*

Automatically apply a named mode profile based on game, car, or car class — no manual switching needed. See the [Advanced Mode Mappings](#-advanced-mode-mappings) section below.

---

## 🗂️ Mode Mapping System

The plugin resolves which modes are active for each switch using the following **priority order** (highest to lowest):

1. **Advanced Mode Mappings** (JSON filter by game/car/car class → references a Custom Mode Mapping)
2. **ModeMappings** (`Game_Car`, `Game`, or `_` fallback key)
3. **Default ModeCsv** (global fallback)

---

## 🏷️ Custom Mode Mappings

Custom Mode Mappings let you define **named mode profiles** that can be referenced by Advanced Mode Mappings.

| Field | Description |
|-------|-------------|
| **Name** | Unique profile name (e.g. `GT3 Racing`, `Rally Setup`) |
| **Modes** | ModeCsv string defining which modes are active per switch |

### Examples

| Name | Modes |
|------|-------|
| GT3 Racing | `[1,2,3][4,5]` |
| Rally Setup | `[6,7][8,9,10]` |
| Drift Modes | `[1,3,5]` |

---

## 🤖 Advanced Mode Mappings

Advanced Mode Mappings allow you to **automatically apply a Custom Mode Mapping** based on the current game, car, or car class. The profile switches automatically when SimHub detects a change.

### JSON Format

```json
{
  "Filter": {
    "Game": "iRacing",
    "CARS": ["GT3 AMG", "GT3 BMW"]
  },
  "Mode Mapping": "GT3 Racing"
}
```

```json
{
  "Filter": {
    "Game": "Assetto Corsa Competizione",
    "CAR CLASSES": ["GT3", "GT4"]
  },
  "Mode Mapping": "GT3 Racing"
}
```

### Filter Parameters

| Parameter | Description |
|-----------|-------------|
| `Game` | Exact game name as reported by SimHub (e.g. `"iRacing"`, `"rFactor 2"`) |
| `CARS` | List of car names or partial names — uses substring matching |
| `CAR CLASSES` | List of car class names — uses substring matching |

> **Note:** `CARS` and `CAR CLASSES` can be combined. All specified conditions must match.

### Setup Steps

1. Create your **Custom Mode Mappings** with unique names
2. Add a new **Advanced Mode Mapping**
3. Enter the JSON filter configuration
4. Click **PARSE** to validate the JSON
5. Click **APPLY** to save

---

## 🔍 Plugin Properties

### Multi-Switch Properties (current version)

```
DonutzModeSwitcherPlugin.Switch[ID]Mode               → Current mode name
DonutzModeSwitcherPlugin.Switch[ID]ModeID             → Current mode ID (number)
DonutzModeSwitcherPlugin.Switch[ID]ModeCSV            → Current mode name split by ';' (array)
DonutzModeSwitcherPlugin.Switch[ID]AllowedModes        → List of allowed mode IDs
DonutzModeSwitcherPlugin.Switch[ID]AllowedModesString  → Formatted text list (current mode marked with >>)
DonutzModeSwitcherPlugin.Switch[ID]Action[ID]          → Name of the role bound to that switch/action
DonutzModeSwitcherPlugin.SwitchAllModes                → Dictionary of all defined modes
DonutzModeSwitcherPlugin.DeviceListConnectedOnly       → List of currently connected devices
```

**Example:**
```
$prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Name   → Name of Mode 1
$prop("DonutzModeSwitcherPlugin.Switch1ModeCSV")[0]        → First part of mode name (split by ';')
```

---

## 🔒 Role Naming Convention: Exclusive vs Normal Mode

- **Normal Mode:** The button triggers regardless of which switch was last used.
- **Exclusive Mode:** The button only triggers if the assigned switch was the last one used.

Add the symbol `§` at the **end of a role name** to enable exclusive mode.

🔹 Normal Mode Example:
- Role name: `TC1+`

🔹 Exclusive Mode Example:
- Role name: `TC1+§`

---

## 🧩 Custom Commands

### IRCHAT

| Syntax | Description |
|--------|-------------|
| `IRCHAT:Hello drivers!` | Sends a message to iRacing chat |
| `IRCHAT:#fuel` | Sends a pitstop command |

### PROPERTY

Creates a cycling property that steps through a list of values each time the mode is activated.

| Syntax | Description |
|--------|-------------|
| `PROPERTY:MyProp,Low,Medium,High` | Creates a property cycling through 3 values |
| `PROPERTY:MyProp,High,Medium,Low` | Reversed order (for decrement direction) |
| `PROPERTY:MyProp,Low,Medium,High,Low` | Loop (first value repeated at end) |

Read the current value in your dashboard:
```
$prop('DonutzModeSwitcherPlugin.CustomProperty.MyProp')
```

### GROUPED

Triggers multiple roles or keyboard inputs in sequence.

| Syntax | Description |
|--------|-------------|
| `GROUPED:ABS+;TC1+` | Triggers both roles simultaneously (default 50 ms) |
| `GROUPED:ABS+[200];TC1+` | ABS+ for 200 ms, TC1+ for default 50 ms |
| `GROUPED:ABS+[200];(wait:1000);TC1+` | ABS+ → wait 1000 ms → TC1+ |
| `GROUPED:(text[200]:bbb)` | Types "b" three times with 200 ms delay |

#### Text Input Modifiers (used inside `text[...]`)

| Symbol | Meaning |
|--------|---------|
| `$` | CTRL |
| `^` | SHIFT |
| `§` | SHIFT + CTRL |

Custom Commands example:  
<img width="1109" height="524" alt="image" src="https://github.com/user-attachments/assets/81ec2383-7094-405a-ad1e-bcf482ad486d" />

---

## ⚡ Events & Trigger Properties

### Events

For every defined mode, the plugin registers a SimHub event that fires whenever that mode becomes active:

```
DonutzModeSwitcherPlugin.ModeChanged_[ModeName]   → fires when the mode named [ModeName] is activated
```

**Example:** A mode named `Race` registers the event `ModeChanged_Race`.  
You can use this in SimHub's Control Mapper or dash scripts to react to mode changes.

### Trigger Properties

These properties briefly switch to `"1"` when an action fires, then return to `"0"` after ~20 ms. Useful for triggering animations or sounds on a dash.

```
DonutzModeSwitcherPlugin.Switch[ID]Activity_detected      → "1" for ~20 ms whenever Switch [ID] changes mode
DonutzModeSwitcherPlugin.Switch[ID]Action[ID]_triggered   → "1" for ~20 ms when Action [ID] of Switch [ID] fires
DonutzModeSwitcherPlugin.LastActionTriggered              → Name of the most recently triggered action/role
```

---

## 💬 Community & Support

📢 Discord: [Join the Community](https://discord.gg/KuSsEYgB3k)
☕ Support the project: [Buy me a coffee](https://paypal.me/donutz75)
