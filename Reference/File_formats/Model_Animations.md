# Model animation file format

**File extension**: .csmodelanim

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt8            |                   1 | Asset type (always 6 for Model Animations)|
| 1                  | UInt16           |                   2 | Format version (currently 3)             |
| 3                  | UInt16           |                   2 | Animation duration (in frames)           |
| 5                  | Boolean          |                   1 | Hold last key frame                      |
| 6                  | UInt16           |                   2 | Animated node count                      |
| 8                  | ModelNodeAnimation[]|       (variable) | Array of model node animations (see below)|

### Model node animation

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | C# String        |          (variable) | Model node name                          |
| ?                  | UInt16           |                   2 | Position keyframe count                  |
| ? + 2              | ModelNodeKeyFrame[]|        (variable) | Array of position keyframes              |
| ? + 2 + ?          | UInt16           |                   2 | Orientation keyframe count               |
| ? + 2 + ? + 2      | ModelNodeKeyFrame[]|        (variable) | Array of orientation keyframes           |
| ? + 2 + ? + 2 + ?  | UInt16           |                   2 | Block size keyframe count                |
| ? + 2 + ? + 2 + ? + 2| ModelNodeKeyFrame[]|        (variable) | Array of block size keyframes            |
| ? + 2 + ? + 2 + ? + 2 + ?| UInt16           |                   2 | Pivot offset keyframe count              |
| ? + 2 + ? + 2 + ? + 2 + ? + 2| ModelNodeKeyFrame[]|        (variable) | Array of pivot offset keyframes          |
| ? + 2 + ? + 2 + ? + 2 + ? + 2 + ?| UInt16           |                   2 | Scale keyframe count                     |
| ? + 2 + ? + 2 + ? + 2 + ? + 2 + ? + 2| ModelNodeKeyFrame[]|        (variable) | Array of scale keyframes                 |

### Model node key frame

| Offset             | Type             | Size (octets)       | Description                              |
| ------------------ | ---------------- | -------------------:| ---------------------------------------- |
| 0                  | UInt16           |                   2 | Key time index                           |
| 2                  | UInt8            |                   1 | Interpolation mode (currently ignored)   |
| 3                  | (variable)       |          (variable) | Key frame value                          |

The key frame value type depends on the type of key frame:

| Key frame type   | Value type      |
| ---------------- | --------------- |
| Position         | Float32[3] (vector XYZ) |
| Orientation      | Float32[4] (quaternion WXYZ) |
| Block size       | Int32[3] (vector XYZ) |
| Pivot offset     | Float32[3] (vector XYZ) |
| Scale            | Float32[3] (vector XYZ) |
