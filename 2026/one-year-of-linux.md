---
status: draft
---

# One year of Linux

I switched from Windows to Linux a year ago, I can now reflect on how this went, and what not to do.

If you are stuck in Windows and desperate to get out, and don't bother to read the rest, trust me and install [Fedora KDE](https://fedoraproject.org/kde/), never ever try Ubuntu or GNOME based desktops first if switching from Windows. When you are switching between two things, it is much easier if the one you switch to is maximally familiar, you don't get that with GNOME, only KDE succeeds here.

First misstep I made was to try Arch Linux. I quickly found out it is too customizable, I mostly spent writing scripts how to bundle my perfect Arch Linux. I got pretty far though, I was briefly running Hyper and very light setup. I made elaborate scripts which could build Arch Linux distro just for me, chasing that reproducible setup that sounds so cool. Reproducibility is red-herring for software engineers, because it can be so satisfying when it works. But that is not something you should tinker as a first step when trying to switch to Linux, and you are not running Linux in the first place. Eventually I got tired of customizing all the things and booted back to Windows to do real work.

Then I saw that Fedora was releasing Fedora 43, I thought what better way than to try that. It was immediately better fit, but I did another error, I installed GNOME version of Fedora. It reminded me of Ubuntu, and I had tried it years past, but it brought back all the small anoyances I had forgotten. GNOME looks amazing, but that is decieving because all the small things are too alien for those switching from Windows.

I desperatedly wanted replace Windows so I spent weeks customizing GNOME to mostly look like Windows, but it became extremly brittle. Simple things like mouse scrollwheel, taskbar, tray, Nautilus, missing titlebars, and so on was all fighting me. I even vibe-forked Nautilus to "fix it", so badly I wanted things to work. One could do many things with extensions, but those made GNOME even more buggier, in the end it was not worth it.

Finally I rediscovered KDE. I had tried it long long time ago, when I had no reason to switch to Linux, but just to test things around. I didn't want to reinstall my Fedora setup, after all most of my terminal setup would transfer if I could just install KDE on top of Fedora Workstation. It is not recommended way, but you can just install KDE with dnf on top of GNOME edition of Fedora. It installed smoothly and this is the setup I still run. Yes my setup is not ideal, it even starts still with GNOME's sddm but I only see that briefly.

This wouldn't be a post without some sales speech for KDE, here is few things that are great:

1. KDE Settings application is amazing. Everything I'd ever want is in one application, organized to single sidebar. Windows made awful mess by switching out from Control Panel, everything became highly non-discoverable settings wise.

2. Taskbar is very similar as in Windows, but you can also put it vertical, and configure it to your liking. One of the most annoying things about Windows 11 is that they removed ability to put it vertically. KDE can also pin taskbar buttons, Google Chrome's installed applications appear to it like you'd expect, tray is sensible, by all accounts it is very similar to Windows.

3. KDE's titlebars are great, there is so much similarity with old Windows. What I want from titlebars is that they are consistent and applications don't get to shovel garbage to titlebars, they are for me to configure.

4. KDE Dolphin is good file manager. You can configure it to your liking, and it will behave a lot like the one Windows used to have. 

5. Window management is just better. KDE has snapping, that is very similar to Windows, you can additionally set rules, where each window will appear etc. Even though I use virtual desktops heavily, there are some windows I want to be placed precisely and it is possible without hacks.

6. Animations are configurable. I always wanted to configure animation speeds in Windows, and in KDE I can. Now if I log in to Windows everything feels slow, because the default animations are slow. With KDE animation speed and styles are configurable, although [KDE Plasma 6.6 had a regression which is not yet fixed](https://bugs.kde.org/show_bug.cgi?id=521639), but at least there is workaround via configuration file.

7. Other small details done right in KDE:
    - By default double clicking on the top or bottom resize handle and it will vertically maximize window. 
    - You can configure KDE to close window by double clicking on the icon on left of your titlebar, this used to be a thing in Windows too, before every app started to reimagine what titlebars are.
    - 

Incidentally, all of the above points, and their equivalents in GNOME are also what is wrong with GNOME. They have one-size-fit-for-all kind of thinking and it is fine for those who've gotten used to it but I don't.