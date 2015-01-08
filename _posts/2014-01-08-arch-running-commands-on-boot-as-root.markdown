---
layout: note
title: Arch - Running commands on boot as root
date: 2014-01-08
categories: arch linux
---

Taken from [this arch linux post](https://bbs.archlinux.org/viewtopic.php?pid=1203583):

> Another, less general, solution. Create a /usr/local/sbin/rc.local script with the following content:
>
>     #!/bin/bash
>     #
>     # /usr/local/sbin/rc.local: Local multi-user startup script.
>     hdparm -B254 /dev/sda
>
> You can add whatever you want to be run at boot with root privileges.
> Make it executable:
>
>
>     chmod +x /usr/local/sbin/rc.local
>
> Create a service file for `rc.local` in `/etc/systemd/system/rc-local.service` with the following content:
>
>
>     [Unit]
>     Description=/etc/rc.local Compatibility
>     ConditionFileIsExecutable=/usr/local/sbin/rc.local
>
>     [Service]
>     Type=oneshot
>     ExecStart=/usr/local/sbin/rc.local
>     TimeoutSec=0
>     StandardOutput=tty
>     RemainAfterExit=yes
>     SysVStartPriority=99
>
>     [Install]
>     WantedBy=multi-user.target
>
>
> Enable it:
>
>      #systemctl enable rc-local
>
> Reboot.
