Perfect ✅
Here’s a **clean architecture diagram + explanation in English** that you can put directly in your `README.md`.

---

# 🚀 Redis with Docker Compose – All-in-One Setup

This `docker-compose.yml` provides **multiple Redis deployment scenarios** in a single environment:

* **Standalone Redis** (simple dev/test)
* **Redis Master/Replica with Sentinel** (High Availability)
* **Redis Cluster (3 masters + 3 replicas)** (Sharding & Scalability)
* **RedisInsight UI** (Web management tool)

---

## 📐 Architecture Overview

### 1. Standalone Redis

A single Redis server with persistence and password authentication.
Best for **development or quick tests**.

```
   ┌───────────────┐
   │ redis-standalone │
   └───────────────┘
```

---

### 2. Redis Master/Replica + Sentinel (High Availability)

* **1 Master**
* **2 Replicas**
* **1 Sentinel** (can be scaled to 3 for production)
  Sentinel monitors the master, and if it fails, promotes a replica to master.

```
          ┌───────────────┐
          │  redis-master │◄─────────┐
          └───────▲───────┘          │
                  │                   │
          ┌───────┴───────┐   ┌───────┴───────┐
          │ redis-slave1  │   │ redis-slave2  │
          └───────▲───────┘   └───────▲───────┘
                  │                   │
          ┌───────┴───────┐
          │   Sentinel    │
          └───────────────┘
```

---

### 3. Redis Cluster (Sharding & Scalability)

* **3 Masters** (data sharded across hash slots)
* **3 Replicas** (each master has one replica)
  Ensures **scalability** and **data distribution**.

```
       ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
       │ Master #1   │       │ Master #2   │       │ Master #3   │
       │ (hash slot) │       │ (hash slot) │       │ (hash slot) │
       └──────▲──────┘       └──────▲──────┘       └──────▲──────┘
              │                     │                     │
       ┌──────┴──────┐       ┌──────┴──────┐       ┌──────┴──────┐
       │ Replica #1  │       │ Replica #2  │       │ Replica #3  │
       └─────────────┘       └─────────────┘       └─────────────┘
```

---

### 4. RedisInsight (UI)

A web interface (port `8001`) to connect, monitor, and manage any Redis instance (Standalone, Sentinel, or Cluster).

```
   ┌───────────────────┐
   │   RedisInsight UI │
   └───────────────────┘
```

---

## 🛠️ How to Run

```bash
docker-compose up -d
```

* Standalone Redis → `localhost:6379`
* Redis Master → `localhost:6380`
* Redis Replica1 → `localhost:6381`
* Redis Replica2 → `localhost:6382`
* Sentinel → `localhost:26379`
* Redis Cluster → `localhost:7000-7005`
* RedisInsight → [http://localhost:8001](http://localhost:8001)

---

⚡ Tip:

* For **production HA**, run **3 Sentinel containers** instead of one.
* For **secure environments**, update strong passwords in `docker-compose.yml` and `sentinel.conf`.

---

Would you like me to also generate a **Markdown diagram (using Mermaid)** so that your README renders the architecture visually on GitHub without external images?
