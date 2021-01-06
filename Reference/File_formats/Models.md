# Model file format

**File extension**: .csmodel

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt8            |                   1 | Asset type (always 0 for Models)         |
| 1                  | UInt16           |                   2 | Format version (currently 5)             |
| 3                  | UInt16           |                   2 | Next unused node ID                      |
| 5                  | UInt16           |                   2 | Node count                               |
| 7                  | ModelNode[]      |          (variable) | Array of nodes (see below)               |
| 7 + ? + 0          | UInt32           |                   4 | Texture data size                        |
| 7 + ? + 4          | UInt8[]          |   Texture data size | Texture data in PNG format               |
| 7 + ? + 4 + ? + 0  | UInt16           |                   2 | Animation count                          |
| 7 + ? + 4 + ? + 2  | UInt16[]         | Animation count × 2 | Asset IDs of associated model animations |


### Model node

Each model node has the following structure:

| Offset        | Type        | Size (octets) | Description                                       |
| ------------- | ----------- | -------------:| ------------------------------------------------- |
| 0             | UInt16      |             2 | ID                                                |
| 2             | UInt16      |             2 | Parent node ID                                    |
| 4             | C# String   |    (variable) | Name                                              |
| 4 + ? + 0     | Vector3     |    12 (3 × 4) | Position                                          |
| 4 + ? + 12    | Vector3     |    12 (3 × 4) | Offset from pivot                                 |
| 4 + ? + 24    | Vector3     |    12 (3 × 4) | Scale                                             |
| 4 + ? + 36    | Quaternion  |    16 (4 × 4) | Orientation                                       |
| 4 + ? + 52    | UInt16      |             2 | Block size X                                      |
| 4 + ? + 54    | UInt16      |             2 | Block size Y                                      |
| 4 + ? + 56    | UInt16      |             2 | Block size Z                                      |
| 4 + ? + 58    | UInt8       |             1 | Unwrap mode (collapsed 0, full 1 or custom 2)     |
| 4 + ? + 59    | Point       |     8 (2 × 4) | Unwrap offset for quad 0                          |
| 4 + ? + 67    | Point       |     8 (2 × 4) | Unwrap offset for quad 1                          |
| 4 + ? + 75    | Point       |     8 (2 × 4) | Unwrap offset for quad 2                          |
| 4 + ? + 83    | Point       |     8 (2 × 4) | Unwrap offset for quad 3                          |
| 4 + ? + 91    | Point       |     8 (2 × 4) | Unwrap offset for quad 4                          |
| 4 + ? + 99    | Point       |     8 (2 × 4) | Unwrap offset for quad 5                          |
| 4 + ? + 107   | UVTransform |             1 | Unwrap transform flags for quad 0                 |
| 4 + ? + 108   | UVTransform |             1 | Unwrap transform flags for quad 1                 |
| 4 + ? + 109   | UVTransform |             1 | Unwrap transform flags for quad 2                 |
| 4 + ? + 110   | UVTransform |             1 | Unwrap transform flags for quad 3                 |
| 4 + ? + 111   | UVTransform |             1 | Unwrap transform flags for quad 4                 |
| 4 + ? + 112   | UVTransform |             1 | Unwrap transform flags for quad 5                 |

### Model node unwrap

Model nodes are rendered textured blocks.

(TODO: Document the way each unwrap mode works. In the meantime, looking at how they behave in CraftStudio should be enough)

The unwrap transform flags have the following values:

| Label            | Value  |
| ---------------- | ------:|
| None             | 0      |
| Rotate90         | 1 << 0 |
| Rotate180        | 1 << 1 |
| Rotate270        | 1 << 2 |
| MirrorHorizontal | 1 << 3 |
| MirrorVertical   | 1 << 4 |

One rotation and both mirroring options can be combined.