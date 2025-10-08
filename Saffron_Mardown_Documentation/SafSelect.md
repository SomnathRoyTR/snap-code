# SafSelect Component Documentation

## Overview

The **SafSelect** component is a dropdown form control that allows users to choose one option from a list. It implements the ARIA select specification with comprehensive accessibility features, floating UI positioning, validation support, and customizable label positioning.

## React Implementation

### Basic Usage

```tsx
import { SafSelect, SafOption } from '@saffron/react-components';
import { useState } from 'react';

function BasicSelect() {
  const [selectedValue, setSelectedValue] = useState('');

  return (
    <SafSelect
      value={selectedValue}
      onChange={(event) => setSelectedValue(event.target.value)}
      placeholder="Choose an option..."
    >
      <SafOption value="option1">Option 1</SafOption>
      <SafOption value="option2">Option 2</SafOption>
      <SafOption value="option3">Option 3</SafOption>
    </SafSelect>
  );
}
```

### Advanced Usage with Validation

```tsx
import { SafSelect, SafOption } from '@saffron/react-components';
import { useState } from 'react';

function AdvancedSelect() {
  const [formData, setFormData] = useState({
    country: '',
    state: '',
    city: '',
    priority: 'medium'
  });
  const [errors, setErrors] = useState({});

  const countries = [
    { value: 'us', label: 'United States' },
    { value: 'ca', label: 'Canada' },
    { value: 'uk', label: 'United Kingdom' },
    { value: 'de', label: 'Germany' },
    { value: 'fr', label: 'France' }
  ];

  const states = {
    us: [
      { value: 'ny', label: 'New York' },
      { value: 'ca', label: 'California' },
      { value: 'tx', label: 'Texas' },
      { value: 'fl', label: 'Florida' }
    ],
    ca: [
      { value: 'on', label: 'Ontario' },
      { value: 'bc', label: 'British Columbia' },
      { value: 'ab', label: 'Alberta' },
      { value: 'qc', label: 'Quebec' }
    ]
  };

  const priorities = [
    { value: 'low', label: 'Low Priority', description: '72+ hours response' },
    { value: 'medium', label: 'Medium Priority', description: '24-48 hours response' },
    { value: 'high', label: 'High Priority', description: '4-8 hours response' },
    { value: 'critical', label: 'Critical', description: 'Immediate response' }
  ];

  const handleSelectChange = (field: string) => (event: React.ChangeEvent<HTMLSelectElement>) => {
    const value = event.target.value;
    setFormData(prev => ({
      ...prev,
      [field]: value,
      // Reset dependent fields
      ...(field === 'country' && { state: '', city: '' }),
      ...(field === 'state' && { city: '' })
    }));
    
    // Clear errors when user makes a selection
    if (errors[field]) {
      setErrors(prev => ({ ...prev, [field]: null }));
    }
  };

  const validateForm = () => {
    const newErrors = {};
    if (!formData.country) newErrors.country = 'Country is required';
    if (!formData.state && states[formData.country]) {
      newErrors.state = 'State/Province is required';
    }
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  return (
    <form className="location-form">
      <h3>Location & Priority Settings</h3>

      <SafSelect
        name="country"
        value={formData.country}
        onChange={handleSelectChange('country')}
        invalid={!!errors.country}
        validationMessage={errors.country}
        placeholder="Select your country"
        density="comfortable"
        a11yAriaLabel="Country selection"
      >
        {countries.map(country => (
          <SafOption key={country.value} value={country.value}>
            {country.label}
          </SafOption>
        ))}
      </SafSelect>

      <SafSelect
        name="state"
        value={formData.state}
        onChange={handleSelectChange('state')}
        invalid={!!errors.state}
        validationMessage={errors.state}
        placeholder="Select state/province"
        disabled={!formData.country || !states[formData.country]}
        density="comfortable"
      >
        {states[formData.country]?.map(state => (
          <SafOption key={state.value} value={state.value}>
            {state.label}
          </SafOption>
        ))}
      </SafSelect>

      <SafSelect
        name="priority"
        value={formData.priority}
        onChange={handleSelectChange('priority')}
        density="comfortable"
        labelPosition="top"
      >
        <label slot="start">Priority Level</label>
        {priorities.map(priority => (
          <SafOption 
            key={priority.value} 
            value={priority.value}
            title={priority.description}
          >
            <div className="priority-option">
              <span className="priority-label">{priority.label}</span>
              <small className="priority-desc">{priority.description}</small>
            </div>
          </SafOption>
        ))}
      </SafSelect>

      <button type="button" onClick={validateForm}>
        Save Settings
      </button>
    </form>
  );
}
```

### Grouped Options

```tsx
import { SafSelect, SafOption } from '@saffron/react-components';
import { useState } from 'react';

function GroupedSelect() {
  const [selectedFont, setSelectedFont] = useState('');

  const fontGroups = {
    'Serif Fonts': [
      { value: 'times', label: 'Times New Roman' },
      { value: 'georgia', label: 'Georgia' },
      { value: 'garamond', label: 'Garamond' }
    ],
    'Sans-Serif Fonts': [
      { value: 'arial', label: 'Arial' },
      { value: 'helvetica', label: 'Helvetica' },
      { value: 'verdana', label: 'Verdana' }
    ],
    'Monospace Fonts': [
      { value: 'courier', label: 'Courier New' },
      { value: 'consolas', label: 'Consolas' },
      { value: 'monaco', label: 'Monaco' }
    ]
  };

  return (
    <SafSelect
      value={selectedFont}
      onChange={(e) => setSelectedFont(e.target.value)}
      placeholder="Choose a font family"
      maxHeight="300px"
    >
      {Object.entries(fontGroups).map(([groupName, fonts]) => (
        <div key={groupName}>
          <SafOption value="" disabled className="group-header">
            {groupName}
          </SafOption>
          {fonts.map(font => (
            <SafOption 
              key={font.value} 
              value={font.value}
              style={{ fontFamily: font.value, paddingLeft: '20px' }}
            >
              {font.label}
            </SafOption>
          ))}
        </div>
      ))}
    </SafSelect>
  );
}
```

### Custom Option Rendering

```tsx
import { SafSelect, SafOption } from '@saffron/react-components';
import { useState } from 'react';

function CustomOptionSelect() {
  const [selectedUser, setSelectedUser] = useState('');

  const users = [
    { id: '1', name: 'John Doe', email: 'john@example.com', avatar: '👨', role: 'Admin' },
    { id: '2', name: 'Jane Smith', email: 'jane@example.com', avatar: '👩', role: 'User' },
    { id: '3', name: 'Mike Johnson', email: 'mike@example.com', avatar: '👨‍💼', role: 'Manager' },
    { id: '4', name: 'Sarah Wilson', email: 'sarah@example.com', avatar: '👩‍💻', role: 'Developer' }
  ];

  return (
    <div className="user-selector">
      <SafSelect
        value={selectedUser}
        onChange={(e) => setSelectedUser(e.target.value)}
        placeholder="Select a team member"
        density="comfortable"
        maxHeight="250px"
      >
        {users.map(user => (
          <SafOption key={user.id} value={user.id}>
            <div className="user-option">
              <span className="user-avatar">{user.avatar}</span>
              <div className="user-details">
                <span className="user-name">{user.name}</span>
                <span className="user-email">{user.email}</span>
                <span className="user-role">{user.role}</span>
              </div>
            </div>
          </SafOption>
        ))}
      </SafSelect>

      {selectedUser && (
        <div className="selected-user-info">
          <h4>Selected User:</h4>
          <p>{users.find(u => u.id === selectedUser)?.name}</p>
        </div>
      )}
    </div>
  );
}
```

### API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `undefined` | The selected option value |
| `placeholder` | `string` | `undefined` | Placeholder text when no option is selected |
| `disabled` | `boolean` | `false` | Disables the select dropdown |
| `invalid` | `boolean` | `false` | Indicates validation error state |
| `validationMessage` | `string` | `undefined` | Error message displayed when invalid |
| `name` | `string` | `undefined` | Name attribute for form submission |
| `multiple` | `boolean` | `false` | Enables multiple selection (not recommended - use multiselect component) |
| `size` | `number` | `undefined` | Number of visible options in dropdown |
| `maxHeight` | `string` | `undefined` | Maximum height of dropdown (e.g., "200px") |
| `density` | `'compact' \| 'comfortable' \| 'spacious'` | `'comfortable'` | Visual density of the component |
| `labelPosition` | `'top' \| 'left' \| 'right'` | `'top'` | Position of the label relative to select |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for screen readers |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for selection changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |
| `onOpen` | `() => void` | `undefined` | Handler for dropdown open events |
| `onClose` | `() => void` | `undefined` | Handler for dropdown close events |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-select',
  template: `
    <saf-select 
      [value]="selectedValue"
      (change)="onSelectionChange($event)"
      placeholder="Choose an option...">
      <saf-option value="option1">Option 1</saf-option>
      <saf-option value="option2">Option 2</saf-option>
      <saf-option value="option3">Option 3</saf-option>
    </saf-select>
  `
})
export class BasicSelectComponent {
  selectedValue = '';

  onSelectionChange(event: any) {
    this.selectedValue = event.target.value;
  }
}
```

### Advanced Usage with Forms

```typescript
// component.ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-advanced-select',
  template: `
    <form [formGroup]="locationForm" (ngSubmit)="onSubmit()">
      <h3>Location Settings</h3>

      <saf-select
        formControlName="country"
        [invalid]="isFieldInvalid('country')"
        [validation-message]="getErrorMessage('country')"
        placeholder="Select your country"
        density="comfortable"
        a11y-aria-label="Country selection">
        <saf-option 
          *ngFor="let country of countries" 
          [value]="country.value">
          {{ country.label }}
        </saf-option>
      </saf-select>

      <saf-select
        formControlName="state"
        [invalid]="isFieldInvalid('state')"
        [validation-message]="getErrorMessage('state')"
        placeholder="Select state/province"
        [disabled]="!getAvailableStates().length"
        density="comfortable">
        <saf-option 
          *ngFor="let state of getAvailableStates()" 
          [value]="state.value">
          {{ state.label }}
        </saf-option>
      </saf-select>

      <saf-select
        formControlName="priority"
        density="comfortable"
        label-position="top">
        <label slot="start">Priority Level</label>
        <saf-option 
          *ngFor="let priority of priorities" 
          [value]="priority.value"
          [title]="priority.description">
          <div class="priority-option">
            <span class="priority-label">{{ priority.label }}</span>
            <small class="priority-desc">{{ priority.description }}</small>
          </div>
        </saf-option>
      </saf-select>

      <button type="submit" [disabled]="locationForm.invalid">
        Save Settings
      </button>
    </form>
  `
})
export class AdvancedSelectComponent implements OnInit {
  locationForm: FormGroup;

  countries = [
    { value: 'us', label: 'United States' },
    { value: 'ca', label: 'Canada' },
    { value: 'uk', label: 'United Kingdom' }
  ];

  states = {
    us: [
      { value: 'ny', label: 'New York' },
      { value: 'ca', label: 'California' },
      { value: 'tx', label: 'Texas' }
    ],
    ca: [
      { value: 'on', label: 'Ontario' },
      { value: 'bc', label: 'British Columbia' }
    ]
  };

  priorities = [
    { value: 'low', label: 'Low Priority', description: '72+ hours response' },
    { value: 'medium', label: 'Medium Priority', description: '24-48 hours response' },
    { value: 'high', label: 'High Priority', description: '4-8 hours response' }
  ];

  constructor(private fb: FormBuilder) {}

  ngOnInit() {
    this.locationForm = this.fb.group({
      country: ['', [Validators.required]],
      state: [''],
      priority: ['medium']
    });

    // Reset state when country changes
    this.locationForm.get('country')?.valueChanges.subscribe(() => {
      this.locationForm.get('state')?.setValue('');
    });
  }

  getAvailableStates() {
    const selectedCountry = this.locationForm.get('country')?.value;
    return this.states[selectedCountry] || [];
  }

  isFieldInvalid(fieldName: string): boolean {
    const field = this.locationForm.get(fieldName);
    return !!(field && field.invalid && (field.dirty || field.touched));
  }

  getErrorMessage(fieldName: string): string {
    const field = this.locationForm.get(fieldName);
    if (field?.errors?.['required']) {
      return `${fieldName.charAt(0).toUpperCase() + fieldName.slice(1)} is required`;
    }
    return '';
  }

  onSubmit() {
    if (this.locationForm.valid) {
      console.log('Form submitted:', this.locationForm.value);
    } else {
      this.markFormGroupTouched();
    }
  }

  private markFormGroupTouched() {
    Object.keys(this.locationForm.controls).forEach(key => {
      this.locationForm.get(key)?.markAsTouched();
    });
  }
}
```

### API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `value` | `string` | `undefined` | Selected option value |
| `placeholder` | `string` | `undefined` | Placeholder text |
| `disabled` | `boolean` | `false` | Disabled state |
| `invalid` | `boolean` | `false` | Error state |
| `validationMessage` | `string` | `undefined` | Error message |
| `name` | `string` | `undefined` | Form field name |
| `multiple` | `boolean` | `false` | Multiple selection |
| `size` | `number` | `undefined` | Visible options count |
| `maxHeight` | `string` | `undefined` | Dropdown max height |
| `density` | `string` | `'comfortable'` | Visual density |
| `labelPosition` | `string` | `'top'` | Label positioning |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when selection changes |
| `input` | `Event` | Emitted when value updates |
| `focus` | `Event` | Emitted when select receives focus |
| `blur` | `Event` | Emitted when select loses focus |
| `open` | `Event` | Emitted when dropdown opens |
| `close` | `Event` | Emitted when dropdown closes |

## Best Practices

### Accessibility
- **Descriptive labels**: Use clear, concise labels that describe what the user is selecting
- **Keyboard navigation**: Support Arrow keys, Enter, Escape, Home, End for navigation
- **Screen reader support**: Provide proper ARIA labels and descriptions
- **Focus management**: Ensure logical focus order and clear visual focus indicators

### UX Guidelines
- **Option ordering**: Order options logically (alphabetical, by frequency, by importance)
- **Default selection**: Provide sensible defaults when appropriate
- **Placeholder text**: Use helpful placeholder text that describes the expected selection
- **Grouping**: Group related options with disabled header options or visual separators

### Performance
- **Large lists**: For 100+ options, consider virtualization or search functionality
- **Dynamic loading**: Load options asynchronously for better initial performance
- **Debounced filtering**: Implement search with debouncing for responsive filtering
- **Minimize re-renders**: Use proper state management to avoid unnecessary updates

### Form Design
- **Validation timing**: Validate on blur or form submission, not on each selection
- **Error placement**: Show validation messages near the select component
- **Required indicators**: Clearly mark required fields with asterisks or other indicators
- **Dependent selects**: Reset dependent select values when parent selections change

## Accessibility Notes

The SafSelect component includes comprehensive accessibility features:

- **ARIA compliance**: Full implementation of ARIA select, listbox, and option roles
- **Screen reader support**: Proper announcements for selections, state changes, and errors
- **Keyboard navigation**: Complete keyboard support for dropdown interaction
- **Focus management**: Proper focus handling for dropdown open/close states
- **Error handling**: Screen reader accessible error messages and validation states

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+
- **Floating UI**: Uses @floating-ui/dom for positioning across all browsers
- **Accessibility**: NVDA, JAWS, VoiceOver support

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: The `value` prop is now controlled by default, requires proper state management
- **v1.x to v2.x**: Floating UI replaced Popper.js for positioning, may affect custom positioning
- **Deprecated props**: `defaultValue` replaced with `value` and proper state management

---

*This documentation provides comprehensive guidance for implementing SafSelect in both React and Angular applications with proper accessibility, performance, and user experience considerations.*
