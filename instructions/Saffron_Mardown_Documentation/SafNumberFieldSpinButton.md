# SafNumberFieldSpinButton

## Overview

SafNumberFieldSpinButton is a form component that provides increment and decrement controls for number input fields. It offers accessible spin button functionality with customizable step values, validation, and formatting, commonly used for quantity selectors, numeric settings, and precise value adjustments.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | `0` | Current numeric value |
| `defaultValue` | `number` | `0` | Default value (uncontrolled) |
| `min` | `number` | - | Minimum allowed value |
| `max` | `number` | - | Maximum allowed value |
| `step` | `number` | `1` | Step increment/decrement amount |
| `precision` | `number` | - | Number of decimal places |
| `disabled` | `boolean` | `false` | Disable the spin buttons |
| `readOnly` | `boolean` | `false` | Make the field read-only |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `variant` | `'default' \| 'inline' \| 'compact'` | `'default'` | Visual style variant |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Button layout orientation |
| `showButtons` | `boolean` | `true` | Show increment/decrement buttons |
| `continuousChange` | `boolean` | `false` | Fire change events continuously on hold |
| `holdDelay` | `number` | `500` | Delay before continuous change starts (ms) |
| `holdInterval` | `number` | `100` | Interval for continuous changes (ms) |
| `formatter` | `(value: number) => string` | - | Custom value formatter |
| `parser` | `(value: string) => number` | - | Custom value parser |
| `placeholder` | `string` | - | Placeholder text |
| `name` | `string` | - | Form field name |
| `required` | `boolean` | `false` | Mark field as required |
| `invalid` | `boolean` | `false` | Show invalid state |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onChange` | `(value: number) => void` | Fired when value changes |
| `onIncrement` | `(value: number) => void` | Fired when increment button is used |
| `onDecrement` | `(value: number) => void` | Fired when decrement button is used |
| `onFocus` | `(event: FocusEvent) => void` | Fired when field receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when field loses focus |
| `onKeyDown` | `(event: KeyboardEvent) => void` | Fired when key is pressed |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | `0` | Current numeric value |
| `min` | `number` | - | Minimum allowed value |
| `max` | `number` | - | Maximum allowed value |
| `step` | `number` | `1` | Step increment/decrement amount |
| `precision` | `number` | - | Number of decimal places |
| `disabled` | `boolean` | `false` | Disable the spin buttons |
| `readOnly` | `boolean` | `false` | Make the field read-only |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `variant` | `'default' \| 'inline' \| 'compact'` | `'default'` | Visual style variant |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Button layout orientation |
| `showButtons` | `boolean` | `true` | Show increment/decrement buttons |
| `continuousChange` | `boolean` | `false` | Fire change events continuously on hold |
| `holdDelay` | `number` | `500` | Delay before continuous change starts (ms) |
| `holdInterval` | `number` | `100` | Interval for continuous changes (ms) |
| `placeholder` | `string` | - | Placeholder text |
| `name` | `string` | - | Form field name |
| `required` | `boolean` | `false` | Mark field as required |
| `invalid` | `boolean` | `false` | Show invalid state |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `valueChange` | `EventEmitter<number>` | Fired when value changes |
| `increment` | `EventEmitter<number>` | Fired when increment button is used |
| `decrement` | `EventEmitter<number>` | Fired when decrement button is used |
| `fieldFocus` | `EventEmitter<FocusEvent>` | Fired when field receives focus |
| `fieldBlur` | `EventEmitter<FocusEvent>` | Fired when field loses focus |

## Usage Examples

### Basic Spin Button

```typescript
// React
const BasicSpinButton = ({ quantity, onQuantityChange }) => {
  return (
    <div className="quantity-selector">
      <SafLabel htmlFor="quantity">Quantity</SafLabel>
      <SafNumberFieldSpinButton 
        id="quantity"
        value={quantity}
        onChange={onQuantityChange}
        min={1}
        max={10}
        step={1}
        placeholder="Enter quantity"
      />
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="quantity-selector">
  <saf-label for="quantity">Quantity</saf-label>
  <saf-number-field-spin-button 
    id="quantity"
    [value]="quantity"
    [min]="1"
    [max]="10"
    [step]="1"
    placeholder="Enter quantity"
    (valueChange)="onQuantityChange($event)">
  </saf-number-field-spin-button>
</div>
```

### Decimal Precision Spin Button

```typescript
// React
const DecimalSpinButton = ({ price, onPriceChange }) => {
  const handleChange = (value) => {
    // Ensure precision and format
    const rounded = parseFloat(value.toFixed(2));
    onPriceChange(rounded);
  };

  const formatCurrency = (value) => {
    return `$${value.toFixed(2)}`;
  };

  const parseCurrency = (value) => {
    return parseFloat(value.replace(/[^0-9.]/g, '')) || 0;
  };

  return (
    <div className="price-input">
      <SafLabel htmlFor="price">Price</SafLabel>
      <SafNumberFieldSpinButton 
        id="price"
        value={price}
        onChange={handleChange}
        min={0}
        max={9999.99}
        step={0.01}
        precision={2}
        formatter={formatCurrency}
        parser={parseCurrency}
        placeholder="$0.00"
      />
    </div>
  );
};
```

### Horizontal Layout Spin Button

```typescript
// React
const HorizontalSpinButton = ({ count, onCountChange }) => {
  return (
    <div className="horizontal-counter">
      <SafLabel htmlFor="count">Count</SafLabel>
      <SafNumberFieldSpinButton 
        id="count"
        value={count}
        onChange={onCountChange}
        min={0}
        max={100}
        step={5}
        orientation="horizontal"
        variant="inline"
        size="large"
      />
    </div>
  );
};
```

### Compact Spin Button

```typescript
// React
const CompactSpinButton = ({ items }) => {
  return (
    <div className="item-list">
      {items.map((item, index) => (
        <div key={item.id} className="item-row">
          <span className="item-name">{item.name}</span>
          <SafNumberFieldSpinButton 
            value={item.quantity}
            onChange={(value) => updateItemQuantity(index, value)}
            min={0}
            max={99}
            step={1}
            variant="compact"
            size="small"
            showButtons={true}
          />
        </div>
      ))}
    </div>
  );
};
```

### Continuous Change Spin Button

```typescript
// React
const ContinuousChangeSpinButton = ({ value, onChange }) => {
  const [displayValue, setDisplayValue] = useState(value);

  const handleChange = (newValue) => {
    setDisplayValue(newValue);
    onChange(newValue);
  };

  const handleIncrement = (newValue) => {
    console.log(`Incremented to: ${newValue}`);
  };

  const handleDecrement = (newValue) => {
    console.log(`Decremented to: ${newValue}`);
  };

  return (
    <div className="continuous-spinner">
      <SafLabel htmlFor="volume">Volume Level</SafLabel>
      <SafNumberFieldSpinButton 
        id="volume"
        value={displayValue}
        onChange={handleChange}
        onIncrement={handleIncrement}
        onDecrement={handleDecrement}
        min={0}
        max={100}
        step={1}
        continuousChange={true}
        holdDelay={300}
        holdInterval={50}
        formatter={(value) => `${value}%`}
      />
    </div>
  );
};
```

### Validation with Spin Button

```typescript
// React
const ValidationSpinButton = ({ age, onAgeChange, errors }) => {
  const [localValue, setLocalValue] = useState(age);
  const [isValid, setIsValid] = useState(true);

  const validateAge = (value) => {
    if (value < 18) {
      return { valid: false, message: 'Must be 18 or older' };
    }
    if (value > 120) {
      return { valid: false, message: 'Please enter a valid age' };
    }
    return { valid: true, message: null };
  };

  const handleChange = (value) => {
    setLocalValue(value);
    const validation = validateAge(value);
    setIsValid(validation.valid);
    
    if (validation.valid) {
      onAgeChange(value);
    }
  };

  const handleBlur = () => {
    const validation = validateAge(localValue);
    if (!validation.valid) {
      // Show error message
      console.error(validation.message);
    }
  };

  return (
    <div className="age-input">
      <SafLabel htmlFor="age" required>Age</SafLabel>
      <SafNumberFieldSpinButton 
        id="age"
        value={localValue}
        onChange={handleChange}
        onBlur={handleBlur}
        min={18}
        max={120}
        step={1}
        required
        invalid={!isValid}
        placeholder="Enter your age"
      />
      {!isValid && (
        <SafFieldMessage 
          type="error"
          message={validateAge(localValue).message}
        />
      )}
    </div>
  );
};
```

### Custom Formatted Spin Button

```typescript
// React
const CustomFormattedSpinButton = ({ weight, onWeightChange, unit }) => {
  const formatWeight = (value) => {
    const units = {
      kg: (v) => `${v} kg`,
      lb: (v) => `${v} lbs`,
      oz: (v) => `${v} oz`
    };
    return units[unit]?.(value) || `${value}`;
  };

  const parseWeight = (value) => {
    const numericValue = value.replace(/[^0-9.]/g, '');
    return parseFloat(numericValue) || 0;
  };

  const getStepSize = () => {
    const steps = {
      kg: 0.1,
      lb: 0.5,
      oz: 1
    };
    return steps[unit] || 1;
  };

  const getPrecision = () => {
    const precisions = {
      kg: 1,
      lb: 1,
      oz: 0
    };
    return precisions[unit] || 0;
  };

  return (
    <div className="weight-input">
      <SafLabel htmlFor="weight">Weight</SafLabel>
      <div className="weight-field-group">
        <SafNumberFieldSpinButton 
          id="weight"
          value={weight}
          onChange={onWeightChange}
          min={0}
          max={1000}
          step={getStepSize()}
          precision={getPrecision()}
          formatter={formatWeight}
          parser={parseWeight}
          placeholder={`0 ${unit}`}
        />
        <SafSelect 
          value={unit}
          onChange={onUnitChange}
          className="unit-selector"
        >
          <SafOption value="kg">kg</SafOption>
          <SafOption value="lb">lbs</SafOption>
          <SafOption value="oz">oz</SafOption>
        </SafSelect>
      </div>
    </div>
  );
};
```

### Disabled and Read-Only States

```typescript
// React
const DisabledReadOnlySpinButtons = ({ 
  editableValue, 
  lockedValue,
  disabledValue,
  onEditableChange 
}) => {
  return (
    <div className="spin-button-states">
      <div className="field-group">
        <SafLabel htmlFor="editable">Editable</SafLabel>
        <SafNumberFieldSpinButton 
          id="editable"
          value={editableValue}
          onChange={onEditableChange}
          min={0}
          max={100}
          step={1}
        />
      </div>

      <div className="field-group">
        <SafLabel htmlFor="readonly">Read Only</SafLabel>
        <SafNumberFieldSpinButton 
          id="readonly"
          value={lockedValue}
          readOnly
          min={0}
          max={100}
          step={1}
        />
      </div>

      <div className="field-group">
        <SafLabel htmlFor="disabled">Disabled</SafLabel>
        <SafNumberFieldSpinButton 
          id="disabled"
          value={disabledValue}
          disabled
          min={0}
          max={100}
          step={1}
        />
      </div>
    </div>
  );
};
```

### Form Integration Spin Button

```typescript
// React
const FormIntegrationSpinButton = ({ formData, onFormChange, errors }) => {
  const handleFieldChange = (field, value) => {
    onFormChange({
      ...formData,
      [field]: value
    });
  };

  return (
    <form className="product-form">
      <div className="form-section">
        <h3>Product Details</h3>
        
        <div className="field-row">
          <div className="field-group">
            <SafLabel htmlFor="quantity" required>Quantity</SafLabel>
            <SafNumberFieldSpinButton 
              id="quantity"
              name="quantity"
              value={formData.quantity}
              onChange={(value) => handleFieldChange('quantity', value)}
              min={1}
              max={1000}
              step={1}
              required
              invalid={!!errors.quantity}
            />
            {errors.quantity && (
              <SafFieldMessage type="error" message={errors.quantity} />
            )}
          </div>

          <div className="field-group">
            <SafLabel htmlFor="price" required>Price</SafLabel>
            <SafNumberFieldSpinButton 
              id="price"
              name="price"
              value={formData.price}
              onChange={(value) => handleFieldChange('price', value)}
              min={0}
              step={0.01}
              precision={2}
              formatter={(value) => `$${value.toFixed(2)}`}
              required
              invalid={!!errors.price}
            />
            {errors.price && (
              <SafFieldMessage type="error" message={errors.price} />
            )}
          </div>
        </div>

        <div className="field-row">
          <div className="field-group">
            <SafLabel htmlFor="weight">Weight (kg)</SafLabel>
            <SafNumberFieldSpinButton 
              id="weight"
              name="weight"
              value={formData.weight}
              onChange={(value) => handleFieldChange('weight', value)}
              min={0}
              step={0.1}
              precision={1}
              formatter={(value) => `${value} kg`}
            />
          </div>

          <div className="field-group">
            <SafLabel htmlFor="discount">Discount %</SafLabel>
            <SafNumberFieldSpinButton 
              id="discount"
              name="discount"
              value={formData.discount}
              onChange={(value) => handleFieldChange('discount', value)}
              min={0}
              max={100}
              step={1}
              formatter={(value) => `${value}%`}
            />
          </div>
        </div>
      </div>
    </form>
  );
};
```

### Mobile-Optimized Spin Button

```typescript
// React
const MobileOptimizedSpinButton = ({ value, onChange }) => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);
  const [showKeyboard, setShowKeyboard] = useState(false);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  const handleFocus = (event) => {
    if (isMobile) {
      setShowKeyboard(true);
      // Prevent zoom on iOS
      event.target.readOnly = true;
      setTimeout(() => {
        event.target.readOnly = false;
        event.target.focus();
      }, 100);
    }
  };

  const handleBlur = () => {
    setShowKeyboard(false);
  };

  return (
    <div className={`mobile-spin-button ${isMobile ? 'mobile' : 'desktop'}`}>
      <SafLabel htmlFor="mobile-quantity">Quantity</SafLabel>
      <SafNumberFieldSpinButton 
        id="mobile-quantity"
        value={value}
        onChange={onChange}
        onFocus={handleFocus}
        onBlur={handleBlur}
        min={1}
        max={99}
        step={1}
        size={isMobile ? 'large' : 'medium'}
        orientation={isMobile ? 'horizontal' : 'vertical'}
        holdDelay={isMobile ? 200 : 500}
        holdInterval={isMobile ? 80 : 100}
        continuousChange={true}
      />
      
      {isMobile && showKeyboard && (
        <div className="mobile-actions">
          <SafButton 
            variant="ghost"
            size="small"
            onClick={() => onChange(Math.max(1, value - 1))}
          >
            -1
          </SafButton>
          <SafButton 
            variant="ghost"
            size="small"
            onClick={() => onChange(value + 1)}
          >
            +1
          </SafButton>
          <SafButton 
            variant="ghost"
            size="small"
            onClick={() => onChange(value + 10)}
          >
            +10
          </SafButton>
        </div>
      )}
    </div>
  );
};
```

### Accessibility-Enhanced Spin Button

```typescript
// React
const AccessibilityEnhancedSpinButton = ({ 
  value, 
  onChange, 
  label,
  description,
  min,
  max 
}) => {
  const [announcements, setAnnouncements] = useState('');

  const handleChange = (newValue) => {
    onChange(newValue);
    
    // Announce value changes
    let announcement = `Value changed to ${newValue}`;
    
    if (newValue === min) {
      announcement += ', minimum value reached';
    } else if (newValue === max) {
      announcement += ', maximum value reached';
    }
    
    setAnnouncements(announcement);
    
    // Clear announcement after delay
    setTimeout(() => setAnnouncements(''), 1000);
  };

  const handleIncrement = (newValue) => {
    const announcement = newValue === max ? 
      'Maximum value reached' : 
      `Increased to ${newValue}`;
    setAnnouncements(announcement);
  };

  const handleDecrement = (newValue) => {
    const announcement = newValue === min ? 
      'Minimum value reached' : 
      `Decreased to ${newValue}`;
    setAnnouncements(announcement);
  };

  return (
    <div className="accessible-spin-button">
      <SafLabel htmlFor="accessible-number" required>
        {label}
      </SafLabel>
      
      {description && (
        <SafFieldDescription id="number-description">
          {description}
        </SafFieldDescription>
      )}
      
      <SafNumberFieldSpinButton 
        id="accessible-number"
        value={value}
        onChange={handleChange}
        onIncrement={handleIncrement}
        onDecrement={handleDecrement}
        min={min}
        max={max}
        step={1}
        required
        aria-describedby="number-description"
        aria-label={`${label}, current value ${value}, minimum ${min}, maximum ${max}`}
      />
      
      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>
    </div>
  );
};
```

## Best Practices

### Usability
- **Clear Boundaries**: Set appropriate min/max values with validation
- **Reasonable Steps**: Use logical step increments for the use case
- **Visual Feedback**: Provide immediate feedback on value changes
- **Error Prevention**: Prevent invalid values through validation

### Accessibility
- **Keyboard Support**: Support arrow keys, Page Up/Down, Home/End
- **Screen Reader Support**: Provide proper labels and value announcements
- **Focus Management**: Maintain visible focus indicators
- **Value Context**: Announce current value, min/max bounds

### Performance
- **Debounced Changes**: Debounce rapid continuous changes
- **Validation Efficiency**: Optimize validation for performance
- **Memory Management**: Clean up timers and event listeners
- **Render Optimization**: Minimize unnecessary re-renders

### Mobile Experience
- **Touch Targets**: Ensure adequate button size for touch
- **Hold Behavior**: Implement appropriate hold-to-repeat functionality
- **Keyboard Handling**: Handle mobile keyboard interactions properly
- **Gesture Support**: Support swipe gestures where appropriate

## Accessibility Considerations

- Uses proper ARIA roles and attributes for spinbutton functionality
- Supports comprehensive keyboard navigation including arrow keys and Page Up/Down
- Provides screen reader announcements for value changes and boundary conditions
- Maintains proper focus management and visible focus indicators
- Includes proper labeling and descriptions for context
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML elements for proper form integration

## Related Components

- **SafNumberField**: Plain number input field without spin buttons
- **SafSlider**: Alternative for range-based numeric input
- **SafSelect**: Dropdown alternative for discrete numeric choices
- **SafFieldMessage**: Error and help message display
- **SafLabel**: Form field labeling component

## Notes

- SafNumberFieldSpinButton automatically validates against min/max bounds
- The component supports both controlled and uncontrolled usage patterns
- Custom formatters and parsers enable flexible value display
- Continuous change mode provides smooth value adjustment on hold
- The component integrates seamlessly with form libraries and validation
- Precision settings ensure accurate decimal handling
- Mobile optimizations provide touch-friendly interactions
- The component maintains proper form field semantics for accessibility
