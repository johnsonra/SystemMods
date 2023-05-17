# Windows
Notes on installing packages on Windows.

## WSL
I ran across an issue with installing WSL on my new Windows 10 computer: I have separate every-day use and admin accounts. The problem is that your account typically needs admin privileges to install WSL, and Microsoft seems to go out of their way to partition WSL images in such a way that it is nearly impossible to install it with my every-day, un-privileged account.

### On your admin account

1. Make sure WSL is enabled. Type Windows-Key + R and type `optionalfeatures.exe`. Scroll down and ensure Windows Sybsystem for Linux is checked.

2. Reboot if you made changes to the option features.

3. Install WSL on the admin account: Run the PowerShell as an administrator and run

`wsl --install`

4. Reboot

5. Check the name of the distribution that was installed with

`wsl --list`

6. Mine is labeled `Ubuntu`. Export the image that was just installed with

`wsl --export [distribution] [save location]`

- In my case that would be

`wsl --export Ubuntu C:\Users\every-day-account\Desktop\Ubuntu.tar`

### On your every-day account

7. Log into your every-day account and run the following in the PowerShell (not as an admin)

`wsl --import [distribution name] [save location] [image for import]`

- The distribution name can be whatever you want to call it. I created a `wsl` folder in my home directory, so I used the following:

`wsl --import Ubuntu C:\Users\every-day-account\wsl C:\Users\every-day-account\Desktop\Ubuntu.tar`

8. Reboot


## WindowsTerminal

1. Windows Terminal is a nice tool, but the Microsoft store is blocked on our computers. Microsoft has a GitHub repository with msixbundle files. Download the latest version from their [release page](https://github.com/microsoft/terminal/releases) and save it to a good location. This will may need to be done on your every-day account.

2. Run PowerShell as Admin while logged into your Admin account and execute the following command:

`DISM.exe /Online /Add-ProvisionedAppxPackage /PackagePath:[path to msixbundle file] /SkipLicense`

- I saved it on my desktop, so I ran:

`DISM.exe /Online /Add-ProvisionedAppxPackage /PackagePath:C:\Users\every-day-account\Desktop\Microsoft.WindowsTerminal_Win10_1.16.10261.0_8wekyb3d8bbwe.msixbundle /SkipLicense`

<!-- `Add-AppxPackage Microsoft.DesktopInstaller_<versionNumber>.msixbundle` will install it on your Admin account, but not your every-day account -->

When logging into your every-day account, Windows Terminal should now be installed and ready to use.
