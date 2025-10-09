# SafNumberField - Numeric Input Component

## Overview
`SafNumberField` is a specialized input component designed for numeric values. It extends the standard text field with numeric validation, step controls, and formatting features. The component supports min/max constraints, step increment/decrement, and various input modes.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `value` | `number` | `undefined` | Current numeric value |
| `min` | `number` | `undefined` | Minimum allowed value |
| `max` | `number` | `undefined` | Maximum allowed value |
| `step` | `number` | `1` | Amount to increment/decrement |
| `placeholder` | `string` | `undefined` | Placeholder text |
| `readonly` | `boolean` | `false` | Whether field is read-only |
| `disabled` | `boolean` | `false` | Whether field is disabled |
| `required` | `boolean` | `false` | Whether field is required |
| `autofocus` | `boolean` | `false` | Whether to focus on page load |
| `hide-step` | `boolean` | `false` | Hide increment/decrement buttons |
| `maxlength` | `number` | `undefined` | Maximum character length |
| `minlength` | `number` | `undefined` | Minimum character length |
| `size` | `number` | `undefined` | Visual width in characters |
| `list` | `string` | `undefined` | Associated datalist ID |
| `appearance` | `'filled' \| 'outline'` | `'outline'` | Visual style variant |
| `density` | `'compact' \| 'standard'` | `'standard'` | Size density |

### Properties
| Property | Type | Description |
|----------|------|-------------|
| `valueAsNumber` | `number` | Numeric value of the input |
| `validity` | `ValidityState` | Validation state |
| `validationMessage` | `string` | Current validation message |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `change` | `CustomEvent<number>` | Fired when value changes |
| `input` | `CustomEvent<number>` | Fired during input |
| `focus` | `FocusEvent` | Fired when field gains focus |
| `blur` | `FocusEvent` | Fired when field loses focus |

### Methods
| Method | Description |
|--------|-------------|
| `focus()` | Focus the input element |
| `blur()` | Remove focus from input |
| `select()` | Select all text in input |
| `stepUp(n?)` | Increment value by step * n |
| `stepDown(n?)` | Decrement value by step * n |
| `setCustomValidity(message)` | Set custom validation message |
| `checkValidity()` | Check if input is valid |

## Usage Examples

### Basic Number Field
```typescript
// React
import { SafNumberField } from '@saffron/react';

export const BasicNumberField = () => {
  const [quantity, setQuantity] = useState(1);
  
  return (
    <SafNumberField
      label="Quantity"
      value={quantity}
      onChange={(e) => setQuantity(e.target.value)}
      min={1}
      max={999}
      step={1}
      placeholder="Enter quantity"
      required
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-number-field
      label="Quantity"
      [value]="quantity"
      (change)="onQuantityChange($event)"
      min="1"
      max="999"
      step="1"
      placeholder="Enter quantity"
      required>
    </saf-number-field>
  `
})
export class BasicNumberFieldComponent {
  quantity = 1;
  
  onQuantityChange(event: CustomEvent<number>) {
    this.quantity = event.detail;
  }
}
```

### Price Input with Decimal Places
```typescript
// React
export const PriceField = () => {
  const [price, setPrice] = useState(0);
  
  return (
    <SafNumberField
      label="Price"
      value={price}
      onChange={(e) => setPrice(e.target.value)}
      min={0}
      max={99999.99}
      step={0.01}
      placeholder="0.00"
      appearance="filled"
    >
      <span slot="start">$</span>
    </SafNumberField>
  );
};
```

### Form with Validation
```typescript
// React
export const NumberForm = () => {
  const [formData, setFormData] = useState({
    quantity: 1,
    price: 0,
    discount: 0
  });
  
  const [errors, setErrors] = useState({});
  
  const validateField = (name: string, value: number) => {
    const newErrors = { ...errors };
    
    switch (name) {
      case 'quantity':
        if (value < 1) {
          newErrors.quantity = 'Quantity must be at least 1';
        } else {
          delete newErrors.quantity;
        }
        break;
      case 'price':
        if (value <= 0) {
          newErrors.price = 'Price must be greater than 0';
        } else {
          delete newErrors.price;
        }
        break;
      case 'discount':
        if (value < 0 || value > 100) {
          newErrors.discount = 'Discount must be between 0 and 100';
        } else {
          delete newErrors.discount;
        }
        break;
    }
    
    setErrors(newErrors);
  };
  
  const handleChange = (name: string) => (e: any) => {
    const value = parseFloat(e.target.value) || 0;
    setFormData({ ...formData, [name]: value });
    validateField(name, value);
  };
  
  return (
    <form>
      <SafNumberField
        label="Quantity"
        value={formData.quantity}
        onChange={handleChange('quantity')}
        min={1}
        max={999}
        step={1}
        required
        error={errors.quantity}
      />
      
      <SafNumberField
        label="Unit Price"
        value={formData.price}
        onChange={handleChange('price')}
        min={0.01}
        step={0.01}
        required
        error={errors.price}
      >
        <span slot="start">$</span>
      </SafNumberField>
      
      <SafNumberField
        label="Discount"
        value={formData.discount}
        onChange={handleChange('discount')}
        min={0}
        max={100}
        step={0.1}
        error={errors.discount}
      >
        <span slot="end">%</span>
      </SafNumberField>
      
      <div style={{ marginTop: '16px' }}>
        <strong>Total: ${((formData.quantity * formData.price) * (1 - formData.discount / 100)).toFixed(2)}</strong>
      </div>
      
      <SafButton 
        type="submit" 
        appearance="primary"
        disabled={Object.keys(errors).length > 0}
      >
        Submit Order
      </SafButton>
    </form>
  );
};
```

### Range Input with Custom Steps
```typescript
// React
export const RangeInputs = () => {
  const [settings, setSettings] = useState({
    temperature: 22,
    humidity: 50,
    brightness: 75
  });
  
  return (
    <div>
      <h3>Environmental Controls</h3>
      
      <SafNumberField
        label="Temperature (°C)"
        value={settings.temperature}
        onChange={(e) => setSettings({...settings, temperature: e.target.value})}
        min={16}
        max={30}
        step={0.5}
        density="compact"
      />
      
      <SafNumberField
        label="Humidity (%)"
        value={settings.humidity}
        onChange={(e) => setSettings({...settings, humidity: e.target.value})}
        min={30}
        max={70}
        step={5}
        density="compact"
      />
      
      <SafNumberField
        label="Brightness (%)"
        value={settings.brightness}
        onChange={(e) => setSettings({...settings, brightness: e.target.value})}
        min={0}
        max={100}
        step={5}
        density="compact"
      />
    </div>
  );
};
```

### Read-only and Disabled States
```typescript
// React
export const NumberFieldStates = () => {
  return (
    <div>
      <SafNumberField
        label="Calculated Total"
        value={1250.75}
        readonly
        appearance="filled"
      >
        <span slot="start">$</span>
      </SafNumberField>
      
      <SafNumberField
        label="Disabled Field"
        value={100}
        disabled
        placeholder="Not available"
      />
      
      <SafNumberField
        label="Hidden Step Controls"
        value={42}
        hide-step
        min={0}
        max={100}
      />
    </div>
  );
};
```

### Number Field with Datalist
```typescript
// React
export const NumberFieldWithSuggestions = () => {
  return (
    <>
      <SafNumberField
        label="Common Quantities"
        list="quantities"
        placeholder="Choose or enter quantity"
      />
      
      <datalist id="quantities">
        <option value="1">1 piece</option>
        <option value="5">5 pieces</option>
        <option value="10">10 pieces</option>
        <option value="25">25 pieces</option>
        <option value="50">50 pieces</option>
        <option value="100">100 pieces</option>
      </datalist>
    </>
  );
};
```

### Advanced Calculation Field
```typescript
// React
export const CalculationField = () => {
  const [values, setValues] = useState({
    principal: 10000,
    rate: 5.5,
    years: 30
  });
  
  const monthlyPayment = useMemo(() => {
    const { principal, rate, years } = values;
    const monthlyRate = rate / 100 / 12;
    const numPayments = years * 12;
    
    if (rate === 0) return principal / numPayments;
    
    return principal * (monthlyRate * Math.pow(1 + monthlyRate, numPayments)) / 
           (Math.pow(1 + monthlyRate, numPayments) - 1);
  }, [values]);
  
  const handleValueChange = (field: string) => (e: any) => {
    setValues({ ...values, [field]: parseFloat(e.target.value) || 0 });
  };
  
  return (
    <saf-card>
      <h3>Mortgage Calculator</h3>
      
      <SafNumberField
        label="Principal Amount"
        value={values.principal}
        onChange={handleValueChange('principal')}
        min={1000}
        max={10000000}
        step={1000}
        appearance="filled"
      >
        <span slot="start">$</span>
      </SafNumberField>
      
      <SafNumberField
        label="Interest Rate"
        value={values.rate}
        onChange={handleValueChange('rate')}
        min={0}
        max={20}
        step={0.1}
        appearance="filled"
      >
        <span slot="end">%</span>
      </SafNumberField>
      
      <SafNumberField
        label="Loan Term"
        value={values.years}
        onChange={handleValueChange('years')}
        min={1}
        max={50}
        step={1}
        appearance="filled"
      >
        <span slot="end">years</span>
      </SafNumberField>
      
      <SafNumberField
        label="Monthly Payment"
        value={monthlyPayment}
        readonly
        appearance="filled"
      >
        <span slot="start">$</span>
      </SafNumberField>
    </saf-card>
  );
};
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support including arrow keys for stepping
- **Screen Reader Support**: Proper labeling and state announcements
- **Validation Messages**: Clear error messaging for invalid inputs
- **Focus Management**: Appropriate focus indicators and behavior
- **High Contrast**: Full high contrast mode support
- **ARIA Attributes**: Proper ARIA labeling for assistive technologies

## Best Practices

1. **Appropriate Constraints**: Set realistic min/max values for your use case
2. **Meaningful Steps**: Choose step values that make sense for user input
3. **Clear Labels**: Provide descriptive labels and help text
4. **Input Validation**: Implement proper client and server-side validation
5. **Error Handling**: Show clear, actionable error messages
6. **Performance**: Use controlled components appropriately to avoid unnecessary re-renders
7. **Accessibility**: Always provide labels and consider screen reader users

## Advanced Usage

### Custom Formatting
```typescript
// React with custom number formatting
export const FormattedNumberField = () => {
  const [value, setValue] = useState(1234.56);
  
  const formatNumber = (num: number) => {
    return new Intl.NumberFormat('en-US', {
      minimumFractionDigits: 2,
      maximumFractionDigits: 2
    }).format(num);
  };
  
  return (
    <SafNumberField
      label="Formatted Number"
      value={value}
      onChange={(e) => setValue(parseFloat(e.target.value))}
      onBlur={(e) => {
        // Format display value on blur
        e.target.value = formatNumber(value);
      }}
    />
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  quantity: number;
  price: number;
}

export const HookFormExample = () => {
  const { control, handleSubmit, formState: { errors } } = useForm<FormData>({
    defaultValues: {
      quantity: 1,
      price: 0
    }
  });
  
  const onSubmit = (data: FormData) => {
    console.log('Form data:', data);
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="quantity"
        control={control}
        rules={{ 
          required: 'Quantity is required',
          min: { value: 1, message: 'Minimum quantity is 1' }
        }}
        render={({ field, fieldState }) => (
          <SafNumberField
            {...field}
            label="Quantity"
            min={1}
            step={1}
            error={fieldState.error?.message}
          />
        )}
      />
      
      <Controller
        name="price"
        control={control}
        rules={{ 
          required: 'Price is required',
          min: { value: 0.01, message: 'Price must be greater than 0' }
        }}
        render={({ field, fieldState }) => (
          <SafNumberField
            {...field}
            label="Price"
            min={0.01}
            step={0.01}
            error={fieldState.error?.message}
          >
            <span slot="start">$</span>
          </SafNumberField>
        )}
      />
      
      <SafButton type="submit" appearance="primary">
        Submit
      </SafButton>
    </form>
  );
};
```

## Notes

- Automatically handles numeric validation and constraints
- Supports both integer and decimal number inputs
- Includes built-in increment/decrement buttons (can be hidden)
- Provides precise number handling to avoid floating-point errors
- Integrates with native form validation
- Supports all standard HTML input attributes where applicable
