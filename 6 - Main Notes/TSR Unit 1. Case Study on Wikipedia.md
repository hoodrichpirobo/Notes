
2025-09-17 13:24

Status: #child #lectures 

Tags: 

# TSR Unit 1. Case Study on Wikipedia

## From the user point of view

Wikipedia is a great example of a large distributed service
Instead of hiring millions of experts, lot of the work is left to volunteers
"Wiki" technology is synonymous with: 
- collaborative edition of contents
- a history of the updates applied on each page

## Going into the computer scientist pov

*LAMP = Linux + Apache + MySQL + PHP*

MediaWiki is a LAMP system

Relational databases usually does not go well with scalibility, which can be the case for MySQL, which is a [[RDBMS]].

### MediaWiki

#### Wikipedia @ LAMP — why it scales (quick notes)

* **Peak load assumption:** \~27,774 requests/s.
* **Bandwidth math:** `req/s × page_size(KB) × 8 / 1,000,000` → **≈ 251–1602 Gbps** (for \~1,130–7,210 KB pages).
* **Single link can’t handle this.** If a server link is \~2,000 Mbps, worst-case needs **≈ 1,602,000/2,000 ≈ 801** such links → **hundreds of servers**.

**Therefore → multi-server architecture:**

* **Replication & sharding:** MySQL write master + many read replicas; big tables split.
* **Heavy caching:** CDN/edge + reverse proxy (e.g., Varnish/NGINX) + Memcached → most reads never hit DB.
* **Stateless app tier:** Many PHP/MediaWiki web nodes behind load balancers.
* **Trade-offs:** load balancing, cache invalidation, propagating edits (replication lag), failure handling.

**Takeaway:** Even on LAMP, Wikipedia scales by **distributing reads across cached replicas and many servers**, pushing writes to a master and minimizing DB work.

### [[MySQL]]

| Apache                             | MySQL               |
| ---------------------------------- | ------------------- |
| Replication                        | Passive replication |
| Caching, with Broker/Reverse proxy |                     |

### LAMP scaling — single-note summary

* **Front component** = edge service that first receives client requests (e.g., **load balancer** or **reverse proxy**); can do TLS, routing, caching, rate-limit, WAF.
* **Load balancer:** splits traffic across many Apache servers, removes unhealthy ones, optional sticky sessions.
* **Reverse proxy:** sits in front of Apache; forwards requests and **caches pages/assets**. On a cache hit it replies immediately → **Apache/MySQL are bypassed**.
* **Apache tier (replicated):** many identical, stateless web/app nodes behind the load balancer for horizontal scale.
* **Apache caching:** stores rendered HTML/API responses and static assets (CSS/JS/images) in memory/disk; cache hits are served by Apache without running PHP or querying MySQL.
* **MySQL (passive replication):** one **primary** handles writes; multiple async **read replicas** serve reads → reads scale out; **writes bottleneck at the primary** (possible replication lag).
* **Net effect:** most reads are served from caches; DB is touched mainly on cache misses and writes, enabling large-scale service on LAMP.
## References

[[TSR Unit 1. Introduction]], [[TSR Concepts.]]