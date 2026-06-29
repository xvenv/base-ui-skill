---
name: base-ui
description: Base UI knowledge base — headless unstyled React component library. Use when asked about Base UI components, APIs, styling patterns, composition, accessibility, or building UI with @base-ui/react.
---

# Base UI — Complete Reference

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

## Detailed References

For deeper dives, see:
- [Components & Compound Parts](references/components.md) - Full anatomy of all 38 components
- [Styling Guide](references/styling.md) - Tailwind, CSS Modules, CSS-in-JS patterns
- [Composition & Render Props](references/composition.md) - Detached triggers, payload, nested composition
- [Forms & Validation](references/forms.md) - Field, Form, constraint validation
- [Advanced Forms](references/forms-advanced.md) - React Hook Form, TanStack, server validation
- [Animation](references/animation.md) - CSS transitions, data attributes
- [Advanced Animation](references/animation-advanced.md) - Motion/framer-motion integration
- [Customization](references/customization.md) - Events, controlled/uncontrolled, cancel/propagation
- [Drawer & Toast](references/drawer-toast.md) - Gestures, snap points, toast manager
- [TypeScript](references/typescript.md) - Generics, types, namespace patterns
- [Architecture](references/architecture.md) - Internal structure, utilities
- [Utilities](references/utilities.md) - useRender, mergeProps, hooks

---

## All Components (38)

### Overlay
Dialog, Popover, Menu, ContextMenu, Tooltip, PreviewCard

### Navigation
Tabs, Menubar, NavigationMenu, Toolbar

### Form
Select, Combobox, Autocomplete, RadioGroup, Radio, Checkbox, CheckboxGroup, Switch, Slider, NumberField, OTPField, Field, Fieldset, Form, Input

### Display
Accordion, Collapsible, AlertDialog, Toast, Drawer, ScrollArea

### Progress
Progress, Meter

### Layout
Separator, Avatar, Button, Toggle, ToggleGroup

---

## Compound Parts

### Dialog
```tsx
import { Dialog } from '@base-ui/react/dialog';
<Dialog.Root>
  <Dialog.Trigger />
  <Dialog.Portal>
    <Dialog.Backdrop />
    <Dialog.Viewport>
      <Dialog.Popup>
        <Dialog.Title />
        <Dialog.Description />
        <Dialog.Close />
      </Dialog.Popup>
    </Dialog.Viewport>
  </Dialog.Portal>
</Dialog.Root>
```

### Popover
```tsx
import { Popover } from '@base-ui/react/popover';
<Popover.Root>
  <Popover.Trigger />
  <Popover.Portal>
    <Popover.Positioner sideOffset={8}>
      <Popover.Popup>
        <Popover.Arrow />
        <Popover.Title />
        <Popover.Description />
        <Popover.Close />
      </Popover.Popup>
    </Popover.Positioner>
  </Popover.Portal>
</Popover.Root>
```

### Menu
```tsx
import { Menu } from '@base-ui/react/menu';
<Menu.Root>
  <Menu.Trigger />
  <Menu.Portal>
    <Menu.Positioner sideOffset={8}>
      <Menu.Popup>
        <Menu.Item />
        <Menu.CheckboxItem />
        <Menu.RadioGroup><Menu.RadioItem /></Menu.RadioGroup>
        <Menu.Separator />
        <Menu.Group><Menu.GroupLabel /></Menu.Group>
        <Menu.SubmenuRoot><Menu.SubmenuTrigger /><Menu.SubmenuPopup /></Menu.SubmenuRoot>
      </Menu.Popup>
    </Menu.Positioner>
  </Menu.Portal>
</Menu.Root>
```

### ContextMenu
Same as Menu but triggered by right-click: `ContextMenu.Root → Trigger → Portal → Positioner → Popup`

### Tooltip
```tsx
import { Tooltip } from '@base-ui/react/tooltip';
<Tooltip.Provider>
  <Tooltip.Root>
    <Tooltip.Trigger />
    <Tooltip.Portal>
      <Tooltip.Positioner>
        <Tooltip.Popup><Tooltip.Arrow /></Tooltip.Popup>
      </Tooltip.Positioner>
    </Tooltip.Portal>
  </Tooltip.Root>
</Tooltip.Provider>
```

### PreviewCard
Same as Popover: `Root → Trigger → Portal → Positioner → Popup → Arrow`

### Select
```tsx
import { Select } from '@base-ui/react/select';
<Select.Root>
  <Select.Label />
  <Select.Trigger><Select.Value /><Select.Icon /></Select.Trigger>
  <Select.Portal>
    <Select.Positioner>
      <Select.Popup>
        <Select.List>
          <Select.Item><Select.ItemText /><Select.ItemIndicator /></Select.Item>
        </Select.List>
        <Select.Group><Select.GroupLabel /></Select.Group>
        <Select.Separator />
      </Select.Popup>
    </Select.Positioner>
  </Select.Portal>
</Select.Root>
```

### Combobox
```tsx
import { Combobox } from '@base-ui/react/combobox';
<Combobox.Root>
  <Combobox.Label />
  <Combobox.InputGroup>
    <Combobox.Input /><Combobox.Trigger /><Combobox.Icon /><Combobox.Clear />
    <Combobox.Chips><Combobox.Chip><Combobox.ChipRemove /></Combobox.Chip></Combobox.Chips>
  </Combobox.InputGroup>
  <Combobox.Portal>
    <Combobox.Positioner>
      <Combobox.Popup>
        <Combobox.List><Combobox.Row><Combobox.Item /></Combobox.Row></Combobox.List>
        <Combobox.Empty /><Combobox.Status />
      </Combobox.Popup>
    </Combobox.Positioner>
  </Combobox.Portal>
</Combobox.Root>
```

### Autocomplete
Same as Combobox: `Root → InputGroup → Portal → Positioner → Popup → List → Row → Item`

### Tabs
```tsx
import { Tabs } from '@base-ui/react/tabs';
<Tabs.Root>
  <Tabs.List><Tabs.Tab /><Tabs.Indicator /></Tabs.List>
  <Tabs.Panel />
</Tabs.Root>
```

### Accordion
```tsx
import { Accordion } from '@base-ui/react/accordion';
<Accordion.Root>
  <Accordion.Item>
    <Accordion.Header><Accordion.Trigger /></Accordion.Header>
    <Accordion.Panel />
  </Accordion.Item>
</Accordion.Root>
```

### Collapsible
```tsx
import { Collapsible } from '@base-ui/react/collapsible';
<Collapsible.Root><Collapsible.Trigger /><Collapsible.Panel /></Collapsible.Root>
```

### Slider
```tsx
import { Slider } from '@base-ui/react/slider';
<Slider.Root>
  <Slider.Label /><Slider.Value />
  <Slider.Control>
    <Slider.Track><Slider.Indicator /><Slider.Thumb /></Slider.Track>
  </Slider.Control>
</Slider.Root>
```

### Switch
```tsx
import { Switch } from '@base-ui/react/switch';
<Switch.Root><Switch.Thumb /></Switch.Root>
```

### Checkbox
```tsx
import { Checkbox } from '@base-ui/react/checkbox';
<Checkbox.Root><Checkbox.Indicator /></Checkbox.Root>
```

### Radio (within RadioGroup)
```tsx
import { Radio } from '@base-ui/react/radio';
<RadioGroup><Radio.Root><Radio.Indicator /></Radio.Root></RadioGroup>
```

### Field
```tsx
import { Field } from '@base-ui/react/field';
<Field.Root name="email">
  <Field.Label /><Field.Control /><Field.Description /><Field.Error /><Field.Validity />
</Field.Root>
```

### Fieldset
```tsx
import { Fieldset } from '@base-ui/react/fieldset';
<Fieldset.Root><Fieldset.Legend /></Fieldset.Root>
```

### Form
```tsx
import { Form } from '@base-ui/react/form';
<Form onSubmit={handleSubmit}><Field.Root>...</Field.Root></Form>
```

### NumberField
```tsx
import { NumberField } from '@base-ui/react/number-field';
<NumberField.Root min={0} max={100}>
  <NumberField.ScrubArea><NumberField.ScrubAreaCursor /></NumberField.ScrubArea>
  <NumberField.Group>
    <NumberField.Decrement /><NumberField.Input /><NumberField.Increment />
  </NumberField.Group>
</NumberField.Root>
```

### OTPField
```tsx
import { OtpField } from '@base-ui/react/otp-field';
<OtpField.Root length={6}><OtpField.Input /><OtpField.Separator /></OtpField.Root>
```

### Progress
```tsx
import { Progress } from '@base-ui/react/progress';
<Progress.Root><Progress.Label /><Progress.Track><Progress.Indicator /></Progress.Track><Progress.Value /></Progress.Root>
```

### Meter
```tsx
import { Meter } from '@base-ui/react/meter';
<Meter.Root><Meter.Label /><Meter.Track><Meter.Indicator /></Meter.Track><Meter.Value /></Meter.Root>
```

### ScrollArea
```tsx
import { ScrollArea } from '@base-ui/react/scroll-area';
<ScrollArea.Root>
  <ScrollArea.Viewport><ScrollArea.Content /></ScrollArea.Viewport>
  <ScrollArea.Scrollbar><ScrollArea.Thumb /></ScrollArea.Scrollbar>
  <ScrollArea.Corner />
</ScrollArea.Root>
```

### Toast
```tsx
import { Toast } from '@base-ui/react/toast';
<Toast.Provider>
  <Toast.Portal><Toast.Viewport>
    <Toast.Root><Toast.Content><Toast.Title /><Toast.Description /><Toast.Action /><Toast.Close /></Toast.Content></Toast.Root>
  </Toast.Viewport></Toast.Portal>
</Toast.Provider>
```

### Drawer
```tsx
import { Drawer } from '@base-ui/react/drawer';
<Drawer.Provider>
  <Drawer.IndentBackground />
  <Drawer.Indent>
    <Drawer.Root>
      <Drawer.Trigger /><Drawer.SwipeArea />
      <Drawer.Portal>
        <Drawer.Backdrop />
        <Drawer.Viewport><Drawer.Popup><Drawer.Content><Drawer.Title /><Drawer.Description /><Drawer.Close /></Drawer.Content></Drawer.Popup></Drawer.Viewport>
      </Drawer.Portal>
    </Drawer.Root>
  </Drawer.Indent>
</Drawer.Provider>
```
Props: `swipeDirection="down"|"up"|"left"|"right"`, `snapPoints={[0.5, 0.75, 1]}`

### NavigationMenu
```tsx
import { NavigationMenu } from '@base-ui/react/navigation-menu';
<NavigationMenu.Root>
  <NavigationMenu.List>
    <NavigationMenu.Item>
      <NavigationMenu.Trigger><NavigationMenu.Icon /></NavigationMenu.Trigger>
      <NavigationMenu.Content><NavigationMenu.Link /></NavigationMenu.Content>
    </NavigationMenu.Item>
  </NavigationMenu.List>
  <NavigationMenu.Portal>
    <NavigationMenu.Positioner><NavigationMenu.Popup><NavigationMenu.Arrow /><NavigationMenu.Viewport /></NavigationMenu.Popup></NavigationMenu.Positioner>
  </NavigationMenu.Portal>
</NavigationMenu.Root>
```

### Menubar
```tsx
import { Menubar } from '@base-ui/react/menubar';
<Menubar><Menu.Root>...</Menu.Root></Menubar>
```

### Toolbar
```tsx
import { Toolbar } from '@base-ui/react/toolbar';
<Toolbar.Root>
  <Toolbar.Button /><Toolbar.Link /><Toolbar.Separator />
  <Toolbar.Group><Toolbar.Button /></Toolbar.Group>
  <Toolbar.Input />
</Toolbar.Root>
```

### Single-Part Components
- **Button** — `<Button />` (use `render` prop for custom elements, `nativeButton={false}` for non-button tags)
- **Input** — `<Input />`
- **Separator** — `<Separator />`
- **Toggle** — `<Toggle />`
- **ToggleGroup** — `<ToggleGroup multiple />`

### Providers
- **DirectionProvider** — `<DirectionProvider direction="rtl">` (RTL support)
- **CSPProvider** — `<CSPProvider nonce="...">` (CSP nonce for inline styles)

---

## Styling

### className (string or function)
```tsx
<Switch.Thumb className="SwitchThumb" />
<Switch.Thumb className={(state) => state.checked ? 'checked' : 'unchecked'} />
```

### Data Attributes
```css
.SwitchThumb[data-checked] { background: green; }
.Menu.Item[data-highlighted] { background: blue; }
.Dialog.Popup[data-nested-dialog-open] { opacity: 0.5; }
```

### CSS Variables
```css
.Popover.Popup { max-height: var(--available-height); }
```

### Style prop
```tsx
<Switch.Thumb style={(state) => ({ color: state.checked ? 'red' : 'blue' })} />
```

### Tailwind CSS
```tsx
<Menu.Popup className="border bg-white py-1">
  <Menu.Item className="px-4 py-2 data-highlighted:bg-neutral-950 data-highlighted:text-white">
```

### CSS Modules
```tsx
import styles from './menu.module.css';
<Menu.Trigger className={styles.Button}>
```

### Common Data Attributes
| Component | Attributes |
|-----------|-----------|
| Switch | `data-checked`, `data-unchecked` |
| Menu.Item | `data-highlighted`, `data-disabled` |
| Dialog | `data-nested-dialog-open` |
| Select.Item | `data-selected`, `data-highlighted` |
| Tabs.Tab | `data-selected` |
| Collapsible/Accordion | `data-open` |

---

## Animation

### CSS Transitions (recommended — can be cancelled)
```css
.Popup {
  transition: transform 150ms, opacity 150ms;
}
.Popup[data-starting-style],
.Popup[data-ending-style] {
  opacity: 0;
  transform: scale(0.9);
}
```

### CSS Animations
```css
.Popup[data-open] { animation: scaleIn 250ms ease-out; }
.Popup[data-closed] { animation: scaleOut 250ms ease-in; }
```

### Motion (Framer Motion)
```tsx
// Unmount mode
<Popover.Portal keepMounted>
  <Popover.Popup render={<motion.div initial={{opacity:0}} animate={{opacity:1}} exit={{opacity:0}} />} />
</Popover.Portal>

// keepMounted mode
<Popover.Popup render={(props, state) => <motion.div {...props} animate={{opacity: state.open ? 1 : 0}} />} />
```

### Tailwind Animation
```tsx
<Menu.Popup className="transition data-starting-style:scale-95 data-starting-style:opacity-0 data-ending-style:scale-95 data-ending-style:opacity-0">
```

### Animation Attributes
| Attribute | When |
|-----------|------|
| `data-starting-style` | Before enter |
| `data-ending-style` | During exit |
| `data-open` | Open |
| `data-closed` | Closing |

---

## Composition

### Render Prop
```tsx
<Menu.Trigger render={<MyButton size="md" />}>Open</Menu.Trigger>
```

### Render Function (full control)
```tsx
<Switch.Thumb render={(props, state) => <span {...props}>{state.checked ? '✓' : '✗'}</span>} />
```

### Detached Triggers
```tsx
const handle = Dialog.createHandle();
<Dialog.Trigger handle={handle}>Open</Dialog.Trigger>
<Dialog.Root handle={handle}>...</Dialog.Root>
```

### Payload Pattern
```tsx
const handle = Dialog.createHandle<{ title: string }>();
<Dialog.Trigger handle={handle} payload={{ title: 'Hello' }}>Open</Dialog.Trigger>
<Dialog.Root handle={handle}>{({ payload }) => <Dialog.Title>{payload?.title}</Dialog.Title>}</Dialog.Root>
```

### Controlled State
```tsx
const [open, setOpen] = React.useState(false);
<Dialog.Root open={open} onOpenChange={setOpen}>
```

---

## Events & Customization

### eventDetails
```tsx
onOpenChange: (open, eventDetails) => void
// eventDetails: { reason, event, cancel(), allowPropagation() }
```

### Cancel Events
```tsx
<Tooltip.Root onOpenChange={(open, e) => { if (e.reason === 'trigger-press') e.cancel(); }}>
```

### Common Reasons
`triggerPress`, `outsidePress`, `escapeKey`, `closePress`, `focusOut`, `imperativeAction`

---

## Forms

### Basic
```tsx
<Form onSubmit={handleSubmit}>
  <Field.Root name="email">
    <Field.Label>Email</Field.Label>
    <Field.Control />
    <Field.Error />
  </Field.Root>
</Form>
```

### Validation
```tsx
<Field.Root name="email" validate={(v) => v.includes('@') ? null : 'Invalid'} validationMode="onChange" validationDebounceTime={300}>
```

### React Hook Form
```tsx
<Controller name="email" control={control} render={({field}) => (
  <Field.Root name={field.name} invalid={!!error}>
    <Field.Control ref={field.ref} value={field.value} onValueChange={field.onChange} onBlur={field.onBlur} />
    <Field.Error match={!!error}>{error?.message}</Field.Error>
  </Field.Root>
)} />
```

### Server Validation
```tsx
<Form errors={serverErrors} onFormSubmit={async (values) => await submit(values)}>
```

### Labeling Rules
- Input, NumberField, OTPField → `<Field.Label>`
- Select → `<Select.Label>`
- Checkbox, Radio, Switch → wrap with `<Field.Label>`
- Fallback → `aria-label`

---

## Utilities

```tsx
import { mergeProps } from '@base-ui/react/merge-props';
mergeProps({ className: 'a' }, { className: 'b' }); // 'b a'
mergeProps({ onClick: a }, { onClick: b }); // b then a
```

### Internal Hooks (from @base-ui/react/internals/)
- `useTimeout` — safe setTimeout
- `useAnimationFrame` — safe requestAnimationFrame
- `useIsoLayoutEffect` — SSR-safe useLayoutEffect
- `useStableCallback` — stable callback ref
- `useTransitionStatus` — entering/entered/exiting/exited
- `useAnimationsFinished` — detect animation end

---

## Docs
https://base-ui.com/react/overview/quick-start
