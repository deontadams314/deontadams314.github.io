# **Split Horizon/Posion Reverse/Route Poisoning**

Today's topic is Split Horizon/Posion Reverse/Route Poisoning and we will discuss what they are and how routing is affected. Split Horizon is a method of preventing loops in distance-vector protocols. It works by not allowing a router to advertise a route back into the same interface it was learned on. For example router R1 learns the route 192.168.0.0/16 from R2 on its e0/0 interface. Due to split horizon it will not advertise that route back to R2 on it's e0/0 interface. Simple enough aint it? Split horizon is only used in distance-vector routing protocols. We can still take a look at different routing protocols and see how they prevent routing loops with similar network settings.

## OSPF - Split Horizon

- OSPF actually doesn't use split horizon as it is a link-state protocol. OSPF uses the SPF algorithm to find the best bath to a route to maintain a loop free topology. The backbone Area 0 is utilized to maintain the loop free structure. OSPF has two major rules regarding the backbone area. For Intra-Area communication to occur the traffic must traverse the backbone area. ABR routers must disregard Type-3 Network LSAs from any non-backbone area and only accept them from area 0.

## BGP - Split Horizon

- BGP has a split horizon rule that is specifically for iBGP. When an iBGP speaker receives a route from an internal peer, that iBGP speaker cannot advertise the route to other iBGP peers. This is because in iBGP the AS_PATH attribute is not modified due to the fact that the AS does not change. An internal iBGP peer could potentially advertise that route back to the originating peer or the route could be withdrawn and still exist in the network as valid. This is why iBGP requires a full mesh topology of BGP peers. This can be remedied with Router Reflectors or with Confederation setups.

## Poison Reverse

- Poison Reverse is used in conjuction with Split Horizon and is actually the reverse of it. If a route is found to be invalid instead of not being advertised, it will be advertised with the infinite (∞) route metric. This ensures a path does not return back to the same router if the metric has changed.

## Route Poisoning

- Route Poisoning is typically used in distance-vector protocols for loop prevention. If a route is detected to be unreachable it is given an infinite (∞) route metric and advertised to other routers in the network. The route is deemed invalid and unreachable at that point. RIP for example uses hop counts to determine the feasaibilty of a route. If the route reaches past the max hop count of 15 the route is invalid and route poisoning is used to let other routers now about this fact.