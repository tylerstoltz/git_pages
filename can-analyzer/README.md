# CAN Bus Analyzer with Message Mapping

A web-based tool for decoding and analyzing CAN bus messages with optional message ID and signal mapping functionality.

## Features

### Basic CAN Message Parsing
- Decode CAN message IDs (11-bit standard and 29-bit extended)
- Parse data payloads up to 8 bytes
- Display data in HEX, DEC, and ASCII formats
- Support multiple input formats:
  - Standard: `123#0102030405060708`
  - With 0x prefix: `0x123#0x11 0x22 0x33`
  - candump format: `(1234.567) can0 123#1122334455`

### Message Mapping (NEW)

Map CAN message IDs to human-readable names and decode payload signals with physical units.

#### Supported Mapping Features:
- **Message ID to Name Mapping**: Assign descriptive names to message IDs
- **Signal Definitions**: Define individual signals within message payloads
- **Byte-level Extraction**: Specify start byte and length for each signal
- **Endianness Support**: Handle both big-endian and little-endian byte ordering
- **Scaling and Offsets**: Apply linear transformations (value = raw × scale + offset)
- **Physical Units**: Display values with engineering units (°C, rpm, km/h, etc.)
- **Bit-level Precision**: Support bit-level signal definitions from DBC files

## Usage

### Method 1: JSON Configuration

Define mappings in JSON format for precise control:

```json
{
  "0x123": {
    "name": "EngineData",
    "signals": [
      {
        "name": "Temperature",
        "startByte": 1,
        "length": 1,
        "offset": 30,
        "scale": 1,
        "endianness": "big",
        "unit": "°C"
      },
      {
        "name": "RPM",
        "startByte": 2,
        "length": 1,
        "offset": 0,
        "scale": 1,
        "endianness": "big",
        "unit": "rpm"
      }
    ]
  }
}
```

**JSON Mapping Parameters:**
- `name` (string): Human-readable message name
- `signals` (array): List of signal definitions
  - `name` (string): Signal name
  - `startByte` (number): Starting byte position (0-indexed)
  - `length` (number): Number of bytes to read
  - `offset` (number): Offset to add after scaling
  - `scale` (number): Scaling factor to multiply raw value
  - `endianness` (string): "big" or "little" (default: "big")
  - `unit` (string, optional): Physical unit for display

### Method 2: DBC File Format

Import standard DBC (CAN Database) files for automatic signal mapping:

```
BO_ 291 EngineData: 8 ECU
 SG_ Temperature : 8|8@1+ (1,30) [0|0] "C"  Receiver
 SG_ RPM : 16|8@1+ (1,0) [0|0] "rpm"  Receiver

BO_ 1122 SpeedData: 8 ECU
 SG_ VehicleSpeed : 0|16@1+ (0.01,0) [0|300] "km/h"  Receiver
```

**DBC Format Support:**
- Message definitions (`BO_`)
- Signal definitions (`SG_`)
- Bit-level positioning
- Endianness (0=big, 1=little)
- Signed/unsigned values
- Scale and offset factors
- Min/max ranges
- Physical units

**To use DBC files:**
1. Paste DBC content into the "DBC File" tab, or
2. Click "Upload DBC File" to load from your computer
3. Click "Parse DBC" to apply the mapping

## Examples

### Example 1: Basic Temperature Mapping

**Input Message:**
```
0x123#0x11 0xF2 0x33
```

**Mapping (JSON):**
```json
{
  "0x123": {
    "name": "EngineData",
    "signals": [
      {
        "name": "Temperature",
        "startByte": 1,
        "length": 1,
        "offset": 0,
        "scale": 1,
        "endianness": "big"
      }
    ]
  }
}
```

**Output:**
```
EngineData
  Temperature: 242
```

### Example 2: Multi-byte Little-Endian Value

**Input Message:**
```
0x456#0x01 0x02 0x03 0x04
```

**Mapping (JSON):**
```json
{
  "0x456": {
    "name": "SpeedData",
    "signals": [
      {
        "name": "VehicleSpeed",
        "startByte": 0,
        "length": 2,
        "offset": 0,
        "scale": 0.01,
        "endianness": "little",
        "unit": "km/h"
      }
    ]
  }
}
```

**Output:**
```
SpeedData
  VehicleSpeed: 5.13 km/h
```
(Bytes [0x01, 0x02] in little-endian = 0x0201 = 513, × 0.01 = 5.13)

### Example 3: Using DBC File

**DBC Content:**
```
BO_ 291 EngineData: 8 ECU
 SG_ Temperature : 8|8@1+ (1,30) [0|0] "C"  Receiver
 SG_ RPM : 16|8@1+ (1,0) [0|0] "rpm"  Receiver
```

**Input Message:**
```
123#0011F23300000000
```

**Output:**
```
EngineData (0x123)
  Temperature: 272 C    (raw 0xF2=242, scaled: 242×1+30=272)
  RPM: 51 rpm          (raw 0x33=51, scaled: 51×1+0=51)
```

## Technical Details

### Signal Decoding Algorithm

1. **Extract bytes**: Read bytes from `startByte` to `startByte + length`
2. **Apply endianness**:
   - Big-endian: MSB first (e.g., [0x12, 0x34] → 0x1234)
   - Little-endian: LSB first (e.g., [0x12, 0x34] → 0x3412)
3. **Calculate physical value**: `physical_value = raw_value × scale + offset`
4. **Format output**: Round and append unit if specified

### DBC Bit-Level Extraction

For DBC signals with bit-level precision:
- Convert byte array to bit array
- Extract bits from `startBit` to `startBit + bitLength`
- Apply endianness at bit level
- Handle signed values using two's complement

## Keyboard Shortcuts

- `Ctrl + Enter`: Parse messages

## Browser Compatibility

Works in all modern browsers:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

## Use Cases

- Automotive ECU development
- CAN bus debugging and analysis
- Embedded systems testing
- Vehicle diagnostics
- Industrial automation
- Robotics communication analysis

## Tips

1. **Flexible Mapping**: The same message can be interpreted differently by changing the mapping configuration
2. **Offset Usage**: Use offsets to handle sensor calibrations (e.g., temperature offset)
3. **Scale Factors**: Convert raw ADC values to engineering units
4. **DBC Files**: Industry-standard format - many automotive tools export DBC files
5. **Validation**: The tool validates message format and data length automatically
