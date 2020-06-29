---
layout: post
title: Dissecting A Dissertation
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
   1. Composed of hierarchical layers by constraining component behavior 
      1. each component cannot see beyond the immediate layer with which they are interacting.
      2. reduce overall complexity
      3. promote substrate independence
      4. encapsulate legacy systems
      5. protect new systems from legacy clients
      6. move infrequently used components to shared intermediary.
      7. improve scalability (eg. LB of a service across multiple n/w & processors)
      8. Caching at boundary of organizational domain can improve performance
      9. Implement security policies on data crossing organization boundary (firewalls)
   2. Trade Offs:
      1. Overhead and latency, reducing user perceived performance.
         * Caching can offset it 
   3. Uniform interface + Layered system = uniform pipe and filter style
   4. Intermediatory components can actively transform data because
      1. Messages are self-descriptive
      2. Semantics are visible to intermediaries 
            
7. Code On Demand
  * REST allows to extend the client functionality by allowing it to download and execute code 
  * Advantage 
    1. Simplify client, reuse, not ro reinvent, not to pre-implement, extendable system after its deployment.
  * Trade-Off
    1. Reduces Visibility
       * Optional component in REST (oxymoron?)
         * An optional constraint allows us to design an architecture that supports the feature in general,
         * But with the understanding that it can be disabled within some context. 

* * *
  
## Architectural Elements

* REST is an abstraction of elements in a distributed hypermedia space.
  * “Hypermedia” as a shorthand for “Hypermedia As The Engine Of Application State” (HATEOAS), which is one of the ugliest acronyms I’ve ever seen.
  * Basically, it means that a REST API provides hyperlinks with each response that link to other related resources.
  * REST ignores component implementation and communication protocol between those components, but considers,
    1.  Roles of components
    2.  Constraints on interaction with each other
    3.  Their interpretation of significant data elements
  * defines the essence of it behavior as a network based application. 

### Data Elements
  * In REST data is moved from the place its stored to the place its needed or requested for.
    * This is unlike many other distributed systems where its easier and efficient to move the processing agent (code, stored procedure, search expression) to the data.
  * A distributed hypermedia architect has only 3 options:
    1. Render data at its location and send across a fixed format image
      * **traditional client-server style.**
      * hide true nature of data
      * client implementation easier
      * client has restricted/limited function
      * processing load on server => harder to scale
    2. Encapsulate data with a rendering engine and send both to recipient
      * **mobile object style**
      * hides information
      * specialized data procession (by the special rendering engine)
      * limits functionality of client based on rendering capability and what it can anticipate
      * more data volume
    3. Send raw data + metadata to recipient, and allow recipient to choose their own rendering engine.
      * light weight sender
      * scalable sender
      * less data volume 
      * no data hiding
      * sender and recipient should understand the same language
  * REST is a hybrid of all 3
    1. shared understanding of data and meta data
      * REST communicates by sharing a representation of a resource
      * In a format matching one of the evolving set of standard data types (JSON, XML, ATOM)
      * The data type is selected dynamically, based on
          1. capability/desire of recipient
          2. nature of the resource
    2. Representation hides behind the interface
    3. Benefits of mobile object style are approximated by 
        * sending data in a standard format
  
| Data Element | Modern Web Examples |
| ----------- | ----------- |
| resource | the intended conceptual target of a hypertext reference |
| resource identifier | URL, URN |
| representation | HTML document, JPEG image |
| representation metadata  | 	media type, last-modified time |
| resource metadata  | source link, alternates, vary |
| control data  | if-modified-since, cache-control |

#### Resources and Resource Identifier
  * a key abstraction 
    * a document
    * a image
    * a temporal service (today's temperature, currency value)
    * a collection of other resources
    * a non virtual object (a person)
  * any concept that might be the target of an author's hypertext reference
  * its the conceptual mapping to a set of entities, 
  * its not the entity that corresponds to the mapping at any point in time.
    > More precisely, a resource R is a temporally varying membership function MR(t), which for time t maps to a set of entities, or values, which are equivalent.

  * the values in the set can be
    1. Resource representation
    2. Resource Identifier
  * a resource can map to an empty set => references can be made to concepts before they become a reality.
    * remember pointers in C
  * Key features provided by this abstraction to web architecture :
    1. provides generality without artificially distinguishing them by type / implementation.
    2. late binding of the reference to a representation => content negotiation.
    3. reference the concept rather than some singular representation of the concept.
  * REST relies on the author choosing a resource identifier that best fits the nature of the concept being identified.
  * Naturally, the quality of an identifier is often proportional to the amount of money spent to retain its validity, which leads to broken links as ephemeral (or poorly supported) information moves or disappears over time.
   
#### Representation
* Actions are performed on resources using representations of the resource.
* Representations are 
  1. used to capture current or intended state of resource.
  2. transferred between component.
  3. a sequence of bytes + representation metadata to represent those bytes.
  4. consists of data + metadata + occasionally, metadata of metadata (for verifying message integrity).
* Metadata
  1. Name value pair
  2. name = a standard that defines the values structure and semantics.
* Response includes :
  1. representation metadata
  2. resource metadata (resource information thats not specific to the representation).
* Control data
  1. defines the purpose of a message between components like
     1. action being requested.
     2. meaning of a response (if-modified-since).
  2. It also can:
     1. parametrize requests
     2. override default behavior of intermediaries (cache-control)
     3. content negotiation
     4. media type (data format of a representation).
        * intended for 
          1. human user
          2. automated processing
          3. both
        * composite media type (multiple representation in a single request)
        * can impact user perceived performance of distributed hypermedia system
          1. If data must be received entirely before processing
          2. incremental rendering (HTML)

### Connectors
* abstract interface 
  1. for component communication.
  2. simplicity by clean separation of concern.
  3. hides implementation details
  4. hides communication mechanism
  5. substitutable (due to the generality of the interface)
* Manages network communication for a component
  * information gets shared through multiple interactions (improves efficiency and responsiveness)

* REST Connectors	

| Connector | Modern Web Examples |
| ----------- | ----------- |
| client | libwww, libwww-perl |
| server | libwww, Apache API, NSAPI |
| cache | browser cache, Akamai cache network |
| resolver | bind (DNS lookup library) |
| tunnel | SOCKS, SSL after HTTP CONNECT |

  * How statelessness helps connectors:
    1. less physical resources, improves scalability
    2. parallel processing (processing mechanism doesn't need to know interaction semantics) 
    3. view and understand request in isolation
    4. reusability of cached component

  #### Client & Server Connectors
    * Client : initiates the connection. Source.
    * Server : listens for connections, responds to requests in order to supply access to its services.
    * A component can include both client & server.

  #### Cache Connector
    * typically implemented within the address space of the connector that uses it.
    * some cache are shared
      * effective in reducing the impact of flash crowds
    * REST attempts to balance the desire for transparency with desire for the efficient use of network
      * It doesn't assume that absolute transparency is always required.
    * Cacheability of a response can be determined since the interface is generic (Uniform interface)
    * Can be overridden by control data (cache-control)
  
  ####  Resolver
    * translates partial or complete resource identifier into network address information needed for inter-component communications. 
    * DNS host name : naming authority of a resource

  #### Tunnel
    * Relays communication across a connection boundary (firewall, low-level network gateway)
    * Some rest components can switch from active component behavior to that of a tunnel.
      * Eg. HTTP Proxy switches to tunnel behavior in response to CONNECT method request
        * This allows client to communicate to remote server directly using a different protocol, such as TLS 

### Components

* * *

