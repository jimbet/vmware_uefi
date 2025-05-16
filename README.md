# vmware_uefi
Custom VMware UEFI ROMS for VMware Workstation 17.6.3 on Linux Host (tested on Fedora 42)

For those who are looking for a custom System Manufacturer, System Model, and BIOS information for the guest OS, such as Windows 11, Server 2019, and more.
These custom UEFI ROMS will hide the virtual VMware info from the guest OSes and make it look like the OS runs on physical hardware.

Newer hardware would no longer accept SMBIOS.reflectHost = "TRUE" to mimic the host System Manufacturer, System Model, and BIOS information. It will be hard for somebody who needs to hide their virtual environment from the guest OSes or some darn Windows application.
This could also be hard for those who work as malware analysts because the malware will do a self-destruct, making the malware analysis impossible.


Before using these custom UEFI ROMS, please pay attention to this:

1. Make sure to back up the original UEFI ROMS
2. Replace the original UEFI ROMS at /usr/lib/vmware/roms/EFI20-64.ROM

For a new installation:
1. For a new installation, you can just create it

For an existing VMware guest OS:
1. Make sure to back up your VMware folder <-- up-2-u
2. Rename/backup/delete your current XXXXX.nvram file <-- must do it
3. You have to know your TPM password <-- must have
4. You have to know your existing user and password for your Microsoft account (Hotmail/Outlook/Live) <-- optional
5. You have to know your existing secondary email (for two-step login) <-- optional
6. You have to get your BitLocker recovery codes (if you set BitLocker to on) <-- optional

Enjoy!!!
