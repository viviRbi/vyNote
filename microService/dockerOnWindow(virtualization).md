# Enable virtualization
- Check if virtualization enable by cmd systeminfo.exe
- In Hyper V, if Virtualization Enabled in Firmware = No. Need to enable it
- Settings -> Update -> recovery -> Advance startup: restart now 
- Troubleshoot -> Advance options -> UEFI Firmware restart 
- F10 right keyboard Virtualization technology -> Enter -> Enable -> F10 (save and exist)
- Check again by cmd -> systeminfo.exe 

# Docker