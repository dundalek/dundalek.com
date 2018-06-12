---
title: "Closh: Where we are and what's next"
---

I've been using bash for a nearly a decade and half. During that time I've seen very little innovation of bash and command line shells in general. The frustration with lack of innovation culminated in October last year. As I've been discovering the power and beauty of Clojure I got a spark of inspiration. I hacked together a proof of concept to see if it would be viable to use Clojure as a language for a shell. This effort then lead me to building a [full-blown command line shell](https://github.com/dundalek/closh).

Over the months I added more features necessary for daily use like searchable history, tab completion, aliases and others. Around 4 months ago I switched to closh as my primary shell and I've been using it daily since.

Next focus is to increase reliability and improve the UI of readline interface. As a way to get there I am planning to add a JVM port of closh which will give us following benefits:

- When running on JVM we can use [rebel-readline](https://github.com/bhauman/rebel-readline) which will give us multiline support, key bindings, syntax highlighting, interactive autocomplete and other cool features.
- When adding another platform it's a good opportunity to re-architecture the internal structure and end up with better and more flexible abstractions.
- Potentially broader adoption by the Clojure audience with aversion against JavaScript.
- Thanks to recently introduced Java modules and GraalVM we there might be an opportunity to create a single executable and have a fast startup time.

Porting closh to JVM will take some time. The pace of adding new features or bug fixes might slow down for a bit, but I believe the benefits will be great in the long run. I am hesitant to do do any estimates for side projects, but I think the end of this year is a reasonable time frame to get this done. Shells have been in use for many decades, so I view this effort as a marathon rather than a quick run. You can always check the progress [in the dev branch](https://github.com/dundalek/closh/commits/dev).

Most importantly I met many curious and smart people on this journey who share this vision with me. I really appreciate all the support and help, thank you.
