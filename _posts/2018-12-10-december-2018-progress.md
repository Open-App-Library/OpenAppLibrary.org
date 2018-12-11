---
layout: post
title: "Vibrato Notes: The Development Progress So Far"
date: 2018-12-10 16:40
summary: The first development update post of Vibrato Notes.
categories: News
media_path: "/images/2018-12-10-update"
---

In this post I would like to cover the current progress of Vibrato Notes.

Creating the first version of this app has taken much longer than I initially thought. It's common to go into software projects thinking that an idea is very easy to implement and then you keep encountering new design problems you hadn't thought of and the scope of the project keeps increasing.

There were a few problems in the beginning of the development of Vibrato Notes that caused me to spend a lot of time, not neccesarily building the core app, but instead building libraries that would be needed for the app. Examples of those include [Markdown Panda](https://gitlab.com/Open-App-Library/markdownpanda) and [QBasicHtmlExporter](https://gitlab.com/Open-App-Library/QBasicHtmlExporter).

[Escriba](https://gitlab.com/Open-App-Library/escriba) is another library I had to spend a decent amount of time on. It is quite important as it is the hybrid text-editor used in the desktop application.

Throughout the experience, I have drastically increased my ability to work with C and C++. It has been a lot of fun even in the most challenging parts, fighting off mysterious segfault after segfault.

**Here is a rough overview of the progress**:

| Component    | Progress                                                     |
| ------------ | ------------------------------------------------------------ |
| Back-end API | Functional, needs slight adjustments.                        |
| Web app      | Close to completion. On hold while I finish the desktop app. |
| Desktop app  | Good progress but a lot to do.                               |
| Mobile app   | Not started.                                                 |

## The journey so far.

The whole project started with me creating a bare-minimal API in Django that provided just enough functionality. After that, I started work on the web app.

However, I took a break developing the web app to move onto the desktop app. I was progressing through the web app at quite a fast pace and that is because working with web technologies can be easy. VueJS in particular helped a lot.

...However, C++ isn't as easy. I was worried I would complete the web app, move onto the desktop app and just completely struggle with it. I like to do the hard things first, saving the easy stuff for last.

C++ (and plain C for MarkdownPanda!) did involve quite a lot of additional learning as I was primarily familiar with languages with garbage collectors.

Working with plain C in particular has improved my documentation-reading skills. There are times where a library has no other documentation other than the code itself and the few comments left within the header files. There are also times where a library that does a specific task does not exist. I needed an HTML to Markdown converter and had to write one myself, with the help of [MyHTML](https://github.com/lexborisov/myhtml).

Qt5 has been an incredibly powerful framework to use. It saves a ton of effort and really makes cross-platform development a breeze. Still, with having to worry about memory management and the header-source-file workflow of C++, it's still not that quick to prototype applications when you are used to being spoiled with web technologies.

I look forward to implementing a scripting language into Vibrato Notes later on. It will allow me to decouple some non-performance-effecting C++ from the project as well as provide the users with a versatile extension system to use. This is a rough idea now - not set in stone - and will be further explored in the future.

![The Desktop app]({{page.media_path}}/desktop.png)

## Desktop App Features

In this section I'll go over a few cool features of the desktop app.

### Hybrid rich-text/markdown editor

You can edit in both rich-text and markdown. Switching between the two is easy! I plan on improving and writing more unit-tests to improve the reliability of the bi-directional conversion.

<video src="{{page.media_path}}/bidirectional.webm" controls>
</video>

### Editing notebooks in a tree-based, hierarchial fashion

<video src="{{page.media_path}}/notebook-tree.webm" controls>
</video>

### Modify the notebook and tags of a note

<video src="{{page.media_path}}/tag-notebook-manipulation.webm" controls>
</video>

### Layout switching

There are three different layout presets. The default one, one that hides the leftmost sidebar, and one that hides both sidebars, leaving you with the text editor.

<video src="{{page.media_path}}/layouts.webm" controls>
</video>

### Fairly efficient note filtering, allowing you to quickly navigate through hundreds of notes

<video src="{{page.media_path}}/filtering.webm" controls>
</video>

---

![Web app screenshot]({{page.media_path}}/webapp.png)

## Web App

The web app is pretty - indeed - however you may notice it lacks a few features of the desktop app. Like I mentioned earlier, I took a break from the web app to build the desktop app. I haven't touched the code of the web app for a few month and plan to return to it after the desktop app is complete.

Here is a video I took of it a while ago:

<blockquote class="reddit-card" data-card-created="1544486919"><a href="https://www.reddit.com/r/UsabilityPorn/comments/99j657/kde_a_notetaking_app_im_building_emacs_and_my/">[KDE] A note-taking app I'm building, Emacs, and my minimal KDE tweaks</a> from <a href="http://www.reddit.com/r/UsabilityPorn">r/UsabilityPorn</a></blockquote>
<script async src="//embed.redditmedia.com/widgets/platform.js" charset="UTF-8"></script>

## Weekly updates

Something new I will be doing is creating a new post every week on OpenAppLibrary.org detailing progress made in the app.

Thanks for reading!
