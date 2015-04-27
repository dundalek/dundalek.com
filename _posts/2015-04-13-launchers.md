---
title: Launchers Digest - summary of various projects
---

## Synapse

[Synapse](http://synapse.zeitgeist-project.com/wiki/index.php?title=Main_Page) is a semantic launcher. It can be used to start applications and access documents. It uses [Zeitgeist engine](http://zeitgeist-project.com/about/) to get relevant context. It is implemented using Vala and can be extended via [plugins](http://bazaar.launchpad.net/~synapse-core/synapse-project/trunk/files/head:/src/plugins/). It also supports fuzzy search and you can run different actions for a given item. Source code is hosted on [Launchpad](https://code.launchpad.net/synapse-project).

![Synapse](../img/synapse.png)

## Gnome Do

[Gnome Do](http://do.cooperteam.net/) is a cross-platform launcher written in C#. It is looks very similar to [Quicksilver]({% post_url 2015-03-26-quicksilver %}). Source code is hosted on [Launchpad](https://code.launchpad.net/do).

![Gnome Do](../img/gnome-do.png)

## Kupfer

[Kupfer](http://engla.github.io/kupfer/) is an another launcher. It includes large number of builtin plugins. It is also written in Python and extending it with custom plugins is easier and simpler than extending other launchers. There is an detailed [PluginAPI documentation](https://git.gnome.org/browse/kupfer/tree/Documentation/PluginAPI.rst) which includes instructions how to write plugins. Source code is hosted on [Gnome Git](https://git.gnome.org/browse/kupfer/).

![Kupfer](../img/kupfer.png)

There are three main building blocks in Kupfer: *Leafs*, *Sources* and *Actions*. Description from the documentation:

> A **Leaf** is an object, it represents a program or a file, or a text or
something else. Every type of Leaf has different possibilities, and you
can define new Leaves. Example: a ``FileLeaf`` represents a file on the
disk.

> A **Source** produces a collection of Leaves, so it makes Kupfer know
about new objects. For example, it can provide all the FileLeaves for a
particular folder.

> An **Action** is the part where something happens, an action is applied
to a Leaf, and something happens. For example, *Open* can be an
action that works with all ``FileLeaf``.

## Mutate

[Mutate](https://github.com/qdore/Mutate) is a simple launcher inspired by Alfred. It is written in C++ and Qt. An interesting feature is that you can include scripts in arbitrary languages like python or bash. Scripts are specified in an [INI config](https://github.com/qdore/Mutate/blob/master/config/config.ini). Eeach item includes *name*, *script file*, *icon* and whether it needs *arguments*. When the given item is invoked in command input then the script file is executed.

![Mutate launcher](../img/mutate.png)

## Launchy

[Launchy](http://www.launchy.net/) is a cross-platform launcher implemented in C++ and Qt. It looks like it is currently an abandoned project. It features plugin architecture. Basic plugins include calculator, web search. It seemed that Launchy does not allow to specify additional action on an item. Source code is hosted on [SourceForge](http://sourceforge.net/p/launchy/code/HEAD/tree/).

![Launchy](../img/launchy.png)