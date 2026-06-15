# TimeStampTool Plugin Documentation

## Overview

TimeStampTool is a lightweight Unreal Engine plugin that provides time-related utility functions for blueprint and C++ developers. It offers easy-to-use timestamp conversion and formatting capabilities.

---

## Installation

### Method 1: Manual Installation

1. **Download or clone** the TimeStampTool plugin folder.
2. **Copy** the entire `TimeStampTool` folder to your Unreal Engine project's `Plugins` directory:
   ```
   YourProject/
   └── Plugins/
       └── TimeStampTool/
           ├── TimeStampTool.uplugin
           ├── Source/
           ├── Binaries/
           └── ...
   ```

### Method 2: Enable in Engine

1. Open your Unreal Engine project.
2. Go to **Edit > Plugins** from the main menu.
3. In the Plugins window, navigate to the **Other** category.
4. Locate **TimeStampTool** in the list.
5. Check the **Enabled** checkbox.
6. Click **Apply** and restart the editor when prompted.

---

## Dependencies & Prerequisites

### Engine Version
- Unreal Engine 5.x (Tested with UE5.7)
- Compatible with both Blueprint and C++ projects

### Required Dependencies
- No external plugins required
- Uses only Unreal Engine's core modules:
  - Core
  - CoreUObject
  - Engine
  - Kismet

### Project Settings
- No additional project settings required
- Works with both Development and Shipping builds

---

## Features & Usage

The TimeStampTool plugin provides the following blueprint-callable functions:

### 1. Get UTC Timestamp (Milliseconds)

**Description:** Returns the current UTC time as a 13-digit Unix millisecond timestamp.

**Blueprint Node:** `GetUTCTimestampMs`

**Return Type:** `int64` (int64)

**Usage Example:**
```blueprint
// Get current timestamp
int64 CurrentTime = GetUTCTimestampMs();

// Example output: 1718102400000
```

**C++ Equivalent:**
```cpp
#include "TimeStampToolBPLibrary.h"

int64 Timestamp = UTimeStampToolBPLibrary::GetUTCTimestampMs();
```

### 2. Convert Timestamp to UTC DateTime

**Description:** Converts a millisecond timestamp to a UTC FDateTime object.

**Blueprint Node:** `TimestampMsToDateTime`

**Parameters:**
- `TimestampMs` (int64): Input timestamp in milliseconds

**Return Type:** `DateTime` (FDateTime)

**Usage Example:**
```blueprint
// Convert timestamp to UTC DateTime
DateTime UTC = TimestampMsToDateTime(1718102400000);

// Access date components
int32 Year = UTC.Year;
int32 Month = UTC.Month;
int32 Day = UTC.Day;
int32 Hour = UTC.Hour;
int32 Minute = UTC.Minute;
int32 Second = UTC.Second;
```

**C++ Equivalent:**
```cpp
#include "TimeStampToolBPLibrary.h"

int64 TimestampMs = 1718102400000;
FDateTime UTCDateTime = UTimeStampToolBPLibrary::TimestampMsToDateTime(TimestampMs);
```

### 3. Convert Timestamp to Local DateTime

**Description:** Converts a millisecond timestamp to a local timezone FDateTime object.

**Blueprint Node:** `TimestampMsToLocalDateTime`

**Parameters:**
- `TimestampMs` (int64): Input timestamp in milliseconds

**Return Type:** `DateTime` (FDateTime)

**Usage Example:**
```blueprint
// Convert timestamp to local DateTime
DateTime LocalTime = TimestampMsToLocalDateTime(1718102400000);

// Use in UI or logging
PrintString(LocalTime.ToString());
```

**C++ Equivalent:**
```cpp
#include "TimeStampToolBPLibrary.h"

int64 TimestampMs = 1718102400000;
FDateTime LocalDateTime = UTimeStampToolBPLibrary::TimestampMsToLocalDateTime(TimestampMs);
```

### 4. Convert Timestamp to UTC Formatted String

**Description:** Converts a millisecond timestamp to a human-readable UTC string in "YYYY-MM-DD HH:MM:SS" format.

**Blueprint Node:** `TimestampMsToUTCFormatString`

**Parameters:**
- `TimestampMs` (int64): Input timestamp in milliseconds

**Return Type:** `String` (FString)

**Usage Example:**
```blueprint
// Convert timestamp to formatted string
String FormattedTime = TimestampMsToUTCFormatString(1718102400000);

// Example output: "2024-06-11 12:00:00"
```

**C++ Equivalent:**
```cpp
#include "TimeStampToolBPLibrary.h"

int64 TimestampMs = 1718102400000;
FString FormattedTime = UTimeStampToolBPLibrary::TimestampMsToUTCFormatString(TimestampMs);
```

---

## Blueprint Usage Example

Here's a complete example demonstrating how to use TimeStampTool in Blueprints:

```
Event BeginPlay
    └── GetUTCTimestampMs
            └── TimestampMsToUTCFormatString
                    └── Print String (to screen)
```

This will print the current UTC time to the screen when the game starts.

---

## Common Errors & Troubleshooting

### Error: Plugin Not Found

**Symptom:** Engine fails to load the plugin, or functions are not available in Blueprints.

**Possible Causes:**
1. Plugin folder is not in the correct location
2. Plugin folder name is incorrect
3. Plugin files are corrupted

**Solutions:**
1. Verify the plugin folder is located at `YourProject/Plugins/TimeStampTool/`
2. Ensure the folder name matches exactly: `TimeStampTool`
3. Re-download or re-copy the plugin files

---

### Error: Missing Binary Files

**Symptom:** "Missing module TimeStampTool" error when starting the editor.

**Possible Causes:**
1. Binary files are missing or incompatible
2. Build configuration mismatch
3. Plugin was not compiled for your platform

**Solutions:**
1. Ensure `Binaries/Win64/` contains the compiled DLL files
2. Rebuild the plugin using the Unreal Engine build system:
   - Right-click `.uproject` file > **Generate Visual Studio Project Files**
   - Open the solution and build the `TimeStampTool` module
   - Or use the Epic Games Launcher to build the project

---

### Error: Function Not Visible in Blueprints

**Symptom:** TimeStampTool functions don't appear in the Blueprint context menu.

**Possible Causes:**
1. Plugin is not enabled
2. Blueprint cache needs to be refreshed
3. Header file has compilation errors

**Solutions:**
1. Verify the plugin is enabled in **Edit > Plugins**
2. Restart the Unreal Editor
3. Check the Output Log for compilation errors

---

### Error: Invalid Timestamp Value

**Symptom:** Functions return incorrect or unexpected dates.

**Possible Causes:**
1. Input timestamp is not in milliseconds
2. Timestamp value is out of valid range

**Solutions:**
1. Ensure the input timestamp is in **milliseconds** (13-digit number), not seconds
2. Validate timestamp ranges:
   - Minimum valid: 0 (January 1, 1970 00:00:00 UTC)
   - Maximum valid: ~3.2e14 (Approximately year 3000)

---

## API Reference

### Blueprint Function Library

| Function Name | Category | Description |
|--------------|----------|-------------|
| `GetUTCTimestampMs` | Time Tools | Returns current UTC time as millisecond timestamp |
| `TimestampMsToDateTime` | Time Tools | Converts ms timestamp to UTC FDateTime |
| `TimestampMsToLocalDateTime` | Time Tools | Converts ms timestamp to local FDateTime |
| `TimestampMsToUTCFormatString` | Time Tools | Converts ms timestamp to "YYYY-MM-DD HH:MM:SS" string |

---

## Changelog

### Version 1.0
- Initial release
- Added `GetUTCTimestampMs` function
- Added `TimestampMsToDateTime` function
- Added `TimestampMsToLocalDateTime` function
- Added `TimestampMsToUTCFormatString` function

---

## License

This plugin is provided as-is. Please refer to Unreal Engine's EULA for usage terms.
