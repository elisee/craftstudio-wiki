# Map file formats

Maps are split in two files: the .csmap file, which contains general info about the map asset, and the .csmapchunks file, which contains the actual map chunks.

## Map description file

**File extension**: .csmap

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt8            |                   1 | Asset type (always 1 for Maps)           |
| 1                  | UInt16           |                   2 | Format version (currently 4)             |
| 3                  | UInt16           |                   2 | Associated Tile Set ID                   |

## Map chunks file

**File extension**: .csmapchunks

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt16           |                   2 | Format version (currently 2)             |
| 2                  | UInt32           |                   4 | Number of chunks defined                 |
| 6                  | MapChunk[]       |          (variable) | The chunk data themselves (see below)    |

Each chunk is 32x32x32 in size. The position of each chunk is stored in terms of chunk offsets relative to the map origin, so you'll want to multiply it by 32 to get the position in world units.

A map chunk is composed of the following:

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt32           |                   4 | X coordinate of the chunk's position     |
| 4                  | UInt32           |                   4 | Y coordinate of the chunk's position     |
| 8                  | UInt32           |                   4 | Z coordinate of the chunk's position     |
| 12                 | UInt32           |                   4 | Compressed chunk data length             |
| 16                 | Byte[]           |          (variable) | Compressed chunk data                    |

The chunk data is compressed using the [DEFLATE algorithm](http://en.wikipedia.org/wiki/DEFLATE). Once uncompressed, it contains 32x32x32 block IDs (each one as a single byte) followed by 32x32x32 block orientations (each one as a single byte).

A block ID of 255 means no block.

Block orientations should be interpreted as such:

| Label            | Value  |
| ---------------- | ------:|
| North            | 0      |
| East             | 1      |
| South            | 2      |
| West             | 3      |