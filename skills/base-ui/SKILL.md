---
name: base-ui
description: Base UI knowledge base — headless unstyled React component library. Use when asked about Base UI components, APIs, styling patterns, composition, accessibility, or building UI with @base-ui/react.
---

# Base UI — Quick Reference

Headless, unstyled React component library from MUI. Provides behavior + accessibility; you provide the CSS.

## Install

```bash
pnpm add @base-ui/react
```

Portal isolation (required for popups):
```css
.root { isolation: isolate; }
```

## Core Concepts

- **Compound Parts** — Every component = `Component.Root` + sub-parts (Trigger, Popup, etc.)
- **Unstyled** — No CSS bundled. Use className, data attributes, CSS variables
- **Tree-shakable** — Import from `@base-ui/react/{component}`
- **React 17/18/19** — Full support

---

## All Components (40)

| Category | Components |
|----------|-----------|
| **Overlay** | Dialog, Popover, Menu, ContextMenu, Tooltip, PreviewCard |
| **Navigation** | Tabs, Menubar, NavigationMenu, Toolbar |
| **Form** | Select, Combobox, Autocomplete, RadioGroup, Radio, Checkbox, CheckboxGroup, Switch, Slider, NumberField, OTPField, Field, Fieldset, Form, Input |
| **Display** | Accordion, Collapsible, AlertDialog, Toast, Drawer, ScrollArea |
| **Progress** | Progress, Meter |
| **Layout** | Separator, Avatar, Button, Toggle, ToggleGroup |
| **Providers** | DirectionProvider, CSPProvider |

---

## Import Pattern

```tsx
import { ComponentName } from '@base-ui/react/{component-kebab-case}';
// Example:
import { Dialog } from '@base-ui/react/dialog';
import { NumberField } from '@base-ui/react/number-field';
```

---

## Compound Parts (Quick)

| Component | Parts |
|-----------|-------|
| Dialog | Root → Trigger → Portal → Backdrop → Viewport → Popup → Title, Description, Close + `createHandle()` |
| Popover | Root → Trigger → Portal → Backdrop → Positioner → Popup → Arrow, Title, Description, Close, Viewport + `createHandle()` |
| Menu | Root → Trigger → Portal → Backdrop → Positioner → Popup → Arrow, Viewport, Item, LinkItem, CheckboxItem, RadioGroup, Separator, Group, SubmenuRoot + `createHandle()` |
| ContextMenu | Root, Trigger (own) + re-exports all Menu parts |
| Tooltip | Provider → Root → Trigger → Portal → Positioner → Popup → Arrow, Viewport + `createHandle()` |
| PreviewCard | Root → Trigger → Portal → Backdrop → Positioner → Popup → Arrow, Viewport + `createHandle()` |
| Select | Root → Label → Trigger (Value, Icon) → Portal → Backdrop → Positioner → Popup → List → Item (ItemText, ItemIndicator), Group, Separator, ScrollArrows |
| Combobox | Root → Label → InputGroup (Input, Trigger, Icon, Clear, Chips) → Portal → Backdrop → Positioner → Popup → List → Row → Item, Status, Empty, Collection + `useFilter`, `useFilteredItems` |
| Autocomplete | Root, Value, Trigger, InputGroup (own) + re-exports Combobox parts + `useFilter`, `useFilteredItems` |
| Tabs | Root → List → Tab, Indicator → Panel |
| Accordion | Root → Item → Header → Trigger → Panel |
| Avatar | Root → Image, Fallback |
| Drawer | Provider → IndentBackground → Indent → Root → Trigger, SwipeArea → Portal → Backdrop → Viewport → Popup → Content → Title, Description, Close + `createHandle()` |
| Toast | Provider → Portal → Viewport → Root → Content → Title, Description, Action, Close, Positioner, Arrow |
| NavigationMenu | Root → List → Item → Trigger, Icon → Content, Link → Portal → Backdrop → Positioner → Popup → Arrow, Viewport |
| ScrollArea | Root → Viewport → Content → Scrollbar → Thumb, Corner |
| Slider | Root → Label, Value → Control → Track → Indicator, Thumb |
| NumberField | Root → ScrubArea → ScrubAreaCursor → Group → Decrement, Input, Increment |
| OTPField | Root → Input (multiple), Separator |
| Field | Root → Label, Control, Description, Item, Error, Validity |

Single-part: Button, Input, Separator, Toggle, ToggleGroup, Form, CheckboxGroup

---

## Styling Cheat Sheet

```tsx
// className string
<Switch.Thumb className="thumb" />

// className function
<Switch.Thumb className={(state) => state.checked ? 'on' : 'off'} />

// Data attributes in CSS
[data-checked] { background: green; }
[data-highlighted] { background: blue; }
[data-starting-style] { opacity: 0; }  /* before enter */
[data-ending-style] { opacity: 0; }    /* during exit */

// Tailwind
<Menu.Item className="data-highlighted:bg-neutral-950">
```

---

## Composition Cheat Sheet

```tsx
// Render prop
<Menu.Trigger render={<MyButton />}>Open</Menu.Trigger>

// Render function
<Switch.Thumb render={(props, state) => <span {...props}>{state.checked ? '✓' : '✗'}</span>} />

// Detached trigger
const handle = Dialog.createHandle();
<Dialog.Trigger handle={handle}>Open</Dialog.Trigger>
<Dialog.Root handle={handle}>...</Dialog.Root>

// Controlled
<Dialog.Root open={open} onOpenChange={setOpen}>
```

---

## Forms Cheat Sheet

```tsx
<Form onSubmit={handleSubmit}>
  <Field.Root name="email" validate={(v) => v.includes('@') ? null : 'Invalid'}>
    <Field.Label>Email</Field.Label>
    <Field.Control />
    <Field.Error />
  </Field.Root>
</Form>
```

Labeling: Input/NumberField/OTPField → `<Field.Label>`, Select → `<Select.Label>`, Checkbox/Radio/Switch → wrap with `<Field.Label>`, fallback → `aria-label`

---

## Utilities

```tsx
import { mergeProps } from '@base-ui/react/merge-props';
```

Internal hooks: `useTimeout`, `useAnimationFrame`, `useIsoLayoutEffect`, `useStableCallback`, `useTransitionStatus`, `useAnimationsFinished`

---

## Detailed References

- [Components & Compound Parts](references/components.md) — Full anatomy of all 40 components
- [Styling Guide](references/styling.md) — Tailwind, CSS Modules, CSS-in-JS
- [Composition & Render Props](references/composition.md) — Detached triggers, payload
- [Forms & Validation](references/forms.md) — Field, Form, constraint validation
- [Advanced Forms](references/forms-advanced.md) — React Hook Form, TanStack, server validation
- [Animation](references/animation.md) — CSS transitions, data attributes
- [Advanced Animation](references/animation-advanced.md) — Motion/framer-motion
- [Customization](references/customization.md) — Events, controlled/uncontrolled
- [Drawer & Toast](references/drawer-toast.md) — Gestures, snap points, toast manager
- [TypeScript](references/typescript.md) — Generics, types, namespace patterns
- [Architecture](references/architecture.md) — Internal structure, utilities
- [Utilities](references/utilities.md) — useRender, mergeProps, hooks

## Source Docs

Official MDX docs: `docs/src/app/(docs)/react/components/{component}/page.mdx`
Handbook: `docs/src/app/(docs)/react/handbook/{topic}/page.mdx`

## Docs
https://base-ui.com/react/overview/quick-start
