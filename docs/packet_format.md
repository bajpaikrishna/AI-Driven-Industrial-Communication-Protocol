# AICP Packet Format

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
```

This should now correctly display the packet structure in a chart format, followed by an example of the serialized data. You can now copy and paste this directly into your markdown file.