# Base UI Composition Guide

## Render Prop Pattern

Use `render` to compose Base UI parts with custom components:

```tsx
<Menu.Trigger render={<MyButton size="md" />}>
  Open menu
</Menu.Trigger>
```

Custom component must forward ref and spread props.

## Changing Default Elements

Override the rendered element:

```tsx
<Menu.Item render={<a href="/link" />}>
  Link item
</Menu.Item>
```

## Nested Composition

Layer multiple Base UI components:

```tsx
<Dialog.Root>
  <Tooltip.Root>
    <Tooltip.Trigger
      render={
        <Dialog.Trigger
          render={<Menu.Trigger render={<MyButton />}>Open</Menu.Trigger>}
        />
      }
    />
    <Tooltip.Portal>...</Tooltip.Portal>
  </Tooltip.Root>
  <Dialog.Portal>...</Dialog.Portal>
</Dialog.Root>
```

## Render Function

For full control over props and state:

```tsx
<Switch.Thumb
  render={(props, state) => (
    <span {...props}>
      {state.checked ? <CheckedIcon /> : <UncheckedIcon />}
    </span>
  )}
/>
```

## Detached Triggers

Link trigger and root when they're in different DOM locations:

```tsx
const myDialog = Dialog.createHandle();

// Trigger anywhere
<Dialog.Trigger handle={myDialog}>Open</Dialog.Trigger>

// Root anywhere else
<Dialog.Root handle={myDialog}>...</Dialog.Root>
```

## Multiple Triggers

One component, multiple triggers:

```tsx
const myPopover = Popover.createHandle();

<Popover.Trigger handle={myPopover}>Trigger 1</Popover.Trigger>
<Popover.Trigger handle={myPopover}>Trigger 2</Popover.Trigger>
<Popover.Root handle={myPopover}>...</Popover.Root>
```

## Payload Pattern

Pass data from trigger to root:

```tsx
const myDialog = Dialog.createHandle<{ title: string }>();

<Dialog.Trigger handle={myDialog} payload={{ title: 'Hello' }}>
  Open
</Dialog.Trigger>

<Dialog.Root handle={myDialog}>
  {({ payload }) => (
    <Dialog.Portal>
      <Dialog.Popup>
        <Dialog.Title>{payload?.title}</Dialog.Title>
      </Dialog.Popup>
    </Dialog.Portal>
  )}
</Dialog.Root>
```

## Controlled State

```tsx
const [open, setOpen] = React.useState(false);

<Dialog.Root open={open} onOpenChange={setOpen}>
  <Dialog.Trigger>Open</Dialog.Trigger>
  ...
</Dialog.Root>
```

## Event Details

`onOpenChange` receives event details with reason:

```tsx
<Dialog.Root
  onOpenChange={(open, eventDetails) => {
    console.log(eventDetails.reason); // 'triggerPress', 'escapeKey', etc.
  }}
>
```
