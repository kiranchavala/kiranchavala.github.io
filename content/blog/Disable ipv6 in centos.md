+++
author = "kiran"
categories = ["Centos"]
date = "2020-08-13"
description = "disable ipv6"
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Disabling ipv6 in centos"
type = "post"

+++

1. To verify if IPv6 is enabled or not, execute

#ifconfig -a | grep inet6

inet6 fe80::211:aff:fe6a:9de4  prefixlen 64  scopeid 0x20

inet6 ::1  prefixlen 128  scopeid 0x10[host]

2. Disable Ipv6 in kernel module (requires reboot)

Edit /etc/default/grub

add ipv6.disable=1 in line GRUB_CMDLINE_LINUX, e.g

cat /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="ipv6.disable=1 crashkernel=auto rhgb quiet"
GRUB_DISABLE_RECOVERY="true"

3. Regenerate a GRUB configuration file and overwrite existing one

grub2-mkconfig -o /boot/grub2/grub.cfg

4. Restart system and verify no line “inet6” in “ip addr show” command output

shutdown -r now

