# Base UI Components Reference

## All Components (40)

### Overlay
- **Dialog** — Modal/popup on top of page
- **Popover** — Anchored popup
- **Menu** — Dropdown menu
- **ContextMenu** — Right-click menu
- **Tooltip** — Hover info popup
- **PreviewCard** — Hover preview popup

### Navigation
- **Tabs** — Tabbed interface
- **Menubar** — Horizontal menu bar
- **NavigationMenu** — Site navigation
- **Toolbar** — Toolbar with keyboard nav

### Form
- **Select** — Dropdown select
- **Combobox** — Filterable select
- **Autocomplete** — Autocomplete input
- **RadioGroup** — Radio button group
- **Radio** — Single radio button
- **Checkbox** — Single checkbox
- **CheckboxGroup** — Checkbox group
- **Switch** — Toggle switch
- **Slider** — Range slider
- **NumberField** — Numeric input
- **OTPField** — One-time password
- **Field** — Form field wrapper
- **Fieldset** — Field group
- **Form** — Form with validation
- **Input** — Text input

### Display
- **Accordion** — Collapsible sections
- **Collapsible** — Single collapsible
- **AlertDialog** — Confirmation dialog
- **Toast** — Notification popup
- **Drawer** — Slide-in panel
- **ScrollArea** — Custom scrollbars

### Progress
- **Progress** — Linear progress
- **Meter** — Value meter

### Layout
- **Separator** — Visual divider
- **Avatar** — User avatar (Root, Image, Fallback)
- **Button** — Button primitive
- **Toggle** — Toggle button
- **ToggleGroup** — Toggle button group

---

## Compound Parts by Component

### Dialog
```
Dialog.Root → Dialog.Trigger → Dialog.Portal → Dialog.Backdrop
                                             → Dialog.Viewport → Dialog.Popup
                                                                → Dialog.Title
                                                                → Dialog.Description
                                                                → Dialog.Close
Dialog.createHandle() — detached trigger support
Dialog.Handle — handle component
```

### Popover
```
Popover.Root → Popover.Trigger → Popover.Portal → Popover.Backdrop
                                               → Popover.Positioner → Popover.Popup
                                                                     → Popover.Arrow
                                                                     → Popover.Viewport
                                                                     → Popover.Title
                                                                     → Popover.Description
                                                                     → Popover.Close
Popover.createHandle() — detached trigger support
Popover.Handle — handle component
```

### Menu
```
Menu.Root → Menu.Trigger → Menu.Portal → Menu.Backdrop
                                       → Menu.Positioner → Menu.Popup
                                                         → Menu.Arrow
                                                         → Menu.Viewport
                                                         → Menu.Item
                                                         → Menu.LinkItem
                                                         → Menu.CheckboxItem
                                                         → Menu.RadioGroup → Menu.RadioItem
                                                                            → Menu.RadioItemIndicator
                                                         → Menu.CheckboxItemIndicator
                                                         → Menu.Group → Menu.GroupLabel
                                                         → Menu.Separator
                                                         → Menu.SubmenuRoot → Menu.SubmenuTrigger
                                                                             → Menu.SubmenuPopup
Menu.createHandle() — detached trigger support
Menu.Handle — handle component
```

### ContextMenu
```
ContextMenu.Root → ContextMenu.Trigger (own)
                 → ContextMenu.Portal (re-export Menu.Portal)
                 → ContextMenu.Backdrop (re-export Menu.Backdrop)
                 → ContextMenu.Positioner (re-export Menu.Positioner)
                 → ContextMenu.Popup (re-export Menu.Popup)
                 → ContextMenu.Arrow (re-export Menu.Arrow)
                 → ContextMenu.Item (re-export Menu.Item)
                 → ContextMenu.LinkItem (re-export Menu.LinkItem)
                 → ContextMenu.CheckboxItem (re-export Menu.CheckboxItem)
                 → ContextMenu.CheckboxItemIndicator (re-export)
                 → ContextMenu.RadioGroup (re-export Menu.RadioGroup)
                 → ContextMenu.RadioItem (re-export Menu.RadioItem)
                 → ContextMenu.RadioItemIndicator (re-export)
                 → ContextMenu.Group (re-export Menu.Group)
                 → ContextMenu.GroupLabel (re-export Menu.GroupLabel)
                 → ContextMenu.SubmenuRoot (re-export)
                 → ContextMenu.SubmenuTrigger (re-export)
                 → ContextMenu.Separator (re-export Separator)
```

### Tooltip
```
Tooltip.Provider → Tooltip.Root → Tooltip.Trigger → Tooltip.Portal
                                                  → Tooltip.Positioner → Tooltip.Popup
                                                                        → Tooltip.Arrow
                                                                        → Tooltip.Viewport
Tooltip.createHandle() — detached trigger support
Tooltip.Handle — handle component
```

### PreviewCard
```
PreviewCard.Root → PreviewCard.Trigger → PreviewCard.Portal → PreviewCard.Backdrop
                                                           → PreviewCard.Positioner → PreviewCard.Popup
                                                                                     → PreviewCard.Arrow
                                                                                     → PreviewCard.Viewport
PreviewCard.createHandle() — detached trigger support
PreviewCard.Handle — handle component
```

### Select
```
Select.Root → Select.Label
            → Select.Trigger → Select.Value
                             → Select.Icon
            → Select.Portal → Select.Backdrop
                            → Select.Positioner → Select.Popup
                                                 → Select.ScrollUpArrow
                                                 → Select.Arrow
                                                 → Select.List
                                                    → Select.Item → Select.ItemText
                                                                  → Select.ItemIndicator
                                                 → Select.Separator
                                                 → Select.Group → Select.GroupLabel
                                                 → Select.ScrollDownArrow
```

### Combobox
```
Combobox.Root → Combobox.Label
              → Combobox.InputGroup → Combobox.Input
                                    → Combobox.Trigger
                                    → Combobox.Icon
                                    → Combobox.Clear
                                    → Combobox.Value
                                    → Combobox.Chips → Combobox.Chip → Combobox.ChipRemove
              → Combobox.Portal → Combobox.Backdrop
                               → Combobox.Positioner → Combobox.Popup
                                                     → Combobox.Arrow
                                                     → Combobox.Status
                                                     → Combobox.Empty
                                                     → Combobox.Collection
                                                     → Combobox.List → Combobox.Row → Combobox.Item
                                                                                     → Combobox.ItemText
                                                                                     → Combobox.ItemIndicator
                                                     → Combobox.Separator (re-export)
                                                     → Combobox.Group → Combobox.GroupLabel
Combobox.useFilter — filtering hook
Combobox.useFilteredItems — filtered items hook
```

### Autocomplete
```
Autocomplete.Root (own)
Autocomplete.Value (own)
Autocomplete.Trigger (own)
Autocomplete.InputGroup (own)
              → Autocomplete.Input (re-export Combobox.Input)
              → Autocomplete.Icon (re-export Combobox.Icon)
              → Autocomplete.Clear (re-export Combobox.Clear)
              → Autocomplete.Chips → Autocomplete.Chip → Autocomplete.ChipRemove (re-export)
                   → Autocomplete.Portal (re-export Combobox.Portal)
                   → Autocomplete.Backdrop (re-export Combobox.Backdrop)
                   → Autocomplete.Positioner (re-export Combobox.Positioner)
                   → Autocomplete.Popup (re-export Combobox.Popup)
                                         → Autocomplete.Arrow (re-export Combobox.Arrow)
                                         → Autocomplete.Status (re-export Combobox.Status)
                                         → Autocomplete.Empty (re-export Combobox.Empty)
                                         → Autocomplete.Collection (re-export Combobox.Collection)
                                         → Autocomplete.List → Autocomplete.Row → Autocomplete.Item (own)
                                                                                  → Autocomplete.ItemText (re-export)
                                                                                  → Autocomplete.ItemIndicator (re-export)
                                         → Autocomplete.Separator (re-export)
                                         → Autocomplete.Group → Autocomplete.GroupLabel (re-export)
Autocomplete.useFilter — filtering hook
Autocomplete.useFilteredItems — filtered items hook
```

### Tabs
```
Tabs.Root → Tabs.List → Tabs.Tab
                       → Tabs.Indicator
          → Tabs.Panel
```

### Accordion
```
Accordion.Root → Accordion.Item → Accordion.Header → Accordion.Trigger
                                                     → Accordion.Panel
```

### Collapsible
```
Collapsible.Root → Collapsible.Trigger
                 → Collapsible.Panel
```

### Slider
```
Slider.Root → Slider.Label
            → Slider.Value
            → Slider.Control → Slider.Track → Slider.Indicator
                                             → Slider.Thumb (multiple for range)
```

### Switch
```
Switch.Root → Switch.Thumb
```

### Checkbox
```
Checkbox.Root → Checkbox.Indicator
```

### Radio (within RadioGroup)
```
RadioGroup → Radio.Root → Radio.Indicator
```

### Field
```
Field.Root → Field.Label
           → Field.Control
           → Field.Description
           → Field.Item
           → Field.Error
           → Field.Validity
```

### Fieldset
```
Fieldset.Root → Fieldset.Legend
```

### NumberField
```
NumberField.Root → NumberField.ScrubArea → NumberField.ScrubAreaCursor
                  → NumberField.Group → NumberField.Decrement
                                      → NumberField.Input
                                      → NumberField.Increment
```

### OTPField
```
OTPField.Root → OTPField.Input (multiple)
              → OTPField.Separator
```

### Progress
```
Progress.Root → Progress.Label
              → Progress.Track → Progress.Indicator
              → Progress.Value
```

### Meter
```
Meter.Root → Meter.Label
           → Meter.Track → Meter.Indicator
           → Meter.Value
```

### ScrollArea
```
ScrollArea.Root → ScrollArea.Viewport → ScrollArea.Content
                → ScrollArea.Scrollbar → ScrollArea.Thumb
                → ScrollArea.Corner
```

### Toast
```
Toast.Provider → Toast.Portal → Toast.Viewport → Toast.Root → Toast.Content → Toast.Title
                                                                            → Toast.Description
                                                                            → Toast.Action
                                                                            → Toast.Close
                                                 → Toast.Positioner → Toast.Arrow
```

### Drawer
```
Drawer.Provider → Drawer.IndentBackground
               → Drawer.Indent → Drawer.Root → Drawer.Trigger
                                               → Drawer.SwipeArea
                                               → Drawer.Portal → Drawer.Backdrop
                                                               → Drawer.Viewport → Drawer.Popup
                                                                                  → Drawer.Content
                                                                                  → Drawer.Title
                                                                                  → Drawer.Description
                                                                                  → Drawer.Close
               → Drawer.VirtualKeyboardProvider
Drawer.createHandle() — detached trigger support (re-export Dialog.createHandle)
Drawer.Handle — handle component (re-export Dialog.Handle)
```

### NavigationMenu
```
NavigationMenu.Root → NavigationMenu.List → NavigationMenu.Item → NavigationMenu.Trigger → NavigationMenu.Icon
                                                                                         → NavigationMenu.Content → NavigationMenu.Link
                     → NavigationMenu.Portal → NavigationMenu.Backdrop
                                             → NavigationMenu.Positioner → NavigationMenu.Popup
                                                                          → NavigationMenu.Arrow
                                                                          → NavigationMenu.Viewport
```

### Menubar
```
Menubar → Menu.Root → Menu.Trigger → Menu.Portal → Menu.Backdrop
                                                    → Menu.Positioner → Menu.Popup
```

### Toolbar
```
Toolbar.Root → Toolbar.Button
             → Toolbar.Link
             → Toolbar.Separator
             → Toolbar.Group → Toolbar.Button (multiple)
             → Toolbar.Input
```

### Avatar
```
Avatar.Root → Avatar.Image
            → Avatar.Fallback
```

### Single-Part Components
- **Button** — `<Button />` (use `render` prop for custom elements, `nativeButton={false}` for non-button tags)
- **Input** — `<Input />`
- **Separator** — `<Separator />`
- **Toggle** — `<Toggle />`
- **ToggleGroup** — `<ToggleGroup />`
- **Form** — `<Form />` (wraps native `<form>`)
- **CheckboxGroup** — `<CheckboxGroup />`

### Provider Components
- **DirectionProvider** — `<DirectionProvider>` (RTL support)
- **CSPProvider** — `<CSPProvider nonce="...">` (Content Security Policy nonce)

---

## Import Examples

```tsx
import { Dialog } from '@base-ui/react/dialog';
import { Popover } from '@base-ui/react/popover';
import { Menu } from '@base-ui/react/menu';
import { ContextMenu } from '@base-ui/react/context-menu';
import { Tooltip } from '@base-ui/react/tooltip';
import { PreviewCard } from '@base-ui/react/preview-card';
import { Select } from '@base-ui/react/select';
import { Combobox } from '@base-ui/react/combobox';
import { Autocomplete } from '@base-ui/react/autocomplete';
import { Tabs } from '@base-ui/react/tabs';
import { Accordion } from '@base-ui/react/accordion';
import { Collapsible } from '@base-ui/react/collapsible';
import { Slider } from '@base-ui/react/slider';
import { Switch } from '@base-ui/react/switch';
import { Checkbox } from '@base-ui/react/checkbox';
import { Radio } from '@base-ui/react/radio';
import { RadioGroup } from '@base-ui/react/radio-group';
import { Field } from '@base-ui/react/field';
import { Fieldset } from '@base-ui/react/fieldset';
import { Form } from '@base-ui/react/form';
import { NumberField } from '@base-ui/react/number-field';
import { OtpField } from '@base-ui/react/otp-field';
import { Progress } from '@base-ui/react/progress';
import { Meter } from '@base-ui/react/meter';
import { ScrollArea } from '@base-ui/react/scroll-area';
import { Toast } from '@base-ui/react/toast';
import { Drawer } from '@base-ui/react/drawer';
import { NavigationMenu } from '@base-ui/react/navigation-menu';
import { Menubar } from '@base-ui/react/menubar';
import { Toolbar } from '@base-ui/react/toolbar';
import { AlertDialog } from '@base-ui/react/alert-dialog';
import { Avatar } from '@base-ui/react/avatar';
import { Button } from '@base-ui/react/button';
import { Input } from '@base-ui/react/input';
import { Separator } from '@base-ui/react/separator';
import { Toggle } from '@base-ui/react/toggle';
import { ToggleGroup } from '@base-ui/react/toggle-group';
import { DirectionProvider } from '@base-ui/react/direction-provider';
import { CSPProvider } from '@base-ui/react/csp-provider';
```
