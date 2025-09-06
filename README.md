# CSCI-550: PostgreSQL Buffer Management Enhancement

## Project Overview
This project enhances **PostgreSQL 16.4** by introducing a **FIFO (First-In-First-Out) buffer replacement strategy** alongside the existing **LRU Clock-Sweep** algorithm.  
The FIFO strategy manages buffers in strict queue order, replacing the oldest buffer first when needed.  

This work was developed as part of **CSCI-550 (Advanced Database Systems)** at USC.

---

## Files Modified
- `src/backend/storage/buffer/freelist.c`  

---

## Key Changes
1. Implemented a **FIFO queue (FifoQueue)** to track buffers in insertion order.  
2. Added functions to **enqueue (enqueueBuffer)** and **dequeue (dequeueBuffer)** buffers from the queue.  
3. Modified buffer selection logic (`GetNewBuffer` and `GetVictimBuffer`) to integrate FIFO.  
4. Introduced a toggle flag (`enable_fifo`) in `BufferStrategyControl` to switch between **FIFO** and **LRU Clock-Sweep**.  
5. Updated `StrategyGetBuffer` to dynamically select the appropriate replacement strategy.  

---

## Usage
- Set the `enable_fifo` flag:  
  - `enable_fifo = true` → Buffers are allocated/replaced using **FIFO**.  
  - `enable_fifo = false` → PostgreSQL’s default **LRU Clock-Sweep** strategy is used.  

---

## Results
- With **FIFO enabled**, buffer replacement follows strict insertion order.  
- With **LRU Clock-Sweep**, PostgreSQL’s adaptive buffer strategy is preserved.  

---

## Attribution
This project builds on the official [PostgreSQL 16.4 source code](https://www.postgresql.org/).  
The modifications here are for **educational purposes only** and represent enhancements implemented by our group.  
