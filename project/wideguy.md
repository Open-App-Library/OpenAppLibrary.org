---
layout: project
title: WideGuy
subtitle: A Linux tool that makes multi-monitor gaming easy. (A GUI tool for Xinerama)
icon: /images/wideguy/icon.svg
downloads:
  - title: AppImage (v.0.5.1)
    url: https://github.com/Open-App-Library/WideGuy-Releases/releases/download/0.5.1/WideGuy-x86_64.AppImage
    help: https://itsfoss.com/use-appimage-linux/
  - title: Source Code
    url: https://gitlab.com/Open-App-Library/WideGuy
---

Right now you might have a three-monitor setup. You're aching to get that immersive extra-wide-screen experience but to your frustration, your game only launches on one monitor.

Thanks to an awesome feature of Xorg called Xinerama, multi-monitor gaming is very possible.

...But enabling it could be difficult. That was my inspiration for creating this little application.

## Basic Usage

![WideGuy Screenshot](/images/wideguy/screenshot.png)

If you or your operating system has already set up an `/etc/X11/xorg.conf` file, this app will do it's job right out of the box.

The button in the middle of the app will say "Enable Wide Mode" or "Disable Wide Mode" depending on whether or not you have Xinerama enabled. You can click the button to toggle between the two modes.

Here is what happens when you click the button:

- Your xorg.conf file is read and Xinerama is enabled or disabled.
- You are prompted to enter your root password
- The xorg.conf is saved. If this is your first time running, a backup file is created named `/etc/X11/xorg.conf.wideguy.backup`.
- Xorg is now reloaded. This is done by restarting your display manager. The application tries to be smart and guess what display manager you are using. You can set a custom command to restart Xorg / your display manager in the [settings](#settings).

## Settings

![WideGuy Settings](/images/wideguy/settings.png)

WideGuy provides very basic but useful settings, accessible by the "WideGuy" menu.

**Confirm changes to Xorg config**: Gives you a popup textbox before saving the Xorg config. You have the option to accept or decline the change.

**xorg.conf location**: Choose where your xorg.conf is located. In most cases you shouldn't change this. The purpose of this option is to locate the file where your `Section "ServerLayout"` is.

**Command to restart xorg**: This is the command that will restart Xorg. More accurately, this is the command that will restart your display manager. WideGuy tries to automatically detect your display manager and output a proper command. In this case, it successfully determined that my display manager was SDDM, the typical display manager used on KDE distribution.

## Advanced Menu

![WideGuy Advanced Menu](/images/wideguy/advanced.png)

There are a few different Advanced options at your disposal.

**Restore Backup**: Restores your WideGuy xorg.conf backup file if one exists. The backup is typically located at `/etc/X11/xorg.conf.wideguy.backup`.

**Force Wide Mode / Force Regular Mode**: These functions are a way to manually enable or disable Xinerama. Note that it will not restart your display manager / Xorg.

**Restart Xorg**: This will manually restart Xorg / your display manager.

## Creating an xorg.conf

If you don't have an xorg.conf, you will be greeted by a popup providing you with some information on creating one.

<p>Here are some resources on creating/generating an xorg.conf:</p>

<ul>
  <li><a target="_blank" href="https://wiki.ubuntu.com/X/Config">Ubuntu</a></li>
  <li><a target="_blank" href="https://askubuntu.com/questions/4662/where-is-the-x-org-config-file-how-do-i-configure-x-there">Ubuntu #2</a></li>
  <li><a target="_blank" href="https://www.youtube.com/watch?v=ZA-pQqN04as">Ubuntu #3</a></li>
  <li><a target="_blank" href="https://wiki.debian.org/Xorg#Edit_xorg.conf">Debian</a></li>
  <li><a target="_blank" href="https://fedoraproject.org/wiki/How_to_create_xorg.conf">Fedora</a></li>
  <li><a target="_blank" href="https://wiki.archlinux.org/index.php/xorg#Using_xorg.conf">Arch</a></li>
</ul>

<p>Note that if you have an Nvidia card and the nvidia-settings program, you can press the "save to file" button to create an xorg.conf.</p>

<p>If your Xorg configuration is in a special location you may manually set it in the WideGuy settings. Note that the Xorg configuration you provide should have a ServerLayout section. If one does not exist, WideGuy will prompt you to add a basic ServerLayout section.</p>


---

I hope this app makes your life easier! If it does, feel free to [buy me a root beer](https://liberapay.com/openapplibrary/). Cheers.
