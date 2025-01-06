# AICP (AI-Driven Industrial Communication Protocol)

## Overview

AICP is a low-latency, secure, and scalable communication protocol optimized for AI-driven tasks in Industry 4.0 applications. It ensures deterministic delivery of AI workloads, handles high-priority tasks, and provides AI-specific optimizations for data transfer.

### Key Features:
- **AI-specific optimizations**: Adaptive data transfer with task prioritization.
- **Real-time synchronization**: Synchronize AI workloads across distributed systems.
- **Hybrid reliability mechanism**: Combining TCP-like reliability with UDP-like speed.
- **Tensor-Optimized Packetization**: Efficient serialization and deserialization of tensor data.
- **Security**: Homomorphic encryption for secure AI model transfer.

## Architecture

AICP's architecture is divided into multiple layers:

1. **Application Layer**:
   - Handles tensor-optimized data format, task prioritization, and AI workload metadata.

2. **Transport Layer**:
   - Manages packet creation, hybrid reliability, and acknowledgment clustering.

3. **Network Layer**:
   - Implements edge-centric routing and dynamic path selection.

4. **Physical Layer**:
   - Ensures deterministic delivery through Time-Sensitive Networking (TSN) and bandwidth reservation.
   - Simulates network transmission and reception for testing purposes.

5. **Security Layer**:
   - Provides encryption and decryption of packets to ensure secure transmission.

## Packet Structure (High-Level Overview)

The AICP packet includes the following fields:

- **Priority Level**: Defines the priority of the task (higher values = higher priority).
- **Task Type**: Defines the type of AI task (e.g., inference, training).
- **Timestamp**: UNIX timestamp for synchronization.
- **Tensor Metadata**: Contains information about the tensor such as dimensions and data type.
- **Payload**: The serialized tensor or model chunk.
- **Checksum**: Used for error detection.
- **Encryption Info**: Includes encryption metadata for secure transmission.

## Supported Tensor Types

| Tensor Type | Size (Bytes) | Use Case |
|-------------|--------------|----------|
| FLOAT32     | 4            | General-purpose, deep learning models |
| INT32       | 4            | Integer-based operations, indexing, categorical data |
| FLOAT64     | 8            | High-precision computations, scientific simulations |
| INT64       | 8            | Large-scale integer operations, time-series data |
| BOOL        | 1            | Flags, binary decisions |
| COMPLEX64   | 8            | Signal processing, neural networks with complex numbers |
| UINT8       | 1            | Image data, binary data processing |
| UINT16      | 2            | Image data, pixel intensities |
| UINT32      | 4            | Color data, indices |
| UINT64      | 8            | Large-scale integers, network tasks |
| BFLOAT16    | 2            | Memory-efficient ML models, especially on TPUs/GPU |
| HALF        | 2            | Memory-efficient deep learning model training/inference |
| STRING      | Variable     | Text data, NLP tasks |
| FLOAT16     | 2            | Memory optimization in deep learning |
| CUSTOM      | Variable     | Custom-defined data types |
| UNKNOWN     | 0            | Placeholder for unknown data types |

## Example of API

The following functions outline the high-level API that can be used to interact with the AICP protocol:

- **serialize_tensor(tensor, size, buffer, buffer_size)**:
  - Serializes tensor data into a byte buffer.
- **add_metadata_header(packet, task_type, priority)**:
  - Adds the task metadata header to the packet.

For full API documentation, please refer to the `docs/api_reference.md` file.

## Licensing

This project is licensed under the [Proprietary License](LICENSE) for commercial use. You are not permitted to share, distribute, or modify the code without explicit permission.

For more details, see the [LICENSE](LICENSE) file.
