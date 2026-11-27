# Day-18-Azure Load Balancer

# 1. What is Load Balancing?

```text
                    Internet
                       |
                       |
                +--------------+
                | Load Balancer|
                +--------------+
                  /          \
                 /            \
          +---------+      +---------+
          | Web VM 1|      | Web VM 2|
          +---------+      +---------+
```

Without a load balancer:

```text
User
  |
  v
Web Server 1
```

If Web Server 1 fails:

```text
User
  |
  X
Server DOWN
```

With load balancing:

```text
             User
               |
               v
       Azure Load Balancer
          /           \
         v             v
     Web VM 1       Web VM 2
```

The load balancer distributes traffic across healthy backend instances.

---

