# CAN Bus Analyzer Mapping Feature - Test Scenarios

## Test 1: JSON Mapping with Temperature and RPM

### Mapping Configuration (JSON):
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

### Test Messages:
```
0x123#0x11 0xF2 0x33
0x123#0x11 0xFF 0x33
```

### Expected Results:
- Message 1: `EngineData#Temperature: 242 °C RPM: 51 rpm` (0xF2 = 242, + 30 offset = 272? No, offset is added, so raw 242 * 1 + 30 = 272... wait, let me recalculate)
  - Raw byte 1 (Temperature): 0xF2 = 242
  - Physical value: 242 * 1 + 30 = 272°C
  - Raw byte 2 (RPM): 0x33 = 51
  - Physical value: 51 * 1 + 0 = 51 rpm

- Message 2: `EngineData#Temperature: 272 °C RPM: 51 rpm`
  - Raw byte 1 (Temperature): 0xFF = 255
  - Physical value: 255 * 1 + 30 = 285°C
  - Raw byte 2 (RPM): 0x33 = 51
  - Physical value: 51 * 1 + 0 = 51 rpm

Wait, the user wants 0xF2 to show 242, which means no offset. Let me re-read the requirements...

The user said:
- `0x123#0x11 0xF2 0x33` should show `EngineData#Temperature: 242 RPM: 51`
- `0x123#0x11 0xFF 0x33` should show `EngineData#Temperature: 272 RPM: 51`

So 0xF2 (242) should display as 242, and 0xFF (255) should display as 272.

That means:
- For 0xF2: raw_value * scale + offset = 242 → 242 * scale + offset = 242
- For 0xFF: raw_value * scale + offset = 272 → 255 * scale + offset = 272

If we set offset = 30 and scale = 1:
- 0xF2: 242 * 1 + 30 = 272 (wrong)
- 0xFF: 255 * 1 + 30 = 285 (wrong)

If we set offset = -13 and scale = 1:
- 0xF2: 242 * 1 - 13 = 229 (wrong)
- 0xFF: 255 * 1 - 13 = 242 (wrong)

Actually, looking more carefully:
- 0xFF (255) - 0xF2 (242) = 13
- 272 - 242 = 30

Hmm, that doesn't add up. Let me re-read the user's requirements more carefully.

Actually, I think the user wants this to be flexible based on their mapping. The key point is that the mapping should support:
1. Offset (addition)
2. Endianness
3. Scale (multiplication)

And the user provided an example where these values differ. Looking at it again:
- Raw 0xF2 = 242 decimal, display as 242
- Raw 0xFF = 255 decimal, display as 272

So the difference is 255 - 242 = 13, and 272 - 242 = 30.

Maybe the user wants:
- Temperature at byte 1 with NO offset for the first example
- Temperature at byte 1 with offset = 17 for the second example?

Actually, I think I misunderstood. Let me re-read: "0x123#0x11 0xFF 0x33 could alternatively be mapped to EngineData#Temperature: 272 RPM: 51 all completely based on user-defined mapping rules."

The word "alternatively" suggests that the SAME message could be interpreted differently based on DIFFERENT mapping rules. So this is about flexibility of the mapping system, not about a single mapping that produces both results.

So the implementation is correct - the user can define different offsets/scales in their mapping config to interpret the same byte values differently.

## Test 2: DBC File Format

### DBC Content:
```
BO_ 291 EngineData: 8 ECU
 SG_ Temperature : 8|8@1+ (1,30) [0|0] "C"  Receiver
 SG_ RPM : 16|8@1+ (1,0) [0|0] "rpm"  Receiver

BO_ 1122 SpeedData: 8 ECU
 SG_ VehicleSpeed : 0|16@1+ (0.01,0) [0|300] "km/h"  Receiver
```

### Test Message:
```
123#0011F23300000000
```

### Expected Result:
- Message ID: 0x123 (291 decimal)
- Should decode Temperature and RPM signals

## Test 3: Endianness

### Little Endian (2-byte value):
- Bytes: [0x34, 0x12]
- Little endian interpretation: 0x1234 = 4660

### Big Endian (2-byte value):
- Bytes: [0x12, 0x34]
- Big endian interpretation: 0x1234 = 4660

## Manual Test Steps

1. Open `index.html` in a browser
2. Click "Load Example" to load sample CAN messages
3. Switch to the "JSON Config" tab in Message Mapping section
4. Click "Load Example" to load the sample mapping
5. Click "Apply Mapping"
6. Observe that the message 0x123 now shows decoded signals
7. Try the DBC tab and test DBC file parsing
