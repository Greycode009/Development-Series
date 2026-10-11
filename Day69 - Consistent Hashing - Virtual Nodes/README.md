# Day 69 - Consistent Hashing


## What I Learned

Today I learned about virtual nodes and how they help improve key distribution in consistent hashing.

## Virtual Nodes

Virtual nodes give each physical server multiple positions on the hash ring. This can help distribute keys more evenly across servers.

## Adding Servers

When a new server is added, only some keys need to move to the new server. Most keys can remain assigned to their existing servers.

## Load Distribution

Virtual nodes can help balance the load, but they do not guarantee that every server receives exactly the same number of keys. The distribution depends on the positions of the virtual nodes on the ring.

## Key Takeaway

Virtual nodes help improve key distribution in consistent hashing while keeping key movement limited when servers are added.
