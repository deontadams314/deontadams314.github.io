---
published: true
---
# **BGP - N WLLA OMNI**

I know what your thinking, N WLLA OMNI, is that weird dive bar that I should know about? No, N WLLA OMNI is the acronym for the BGP decision process. When a BGP router has multiple routes to an NLRI it must choose the best path to the NLRI. To figure out the best path this is where N WLLA OMNI comes into play. It is a rather deep system BGP uses to choose the best path. Here we will discuss the decision process in detail so it can become easier to understand and remember.

## The Decision Process

There are 9 total steps in the decision process with 3 additional tie-breaker steps. Let's take a look and see how BGP decides the best route to an NLRI when multiples exist.

1) Is the NEXT_HOP reachable?: If a router does not have a route next to the NEXT_HOP path atrribute, the route should then be rejected.

2) Highest Weight: Weight is a Cisco propriety feature so you will most likely not see this on other vendors. This attribute it set locally on the router to the NLRI and is not advertised to other routers. The higher the Weight the better the route.

3) Highest LOCAL_PREF: The higher the LOCAL_PREF the better the route. This is a well-known discretionary path attribute and is only used in iBGP. This attribute does not leave the AS and all routers within the AS can configure this attribute to choose the same exit route to an NLRI.

4) Locally Injected Routes: Choose the route locally injected into BGP (via network cmd, summarization or redistribution). Better than iBGP/eBGP learned routes.

5) Shortest AS_PATH length: AS_PATH is the attribute that shows the AS numbers that the NLRI has passed through. The shorter the AS_PATH the better the route.

6) ORIGIN attribute: IGP routes (I) are preferred over EGP (E) routes. Which is then preferred over incomplete (?) routes, You should rarely see EGP routes being BGP is the successor to EGP.

7) Smallest MED attribute:  The smaller the MED value the better the route. The MED attribute is an optional transitive attribute. Typically a sender will use MED to tell a receiving peer with multiple connections to them the better pathway to an NLRI. 

8) Neighbor Type: eBGP routes are preferred over iBGP routes. Confedration eBGP routes are treated as equal to iBGP.

9) IGP metric for reaching the NEXT_HOP: Compare the IGP metrics of the NEXT_HOP of an NLRI. The lower the metric the better the route.

## Tiebreaker Steps

If a best path is not determined after going through steps 1-9, 3 tiebreaker steps are used to find the best path to a NLRI. They are as follows:

10) Keeps the oldest eBGP route. If the routes being compared are eBGP routes  and one of the paths is currently the best path, then keep that route as the best path.

11) Choose the route whose next-hop router ID (RID) is the smallest.

12) Choose the smallest neighbor ID. If a router has at least two neighbor connections with a single router, the router will prefer the route advertised by the lowest neighbor ID listed in the routers neighbor commands.

## N WLLA OMNI

The bread and better of the post and what we all have been waiting for. Here is the acronym used to help memorize this 9 step decision process.

- NEXT_HOP reachable?

- WEIGHT
- LOCAL_PREF
- Locally Injected
- AS_PATH length

- ORIGIN
- MED
- Neighbor Type
- IGP Metric to NEXT_HOP

## Key Things to Note

- The decision process is only used to find one best path to reach an NLRI. It is not used to find multiple equal routes to install them into the routing table.

- If a step determines the best route the process ends at that step and does not move forward. For example, if LOCAL_PREF determines the best path it will not look at locally injected routes or AS_PATH.

