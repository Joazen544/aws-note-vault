### What is TLS Offloading?
TLS (formerly SSL) is a network encryption protocol used to secure data transmission between clients and servers (e.g., HTTPS).

**TLS offloading** means:
> **Moving the task of TLS encryption/decryption from the backend servers to the load balancer.**

### What are the benefits?
1. **Reduces server load**: Backend servers don’t need to handle TLS processing and can focus on business logic.
2. **Centralized certificate management**: You only need to manage TLS certificates on the load balancer, not on every server.
3. **Easier to scale**: You can add backend servers without worrying about their TLS support.

### Example
If your service only has 100 users at a time, the backend servers can probably handle TLS without issue.

But for large platforms like YouTube or Shopee, which have hundreds of thousands or even millions of concurrent users, letting each backend server do its own TLS processing would overload them.

That’s where **TLS offloading with a Network Load Balancer** becomes very useful.

