# SafRadio & SafRadioGroup Component Documentation

## Overview

The **SafRadio** and **SafRadioGroup** components work together to provide mutually exclusive selection options. SafRadioGroup manages a collection of SafRadio components, ensuring only one radio button can be selected at a time. Both components implement ARIA radiogroup and radio specifications with comprehensive accessibility features.

## React Implementation

### Basic Usage

```tsx
import { SafRadioGroup, SafRadio } from '@saffron/react-components';
import { useState } from 'react';

function BasicRadioGroup() {
  const [selectedValue, setSelectedValue] = useState('option1');

  return (
    <SafRadioGroup
      value={selectedValue}
      onChange={(event) => setSelectedValue(event.target.value)}
    >
      <label slot="label">Choose an option:</label>
      <SafRadio value="option1">Option 1</SafRadio>
      <SafRadio value="option2">Option 2</SafRadio>
      <SafRadio value="option3">Option 3</SafRadio>
    </SafRadioGroup>
  );
}
```

### Advanced Usage with Validation

```tsx
import { SafRadioGroup, SafRadio } from '@saffron/react-components';
import { useState } from 'react';

function AdvancedRadioGroup() {
  const [formData, setFormData] = useState({
    priority: '',
    category: '',
    urgency: 'medium'
  });
  const [errors, setErrors] = useState({});

  const handleRadioChange = (field: string) => (event: React.ChangeEvent<HTMLInputElement>) => {
    setFormData(prev => ({
      ...prev,
      [field]: event.target.value
    }));
    
    // Clear error when user selects an option
    if (errors[field]) {
      setErrors(prev => ({ ...prev, [field]: null }));
    }
  };

  const validateForm = () => {
    const newErrors = {};
    if (!formData.priority) {
      newErrors.priority = 'Priority is required';
    }
    if (!formData.category) {
      newErrors.category = 'Category is required';
    }
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  return (
    <form className="ticket-form">
      <h3>Create Support Ticket</h3>

      <SafRadioGroup
        name="priority"
        value={formData.priority}
        onChange={handleRadioChange('priority')}
        orientation="horizontal"
        invalid={!!errors.priority}
        validationMessage={errors.priority}
        a11yAriaDescription="Select the priority level for your support request"
      >
        <label slot="label">Priority Level *</label>
        <SafRadio value="low">Low</SafRadio>
        <SafRadio value="medium">Medium</SafRadio>
        <SafRadio value="high">High</SafRadio>
        <SafRadio value="critical">Critical</SafRadio>
      </SafRadioGroup>

      <SafRadioGroup
        name="category"
        value={formData.category}
        onChange={handleRadioChange('category')}
        invalid={!!errors.category}
        validationMessage={errors.category}
      >
        <label slot="label">Issue Category *</label>
        <SafRadio value="technical">Technical Issue</SafRadio>
        <SafRadio value="billing">Billing Question</SafRadio>
        <SafRadio value="feature">Feature Request</SafRadio>
        <SafRadio value="other">Other</SafRadio>
      </SafRadioGroup>

      <SafRadioGroup
        name="urgency"
        value={formData.urgency}
        onChange={handleRadioChange('urgency')}
        disabled={!formData.priority || !formData.category}
      >
        <label slot="label">Response Time</label>
        <SafRadio value="immediate">Immediate (1 hour)</SafRadio>
        <SafRadio value="urgent">Urgent (4 hours)</SafRadio>
        <SafRadio value="medium">Medium (24 hours)</SafRadio>
        <SafRadio value="low">Low (72 hours)</SafRadio>
      </SafRadioGroup>

      <button type="button" onClick={validateForm}>
        Create Ticket
      </button>
    </form>
  );
}
```

### Conditional Options

```tsx
import { SafRadioGroup, SafRadio } from '@saffron/react-components';
import { useState } from 'react';

function ConditionalRadioGroup() {
  const [paymentMethod, setPaymentMethod] = useState('');
  const [cardType, setCardType] = useState('');

  const paymentOptions = [
    { value: 'card', label: 'Credit/Debit Card', icon: '💳' },
    { value: 'paypal', label: 'PayPal', icon: '🅿️' },
    { value: 'bank', label: 'Bank Transfer', icon: '🏦' },
    { value: 'crypto', label: 'Cryptocurrency', icon: '₿' }
  ];

  const cardTypes = [
    { value: 'visa', label: 'Visa' },
    { value: 'mastercard', label: 'Mastercard' },
    { value: 'amex', label: 'American Express' },
    { value: 'discover', label: 'Discover' }
  ];

  return (
    <div className="payment-form">
      <SafRadioGroup
        name="payment-method"
        value={paymentMethod}
        onChange={(e) => {
          setPaymentMethod(e.target.value);
          if (e.target.value !== 'card') {
            setCardType('');
          }
        }}
        orientation="vertical"
      >
        <label slot="label">Select Payment Method</label>
        {paymentOptions.map(option => (
          <SafRadio key={option.value} value={option.value}>
            <span className="radio-option">
              <span className="radio-icon">{option.icon}</span>
              <span className="radio-text">{option.label}</span>
            </span>
          </SafRadio>
        ))}
      </SafRadioGroup>

      {paymentMethod === 'card' && (
        <SafRadioGroup
          name="card-type"
          value={cardType}
          onChange={(e) => setCardType(e.target.value)}
          orientation="horizontal"
          style={{ marginTop: '20px' }}
        >
          <label slot="label">Card Type</label>
          {cardTypes.map(type => (
            <SafRadio key={type.value} value={type.value}>
              {type.label}
            </SafRadio>
          ))}
        </SafRadioGroup>
      )}

      {paymentMethod && (
        <div className="summary">
          <p>Selected: {paymentMethod} {cardType && `(${cardType})`}</p>
        </div>
      )}
    </div>
  );
}
```

### SafRadioGroup API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `undefined` | The value of the selected radio button |
| `name` | `string` | `undefined` | Name attribute for the radio group |
| `disabled` | `boolean` | `false` | Disables all radio buttons in the group |
| `readOnly` | `boolean` | `false` | Makes the radio group read-only |
| `invalid` | `boolean` | `false` | Indicates validation error state |
| `validationMessage` | `string` | `undefined` | Error message displayed when invalid |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Layout direction for radio buttons |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for the radio group |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for value changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |

### SafRadio API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `"on"` | The value sent when this radio is selected |
| `checked` | `boolean` | `false` | Whether this radio is selected (managed by group) |
| `disabled` | `boolean` | `false` | Disables this specific radio button |
| `invalid` | `boolean` | `false` | Indicates validation error state |
| `validationMessage` | `string` | `undefined` | Error message for this radio |
| `name` | `string` | `undefined` | Name attribute (inherited from group) |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for screen readers |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for selection changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-radio',
  template: `
    <saf-radio-group 
      [value]="selectedOption"
      (change)="onSelectionChange($event)">
      <label slot="label">Choose an option:</label>
      <saf-radio value="option1">Option 1</saf-radio>
      <saf-radio value="option2">Option 2</saf-radio>
      <saf-radio value="option3">Option 3</saf-radio>
    </saf-radio-group>
  `
})
export class BasicRadioComponent {
  selectedOption = 'option1';

  onSelectionChange(event: any) {
    this.selectedOption = event.target.value;
  }
}
```

### Advanced Usage with Forms

```typescript
// component.ts
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-advanced-radio',
  template: `
    <form [formGroup]="ticketForm" (ngSubmit)="onSubmit()">
      <h3>Create Support Ticket</h3>

      <saf-radio-group 
        formControlName="priority"
        orientation="horizontal"
        [invalid]="isFieldInvalid('priority')"
        [validation-message]="getErrorMessage('priority')"
        a11y-aria-description="Select the priority level for your support request">
        <label slot="label">Priority Level *</label>
        <saf-radio value="low">Low</saf-radio>
        <saf-radio value="medium">Medium</saf-radio>
        <saf-radio value="high">High</saf-radio>
        <saf-radio value="critical">Critical</saf-radio>
      </saf-radio-group>

      <saf-radio-group 
        formControlName="category"
        [invalid]="isFieldInvalid('category')"
        [validation-message]="getErrorMessage('category')">
        <label slot="label">Issue Category *</label>
        <saf-radio value="technical">Technical Issue</saf-radio>
        <saf-radio value="billing">Billing Question</saf-radio>
        <saf-radio value="feature">Feature Request</saf-radio>
        <saf-radio value="other">Other</saf-radio>
      </saf-radio-group>

      <button type="submit" [disabled]="ticketForm.invalid">
        Create Ticket
      </button>
    </form>
  `
})
export class AdvancedRadioComponent {
  ticketForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.ticketForm = this.fb.group({
      priority: ['', [Validators.required]],
      category: ['', [Validators.required]],
      urgency: ['medium']
    });
  }

  isFieldInvalid(fieldName: string): boolean {
    const field = this.ticketForm.get(fieldName);
    return !!(field && field.invalid && (field.dirty || field.touched));
  }

  getErrorMessage(fieldName: string): string {
    const field = this.ticketForm.get(fieldName);
    if (field?.errors?.['required']) {
      return `${fieldName.charAt(0).toUpperCase() + fieldName.slice(1)} is required`;
    }
    return '';
  }

  onSubmit() {
    if (this.ticketForm.valid) {
      console.log('Form submitted:', this.ticketForm.value);
    } else {
      this.markFormGroupTouched();
    }
  }

  private markFormGroupTouched() {
    Object.keys(this.ticketForm.controls).forEach(key => {
      this.ticketForm.get(key)?.markAsTouched();
    });
  }
}
```

### SafRadioGroup API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `value` | `string` | `undefined` | Selected radio button value |
| `name` | `string` | `undefined` | Form field name |
| `disabled` | `boolean` | `false` | Disables entire group |
| `readOnly` | `boolean` | `false` | Makes group read-only |
| `invalid` | `boolean` | `false` | Validation error state |
| `validationMessage` | `string` | `undefined` | Error message text |
| `orientation` | `string` | `'vertical'` | Layout direction |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when selection changes |
| `focus` | `Event` | Emitted when group receives focus |
| `blur` | `Event` | Emitted when group loses focus |

### SafRadio API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `value` | `string` | `"on"` | Radio button value |
| `checked` | `boolean` | `false` | Selected state |
| `disabled` | `boolean` | `false` | Disabled state |
| `invalid` | `boolean` | `false` | Error state |
| `validationMessage` | `string` | `undefined` | Error message |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when selection changes |
| `focus` | `Event` | Emitted when radio receives focus |
| `blur` | `Event` | Emitted when radio loses focus |

## Best Practices

### Accessibility
- **Use descriptive labels**: Provide clear, concise labels for each radio option
- **Group labeling**: Always use the label slot for radio group titles
- **Logical ordering**: Order options in a logical sequence (alphabetical, by priority, etc.)
- **Keyboard navigation**: Arrow keys navigate between options, Tab moves to next form element

### UX Guidelines
- **Mutual exclusion**: Radio buttons should represent mutually exclusive choices
- **Default selection**: Consider providing a sensible default selection
- **Option limits**: Keep radio groups to 7 or fewer options for better usability
- **Vertical layout**: Use vertical orientation for better readability in most cases

### Form Design
- **Required fields**: Clearly mark required radio groups with asterisks or other indicators
- **Validation timing**: Validate on blur or form submission, not on each selection
- **Error placement**: Show validation messages near the radio group
- **Progressive disclosure**: Use conditional options to reduce cognitive load

### Performance
- **Minimize re-renders**: Use proper state management to avoid unnecessary updates
- **Large lists**: For many options, consider using SafSelect instead
- **Event handling**: Use single event handlers at the group level when possible

## Accessibility Notes

The SafRadio and SafRadioGroup components provide comprehensive accessibility:

- **ARIA compliance**: Full implementation of ARIA radiogroup and radio roles
- **Screen reader support**: Proper announcements for selection changes and states
- **Keyboard navigation**: Arrow keys for option selection, Tab for focus movement
- **Focus management**: Clear focus indicators and logical focus order
- **Error handling**: Screen reader accessible error messages and validation states

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+
- **Accessibility**: NVDA, JAWS, VoiceOver support

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: The `value` prop is now controlled by default
- **v1.x to v2.x**: `onChange` event signature changed to match native input events
- **Deprecated props**: `defaultValue` replaced with `value` and proper state management

---

*This documentation provides comprehensive guidance for implementing SafRadio and SafRadioGroup components in both React and Angular applications with proper accessibility and user experience considerations.*
