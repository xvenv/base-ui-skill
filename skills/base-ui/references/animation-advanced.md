# Base UI Animation — Advanced Guide

## CSS Transitions (Recommended)

Transitions can be smoothly cancelled midway — preferred over animations.

```css
.Popup {
  transition: transform 150ms, opacity 150ms;

  &[data-starting-style],
  &[data-ending-style] {
    opacity: 0;
    transform: scale(0.9);
  }
}
```

## CSS Animations

For non-cancellable animations:

```css
@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}

@keyframes scaleOut {
  from { opacity: 1; transform: scale(1); }
  to { opacity: 0; transform: scale(0.9); }
}

.Popup[data-open] { animation: scaleIn 250ms ease-out; }
.Popup[data-closed] { animation: scaleOut 250ms ease-in; }
```

## Motion (Framer Motion) Integration

Base UI uses `element.getAnimations()` to detect animation finish. `opacity` must be animated (use `opacity: 0.9999` if not visible).

### Unmounted Components (Default)

Most popovers unmount when closed. Use `AnimatePresence` + `keepMounted`:

```tsx
const [open, setOpen] = React.useState(false);

<Popover.Root open={open} onOpenChange={setOpen}>
  <Popover.Trigger>Trigger</Popover.Trigger>
  <AnimatePresence>
    {open && (
      <Popover.Portal keepMounted>
        <Popover.Positioner>
          <Popover.Popup
            render={
              <motion.div
                initial={{ opacity: 0, scale: 0.8 }}
                animate={{ opacity: 1, scale: 1 }}
                exit={{ opacity: 0, scale: 0.8 }}
              />
            }
          />
        </Popover.Positioner>
      </Popover.Portal>
    )}
  </AnimatePresence>
</Popover.Root>
```

### keepMounted Components

For components that stay in DOM, animate based on `open` state:

```tsx
<Popover.Root>
  <Popover.Portal keepMounted>
    <Popover.Positioner>
      <Popover.Popup
        render={(props, state) => (
          <motion.div
            {...props}
            initial={false}
            animate={{
              opacity: state.open ? 1 : 0,
              scale: state.open ? 1 : 0.8,
            }}
          />
        )}
      />
    </Popover.Positioner>
  </Popover.Portal>
</Popover.Root>
```

### Select with Motion

Select is initially unmounted but stays mounted after first interaction — mix both approaches.

## Manual Unmount with actionsRef

```tsx
const actionsRef = React.useRef(null);

<Popover.Root open={open} onOpenChange={setOpen} actionsRef={actionsRef}>
  <AnimatePresence>
    {open && (
      <Popover.Portal keepMounted>
        <Popover.Popup
          render={
            <motion.div
              initial={{ scale: 0 }}
              animate={{ scale: 1 }}
              exit={{ scale: 0 }}
              onAnimationComplete={() => {
                if (!open) actionsRef.current.unmount();
              }}
            />
          }
        />
      </Popover.Portal>
    )}
  </AnimatePresence>
</Popover.Root>
```

## Tailwind CSS Animation Classes

```tsx
<Menu.Popup className="transition data-starting-style:scale-95 data-starting-style:opacity-0 data-ending-style:scale-95 data-ending-style:opacity-0">

<Dialog.Popup className="transition data-starting-style:scale-95 data-starting-style:opacity-0">

<Collapsible.Content className="transition data-starting-style:h-0 data-starting-style:overflow-hidden">
```

## Component-Specific Animation Patterns

### Collapsible / Accordion

```css
.Content {
  transition: height 200ms ease-out;
  overflow: hidden;
}
.Content[data-starting-style] { height: 0; }
```

### Popover Position Animation

```css
.Popover.Positioner {
  transition: left 200ms, top 200ms, width 200ms, height 200ms;
}
```

### Toast Stacking

```css
.Toast {
  z-index: calc(1000 - var(--toast-index));
  transform: scale(1 - calc(0.1 * var(--toast-index)));
}

.Toast[data-expanded] {
  transform: translateY(var(--toast-offset-y));
}
```

## Hooks

| Hook | Purpose |
|------|---------|
| `useTransitionStatus` | Returns `entering`, `entered`, `exiting`, `exited` |
| `useAnimationsFinished` | Fires when element animations complete |
| `useOpenChangeComplete` | Fires after open/close animation finishes |

## Key Attributes Summary

| Attribute | When Applied |
|-----------|-------------|
| `data-starting-style` | Before enter transition |
| `data-ending-style` | During exit transition |
| `data-open` | Component is open |
| `data-closed` | Component is closing |
