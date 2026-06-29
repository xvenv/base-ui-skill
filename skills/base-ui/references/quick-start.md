# Base UI Quick Start

## Installation

```bash
pnpm add @base-ui/react
```

All components are included in a single package. Base UI is tree-shakable — only components you use are bundled.

## Portal Setup

Add to your app's global CSS for proper popup stacking:

```css
.root {
  isolation: isolate;
}
```

This creates a separate stacking context so popups always appear above page contents.

## iOS 26+ Safari

For backdrops to cover the visual viewport after scroll:

```css
body {
  position: relative;
}
```

## Basic Usage

```tsx
import { Popover } from '@base-ui/react/popover';

function MyPopover() {
  return (
    <Popover.Root>
      <Popover.Trigger>Open</Popover.Trigger>
      <Popover.Portal>
        <Popover.Positioner sideOffset={8}>
          <Popover.Popup>
            Popover content
          </Popover.Popup>
        </Popover.Positioner>
      </Popover.Portal>
    </Popover.Root>
  );
}
```

## Pre-styled Options

- [shadcn/ui](https://ui.shadcn.com/create?base=base) — pre-styled components using Base UI
- See [Community](https://base-ui.com/react/overview/community) for more

## LLM Resources

- Each docs page has "View as Markdown" link
- `/llms.txt` available in navigation sidebar for AI assistants
