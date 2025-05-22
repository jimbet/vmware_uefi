# vmware_uefi
Custom VMware UEFI ROMS for VMware Workstation 17.6.3 on Linux Host (tested on Fedora 42) / It can also be used in Windows VMware Workstation Pro 17.6.3 (tested on Windows 11 Pro)

For those who are looking for a custom ***System Manufacturer, System Model, and BIOS information*** for the guest OS, such as Windows 11, Server 2019, and more.
These custom UEFI ROMS will hide the virtual VMware info from the guest OSes and make it look like the OS runs on physical hardware.

Newer hardware would no longer accept ***SMBIOS.reflectHost = "TRUE"*** to mimic the host ***System Manufacturer, System Model, and BIOS information***. 
Most error messages on a Linux host are ***"vcpu-0 Host: can't find host SMBIOS entry point"***. This indicates that VMware could not find the SMBIOS entry point to inject its content into the host SMBIOS table while starting the VMware guest OS. 
VMware VMX file injection can only work on SMBIOS version 2.7 and below. That's why old version hardware can use this method, but on modern hardware (Laptop/Desktop), they use a higher version of SMBIOS (mostly version 3.6), thus the ***SMBIOS.reflectHost = "TRUE"*** injection into the ***XXXX.vmx*** file is impossible. The only solution is to modify the UEFI ROM/firmware and inject the custom text into a specific location.

Without changing the ***System Manufacturer, System Model, and BIOS information***, it will be hard for somebody who needs to hide their virtual environment from the guest OSes or some darn application.
This could also be hard for those who work as malware analysts because the malware will do a self-destruct when it detects the machine is running under a virtual environment, making malware analysis impossible.

So, my custom ROMs will cater:
1. ***System Manufacturer*** = ***Dell.Inc.A00***
2. ***System Model*** = ***Dell.XPS11***
3. ***BIOS Version/Date*** = ***Dell.Inc.A00 Dell.XPS, 5/5/2025***

System Information:
![System Information](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/sys-info-grab.png)

The three pieces of information above are mostly looked up by malware or some darn Windows app.
By changing all three information above, you will fool the malware/app into thinking that the guest OS is running on physical hardware, not virtual hardware.
At the moment, only three pieces of information above can be modified. For deep analysis tools such as [ScoopyNG](https://www.trapkit.de/tools/scoopyng/), this tool will detect that the guest OSes were running under VMware, as the detection tools would query _get version_ and _get memory size_.

![WMIC Command v1-UGLY](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/wmic-1.jpg)

***v1-UGLY***: There is still a VMware string in the UEFI BIOS firmware


![WMIC Command v2-MAKEUP](https://raw.githubusercontent.com/jimbet/vmware_uefi/refs/heads/main/wmic-2.jpg)

***Update v2-MAKEUP***: I've successfully modded the UEFI Firmware info from v1-UGLY.. replacing another string in the UEFI BIOS firmware


This mod is far from perfect. However, it should be enough to help us hide our virtual environment, as this problem has arisen over the past 7 years without a single solution.
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

_P/S: I do need your feedback after you have used this modded ROM_
