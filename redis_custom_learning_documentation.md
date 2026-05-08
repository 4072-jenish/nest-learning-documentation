# Redis — Custom Learning Documentation 🚀

## Introduction

Redis is an in-memory database and caching system designed for extremely fast data access. Unlike traditional databases that store data on disk, Redis stores data directly inside RAM (memory), which makes read and write operations very fast.

Redis is mainly used to:

- Improve backend performance
- Reduce database load
- Speed up repeated API requests
- Store temporary data
- Handle caching systems
- Manage sessions and rate limiting

---

# Core Understanding Of Redis

The main idea behind Redis is:

```txt
Store frequently requested data in memory so the backend does not repeatedly query the database.
```

Without Redis, every request directly queries the database.

Example:

```txt
Client
   ↓
Backend
   ↓
Database
   ↓
Response
```

If thousands of users request the same data repeatedly, the database performs the same query many times, increasing load and reducing performance.

Redis solves this problem by acting as a fast-access layer between the backend and database.

---

# Redis Cache Flow

The caching flow implemented during learning:

```txt
Client Request
      ↓
Backend API
      ↓
Check Redis Cache
      ↓
If Cache Exists:
      Return Cached Data
Else:
      Fetch Data From Database
      Store Data In Redis
      Return Response
```

This reduces unnecessary database queries and improves response speed.

---

# Cache Hit & Cache Miss

## Cache Hit

A cache hit happens when Redis already contains the requested data.

Example:

```txt
categories:list
```

exists inside Redis.

Flow:

```txt
Request
   ↓
Redis returns data instantly
   ↓
Database query skipped
```

This improves API performance significantly.

---

## Cache Miss

A cache miss happens when Redis does not contain the requested data.

Flow:

```txt
Request
   ↓
Redis returns null
   ↓
Backend queries database
   ↓
Database result stored in Redis
   ↓
Response returned
```

This is how cache gets generated dynamically.

---

# Lazy Cache Generation

One important concept learned was:

```txt
Redis cache is usually generated automatically on first request.
```

The cache does not need to be manually inserted beforehand.

First request creates the cache.
Future requests reuse it.

---

# Cache Invalidation

Another important concept learned was cache invalidation.

Problem:

When data changes in database:

- POST
- PUT
- DELETE

existing Redis cache becomes outdated.

Solution:

Clear the cache after data modification.

Example:

```txt
redis.del("categories:list")
```

This forces Redis to rebuild fresh cache during next request.

---

# Redis Expiration Time

Redis supports automatic cache expiration.

Example:

```txt
60 seconds
```

After expiration:

```txt
Redis automatically removes cached data.
```

This prevents old data from remaining in memory forever.

---

# Data Serialization

Redis stores data as strings.

Because JavaScript objects and arrays cannot be directly stored, data must be converted.

## Storing Data

```txt
JSON.stringify(data)
```

## Reading Data

```txt
JSON.parse(data)
```

This serialization process was required during Redis implementation.

---

# Runtime Understanding

One major learning outcome was understanding runtime environments.

## Browser Runtime

Used by frontend applications.

Supports:

- window
- document
- localStorage

---

## Node.js Runtime

Traditional backend runtime.

Supports:

- TCP sockets
- fs module
- net module
- traditional Redis clients

---

## Edge Runtime

Used by:

- Cloudflare Workers
- Edge Functions

Optimized for:

```txt
fetch()
```

instead of Node.js APIs.

---

# Why Traditional Redis Failed

Initially, a traditional Redis package was used.

Problem:

```txt
Cloudflare Workers Edge Runtime does not support TCP socket connections.
```

Traditional Redis packages require:

```txt
TCP socket communication
```

which Edge runtime blocks.

---

# Upstash Redis Understanding

To support Edge Runtime, an HTTP-based Redis system was used.

Upstash Redis communicates through:

```txt
HTTP REST API
```

instead of TCP sockets.

This allows Redis usage inside Cloudflare Workers using:

```txt
fetch()
```

requests.

---

# Cloudflare Workers Learning

Cloudflare Workers use:

```txt
Edge Runtime
```

instead of Node.js runtime.

Important differences learned:

## Node.js

```txt
process.env
```

## Cloudflare Workers

```txt
c.env
```

Cloudflare Workers also use fetch-based architecture instead of traditional server architecture.

---

# D1 Database Learning

During implementation, D1 database behavior was also explored.

Learned that:

```txt
Local D1 database is simulated locally inside .wrangler.
```

Deleting:

```txt
.wrangler
```

can reset local database state.

---

# CORS & Backend Debugging

During Redis integration, multiple backend debugging concepts were explored:

- CORS configuration
- OPTIONS preflight requests
- Allowed request headers
- Cloudflare Access headers
- Backend response handling

This helped understand how browsers validate backend requests before sending actual API calls.

---

# Frontend & Backend Response Structure

Another important debugging issue encountered:

```txt
categories.map is not a function
```

This happened because frontend expected:

```txt
Array response
```

while backend returned:

```txt
Object/String response
```

This highlighted the importance of maintaining correct response structures between frontend and backend systems.

---

# Packages Explored During Learning

Packages used during Redis learning:

```txt
@upstash/redis
wrangler
hono
```

---

# What Was Implemented

During this learning process, the following systems were implemented:

- Redis caching flow
- Cache hit & cache miss handling
- Cache invalidation system
- Edge-compatible Redis integration
- Redis REST API communication
- Backend category caching system
- HTTP-based Redis helper
- Cloudflare Workers runtime integration

---

# Final Understanding

Redis is not designed to permanently replace traditional databases.

Redis is mainly used as:

```txt
A fast temporary access layer.
```

Its primary purpose is improving backend performance and reducing unnecessary database operations.

---

# Final Mental Model

```txt
Client Request
      ↓
Backend
      ↓
Redis Cache Check
      ↓
Cache Exists?
   ↙           ↘
YES             NO
↓               ↓
Return Cache    Query Database
                ↓
                Store In Redis
                ↓
                Return Response
```

---

# Most Important Learning

```txt
Not every JavaScript package works in every runtime environment.
```

Understanding runtime compatibility, caching systems, backend architecture, and edge runtime limitations became one of the most important learning outcomes from this Redis implementation journey.

