##Disable IPv6 using Sysctl
````bash
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1
````
However, this only temporarily disables IPv6. The next time your system boots, IPv6 will be enabled again.

One method to make this option persist is modifying /etc/sysctl.conf. I’ll be using vim to edit the file, but you can use any editor you like. Make sure you have administrator rights (use sudo).<br>
Add the following lines to the file:
````bash
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1
````
For the settings to take effect use:
````bash
sudo sysctl -p
````
If IPv6 is still enabled after rebooting, you must create (with root privileges) the file /etc/rc.local and fill it with:
````bash
#!/bin/bash
# /etc/rc.local

/etc/sysctl.d
/etc/init.d/procps restart

exit 0
````
Now use chmod command to make the file executable:
````bash
sudo chmod 755 /etc/rc.local
````
##Disable IPv6 using Sysctl

An alternative method is to configure GRUB to pass kernel parameters at boot time. You’ll have to edit /etc/default/grub. Once again, make sure you have administrator privileges.
Now you need to modify GRUB_CMDLINE_LINUX_DEFAULT and GRUB_CMDLINE_LINUX to disable IPv6 on boot:
````bash
GRUB_CMDLINE_LINUX_DEFAULT="<your parameters> ipv6.disable=1"
GRUB_CMDLINE_LINUX="ipv6.disable=1"
````
Save the file and run the update-grub command:
````bash
sudo update-grub
````
The settings should now persist on reboot.