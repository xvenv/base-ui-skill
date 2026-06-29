# Base UI Customization Guide

## Base UI Events

Change events (`onOpenChange`, `onValueChange`, `onPressedChange`) are custom to Base UI.

```tsx
onOpenChange: (open, eventDetails) => void
onValueChange: (value, eventDetails) => void
onPressedChange: (pressed, eventDetails) => void
```

## eventDetails Object

```tsx
interface BaseUIChangeEventDetails {
  reason: string;        // Why the change occurred
  event: Event;          // Native DOM event
  cancel: () => void;    // Prevent state change
  allowPropagation: () => void;  // Allow DOM event propagation
  isCanceled: boolean;
  isPropagationAllowed: boolean;
}
```

### Canceling Events

Prevent state change without controlled mode:

```tsx
<Tooltip.Root
  onOpenChange={(open, eventDetails) => {
    if (eventDetails.reason === 'trigger-press') {
      eventDetails.cancel();  // Prevents state update
    }
  }}
>
```

### Allowing Propagation

Override default Esc propagation blocking:

```tsx
<Tooltip.Root
  onOpenChange={(open, eventDetails) => {
    if (eventDetails.reason === 'escape-key') {
      eventDetails.allowPropagation();  // Let parent popups close too
    }
  }}
>
```

## Preventing Base UI from Handling React Events

```tsx
<NumberField.Input
  onPaste={(event) => {
    event.preventBaseUIHandler();  // Escape hatch
  }}
/>
```

## Controlled vs Uncontrolled

### Uncontrolled (default)

```tsx
<Dialog.Root>  {/* Manages own state */}
  <Dialog.Trigger />
</Dialog.Root>
```

### Controlled

```tsx
const [open, setOpen] = React.useState(false);

<Dialog.Root open={open} onOpenChange={setOpen}>
  <Dialog.Trigger />
</Dialog.Root>
```

### Imperative Control

```tsx
const [open, setOpen] = React.useState(false);

React.useEffect(() => {
  setTimeout(() => setOpen(true), 1000);
}, []);

<Dialog.Root open={open} onOpenChange={setOpen}>
```

## Event Reason Values

Common reasons across components:

| Reason | Description |
|--------|-------------|
| `triggerPress` | Trigger element clicked |
| `outsidePress` | Click outside the component |
| `escapeKey` | Esc key pressed |
| `closePress` | Close button clicked |
| `focusOut` | Focus moved outside |
| `imperativeAction` | Programmatic close |
| `arrowUp` / `arrowDown` | Arrow key navigation |
| `typeahead` | Character typed for typeahead |

## Data Attributes for Customization

Use data attributes to style based on state:

```css
/* All components */
[data-open] { /* Component is open */ }
[data-closed] { /* Component is closed */ }

/* Dialog */
[data-nested-dialog-open] { /* Parent when child is open */ }

/* Menu/Select */
[data-highlighted] { /* Item is highlighted */ }

/* Switch */
[data-checked] { /* Switch is on */ }
[data-unchecked] { /* Switch is off */ }

/* Tabs */
[data-selected] { /* Tab is selected */ }

/* Collapsible/Accordion */
[data-open] { /* Section is expanded */ }
```

## CSS Variables for Customization

Components expose dynamic values:

```css
/* Popover */
--available-height
--available-width
--anchor-width
--anchor-height
--transform-origin

/* Toast */
--toast-index
--toast-offset-y

/* Select */
--positioner-width
--positioner-height
```

## Actions Ref (Manual Unmount)

For full control over unmounting after animations:

```tsx
const actionsRef = React.useRef(null);

<Popover.Root actionsRef={actionsRef}>
  <Popover.Portal keepMounted>
    <Popover.Popup
      render={
        <motion.div
          onAnimationComplete={() => {
            if (!open) {
              actionsRef.current.unmount();
            }
          }}
        />
      }
    />
  </Popover.Portal>
</Popover.Root>
```
