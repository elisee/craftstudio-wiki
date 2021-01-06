# Script file format

**File extension:** .csscript

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt8            |                   1 | Asset type (always 7 for Scripts)        |
| 1                  | UInt16           |                   2 | Format version (currently 11)            |
| 3                  | UInt8            |                   1 | Non-zero if visual script                |
| 4                  | Script data      |          (variable) | Visual or text script data (see below)   |
| 4 + ?              | UInt16           |                   2 | Script property count                    |
| 4 + ? + 2          | UInt16           |                   2 | Next unused property ID                  |
| 4 + ? + 4          | ScriptProperty[] |                   2 | Array of script properties (see below)   |

### Visual script data

(Not yet documented)

### Text script data

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | Int32            |                   4 | Last state index (ignore, internal stuff)|
| 4                  | C# String        |          (variable) | Actual script text                       |

## Script properties

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt16           |                   2 | ID                                       |
| 2                  | C# String        |          (variable) | Property variable name                   |
| 2 + ?              | UInt8            |                   1 | Property type (see below)                |
| 2 + ? + 1          | (variable)       |          (variable) | Property default value (see below)        |

### Property types & default values

| Label            | Value  | Default value type |
| ---------------- | ------:| ------------------ |
| Boolean          | 0      | UInt8 (non-zero means true) |
| Number           | 1      | Float64 |
| String           | 2      | C# String |
