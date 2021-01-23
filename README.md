# ubuntuMacBookPro2010

# Tips ubuntu 20.04

## To enable grub menu list working fine: 
<pre>
root@MacBookPro:/etc/default/grub
GRUB_TERMINAL=console

sudo update-grub
reboot
</pre>

## Drivers

It should be as simple as:

sudo ubuntu-drivers autoinstall

Some issues with nvidia...
...
Configurando nvidia-340 (340.108-0ubuntu5.20.04.1) ...

Building for 5.8.0-38-generic
Building for architecture x86_64
Building initial module for 5.8.0-38-generic
This system doesn't support Secure Boot
Secure Boot not enabled on this system.
Done.



### wifi drivers
search for non-free ones to make it work

### nvidia card driver
* non-free nvidea was great until kernel 5.8, they discontinue the support and kernel fails at boot
* noveau are the default option but has an dummy behaviour with acpi, suspend takes more than 5 or 10 minutes, most of the times you have to force a shutdown pusshing the button. So it is preferable ask for non suspend anytime neither when switch the lid. 
To avoid suspend when lid, so ignore the lid switch:
<pre>
root@MacBookPro:/etc/default# cat /etc/systemd/logind.conf | grep -i lid
#HandleLidSwitch=suspend
HandleLidSwitch=ignore
#HandleLidSwitchExternalPower=suspend
#HandleLidSwitchDocked=ignore
#LidSwitchIgnoreInhibited=yes
</pre>


Bumblebee is not helping neither
https://wiki.debian.org/Bumblebee#Installation

sudo apt install bumblebee primus


<pre>
omega@MacBookPro:~$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:17.0/0000:04:00.0 ==
modalias : pci:v000010DEd000008A0sv0000106Bsd000000C2bc03sc00i00
vendor   : NVIDIA Corporation
model    : MCP89 [GeForce 320M]
driver   : nvidia-340 - distro non-free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin

== /sys/devices/pci0000:00/0000:00:15.0/0000:02:00.0 ==
modalias : pci:v000014E4d0000432Bsv0000106Bsd0000008Dbc02sc80i00
vendor   : Broadcom Inc. and subsidiaries
model    : BCM4322 802.11a/b/g/n Wireless LAN Controller (AirPort Extreme)
driver   : bcmwl-kernel-source - third-party free
</pre>

this combinaton is working ok but not suspending is a pain on the neck
