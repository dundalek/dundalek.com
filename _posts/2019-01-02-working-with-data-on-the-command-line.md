---
title: Working with data on the Command Line
---

Often times there is a need to extract information or do a transformation involving structured data in formats like JSON, XML and others. For one-off tasks a command line is very useful but traditional tools like `sed` and `awk` are lacking in these cases. What other tools can we use to work with data on the command line?

There exist special purpose tools like [jq](https://github.com/stedolan/jq) for JSON or [xsv](https://github.com/BurntSushi/xsv) for XML. However, each of these have their own syntax. Many times it is easier just to open up a text editor and parse and manipulate the data using a full fledged programming language. Clojure is designed and built for working with data so I am trying to imagine if it could be helpful also on the command line.

### JSON

For example we could have a helper command to parse JSON into data:

```clojure
echo "{\"a\":1,\"b\":2}" | from-json
; => {:a 1, :b 2}
```

Then we could extract a package version like so:

```clojure
cat package.json | from-json | (:version)
; => "0.3.1"
```

Or get a list of dependencies:

```clojure
cat package.json | from-json | (:dependencies) | (keys)
; => (:deasync :glob :lumo-cljs :sqlite3 :tmp)
```

### EDN

Similarly working with other formats like EDN and get a number of dependencies:

```clojure
cat deps.edn | from-edn | #(-> % :deps count)
; => 14
```

It could be used for ad-hoc format conversions:

```clojure
cat deps.edn | from-edn | to-json
```

### XML

XML can be accessible too:

```clojure
echo "<foo name=\"bar\">hello</foo>" | from-xml |
     ((juxt :tag #(-> % :attrs :name)))
; => [:foo "bar"]
```

Or manipulate XML with [zippers](http://josf.info/blog/2014/03/21/getting-acquainted-with-clojure-zippers/):

```clojure
echo "<foo name=\"bar\">hello</foo>" | from-xml | #(-> % xml-zip down node)
; => "hello"
```

### CSV

CSV files also appear often. Let's take a following example data `accounts.csv`:

```
account,balance
a,20
b,55
c,80
```

Parse it into data:

```clojure
cat accounts.csv | from-csv
; =>
(["account" "balance"]
 ["a" "20"]
 ["b" "55"]
 ["c" "80"])
```

Compute the sum of balances:

```clojure
cat accounts.csv | from-csv |
    (rest) | (map (comp read-string second)) | (reduce +)
; => 155
```

It is more natural to work with data using maps. To transform rows into maps we could use a helper function. Then for example increase the balance of each record by 10:

```clojure
cat accounts.csv | from-csv | (csv-data->maps) |
    (map #(update % :balance (comp (partial + 10) read-string)))
; =>
({:account "a", :balance 30}
 {:account "b", :balance 65}
 {:account "c", :balance 90})
```

## Other conversions

Sometimes a conversion between other various formats is needed. For example when using a React component there might be an example code in JSX/HTML but to use it in a re-frame app it needs to be converted into hiccup. There is a handy function [html->hiccup](https://github.com/hozumi/hiccup-bridge) that will do just that.

For easier use people often create [web apps](http://htmltohiccup.herokuapp.com/) that do the conversion. It is useful but at the same time seems wasteful to have so much effort and code to just wrap a single function. And also these are not available for less popular formats and don't work offline.

We can call the function directly:

```clojure
(html->hiccup "<a href=\"foo\">foo</a>")
; =>
([:html [:body [:a {:href "foo"} "foo"]]])
```

A more useful way is to copy the example html into a clipboard while reading docs. Then we could transform the contents of the clipboard:

```clojure
pbpaste | html->hiccup
; =>
([:html [:body [:a {:href "foo"} "foo"]]])
```

## Summary

The command line is based on text manipulation but we mostly need to work with sctructured information. There is an advantage to using the same set of functions on various different data formats. Clojure has a large number of powerful functions built in. We can also leverage additional libraries like [Specter](https://github.com/nathanmarz/specter) which provides powerful data navigators.

As an experiment I implemented those [data utilities](https://github.com/dundalek/dotfiles/blob/master/closh/.closh_data_utils.cljc) mentioned here. All of the code examples above can be run and used with [closh](https://github.com/dundalek/closh). I feel that using the command line in a more a functional way has a promising potential to enable to accomplish ever more tasks and workflows more efficiently.

What other tasks do you need to often accomplish on the command line that would benefit from such approach? Please [leave a comment](https://www.reddit.com/r/Clojure/comments/abuegl/working_with_data_on_the_command_line/).
