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