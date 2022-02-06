---
published: true
---
# **Route Reflectors And Confederations**

Today we will be discussing two different set of BGP related tools you can use to help scale and maintain a large BGP implementation. One is called Route Reflectors and the other is called Confederations. While these two names do sound like something out of Star Trek, please do not be afraid of them. They can make your large BGP setups become stress free (assuming you use them right :P). Lets take a dive!

## Route Reflectors

- To understand Route Reflectors you must understand the problem they attempt to alleviate. In iBGP peers must exist in a fully meshed topology to insure no routing loops. Imagine an iBGP setup where you have 50+ routers in a full mesh - it would be a very tough situation to manage! With route reflectors you can have one router configured as a route reflector (RR) and other iBGP peers called clients. 

- A router reflector and it's clients are known as a cluster. The RR can learn routes from its clients and advertise them to clients and non-clients. The clients can peer with other external neighbors or clients in the cluster. The RR can peer with both internal and external neighbors outside of the cluster. An AS can have multiple clusters and there also can be multiple RR for redundancy in the setup. Route Reflectors follow three rules to determine who the route is advertised to:

  - If the route is learned from a non-client iBGP it is reflected to clients only
  - If the route was learned from a client, it is reflected to all non-clients and clients (except for the originating client)
  - If the route was learned from an eBGP - it is reflected to all clients and non-clients
  
- Due to the iBGP rule where internal neighbors cannot advertise routes learned from on internal router to another, route reflectors need a method in order to prevent 
routing loops. In order to do that RR's make use of two BGP path attributes: ORIGINATOR_ID & CLUSTER_LIST.

- The ORIGINATOR_ID is created by the route reflector and is the router-id (RID) of the originator of a route. If an RR sees an update with it's own RID the route is ignored.

- The CLUSTER_LIST is 4-octet number given to every cluster. When routes are reflected it is prepended with a cluster id just as an AS_PATH. If a RR sees its own cluster id in on the prefix it is dropped.

## Confederations

- Confederations can help segment your AS into smaller sections. A confederation allows you to have sub-autonomous systems known as "member autonomous systems". A confederation receives an identifer called a confederation ID. This is what is actually spread to external AS systems - not the internal sub member AS numbers.

- There are two AS_PATH attributes added to confederations. They are called AS_CONFED_SEQUENCE and AS_CONFED_SET.
    - AS_CONFED_SEQUENCE - Contains an ordered list of AS numbers along the path to the destination. These would be the internal sub member AS numbers.
    - AS_CONFED_SET - Contains an unordered list of AS numbers along the path to the destination. These would be the internal sub member AS numbers.

- From the view of external numbers a confederation is just one AS system. They do not see the internal AS numbers of the confederationl. eBGP routes external to the confederation are preffered over eBGP routes to member AS systems, which is preffered over iBGP routes.