# Project file format

**File name**: Project.dat

| Offset                    | Type             | Size (octets)       | Description                              |
| ------------------------- | ---------------- | -------------------:| ---------------------------------------- |
| 0                         | UInt8            |                   1 | Format version (currently 9)             |
| 1                         | UInt8            |                   1 | Project type (0 is game, 1 is movie)     |
| 2                         | C# String        |          (variable) | Project name                             |
| 2 + ?                     | UInt16           |                   2 | Startup scene ID                         |
| 2 + ? + 2                 | UInt16           |                   2 | Script API Version                       |
| 2 + ? + 4                 | UInt8            |                   1 | Membership policy (see below)            |
| 2 + ? + 5                 | UInt8            |                   1 | Default member role (see below)          |
| 2 + ? + 6                 | C# String        |          (variable) | Project description                      |
| 2 + ? + 6 + ?             | UInt16           |                   2 | Next unused game control ID              |
| 2 + ? + 6 + ? + 2         | UInt16           |                   2 | Game control count                       |
| 2 + ? + 6 + ? + 4         | GameControl[]    |          (variable) | Array of game controls (see below)       |
| 2 + ? + 6 + ? + 4 + ?     | UInt16           |                   2 | Next project entry ID                    |
| 2 + ? + 6 + ? + 4 + ? + 2 | UInt16           |                   2 | Project entries count                    |
| 2 + ? + 6 + ? + 4 + ? + 4 | ProjectEntry[]   |          (variable) | Array of project entries (see below)     |

### Project metadata

The project's membership policy can take one of the following values:

| Label            | Value  |
| ---------------- | ------:|
| MembershipRequest| 0      |
| InviteOnly       | 1      |
| Open             | 2      |

The project's default member role can be one of:

| Label            | Value  |
| ---------------- | ------:|
| Spectator        | 1      |
| Member           | 2      |
| Moderator        | 3      |
| Administrator    | 4      |

Note that there is no value of 0 (it's used for membership requests)

### Game control

Each game control has the following structure:

| Offset                 | Type             | Size (octets)       | Description                              |
| ---------------------- | ---------------- | -------------------:| ---------------------------------------- |
| 0                      | UInt16           |                   2 | Game control ID                          |
| 2                      | C# String        |          (variable) | Game control name                        |
| 3                      | ControlType      |                   1 | Game control type (see below)            |
| 4                      | ControlSource    |                   1 | Game control source (see below)          |
| 5                      | Key              |                   1 | Positive key                             |
| 6                      | Key              |                   1 | Negative key                             |
| 7                      | UInt8            |                   1 | Positive button index                    |
| 8                      | UInt8            |                   1 | Negative button index                    |
| 9                      | UInt8            |                   1 | Joystick index                           |
| 10                     | UInt8            |                   1 | Joystick axis index                      |
| 11                     | Float32          |                   4 | Joystick axis dead zone                  |
| 15                     | Float32          |                   4 | Axis sensivity (towards one, per second) |
| 19                     | Float32          |                   4 | Axis gravity (towards zero, per second)  |
| 24                     | Boolean          |                   1 | Snap to zero when changing direction     |

(TODO: Document ControlType, ControlSource and Key)

### Project entry

Each project entry has the following structure:

| Offset                 | Type             | Size (octets)       | Description                              |
| ---------------------- | ---------------- | -------------------:| ---------------------------------------- |
| 0                      | Boolean          |                   1 | True if folder, false if asset           |
| 1                      | UInt16           |                   2 | Project entry ID                         |
| 3                      | UInt16           |                   2 | Parent ID (or 65536 if root entry)       |
| 5                      | C# String        |          (variable) | Name                                     |
| 5 + ?                  | ProjectEntryType |                   1 | Entry type (see below)                   |
| 5 + ? + 1              | Boolean          |                   1 | True if locked, false otherwise          |

Then, for assets only:

| Offset                 | Type             | Size (octets)       | Description                              |
| ---------------------- | ---------------- | -------------------:| ---------------------------------------- |
| 5 + ? + 2              | Boolean          |                   1 | True if trashed, false otherwise         |
| 5 + ? + 3              | UInt16           |                   2 | Next revision ID                         |
| 2 + ? + 5              | UInt16           |                   2 | Asset revisions count                    |
| 2 + ? + 7              | AssetRevision[]  |          (variable) | Array of asset revisions (see below)     |


### Asset Revision

Each asset entry has a list of revisions with following structure:

| Offset                 | Type             | Size (octets)       | Description                              |
| ---------------------- | ---------------- | -------------------:| ---------------------------------------- |
| 0                      | UInt16           |                   2 | Entry Revision ID                        |
| 2                      | C# String        |          (variable) | Name                                     | 

### Project entry type

| Label            | Value  |
| ---------------- | ------:|
| Model            | 0      |
| ModelAnimation   | 6      |
| Map              | 1      |
| TileSet          | 3      |
| Scene            | 2      |
| Script           | 7      |
| Document         | 4      |
| Sound            | 8      |
| Font             | 9      |