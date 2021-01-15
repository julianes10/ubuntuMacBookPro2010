# ubuntuMacBookPro2010

# Tips ubuntu 20.04

## To enable grub menu list working fine: 
<pre>
root@MacBookPro:/etc/default/grub
GRUB_TERMINAL=console

sudo update-grub
reboot
</pre>
## wifi drivers
search for non-free ones to make it work

## nvidia card driver
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

Alternatively, try this to solve acpi issue with free drivers:s

https://wiki.debian.org/Bumblebee#Installation

sudo apt install bumblebee primus
