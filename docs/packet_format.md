# AICP Packet Format

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

AICP packets are structured to efficiently carry AI workload data and ensure reliable communication. Each packet consists of the following fields:

| Field               | Size (Bytes) | Description                                      |
|---------------------|--------------|--------------------------------------------------|
| **Priority Level**   | 1            | The priority of the task (0-255). Higher values indicate higher priority. |
| **Task Type**        | 2            | The type of AI task (e.g., inference, training). |
| **Timestamp**        | 8            | A UNIX timestamp for packet synchronization across distributed systems. |
| **Tensor Metadata**  | Variable     | Information about the tensor (dimensions, data type, size). |
| **Payload**          | Variable     | Serialized tensor data or AI model chunk. |
| **Checksum**         | 4            | For error detection to ensure data integrity. |
| **Encryption Info**  | Variable     | Encryption-related metadata (e.g., encryption algorithm, key size). |

## Example Packet Structure

Here’s an example of how a packet might be structured:

| Priority Level | Task Type | Timestamp        | Tensor Metadata     | Payload       | Checksum | Encryption Info |
|----------------|-----------|------------------|---------------------|---------------|----------|------------------|
| 255            | 1         | 1609459200       | {3, float32, 12}    | [1.0, 2.0, 3.0] | 0x1a2b3c4d | AES-GCM, 256-bit |

## Example of Serialized Packet

A serialized packet might look like this (in raw bytes or hexadecimal):

```
[0xFF, 0x01, 0x60, 0x59, 0x59, 0x00, 0x00, 0x00, 0x00, 0x00, 0x03, 0x66, 0x6C, 0x6F, 0x61, 0x74, 0x33, 0x00, 0x00, 0x00, 0x01, 0x02, 0x03, 0x01, 0x02, 0x03, 0x04, 0x5A, 0x2B, 0x3C, 0x4D, 0xE5, 0xB9, 0xF1, 0x3C, 0x07, 0xF4, 0x9A, 0x58, 0x60, 0x56, 0x9F, 0x12]
```

### Explanation of Serialized Packet:

- **0xFF**: Priority Level (255, highest priority).
- **0x01**: Task Type (1, indicating inference).
- **0x60, 0x59, 0x59, 0x00, 0x00, 0x00, 0x00, 0x00**: Timestamp (1609459200).
- **0x03, 0x66, 0x6C, 0x6F, 0x61, 0x74, 0x33**: Tensor Metadata (`{3, float32, 12}`).
- **0x01, 0x02, 0x03**: Serialized tensor data (`[1.0, 2.0, 3.0]`).
- **0x5A, 0x2B, 0x3C, 0x4D**: Checksum (for error detection).
- **0xE5, 0xB9, 0xF1, 0x3C, 0x07, 0xF4, 0x9A, 0x58, 0x60, 0x56, 0x9F, 0x12**: Encryption Info (AES-GCM, 256-bit).