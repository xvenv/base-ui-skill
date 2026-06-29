# Base UI TypeScript Guide

## Generic Components

Some components accept generic type parameters:

```tsx
// Select with object values
<Select.Root<MyItem[]>>
  <Select.Item>...</Select.Item>
</Select.Root>

// Typed wrapper component
function MySelect<Value, Multiple extends boolean | undefined = false>(
  props: Select.Root.Props<Value, Multiple>
): React.JSX.Element {
  return <Select.Root {...props} />;
}
```

## Event Details Types

```tsx
import type { BaseUIChangeEventDetails } from '@base-ui/react/internals/createBaseUIEventDetails';

// Dialog change event details
type DialogChangeEventDetails = BaseUIChangeEventDetails<'triggerPress' | 'escapeKey'> & {
  preventUnmountOnClose(): void;
};
```

## Handle Types

```tsx
// Typed handle with payload
const myDialog = Dialog.createHandle<{ userId: string }>();

// Usage
<Dialog.Trigger handle={myDialog} payload={{ userId: '123' }}>
  Open
</Dialog.Trigger>
```

## Component State Types

```tsx
// Each component exports its state type
import type { DialogRootState } from '@base-ui/react/dialog';
import type { SwitchThumbState } from '@base-ui/react/switch';
```

## Render Function Props

```tsx
<Switch.Thumb
  render={(props, state) => {
    // props: React.HTMLAttributes<HTMLSpanElement>
    // state: { checked: boolean }
    return <span {...props} />;
  }}
/>
```

## Namespace Pattern

Components export types via namespace:

```tsx
import { Dialog } from '@base-ui/react/dialog';

// All types available via namespace
type Props = Dialog.Root.Props;
type State = Dialog.Root.State;
type Actions = Dialog.Root.Actions;
```

## Forwarded Ref Components

All parts forward refs. Custom render components must also forward:

```tsx
const MyButton = React.forwardRef<HTMLButtonElement, ButtonProps>(
  (props, ref) => <button ref={ref} {...props} />
);
```

## Strict Mode

Base UI works with React.StrictMode. All effects are idempotent.

## React 17/18/19 Support

Peer dependencies: `react: ^17 || ^18 || ^19`

Some features require `use-sync-external-store` for React 17/18 compatibility.
