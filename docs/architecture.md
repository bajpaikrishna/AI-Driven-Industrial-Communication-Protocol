# AICP Architecture

## Overview
The AICP protocol is designed around a layered architecture that separates concerns related to data serialization, transport, networking, and physical layer integration. Each layer has specific responsibilities, which together enable real-time AI communication.

## Layered Architecture

### 1. Application Layer
- **Responsibilities**: Handles AI-specific data formats, tensor serialization, metadata management, and task prioritization.
- **Components**:
  - Tensor Serialization (`tensor_serializer.c`)
  - Metadata Handling (`metadata_handler.c`)
  - Priority Tagging (`priority_manager.c`)

### 2. Transport Layer
- **Responsibilities**: Responsible for packet creation, fragmentation, reassembly, and ensuring reliable data transfer using hybrid mechanisms like FEC and ACK clustering.
- **Components**:
  - Packet Management (`packet_manager.c`)
  - Reliability Management (`reliability_manager.c`)

### 3. Network Layer
- **Responsibilities**: Focuses on edge-centric routing and dynamic path selection, allowing the protocol to adapt to network conditions in real-time.
- **Components**:
  - Edge Routing (`edge_router.c`)
  - Path Optimization (`path_optimizer.c`)

### 4. Physical Layer
- **Responsibilities**: Integrates Time-Sensitive Networking (TSN) for deterministic data delivery and bandwidth reservation.
- **Components**:
  - TSN Support (`tsn_support.c`)
  - Bandwidth Management (`bandwidth_manager.c`)

### 5. Security Layer
- **Responsibilities**: Provides encryption and authentication for secure communication.
- **Components**:
  - Encryption (`encryption.c`)
  - Authentication (`auth.c`)

## Communication Flow
1. The **Application Layer** prepares and serializes AI data (e.g., tensors) with metadata.
2. The **Transport Layer** handles the creation and transmission of packets, applying reliability mechanisms.
3. The **Network Layer** routes packets through the network, optimizing paths dynamically.
4. The **Physical Layer** ensures the packets are delivered deterministically with TSN support.
5. The **Security Layer** encrypts and authenticates data to secure the communication.
