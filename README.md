# Variable Opacity Usage Auditor

## Overview

The Variable Opacity Usage Auditor is a Figma plugin that helps identify and manage opacity variables across collections. It specifically focuses on auditing underscore syntax variables (e.g., `red/25_90`) by comparing a source collection against a target collection to identify which opacity variables should be removed.

## Features

- **Collection Comparison**: Compare variables between source and target collections
- **Smart Variable Detection**: Specifically focuses on underscore syntax opacity variables
- **Large Collection Support**:
  - Automatic handling for collections with <500 variables via Figma API
  - JSON upload support for collections with >500 variables
- **Audit Report Generation**: Generates a JSON file of variables that should be removed
- **Flexible Source Input**: Works with both API-retrieved and JSON-uploaded variable lists

## Technical Architecture

### Plugin Structure

```
variable-opacity-usage-to-json/
├── manifest.json     # Plugin configuration
├── code.js          # Main plugin logic (ES5 compatible)
├── ui.html          # Plugin interface with inline CSS/JS
└── README.md        # Documentation
```

### Technology Stack

- **JavaScript**: ES5-compatible for Figma plugin environment
- **Figma Plugin API**: For variable and collection management
- **Promise-based**: Async handling for collection processing

## How It Works

### 1. Variable Format

The plugin specifically looks for opacity variables with underscore syntax:

| Variable Type    | Format Example | Description                       |
| ---------------- | -------------- | --------------------------------- |
| Opacity Variable | `red/25_90`    | Color variable with opacity value |

### 2. Processing Flow

1. **Collection Selection**

   - User selects source collection (where variables might be removed from)
   - User selects target collection (to check variable usage against)

2. **Variable Loading**

   - For collections with <500 variables:
     - Automatically loads variables using Figma API
   - For collections with >500 variables:
     - Prompts for JSON upload of complete variable list

3. **Audit Process**

   - Identifies all underscore syntax variables from source
   - Cross-references against target collection
   - Identifies variables not used in target collection

4. **Output Generation**
   - Generates JSON file containing variables to be removed
   - Maintains same format as input JSON

## UI Components

### Collection Selection Screen

```
┌─────────────────────────────────────┐
│  📚 Collection Selection            │
│  ├─ Source Collection               │
│  │  [Select Source Collection ▼]    │
│  └─ Target Collection               │
│     [Select Target Collection ▼]    │
├─────────────────────────────────────┤
│  [Next]                             │
└─────────────────────────────────────┘
```

### JSON Upload Screen (if needed)

```
┌─────────────────────────────────────┐
│  📋 Selected Collections            │
│  Source: [Selected Source]          │
│  Target: [Selected Target]          │
├─────────────────────────────────────┤
│     📁 Upload Variables JSON        │
│     [Choose File]                   │
└─────────────────────────────────────┘
```

### Results Screen

```
┌─────────────────────────────────────┐
│  [Start New Audit]  [Close]         │
├─────────────────────────────────────┤
│  📊 Audit Results                   │
├─────────────────────────────────────┤
│  Total Variables Checked: X         │
│  Opacity Variables Found: Y         │
│  Variables to Remove: Z             │
│                                     │
│  [Download Results JSON]            │
└─────────────────────────────────────┘
```

## Key Functions

### code.js

#### `loadCollections()`

- Loads all available collections
- Sends collection data to UI for display
- Handles collection size checking

#### `processVariables(...)`

- Main orchestrator for variable auditing
- Handles both API and JSON-based variable lists
- Identifies underscore syntax variables

#### `generateAuditReport(...)`

- Creates final JSON output
- Includes only variables to be removed
- Maintains original JSON structure

### ui.html

#### `handleCollectionSelection()`

- Manages collection selection process
- Determines if JSON upload is needed

#### `processAuditResults(results)`

- Displays audit results
- Provides download option for JSON output

## Console Logging

The plugin uses collapsible console groups for clean output:

```javascript
// Normal view
📚 Loading all collections...
✅ Found 1 local collections
✅ Successfully loaded 1 library collections
📄 Parsing CSS content...
✅ Found 75 theme variables
▼ ⚡ Processing 75 variables...    // Click to expand
✅ All library imports completed
📊 === FINAL RESULTS ===
✅ Created: 70
✏️ Updated: 5
❌ Failed: 0

// Expanded view shows all details
▼ ⚡ Processing 75 variables...
  🔄 Processing: color/fill/danger
  ✏️ Updated: color/fill/danger
  🔄 Processing: color/fill/primary
  ✨ Created: color/fill/primary
  // ... all 75 entries
```

## Error Handling

- **Collection Loading**: Falls back to local-only if libraries fail
- **CSS Parsing**: Validates content and shows clear error messages
- **Variable Creation**: Tracks and reports failed variables individually
- **Library Imports**: Handles async failures gracefully

## Best Practices

1. **CSS Organization**

   - Keep `@theme` block clean with only variable mappings
   - Ensure all referenced variables exist in light/dark blocks
   - Use consistent naming conventions

2. **Collection Management**

   - Organize source tokens in a dedicated library
   - Create a separate local collection for theme variables
   - Use descriptive collection names

3. **Large Files**
   - The plugin handles 75+ variables efficiently
   - Results start collapsed for better overview
   - Use console expansion to debug specific issues

## Limitations

- **ES5 Only**: Due to Figma plugin environment constraints
- **Color Variables Only**: Currently supports only COLOR type variables
- **Local Targets**: Can only create variables in local collections
- **Opacity Format**: Must use `--alpha(var(--color) / X%)` syntax

## Troubleshooting

### Variables Not Found

- Check exact naming in source collection
- Verify the plugin's variable name conversion logic
- Use console logs to see what names are being searched

### Import Failures

- Ensure you have access to the library
- Check library publishing status
- Verify variable keys haven't changed

### Performance Issues

- Large files are handled with async batching
- Console logs are collapsed by default
- UI uses accordions to manage long lists

## Future Enhancements

- Support for additional variable types (spacing, typography)
- Export functionality for created mappings
- Batch processing of multiple CSS files
- Variable validation and preview
- Undo/redo functionality

## Version History

- **1.0.0**: Initial release with core functionality
- **1.1.0**: Added console grouping and UI improvements
- **1.2.0**: Fixed async handling and button positioning
