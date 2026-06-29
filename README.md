# base-ui-skill

AI agent knowledge base for [Base UI](https://base-ui.com) — a headless, unstyled React component library from MUI.

## What's Inside

Expert knowledge on all 36+ Base UI components, patterns, and best practices for AI coding assistants.

### Topics Covered

- **Components** — All compound parts (Root, Trigger, Popup, etc.) and their APIs
- **Styling** — Tailwind CSS, CSS Modules, CSS-in-JS approaches
- **Composition** — Render props, detached triggers, nested components
- **Forms** — Field, Form, validation patterns
- **Animation** — CSS transitions, data attributes, hooks
- **TypeScript** — Generics, types, namespace patterns
- **Architecture** — Internal structure, utilities, positioning

## Installation

Copy the `SKILL.md` and `references/` folder into your agent's skills directory:

### Claude Code / MiMoCode

```bash
cp -r . ~/.agents/skills/base-ui
```

### Codex

```bash
cp -r . ~/.codex/skills/base-ui
```

### Project-local

```bash
cp -r . your-project/.agents/skills/base-ui
```

## Usage

Once installed, the skill auto-loads when you ask about Base UI:

```
How do I create a controlled dialog?
What's the anatomy of a Select component?
How to animate a Popover?
```

## File Structure

```
base-ui-skill/
├── SKILL.md              # Main skill file (router + principles)
├── README.md             # This file
└── references/
    ├── quick-start.md    # Install, setup, basic usage
    ├── components.md     # All components list & parts
    ├── styling.md        # Tailwind, CSS Modules, CSS-in-JS
    ├── composition.md    # Render props, detached triggers
    ├── forms.md          # Field, Form, validation
    ├── animation.md      # CSS transitions, data attributes
    ├── typescript.md     # Generics, types, patterns
    └── architecture.md   # Internal structure, utilities
```

## Source

Extracted from the official Base UI documentation (82 MDX files).

## License

MIT
