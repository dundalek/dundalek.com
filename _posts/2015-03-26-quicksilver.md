---
title: Quicksilver - Universal Access and Action
---

Quicksilver is a productivity application for Mac. There is a [video](https://www.youtube.com/watch?v=P_WOPkT-9EI) from 2007 by its author Nicholas Jitkoff explaining some of the concepts. Quicksilver's goals are consistent and similar with those in Aza Raskin's talk Away with Applications. Quicksilver is a mixture of command-line and Finder, most people use it as an application launcher. It is now being maintained by community on [Github](https://github.com/quicksilver/Quicksilver). You can visit the [homepage](http://qsapp.com/) or read the [extensive manual](http://qsapp.com/docs/Quicksilver.pdf) for more information.

The basic idea is that you search for objects and perform actions on them. You can search for iTunes and launch it or jump back and forth between apps. You can also list and navigate in the contents of objects, for example in iTunes you can drill down by artists or albums.

Each user action takes a form of a triple: *noun*,  *verb* and *object*.

![Quicksilver](../img/quicksilver1.png)

You find the thing you want and choose what to do with it. The *object* is an optional third parameter and it used for example when you want to email something to somebody. Using this system you can chain things together and do almost anything. You can select alternative items for each part of the triple.

![Quicksilver](../img/quicksilver2.png)

## Basics

At the core there are some basic things we can do with information:

**Search** - Finding stuff across computer, select items that match.

**Summon** - It is a bit like search but I know exactly what I'm looking for. The goal is to get to the object as fast as possible.

**Browse** - You don't know where the object itself is but You know where it sits in relation to other objects. You can get to a specific song by navigating through the list of albums.

**Act** - Perform a action on the object, accomplish some task.

## Philosophy

There are three principles which provide general guidelines.

**Fast universal access** is about finding anything, instantly. We should be albe to search anything, not just files but also apps, people etc.
  
**Ignoring boundaries** means that it does not matter where the data lives. We should be able to search across multiple places, services and data in cloud. Each app logically consists of different items, you can navigate and jump to them: Safari shows you bookmarks, iTunes show you music, iPhoto shows you albums.

**Act without doing** is to accomplish work without effort. Simple things like jotting down an email or adding an item to todo list should not interrupt what I am currently doing by switching to another application. Also the task should not require upfront effort or planning like setting up chains of commands like in Automator. Finally, is should take current context into account. When I select a word and type define it should define the selected word without any more typing.

## Implementation details

An user input is what is slowing down the system the most. The way to optimize the speed is to decrease input. One way is to type just abbreviations, system learns their meaning from the user over time. This can be done by fuzzy ranking of items. The user must have confidence that he always finds what he is looking for. Therefore the system always returns the same item for a given abbreviation, but it must be flexible and learn new meaning if the user desires.

To provide flexibility and extensibility a plugin architecture is used. Each plugin provides items and actions on them. This allows to get the data, directly manipulate it and pipe it in between the apps. It also allows to index of all items and create catalog. Actions themselves are objects, users can extend or organize the functionality.

Magic and mystery is an interesting feel. The technology will eventually be so advanced and it will seem like it is doing magic and is reading user's mind.

Quicksilver is keyboard focused. Possible extensions could include mouse interaction. There was an experiment of gesture recognition extension called Abracadabra. For visual navigation through content using pie menus there was an extension called Constellation.

One of the limitation of the current system is that you can't search for actions, you have to find the noun first.

## Interaction

In this section I extracted interested parts describing interaction from the [manual](http://qsapp.com/docs/Quicksilver.pdf) by Howard Melman, the content is licensed under [Creative Commons](http://creativecommons.org/licenses/by-nc-sa/3.0/):

> The basic way is to activate the command window with the HotKey ⌃-space. When you type this the command window appears, the first pane is active and you can type to select some item in your catalog.
> 
> Quicksilver keeps track of what you type and what you select and uses that past history to guess what you’re looking for now.
> 
> By default Quicksilver will show its other guesses for what you typed after a few seconds, you can then scroll through them by typing ↓.
> 
> Usually when an item has sub-items you’ll see a > on the right side of the item in the results list. The way you select the sub-items is by typing → or /. 
> 
> In a results list there’s a gear menu in the top right of the window, from there you can choose these behaviors via the Search Modes sub-menu:
> - Filter Results - Filters the current results list.
> - Filter Catalog - Filters, but also includes the entire contents of the top-level catalog. Lasts until you type esc or activate Quicksilver again (⌃-space).
> - Snap to Best - scrolls the results list to the best match but doesn’t remove non-matching items.
> 
> “Switch to text mode if no match is found” will allow you to save typing . or ‘ to enter text mode in a pane. “Reset search after” lets you configure how much of a pause in typing into the command will start a new search as opposed to appending to the existing search.
> 
> If you mistype something, you can type the delete key or ⌘X to clear the pane and start over. If you navigate to something via → or / then these keys will still keep you in the current position but clear the search. To reset entirely so that you’re using the top-level global catalog use the esc key. There’s no way to delete just the last letter typed. 
> 
> A less obvious feature is known as the comma trick. Using the comma key, you can select multiple items in the object pane (or the third pane) and then have a single action operate on all of them at the same time. 
> 
> The Catalog is the collection of items indexed by Quicksilver during its periodic scans. You populate it by configuring catalog sources which Quicksilver periodically indexes.
> 
> Since there are probably a lot of files on the machine, to avoid using a lot of memory and CPU Quicksilver doesn’t scan them all into the catalog. Instead the folders only scan to a configured depth. The default Home source is only indexed one level down and the default Documents source only 2 levels. 
> 
> Quicksilver also understands the tilde (~) as the Unix shortcut for the home directory. Since the Desktop is just a folder in the home directory I could navigate to this manual’s file (at ~/Desktop/Quicksilver.pages) by typing ~/De/Qui
> 
> Triggers allow you to execute Quicksilver commands without having to use the command window. Quicksilver supports executing triggers by typing a HotKey, clicking or dragging the mouse, or (if you have the Abracadabra plug-in installed) making a mouse gesture. 
