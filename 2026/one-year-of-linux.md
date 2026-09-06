---
status: draft
---

# One year of Linux

I switched from Windows to Linux a year ago, I can now reflect on how this went, and what not to do.

If you are stuck in Windows and desperate to get out, and don't bother to read the rest, trust me and install [Fedora KDE](https://fedoraproject.org/kde/), do not try Ubuntu or GNOME-based desktops first if switching from Windows. When you are switching between two things, it is much easier if the one you switch to is maximally familiar, you don't get that with GNOME, only KDE succeeds here.

First misstep I made was to try Arch Linux. I quickly found out it is too customizable, I mostly spent writing scripts how to bundle my perfect Arch Linux. I got pretty far though, I was briefly running Hyper and a very light setup. I made elaborate scripts which could build Arch Linux distro just for me, chasing that reproducible setup that sounds so cool. Reproducibility is a red herring for software engineers, because it can be so satisfying when it works. But that is not something you should tinker with as a first step when trying to switch to Linux, and you are not running Linux in the first place. Eventually I got tired of customizing all the things and booted back to Windows to do real work.

Then I saw that Fedora was releasing Fedora 43, I thought what better way than to try that. It was immediately a better fit, but I made another error, I installed the GNOME version of Fedora. It reminded me of Ubuntu, which I had tried in years past. Soon enough it brought back all the small annoyances I had forgotten. GNOME looks amazing, it looks polished with smooth animations, but that is deceiving because all the small things are too alien for those switching from Windows.

I desperately wanted to replace Windows so I spent weeks customizing GNOME to mostly look like Windows, but it became extremely brittle. Simple things like mouse scroll wheel, taskbar, tray, Nautilus, missing titlebars, and so on were all fighting me. I even vibe-forked Nautilus to "fix it", so badly I wanted things to work. One could do many things with extensions, but those made GNOME very brittle, in the end it was not worth it.

Finally I rediscovered KDE. I had tried it a long, long time ago, when I had no reason to switch to Linux. I didn't want to reinstall my Fedora setup, after all most of my terminal setup would transfer if I could just install KDE on top of Fedora Workstation. It is not the recommended way, but you can just install KDE with dnf on top of the GNOME edition of Fedora. It installed smoothly and this is the setup I still run. Yes my setup is not ideal, it even starts still with GNOME's sddm but I only see that briefly.

This wouldn't be a post without some sales speech for KDE, here are a few things that are great:

1. KDE Settings application is amazing. Everything I'd ever want is in one application, organized into a single sidebar. Windows made an awful mess by switching out from Control Panel, everything became highly non-discoverable settings-wise.

2. Taskbar is very similar to Windows, but you can also put it vertically, and configure it to your liking. One of the most annoying things about Windows 11 is that they removed the ability to put it vertically. KDE can also pin taskbar buttons, Google Chrome's installed applications appear to it like you'd expect, tray is sensible, by all accounts it is very similar to Windows.

3. KDE's titlebars are great, there is so much similarity with old Windows. What I want from titlebars is that they are consistent and applications don't get to shovel garbage to titlebars, they are for me to configure.

4. KDE Dolphin is a good file manager. You can configure it to your liking, and it will behave a lot like the one Windows used to have.

5. Window management is just better. KDE has snapping, which is very similar to Windows, you can additionally set rules, such as where each window will appear. Even though I use virtual desktops heavily, there are some windows I want to be placed precisely and it is possible without hacks.

6. Animations are configurable. I always wanted to configure animation speeds in Windows, and in KDE I can. With KDE animation speed and styles are configurable, although [KDE Plasma 6.6 had a regression which is not yet fixed](https://bugs.kde.org/show_bug.cgi?id=521639), but at least there is a workaround via a configuration file.

7. Other small details done right in KDE:
    - By default double-clicking on the top or bottom resize handle will vertically maximize the window.
    - You can configure KDE to close a window by double-clicking on the icon on the left of your titlebar, this used to be a thing in Windows too, before every app started to reimagine what titlebars are.
