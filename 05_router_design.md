Basic components:

- Forwarding or switching fx:

Control plane: Software switches
Data plane:

Types of switching:

- Via memory: I/O ports operate as I/O copied by memory
- Via bus: using a shared bus labeled using headers
- Via interconnection network: crossbar switch

Which plane operates on a shorter timescale? **Data**

The data plane forwards each packet in nanoseconds, usually in switch or router hardware. The control plane computes routes over seconds (routing protocol updates, SDN controller decisions). The management plane handles configuration and monitoring over minutes, hours, or days.

The split rests on one test: does the task act on each packet as it passes through (data plane), or does it build the rules and state the forwarding hardware later follows (control plane)?

1. **Computing paths (Control).** Algorithms such as Dijkstra in OSPF run periodically over topology information to pick routes. No individual packet triggers the computation.
2. **Layer 3 forwarding (Data).** The router looks up each packet's destination IP in the forwarding table and sends the packet out the matching port. This happens per packet, in nanoseconds, often in ASICs.
3. **Layer 2 switching (Data).** The switch looks up each frame's destination MAC in its table and forwards the frame. Same per-packet pattern as #2, one layer down.
4. **Building a routing table (Control).** Protocols such as OSPF and BGP exchange messages with neighbors to learn reachability. The resulting table then gets installed into the forwarding hardware for the data plane to use.
5. **Spanning Tree (Control).** STP exchanges BPDUs between switches to compute a loop-free topology and decide which ports to block. The data plane then forwards frames only on the unblocked ports.
6. **Decrementing TTL (Data).** Every router subtracts 1 from each packet's TTL as part of forwarding the packet. No routing decision happens here; the operation runs on every packet in the forwarding path.
7. **IP header checksum (Data).** Changing the TTL changes the header, so the router recomputes or incrementally updates the checksum for each packet before sending it out. Same per-packet work as #6.
8. **Configuring a load-balancing middlebox (Control).** This logic decides the policy: which servers receive traffic and in what proportion. The output consists of rules, pushed to the device ahead of time.
9. **Forwarding by installed middlebox rules (Data).** The middlebox matches each packet against the rules from #8 and forwards the packet accordingly. The pattern pairs

Which, if any, of the following types of switching can send multiple packets across the fabric in parallel?  

 Interconnection Network / Crossbar