# AICP API Reference

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

## Application Layer

### `int serialize_tensor(const float *tensor, size_t size, char *buffer, size_t buffer_size)`
- **Description**: Serializes a tensor (array of floats) into a buffer for transmission.
- **Parameters**:
  - `tensor`: The tensor to serialize.
  - `size`: The number of elements in the tensor.
  - `buffer`: The buffer to store the serialized data.
  - `buffer_size`: The size of the buffer.
- **Returns**: The number of bytes written to the buffer, or -1 if the buffer is too small.

---

## Transport Layer

### `void create_packet(const char *data, size_t size, char *packet)`
- **Description**: Creates a packet by appending data to the packet header.
- **Parameters**:
  - `data`: The data to be transmitted.
  - `size`: The size of the data.
  - `packet`: The packet to store the created data.
