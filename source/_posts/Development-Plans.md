title: "Development Plans"
date: 2015-04-14 17:08:59
tags:
categories: Plans
---

As I said in my previous post, I would like to explore alternative means of communicating between programs written in different languages, and then using those components to assemble working applications.  

I see three major steps to this effort:
- develop data structures in shared memory to simplify interprocess communication in C
- use foreign function interfaces in various languages to use those data structures
- develop scripting to assemble programs written in various languages to assemble working applications

Because there are several shared memory data structures I have in mind, I do not intend to complete each step before proceeding to the next. Rather, I intend to iteratively go through these steps for each data structure.  For example, the first data structure I am building is a new, improved version of the interprocess queue that is simpler to use and much more functional than OS based implementations currently available.  It would be quite useful to at least partially complete steps two and three before moving on to the next data structure.  In fact, the majority of the benefit will come from completing those steps for the shared memory queue.

The three data structures I have in mind at this point, all to go in the same library, are as follows:
- shared memory queue that can grow dynamically and has no limits on message sizes
- shared memory allocator that allows dynamically allocating portions of memory that can be referenced through a passed token
- shared memory map for storing and accessing key/value pairs using arbitrary data as keys and values

I am beginning with the shared memory queue because that allows me to pass messages between programs and simulate both Actor and communicating sequential processes (CSP) models of computation.  The shared memory allocator is an idea that occurred to me while considering how I would practically build applications using the queue.  The queue is designed to handle messages of arbitrary length, but the occasional large message would cause all queues it was placed on to grow to an unnecessary size for just that one message.  My solution is allocate space in shared memory associated with a token that can be passed via the queue and to allow the safe access of that memory through the use of the token.  Lastly, the associative shared memory map is on the agenda as a generally useful data structure for building multiple types of applications.  The Lua language, for example, demonstrates the utility of the associative array, or table in its vernacular, for implementing multiple software development paradigms.
