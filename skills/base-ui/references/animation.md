# Base UI Animation Guide

## CSS Transitions

Most components support CSS transitions via data attributes:

```css
.Menu.Popup {
  transition: transform 200ms, opacity 200ms;
}
.Menu.Popup[data-starting-style] {
  transform: scale(0.95);
  opacity: 0;
}
.Menu.Popup[data-ending-style] {
  transform: scale(0.95);
  opacity: 0;
}
```

## Data Attributes for Animation

| Attribute | Meaning |
|-----------|---------|
| `data-starting-style` | Applied before enter animation |
| `data-ending-style` | Applied during exit animation |
| `data-open` | Component is open |
| `data-closed` | Component is closed |

## Dialog Animation

```css
.Dialog.Popup {
  transition: transform 200ms ease-out, opacity 200ms ease-out;
}
.Dialog.Popup[data-starting-style] {
  transform: scale(0.95);
  opacity: 0;
}
.Dialog.Popup[data-ending-style] {
  transform: scale(0.95);
  opacity: 0;
}
.Dialog.Backdrop {
  transition: opacity 200ms ease-out;
}
.Dialog.Backdrop[data-starting-style] {
  opacity: 0;
}
```

## Popover Animation

Position and size transitions on Positioner:

```css
.Popover.Positioner {
  transition: left 200ms, top 200ms, width 200ms, height 200ms;
}
```

Content transitions using Viewport:

```tsx
<Popover.Viewport>
  <div data-current>Current content</div>
</Popover.Viewport>
```

Viewport provides `data-activation-direction` for direction-aware animations.

## Collapsible Animation

```css
.Collapsible.Content {
  transition: height 200ms ease-out;
  overflow: hidden;
}
.Collapsible.Content[data-starting-style] {
  height: 0;
}
```

## Accordion Animation

```css
.Accordion.Content {
  transition: height 200ms ease-out;
  overflow: hidden;
}
.Accordion.Content[data-starting-style] {
  height: 0;
}
```

## useTransitionStatus Hook

For imperative animation control:

```tsx
import { useTransitionStatus } from '@base-ui/react/internals/useTransitionStatus';

const { status, ownerState } = useTransitionStatus(open);
// status: 'entering' | 'entered' | 'exiting' | 'exited'
```

## useAnimationsFinished Hook

Detect when animations complete:

```tsx
import { useAnimationsFinished } from '@base-ui/react/internals/useAnimationsFinished';

const isFinished = useAnimationsFinished(elementRef);
```

## Tailwind CSS Transitions

```tsx
<Menu.Popup className="transition data-starting-style:scale-95 data-starting-style:opacity-0 data-ending-style:scale-95 data-ending-style:opacity-0">
```
