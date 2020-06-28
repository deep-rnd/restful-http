--
layout: post
title: Introducing REST
---

## Rest
A hybrid architectural style derived from several network based architectural styles. 

## Two Perspectives in Architectural design
There are 2 common perspectives in architectural design (be it building or software)
The designer 
1. starts with nothing.
   1. a blank slate, whiteboard.
   2. builds up an architecture from _familiar components_ until it satisfies the need of an intended system.
   3. emphasis on creativity and unbounded vision.
   4. used by REST
2. starts with all the system needs, 
   1. without _constraints first._
   2. incrementally identifies and applies constraints to the elements of the system.
   3. restraint and an understanding od system context.


* * *

## Deriving REST

1. Null Style
   * Simple an empty set of constraints
   * A system which has no distinguishable boundaries between components. 

2. Client Server
   * Separation of Concern:
   * Client - 
     * user interface concerns
     *  to improve portability of user interface across multiple platforms.
   * Server - 
     * data storage concerns
     * to improve scalability
   * Each scale independency, supporting internet scale requirements 

3. Stateless
   * A constraint to client server interaction.
   * Session state kept entirely on the client side.
   * Each request from client to server must contain all necessary information.
   * Improves/Adds
     * Visibility
       * Monitoring systems doesn't need to look beyond a single request datum.
     * Scalability
     * Reliability
       * Easy
4. Cache
   * 
5. Uniform Interface
6. Layered System
7. Code On Demand
