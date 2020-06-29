---
layout: page
title: Introducing REST
---

## Rest, What?

REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems and was first presented by Roy Fielding in 2000 in his famous [dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) and [notes](/_posts/2020-06-28-royfielding_dissertation_chapter5.md).

## Why REST?

REST provides a set of architectural constraints that, when applied as a whole, 
* emphasizes scalability of component interactions, 
* generality of interfaces, 
* independent deployment of components, and 
* intermediary components to reduce 
  * interaction latency, 
  * enforce security, and 
  * encapsulate legacy systems. 

### Representations, What?    

* Its a means to manipulate resources 
    * Resources, the actual stuff, will never be transmitted over the network, instead representation of resource are transmitted.
* A Representation consists of
    1. Data (as JSON, XML,..)
    2. Metadata (http headers : content-type,...)
    3. Metadata of Metadata (for verifying data integrity)

Cheers!
