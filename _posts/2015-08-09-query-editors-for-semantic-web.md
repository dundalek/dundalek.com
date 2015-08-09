---
title: Query Editors for Semantic Web
---
I believe that Semantic Web and Linked Data is a way of future. However, if we want the widespread adoption, tools that are accessible for common users must be available. These tools must be easy to use and deliver notable benefits by unlocking the full potential of semantic web. The goal of this post is to review the tools for querying semantic data that are available.

Various datasets are scattered around the web. Most notable is [DBpedia](http://dbpedia.org) which leverages information from Wikipedia and contains lost of data. [This page](http://wiki.dbpedia.org/OnlineAccess) lists possible ways how one can access DBpedia's data. Lets take a look at the tools.

### SNORQL

SNORQL at [http://dbpedia.org/snorql](http://dbpedia.org/snorql) is a pretty basic query explorer. There is a text area where you type your query. Results can be displayed in a table or downloaded in JSON, XML or XML transformed with a XSL template. You can click on a entity in the result table which takes you to a query that lists all triples for a given entity. Source code can be found on [github](https://github.com/kurtjx/SNORQL).

<a href="../img/sparql/snorql.png"><img src="../img/sparql/snorql.png" alt="SNORQL" style="height: 300px;"></a>

### Virtuoso SPARQL Query Editor

Virtuoso SPARQL Query Editor at [http://dbpedia.org/sparql](http://dbpedia.org/sparql) is very similar to SNORQL. It offers additional export formats like Turtle, RDF/XML, CSV and others. It has also more predefined namespace prefixes. However, the results are displayed on a separate page. Therefore I prefer SNORQL, where it is easier and faster to tweak the query.

|-|-|
| [![Virtuoso SPARQL Query Editor](../img/sparql/sparql_01.png)](../img/sparql/sparql_01.png) | [![Virtuoso SPARQL Results](../img/sparql/sparql_02.png)](../img/sparql/sparql_02.png) |

### iSPARQL

OpenLink [Interactive SPARQL Query Builder (iSPARQL)](http://wikis.openlinksw.com/dataspace/owiki/wiki/OATWikiWeb/InteractiveSparqlQueryBuilderOverview) at [http://dbpedia.org/isparql](http://dbpedia.org/isparql) is an advanced query builder with many features. It helps you to write queries by choosing from predefined templates. There is also an option to build a query visually by constructing a graph, but I find this method confusing. There are more ways how you can display results. In addition to grid view there is also some kind of chart. iSPARQL may be useful for intranet portals, because you can save your queries to a WebDAV server which you can browse and run later. I personally find iSPARQL very unintuitive. Source code is available on [github](https://github.com/openlink/iSPARQL).

|-|-|-|-|
| [![iSPARQL Query Input](../img/sparql/isparql_01.png)](../img/sparql/isparql_01.png) | [![iSPARQL Results Table](../img/sparql/isparql_02.png)](../img/sparql/isparql_02.png) | [![iSPARQL Graph Visualization](../img/sparql/isparql_03.png)](../img/sparql/isparql_03.png) | [![iSPARQL Grapch Query Editor](../img/sparql/isparql_04.png)](../img/sparql/isparql_04.png) |


### DBpedia Query builder

DBpedia Query builder at [http://querybuilder.dbpedia.org](http://querybuilder.dbpedia.org) is very simple tool. It shields you from directly typing in the SPARQL query by providing inputs which are translated into a WHERE clause. It is very limited and I do not find it practical at all.

<a href="../img/sparql/query-builder.png"><img src="../img/sparql/query-builder.png" alt="DBpedia Query builder" style="height: 300px;"></a>

### Virtuoso Faceted Browser

Faceted Browser at [http://dbpedia.org/fct](http://dbpedia.org/fct) is an alternative way how to query the data. The advantage is that user does not have to know SPARQL. First a search box is present and the text query matches among all values and attributes. One can view matched entities, attributes and values including their frequency count. This can be used as a facet and refine the query. The final query can be exported in SPARQL. I like this approach, but I think the UI can be even more intuitive.

|-|-|-|-|
| [![Faceted Browser Text Input](../img/sparql/fct_01.png)](../img/sparql/fct_01.png) | [![Faceted Browser Results](../img/sparql/fct_02.png)](../img/sparql/fct_02.png) | [![Faceted Browser Entity Facet](../img/sparql/fct_03.png)](../img/sparql/fct_03.png) | [![Faceted Browser Resource Description](../img/sparql/fct_04.png)](../img/sparql/fct_04.png) |

## Summary

From the tools described above I prefer to craft the query using SNORQL. Faceted Browser can be sometimes used to speed up the creation of initial query. However, I conclude that none of these tools are suitable for a common user and better tools must be developed.
