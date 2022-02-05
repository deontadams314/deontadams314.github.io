---
published: true
---
# **BGP Path Attributes**

BGP uses a series of path attributes to make its routing decisions. This can affect how traffic is routed to or even how traffic is received from peers. Here we will take a look and discuss these path attributes to better understand how they can affec BGP behavior.

## AS_PATH

- The AS_PATH attribute describes the autonomous systems that the network prefix (NLRI) has crossed. The AS numbers listed in the AS_PATH were prepended from other BGP speakers.

- AS_PATH can help prevent loops because if a BGP speaker see's it's own AS in the attribute path it will know to disregard the route.

- This attribute can also help influence incoming traffic by changing the AS path of it's advertised route. The BGP router will add it's own AS multiple times to the AS_PATH. This is know as _AS Path Prepending_.

- This is a well-known mandatory attribute.


## ORIGIN

- The ORIGIN attribute tells the BGP speaker where the route originated from. There are 3 possible areas of origin for a NLRI.
	- IGP: The route originated from a routing protocol internal to the originating AS. IGP has the highest preference.
	- EGP: The route originated from the Exterior Gateway Protocol. This has the second highest preference.
	- Incomplete: This means there is not enough information to determine where the route originated. This doesnt necessarily mean the route is bad just there is no way to determine the original source.

- This is a well-known mandatory attribute.

## NEXT_HOP

- As the name suggests, the NEXT_HOP attribute will tell us the the IP address of the next hop router on the path to the destination. Keep in mind this will not always be the next hop neighbor. Here are 3 rules regarding this attribute.
	- EBGP: If the advertising peer and receiving peer are in different AS, the NEXT_HOP will be the IP address of that advertising peer.
	
	- IBGP_1: If the advertising peer is in the same AS and the prefix is in the same AS, then the NEXT_HOP will the be the IP address of the peer who advertised the route.
	
	- IBGP_2: If the advertising peer are IBGP neighbors and the prefix was learned from another AS, the NEXT_HOP will be the ip address of external peer where the prefix was learned.

- This is a well-known mandatory attribute.

## LOCAL_PREF

- LOCAL_PREF is an attribute that is only shared with iBGP neighbors not eBGP neighbors. The LOCAL_PREF does not leave the AS. A route will share the LOCAL_PREF to iBGP neighbors to dictate where traffic will be preffered. 

- The highest LOCAL_PREF is preffered and chosen for those routes.

- Ths is a well-known discretionary attribute.

## MULTI_EXIT_DISC (MED)

- The MULTI_EXIT_DISC can influence incoming traffic from external AS. This attribute is actually carried in EBGP update messages and will tell another AS its preferred ingress point. MEDs are only used to influence traffic between two directly connected AS and will not pass onto others.

- The lowest MED value is the preffred value for routes.

- This is an optional non-transitive attribute.

## ATOMIC_AGGREGATE & AGGREGATOR

- The ATOMIC_AGGREGATE and AGGREGATOR are two seperate path attributes but go hand and hand. When routes are summarized and then advertised via BGP the AS_PATH information is lost on the route. The adveriser of the route removes all other AS#s and instead add it's own. The ATOMIC_AGGREGATE attribute is added to warn neighbors that "Hey I am advertising a summarized route the AS info was lost". 

- The ATOMIC_AGGREGATE never leaves the route when passed onto other neighbors

- This is a well-known discretionary attribute.

## AGGREGATOR

- The AGGREGATOR is an optional path attribute that a BGP speaker can use when when the ATOMIC_AGGREGATE has been set. This attribute provides information about wher the aggregation was performed. This will include the AS# and IP address of the router that originated the aggregate route.

- This is an optional transitive attribute.

## COMMUNITY

- The COMMUNITY attribute can be used to tag routes to modify routing attiributes. For example I can tag routes from Group A all with a COMMUNITY attribute. This way I can change MED or LOCAL_PREF attributes based upon the COMMUNITY.

- There are 4 well known COMMUNITY groups
	- Internet: All routes belong here by default. Routes can be advertised to all BGP neighbors.
	- No-Advertise: Routes cannot be advertised at all.
	- No-Export: Routes receiving this value cannot be advertised to eBGP peers.
	- Local-AS: Routes with this cannot be advertised to eBGP peers and stay within the AS.

- This is an optional transitive attribute.

## ORIGINATOR_ID

- ORIGINATOR_ID is used by route reflectors and used for preventing route loops. This is created by the route reflector and if the router see its RID in this attribute it knows to ignore the route because a loop has occured.

- This is an optional non-transitive attribute.

## CLUSTER_LIST

- CLUSTER_LIST is also used by route reflectors. This is a sequence of route reflector ID's in which the route has passed through. If a route reflector see its local cluster ID here in a received route it, a loop has occured and the route is ignored.

- This is an optional non-transitive attribute.

## WEIGHT

- This is a Cisco specific attribute that only exists on the local router. This is not shared with any other router.

- The weight can be assigned to a route the higher the weight the more preffered the route. Weight is considered above all attributes on Cisco devices.

- A number between 0-65,535 can be used for Weight.
