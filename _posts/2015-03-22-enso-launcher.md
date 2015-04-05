---
title: Enso Launcher - Away with Applications
---

In a talk [Away with Applications: The Death of the Desktop](https://www.youtube.com/watch?v=3UwZkKsWgc0) Aza Raskin presented thoughts for better workflow on desktop and introduced program called Enso. First he starts showing the problem we have with applications on desktop. The talk is from 2007, yet almost all issues still remain to this day.

![Enso interface](../img/enso.png)

Imagine you want to add a map to email, maybe there is some word you don't understand and would like to see the definition. You can have a photo in a document and want to remove red-eyes from it. You can't remove red-eye from a picture in Word, you can't spellcheck or translate text in Photoshop. Either developer has to think about all the possible cases and implement them or you have to inconveniently load the content into another application and then export it back. There will always be features that you are missing and at the same time lots of other features that get into your way. It is not an ideal situation to prepare meal and assemble furniture using the same universal swiss-army knife.

Applications are liked walled cities, each has its own infrastructure and customs. You should just be able to act on the content. Instead you always have to move information from one application to another to get the functionality you need. It is bad from the user standpoint. When you learn a new application you have to learn an entire range of things. Not just the one thing you need. You get a lot of waste when functionality overlaps and that is why the computers are so bloated. 

First there is a simple solution of how to get to content. Aza proposes command-line interface, because language is powerful. Some might argue that it is too complicated and regular users would not be able to use it. In fact the opposite is true. Everyone uses the command-line in form of a location bar in browser. When you want to see your email you type in "gmail", it is like issuing a command. Another example is when you quickly add event in Google Calendar, you type in the info in single input and calendar figures out the event title, date, place.

There are too many possible things that it is impossible to add them to the application interface without making it too cluttered. An universal access interface might be solution to this problem. Combined with services it can be part of the bigger solution and bring in the functionality. You can have different vendors provide services for individual tasks. The UI will be separated from backend. Imagine providers for maps, searching, translation, calculator, etc. You can access this functionality from anywhere, even when developers of the original application did not think of it. 

Current access methods are not scalable. The new approach should marry the graphical with command-line interfaces (GUIs + CLIs). You can present command lines in a nice way and you can provide good help and discovery system. Content is everything, all you do on a computer is a form of manipulating, creating, selecting, navigating or searching content. Applications and desktop should not get into the way.

Enso Launcher was an commercial software. After it was discontinued it got released as open source. The code is officially hosted on [launchpad](https://launchpad.net/enso) but there appears to be newer version on [github](https://github.com/GChristensen/enso-portable). After the Caps-lock key is pressed an overlay is shown. Commands than can be typed and Enso presents choices for execution.

The community version is written in Python and should be cross-platform, however many of the implemented commands use Win32 APIs making them windows only.
