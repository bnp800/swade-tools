# Project Structure

## Root Files

- `module.json` - FoundryVTT module manifest (metadata, compatibility, entry points)
- `package.json` - Minimal package file marking project as ES module
- `README.md` - User-facing documentation with features and screenshots
- `UPDATEHISTORY.md` - Version history for releases prior to v1.12

## Directory Organization

### `/scripts/`
Main JavaScript code organized by purpose:

- `start.js` - Module entry point, registers all Foundry hooks and initializes game.swadetools API
- `gb.js` - Global utility functions and constants (module-wide helpers)
- `st.js` - Public API functions exposed via game.swadetools namespace
- `settings.js` - Module settings registration

### `/scripts/class/`
Object-oriented class implementations:

- `BasicRoll.js` - Base roll mechanics (dice rolling, raise counting, critical detection)
- `Char.js` - Character/actor data access and manipulation
- `CharRoll.js` - Character-specific roll handling
- `CharUp.js` - Character update logic
- `CombatControl.js` - Combat turn/round management
- `ItemDialog.js` - Dialog UI for items (weapons/powers)
- `ItemRoll.js` - Item-based roll mechanics
- `MacroControl.js` - Macro execution logic
- `RollControl.js` - Chat message roll processing
- `SettingCustom.js`, `SettingName.js`, `SettingRules.js` - Settings UI forms
- `SheetControl.js` - Actor sheet event binding
- `StatusIcon.js` - Status effect icon management
- `SystemRoll.js` - System-level roll interface
- `TokenHud.js` - Token HUD customization

### `/lang/`
Internationalization files (JSON format):
- `en.json`, `fr.json`, `pt-BR.json`, `es.json`, `it.json`, `de.json`, `ca.json`, `cn.json`
- Key format: `SWADETOOLS.KeyName`

### `/css/`
- `swadetools.css` - Module styling

### `/icons/`
Status effect and UI icons (PNG format):
- Status: `shaken.png`, `stunned.png`, `distracted.png`, `vulnerable.png`, `entangled.png`, `bound.png`
- Wounds: `w1.png` through `w6.png`
- Fatigue: `f1.png`, `f2.png`
- Macros: `macro-*.png`
- Other: `benny.png`, `boost-trait.png`, `lower-trait.png`

### `/templates/`
Handlebars templates for settings dialogs:
- `setting-custom.html`, `setting-name.html`, `setting-rules.html`

### `/packs/`
FoundryVTT compendium packs:
- `macros.db` - Pre-built macros for common actions
- `macros/` - LevelDB database files for the macros compendium

## Code Architecture Patterns

### Hook-Based Event System
The module uses Foundry's Hooks system extensively:
- `ready` - Initialize module, register settings, modify CONFIG
- `renderChatMessage` - Process rolls, add custom buttons
- `updateActor` / `updateToken` - React to character/token changes
- `updateCombat` - Handle combat turn/round transitions
- `renderActorSheet` - Rebind custom sheet controls

### Class Hierarchy
- `BasicRoll` - Base class for all roll types
- `CharRoll extends BasicRoll` - Character-specific rolls
- `ItemRoll extends BasicRoll` - Item-based rolls
- `SystemRoll` - Public API wrapper for rolls

### Data Access Pattern
- `Char` class wraps actor/token data access
- `data(key)` method navigates nested properties (e.g., 'wounds.value')
- Handles both actor and token contexts transparently

### Settings Management
- Custom FormApplication classes for complex settings UI
- Settings stored in Foundry's game.settings API
- Naming conventions: edges/abilities/traits can be customized per language/setting
