---
layout: post
title: "Embeddable GUIs – A plan for the ultimate software productivity suite"
date: 2019-01-15 11:28 -0500
category: Ideas
---

Something real great about using a framework like Qt is the ability to create “widgets” that are very portable and can be embedded in all sorts of other Qt applications.

An example of this is Escriba, our hybrid Rich-text/Markdown editor. This editor can be embedded in any Qt project you wish to create. Vibrato Notes embeds it.

There are two main benefits from the text-editor widget being separated from Vibrato Notes. First, it’s easier to develop. When a developer wants to add features to it, they don’t have to compile the entire Vibrato Notes application. They just compile Escriba, which is a much smaller program. Another benefit is that the project will catch more interest. It being a general-use text-editor embeddable in any Qt app makes it attractive for all sorts of applications. This enables developers who never have heard of Vibrato Notes – or don’t even care to for that matter – to contribute to Escriba. Anyone contributing to Escriba indirectly (Or directly depending on how you look at it) helps Vibrato Notes become a better piece of software.

Now, let’s say I create a todo-list application. I can make it easily embedable and very flexible. This will allow me to both embed it into Vibrato Notes and create a standalone todo-list application. This could help the software appeal to two audiences – those who want todo-list capabilities in Vibrato Notes and those who just simply want a todo-list app. This could even appeal to a third audience depending on how flexible the app is created: Developers who want todo-list capabilities in their software.

There are a lot of productivity apps to be created; maybe not all of them need to be embed in Vibrato Notes. However, creating all sorts of embeddable widgets and creating helper libraries to add features such as a scripting language can make for a set of apps that are extremely customizable and useful.
