

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

### Complexity

```latex
n(n+1) / 2
```