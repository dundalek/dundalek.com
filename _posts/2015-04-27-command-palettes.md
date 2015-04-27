---
title: Menus and Command Palettes
---

Traditional desktop apps contain a lot of functionality. To save screen space, prevent user distraction and overwhelming, functionality is hidden in hierarchical menus. Each app has an non-written contract that it should contain certain functionality a user expects form a given app.

When user wants to accomplish certain task, it is often difficult to find where in the menu is correct item located. One way to prevent this is to offer search of available actions. This is what Mac's [Help Menu](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/MenuBarMenus.html#//apple_ref/doc/uid/20000957-CH29-SW5) or [Unity's HUD]({% post_url 2015-03-29-unity %}#hud-and-menu-bar) do.

Some software like [Sublime Text](http://www.sublimetext.com/) or [Atom Editor](https://atom.io/) take this useful approach even further. They make actions first-class and invoke them using command palettes. Menus and keyboard shortcuts become just alternative means for access provided for convenience. When you find a command you also see its keyboard shortcut, so you can remember it for next time for faster workflow. Sublime and Atom can be extended by plugins, which can register additional commands.

### Atom Editor

![Command Palette in Atom](../img/atom-command-palette.png)

Commands are associated using [CommandRegistry](https://atom.io/docs/api/v0.170.0/CommandRegistry)'s `add` method. Context for a command can be specified using CSS selectors, you may for example want to limit the context only to a given panel or editor. The `findCommands` method searches matching commands, this is what the command palette uses. Finally there is a `dispatch` method that allows for a command to be executed programmatically.

Once a plugin registers a command, it can bind it to a keyboard shortcut using [KeymapManager](https://atom.io/docs/api/v0.170.0/KeymapManager). When a single shortcut is bound to multiple commands, dispatcher selects a command based on CSS rule precedence of its selector. The *Key Binding Resolver* can be used to explore how the commands are dispatched.

![Key Binding Resolver](../img/atom-key-resolver.png)

Extensions to Atom a distributed through the [package system](https://atom.io/packages). You have to first install a package to be able to search the commands it contains. I think it might be useful to search through all the metadata and then install the packages on-demand when the command is triggered.
