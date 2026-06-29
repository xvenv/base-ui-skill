# Base UI Drawer & Toast

## Drawer

A panel that slides in from the edge with gesture support. Extends Dialog.

### Anatomy

```tsx
import { Drawer } from '@base-ui/react/drawer';

<Drawer.Provider>
  <Drawer.IndentBackground />
  <Drawer.Indent>
    <Drawer.Root>
      <Drawer.Trigger />
      <Drawer.SwipeArea />
      <Drawer.Portal>
        <Drawer.Backdrop />
        <Drawer.Viewport>
          <Drawer.Popup>
            <Drawer.Content>
              <Drawer.Title />
              <Drawer.Description />
              <Drawer.Close />
            </Drawer.Content>
          </Drawer.Popup>
        </Drawer.Viewport>
      </Drawer.Portal>
    </Drawer.Root>
  </Drawer.Indent>
</Drawer.Provider>
```

### Key Props

| Prop | Values | Description |
|------|--------|-------------|
| `swipeDirection` | `down` (default), `up`, `left`, `right` | Swipe-to-dismiss direction |
| `snapPoints` | `number[]` | Snap positions (0-1, fraction of viewport) |
| `snapPoint` | `number` | Controlled snap point |

### Snap Points

```tsx
<Drawer.Root snapPoints={[0.5, 0.75, 1]}>
```

### Gestures

- Swipe to dismiss in `swipeDirection`
- `data-base-ui-swipe-ignore` attribute to prevent swipe on elements
- `<Drawer.Content>` allows text selection without swipe interference

### VirtualKeyboardProvider

For forms in bottom sheets:

```tsx
<Drawer.Root>
  <Drawer.Portal>
    <Drawer.Popup>
      <Drawer.VirtualKeyboardProvider>
        <input />
      </Drawer.VirtualKeyboardProvider>
    </Drawer.Popup>
  </Drawer.Portal>
</Drawer.Root>
```

### Drawer vs Dialog

Use **Drawer** when you need:
- Swipe gestures
- Snap points
- Edge-of-screen slide-in

Use **Dialog** when you need:
- Simple modal/popup
- No gesture support

---

## Toast

Notification system with stacking, promises, and global manager.

### Anatomy

```tsx
import { Toast } from '@base-ui/react/toast';

<Toast.Provider>
  <Toast.Portal>
    <Toast.Viewport>
      <Toast.Root>
        <Toast.Content>
          <Toast.Title />
          <Toast.Description />
          <Toast.Action />
          <Toast.Close />
        </Toast.Content>
      </Toast.Root>
    </Toast.Viewport>
  </Toast.Portal>
</Toast.Provider>
```

### useToastManager Hook

```tsx
const { toasts, add, close, update, promise } = Toast.useToastManager();

// Add a toast
add({ title: 'Saved!', description: 'Your changes were saved.' });

// Promise toast
promise(saveData(), {
  loading: 'Saving...',
  success: 'Saved!',
  error: 'Failed to save',
});

// Update a toast
update(toast.id, { title: 'Updated' });

// Close a toast
close(toast.id);
```

### Global Manager (Outside React Tree)

```tsx
const toastManager = Toast.createToastManager();

// Use in Provider
<Toast.Provider toastManager={toastManager}>

// Use anywhere (even outside React)
toastManager.add({ title: 'Hello' });
toastManager.promise(asyncFn(), { ... });
```

### Stacking Animation

```css
.Toast {
  z-index: calc(1000 - var(--toast-index));
  transform: scale(1 - calc(0.1 * var(--toast-index)));
}

.Toast[data-expanded] {
  transform: translateY(var(--toast-offset-y));
}

.ToastContent {
  overflow: hidden;
  transition: opacity 0.25s;
}

.ToastContent[data-behind] {
  opacity: 0;
}
```

### Keyboard Navigation

- <kbd>F6</kbd> — Jump to toast viewport
- <kbd>Tab</kbd> — Navigate between toasts
- <kbd>Esc</kbd> — Dismiss focused toast

### Toast Props

| Prop | Description |
|------|-------------|
| `swipeDirection` | `right` (default), `left`, `up`, `down` |
| `timeout` | Auto-dismiss timeout in ms |
| `skipDelay` | Delay before showing next toast |

### Anchored Toasts

For positioned toasts with arrows:

```tsx
<Toast.Viewport>
  <Toast.Positioner side="bottom-end" sideOffset={16}>
    <Toast.Root>
      <Toast.Arrow />
      <Toast.Content>...</Toast.Content>
    </Toast.Root>
  </Toast.Positioner>
</Toast.Viewport>
```
