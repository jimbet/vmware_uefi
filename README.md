***FOR EDUCATIONAL PURPOSES ONLY!!***
<br><br>
***I've closed this repo***
<br><br>
***No more releases will be updated, and all binaries have been removed***
<br><br>
***I'm now using it for my own research only and still actively doing the R&D***
<br><br>
Disclaimer: If a brand name mentioned here is registered and you wish to have it masked/removed, please open a thread in [Issues](https://github.com/jimbet/vmware_uefi/issues), and I will be glad to remove it at your request. Thanks
<br><br>

# vmware_uefi
Custom VMware UEFI ROMS for VMware Workstation 17.6.3 on Linux Host (tested on Fedora 42) / It can also be used in Windows Host VMware Workstation Pro 17.6.3 (tested on Windows 11 Pro)

For those who are looking for a custom ***System Manufacturer, System Model, BIOS information, Motherboard Model and RAM Manufacturer*** for the guest OS, such as Windows 11, Server 2019, and more.
These custom UEFI ROMS will hide the virtual VMware info from the guest OSes and make it look like the OS runs on physical hardware.

Newer hardware would no longer accept ***SMBIOS.reflectHost = "TRUE"*** to mimic the host ***System Manufacturer, System Model, BIOS information, Motherboard Model and RAM Manufacturer***. 
Most error messages on a Linux host are ***"vcpu-0 Host: can't find host SMBIOS entry point"***. This indicates that VMware could not find the SMBIOS entry point to inject its content into the host SMBIOS table while booting the VMware guest OS. 
VMware VMX file injection can only work on SMBIOS version 2.8 and below. That's why old version hardware can use this method, but on modern hardware (Laptop/Desktop), they use a higher version of SMBIOS (mostly version 3.6), thus the ***SMBIOS.reflectHost = "TRUE"*** injection into the ***XXXX.vmx*** file is impossible. The only solution is to modify the UEFI ROM/firmware and inject the custom text into a specific location.

Without changing the ***System Manufacturer, System Model, BIOS information, Motherboard Model and RAM Manufacturer***, it will be hard for somebody who needs to hide their virtual environment from the guest OSes or some darn Windows application.
This could also be hard for those who work as malware analysts because the malware will do a self-destruct when it detects the machine is running under a virtual environment, making malware analysis impossible.

So, my custom ROMs will cater:
1. ***System Manufacturer*** = ***Dell.Inc.A00***
2. ***System Model*** = ***Dell.XPS11***
3. ***BIOS Version/Date*** = ***Dell.Inc.A00 Dell.XPS, 5/5/2025***
4. ***Motherboard Model*** = ***Intel Corporation H610E Alder Lake Intel Corporate***
5. ***RAM Manufacturer*** = ***Kingston Tech. RAM***


***Update: The whole solution now completely hides the virtual environment. Not even Windows itself know that it's on a virtual environment. The downside is that many remnants of 15AD are in the driver INF. Will do if I have the spare time*** 

<br><br>
System Information:
![System Information](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/sys-info-grab.png)

The five pieces of information above are mostly looked up by malware or some darn Windows app.
By changing all five information above, you will fool the malware/app into thinking that the guest OS is running on physical hardware, not virtual hardware.
At the moment, only five pieces of information above can be modified. For deep analysis tools such as ~~[ScoopyNG](https://www.trapkit.de/tools/scoopyng/), this tool will detect that the guest OSes were running under VMware, as the detection tools would query _get version_ and _get memory size_~~ (ScoopyNG is now defeated.. sorry).

![ScoopyNG Defeated](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/scoopyNG_Defeated.jpeg)

***ScoopyNg*** does not detect my modded ROM/FILE/Config as a VMware anymore.. The mystery of the serial number was also solved, ~~but the UUID could not be changed as of now, as the UUID is defined in so many places. Maybe later I will find the way..~~ ***I've found the way to change the UUID***
<br><br>
![UUID_CHANGED](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/UUID_Serial-number.png)

***UUID*** can now be changed and no longer starts with [56 4d], but it remains in UUID format.
<br><br>
![Speccy HDD Before](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/speccy-hdd-before.PNG)
![Speccy HDD After](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/speccy-hdd-after.PNG)
<br>
Difference between before and after using [Speccy](https://www.ccleaner.com/speccy) for the HDD controller.
<br><br>
![Speccy OS Before](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/speccy-OS-before.PNG)
![Speccy OS After](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/speccy-OS-after.PNG)
<br>
Difference between before and after using [Speccy](https://www.ccleaner.com/speccy) for the computer type.
<br><br>
![TaskMGR Before](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/taskmgr-before.PNG)
![TaskMGR After](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/taskmgr-after.PNG)
<br>
Difference between before and after using [Windows Task Manager](https://www.microsoft.com) for the Virtualization.
<br><br>
![SVGA](https://github.com/jimbet/vmware_uefi/blob/main/speccy-SVGA.png?raw=true)
<br>
Only one downside.. the SVGA still detected as VMware SVGA 3D..
<br><br>
![]()
![]()

<br><br>
![WMIC Command v1-UGLY](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/wmic-1.jpg)

***v1-UGLY***: There is still a VMware string in the UEFI BIOS firmware


![WMIC Command v2-MAKEUP](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/wmic-2.jpg)

***Update v2-MAKEUP***: I've successfully modded the UEFI Firmware info from v1-UGLY.. replacing another VMware string in the UEFI BIOS firmware


![mboard-v1](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/mboad-v1.jpg)

***Update v3-PRIMER***: Yeahhh.. changing the Motherboard model into H610E from the default 440BX.. Don't worry about the chipset.. It'll be just fine to use it



![RAM-v1](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/RAM-VM-v1.jpg)

***v3-PRIMER***: RAM is identifying as a VMware Virtual RAM



![RAM-v2](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/RAM-VM-v2.jpg)

***Update v4-FOUNDATION***: Changing the RAM Manufacturer to Kingston Tech. RAM


This mod is far from perfect. However, it should be enough to help hide our virtual environment, as this problem has arisen over the past 7 years without a single solution.
I might try to compile a new release that will eliminate most points of virtual identification. Do keep watching my release.

Before using these custom UEFI ROMS, please pay attention to this:

1. Make sure to back up the original UEFI ROMS
2. Replace/rename the original UEFI ROMS at ***/usr/lib/vmware/roms/EFI20-64.ROM*** (for Linux host)
3. Replace/rename the original UEFI ROMS at ***C:\Program Files (x86)\VMware\VMware Workstation\x64\EFI20-64.ROM*** (for Windows host)

For a new installation:
1. For a new installation, you can just create it

For an existing VMware guest OS:
1. Make sure to back up your VMware guest OS folder <-- up-2-u
2. Rename/backup/delete your current ***XXXXX.nvram*** file in the VMware guest OS folder <-- must do
3. You have to know your TPM password <-- optional
4. You have to know your existing user and password for your Microsoft account (Hotmail/Outlook/Live) <-- optional
5. You have to know your existing secondary email (for two-step login) <-- optional
6. You have to get your BitLocker recovery codes (if you set BitLocker to on) <-- optional

Enjoy!!!

