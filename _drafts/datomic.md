
Datomic

rethink of DB
broken to smaller pieces
time-aware

Universal schema (agile)
DB is set of 5 tuples - entity, attribute, value, transaction, operation (added/retracted)

easy to model, easy to migrate

Robust
do not update in place, immutable - memory storage is cheap
sharing, distribution, concurency, caching

persistent data structures - remember data from the past - like source control

Powerful
indexes data in many directions
row, column, key-value, document, graph
declarative language dataload - based on relational algebra

Time-aware
- current situtation
- - how were things in the past
- - how have things changed?

transactions, indexing, queries
many choices at once when selection a database

separated services
- Queries
- Transactions
- Storage

Tools
console GUI
REST API - self-documenting for browsers or data for non browsers

Information model
notation: EDN
strings, character, integer, float
boolean, nil, symbol, keyword
collection types:
- list ()
- vector []
- map {:x 1 :y 2}
- set #{:a :b}

Datom  - atomic fact, immutable, 5-tuple

Database - a set of datoms
efficient storage
accumulate only (not append only)

Entity - a view on a group of datoms
- immutable
- lazy (immutable and lazy are tied together - if something is mutable, I cannot deliver it lazily)
- associative - associates keys and values
- represent point-in-time
- can be navigated bidirectionally

Schema
- schemas add power but there is cost and tradeoff
- in datomic schema is plain data added using transactions

identifier
valueType
cardinality - one or many
index
unique - unique or upsert
isComponent - one entity owns other

3 Transactional model

Atomic
Consistent - all processes see the same ordering of transactions
Isolated
Durable - the system always flushes to durable storage before reporting transaction complete

[:db/add entityId attr value]
[db/rectract      ...]



transaction can be entity map
temporary id
partition

Identity
squuid - semi-sequential UUID - for better indexing (indexing friendly)

Atomic increment
- can be created using transaction functions
- kind of like a macro expansion
Compare and swap (CAS) optimistic concurency

4 Datomic Query Data Model
id
lookup - ref - unique attribute
programmable identifier

Datalog
- logic based, relational algebra (prolog no guaranteed termination)
- positional matchin pattern language

Data patterns
- constraints result    :emal
- bind variables        ?customer

[:find ?customer :where [?customer :email]]

:in $ database - binds arguments

exaxt match, joins, predicates (<60 ?price)

stores different indexes to make various query types possible

5 Datomic Time Model

reified transactions
- transactions are like any other entity in the system
- associated within increasing counter t
- can have other attributes

Log
- can ask for range of transactions
- point in time

current state
.asOf
.since
.history

sync - coordinated multiple peers - e.g. load balancing

6 Datomic Operational Model

caching + live index - to avoid rebuilding whole index on every write

object cache is in the peer process
- it beats RPC-based DBs when cache hits



----

Accountants Don't Use Erasers
http://blogs.msdn.com/b/pathelland/archive/2007/06/14/accountants-don-t-use-erasers.aspx

Partial knowledge and eventual consistency
http://blogs.msdn.com/b/pathelland/archive/2007/05/15/memories-guesses-and-apologies.aspx

---

http://nathanmarz.com/blog/how-to-beat-the-cap-theorem.html

Defines data and query

designing a human fault-tolerant data system that beats the CAP theorem

The human fault-tolerance of the batch system is as good as you can get. There are only two mistakes a human can make in a system like this: deploy a buggy implementation of a query or write bad data.

If you deploy a buggy implementation of a query, all you have to do to fix things is fix the bug, deploy the fixed version, and recompute everything from the master dataset. This works because queries are pure functions.

Likewise, writing bad data has a clear path to recovery: delete the bad data and precompute the queries again. Since data is immutable and the master dataset is append-only, writing bad data does not override or otherwise destroy good data. This is in stark contrast to almost all traditional databases where if you update a key you lose the old value.





There are two crucial properties to note about data. First, data is inherently time based. A piece of data is a fact that you know to be true at some moment of time.

The second property of data follows immediately from the first: data is inherently immutable. Because of its connection to a point in time, the truthfulness of a piece of data never changes. One cannot go back in time to change the truthfulness of a piece of data. This means that there are only two main operations you can do with data: read existing data and add more data. CRUD has become CR.

I've left out the "Update" operation. This is because updates don't make sense with immutable data. For example, "updating" Sally's location really means that you're adding a new piece of data saying she lives in a new location as of a more recent time.

I've also left out the "Delete" operation. Again, most cases of deletes are better represented as creating new data. For example, if Bob stops following Mary on Twitter, that doesn't change the fact that he used to follow her. So instead of deleting the data that says he follows her, you'd add a new data record that says he un-followed her at some moment in time.

There are a few cases where you do want to permanently delete data, such as regulations requiring you to purge data after a certain amount of time. These cases are easily supported by the data system design I'm going to show, so for the purposes of simplicity we can ignore these cases.

<<<
A data system answers questions about a dataset. Those questions are called "queries". And this equation states that a query is just a function of all the data you have.
>>>

<<<
The CAP theorem states a database cannot guarantee consistency, availability, and partition-tolerance at the same time. But you can't sacrifice partition-tolerance (see here and here), so you must make a tradeoff between availability and consistency. Managing this tradeoff is a central focus of the NoSQL movement.

Consistency means that after you do a successful write, future reads will always take that write into account. Availability means that you can always read and write to the system. During a partition, you can only have one of these properties.

The complexity caused by the CAP theorem is a symptom of fundamental problems in how we approach building data systems. Two problems stand out in particular: the use of mutable state in databases and the use of incremental algorithms to update that state. It is the interaction between these problems and the CAP theorem that causes complexity.
<<< 

---

Event sourcing

http://martinfowler.com/eaaDev/EventSourcing.html

http://codebetter.com/gregyoung/2010/02/20/why-use-event-sourcing/

---

Datomic

Rich Hickey: Deconstructing the Database
https://www.youtube.com/watch?v=Cym4TZwTCNU

http://tonsky.me/blog/unofficial-guide-to-datomic-internals/


---

Incidental complexity - C++ has no garbage collection
Time/Process - Java - hidden complexity - mutability, concurency, no time management

function value identity state

action / perception

pure functions are worry-free
we are building processes

we invented mutable objects because of the price of storage

we associate identites with seris of causally related values

perception is masively paralel and requires no coordination - there is no message passing


complexity = out of the tarpit

problems
- state
- control

declarative and functional programming, relational model of data

declarative programming - most know SQL


process and perception are independent

novelty - new facts
