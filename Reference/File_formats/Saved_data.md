# Saved data file format

**File extension:** .cssave

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt16           |                   2 | Format version (currently 2)             |
| 1                  | Lua table        |          (variable) | The saved Lua table                      |

## Lua table layout

A Lua table contains zero or more key-value pairs. Each key can either be a number or a string. Each value can be one of: string, number, boolean or table.

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt32           |                   4 | Number of entries in the table           |
| 4                  | TableEntry[]     |          (variable) | Key and value pairs                      |

## Table entry layout

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt8            |                   1 | Non-zero if key is numeric |
| 1                  | (variable)       |          (variable) | Key (Float64 or C# string) |
| 1 + ?              | UInt8            |                   1 | Value type (see below) |
| 1 + ? + 1          | (variable)       |          (variable) | Value of the announced type |

## Value types

| Label            | Value  | Value type |
| ---------------- | ------:| ---------- |
| String           | 0      | C# String |
| Number           | 1      | Float64 |
| Boolean          | 2      | UInt8 (non-zero means true) |
| Table            | 3      | Table (see above) |
