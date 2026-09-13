

**Forwarding** refers to moving packet from single router

**Routing** is how routers work together to find the good routes to move data.

**Intraroutinq** involves input and output for a single router.

**Interouting** involves multiple routers to move data.

Time delay to traverse the link is what the hops represent in the graph.

## Link state routing

![](03_intradomain_routing-1789333820636.jpeg)

We start with the initialization step, where we set all the currently known least-cost paths from u to it’s directly attached neighbors v, x and w. For the rest of the nodes in the network we set the cost to infinity, because they are not immediate neighbors to source node u. We also initialize the set N' to include only the source node u. The first row in our table represents the initialization step.  

In the first iteration, we look among the nodes that are not yet in N’, and we select the node with the least cost from the previous iteration. In this case, this is node x. Then we update D for all the immediate neighbors of x, which in this case are nodes v, w, and y. For example, we update D(w) as the minimum between: the cost we had from the previous iteration which is 5, and the cost from u to x (1) plus cost from x to w (3). The minimum between the two is 4. We update the second row in our table. 

We continue in a similar manner for the rest of the nodes in the table. The algorithm exits in the 5th iteration.

![](03_intradomain_routing-1789335588136.jpeg)

### Complexity

$$
n(n+1) / 2
$$

## Distance vector (Belford-Ford)

$$
Dx(y) = minv{c(x,v) + Dv(y)}
$$
![](03_intradomain_routing-1789336071720.jpeg)

## Failures in Distance Vector

The count to infinity problem:

![](03_intradomain_routing-1789337418353.jpeg)

Let’s assume that the link y-x has a new cost of 60. 

1. At t0, y detects that the cost has changed, and now it will update its distance vector thinking that it can still reach x through z with a total cost of 5+1=6.
2. At t1, we have a routing loop where z thinks it can reach x through y, and y thinks it can reach x through z. This will cause the packets to be bouncing back and forth between y and z until their tables change. 
3. Nodes z and y keep updating each other about their new cost to reach x. For example, y computes its new cost to be 6 and then informs z. Then z computes its new cost to be 7, and then informs y, and so on. 

This back and forth continues for a total of 44 iterations, at which point z computes its cost to be larger than 50, and at that point it will prefer to reach x directly rather than through y. 

In contrast to the previous scenario, this link cost change took a long time to propagate among the nodes of the network. This is known as the count-to-infinity problem. 

Understanding why it is 5 in step 1 is one of the keys to understanding the count-to-infinity problem.

All of the nodes have their own table. So, Node Y detected the change, but Node Z didn't. Node Y sees that Node Z has a path to x with a cost of 5. So, it may be easier to interpret the equation as (cost of y->x) = 1 + 5 = (cost of link y->z) + (cost of z->x, which is stored in Node Z's DV).

Pause to make sure you see where the count-to-infinity problem shows up. Since Node Y advertises a cost of 6, Node Z updates and its cost to 7, and the process repeats.
