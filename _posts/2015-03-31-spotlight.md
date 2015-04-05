---
title: Spotlight - Desktop Search for Mac
---

Spotlight is a desktop search system for Mac. User can use Spotlight to quickly search for things like app, documents, other files, system preferences and additional results from Wikipedia, news sites, Maps, movie listings, and more. Additionaly results can also include dictionary definitions, currency conversions, and quick calculations.

Spotlight can be opened by pressing `command+space` or clicking the magnifying glass icon in the upper-right menu.

![Spotlight in OX Leopard (source Wikipedia)](../img/spotlight-leopard.png)

Spotlight was redesigned in OS X Yosemite and it now displays centered window similar to Ubiquity. There is a list of possible results on the left and preview of the currently selected result using QuickLook on the right. The results are grouped by the item category. User can use `arrow` keys to navigate in the result list, `command + arrows` jumps to different category.

![Spotlight in OS X Yosemite (source Wikipedia)](../img/spotlight-yosemite.png)

## Query Language

 The query can include boolean operators `AND`, `OR`, and `NOT` and items can be filtered by metadata attributes like creation date, modification date, size, author, etc. For example query like `budget kind:document AND author:Pete` searches all documents by Pete that contain the word `budget`. There is detailed description of [query parameters](https://support.apple.com/kb/PH18758?locale=en_GB&viewlocale=en_US). Here is a list of [item types](https://support.apple.com/kb/PH18800?locale=en_GB&viewlocale=en_US) that can be used for the `kind:` parameter.

## Finder Search

Finder Search can be opened using `Option + Command + Space` and can search same queries as Spotlight. Finder Search can be used to further refine the query and narrow down the results. It presents graphical interface to build the expression and lists the available attributes.

![Finder Search](../img/mac-search1.png)
![Finder Search Attributes](../img/mac-search2.png)

## Command-line tools

There are command line tools that can be used to interact with Spotlight.

`mdfind` can be used for performing searches.  
`mdls` lists all attributes extracted for a given file.  
`mdimport` is used to import additional attributes or files.  
`mdutil` is a tool for managinx Spotlight indexes.

## Settings

Spotlights settings includes options to choose which categories should be displayed in results and their order. In the privacy settings one can setup which locations should be excluded from the search.

![Spotlight Settings](../img/spotlight-settings.png)