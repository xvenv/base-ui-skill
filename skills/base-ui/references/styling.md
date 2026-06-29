# Base UI Styling Guide

Base UI components are unstyled and compatible with any CSS solution.

## Style Hooks

### className prop

Components accept `className` — can be a string or function receiving state:

```tsx
<Switch.Thumb className="SwitchThumb" />
<Switch.Thumb className={(state) => state.checked ? 'checked' : 'unchecked'} />
```

### Data Attributes

Components expose state via data attributes:

```css
.SwitchThumb[data-checked] { background-color: green; }
.Menu.Item[data-highlighted] { background: blue; }
.Dialog.Popup[data-nested-dialog-open] { opacity: 0.5; }
```

### CSS Variables

Components expose dynamic values:

```css
.Popover.Popup { max-height: var(--available-height); }
.Popover.Positioner { width: var(--anchor-width); }
```

### Style prop

Accepts CSS object or function:

```tsx
<Switch.Thumb style={{ height: '100px' }} />
<Switch.Thumb style={(state) => ({ color: state.checked ? 'red' : 'blue' })} />
```

## Tailwind CSS

```tsx
import { Menu } from '@base-ui/react/menu';

<Menu.Root>
  <Menu.Trigger className="flex h-8 items-center rounded-md border px-3">
    Open
  </Menu.Trigger>
  <Menu.Portal>
    <Menu.Positioner sideOffset={8}>
      <Menu.Popup className="border bg-white py-1">
        <Menu.Item className="px-4 py-2 data-highlighted:bg-neutral-950">
          Option 1
        </Menu.Item>
      </Menu.Popup>
    </Menu.Positioner>
  </Menu.Portal>
</Menu.Root>
```

Tailwind data attribute classes: `data-highlighted:`, `data-checked:`, `data-popup-open:`, etc.

## CSS Modules

```tsx
import { Menu } from '@base-ui/react/menu';
import styles from './menu.module.css';

<Menu.Trigger className={styles.Button}>Open</Menu.Trigger>
<Menu.Popup className={styles.Popup}>...</Menu.Popup>
```

```css
.Button { padding: 8px 16px; }
.Popup { border: 1px solid #ccc; }
```

## CSS-in-JS

```tsx
import styled from '@emotion/styled';
import { Menu } from '@base-ui/react/menu';

const StyledTrigger = styled(Menu.Trigger)`
  padding: 8px 16px;
`;
```

## Common Data Attributes by Component

| Component | Data Attributes |
|-----------|-----------------|
| Switch | `data-checked`, `data-unchecked` |
| Menu.Item | `data-highlighted`, `data-disabled` |
| Dialog | `data-nested-dialog-open` |
| Select.Item | `data-selected`, `data-highlighted` |
| Tabs.Tab | `data-selected` |
| Accordion.Item | `data-open` |
| Collapsible.Root | `data-open` |
