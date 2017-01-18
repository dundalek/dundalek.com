---
title: Shell Auto-completion Systems
---

One great feature of modern command shells that improves experience is the tab-completion of commands. After typing part of a command and hitting the TAB key the shell presents list of possible completions of a given command. For some commands the completions are quite sophisticated. Lets look how it works for most common shells.

### Bash

Completion scripts are based on shell functions. A completion function will be called and variable `COMP_WORDS` will contain strings that user typed and `COMP_CWORD` indicates current position in input. To offer a suggestions the function will set `COMPREPLY` variable to possible values.

The `compgen` is a helper builtin that is often used to generate list of possible options given all options and prefix.

The completion functions are registered with the `complete` builtin. To list all registered completions one can run `complete -p`.

**Resources**

- Tutorial [part 1](https://debian-administration.org/article/316/An_introduction_to_bash_completion_part_1) and [part 2](https://debian-administration.org/article/317/An_introduction_to_bash_completion_part_2)
- Reference in [bash manual](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html), description of [completion builtins](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html)
- Completion scripts implementation: [bash-completion](https://github.com/scop/bash-completion) package
- A script for accessing [completions programatically](https://brbsix.github.io/2015/11/29/accessing-tab-completion-programmatically-in-bash/)


### Zsh

Zsh has a bit more sophisticated system. It offers more helper builtins to help with writing the completion functions. Another improvement is that completions can contain short descriptions for proposed options that are displayed to the user.

The `_describe` function is a simple way to specify options and arguments similar to `compgen` in bash. For advanced cases there is the `_arguments` helper that takes more formal specification of possible options and arguments and generates completions accordingly. There is also an option to generate completion from the commands help usage message that is taken from `command --help`.

The completion functions are registered with the `#compdef` directive and lazily loaded when a completion for a particular command is invoked.

**Resources**

- Tutorial [here](https://github.com/zsh-users/zsh-completions/blob/master/zsh-completions-howto.org) and [another one](https://askql.wordpress.com/2011/01/11/zsh-writing-own-completion/)
- Reference in [zsh docs](http://zsh.sourceforge.net/Doc/Release/Completion-System.html)
- Completion scripts [built in](https://github.com/zsh-users/zsh/tree/master/Completion) and [community provided](https://github.com/zsh-users/zsh-completions)
-  A script for accessing [completions programatically](https://github.com/Valodim/zsh-capture-completion)

### Fish

Fish has a simple completion system similar to bash but it does not seem to provide additional helper functions. Completion functions are registered with a custom version of `complete`.

**Resources**

- Tutorial and reference in [Fish docs](http://fishshell.com/docs/current/index.html#completion)
- Completion script [implementations](https://github.com/fish-shell/fish-shell/tree/master/share/completions)


## Summary

I explored completion systems in hope of leveraging existing command descriptions. It turns out completion scripts are written in quite an ad-hoc fashion, usually hand-crafted and often do not contain complete set of possible options and arguments. Therefore it will not be possible to reuse them for generating command UIs.

However, they could used initially for a context-sensitive completion. By that I mean when a command needs a file the autocompletion suggests existing files from a current directory. Or when a command requires a server we can list suggestions based on known hosts and so on.
