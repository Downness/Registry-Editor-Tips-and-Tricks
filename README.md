
* Info: See PDF for images and better view...

How to speed up your processor using Registry Keys
-------------------------------------------------------------------------------

Warning
Increasing speed of the laptop CPU can overheat the laptop, so, without a good cooler below laptop it will simply shut down because of overheat… I am suggesting you buying at least:
https://www.coolermaster.com/en-global/products/notepal-i300/?tab=tech_spec


Specifications:
* Fan Dimensions (L x W x H)160 x 160 x 15 mm / 6.3 x 6.3 x 0.6 inch
* Fan Speed 700–1400 RPM ± 150
* Fan Airflow 35 - 70 CFM
Laptop temperatures with this cooler always connected and working are:

How to speed up your processor using Registry Keys
In my example I have a laptop “Dell Vostro 5502” with processor “11th Gen Intel® Core™ i7-1165G7 @ 2.80GHz” working on up to 4.7 GHz where it is for some reason set to work on up to 1.69 GHz with a possible boost up to 2.7 GHz and later on 4.1 GHz (because for some reason Windows doesn’t allow the full usage of the CPU)…
In Task Manager you will find this description about the processor:

First thing that I was asking is the 2 given options in the Registry Keys for “EfficiencyClass” when I can have 3 if processor is locked on 1.69… The other thing to consider here is enabled energy saver locking that processor on 1.69 GHz, and not on 2.7 GHz… That energy saver with Windows given options shall make this Intel CPU to work on 0.87 GHz and even slower on about 0.4 GHz when the greater CPU consumption and usage comes in place…

First of all to avoid that we need to fix some Registry values and settings:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power

Here I would pay attention what does EnergyEstimationEnabled option… Leave it turned on, because, by some thinking – under the folder EnergyEstimation , but that is my choice…

* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\EnergyEstimation\CPU\EfficiencyClass\0


* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\EnergyEstimation\CPU\EfficiencyClass\0\PowerCurve\0
Explanation for the values: FrequencyPercent is represented in decimals as a percentage, and PowerEnvelope is represented in HexaDecimal values but through the Decimal values – so for example if you type in the Decimal value “1000” you should see it as is written in HexaDecimal values, which translated gives us 4.096 GHz… You should notice one interesting thing that you can’t type in all of the Frequencies for the processor because in hexadecimal values you can write and letters A – F, so for example “A99” would be 2.713 GHz, and here you can write only numbers which means either you would need to agree to processor speed of (in Hexadecimal values) “999” or “1000”, which is translated: 2.457 GHz (for “999”) or 4.096 GHz (for “1000)…
So my setting is:

* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\EnergyEstimation\CPU\EfficiencyClass\1

* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC

Laptop works faster if VetoPolicy options are turned off…

* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\Activators\28\VetoPolicy
- EA:PowerStateDischarging: 0
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\Activators\Default\VetoPolicy
- EA:EnergySaverEngaged: 0


I am not sure if this values represent the maximum speed of the processor but I have placed them all on maximum for my processor:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\VetoPolicy\EA\{DDC4A1A9-7163-4072-878F-5416933D22D1}\{885D4A75-7CE6-4075-8AF0-2BFC82B62FE3}\{AAF91665-FAFF-449D-B47A-5E19B4ABB4E2}
- Type 4121 -> 4700
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\VetoPolicy\EA\{DDC4A1A9-7163-4072-878F-5416933D22D1}\{885D4A75-7CE6-4075-8AF0-2BFC82B62FE3}\{EC5C2F86-8FC5-4ACE-BC77-B29BF20276B0}
- Type 4106 -> 4700
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\VetoPolicy\EA\{EE8ED144-1D82-4B2E-B807-2082FE3D4AC7}\{850FAEAE-3ADC-4CC6-BA5C-7F4151466500}\{CF69B873-5A0E-4F7E-AC84-8A185A47A85F}
- Type 4106 -> 4700
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PDC\VetoPolicy\EA\{EE8ED144-1D82-4B2E-B807-2082FE3D4AC7}\{850FAEAE-3ADC-4CC6-BA5C-7F4151466500}\{E4E90B30-BD23-4AEA-B44E-3777C9401354}
- Type 4145 -> 4700
You will notice that those folders – “keys” there is a value that has a DWORD named “Value” and that it is turned off, I have placed it to 1…

* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings

Talking about PowerSettings you need to turn High Performance on, set graphics to work in High performance mode, to set CPU to work by High Performance if you wish on all 3 levels (3 different keys under “DefaultPowerSchemeValues” folder) – because it is unknown in Registry Editor which level is for “Best Battery Life” setting, which is “Balanced” setting, and which is for “Best (High) performance” setting… What I can conclude, for my processor and type of Windows that I have – key: “8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c” represents the “High performance” mode and mostly from that key I have been copying to other two keys it’s own already set values… Some keys I have changed completely, adjusting values how I liked…
How this part of the registry works? First you will have a “key” (folder) where you will find options that you can implement under “keys” (folders) 0, 1, 2 and you will have a folder where you can implement those options named: “DefaultPowerSchemeValues”… In those folders you can find the description and a “friendly name” (also a type of a description) of the current part of the Registry Keys… Each of the main folders named for example: “0”, “1” or “2” will have some type of a value that you can use later on… That value you will find under a DWORD (data) name “SettingValue”… The best setting whether it’s under folder “0”, “1” or “2” you can copy into the “AcSettingIndex” or “DcSettingIndex”, or “ProvAcSettingIndex” or “ProvDcSettingIndex”…
In cases where you don’t have options under keys (folders) “0”, “1”, “2”, you will have some type of a scale that you can implement… Maximum value of the scale you can find under the main folder and it’s DWORD named “ValueMax” and it’s possible minimum under a DWORD named “ValueMin”… Always take a look at: DWORD named ValueUnits that will have a description for example: “@%SystemRoot%\system32\powrprof.dll,-81,percent” – there the last word we can find is the word “percent” meaning you should implement in decimal numbers value from 0 to 100 representing some kind of a percentage of a usage for some of the situations…
Some of the settings that I have implemented are:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00

Under power settings you will find the key: “54533251-82be-4824-96c1-47b60b740d00” with “Processor power settings” and you need to see each of the keys (folders) it has and to adjust them except time settings which I haven’t changed…
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\3b04d4fd-1cc7-4f23-ab1c-d1337819c4bb
- FriendlyName: Allow Throttle States
- Setting implemented: Off
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\40fbefc7-2e9d-4d25-a185-0cfd8574bac6
- FriendlyName: Processor performance decrease policy
- Setting implemented: Single
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\40fbefc7-2e9d-4d25-a185-0cfd8574bac7
- FriendlyName: Processor performance decrease policy for Processor Power Efficiency Class 1
- Setting implemented: Single
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\447235c7-6a8d-4cc0-8e24-9eaf70b96e2b
- Processor performance core parking parked performance state
- Best option for the speed of processor: Lightest Performance State
- My setting implemented: No preference
- Some theory on that topic: Unused CPUs enter parked state and not to spend energy they can enter Deepest Performance state to save power and reduce the heat… Otherwise faster option is “Lightest Performance state”…
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\45bcc044-d885-43e2-8605-ee0ec6e96b59
- FriendlyName: Processor performance boost policy
- All Settings implemented: 0x64 (or Decimal: 100 (%))
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\465e1f50-b610-473a-ab58-00d1077dc418
- FriendlyName: Processor performance increase policy
- Setting implemented: Rocket
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\4e4450b3-6179-4e91-b8f1-5bb9938f81a1
- FriendlyName: Processor duty cycling
- Setting implemented: Allow processor duty cycling.
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\5d76a2ca-e8c0-402f-a133-2158492d58ad
- Description: Specify if idle states should be disabled. 
- Setting implemented: Enable idle
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\6c2993b0-8f48-481f-bcc6-00dd2742aa06
- FriendlyName: Processor idle threshold scaling
- Setting implemented: Disable scaling
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\71021b41-c749-4d21-be74-a00f335d582b
- Description: Specify the number of cores/packages to park when fewer cores are required.
- Setting implemented: Ideal number of cores
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\75b0ae3f-bce0-45a7-8c89-c9611c25e100
- FriendlyName: Maximum processor frequency
- Setting implemented: Decimal value: 4700
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\75b0ae3f-bce0-45a7-8c89-c9611c25e101
- FriendlyName: Maximum processor frequency for Processor Power Efficiency Class 1
- Setting implemented: Decimal value: 2457
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\7f2f5cfa-f10c-4823-b5e1-e93ae85f46b5
- FriendlyName: Heterogeneous policy in effect.
- Setting implemented: Use heterogeneous policy 0

Don’t forget to check options for Graphic card:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\5FB4938D-1EE8-4b0f-9A3C-5036B0AB995C
- FriendlyName: GPU preference policy
- Setting implemented: No preference (because other setting I had was: Low Power)
Check Energy Saving settings:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\DE830923-A562-41AF-A086-E3A2C6BAD2DA
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\DE830923-A562-41AF-A086-E3A2C6BAD2DA\5C5BB349-AD29-4ee2-9D0B-2B25270F7A81
- FriendlyName: Energy Saver Policy
- Setting implemented: User
Also, you can go back to processor settings and find the “Processor performance increase threshold” and “Processor performance decrease threshold” options, as I know I have changed some of the percentages, for example from 35 to 20 if is faster and from 45 to 50, but maybe I have pushed it above the edge or below the edge (I am not even sure)… Maybe those settings are fine by themselves…
My options there are in decimal values:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\7b224883-b3cc-4d79-819f-8374152cbe7c
- FriendlyName: Processor idle promote threshold
- Setting implemented: 14 (20)
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\943c8cb6-6f93-4227-ad87-e9a3feec08d1
- FriendlyName: Processor performance core parking over utilization threshold
- Setting implemented: 1e (30)
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\06cadf0e-64ed-448a-8927-ce7bf90eb35d
- FriendlyName: Processor performance increase threshold
- Setting implemented: 50 (80)
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\06cadf0e-64ed-448a-8927-ce7bf90eb35e
- FriendlyName: Processor performance increase threshold for Processor Power Efficiency Class 1
- Setting implemented: 50 (80)	
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\12a0ab44-fe28-4fa9-b3bd-4b64f44960a6
- FriendlyName: Processor performance decrease threshold
- Description: Specify the lower busy threshold that must be met before decreasing the processor's performance state (in percentage).
- Setting implemented: 14 (20)
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\12a0ab44-fe28-4fa9-b3bd-4b64f44960a7
- FriendlyName: Processor performance decrease threshold
- Description: Specify the lower busy threshold that must be met before decreasing the processor's performance state (in percentage).
- Setting implemented: 14 (20)
There is also a setting for “Processor performance boost mode”:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\be337238-0d82-4146-a960-4f3749d470c7
- Setting implemented: 5
Set System cooling policy:
* Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\94D3A615-A899-4AC5-AE2B-E4D8F634367F\1
- Setting implemented: Increase fan speed before slowing the processor
Edit the option for Minimal Power Management:
* Computer\HKEY_CURRENT_USER\Control Panel\PowerCfg

Here, on my Windows, under a number 4 is:

So just set in the PowerCfg string CurrentPowerPolicy: 4

-------------------------------------------------------------------------------

Graphic cards
This Laptop “Dell Vostro 5502” has also dual graphics cards - integrated “Intel® Iris® Xe Graphics” and “NVIDIA GeForce MX330”… It has 16GB of RAM memory, and 500 GB SSD hard drive…
There is a topic of a small and reducing processor speed thanks to the small “Bus” (an implemented cable for transferring the data in between the graphic card and the other chips), and that because of it (maybe set on 1.3 GHz) and the processor reduces it’s speed…
HardwareAcceleration
In Registry Editor add the key for removing hardware support for graphics into:
* Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphic
Create DWORD named DisableHWAcceleration and set it to the value: 1
NVIDIA Control Panel:
* Turn on Developer settings: (see PDF)
Set PhysX processor to NVIDIA: (see PDF)
Allow this: (see PDF)
And make sure you implement best options for NVIDIA graphic card: (see PDF)
-------------------------------------------------------------------------------
Intel graphics settings:
Let’s talk about the Intel graphic card settings… Besides regular settings for brightness, contrast, saturation and hue, there are some more options under Registry Keys that you might find interesting for a better display view…
I believe that here a setting: “Enable…” or “…Enabled” (for example “EnableACE” or SuperResolutionEnabled”) doesn’t need to have only options 0 or 1, but it can have any possible options, and the point is that you actually play with the display settings and figure out when you have the best view… I will give you a hint – if you set everything else right – setting the “SkinTone” to a value “3” gives you somehow “a Saint computer user”… So, the conclusion is that you can create anything that you like from these values without needing to restart the computer to see the results…
* Computer\HKEY_CURRENT_USER\SOFTWARE\Intel\Display\igfxcui\Media

My current settings are shown on this image: (see PDF)

My previous settings were not that good: (see PDF)

There is one more thing to add:
* Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Intel\IGFX\DPP

Edit DWORD: “EnableHardware3DLUT”, set value: “12312123”
