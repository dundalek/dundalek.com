---
title: Assistant - Graphical Command Shell
---

[Assistant](https://github.com/29decibel/assistant) allows you to run commands. It displays results as cards, you can show them as grid, list or markdown. It is like a command-line shell which displays results graphically.

![Assitant commands](../img/assistant.png)

Assitant consists of two main parts: processors/dispatchers and cards.

**Processors** take text commands and return results by putting them into the result [channel](http://clojure.com/blog/2013/06/28/clojure-core-async-channels.html). Processors get dispatched by a command name which is the first keyword entered. The result which is put into the channel has the content and information which card to use for display. Processors get registered into the system using `register-dispatcher` function.

**Cards** are Om components that display results. There are several built-in cards: `image-list-card`, `list-card`, `markdown-card` and `info-card`. You can add your own card using `register-card` function. You can also add custom CSS using `register-css`.

Assistant is written in ClojureScript and is very extensible. It uses [NW.js](http://nwjs.io/) (previously known as node-webkit) to run as a desktop application.
