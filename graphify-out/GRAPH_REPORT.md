# Graph Report - /home/aarav/CP  (2026-05-09)

## Corpus Check
- Corpus is ~4,198 words - fits in a single context window. You may not need a graph.

## Summary
- 72 nodes · 84 edges · 17 communities (13 shown, 4 thin omitted)
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 7 edges (avg confidence: 0.83)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Sender Server Logic|Sender Server Logic]]
- [[_COMMUNITY_Core Protocol Components|Core Protocol Components]]
- [[_COMMUNITY_Receiver Node Implementation|Receiver Node Implementation]]
- [[_COMMUNITY_Sender Node Implementation|Sender Node Implementation]]
- [[_COMMUNITY_Packet SerializationCRC|Packet Serialization/CRC]]
- [[_COMMUNITY_Config Loading|Config Loading]]
- [[_COMMUNITY_Session Structure|Session Structure]]
- [[_COMMUNITY_Config Object|Config Object]]
- [[_COMMUNITY_Integrity Echo Mechanism|Integrity Echo Mechanism]]

## God Nodes (most connected - your core abstractions)
1. `send()` - 9 edges
2. `processPacket()` - 6 edges
3. `sendToAgent()` - 5 edges
4. `eventLoop()` - 4 edges
5. `sendToSession()` - 4 edges
6. `checkTimers()` - 4 edges
7. `abortSession()` - 4 edges
8. `CPServer` - 4 edges
9. `CPReceiverNode` - 4 edges
10. `computeCRC32()` - 3 edges

## Surprising Connections (you probably didn't know these)
- `connect()` --calls--> `send()`  [INFERRED]
  receiver/cp_receiver_node.cpp → sender/cp_sender_node.cpp
- `heartbeatLoop()` --calls--> `send()`  [INFERRED]
  receiver/cp_receiver_node.cpp → sender/cp_sender_node.cpp
- `sendPacket()` --calls--> `send()`  [INFERRED]
  receiver/cp_receiver_node.cpp → sender/cp_sender_node.cpp
- `CPServer` --conceptually_related_to--> `CPReceiverNode`  [INFERRED]
  sender/cp_server.hpp → receiver/cp_receiver_node.hpp
- `processPacket()` --calls--> `send()`  [INFERRED]
  sender/cp_server.cpp → sender/cp_sender_node.cpp

## Hyperedges (group relationships)
- **CP Protocol Architecture** — cp_server_cpserver, cp_sender_node_cpsendernode, cp_receiver_node_cpreceivernode [INFERRED 0.95]
- **Distributed Session Flow** — cp_session_cpsession, cp_packet_cppacket, cp_types_dialoguerole [INFERRED 0.85]

## Communities (17 total, 4 thin omitted)

### Community 0 - "Sender Server Logic"
Cohesion: 0.27
Nodes (10): abortSession(), checkTimers(), CPServer(), eventLoop(), handleClientData(), handleNewConnection(), processPacket(), sendToAgent() (+2 more)

### Community 1 - "Core Protocol Components"
Cohesion: 0.27
Nodes (10): CPCrypto, CPPacket, CPReceiverNode, CPSenderNode, CPServer, CPSession, DialogueRole, SessionState (+2 more)

### Community 2 - "Receiver Node Implementation"
Cohesion: 0.28
Nodes (6): connect(), CPReceiverNode(), disconnect(), heartbeatLoop(), run(), sendPacket()

### Community 3 - "Sender Node Implementation"
Cohesion: 0.39
Nodes (6): connect(), CPSenderNode(), disconnect(), heartbeatLoop(), isConnected(), send()

### Community 4 - "Packet Serialization/CRC"
Cohesion: 0.47
Nodes (3): computeCRC32(), init_crc32(), serialize()

## Knowledge Gaps
- **5 isolated node(s):** `CPSession`, `SessionState`, `CPConfig`, `Receiver Main`, `Integrity Echo Mechanism`
  These have ≤1 connection - possible missing edges or undocumented components.
- **4 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `send()` connect `Sender Node Implementation` to `Sender Server Logic`, `Receiver Node Implementation`?**
  _High betweenness centrality (0.117) - this node is a cross-community bridge._
- **Why does `processPacket()` connect `Sender Server Logic` to `Sender Node Implementation`?**
  _High betweenness centrality (0.045) - this node is a cross-community bridge._
- **Why does `sendToAgent()` connect `Sender Server Logic` to `Sender Node Implementation`?**
  _High betweenness centrality (0.038) - this node is a cross-community bridge._
- **Are the 5 inferred relationships involving `send()` (e.g. with `processPacket()` and `sendToAgent()`) actually correct?**
  _`send()` has 5 INFERRED edges - model-reasoned connections that need verification._
- **What connects `CPSession`, `SessionState`, `CPConfig` to the rest of the system?**
  _5 weakly-connected nodes found - possible documentation gaps or missing edges._