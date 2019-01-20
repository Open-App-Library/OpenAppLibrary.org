---
layout: page
title: About
permalink: /about/
---

**The Open App Library Project's goal is to create a sustainable open-source software company** - One that allows us to donate to other open-source projects that rely on donations.

The first app and primary focus of the Open App Library will be [Vibrato Notes](https://vibrato.app), a powerful cross-platform note-taking application. It will operate under a SaaS business model and charge an estimated $10 a month for its cloud note-syncing service. You will have the option of self-hosting at the expense of paying for your own server and providing your own server maintenance.

5% of sales go to open-source projects and foundations.

<span id="about-page-optin-heading">Get notified when Vibrato Notes launches!</span>
{% include email-signup.html %}

## Freedom over Price

When talking about free software it is important to understand the difference between "libre" and "gratis", two latin words that offer distinctions that the English language cannot.

- "Libre" means free; Free as in freedom.
- "Gratis" means free; Free as in price.

The belief of this project is that 'libre' software is the holy grail - the only aspect that truly matters is having your code public and using a fair license that promotes software freedom. (See the [GNU General Public License](https://en.wikipedia.org/wiki/GNU_General_Public_License))

There are several expected benefits to implementing a business model into open-source software

- More predictable funding
- Faster growth
- Developers of popular projects have a greater chance of earning a full-time income
- Full-time developers will be able to put in more time to the project
- Larger and more predictable funding means you are able to purchase more resources, services, and equipment to help your project.

## Stallman's four principals

Having your code publicly available does not cover the entire spectrum of software freedom. Richard Stallman has created [four essential principals](https://www.gnu.org/philosophy/free-sw.en.html) to define free (libre) software.

1. The freedom to run the program as you wish, for any purpose.
2. The freedom to study how the program works, and change it so it does your computing as you wish. Access to the source code is a precondition for this.
3. The freedom to redistribute copies so you can help others.
4. The freedom to distribute copies of your modified versions to others. By doing this you can give the whole community a chance to benefit from your changes. Access to the source code is a precondition for this.

## Different ways to implement an open-source business model

### SaaS (Software as a Service)

Vibrato Notes will follow an excellent open-source business model. All of the apps will be free whether you are on desktop or mobile. You will not need an account to use them.

However, we will offer a very convenient and seamless cloud syncing service, similar to Evernote, at a reasonable price.

It will save the user from spending time and money maintaining a self-hosted Vibrato Notes instance and also give them the peace of mind knowing that their data was encrypted on the client side (We can't read your notes if we wanted to) and they are funding us to provide a reliable & featureful service.

### Paid apps

The Mac App Store shows how much potential there is for indie developers to make money selling paid software. The prices are generally from $4 to $40.

If a piece of software solves my problems better than what is available and has a reasonable price, I have no problem paying money for it.

Now, the big question. Why would anyone pay money for software that they could get for free?

To answer that, we have to go over what "get" entails.

If you have your code on Github, "getting your software for free" means that other people have to either clone your repository or download it as a zip and then compile everything. After the program is compiled they then would have to package it in some way, shape or form or move it to the proper system location.

That's not an easy task that every person could do. Not only that, they also need to manually update and recompile the application.

This offers you the ability to sell the executable and leave the source code open.

There is one clear flaw though. What is stopping a fellow developer from killing your profitability by distributing pre-compiled executables for free?

Well, you could write this off in the hope that people won't trust that person and that the person could be slow distributing the updates. You could also hope that after people try the software and fall in love with it they will buy your version.

One idea that could prevent this is creating a license that forbids users from freely distributing your application for the purpose of bypassing payment.

This idea gets challenging when you want to forbid people from "pirating" your software as described above but you also want to enable people to fork your work and create their own version.

It also might violate Stallman's third principal mentioned earlier.

Due to the complications of that special license idea, I believe the best way is to offer additional incentives that are impossible to pirate. A few examples are:

- Product support
- Cloud syncing
- Private forum

## Does everything have to cost money?

Not at all. It's very likely that the Open App Library will produce certain utilities free of cost.

One of those apps in Particular is [MiniBoard](https://gitlab.com/Open-App-Library/MiniBoard). It's currently written in Gtk+3 but will likely be ported to Qt5. It is a free-to-use whiteboard / primitive painting app with touchscreen / tablet support. It will also likely be the way that we implement drawing into Vibrato Notes later down the road.
