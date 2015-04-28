---
title: The Essence of Apps
---

The purpose of software is to enable us to accomplish various tasks.

The functionality of software is packaged as apps. This is an artificial invention that allows vendors to sell apps as products and charge money. Being able to get rewarded through business helps to drive innovation. However if the functionality is locked in black-boxed apps the rate of innovation slows down.

Lets look at main concepts applications consist of. The essence of apps can be distilled into three parts: managing **context**, data **representation** and providing **actions**.

The job of app designers is to imagine a set of possible tasks people might want to accomplish in a given area (called *use cases*). Then they design the interaction and logically divide various contexts into screens. These screens then present actions a user can perform in a given context.

This is a very hard job which is about balancing things out and compromises. One one side you can have feature bloated programs we've seen in 90s. On the other hand you have minimalistic mobile UIs. Being simple is a good thing but sometimes developers take it to extremes and remove functionality without providing an alternative.

On the traditional desktop the situation is bearable using the file metaphor. You can share the files between apps and get the functionality you need by combining different apps. It is not an ideal situation, switching between apps is distracting and slow but it gets the job done.

However with introduction of small-screen smartphones you can fit only one app on the screen. Therefore interoperability between apps is not a concern and it gets neglected. I think we are heading into wrong direction because we are ending up with apps with overlapping functionality and missing other non-common functionality.

No designer can design a software that perfectly fits your needs because they don't know your exact needs. We end up in compromises. Thanks to advancements of computer science computers can learn and predict patterns very accurately. In an ideal world you would perform your tasks that consists of multiple steps and computer would learn it and present it next time you need it click of a button. However, it is not possible if the apps are sealed-in blackboxes.

Great thougts how context inference and information ecosystems might work are described in Bret Victor's essay [Magic Ink](http://worrydream.com/MagicInk/#engineering_inference_from_history). Another ideas how the separation might be implemented can be found in [command palettes]({% post_url 2015-04-27-command-palettes %}) or [Ubiquity]({% post_url 2015-03-24-mozilla-ubiquity %}).

### Conclusion

To move into a better future we need to separate the three concerns applications provide. These are:

1. **managing context**
2. **representing data**
3. **providing actions**

<br><br>

### Examples

The text above is pretty abstract and meta-level. In this section I present some examples that illustrate those abstractions. Here are examples of tasks we often want to accomplish. Notice that often the tasks are composed of a number of subtasks.

> - Take a picture, add text labels, frame it, adjust colors, publish/share to various services.
> - Look at historical data, analyze trends and predict future outcomes.
> - Find a restaurant of particular style, get driving directions, send it to a friend so we can meet there.

Following are examples to illustrate principle of context, representation and actions of apps.

> | | **File manager** |
> | **Context** | opened folder and files it contains,<br>custom selection of files |
> | **Representations** | textual list or grid of icons |
> | **Actions** | copy, delete, move file, etc. |

> | | **Video** |
> | **Context** | video clip |
> | **Representations** | play it as a movie,<br>display it as a time line and frames for editing |
> | **Actions** | play it, attach subtitles, play it at faster speed,<br>cut frames, move a sequence |

> | | **Web page** |
> | **Context** | URL |
> | **Representations** | graphical rendering, source code |
> | **Actions** | navigate to another url by clicking link, fill in a form, make text bigger, extract some useful information |

Now two examples of how simplified interfaces can make apps entirely unusable:

>  *Example 1:* Android timer. Great interface, simple and does what it is supposed to do. But the sound is super annoying to me. Unfortunately it does not have settings. I have to download and learn another app. Another downside is that many apps that replace basic system's functionality abuse permissions and display invasive adds.
  
> *Example 2:* I use Dropbox to store my notes as a files. I can use powerful editor on desktop to manipulate the notes. Sometimes I have ideas on the go. There is no way to open and edit particular text file on iOS and save it back. This makes Dropbox on iOS pretty much useless. There are some editors for which the developers explicitly created integration. But these apps usually access all of the files and need to synchronize them upfront.

This example illustrates how computer can learn what tasks we want to accomplish with certain files. The computer can automatically make the process much more efficient.

> For example the computer can learn that for JPEG images large 1000px (usually photos) I often adjust white balance, apply some filters and share to other platforms. The interface would automatically present these actions based on the context. On the other hand, PNGs are mostly used for web graphics, so computer could learn that it is important to optimize the size.

Many tasks are very hard or even impossible to accomplish. Either you must be lucky that someone has built the solution to the exact task you want. Or you can program the solution yourself, which is usually non-feasible for one-off tasks. This example shows how composition of smaller pieces can enable us to achieve things that might be very difficult with current-state software.

> Many applications implement different versions of a slideshow functionality. Slideshow is just displaying images one at a time on full screen. When the system already knows how to display an image and includes operations on list of things, there is no need to load external application. Lets say you want to display 4 images at a time. Either you can search for an application that supports it, or maybe you can drag these into a presentation program and manually arrange them. In a more mature ecosystem you could instead use standard functions to partition the files into groups of 4 and then display grid of images for each group.

Now I present some scenarios how composition of functionality created by different vendors might allow us greater flexibility and effectiveness. Imagine following possibilities:

> - Microsoft Excel is great for manipulating data. Imagine you could buy extra plugin to predict some patterns. You could use this plugins to analyze data from a table on some web page or sales data from your eshop. Once you need more capability you could use some of the MATLAB functionality and you would not loose the plugin functionality because of an introduction of another environment.
> - Imagine Instagram being separated into actions applying filters and sharing. You could then use the filter for images taken on your DSLR.
> - You would buy Photoshop bundle from Adobe than performs certain effects. You could then use them also to modify photos on your phone.
