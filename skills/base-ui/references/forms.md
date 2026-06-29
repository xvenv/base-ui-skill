# Base UI Forms Guide

## Form Component

`Form` wraps native `<form>` with validation:

```tsx
import { Form } from '@base-ui/react/form';

<Form onSubmit={(event) => {
  event.preventDefault();
  const formData = new FormData(event.currentTarget);
  // process formData
}}>
  <Field.Root name="email">
    <Field.Label>Email</Field.Label>
    <Field.Control render={<input />} />
    <Field.Error />
  </Field.Root>
  <button type="submit">Submit</button>
</Form>
```

## Field Component

`Field` connects form controls with labels and error messages:

```tsx
<Field.Root name="password" validate={validatePassword}>
  <Field.Label>Password</Field.Label>
  <Field.Control render={<input type="password" />} />
  <Field.Error />
</Field.Root>
```

## Validation

### On blur (default)

```tsx
<Field.Root name="email" validate={validateEmail}>
```

### On change

```tsx
<Field.Root name="email" validate={validateEmail} validateOnChange>
```

### On submit

```tsx
<Field.Root name="email" validate={validateEmail} validateOnSubmit>
```

### Custom validate function

```tsx
function validateEmail(value: string) {
  if (!value.includes('@')) return 'Invalid email';
  return null; // no error
}
```

## Select Labeling

Always provide accessible names:

```tsx
<Select.Root>
  <Select.Label>Theme</Select.Label>
  <Select.Trigger />
  ...
</Select.Root>

// Or aria-label
<Select.Trigger aria-label="Theme" />
```

## Fieldset

Group related fields:

```tsx
<Fieldset.Root>
  <Fieldset.Legend>Personal Info</Fieldset.Legend>
  <Field.Root name="name">
    <Field.Label>Name</Field.Label>
    <Field.Control render={<input />} />
  </Field.Root>
  <Field.Root name="email">
    <Field.Label>Email</Field.Label>
    <Field.Control render={<input />} />
  </Field.Root>
</Fieldset.Root>
```

## NumberField

For numeric inputs with increment/decrement:

```tsx
import { NumberField } from '@base-ui/react/number-field';

<NumberField.Root defaultValue={0} min={0} max={100}>
  <NumberField.Label>Quantity</NumberField.Label>
  <NumberField.Decrement>-</NumberField.Decrement>
  <NumberField.Input />
  <NumberField.Increment>+</NumberField.Increment>
</NumberField.Root>
```

## OTP Field

For one-time password inputs:

```tsx
import { OtpField } from '@base-ui/react/otp-field';

<OtpField.Root length={6}>
  <OtpField.Slot index={0} />
  <OtpField.Slot index={1} />
  <OtpField.Slot index={2} />
  <OtpField.Slot index={3} />
  <OtpField.Slot index={4} />
  <OtpField.Slot index={5} />
</OtpField.Root>
```
