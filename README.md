# install-idex-w10-wsl

Install IDEX replicator on Windows 10 using powershell and Ubuntu on WSL

Pre-requisites:
      - Windows 10 OS
      - Admin access
      - Powershell
      - WSL- Windows Subsystem for Linux
      - Internet connection
      - if running on virtual Windows enable virtualisation support on your hypervisor
      on mac with Vmware Fusion: https://www.trustedsec.com/blog/running-hyper-v-inside-vmware-fusion/ 

1. Enable WSL and VirtualMachine platform feature from Powershell as admin: 
	a. Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
	b. dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
	c. update wsl kernel to version 2: https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
	https://docs.microsoft.com/en-gb/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package
	d: set wsl version: wsl --set-default-version 2

2. install linux distro (Ubuntu 20.04LTS)
	a: install distro (ubuntu 20.04LTS): https://www.microsoft.com/store/apps/9n6svws3rx71
	or by commandline (slow):  Invoke-WebRequest -Uri https://aka.ms/wslubuntu2004 -OutFile Ubuntu.appx -UseBasicParsing
	install from commandline: Add-AppxPackage .\Ubuntu.appx 
	or when manual downloaded example: Add-AppxPackage C:\Users\PC\Downloads\Ubuntu_2004.2020.424.0_x64.appx
	Download source: https://wiki.ubuntu.com/WSL 
	Start Ununtu, from startmenu, this will initiate the ubuntu setup
	I ran into the following error ‘error 0x80370109’  it was fixed by Installing hyper-V as windows feature.
	Powershell:  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All or DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V
	source: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v
	
	b: set username password for linux distro. 
	https://docs.microsoft.com/nl-nl/windows/wsl/setup/environment#set-up-your-linux-user-info
	- from commandline run: ubuntu
	- username and password will be asked: set you username/password
	
	c. update and upgrade packages: sudo apt update && sudo apt upgrade
	I got an error after entering new credentials ‘the windows subsystem for linux instance has terminated’ I closed the windows and started Ubuntu again from
	startmenu. And I was logged in as root. (no password)

3. install IDEX Staking replicator 
	Follow instructions on https://github.com/idexio/staking-replicator

4. set your firewall
	set your windows firewall to forward port 8081 from you windows host to Ubuntu
