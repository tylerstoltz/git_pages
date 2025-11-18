# CAN Signal Decoder

A specialized tool for decoding CAN bus message payloads into individual signal values with support for various data formats, endianness, and scaling.

## Features

### CAN Message Parsing
- **Flexible Input Formats**: Supports multiple CAN message formats including:
  - Standard Candump format: `vcan0  345   [8]  FF 00 00 00 00 00 00 00`
  - Raw hex payload: `FF 00 00 00 00 00 00 00`
  - Auto-extraction of CAN ID and DLC when present
- **Message Information Display**: Shows CAN ID, DLC, and payload in both hex and decimal formats

### Signal Definition Modes

#### Byte-Based Addressing
- Specify start byte (0-7) and number of bytes (1-8)
- Ideal for byte-aligned signals
- Simple and intuitive for most use cases

#### Bit-Based Addressing
- Specify start bit (0-63) and number of bits (1-64)
- Precise control for bit-level signal extraction
- Supports signals that span byte boundaries

### Signal Processing

#### Endianness Support
- **Big Endian (Motorola)**: MSB first, common in automotive applications
- **Little Endian (Intel)**: LSB first, common in embedded systems

#### Data Types
- **Unsigned**: Standard unsigned integer values (0 to 2^n - 1)
- **Signed**: Two's complement signed integers (-2^(n-1) to 2^(n-1) - 1)

#### Value Transformation
- **Scale Factor**: Multiply raw value by a factor (e.g., 0.1 for tenth precision)
- **Offset**: Add a constant offset to the scaled value
- **Formula**: `Final Value = (Raw Value × Scale) + Offset`

### Additional Features
- **Real-Time Decoding**: Auto-decode as you type CAN messages
- **Multiple Signals**: Define and decode multiple signals from a single message
- **Unit Support**: Specify units for each signal (RPM, km/h, °C, etc.)
- **Error Handling**: Clear error messages for invalid inputs or out-of-range values
- **Copy Results**: One-click copy of all decoded values to clipboard

## Usage Examples

### Example 1: Engine Speed (Big Endian, 2 bytes)

**CAN Message:**
```
vcan0  345   [8]  0F A0 00 00 00 00 00 00
```

**Signal Definition:**
- Name: Engine Speed
- Start Byte: 0
- Number of Bytes: 2
- Endianness: Big Endian
- Data Type: Unsigned
- Scale: 0.25
- Offset: 0
- Unit: RPM

**Result:** 1000 RPM
- Raw value: 0x0FA0 = 4000
- Scaled: 4000 × 0.25 = 1000 RPM

### Example 2: Temperature (Signed, 1 byte)

**CAN Message:**
```
vcan0  123   [8]  00 E6 00 00 00 00 00 00
```

**Signal Definition:**
- Name: Temperature
- Start Byte: 1
- Number of Bytes: 1
- Endianness: Big Endian
- Data Type: Signed
- Scale: 1
- Offset: 0
- Unit: °C

**Result:** -26 °C
- Raw value: 0xE6 = 230 unsigned, -26 signed (2's complement)

### Example 3: Vehicle Speed (Little Endian, 2 bytes)

**CAN Message:**
```
vcan0  456   [8]  00 00 64 00 00 00 00 00
```

**Signal Definition:**
- Name: Vehicle Speed
- Start Byte: 2
- Number of Bytes: 2
- Endianness: Little Endian
- Data Type: Unsigned
- Scale: 0.01
- Offset: 0
- Unit: km/h

**Result:** 1.00 km/h
- Raw value: 0x0064 = 100 (little endian: 64 00 → 0064)
- Scaled: 100 × 0.01 = 1.00 km/h

### Example 4: Bit-Level Signal Extraction

**CAN Message:**
```
vcan0  789   [8]  A5 00 00 00 00 00 00 00
```

**Signal Definition:**
- Name: Status Bits
- Start Bit: 0
- Number of Bits: 4
- Endianness: Big Endian
- Data Type: Unsigned

**Result:** 10
- Byte 0 = 0xA5 = 10100101 in binary
- First 4 bits (1010) = 10 in decimal

## Use Cases

1. **CAN Bus Development**: Decode and verify signal values during development
2. **Testing & Debugging**: Quickly test different byte arrangements and endianness
3. **Reverse Engineering**: Analyze unknown CAN messages to identify signal locations
4. **Documentation**: Verify signal definitions match specification documents
5. **Education**: Learn about endianness, bit manipulation, and CAN protocols

## Tips

- Start with byte-based addressing for simpler signals, switch to bit-based for complex DBC files
- Use the auto-decode feature to see results update in real-time
- For multi-byte signals, verify endianness carefully (Big vs. Little can drastically change values)
- Remember that signed values use two's complement representation
- Scale and offset are applied in order: (raw × scale) + offset

## Related Tools

- **CAN Analyzer**: Full CAN bus message analysis with DBC file support
- **Hex Converter**: General purpose hex/decimal/binary conversion
- **Base64 Tool**: Encode/decode base64 data
