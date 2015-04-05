---
title: Mozilla Ubiquity - Solution for the Disconnected Web
---
Ubiquity is a successor to [Enso Launcher]({% post_url 2015-03-22-enso-launcher %}). It was developed by Mozilla Labs from 2008 to 2009 as a Firefox plugin. There is a introductory post on [Aza Raskin's blog](http://www.azarask.in/blog/post/ubiquity-in-depth/) and a [demo video](https://vimeo.com/1561578).

Ubiquity tries to solve the problem of disconnected web. It is hard for a user to combine functionality of different web sites and apps. One way is to create mashups, but it requires skills of a developer. The solution is a universal access interface so that user can create mashups without the need to wait for developers.

The home page with details is on [Mozilla Labs Wiki](https://wiki.mozilla.org/Labs/Ubiquity). The latest code and plugin can be downloaded from this [repository](https://bitbucket.org/satyr/ubiquity).

## Using Ubiquity

The basic usage is to press `alt + space`. Ubiquity shows up and you can type in the command. To execute the command press `enter`. To cancel or hide you press `esc`. When you select a text and then launch Ubiquity, the text is used as argument. For certain commands like translation the result is inserted into the page in place of the original text.

Use the command `list` to discover all available commands and `help <command>` to see the description for a given command. There is also a [complete tutorial](https://wiki.mozilla.org/Labs/Ubiquity/Latest_Ubiquity_User_Tutorial).

![Ubiquity](../img/ubiquity1.png)

## Developing custom commands

Developers can easily add new commands. Here is an example of a command called `say hello` that displays `Hello World!` message.

{% highlight javascript %}
CmdUtils.CreateCommand({
  names: ["say hello"],
  execute: function() {
    displayMessage( _("Hello, World!") );
  }
});
{% endhighlight %}

The `names` and `execute` are the mandatory attributes of an command. Execute specifies behavior when the `enter` is pressed. You can also specify `preview` that is displayed and updated as the user types in the command. Most commands also takes parameters that are specified using `arguments` attribute. Each argument is of specific `Noun Type` and takes an `Argument Role`.

{% highlight javascript %}
CmdUtils.CreateCommand({
  names: ["echo"],
  arguments: [{role: "object",
               nountype: noun_arb_text,
               label: "your shout"}],
  preview: function( pblock, arguments ) {
    pblock.innerHTML = _("Will echo: ") + arguments.object.text;
  },
  execute: function( arguments ) {
    var msg = arguments.object.text + "... " + arguments.object.text + "......";
    displayMessage( msg );
  }
});
{% endhighlight %}

The `Noun Type` specifies the kind of input. It can be for example text, date, time, url, contact, geolocation etc. The complete list is specified in file [nountypes.js](about:ubiquity?file#index.html#modules/nountypes.js).

The `Argument Role` specifies semantic role of the argument so that arguments can be parsed from a natural language. The roles can be object, goal, source, location, time, etc. See the complete [list of semantic roles](https://wiki.mozilla.org/Labs/Ubiquity/Parser_2/Semantic_Roles).

Imagine an email command with two arguments: `message` and `person`. The user can type in the arguments in an arbitrary position:

- email message
- email to person
- email message to person
- email to person message


By specifying the argument roles, the parser can correctly identify the arguments:

{% highlight javascript %}
arguments: [{role: "object",
             nountype: noun_arb_text,
             label: "message"},
            {role: "goal",
             nountype: noun_type_contact,
             label: "recipient"}]
{% endhighlight %}

See a [detailed tutorial](https://wiki.mozilla.org/Labs/Ubiquity/Ubiquity_Source_Tip_Author_Tutorial) for more information how to develop commands.

Once you have Ubiquity installed, you can look at the [API documentation](about:ubiquity?file#index.html) in a form of an annotated source code. The API for specifying commands is available in file [nountypes.js](about:ubiquity?file#index.html#modules/cmdutils.js).
