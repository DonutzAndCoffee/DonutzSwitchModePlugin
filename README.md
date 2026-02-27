
# DonutzSwitchModePlugin

This SimHub plugin transforms a simple rotary encoder into a **mode switch**. Depending on the selected mode, a second encoder can trigger different **Control Mapper roles** in SimHub — multiplying your button functionality.

📺 **Watch the tutorial on YouTube:**  
[▶️ Click here](https://www.youtube.com/watch?v=dLPLN8p9JPM)

---

## 🚀 Features

- Up to **5 independent mode switches**
- Each switch can control **12 Control Mapper roles**
- **Legacy mode** support for backward compatibility
- **Exclusive mode** for precise button behavior
- **Custom commands**: IRCHAT, PROPERTY, GROUPED

---

## 🛠️ Setup Guide

### 1. Assign Keybindings
You can configure up to five mode switches. Each switch can control 12 roles.  
![Keybindings](https://github.com/user-attachments/assets/a03ced6a-1c00-4224-b789-2aed48e1bf88)

### 2. Define Modes
Before defining modes, make sure you've set up roles in SimHub's Control Mapper.  
![Define Modes](https://github.com/user-attachments/assets/d1cefbf1-be87-4480-8a70-e98ff889b368)

### 3. Assign Modes to Switches
Example: `[1,2,4][2,3][5,7]`  
- Mode Switch 1 → Modes 1, 2, 4  
- Mode Switch 2 → Modes 2, 3  
- Mode Switch 3 → Modes 5, 7  
![Assign Modes](https://github.com/user-attachments/assets/6ba3882d-ae8e-47e4-8d52-3f1b4aa0850f)

---

## 🔍 Plugin Properties

```
DonutzModeSwitcherPlugin.Switch[ID]AllowedModesString → List of allowed modes (current mode marked)
DonutzModeSwitcherPlugin.Switch[ID]ModeID → Current mode ID
DonutzModeSwitcherPlugin.Switch[ID]Mode → Current mode name
DonutzModeSwitcherPlugin.Switch[ID]ModeCSV[x] → Access sub-names in mode name (split by ';')
DonutzModeSwitcherPlugin.SwitchAllModes → List of all defined modes
DonutzModeSwitcherPlugin.Switch[ID]Action[ID] → name of the role bound to that switch/action
```

Example:  
`$prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Name` → Name of Mode 1

---

## 🔒 Role Naming Convention: Exclusive vs Normal Mode

- **Normal Mode**: Button triggers regardless of which switch was last used.
- **Exclusive Mode**: Button only triggers if the assigned switch was the last one used.

Use the symbol `§` at the end of a role name to enable **exclusive mode**.

🔹 **Normal Mode Example:**  
![Normal Mode](https://github.com/user-attachments/assets/e8947c53-e94f-4e39-b141-ed23fbab192e)

🔹 **Exclusive Mode Example:**  
![Exclusive Mode](https://github.com/user-attachments/assets/5bc0f782-2703-4ae1-a0c2-ca172e36c2fe)

---

## 🧩 Custom Commands

### IRCHAT

| Command Type | Syntax Example | Description |
|--------------|----------------|-------------|
| IRCHAT       | `IRCHAT:Hello drivers!` | Sends a message to iRacing chat |
| IRCHAT       | `IRCHAT:#fuel`         | Sends a pitstop command |

### PROPERTY

| Command Type | Syntax Example | Description |
|--------------|----------------|-------------|
| PROPERTY     | `PROPERTY:MyProp,Low,Medium,High` | Creates a property with 3 values |
| PROPERTY     | `PROPERTY:MyProp,High,Medium,Low` | Reversed order (for decrementing) |
| PROPERTY     | `PROPERTY:MyProp,Low,Medium,High,Low` | Creates a loop (first item repeated at end) |

### GROUPED

| Command Type | Syntax Example | Description |
|--------------|----------------|-------------|
| GROUPED      | `GROUPED:ABS+;TC1+` | Triggers both roles simultaneously (default 50ms) |
| GROUPED      | `GROUPED:ABS+[200];TC1+` | ABS+ for 200ms, TC1+ for 50ms |
| GROUPED      | `GROUPED:ABS+[200];(wait:1000);TC1+` | ABS+ → wait 1000ms → TC1+ |
| GROUPED      | `GROUPED:(text[200]:bbb)` | Sends "b" three times with 200ms delay |

#### Text Input Modifiers

| Symbol | Meaning |
|--------|---------|
| `$`    | CTRL    |
| `^`    | SHIFT   |
| `§`    | SHIFT + CTRL |

---

## 🧓 Legacy Compatibility

<details>
<summary>Legacy Properties</summary>

```
DonutzModeSwitcherPlugin.SwitchMode → Current mode name
DonutzModeSwitcherPlugin.SwitchModeID → Current mode ID
DonutzModeSwitcherPlugin.SwitchAllowedModesString → Allowed modes (string)
DonutzModeSwitcherPlugin.SwitchAllowedModes → Allowed modes (list)
DonutzModeSwitcherPlugin.SwitchAllModes → All defined modes
```

Example:  
`$prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Action1` → Role assigned to button 1

![Legacy](https://github.com/user-attachments/assets/f6bdae17-413a-4857-86ba-0793e505fb43)
</details>

---

## 💬 Community & Support

📢 **Discord:** [Join the Community](https://discord.gg/KuSsEYgB3k)  
☕ **Support the project:** [Buy me a coffee](https://paypal.me/donutz75)  
