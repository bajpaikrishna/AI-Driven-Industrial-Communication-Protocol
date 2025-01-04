# AICP API Reference

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
