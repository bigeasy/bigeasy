Writing software in C, shell, Node.js and Go. Managing infrastructure with
Kubernetes, Consul/Vault, Terraform and Pulumi.

## Database

[Strata](https://github.com/bigeasy/strata) gets a lot of attention because it
is a pure-JavaScript b-tree for Node.js. A proper file-backed b-tree that can
write to either a directory tree or a write-ahead log. The write-ahead log is
itself useful and you can find it in
[WriteAhead](https://github.com/bigeasy/writeahead).

[Memento](https://github.com/bigeasy/memento) is a practical application of
Strata. It is a pure-JavaScript noSQL relational database for Node.js. It is
[ACID](https://en.wikipedia.org/wiki/ACID). It is atomic with all or nothing
transactions, isolated in that changes made during a transaction are only
visible to that transaction, and durable in that there are no parietal writes
and committed writes will survive a system crash. It is based a multi-version
concurrency control model and I've a collection of libraries to build MVCC
databases off of Strata.

[IndexedDB](https://github.com/bigeasy/indexeddb) is a pure-JavaScript
implementation of IndexedDB for Node.js. It is build on top of Memento and is
primarily a proof of concept and is used to leverage the Web Platform Test suite
for IndexedDB to get a through testing of Memento.

## Consensus

[Compassion](https://github.com/bigeasy/compassion) is an atomic log based on a
[Paxos](https://github.com/bigeasy/paxos). People are drawn to the Paxos
implementation via NPM but all that repo it is core Paxos algorithm. If you want
to use that Paxos you should instead use Compassion. Compassion provides the
network communication and implements an `async`/`await` interface you can use to
build applications. It provides an interface for onboarding new instances. You
can use [Conference](https://github.com/bigeasy/conference) to implement a
map/reduce, which ends up being a useful concept in consensus applications,
allowing you to take actions based on whether or not all participants have been
notified. Currently sketching out
[Addendum](https://github.com/bigeasy/addendum) as a proof-of-concept for this
consensus work that implements the `etcd` interface in Node.js using Paxos
instead of Raft.

## Packet Parsing

[Packet](https://github.com/bigeasy/packet) is a binary parser generator for
Node.js that generates pure-JavaScript whole or _incremental_  parsers and
serializers from a syntax-bashed JavaScript. These ought to be as performant as
any parser or serializer you would write by hand.

## Logging

[Prolific](https://github.com/bigeasy/prolific) is yet another logging library,
but one that is both performant due to asynchronous message processing during
normal operation, and durable due to synchronous message processing upon
uncaught exception. Unlike other logging libraries Prolific will not lose your
parting stack trace. The final messages will be captured and redirected to the
same logging stream as your runtime messages. This is kind of a big deal.

## Structured Concurrency

[Destructible](https://github.com/bigeasy/destructible) is a structured
concurrency library I created before I learned about [structured
concurrency](https://learningactors.com/structured-concurrency-in-python-with-anyio/).
It has a different interface than the Python libraries like Trio with it's
nurseries, but the underlying concepts are the same, launching multiple
concurrent paths of execution and having them rendezvous in a single promise
upon completion. Destructible manages multiple `async`/`await` call stacks and
when an exception occurs in any one of them it will gather all exceptions from
an `async`/`await` call combine them into an elaborate report of all stack
traces through that single promise.

[Turnstile](https://github.com/bigeasy/turnstile) performs parallel concurrency
with an explicit work queue that can be monitored rather than the implicit work
queue of spawning an arbitrary number of `async` function calls.
[Fracture](https://github.com/bigeasy/fracture) is a more elaborate parallel
concurrency library with the ability to enqueue work in the work queue from the
work queue in a way that will avoid deadlock.

[Avenue](https://github.com/bigeasy/avenue) is a module that implements what are
essentially Go channels, channels that can be processed synchronously or
asynchronously by zero, one or more consumers (i.e. multiplexed.) The
consumption decisions are deferred so that the producer does not have to concern
itself with the concurrency considerations of the consumer.
