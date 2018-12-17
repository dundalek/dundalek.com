---
title: Script mode design proposal for Closh
---

The purpose of this post is to go through possible features and summarize the design of the script mode for [Closh](https://github.com/dundalek/closh). It can be divided into two parts. I am going to start with definition of CLI arguments. The second part describes details of the script mode behavior.

## CLI arguments

The basic idea is to make the accepted CLI arguments mirror the [clojure.main CLI](https://clojure.org/reference/repl_and_main#_clojure_main_help). It already contains flags to execute files, evaluate input, etc. The advantage is a familiarity to the most of Clojure audience. Next I am going to try to discuss some other options commonly found in traditional shells.

### -l, --login

When passing `-l` or `--login` argument to bash it starts a login shell. From my understanding the difference of login shell to an interactive is that login shell loads additional config files. I've always found this behavior confusing and always had to google to see which files and in which order would be loaded (the actual sequence is first `/etc/profile` and then one of `~/.bash_profile`, `~/.bash_login`, or `~/.profile`). Therefore I am considering not having the login mode.

If needed users can simulate the login mode behavior by adding something like this into `.closhrc`:

```clojure
  (when (some #{"-l" "--login"} *args*))
    (source-shell ". /etc/profile")
    (source-shell ". ~/.profile")
```

While looking into this I thought about lifecycle hooks. For example when exiting bash it executes `~/.bash_logout` if it is present. For these kind of hooks I am thinking to having functions. So similarly to currently overriding `closh-prompt` we could override `closh-logout` in `.closhrc`:

```clojure
(defn closh-logout []
  ...)
```

### -i,  --interactive

Shells use the `-i` or `--interactive` arguments to force the interactive mode. The clojure.main uses `-r` or `--repl` for REPL which is the same as interactive mode is for shells. I am wondering whether omitting `-i,  --interactive` might break 3rd party programs that depend on it or not.

It might be useful to check whether the script runs in script mode or interactive mode. Here are snippets how it is done in existing shells:

Bash:
```sh
shopt -q login_shell && echo 'Login shell'

[[ $- == *i* ]] && echo 'Interactive'
```

Zsh:
```sh
if [[ -o login ]]; then
  echo "I'm a login shell"
fi

if [[ -o interactive ]]; then
  echo "I'm interactive"
fi
```
Fish:

```
if status --is-login
    # ...
end

if status --is-interactive
    # ...
end
```

My design philosophy is to minimize the number of options, but eventually we might need to support some options. I currently don't have an opinion what a good API for that could be. I welcome any suggestions.

### -c

The `-c` argument is used to pass a string of commands for evaluation. This corresponds to th `-e` option of clojure.main. Again the question here is whether we need to support it for compatibility reasons with existing programs like multiplexers, terminals or ssh. Another option might be to make the `-c` command execute the input using the `(source-shell)` function which delegates to other shells (bash by default). If we were to use `-c` for this functionality we would need to find and alternative short option for clojure.main `--classpath`, probably `-C` (capital C).

### -s

Read commands from standard input. I think this may be a useful option to add.


## Script mode behavior


### Custom commands usage

For example if you define a command with `defcmd` you can then both invoke it as command or as a function:

```clojure
(defcmd hello [name]
  (println "Hello" name))

; as command
hello Peter

; or as function
(hello "Peter")
```

To make scripts easier to reason about I am considering allowing only the function form in script mode. All external functions would need to be explicitly required and referred.

### Multi-line commands

Commands in command mode are separated by a newline. For multi-line commands the newline could be escaped by the backslash.

```clojure
echo a
echo b
; => a b

echo a \
     b
; Becomes: echo a b
; => a b

; Combining with multi line commands with pipes
echo a \
  | (str/upper-case)
; => A
```

The escaped newline change is part of escaped whitespace support that will be also useful for tab-completion of filenames with spaces. For example:

```clojure
ls A\ Filename\ With\ Spaces
; will be equivalent to:
ls "A Filename With Spaces"
```


### Multiple commands on a single line

Shells use semicolon `;` to separate multiple commands on a single line. We cannot use semicolon directly because it denotes comments in Clojure. I am thinking of using a backslash-escaped semicolon `\;`.

Therefore

```sh
echo a \; echo b
```
will be same as

```sh
echo a
echo b
```

Sometimes there is a need to pass a literal semicolon. We can use the string literal. This case does not happen often so the extra quote seems acceptable.

Bash:
```sh
find . -exec ls '{}' \;
```

Closh:
```sh
find . -exec ls "{}" ";"
```

### Command line arguments

In bash command line arguments can be accessed with `"$@"` and `$#`. Which is not very user friendly to begin with, but it is even worse when one forgets the to write the quotes around `$@` or when beginners get bitten by `$*`.

In fish the situation is much better with a `$argv` variable which is an actual list of strings.

Clojure core exposes `*command-line-args*` which seems too long to me, so I am considering adding an alias like `*args*` for that.

Another alternative is that one could use the `-main` function which accepts the arguments and could be called with `closh -m`.

```clojure
(defn -main [& args]
  ...)
```

### Sequential evaluation

Clojure CLI compiles and evals forms in files sequentially. This might not be ideal in some situations. For example if at the beginning there are some destructive operations with files and after an user makes a typo. In that case the destructive operations are carried out and then the execution aborts with an exception. I think much better would be to analyze the script as much as possible and not even start to execute when there is a compilation error. However, I am not sure how to do this, so I will just mention it as a potential feature for the next iteration.

The example:

```clojure
(println "Desctructive operation 1")
(println name-wth-typo)
(println "Other operation")
```

Results in:

```
Desctructive operation 1
Exception in thread "main" java.lang.RuntimeException: Unable to resolve symbol: name-wth-typo in this context, compiling:(/home/me/github/closh/script.clj:2:1)
	at clojure.lang.Compiler.analyze(Compiler.java:6792)
	at clojure.lang.Compiler.analyze(Compiler.java:6729)
	...
```

## Summary

I outlined a potential specification of the script mode for Closh in accordance with the [design philosophy](https://github.com/dundalek/closh/blob/master/doc/principles.md). I am looking for any kind of thoughts and feedback.

Please post comments in the [Reddit thread](https://www.reddit.com/r/closh/comments/a71usj/script_mode_design_proposal_for_closh/).
