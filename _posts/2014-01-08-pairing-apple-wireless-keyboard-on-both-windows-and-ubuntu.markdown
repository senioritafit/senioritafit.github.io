---
layout: note
title: Pairing Apple Wireless Keyboard on both Windows and Ubuntu
date: 2014-01-08
categories: note windows linux keyboard
---

 1. Pair the keyboard with Windows.

 2. Install [PsExec v2.1](http://technet.microsoft.com/en-us/sysinternals/bb897553.aspx) and run the PsExec program:

	```
	PSexec -i -d -s C:\Windows\regedit.exe
	```

 3. Copy the key from this file and record the data value.

	```
	HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\services\BTHPORT\Parameters\Keys\aaaaaaaa\bbbbbbbb
	```

 4. In Linux (Ubuntu 13.04), replace the values in the file with the data value obtained from Windows.

	```
	/var/lib/bluetooth/AA:11:11:11:11:11/linkkeys
	```
