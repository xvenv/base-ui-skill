# Base UI Architecture

## Package Structure

```
@base-ui/monorepo
├── packages/
│   ├── react/          # @base-ui/react (main component library)
│   └── utils/          # @base-ui/utils (shared utilities)
├── docs/               # Documentation site
└── test/               # E2E and regression tests
```

## Component File Structure

Each component follows this pattern:

```
dialog/
├── root/
│   ├── DialogRoot.tsx          # Main component
│   ├── DialogRootContext.ts    # React context
│   ├── useDialogRoot.ts       # Core logic hook
│   └── useRenderDialogRoot.tsx # Render logic
├── trigger/
├── popup/
├── portal/
├── backdrop/
├── title/
├── description/
├── close/
├── viewport/
├── store/
│   └── DialogHandle.ts        # Detached trigger handle
├── index.ts                    # Public exports
└── index.parts.ts             # Namespace exports
```

## Import Pattern

```tsx
// Tree-shakable import
import { Dialog } from '@base-ui/react/dialog';

// Direct import (less optimal)
import { DialogRoot } from '@base-ui/react/dialog/root';
```

## Internal Architecture

### Root Components

Root components don't render DOM. They provide context:

```tsx
function DialogRoot(props) {
  return useRenderDialogRoot(props, mode);
  // useRenderDialogRoot manages state, context, and renders children
}
```

### useRenderElement

Internal hook for rendering elements with proper ref forwarding and props spreading:

```tsx
import { useRenderElement } from '@base-ui/react/internals/useRenderElement';

const element = useRenderElement('button', { customElement, props, state });
```

### State Management

Components use internal state hooks:

```tsx
// useDialogRoot manages open/close state
// Uses controlled/uncontrolled pattern
// Handles keyboard, pointer, and focus events
```

### Context Pattern

```tsx
// DialogRootContext provides shared state to child parts
const context = React.useContext(DialogRootContext);
```

### Event Details

Standardized event details for callbacks:

```tsx
type EventDetails = {
  reason: string;  // What triggered the change
  nativeEvent: Event;
};
```

## Key Utilities

| Utility | Purpose |
|---------|---------|
| `useTimeout` | Safe timeout (replaces window.setTimeout) |
| `useAnimationFrame` | Safe rAF (replaces requestAnimationFrame) |
| `useIsoLayoutEffect` | SSR-safe useLayoutEffect |
| `useStableCallback` | Stable callback ref (replaces useCallback in effects) |
| `contains` | Shadow DOM-safe contains check |
| `getTarget` | Shadow DOM-safe event target |
| `ownerDocument` | Shadow DOM-safe document access |
| `ownerWindow` | Shadow DOM-safe window access |

## Positioning

Uses `@floating-ui/react-dom` for:

- Popover positioning
- Select popup positioning
- Menu positioning
- Tooltip positioning

Key props: `side`, `align`, `sideOffset`, `alignOffset`, `anchor`

## Accessibility

Every component follows WAI-ARIA patterns:

- Dialog: `role="dialog"`, `aria-modal`, focus trap
- Menu: `role="menu"`, `role="menuitem"`, keyboard navigation
- Select: `role="listbox"`, `role="option"`, typeahead
- Tabs: `role="tablist"`, `role="tab"`, `role="tabpanel"`
