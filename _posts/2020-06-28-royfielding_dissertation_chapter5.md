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
       * monitoring systems doesn't need to look beyond a single request datum.
     * Scalability
       * server doesn't have to manage resource usage across requests.
       * allows the server component to quickly free resources
       * stateless applications are a prerequisite to auto scaling and immutable infrastructure since any request can be handled by available computing resources
     * Reliability
       * easy recovery from partial failure.
       * stateless applications are a prerequisite to auto scaling and immutable infrastructure since any request can be handled by available computing resources
     * Design trade-off
       * decrease network performance 
       * reduces the server's control over consistent application behavior.
         *  server's dependent on the correct implementation of semantics across multiple client versions
   
4. Cache
   * to improve network efficiency, scalability, and user-perceived performance
   * require that the data within a response to a request be _implicitly or explicitly labeled_ as cacheable or non-cacheable.
   * decrease reliability if stale data
  
5. Uniform Interface
   * uniform interface between components
   * applying the software engineering principle of generality to the component interface
     * overall system architecture is simplified
     * visibility of interactions is improved
     * Implementations are decoupled from the services (independent evolvability)
   * Design trade-off
     * degrades efficiency (information is transferred in a standardized form rather than one which is specific to an application's needs)
   * _The REST interface is designed to be efficient for large-grain hypermedia data transfer, optimizing for the common case of the Web, but resulting in an interface that is not optimal for other forms of architectural interaction._
   * In order to obtain a uniform interface, multiple architectural constraints are needed:
     * REST is defined by four interface constraints
      1. identification of resources; 
      2. manipulation of resources through representations; 
      3. self-descriptive messages; and, 
      4. hypermedia as the engine of application state.  
6. Layered System
7. Code On Demand
