# DonutzSwitchModePlugin

This little Simhub plugin adds an option to transform a simple rotary encoder into a mode switch. Based on the selected mode you can use a second rotary encoder to address Simhubs Control Mapper roles. It multiplies your button functionality.

## Instructions

Youtube tutorial: https://www.youtube.com/watch?v=dLPLN8p9JPM
<br>

### 1) Assign keybindings. Up to five independent Mode Switches are possible now. Each of these five mode switches is able to control 12 control mapper roles.
Legacy mode is still there for backwards compatibility.<br>
<img width="391" height="429" alt="grafik" src="https://github.com/user-attachments/assets/a03ced6a-1c00-4224-b789-2aed48e1bf88" />

### 2) Define modes (before of course you need to define roles in Simhub Control mapper)
<img width="989" height="687" alt="grafik" src="https://github.com/user-attachments/assets/d1cefbf1-be87-4480-8a70-e98ff889b368" />

### 3) Assign mode settings to mode switches
   e.g. [1,2,4][2,3][5,7] would mean that Mode Switch 1 is assigned to modes 1,2,4, Mode Switch 2 is assigned to modes 2 and 3, Mode Switch 3 is assigned to modes 5 and 7. Up to five [] groups can be defined here.
<img width="576" height="367" alt="grafik" src="https://github.com/user-attachments/assets/6ba3882d-ae8e-47e4-8d52-3f1b4aa0850f" />

## Properties
### DonutzModeSwitcherPlugin.Switch[ID]AllowedModesString<br>
--> list of allowed modes including current mode marked (as string)<br><br>

### DonutzModeSwitcherPlugin.Switch[ID]ModeID<br>
--> current mode ID<br><br><br>

### DonutzModeSwitcherPlugin.Switch[ID]Mode<br>
--> current mode name<br><br>

### DonutzModeSwitcherPlugin.Switch[ID]ModeCSV[x]<br>
--> DonutzModeSwitcherPlugin.SwitchModeCSV')<br>
---> You can define more than one label in the mode name tag (separated by a colon ';'). This way you can address each sub-name <br>
---> Example: <br>
<img width="397" height="80" alt="461916571-e01fa751-b163-4b3d-bfda-a320ce24428e" src="https://github.com/user-attachments/assets/878bca38-fcc8-4706-bb13-43524860400a" /><br>
<img width="610" height="76" alt="grafik" src="https://github.com/user-attachments/assets/a5cf9d05-bbb7-4724-883c-8354eb4abed5" /><br>
<img width="454" height="196" alt="grafik" src="https://github.com/user-attachments/assets/0fcaee00-b085-4b70-bf31-44eb264d3a2c" /><br>
<br><br>
### DonutzModeSwitcherPlugin.SwitchAllModes<br>
--> list of all modes<br><br>
---> $prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Name = name of Mode 1<br><br><br>
<img width="1127" height="761" alt="grafik" src="https://github.com/user-attachments/assets/cc3f71be-b1a2-4bee-a452-6731e4fd09d2" />
<br><br>
### Role name convention / exclusive mode
A "§" Symbol at the end of the role name means "exclusive mode". You only need it if more than one mode switch shall control the behavior of the same button.
If you do not set the §, then the role is working in "normal mode". Which means it does not matter which switch has been used as last. This mode will be triggered. 
If the role ends with this § symbol, then this role is working in "exclusive mode". Only if the assigned mode switch has been the last one used, then this role will be triggered.
This is only important if you want to assign the very same buttons to different mode switches. With "normal mode" the click on a button then would trigger multiple roles which might not be what you want.

"Normal mode" scenario:<br>
<img width="764" height="435" alt="grafik" src="https://github.com/user-attachments/assets/e8947c53-e94f-4e39-b141-ed23fbab192e" /><br>
-> strictly separated buttons for each mode switch.

"Exclusive mode" scenario:<br>
<img width="789" height="457" alt="grafik" src="https://github.com/user-attachments/assets/5bc0f782-2703-4ae1-a0c2-ca172e36c2fe" /><br>
-> same buttons assigned to different mode switches.



<br><br><br><br>### Legacy stuff for backwards compatibility:<br>
<details>

DonutzModeSwitcherPlugin.SwitchMode<br>
--> current mode name<br>
DonutzModeSwitcherPlugin.SwitchModeID<br>
--> current mode ID<br>
DonutzModeSwitcherPlugin.SwitchAllowedModesString<br>
--> list of allowed modes including current mode marked (as string)<br>
DonutzModeSwitcherPlugin.SwitchAllowedModes<br>
--> list of allowed modes<br>
DonutzModeSwitcherPlugin.SwitchAllModes<br>
--> list of all modes<br><br>
---> $prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Name = name of Mode 1<br>
---> $prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Action1 (.Action2, .Action3, ...) = shows the action/role assigned to the mapped button.<br>
<img width="467" height="497" alt="grafik" src="https://github.com/user-attachments/assets/f6bdae17-413a-4857-86ba-0793e505fb43" /><br>




![grafik](https://github.com/user-attachments/assets/7fa2f31a-aa6d-44c9-a015-56387a02077d)

![grafik](https://github.com/user-attachments/assets/18f1f40f-bde6-4887-ae36-b475eb855647)

</details>

<br>Discord: https://discord.gg/KuSsEYgB3k
<br>Buy me a coffee if you want at [Paypal](https://paypal.me/donutz75?country.x=DE&locale.x=de_DE).
