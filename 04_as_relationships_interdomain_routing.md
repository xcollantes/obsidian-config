
provider and sucteorm relationship based on financial settlement on how much the customer will pay the provider.

as long as the two peers are not highly asymeetric.

Smaller ISPs will peer base on need of similar size.

provider ASes have a financial incentive to forward as much of their customers' traffic as possible.

In this chapter we're using GCP but other method exists such as RIP.

- **Routes learned from customers:** These are the routes X receives as advertisements from its customers. Since provider X is getting paid to provide reachability to a customer AS, it makes sense that X wants to advertise these customer routes to as many neighboring ASes as possible. This will likely cause more traffic toward the customer (through X) and, hence, more revenue for X.   
- **Routes learned from providers:** These are the routes X receives as advertisements from its providers. Advertising these routes does not make sense since X has no financial incentive to carry traffic for its provider's routes. Therefore, these routes are withheld from X's peers and X's other providers, but they are advertised to X's customers.  
- **Routes learned from peers:** These are routes that X receives as advertisements from its peers. As we saw earlier, it does not make sense for X to advertise to provider A the routes it receives from provider B. Because in that case, providers A and B will use X to reach the advertised destinations without X making revenue. The same is true for the routes that X learns from peers.

