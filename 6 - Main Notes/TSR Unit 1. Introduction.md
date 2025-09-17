2025-09-17 13:05

Status: #child #lectures

Tags: [[Concurrency]]

# TSR Unit 1. Introduction

... I  was terribly lost on the previous lectures, the teacher pronunciation is really difficult for me, plus he doesn't use the mic
## 5.1. Concurrent, state-sharing servers

We treat our program as a collection of events with a set of instructions

## 5.2 Async(hronous) Servers
Here’s the text version of the slide:

**Advantages**

* Shared state handling complexity greatly diminishes
	Now we only have a single active action
	Still, careful on handling of the turn queue to avoid surprises
* Less overhead, as no multi-threading environment is supported
	  Better ability to scale
* Close match to how a distributed system actually works: event-driven
	  Easier to reason about what is going on
	We have a mathematical way to ensure the correctness, making it easier to reason about what is going on

**Disadvantages**

* Proper state-handling is necessary when building actions
* Needs all environment to be async, not just IPC
	  OS services need to be async too, to avoid blocking

**Prevalent environments with built-in support in language**

* Nodejs
* Async .NET


## References

[[TSR Concepts.]]