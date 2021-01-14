---
title: 'Windows 7 - QoS Policies not working'
date: 2010-12-12T06:10:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2010/12/windows-7-qos-policies-not-working.html"
---

I've noticed that QoS Policies does not work in Windows 7.  
  
**Solution** (thanks to [xedoc in speedguide.net](http://forums.speedguide.net/showthread.php?274421-Windows-7-resets-DiffServ-(DSCP)-to-0x00&p=2375165#post2375165)):  
  

```
Windows Registry Editor Version 5.00  
  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\QoS]  
"Do not use NLA"="1"
```  

***
  
I configure them using "Group Policy Manager", followingly:  

![](./windows-7-qos-policies-not-working-01.jpg)

And capturing using [WireShark](http://www.wireshark.org/) like this:  

![](./windows-7-qos-policies-not-working-02.jpg)

More about this in: [Wireshark Ask Forum](http://ask.wireshark.org/questions/1188/why-is-dscp-always-0-on-windows-7),  [MSDN QoS Policy](http://technet.microsoft.com/en-us/library/dd919203(WS.10).aspx)