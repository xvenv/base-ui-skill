# Base UI Forms — Advanced Guide

## React Hook Form Integration

```tsx
import { useForm, Controller } from 'react-hook-form';
import { Field } from '@base-ui/react/field';
import { Form } from '@base-ui/react/form';

const { control, handleSubmit } = useForm({
  defaultValues: { username: '', email: '' },
});

<Form onSubmit={handleSubmit(submitForm)}>
  <Controller
    name="username"
    control={control}
    rules={{ required: 'Required', minLength: { value: 3, message: 'Too short' } }}
    render={({
      field: { name, ref, value, onBlur, onChange },
      fieldState: { invalid, isTouched, isDirty, error },
    }) => (
      <Field.Root name={name} invalid={invalid} touched={isTouched} dirty={isDirty}>
        <Field.Label>Username</Field.Label>
        <Field.Control ref={ref} value={value} onBlur={onBlur} onValueChange={onChange} />
        <Field.Error match={!!error}>{error?.message}</Field.Error>
      </Field.Root>
    )}
  />
</Form>
```

## TanStack Form Integration

```tsx
import { useForm } from '@tanstack/react-form';
import { Field } from '@base-ui/react/field';

const form = useForm({
  defaultValues: { username: '' },
  onSubmit: async ({ value }) => { /* submit */ },
});

<form.Field
  name="username"
  children={(field) => (
    <Field.Root
      name={field.name}
      invalid={!field.state.meta.isValid}
      dirty={field.state.meta.isDirty}
      touched={field.state.meta.isTouched}
    >
      <Field.Label>Username</Field.Label>
      <Field.Control
        value={field.state.value}
        onValueChange={field.handleChange}
        onBlur={field.handleBlur}
      />
      <Field.Error match={!field.state.meta.isValid}>
        {field.state.meta.errors.join(',')}
      </Field.Error>
    </Field.Root>
  )}
/>
```

## Constraint Validation

Native HTML validation attributes:

```tsx
<Field.Root name="website">
  <Field.Control type="url" required pattern="https?://.*" minLength={10} maxLength={100} />
  <Field.Error />
</Field.Root>
```

Supported attributes: `required`, `minLength`, `maxLength`, `pattern`, `step`

## Custom Validation

```tsx
<Field.Root
  name="username"
  validationMode="onChange"        // onSubmit | onBlur | onChange
  validationDebounceTime={300}     // Debounce async validation
  validate={async (value) => {
    if (value === 'admin') return 'Reserved';
    const available = await checkAvailability(value);
    return available ? null : 'Unavailable';
  }}
>
  <Field.Control />
  <Field.Error />
</Field.Root>
```

## Server-Side Validation

```tsx
const [errors, setErrors] = React.useState();

<Form
  errors={errors}
  onSubmit={async (event) => {
    event.preventDefault();
    const response = await submitToServer(data);
    setErrors(response.errors);  // { fieldName: 'Error message' }
  }}
>
  <Field.Root name="promoCode">
    <Field.Control />
    <Field.Error />
  </Field.Root>
</Form>
```

## Server Functions with useActionState

```tsx
const [state, formAction] = React.useActionState(login, {});

<Form action={formAction} errors={state.errors}>
  <Field.Root name="password">
    <Field.Control />
    <Field.Error />
  </Field.Root>
</Form>
```

## onFormSubmit (Object Values)

```tsx
<Form
  onFormSubmit={async (formValues, eventDetails) => {
    // formValues is a JS object: { id: '123', quantity: 5 }
    await fetch('/api', { body: JSON.stringify(formValues) });
  }}
>
```

## Field.Item (Grouped Controls)

For checkbox/radio groups with individual labels:

```tsx
<Field.Root>
  <Fieldset.Root render={<CheckboxGroup />}>
    <Fieldset.Legend>Options</Fieldset.Legend>
    <Field.Item>
      <Checkbox.Root value="a" />
      <Field.Label>Option A</Field.Label>
      <Field.Description>Description for A</Field.Description>
    </Field.Item>
    <Field.Item>
      <Checkbox.Root value="b" />
      <Field.Label>Option B</Field.Label>
    </Field.Item>
  </Fieldset.Root>
</Field.Root>
```

## Field.Error match prop

Customize error messages by validity state:

```tsx
<Field.Error match="valueMissing">This field is required</Field.Error>
<Field.Error match="typeMismatch">Please enter a valid email</Field.Error>
```

## Labeling Rules

| Component | Label Strategy |
|-----------|---------------|
| Input, NumberField, OTPField | `<Field.Label>` or native `<label>` |
| Checkbox, Radio, Switch | `<Field.Label>` wrapping the control |
| Select | `<Select.Label>` |
| Combobox (input in popup) | `<Combobox.Label>` |
| Slider | `<Slider.Label>` + `aria-label` on each Thumb |
| Fallback | `aria-label` on the control |
