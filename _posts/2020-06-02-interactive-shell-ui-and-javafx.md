---
title: Interactive Shell UI and JavaFX
---

It's been a while since the last update about Closh. The reason is that I wanted to finish the GraalVM port before a release. Unfortunately, the port proved more difficult. I kept working on it but kept running into more issues delaying the release. So I finally claimed a defeat in this round and went for a [release](https://github.com/dundalek/closh/releases/tag/v0.5.0) without it.

I've decided to defer the Graal port and continue working on other things. For scripting needs there is already [Babashka](https://github.com/borkdude/babashka) which works great. And the interactive mode is [blocked by JLine](https://github.com/dundalek/closh/issues/173) dependency. Rebel-readline is a great building block to get something up fast. But I want to replace it eventually in the future to get more flexibility, so I am not too motivated to invest much more time in it.

I am also revisiting my approach to writing posts. Previously I tried to write about milestones or breakthroughs. But it was difficult to tell what is noteworthy and I've put pressure on myself with writing and skipped posting updates for some time completely. From now on I will try to write monthly updates. Those will hopefully be about progress and successes. But they can also include failures or just interesting observations along the way.

What's new in May? With the Graal port being on hold for now, I started to focus on building the next version of the interactive UI. I plan to explore interfaces beyond a plain list of items with filtering (as is implemented by existing shells). My vision is to have the ability to write small interactive widgets.

Even [Fish shell](https://fishshell.com/), which I regard as state-of-the-art in interactive shell UIs, has many limitations. First of all the completion UI is just a list of implementing interactive search. It might be useful to be able to specify more actions with the items from the list or display it in a more structured way.

Another issue is the height of the tab-complete list. By default, the Fish's tab-complete list is 5 rows tall. If there are more rows then the list can be expanded by the user to fill more space. This works well when the active line is near the bottom of the screen. But when the prompt line is at the top then space could be utilized automatically. To make this work is [quite tricky](http://ballingt.com/rich-terminal-applications-2/), but it [can be done](https://github.com/bpython/bpython#readme). It is quite a minor detail, but it illustrates that existing shell UIs are built using too low-level primitives, which makes certain details hard to get right.

To experiment with text interfaces I want to use a full-fledged GUI framework. I don't want to be constrained by existing TUI toolkits. I might have missed some interesting ideas if I was limited by what is possible with existing terminals. Once I get a better understanding of the space and come up with more ideas, I can introduce constraints and try to make it work with terminal escape sequences. My main direction is to explore what it would be like to build shell UI using user-composable widgets. There could be different widgets for prompt, input, or better custom-tailored mini UIs for each command.

I am trying out [Cljfx](https://github.com/cljfx/cljfx) because it enables to build UIs with a react-like declarative approach. I also want to learn more about JavaFX. With the rise of Graal it might become a viable alternative for building cross-platform desktop and mobile apps.

To get inspired I wanted to see if there are any existing terminal emulators built using JavaFX. I found [TerminalFX](https://github.com/javaterminal/TerminalFX) library which provides a terminal widget. I looked at the code to see how the rendering is implemented to get some inspiration. Turns out they cheat and run a javascript library inside a webview :)

So I set out to build it from scratch using cljfx. I got the basic text grid with colors and positioning working:

[![Terminal Experiments](../img/terminal-experiments.png)](../img/terminal-experiments.png)

That's all for now. Hopefully, I will stick to my plan and will be back with another post next month.
There is an [RSS feed](https://dundalek.com/feed.xml) if you would like to get notified about future posts. You can discuss the post on [Reddit](https://www.reddit.com/r/closh/comments/gvczro/interactive_shell_ui_and_javafx/).
