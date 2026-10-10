# Day 68 - Consistent Hashing

Repository: https://github.com/Greycode009/Development-Series

## What I Learned

Today I learned how consistent hashing helps distribute keys across multiple servers while minimizing unnecessary key movement when servers are added or removed.

## 1. The Problem with Simple Hashing

A simple way to assign a key to a server is to use the modulo operator:

```text
server = hash(key) % numberOfServers
```

For example, if there are 3 servers, a key is assigned based on the hash result modulo 3.

The problem appears when the number of servers changes. If we add or remove a server, the modulo result can change for many keys. Those keys may be assigned to different servers, causing unnecessary data movement and cache misses.

## 2. What Is Consistent Hashing?

Consistent hashing is a technique for assigning keys to servers in a way that minimizes how many keys need to move when the server group changes.

It is commonly useful in distributed systems, such as distributed caching.

## 3. The Hash Ring

Consistent hashing represents the hash space as a ring.

- Servers are placed at positions on the ring.
- Keys are also placed at positions on the ring.
- To find the server for a key, move clockwise from the key's position.
- The first server encountered is responsible for that key.

```text
                 [Server A]
                /           \
               /             \
          key: user:101       |
             |                |
          (clockwise)      [Server B]
               \             /
                \           /
                 [Server C]
```

This is a simplified illustration of the idea. The actual positions are determined by hashing.

## 4. Adding a Server

Suppose a new server, Server D, is added to the ring.

Only keys in the affected region may be reassigned to Server D. Keys whose first clockwise server remains the same can stay where they are.

This is the main advantage over simple modulo-based hashing: **most keys do not need to move when a server is added.**

## 5. Removing a Server

If Server B is removed, the keys that were assigned to Server B are reassigned to the next available servers according to the clockwise rule.

Keys already assigned to other servers generally remain there.

Consistent hashing does not mean that no keys move. It means that it minimizes unnecessary movement.

## 6. Load Distribution

Consistent hashing can still distribute keys unevenly. For example, one server might receive a much larger share of keys than the others.

An overloaded server may respond more slowly or reach its capacity while other servers have spare resources.

A common technique for improving distribution is **virtual nodes**. Instead of placing each physical server at only one position on the ring, a server is represented by multiple positions. This can help distribute keys more evenly.

Virtual nodes were introduced today and will be explored further in the next lesson.

## 7. Simple Hashing vs. Consistent Hashing

| Simple modulo hashing | Consistent hashing |
| --- | --- |
| Uses the number of servers in the modulo calculation. | Places servers and keys on a hash ring. |
| Adding or removing a server can change assignments for many keys. | Usually only keys in the affected region need to move. |
| Can cause many cache misses after a server-count change. | Helps minimize unnecessary key movement. |

## Key Takeaway

Consistent hashing assigns keys to servers using a hash ring and the clockwise rule. When servers are added or removed, it minimizes how many keys need to move. Virtual nodes can help improve load distribution across servers.
