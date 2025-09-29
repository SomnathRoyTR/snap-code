# SafCheckbox Component Documentation

## Overview

The **SafCheckbox** component is a form control that allows users to select one or more options from a set. It implements the ARIA checkbox specification and provides comprehensive accessibility features, validation support, and indeterminate state handling.

## React Implementation

### Basic Usage

```tsx
import { SafCheckbox } from '@saffron/react-components';

function BasicCheckbox() {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <SafCheckbox
      checked={isChecked}
      onChange={(event) => setIsChecked(event.target.checked)}
    >
      Accept Terms and Conditions
    </SafCheckbox>
  );
}
```

### Advanced Usage

```tsx
import { SafCheckbox } from '@saffron/react-components';
import { useState } from 'react';

function AdvancedCheckbox() {
  const [formData, setFormData] = useState({
    notifications: false,
    newsletter: true,
    marketing: false
  });
  const [errors, setErrors] = useState({});

  const handleCheckboxChange = (name: string) => (event: React.ChangeEvent<HTMLInputElement>) => {
    setFormData(prev => ({
      ...prev,
      [name]: event.target.checked
    }));
    
    // Clear error when user interacts
    if (errors[name]) {
      setErrors(prev => ({ ...prev, [name]: null }));
    }
  };

  const validateForm = () => {
    const newErrors = {};
    if (!formData.notifications && !formData.newsletter) {
      newErrors.notifications = 'Please select at least one option';
    }
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  return (
    <div className="checkbox-group">
      <h3>Communication Preferences</h3>
      
      <SafCheckbox
        id="notifications"
        checked={formData.notifications}
        onChange={handleCheckboxChange('notifications')}
        invalid={!!errors.notifications}
        validationMessage={errors.notifications}
        a11yAriaDescription="Receive important account notifications"
      >
        Email Notifications
      </SafCheckbox>

      <SafCheckbox
        id="newsletter"
        checked={formData.newsletter}
        onChange={handleCheckboxChange('newsletter')}
        a11yAriaDescription="Weekly newsletter with updates"
      >
        Newsletter
      </SafCheckbox>

      <SafCheckbox
        id="marketing"
        checked={formData.marketing}
        onChange={handleCheckboxChange('marketing')}
        disabled={!formData.notifications}
        a11yAriaDescription="Marketing emails and promotions"
      >
        Marketing Communications
      </SafCheckbox>

      <button onClick={validateForm}>
        Save Preferences
      </button>
    </div>
  );
}
```

### Indeterminate State

```tsx
import { SafCheckbox } from '@saffron/react-components';
import { useState, useEffect } from 'react';

function IndeterminateCheckbox() {
  const [items, setItems] = useState([
    { id: 1, label: 'Item 1', checked: false },
    { id: 2, label: 'Item 2', checked: true },
    { id: 3, label: 'Item 3', checked: false }
  ]);

  const checkedItems = items.filter(item => item.checked);
  const isAllChecked = checkedItems.length === items.length;
  const isIndeterminate = checkedItems.length > 0 && checkedItems.length < items.length;

  const handleSelectAll = (event: React.ChangeEvent<HTMLInputElement>) => {
    const checked = event.target.checked;
    setItems(items.map(item => ({ ...item, checked })));
  };

  const handleItemChange = (id: number) => (event: React.ChangeEvent<HTMLInputElement>) => {
    setItems(items.map(item => 
      item.id === id ? { ...item, checked: event.target.checked } : item
    ));
  };

  return (
    <div>
      <SafCheckbox
        checked={isAllChecked}
        indeterminate={isIndeterminate}
        onChange={handleSelectAll}
      >
        Select All ({checkedItems.length} of {items.length})
      </SafCheckbox>
      
      <div style={{ marginLeft: '20px' }}>
        {items.map(item => (
          <SafCheckbox
            key={item.id}
            checked={item.checked}
            onChange={handleItemChange(item.id)}
          >
            {item.label}
          </SafCheckbox>
        ))}
      </div>
    </div>
  );
}
```

### API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `checked` | `boolean` | `false` | Controls the checked state of the checkbox |
| `indeterminate` | `boolean` | `false` | Sets the checkbox to an indeterminate state |
| `disabled` | `boolean` | `false` | Disables the checkbox interaction |
| `invalid` | `boolean` | `false` | Indicates validation error state |
| `validationMessage` | `string` | `undefined` | Error message displayed when invalid |
| `value` | `string` | `"on"` | The value sent with form data when checked |
| `name` | `string` | `undefined` | Name attribute for form submission |
| `id` | `string` | `auto-generated` | Unique identifier for the checkbox |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for screen readers |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `errorAriaLabel` | `string` | `"Error"` | Label for error icon accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for checked state changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-checkbox',
  template: `
    <saf-checkbox 
      [checked]="isChecked"
      (change)="onCheckboxChange($event)">
      Accept Terms and Conditions
    </saf-checkbox>
  `
})
export class BasicCheckboxComponent {
  isChecked = false;

  onCheckboxChange(event: any) {
    this.isChecked = event.target.checked;
  }
}
```

### Advanced Usage with Forms

```typescript
// component.ts
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-advanced-checkbox',
  template: `
    <form [formGroup]="preferencesForm" (ngSubmit)="onSubmit()">
      <h3>Communication Preferences</h3>
      
      <saf-checkbox 
        formControlName="notifications"
        [invalid]="isFieldInvalid('notifications')"
        [validation-message]="getErrorMessage('notifications')"
        a11y-aria-description="Receive important account notifications">
        Email Notifications
      </saf-checkbox>

      <saf-checkbox 
        formControlName="newsletter"
        a11y-aria-description="Weekly newsletter with updates">
        Newsletter
      </saf-checkbox>

      <saf-checkbox 
        formControlName="marketing"
        [disabled]="!preferencesForm.get('notifications')?.value"
        a11y-aria-description="Marketing emails and promotions">
        Marketing Communications
      </saf-checkbox>

      <button type="submit" [disabled]="preferencesForm.invalid">
        Save Preferences
      </button>
    </form>
  `
})
export class AdvancedCheckboxComponent {
  preferencesForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.preferencesForm = this.fb.group({
      notifications: [false, [this.atLeastOneSelected]],
      newsletter: [true],
      marketing: [false]
    });
  }

  atLeastOneSelected(control: any) {
    const formGroup = control.parent;
    if (formGroup) {
      const notifications = formGroup.get('notifications')?.value;
      const newsletter = formGroup.get('newsletter')?.value;
      return (notifications || newsletter) ? null : { required: true };
    }
    return null;
  }

  isFieldInvalid(fieldName: string): boolean {
    const field = this.preferencesForm.get(fieldName);
    return !!(field && field.invalid && (field.dirty || field.touched));
  }

  getErrorMessage(fieldName: string): string {
    const field = this.preferencesForm.get(fieldName);
    if (field?.errors?.['required']) {
      return 'Please select at least one option';
    }
    return '';
  }

  onSubmit() {
    if (this.preferencesForm.valid) {
      console.log('Form submitted:', this.preferencesForm.value);
    }
  }
}
```

### API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `checked` | `boolean` | `false` | Controls the checked state |
| `indeterminate` | `boolean` | `false` | Sets indeterminate state |
| `disabled` | `boolean` | `false` | Disables the checkbox |
| `invalid` | `boolean` | `false` | Validation error state |
| `validationMessage` | `string` | `undefined` | Error message text |
| `value` | `string` | `"on"` | Form value when checked |
| `name` | `string` | `undefined` | Form field name |
| `id` | `string` | `auto-generated` | Element identifier |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |
| `errorAriaLabel` | `string` | `"Error"` | Error icon label |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when checked state changes |
| `focus` | `Event` | Emitted when checkbox receives focus |
| `blur` | `Event` | Emitted when checkbox loses focus |

## Best Practices

### Accessibility
- **Always provide labels**: Use either text content or `a11yAriaLabel` for screen readers
- **Use descriptions**: Add `a11yAriaDescription` for additional context
- **Group related checkboxes**: Use fieldsets or clear headings for checkbox groups
- **Maintain focus order**: Ensure logical tab navigation through checkbox groups

### UX Guidelines
- **Clear labeling**: Use concise, descriptive labels that clearly indicate what will happen when checked
- **Logical grouping**: Group related options together with clear headings
- **Indeterminate state**: Use for parent checkboxes that control multiple child options
- **Validation feedback**: Provide immediate, clear error messages for invalid states

### Performance
- **Avoid excessive re-renders**: Use proper state management to prevent unnecessary updates
- **Batch updates**: When updating multiple checkboxes, batch the operations
- **Event delegation**: For large lists, consider event delegation patterns

### Form Integration
- **Use proper names**: Set meaningful `name` attributes for form submission
- **Validate appropriately**: Implement client-side validation with server-side backup
- **Default values**: Set sensible defaults for better user experience

## Accessibility Notes

The SafCheckbox component includes comprehensive accessibility features:

- **ARIA compliance**: Full implementation of ARIA checkbox role and states
- **Screen reader support**: Proper labels, descriptions, and state announcements
- **Keyboard navigation**: Space key toggles, Tab for navigation
- **Focus management**: Clear focus indicators and logical focus order
- **Error handling**: Screen reader accessible error messages and validation

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+
- **Accessibility**: NVDA, JAWS, VoiceOver support

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: The `checked` prop is now controlled by default
- **v1.x to v2.x**: `onChange` event signature changed to match native input events
- **Deprecated props**: `defaultChecked` replaced with `checked` and proper state management

---

*This documentation provides comprehensive guidance for implementing SafCheckbox in both React and Angular applications with proper accessibility and user experience considerations.*
