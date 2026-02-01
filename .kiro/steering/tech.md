# Technology Stack

## Platform

- **FoundryVTT Module** for the SWADE (Savage Worlds Adventure Edition) system
- **Minimum Foundry Version**: 10
- **Verified Foundry Version**: 11

## Tech Stack

- **JavaScript ES6 Modules** (type: "module" in package.json)
- **No build system** - direct JavaScript files loaded via esmodules
- **No external dependencies** - vanilla JavaScript implementation

## Project Structure

- Entry point: `scripts/start.js` (loaded via module.json esmodules)
- Class-based architecture in `scripts/class/`
- Utility functions in `scripts/gb.js` and `scripts/st.js`
- Foundry Hooks system for event handling

## Key Libraries & APIs

- **FoundryVTT API**: Hooks, game objects, ChatMessage, Roll/SwadeRoll classes
- **SWADE System API**: game.swade namespace, SWADE-specific data structures
- **Dice So Nice** (optional): 3D dice animation support via game.dice3d

## Common Commands

No build, test, or compilation commands - this is a pure runtime module. Development workflow:

1. Edit JavaScript files directly
2. Reload FoundryVTT to test changes
3. Check browser console for errors

## Module Loading

The module is loaded by FoundryVTT via `module.json` which specifies:
- ES modules to load (`scripts/start.js`)
- CSS files (`css/swadetools.css`)
- Language files (`lang/*.json`)
- Compendium packs (`packs/macros.db`)
