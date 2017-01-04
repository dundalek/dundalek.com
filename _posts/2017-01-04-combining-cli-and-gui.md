---
title: Combining CLI and GUI
---
The command-line interface (CLI) is a powerful way to control computers. However, it is also quite difficult to learn and more complicated to use. Graphical user interfaces (GUI) offer alternative approach that is more intuitive and easier to use but they loose some power. My goal is to explore an approach that takes power from CLI and intuitiveness from GUIs.

Let me describe a usual situation when working in command line. I am in my terminal and I need to accomplish a certain task and I don't know the command. I search google and find a suitable candidate. If I am lucky it is exactly what I need. But often I need to tweak the parameters a bit for my specific situation. Also it is a good idea to verify from another source that the command does what the page says to be secure and prevent malicious behavior. So I open another window and look up the manual page. I read through extensive description and find the additional parameters I need. Then I switch back to the original terminal and I have to manually type out the parameters.

## Interactive CLI approach

So lets imagine an alternative approach. From the command-line I search all available commands. When I find the command I fill out the parameters via a graphical form. Sometimes commands have so many parameters to span over multiple pages. So there is also ability to quickly narrow down the parameters. When the parameters are filled my command is automatically typed out for me and I can run it with by pressing a single key.

There are some common cases one can encounter while working in command line where alternative approach can help:

- You know which command to use but you don't remember the parameter names exactly (also known as [XKCD 1168](https://xkcd.com/1168/))
- You don't know which command can be used to accomplish your task. With alternative approach you can search for it directly from the command line terminal.
- At a last resort you search on google and find possible command. You want to verify it does what the website says.
- You want to repeatedly run some command you ran previously. You can use `Ctrl-R` in most shells to search in history, but that only presents you one command at a time.
- You work on a project with specific commands that are commonly run, for example for compiling the program using `Makefile` or `npm scripts`.

## Technical details

To build such a system we first need to extract the possible command options from the manual pages. Manual pages usually follow formatting conventions but often times are are small differences.

The next step is to build the app and the text-based graphical interface ([TUI](https://en.wikipedia.org/wiki/Text-based_user_interface)). Most terminals also support mouse events so we can bridge the gap further to allow point and click mouse interaction for easier use.

Here are some work in progress screenshots from the prototype of a possible system. First we see a list of commands, one can type out query to search and filter them down. We see short description at a first glance and we can see more details for the selected command. On the second screenshot we see that once we pick the command we get list of options in a form. We just fill in values and we can see the final command we are building at the bottom.

|-|-|
| [![List of available commands with search](../img/command-list.png)](../img/command-list.png) | [![Command detail with options form](../img/command-detail.png)](../img/command-detail.png) |
