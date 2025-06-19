# Opacity Variables Usage Auditor

This Figma plugin audits and manages opacity variables with underscore syntax (like `red/25_90`) by comparing source and target collections to identify unused variables for removal, while also converting CSS theme variables into properly organized Figma variables with cross-collection alias support and automated light/dark mode mapping.

## Features

### 🔍 Variable Auditing

- **Smart Detection**: Automatically identifies opacity variables with underscore syntax (`red/25_90`, `color/rose/500_90`)
- **Collection Comparison**: Cross-references variables between source and target collections
- **Usage Analysis**: Identifies which opacity variables should be removed based on actual usage
- **Audit Reports**: Generates comprehensive JSON reports of variables marked for removal

### 🎨 CSS Variable Mapping

- **CSS-to-Figma Conversion**: Transforms CSS variables (`--color-red-500`) into Figma variables (`color/red/500`)
- **Theme Variable Support**: Processes CSS `@theme` declarations automatically
- **Cross-Collection Aliases**: Creates proper variable references between different collections
- **Light/Dark Mode Mapping**: Automatically handles mode-specific variable assignments

### 📊 Collection Management

- **Library & Local Support**: Works with both library and local variable collections
- **Large Collection Handling**:
  - Automatic API loading for collections <500 variables
  - JSON upload support for collections >500 variables
- **Smart Import**: Automatically imports library variables when needed
- **Progress Tracking**: Real-time feedback on creation, updates, and failures

## Technical Architecture

### Plugin Structure

```
opacity-variables-usage-to-json/
├── manifest.json              # Plugin configuration
├── code.js                   # Main plugin logic (ES5 compatible)
├── ui.html                   # Plugin interface with inline CSS/JS
├── check-es5.js              # ES5 compatibility checker
├── ES5_COMPATIBILITY_GUIDE.md # Development guidelines
└── README.md                 # Documentation
```

### ES5 Compatibility

- **Figma-Ready**: All code written in ES5-compatible JavaScript
- **No Modern Syntax**: Avoids arrow functions, template literals, const/let, destructuring
- **Built-in Checker**: Includes `check-es5.js` tool for syntax validation
- **Development Guide**: Comprehensive ES5 conversion reference

## How It Works

### Variable Format Detection

The plugin specifically targets opacity variables with underscore syntax:

| Variable Type    | Format Example      | Description                       |
| ---------------- | ------------------- | --------------------------------- |
| Opacity Variable | `red/25_90`         | Color variable with opacity value |
| Theme Variable   | `color/rose/500_90` | Themed color with opacity         |

### Workflow

1. **Collection Selection**

   - Choose source collection (where variables might be removed)
   - Select target collection (to check variable usage)

2. **Variable Processing**

   - Automatic loading via Figma API (<500 variables)
   - JSON file upload for large collections (>500 variables)
   - Smart detection of underscore syntax variables

3. **Analysis & Output**
   - Cross-reference variables between collections
   - Generate removal recommendations
   - Create organized Figma variables with proper aliases
   - Export audit results as JSON

## Installation

1. **Download** the plugin files from this repository
2. **Open Figma** and navigate to Plugins → Development
3. **Import** the plugin using the `manifest.json` file
4. **Run** the plugin from your Figma file

## Usage

### Auditing Variables

1. Launch the plugin in your Figma file
2. Select your source and target collections
3. Let the plugin analyze variable usage
4. Download the generated audit report
5. Review recommendations for variable cleanup

### Converting CSS Variables

1. Prepare your CSS file with `@theme` variable declarations
2. Upload the CSS file through the plugin interface
3. Choose target collection for new variables
4. Review the conversion preview
5. Apply changes to create Figma variables

## Development

### ES5 Compatibility Check

```bash
node check-es5.js
```

### File Structure

- `code.js` - Main plugin logic with ES5-compatible syntax
- `ui.html` - Plugin interface with embedded CSS and JavaScript
- `check-es5.js` - Development tool for syntax validation

## API Permissions

- `currentuser` - Access user information
- `teamlibrary` - Read and import library variables

## Contributing

1. Ensure all code follows ES5 compatibility guidelines
2. Run `node check-es5.js` before committing
3. Reference `ES5_COMPATIBILITY_GUIDE.md` for syntax rules
4. Test thoroughly in Figma's plugin environment

## License

[Add your license information here]

## Support

For issues, feature requests, or questions, please [open an issue](../../issues) on this repository.
