# Base UI Utilities

## useRender

A custom `render` prop hook for building composable components.

```tsx
import { useRender } from '@base-ui/react/use-render';

// Element render (simple)
const element = useRender(<div />, { className: 'my-class' });

// Callback render (full control)
const element = useRender((props, state) => (
  <span {...props}>{state.open ? 'Open' : 'Closed'}</span>
), { className: 'my-class' });
```

## mergeProps

Merges multiple sets of React props safely:

```tsx
import { mergeProps } from '@base-ui/react/merge-props';

// className: concatenated right-to-left
mergeProps({ className: 'a' }, { className: 'b' }); // 'b a'

// style: merged, rightmost wins
mergeProps({ style: { color: 'red' } }, { style: { fontSize: 12 } });

// event handlers: all invoked, right-to-left
mergeProps({ onClick: a }, { onClick: b }); // b runs first, then a

// ref: only rightmost kept (not merged)
mergeProps({ ref: refA }, { ref: refB }); // only refB
```

Use inside `render` callback:

```tsx
import { mergeProps } from '@base-ui/react/merge-props';

<Menu.Item
  render={(props, state) => (
    <a {...mergeProps(props, { className: 'my-link' })} />
  )}
/>
```

## DirectionProvider

Wraps app for RTL support. Does NOT set HTML `dir` or CSS — you must do that yourself.

```tsx
import { DirectionProvider } from '@base-ui/react/direction-provider';

<DirectionProvider direction="rtl">
  {/* Base UI components adjust behavior */}
</DirectionProvider>
```

## CSPProvider

Provides nonce for inline `<style>`/`<script>` tags under strict Content Security Policy.

```tsx
import { CSPProvider } from '@base-ui/react/csp-provider';

<CSPProvider nonce={nonce}>
  {/* All Base UI inline styles/scripts get the nonce */}
</CSPProvider>
```

## Internal Hooks (from @base-ui/react/internals/)

| Hook | Purpose |
|------|---------|
| `useTimeout` | Safe timeout (replaces `window.setTimeout`) |
| `useAnimationFrame` | Safe rAF (replaces `requestAnimationFrame`) |
| `useIsoLayoutEffect` | SSR-safe `useLayoutEffect` |
| `useStableCallback` | Stable callback ref (replaces `useCallback` in effects) |
| `useTransitionStatus` | Returns `entering`/`entered`/`exiting`/`exited` |
| `useAnimationsFinished` | Fires when element animations complete |
| `useOpenChangeComplete` | Fires after open/close animation finishes |
| `usePressAndHold` | Detects press-and-hold gestures |
| `useValueChanged` | Fires when a value changes |
| `useRenderElement` | Renders elements with ref forwarding |

## Internal Utilities (from @base-ui/react/internals/)

| Utility | Purpose |
|---------|---------|
| `contains` | Shadow DOM-safe `contains()` |
| `getTarget` | Shadow DOM-safe event target |
| `ownerDocument` | Shadow DOM-safe document access |
| `ownerWindow` | Shadow DOM-safe window access |
| `formatErrorMessage` | Formats Base UI error messages |
| `mergeCleanups` | Merges cleanup functions |
| `mergeObjects` | Shallow merge objects |
| `inertValue` | Returns `''` or `undefined` for inert attribute |
| `RequestQueue` | Queues async requests |
| `TimeoutManager` | Manages multiple timeouts |

## useRender Usage Pattern

```tsx
// Simple: just pass an element
<Dialog.Popup render={<motion.div />}>
  Content
</Dialog.Popup>

// With custom props
<Dialog.Popup render={<motion.div initial={{ opacity: 0 }} />}>
  Content
</Dialog.Popup>

// Callback: full control over props and state
<Dialog.Popup
  render={(props, state) => (
    <motion.div
      {...props}
      animate={{ opacity: state.open ? 1 : 0 }}
    />
  )}
>
  Content
</Dialog.Popup>
```
