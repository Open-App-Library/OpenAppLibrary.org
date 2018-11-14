---
layout: post
title: A Guide to Using Icon Themes in Qt on All Platforms
date: 2018-11-14 11:03 -0500
summary: Icon themes can be a slightly confusing topic in Qt. In this post you will learn how to create icon themes that are cross-platform."
categories: Dev-Tutorials
---

This guide will attempt to demystify the usage of icon themes in Qt applications.

Icon themes are a standard on the Linux desktop but seem to be a foreign concept on Mac and Windows. Lucky for us, Qt has integrated icon themes quite seamlessly no matter what operating system you are using.

To see a working example of icon theme usage that uses a variety of techniques from this article, check out our "[Qt5 Cross-Platform Icon Themes](https://gitlab.com/open-app-library-education/qt5-cross-platform-icon-themes)" repo.

## What is an "icon theme"?

FreeDesktop.org created [the spec](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html) on how icon themes should work in free software desktop environments.

They define an icon theme as the following:

> An icon theme is a set of icons that share a common look and feel. The user can then select the icon theme that they want to use, and all applications will use icons from the theme.

## Adding your own icons to the default theme

An easy way to add "cross-platform support" is to:

**1.)** create a folder in your project. (ex. "custom-icons")

**2.)** Add all of your icons.

**3.)** Use the following code to define a fallback icon search pack:

```c++
QIcon::setFallbackSearchPaths(QIcon::fallbackSearchPaths() << ":custom-icons");
```

**4.)** Create a new resources and add your custom icons. Your qrc file's structure should look similar to the following:

![QRC file structure for custom icons](/images/qt5-icons/custom-icons-structure.png)

Now, you can reference any icons in that folder by their filename (minus the file extension). So, in the example of the above screenshot, I would reference the icon as "open-app-library".

To reference the icons, you can either use Qt Designer or enter it programatically.

Here is how I changed a button's icon from [the example repo](https://gitlab.com/open-app-library-education/qt5-cross-platform-icon-themes/blob/master/main.cpp):

```c++
b2->setIcon( QIcon::fromTheme("open-app-library") );
```

If it is important to you that the icons should first try to obey the user's system icons, please make sure to follow [the naming conventions defined by FreeDesktop.org](https://standards.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html). However, if your icon is something truly unique (Like the Open App Library logo I used in this example) you can of course deviate from the specification.

## Configuring a new icon theme in Qt

You might want to completely overwrite the system icon theme and use your own.

You could either create your icon theme from scratch or use the [many existing themes](https://www.gnome-look.org/browse/cat/132/). I personally like [KDE's Breeze icons](https://github.com/KDE/breeze-icons) and [Elementary OS's icons](https://github.com/elementary/icons).

Be aware that not all icon themes include every single icon detailed in the FreeDesktop specification. I've found that KDE's Breeze icons contain the widest selection of icons - I believe they even offer additional icons outside of the specification.

### How icon themes work

Here is the file structure of a very minimal icon theme:

```
└── my-theme/
  └── actions/
    └── 16/
      └── hello-world.png
    └── 24/
      └── hello-world.png
    └── index.theme
```

It could be even simpler than that! (Note that this structure, while it works, deviates from the specification.)

```
└── my-theme/
  └── my-special-ui-icons
    └── hello-world.png
  └── index.theme
```

The most important file is that index.theme. Here is an example of what an index.theme may look like:

```
[Icon Theme]
Name=My Theme
Comment=An example icon theme

[actions/16]
Size=16
Context=Actions
Type=Fixed

[actions/24]
Size=24
Context=Actions
Type=Fixed
```

There are all sorts of things you could do in this index.theme file. You could even inherit icons from another theme! Once again, to learn more about how this all works, check out [the official specification](https://standards.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html).

### Where does Qt search for icon themes?

Now that we have either downloaded an icon pack or have created our own, how can we actually load it?

First, let's figure out where Qt is searching for icons. Run the following C++ code (Make sure to include QIcon and QDebug):

```c++
qDebug() << QIcon::themeSearchPaths();
```

Depending on your operating system, you will get different output. Here are the different paths the command returned for me:

- /home/doug/.icons
- /var/lib/flatpak/exports/share/icons
- /usr/share/icons
- :/icons

What's important to know is that while the theme search paths will vary from operating system to operating system, the `:icons/` resource path will always be present.

This is where we will place our icon paths.

### Adding the icon pack as a resource

If you're in Qt Creator, the process is quite painless. After you create a new resource file, right click on it and choose "Add existing directory".

Now, it might be tempting to add EVERY file from your icon pack but that is not the most efficient way.

Instead, only add the `index.theme` and icons that you plan on using.

For this example project, I decided to use [the Zafiro](https://www.opendesktop.org/p/1209330/) icon pack. Here is what my resources file structure looks like after adding the one icon I wanted:

![Zafiro icon pack resource structure](/images/qt5-icons/zafiro-structure.png)

In case you want to see what my Qt resource file looks like after adding Zafiro, here it is:

```xml
<RCC>
    <qresource prefix="/">
        <file>icons/zafiro/index.theme</file>
        <file>icons/zafiro/places/48/folder-alt.svg</file>
    </qresource>
</RCC>

```

### Loading the icon theme programatically

There very well may be a way to do this directly in Qt Designer but I have not yet found it.

Here is how you would load your icon theme in C++:

```c++
QIcon::setThemeName( "zafiro" );
```

Easy peasy!

**The result**:

- Button 1 is showing Zafiro's folder-alt icon.
- Button 2 is showing the custom open-app-library icon.

![The Result](/images/qt5-icons/result.png)

## Did I miss anything about icon packs?

Hope you have enjoyed this article. If you have any further questions or have any ideas to improve this guide, don't hesitate to drop a comment below.

You may also edit this page by clicking the "Edit this page" button below and submitting a pull request.
