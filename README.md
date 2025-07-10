# DonutzSwitchModePlugin

This little Simhub plugin adds an option to transform a simple rotary encoder into a mode switch. Based on the selected mode you can use a second rotary encoder to address Simhubs Control Mapper roles. It multiplies your button functionality.

The current mode can be read as property [DonutzModeSwitcherPlugin.SwitchMode]

Available Simhub properties:<br>
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
 --> $prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Name = name of Mode 1
 --> $prop("DonutzModeSwitcherPlugin.SwitchAllModes")[1].Action1 (.Action2, .Action3, ...) = shows the action/role assigned to the mapped button.

Discord: https://discord.gg/KuSsEYgB3k

![grafik](https://github.com/user-attachments/assets/7fa2f31a-aa6d-44c9-a015-56387a02077d)

![grafik](https://github.com/user-attachments/assets/18f1f40f-bde6-4887-ae36-b475eb855647)


<br>Buy me a coffee if you want at [Paypal](https://paypal.me/donutz75?country.x=DE&locale.x=de_DE).
