# Variable Keys to JSON

A Figma plugin that exports variable data from local collections as downloadable JSON files, providing variable names, keys, IDs, and types in a structured format for use in external tools or documentation workflows.

## Features

- 📁 **Collection Selection**: Browse and select from available local variable collections
- 📊 **Complete Variable Export**: Exports name, key, ID, and resolved type for each variable
- 📋 **Copy to Clipboard**: Instantly copy JSON data for quick use
- 💾 **Download JSON Files**: Save structured data as timestamped JSON files
- 🎯 **Clean Data Structure**: Uses variable names as keys with organized metadata

## How It Works

1. **Select Collection**: Choose a local variable collection from the dropdown
2. **Generate JSON**: Click to process all variables in the selected collection
3. **Export Data**: Copy to clipboard or download as a JSON file

## JSON Output Format

The plugin generates clean, structured JSON with variable names as keys:

```json
{
  "color/primary/500": {
    "name": "color/primary/500",
    "key": "abc123def456...",
    "id": "VariableID:123:456",
    "resolvedType": "COLOR"
  },
  "spacing/lg": {
    "name": "spacing/lg",
    "key": "def456ghi789...",
    "id": "VariableID:789:012",
    "resolvedType": "FLOAT"
  }
}
```

## Use Cases

- **Documentation**: Generate variable inventories for design system documentation
- **Plugin Development**: Prepare variable data for other Figma plugins
- **External Tools**: Export design tokens for use in development workflows
- **Auditing**: Review and analyze variable structures across collections

## Installation

1. Download the plugin files from this repository
2. In Figma, go to **Plugins** → **Development** → **Import plugin from manifest**
3. Select the `manifest.json` file from the downloaded folder

## Technical Details

- **ES5 Compatible**: Written for Figma's plugin environment
- **Local Collections Only**: Works exclusively with local variable collections
- **All Variable Types**: Supports COLOR, FLOAT, STRING, BOOLEAN variables
- **Lightweight**: Fast processing with clean console logging

## File Structure

```
├── manifest.json     # Plugin configuration
├── code.js          # Main plugin logic (ES5 compatible)
├── ui.html          # Plugin interface with inline styles
└── README.md        # Documentation
```

## Development

The plugin is built with ES5 JavaScript for maximum compatibility with Figma's plugin environment. All functionality is contained within the three core files with no external dependencies.

## License

MIT License - feel free to modify and distribute as needed.
