Eject Media from a Windows Volume

This is just a convenience repository for the `EjectVolumeMedia.exe` binary.

I use it mainly on Windows Packer/Vagrant environments to eject the VirtualBox Guest Additions media.

The following PowerShell script will eject the media on the `E` volume:

```powershell
# download the binary.
$ejectVolumeMediaExeUrl = 'https://github.com/rgl/EjectVolumeMedia/releases/download/v1.0.0/EjectVolumeMedia.exe'
$ejectVolumeMediaExeHash = 'f7863394085e1b3c5aa999808b012fba577b4a027804ea292abf7962e5467ba0'
$ejectVolumeMediaExe = "$($env:TEMP)\EjectVolumeMedia.exe"
Invoke-WebRequest $ejectVolumeMediaExeUrl -OutFile $ejectVolumeMediaExe
$ejectVolumeMediaExeActualHash = (Get-FileHash $ejectVolumeMediaExe -Algorithm SHA256).Hash
if ($ejectVolumeMediaExeActualHash -ne $ejectVolumeMediaExeHash) {
    throw "the $ejectVolumeMediaExeUrl file hash $ejectVolumeMediaExeActualHash does not match the expected $ejectVolumeMediaExeHash"
}

# eject E.
&$ejectVolumeMediaExe E
```

The code came from [How To Ejecting Removable Media in Windows NT/Windows 2000/Windows XP](https://support.microsoft.com/en-us/kb/165721).

For a more complete version see the [Windows Device Console (Devcon.exe) source code](https://msdn.microsoft.com/windows/hardware/drivers/devtest/devcon).

For a closed-source alternative use [Sync](https://technet.microsoft.com/en-us/sysinternals/bb897438).
