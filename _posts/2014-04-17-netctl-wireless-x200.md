---
layout: note
title: Netctl wireless on x200
date: 2014-04-17
updated: 2014-05-09
categories: note postgres linux upgrade
---

Paraphrasing from: [https://wiki.archlinux.org/index.php/netctl](https://wiki.archlinux.org/index.php/netctl)

I had issues with wireless on my Lenovo X200 netctl profiles. Installing a different dhcp client and telling the profile to use it fixed my problem.

```sh
pacman -S dhclient
echo -e "ForceConnect=yes\nDHCPClient='dhclient'" >> /etc/netctl/<yourProfileName>
netctl start <yourProfileName>
```

Then check with:

```sh
iw dev <interfaceName> link
```

## Update

After reading the man page for another unrelated issue, it's recommended that you *do not* use the force connect option. Try it without the option first.
