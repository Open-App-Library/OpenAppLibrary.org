---
layout: post
title: "Building an Open-Source Evernote Alternative: January 2019 Update"
date: 2019-01-22 06:30 -0500
category: News
media_path: "/images/2019-01-21-progress"
---

<div class="video-responsive">
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/e7iCC8Q2fSg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## The Desktop App

*Demo video: This video shows various features of the desktop app. Music by Kevin MacLeod (incompetech.com) under Creative Commons 3.0. Please excuse any flicking in the recording. I should've used SimpleScreenRecorder to avoid that problem.*

There have been many improvements made in the desktop app. Let's go over them.

### Big performance upgrade

One change that I am very excited about is not actually noticeable - which is a good thing! The note list widget used to use a custom widget for each note in the list - via Qt's [setIndexWidget](http://doc.qt.io/qt-5/qabstractitemview.html#setIndexWidget) function.

This wouldn't cause a major problem until you have hundreds of notes. At that point the app would use more memory (Still way, way less than an Electron app following best practices, haha.) and you would notice a delay when switching between different filtered note views - "All Notes", "Favorited", "Notebooks", "Tags".

Thanks to the helpful people at the [Qt forum](https://forum.qt.io) I found out that it wouldn't be too hard to migrate my code to a much more efficient display model - By sub-classing `QStyledItemDelegate`.

Now, instead of creating custom widgets which take time initializing, the note list items are painted using **QPainter**, which "performs low-level painting on widgets and other paint devices.", according to [the docs](http://doc.qt.io/qt-5/qpainter.html).

[Commit c139b824](https://github.com/Open-App-Library/vibrato-notes-desktop/commit/c139b8244d496e7000bd0bf11ae026b77cecdccc)

### A C++ API to interact with the back-end API

[Qt-Vibrato-Cloud-API-Library](https://github.com/Open-App-Library/Qt-Vibrato-Cloud-API) was created to provide a C++ API for connecting to the [Note Sync Server](https://github.com/Open-App-Library/Vibrato-Notes-Back-End).

It is essentially complete minus the code for client-side encryption and decryption. That will come soon.

Now I am focusing on using the Qt-Vibrato-Cloud-API-Library in conjunction with the desktop app to sync notes to the cloud.

## The back-end API / sync-server has a lot more functionality

A ton of progress was made on [the back-end](https://github.com/Open-App-Library/Vibrato-notes-Back-End). When the server runs, there is now API documentation available at `{SERVER_URL}/docs`.

Thanks to the [Django Rest Framework](https://django-rest-framework.org/) it was quite easy to add useful features to the REST API such as sorting & filtering - As an example, you can sort by notes from oldest-to-newest using the URL `{SERVER_URL}/notes?ordering=date_created`.

The supported authentication types are token authentication and OAuth2. You could generate a token for your account via the URL, `{SERVER_URL}/users/login` and use HTTP Basic Authentication with your user credentials. Tokens last for 30 days. You also can use the URL `{SERVER_URL}/users/logoutall` to delete all of your tokens.

Various changes were made to the [database model](https://github.com/Open-App-Library/Vibrato-notes-Back-End/blob/master/notes/models.py).

`sync_hash` was added to provide a unique "fingerprint" to all of your notes, notebooks and tags. Why not just use the database's built-in `id` field you might ask? It is very easy to run into `id` conflicts when you have multiple devices that can create notes offline, saving to a SQLite database, and then sending them up to the cloud eventually. The back-end API gives notes, notebooks and tags a unique fingerprint, called a `sync_hash` which is just a [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier). With this, you can easily check if an object exists in the cloud.

Currently, the `sync_hash` is read-only and is only set by the back-end server when objects are initially synced to the cloud. But perhaps there are benefits to generating these on the clients too and also using these as "IDs" in foreignkeys as well. This could potentially improve reliability and require less hand-holding (additional code) to sync objects.

The sync server will use Postgres as a database back-end by default. It's currently using SQLite just for ease of development purposes but that will be changed. However, the desktop and mobile app will still use SQLite as I believe it is the right tool for the job for that particular case.

The `row` column in the Notebook table allows you to specify a custom ordering of your notebooks. The back-end will also normalize whatever row number you provide to keep things neat & simple. Here's a quick little text diagram that shows how rows are represented. They represent the current index number of the current hierarchy level.

```
0 - Recipes
1 - Journaling
2 - CompSci
0   - Python
1   - C++
3 Fitness Tracking
```

Qt uses the same row concept for their TreeModel. Here is their diagram to explain the concept (Ignore the root item):

![Tree diagram with row concept]({{page.media_path}}/qttree.png)

## The status of the web app?

The web app will be put on hold for now as the desktop app and back-end server are top priority.

Likely, the next big thing I will be working on is the mobile app, created in Qt.

The web app has a lot of progress already but I suspect the majority of the users will use the desktop and mobile app, only occasionally using the web app. For that reason it is on hold - but not forgotten or abandoned.

## Thank you for the support!

I have received a good amount of encouragement from reddit and greatly appreciate it. Please [sign up for the waiting list](https://vibrato.app/) to get a notification as soon as the app is released if you are interested.

## Upcoming project goals

- Connecting the desktop app to the sync server.
- Ironing out text-editor bugs and adding a more complete feature set to it.
- Client-side encryption!
- Launching a pre-alpha program.
- Plenty of usability and design tweaks.
- Creating the mobile application.
- Implement the plugin system, using a lisp-like scripting language - likely Chicken Scheme.
- Implementing image & file upload support.

## Useful links

- [About the Open App Library Project](https://openapplibrary.org/about/)
- [Vibrato Notes website](https://vibrato.app)
- [Feature Requests](https://features.vibrato.aapp/)
- [Telegram Group](https://t.me/joinchat/FslNFBYI88kLFXU5TJFJag)
- [Source Code](https://github.com/Open-App-Library)
