---
description: >-
  Avail light client (LC) lets you interact with Avail DA without requiring a
  full node and without trust assumptions towards remote peers. This is
  accomplished by leveraging Data Availability Sampling
---

# Avail - Light Client

The Avail Light Client (LC) monitors finalized blocks on the network, utilizing Data Availability Sampling (DAS) to ensure data integrity. It connects to Avail nodes via WebSocket, conducting random sampling of block matrices to retrieve data cells. If needed, it uses both DHT and RPC methods for data retrieval, enhancing data availability.

LC functionality is divided into two parts: DAS-focused LC and app client for data reconstruction. LC operates independently, persisting block confidence locally. It synchronizes with nodes on startup and exposes an HTTP API for querying block status, confidence, and application data.

The Avail LC enhances data availability and integrity through random sampling, akin to full nodes, while reducing the load on them. It enables convenient access to application-specific data through its API, ensuring the reliability of data within the Avail network.

### Requirement

#### Minimum Hardware Requirement&#x20;

* CPU : 2 core
* Memory : 2 GB
* SSD : 300 GB (recomended)

#### Software Requirement

* Operating System : Ubuntu 22.0+

### Claim Faucet

* Link Faucet : [Here](https://faucet.avail.tools/)
