# SafTextInput Component

## Overview

SafTextInput is a versatile text input component that provides a consistent interface for single-line text entry. It supports various input types, validation states, formatting options, and accessibility features. SafTextInput is designed to handle common text input scenarios including user registration, search, data entry, and form filling with built-in support for validation, masking, and real-time feedback.

## React API

### SafTextInput

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `value` | `string` | No | `''` | Current input value |
| `defaultValue` | `string` | No | `''` | Default value for uncontrolled usage |
| `type` | `'text' \| 'email' \| 'password' \| 'tel' \| 'url' \| 'search' \| 'number'` | No | `'text'` | Input type for validation and keyboard |
| `placeholder` | `string` | No | - | Placeholder text when input is empty |
| `label` | `string \| ReactNode` | No | - | Label text for the input |
| `description` | `string \| ReactNode` | No | - | Additional descriptive text |
| `helperText` | `string \| ReactNode` | No | - | Helper text below the input |
| `error` | `string \| boolean` | No | `false` | Error state and message |
| `success` | `string \| boolean` | No | `false` | Success state and message |
| `warning` | `string \| boolean` | No | `false` | Warning state and message |
| `required` | `boolean` | No | `false` | Whether the input is required |
| `disabled` | `boolean` | No | `false` | Whether the input is disabled |
| `readOnly` | `boolean` | No | `false` | Whether the input is read-only |
| `autoComplete` | `string` | No | - | Autocomplete attribute value |
| `autoFocus` | `boolean` | No | `false` | Whether to auto-focus the input |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the input |
| `variant` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `fullWidth` | `boolean` | No | `false` | Whether input takes full container width |
| `maxLength` | `number` | No | - | Maximum number of characters |
| `minLength` | `number` | No | - | Minimum number of characters |
| `pattern` | `string` | No | - | Regex pattern for validation |
| `mask` | `string \| MaskFunction` | No | - | Input mask for formatting |
| `prefix` | `string \| ReactNode` | No | - | Content before input text |
| `suffix` | `string \| ReactNode` | No | - | Content after input text |
| `startAdornment` | `ReactNode` | No | - | Icon or content at start of input |
| `endAdornment` | `ReactNode` | No | - | Icon or content at end of input |
| `clearable` | `boolean` | No | `false` | Whether to show clear button |
| `showCharacterCount` | `boolean` | No | `false` | Whether to show character counter |
| `debounceMs` | `number` | No | `0` | Debounce delay for onChange callback |
| `validateOnChange` | `boolean` | No | `true` | Whether to validate on each change |
| `validateOnBlur` | `boolean` | No | `true` | Whether to validate on blur |
| `formatOnBlur` | `boolean` | No | `false` | Whether to format value on blur |
| `selectOnFocus` | `boolean` | No | `false` | Whether to select all text on focus |
| `onChange` | `(value: string, event: ChangeEvent) => void` | No | - | Callback when input value changes |
| `onBlur` | `(event: FocusEvent) => void` | No | - | Callback when input loses focus |
| `onFocus` | `(event: FocusEvent) => void` | No | - | Callback when input gains focus |
| `onKeyDown` | `(event: KeyboardEvent) => void` | No | - | Callback for key down events |
| `onClear` | `() => void` | No | - | Callback when clear button is clicked |
| `validate` | `(value: string) => string \| null` | No | - | Custom validation function |
| `format` | `(value: string) => string` | No | - | Custom formatting function |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

## Angular API

### saf-text-input

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[value]` | `string` | No | `''` | Current input value |
| `[type]` | `'text' \| 'email' \| 'password' \| 'tel' \| 'url' \| 'search' \| 'number'` | No | `'text'` | Input type for validation and keyboard |
| `[placeholder]` | `string` | No | - | Placeholder text when input is empty |
| `[label]` | `string \| TemplateRef` | No | - | Label text for the input |
| `[description]` | `string \| TemplateRef` | No | - | Additional descriptive text |
| `[helperText]` | `string \| TemplateRef` | No | - | Helper text below the input |
| `[error]` | `string \| boolean` | No | `false` | Error state and message |
| `[success]` | `string \| boolean` | No | `false` | Success state and message |
| `[warning]` | `string \| boolean` | No | `false` | Warning state and message |
| `[required]` | `boolean` | No | `false` | Whether the input is required |
| `[disabled]` | `boolean` | No | `false` | Whether the input is disabled |
| `[readonly]` | `boolean` | No | `false` | Whether the input is read-only |
| `[autoComplete]` | `string` | No | - | Autocomplete attribute value |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the input |
| `[variant]` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `[fullWidth]` | `boolean` | No | `false` | Whether input takes full container width |
| `[maxLength]` | `number` | No | - | Maximum number of characters |
| `[minLength]` | `number` | No | - | Minimum number of characters |
| `[pattern]` | `string` | No | - | Regex pattern for validation |
| `[mask]` | `string` | No | - | Input mask for formatting |
| `[prefix]` | `string \| TemplateRef` | No | - | Content before input text |
| `[suffix]` | `string \| TemplateRef` | No | - | Content after input text |
| `[clearable]` | `boolean` | No | `false` | Whether to show clear button |
| `[showCharacterCount]` | `boolean` | No | `false` | Whether to show character counter |
| `[debounceMs]` | `number` | No | `0` | Debounce delay for valueChange event |
| `[validateOnChange]` | `boolean` | No | `true` | Whether to validate on each change |
| `[validateOnBlur]` | `boolean` | No | `true` | Whether to validate on blur |
| `[selectOnFocus]` | `boolean` | No | `false` | Whether to select all text on focus |
| `(valueChange)` | `EventEmitter<string>` | No | - | Event when input value changes |
| `(blur)` | `EventEmitter<FocusEvent>` | No | - | Event when input loses focus |
| `(focus)` | `EventEmitter<FocusEvent>` | No | - | Event when input gains focus |
| `(keydown)` | `EventEmitter<KeyboardEvent>` | No | - | Event for key down events |
| `(clear)` | `EventEmitter<void>` | No | - | Event when clear button is clicked |

## Usage Examples

### Basic Text Inputs

#### React
```jsx
import { SafTextInput, SafCard, SafIcon } from '@saffron/react';
import { useState } from 'react';

const BasicTextInputExample = () => {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    website: ''
  });

  const handleInputChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }));
  };

  return (
    <SafCard className="text-input-demo">
      <SafCard.Header>
        <h2>Contact Information</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="form-grid">
          <SafTextInput
            label="First Name"
            placeholder="Enter your first name"
            value={formData.firstName}
            onChange={(value) => handleInputChange('firstName', value)}
            required={true}
            autoComplete="given-name"
            size="medium"
          />

          <SafTextInput
            label="Last Name"
            placeholder="Enter your last name"
            value={formData.lastName}
            onChange={(value) => handleInputChange('lastName', value)}
            required={true}
            autoComplete="family-name"
            size="medium"
          />

          <SafTextInput
            label="Email Address"
            type="email"
            placeholder="Enter your email"
            value={formData.email}
            onChange={(value) => handleInputChange('email', value)}
            required={true}
            autoComplete="email"
            startAdornment={<SafIcon name="mail" />}
            helperText="We'll never share your email"
            fullWidth={true}
          />

          <SafTextInput
            label="Phone Number"
            type="tel"
            placeholder="(555) 123-4567"
            value={formData.phone}
            onChange={(value) => handleInputChange('phone', value)}
            autoComplete="tel"
            mask="(999) 999-9999"
            startAdornment={<SafIcon name="phone" />}
          />

          <SafTextInput
            label="Website"
            type="url"
            placeholder="https://your-website.com"
            value={formData.website}
            onChange={(value) => handleInputChange('website', value)}
            autoComplete="url"
            startAdornment={<SafIcon name="globe" />}
            clearable={true}
          />
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// basic-text-input.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-text-input',
  template: `
    <saf-card class="text-input-demo">
      <saf-card-header>
        <h2>Contact Information</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="form-grid">
          <saf-text-input
            label="First Name"
            placeholder="Enter your first name"
            [value]="formData.firstName"
            (valueChange)="handleInputChange('firstName', $event)"
            [required]="true"
            autoComplete="given-name"
            size="medium">
          </saf-text-input>

          <saf-text-input
            label="Last Name"
            placeholder="Enter your last name"
            [value]="formData.lastName"
            (valueChange)="handleInputChange('lastName', $event)"
            [required]="true"
            autoComplete="family-name"
            size="medium">
          </saf-text-input>

          <saf-text-input
            label="Email Address"
            type="email"
            placeholder="Enter your email"
            [value]="formData.email"
            (valueChange)="handleInputChange('email', $event)"
            [required]="true"
            autoComplete="email"
            helperText="We'll never share your email"
            [fullWidth]="true">
            <saf-icon name="mail" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-text-input
            label="Phone Number"
            type="tel"
            placeholder="(555) 123-4567"
            [value]="formData.phone"
            (valueChange)="handleInputChange('phone', $event)"
            autoComplete="tel"
            mask="(999) 999-9999">
            <saf-icon name="phone" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-text-input
            label="Website"
            type="url"
            placeholder="https://your-website.com"
            [value]="formData.website"
            (valueChange)="handleInputChange('website', $event)"
            autoComplete="url"
            [clearable]="true">
            <saf-icon name="globe" slot="start-adornment"></saf-icon>
          </saf-text-input>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class BasicTextInputComponent {
  formData = {
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    website: ''
  };

  handleInputChange(field: string, value: string) {
    this.formData = {
      ...this.formData,
      [field]: value
    };
  }
}
```

### Advanced Text Inputs with Validation

#### React
```jsx
import { SafTextInput, SafCard, SafButton, SafIcon } from '@saffron/react';
import { useState } from 'react';

const AdvancedTextInputExample = () => {
  const [formData, setFormData] = useState({
    username: '',
    password: '',
    confirmPassword: '',
    socialSecurityNumber: '',
    creditCard: ''
  });

  const [errors, setErrors] = useState({});
  const [touched, setTouched] = useState({});

  const validateUsername = (value) => {
    if (!value) return 'Username is required';
    if (value.length < 3) return 'Username must be at least 3 characters';
    if (!/^[a-zA-Z0-9_]+$/.test(value)) return 'Username can only contain letters, numbers, and underscores';
    return null;
  };

  const validatePassword = (value) => {
    if (!value) return 'Password is required';
    if (value.length < 8) return 'Password must be at least 8 characters';
    if (!/(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/.test(value)) {
      return 'Password must contain uppercase, lowercase, and numbers';
    }
    return null;
  };

  const validateConfirmPassword = (value) => {
    if (!value) return 'Please confirm your password';
    if (value !== formData.password) return 'Passwords do not match';
    return null;
  };

  const validateSSN = (value) => {
    if (!value) return null; // Optional field
    const ssnPattern = /^\d{3}-\d{2}-\d{4}$/;
    if (!ssnPattern.test(value)) return 'SSN must be in format 123-45-6789';
    return null;
  };

  const validateCreditCard = (value) => {
    if (!value) return null; // Optional field
    const cleaned = value.replace(/\s+/g, '');
    if (!/^\d{13,19}$/.test(cleaned)) return 'Invalid credit card number';
    return null;
  };

  const handleInputChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }));

    // Validate field
    let error = null;
    switch (field) {
      case 'username': error = validateUsername(value); break;
      case 'password': error = validatePassword(value); break;
      case 'confirmPassword': error = validateConfirmPassword(value); break;
      case 'socialSecurityNumber': error = validateSSN(value); break;
      case 'creditCard': error = validateCreditCard(value); break;
    }

    setErrors(prev => ({
      ...prev,
      [field]: error
    }));
  };

  const handleBlur = (field) => {
    setTouched(prev => ({
      ...prev,
      [field]: true
    }));
  };

  const formatCreditCard = (value) => {
    const v = value.replace(/\s+/g, '').replace(/[^0-9]/gi, '');
    const matches = v.match(/\d{4,16}/g);
    const match = matches && matches[0] || '';
    const parts = [];
    for (let i = 0, len = match.length; i < len; i += 4) {
      parts.push(match.substring(i, i + 4));
    }
    if (parts.length) {
      return parts.join(' ');
    } else {
      return v;
    }
  };

  const getPasswordStrength = (password) => {
    let strength = 0;
    if (password.length >= 8) strength++;
    if (/[a-z]/.test(password)) strength++;
    if (/[A-Z]/.test(password)) strength++;
    if (/\d/.test(password)) strength++;
    if (/[^a-zA-Z0-9]/.test(password)) strength++;
    
    const levels = ['Very Weak', 'Weak', 'Fair', 'Good', 'Strong'];
    const colors = ['error', 'error', 'warning', 'primary', 'success'];
    
    return {
      level: levels[Math.min(strength, 4)],
      color: colors[Math.min(strength, 4)],
      percentage: (strength / 5) * 100
    };
  };

  const passwordStrength = getPasswordStrength(formData.password);

  return (
    <SafCard className="advanced-text-input-demo">
      <SafCard.Header>
        <h2>Account Registration</h2>
      </SafCard.Header>
      <SafCard.Content>
        <form className="registration-form">
          <SafTextInput
            label="Username"
            placeholder="Choose a username"
            value={formData.username}
            onChange={(value) => handleInputChange('username', value)}
            onBlur={() => handleBlur('username')}
            error={touched.username ? errors.username : false}
            required={true}
            autoComplete="username"
            startAdornment={<SafIcon name="user" />}
            helperText="3+ characters, letters, numbers, and underscores only"
            showCharacterCount={true}
            maxLength={20}
          />

          <SafTextInput
            label="Password"
            type="password"
            placeholder="Create a strong password"
            value={formData.password}
            onChange={(value) => handleInputChange('password', value)}
            onBlur={() => handleBlur('password')}
            error={touched.password ? errors.password : false}
            required={true}
            autoComplete="new-password"
            startAdornment={<SafIcon name="lock" />}
            helperText={
              <div className="password-strength">
                <div className="strength-bar">
                  <div 
                    className={`strength-fill ${passwordStrength.color}`}
                    style={{ width: `${passwordStrength.percentage}%` }}
                  />
                </div>
                <span className={`strength-text ${passwordStrength.color}`}>
                  {passwordStrength.level}
                </span>
              </div>
            }
          />

          <SafTextInput
            label="Confirm Password"
            type="password"
            placeholder="Confirm your password"
            value={formData.confirmPassword}
            onChange={(value) => handleInputChange('confirmPassword', value)}
            onBlur={() => handleBlur('confirmPassword')}
            error={touched.confirmPassword ? errors.confirmPassword : false}
            success={formData.confirmPassword && !errors.confirmPassword ? 'Passwords match' : false}
            required={true}
            autoComplete="new-password"
            startAdornment={<SafIcon name="check" />}
          />

          <SafTextInput
            label="Social Security Number (Optional)"
            placeholder="123-45-6789"
            value={formData.socialSecurityNumber}
            onChange={(value) => handleInputChange('socialSecurityNumber', value)}
            onBlur={() => handleBlur('socialSecurityNumber')}
            error={touched.socialSecurityNumber ? errors.socialSecurityNumber : false}
            mask="999-99-9999"
            autoComplete="off"
            startAdornment={<SafIcon name="shield" />}
            helperText="This information is encrypted and secure"
          />

          <SafTextInput
            label="Credit Card (Optional)"
            placeholder="1234 5678 9012 3456"
            value={formData.creditCard}
            onChange={(value) => handleInputChange('creditCard', value)}
            onBlur={() => handleBlur('creditCard')}
            error={touched.creditCard ? errors.creditCard : false}
            format={formatCreditCard}
            maxLength={19}
            autoComplete="cc-number"
            startAdornment={<SafIcon name="credit-card" />}
            clearable={true}
          />

          <SafButton 
            variant="primary" 
            size="large" 
            fullWidth={true}
            disabled={Object.values(errors).some(error => error)}
          >
            Create Account
          </SafButton>
        </form>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// advanced-text-input.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-text-input',
  template: `
    <saf-card class="advanced-text-input-demo">
      <saf-card-header>
        <h2>Account Registration</h2>
      </saf-card-header>
      <saf-card-content>
        <form class="registration-form">
          <saf-text-input
            label="Username"
            placeholder="Choose a username"
            [value]="formData.username"
            (valueChange)="handleInputChange('username', $event)"
            (blur)="handleBlur('username')"
            [error]="getFieldError('username')"
            [required]="true"
            autoComplete="username"
            helperText="3+ characters, letters, numbers, and underscores only"
            [showCharacterCount]="true"
            [maxLength]="20">
            <saf-icon name="user" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-text-input
            label="Password"
            type="password"
            placeholder="Create a strong password"
            [value]="formData.password"
            (valueChange)="handleInputChange('password', $event)"
            (blur)="handleBlur('password')"
            [error]="getFieldError('password')"
            [required]="true"
            autoComplete="new-password">
            <saf-icon name="lock" slot="start-adornment"></saf-icon>
            <div slot="helper-text" class="password-strength">
              <div class="strength-bar">
                <div 
                  class="strength-fill"
                  [class]="passwordStrength.color"
                  [style.width.%]="passwordStrength.percentage">
                </div>
              </div>
              <span 
                class="strength-text"
                [class]="passwordStrength.color">
                {{ passwordStrength.level }}
              </span>
            </div>
          </saf-text-input>

          <saf-text-input
            label="Confirm Password"
            type="password"
            placeholder="Confirm your password"
            [value]="formData.confirmPassword"
            (valueChange)="handleInputChange('confirmPassword', $event)"
            (blur)="handleBlur('confirmPassword')"
            [error]="getFieldError('confirmPassword')"
            [success]="getFieldSuccess('confirmPassword')"
            [required]="true"
            autoComplete="new-password">
            <saf-icon name="check" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-text-input
            label="Social Security Number (Optional)"
            placeholder="123-45-6789"
            [value]="formData.socialSecurityNumber"
            (valueChange)="handleInputChange('socialSecurityNumber', $event)"
            (blur)="handleBlur('socialSecurityNumber')"
            [error]="getFieldError('socialSecurityNumber')"
            mask="999-99-9999"
            autoComplete="off"
            helperText="This information is encrypted and secure">
            <saf-icon name="shield" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-text-input
            label="Credit Card (Optional)"
            placeholder="1234 5678 9012 3456"
            [value]="formData.creditCard"
            (valueChange)="handleInputChange('creditCard', $event)"
            (blur)="handleBlur('creditCard')"
            [error]="getFieldError('creditCard')"
            [maxLength]="19"
            autoComplete="cc-number"
            [clearable]="true">
            <saf-icon name="credit-card" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <saf-button 
            variant="primary" 
            size="large" 
            [fullWidth]="true"
            [disabled]="hasErrors()">
            Create Account
          </saf-button>
        </form>
      </saf-card-content>
    </saf-card>
  `
})
export class AdvancedTextInputComponent {
  formData = {
    username: '',
    password: '',
    confirmPassword: '',
    socialSecurityNumber: '',
    creditCard: ''
  };

  errors: { [key: string]: string } = {};
  touched: { [key: string]: boolean } = {};

  handleInputChange(field: string, value: string) {
    this.formData = {
      ...this.formData,
      [field]: value
    };

    // Validate field
    let error = '';
    switch (field) {
      case 'username': error = this.validateUsername(value); break;
      case 'password': error = this.validatePassword(value); break;
      case 'confirmPassword': error = this.validateConfirmPassword(value); break;
      case 'socialSecurityNumber': error = this.validateSSN(value); break;
      case 'creditCard': error = this.validateCreditCard(value); break;
    }

    this.errors[field] = error;
  }

  handleBlur(field: string) {
    this.touched[field] = true;
  }

  validateUsername(value: string): string {
    if (!value) return 'Username is required';
    if (value.length < 3) return 'Username must be at least 3 characters';
    if (!/^[a-zA-Z0-9_]+$/.test(value)) return 'Username can only contain letters, numbers, and underscores';
    return '';
  }

  validatePassword(value: string): string {
    if (!value) return 'Password is required';
    if (value.length < 8) return 'Password must be at least 8 characters';
    if (!/(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/.test(value)) {
      return 'Password must contain uppercase, lowercase, and numbers';
    }
    return '';
  }

  validateConfirmPassword(value: string): string {
    if (!value) return 'Please confirm your password';
    if (value !== this.formData.password) return 'Passwords do not match';
    return '';
  }

  validateSSN(value: string): string {
    if (!value) return ''; // Optional field
    const ssnPattern = /^\d{3}-\d{2}-\d{4}$/;
    if (!ssnPattern.test(value)) return 'SSN must be in format 123-45-6789';
    return '';
  }

  validateCreditCard(value: string): string {
    if (!value) return ''; // Optional field
    const cleaned = value.replace(/\s+/g, '');
    if (!/^\d{13,19}$/.test(cleaned)) return 'Invalid credit card number';
    return '';
  }

  getFieldError(field: string): string | boolean {
    return this.touched[field] ? this.errors[field] || false : false;
  }

  getFieldSuccess(field: string): string | boolean {
    if (field === 'confirmPassword') {
      return this.formData.confirmPassword && !this.errors.confirmPassword ? 'Passwords match' : false;
    }
    return false;
  }

  get passwordStrength() {
    const password = this.formData.password;
    let strength = 0;
    if (password.length >= 8) strength++;
    if (/[a-z]/.test(password)) strength++;
    if (/[A-Z]/.test(password)) strength++;
    if (/\d/.test(password)) strength++;
    if (/[^a-zA-Z0-9]/.test(password)) strength++;
    
    const levels = ['Very Weak', 'Weak', 'Fair', 'Good', 'Strong'];
    const colors = ['error', 'error', 'warning', 'primary', 'success'];
    
    return {
      level: levels[Math.min(strength, 4)],
      color: colors[Math.min(strength, 4)],
      percentage: (strength / 5) * 100
    };
  }

  hasErrors(): boolean {
    return Object.values(this.errors).some(error => error);
  }
}
```

### Search and Filter Inputs

#### React
```jsx
import { SafTextInput, SafCard, SafIcon, SafBadge, SafButton } from '@saffron/react';
import { useState, useMemo } from 'react';

const SearchFilterInputExample = () => {
  const [searchQuery, setSearchQuery] = useState('');
  const [filterValue, setFilterValue] = useState('');
  const [quickSearch, setQuickSearch] = useState('');

  // Mock data for demonstration
  const mockData = [
    { id: 1, name: 'John Doe', email: 'john@example.com', department: 'Engineering' },
    { id: 2, name: 'Jane Smith', email: 'jane@example.com', department: 'Marketing' },
    { id: 3, name: 'Bob Johnson', email: 'bob@example.com', department: 'Sales' },
    { id: 4, name: 'Alice Wilson', email: 'alice@example.com', department: 'Engineering' },
    { id: 5, name: 'Charlie Brown', email: 'charlie@example.com', department: 'HR' }
  ];

  const filteredData = useMemo(() => {
    return mockData.filter(item => {
      const matchesSearch = !searchQuery || 
        item.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
        item.email.toLowerCase().includes(searchQuery.toLowerCase());
      
      const matchesFilter = !filterValue ||
        item.department.toLowerCase().includes(filterValue.toLowerCase());
      
      const matchesQuick = !quickSearch ||
        item.name.toLowerCase().includes(quickSearch.toLowerCase());
      
      return matchesSearch && matchesFilter && matchesQuick;
    });
  }, [searchQuery, filterValue, quickSearch, mockData]);

  const handleClearAll = () => {
    setSearchQuery('');
    setFilterValue('');
    setQuickSearch('');
  };

  const handleKeyDown = (event, action) => {
    if (event.key === 'Enter') {
      action();
    }
  };

  return (
    <SafCard className="search-filter-demo">
      <SafCard.Header>
        <h2>Employee Directory</h2>
        <SafButton variant="outline" onClick={handleClearAll}>
          Clear All Filters
        </SafButton>
      </SafCard.Header>
      <SafCard.Content>
        <div className="search-controls">
          <SafTextInput
            type="search"
            placeholder="Search employees..."
            value={searchQuery}
            onChange={setSearchQuery}
            startAdornment={<SafIcon name="search" />}
            clearable={true}
            size="large"
            fullWidth={true}
            debounceMs={300}
            helperText={`${filteredData.length} results found`}
            onKeyDown={(e) => handleKeyDown(e, () => console.log('Search initiated'))}
          />

          <div className="filter-row">
            <SafTextInput
              placeholder="Filter by department..."
              value={filterValue}
              onChange={setFilterValue}
              startAdornment={<SafIcon name="filter" />}
              clearable={true}
              size="medium"
              debounceMs={200}
            />

            <SafTextInput
              placeholder="Quick name search..."
              value={quickSearch}
              onChange={setQuickSearch}
              startAdornment={<SafIcon name="zap" />}
              endAdornment={
                quickSearch && (
                  <SafBadge variant="primary" size="small">
                    {filteredData.length}
                  </SafBadge>
                )
              }
              size="medium"
              selectOnFocus={true}
            />
          </div>
        </div>

        <div className="results-section">
          <div className="results-header">
            <h3>Search Results</h3>
            {(searchQuery || filterValue || quickSearch) && (
              <div className="active-filters">
                {searchQuery && (
                  <SafBadge variant="primary" className="filter-badge">
                    Search: {searchQuery}
                  </SafBadge>
                )}
                {filterValue && (
                  <SafBadge variant="secondary" className="filter-badge">
                    Dept: {filterValue}
                  </SafBadge>
                )}
                {quickSearch && (
                  <SafBadge variant="success" className="filter-badge">
                    Quick: {quickSearch}
                  </SafBadge>
                )}
              </div>
            )}
          </div>

          <div className="results-list">
            {filteredData.length > 0 ? (
              filteredData.map(item => (
                <div key={item.id} className="result-item">
                  <div className="result-info">
                    <h4>{item.name}</h4>
                    <p>{item.email}</p>
                  </div>
                  <SafBadge variant="outline">
                    {item.department}
                  </SafBadge>
                </div>
              ))
            ) : (
              <div className="no-results">
                <SafIcon name="search" size="large" />
                <p>No employees found matching your criteria</p>
              </div>
            )}
          </div>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// search-filter-input.component.ts
import { Component } from '@angular/core';

interface Employee {
  id: number;
  name: string;
  email: string;
  department: string;
}

@Component({
  selector: 'app-search-filter-input',
  template: `
    <saf-card class="search-filter-demo">
      <saf-card-header>
        <h2>Employee Directory</h2>
        <saf-button variant="outline" (click)="handleClearAll()">
          Clear All Filters
        </saf-button>
      </saf-card-header>
      <saf-card-content>
        <div class="search-controls">
          <saf-text-input
            type="search"
            placeholder="Search employees..."
            [value]="searchQuery"
            (valueChange)="searchQuery = $event; updateResults()"
            [clearable]="true"
            size="large"
            [fullWidth]="true"
            [debounceMs]="300"
            [helperText]="filteredData.length + ' results found'"
            (keydown)="handleKeyDown($event, 'search')">
            <saf-icon name="search" slot="start-adornment"></saf-icon>
          </saf-text-input>

          <div class="filter-row">
            <saf-text-input
              placeholder="Filter by department..."
              [value]="filterValue"
              (valueChange)="filterValue = $event; updateResults()"
              [clearable]="true"
              size="medium"
              [debounceMs]="200">
              <saf-icon name="filter" slot="start-adornment"></saf-icon>
            </saf-text-input>

            <saf-text-input
              placeholder="Quick name search..."
              [value]="quickSearch"
              (valueChange)="quickSearch = $event; updateResults()"
              size="medium"
              [selectOnFocus]="true">
              <saf-icon name="zap" slot="start-adornment"></saf-icon>
              <saf-badge 
                *ngIf="quickSearch" 
                variant="primary" 
                size="small"
                slot="end-adornment">
                {{ filteredData.length }}
              </saf-badge>
            </saf-text-input>
          </div>
        </div>

        <div class="results-section">
          <div class="results-header">
            <h3>Search Results</h3>
            <div 
              *ngIf="hasActiveFilters()" 
              class="active-filters">
              <saf-badge 
                *ngIf="searchQuery" 
                variant="primary" 
                class="filter-badge">
                Search: {{ searchQuery }}
              </saf-badge>
              <saf-badge 
                *ngIf="filterValue" 
                variant="secondary" 
                class="filter-badge">
                Dept: {{ filterValue }}
              </saf-badge>
              <saf-badge 
                *ngIf="quickSearch" 
                variant="success" 
                class="filter-badge">
                Quick: {{ quickSearch }}
              </saf-badge>
            </div>
          </div>

          <div class="results-list">
            <div 
              *ngFor="let item of filteredData" 
              class="result-item">
              <div class="result-info">
                <h4>{{ item.name }}</h4>
                <p>{{ item.email }}</p>
              </div>
              <saf-badge variant="outline">
                {{ item.department }}
              </saf-badge>
            </div>

            <div 
              *ngIf="filteredData.length === 0" 
              class="no-results">
              <saf-icon name="search" size="large"></saf-icon>
              <p>No employees found matching your criteria</p>
            </div>
          </div>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class SearchFilterInputComponent {
  searchQuery = '';
  filterValue = '';
  quickSearch = '';

  mockData: Employee[] = [
    { id: 1, name: 'John Doe', email: 'john@example.com', department: 'Engineering' },
    { id: 2, name: 'Jane Smith', email: 'jane@example.com', department: 'Marketing' },
    { id: 3, name: 'Bob Johnson', email: 'bob@example.com', department: 'Sales' },
    { id: 4, name: 'Alice Wilson', email: 'alice@example.com', department: 'Engineering' },
    { id: 5, name: 'Charlie Brown', email: 'charlie@example.com', department: 'HR' }
  ];

  filteredData: Employee[] = [...this.mockData];

  updateResults() {
    this.filteredData = this.mockData.filter(item => {
      const matchesSearch = !this.searchQuery || 
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        item.email.toLowerCase().includes(this.searchQuery.toLowerCase());
      
      const matchesFilter = !this.filterValue ||
        item.department.toLowerCase().includes(this.filterValue.toLowerCase());
      
      const matchesQuick = !this.quickSearch ||
        item.name.toLowerCase().includes(this.quickSearch.toLowerCase());
      
      return matchesSearch && matchesFilter && matchesQuick;
    });
  }

  handleClearAll() {
    this.searchQuery = '';
    this.filterValue = '';
    this.quickSearch = '';
    this.updateResults();
  }

  handleKeyDown(event: KeyboardEvent, action: string) {
    if (event.key === 'Enter') {
      console.log(`${action} initiated`);
    }
  }

  hasActiveFilters(): boolean {
    return !!(this.searchQuery || this.filterValue || this.quickSearch);
  }
}
```

## Best Practices

1. **Label and Placeholder Design**
   - Use clear, descriptive labels for all inputs
   - Write helpful placeholder text that guides user input
   - Provide context through descriptions and helper text

2. **Validation Strategy**
   - Implement real-time validation for immediate feedback
   - Use appropriate validation timing (onChange vs onBlur)
   - Provide clear, actionable error messages

3. **Input Types and Formatting**
   - Use semantic input types for better UX and validation
   - Implement input masking for structured data
   - Format values appropriately on blur

4. **Performance Optimization**
   - Use debouncing for search and filter inputs
   - Implement efficient validation logic
   - Optimize re-rendering with proper state management

5. **Accessibility**
   - Associate labels with inputs properly
   - Provide meaningful error announcements
   - Support keyboard navigation and screen readers

## Accessibility Considerations

1. **ARIA Support**
   - Use `aria-describedby` for error and helper text
   - Implement `aria-invalid` for error states
   - Provide `aria-required` for required fields

2. **Keyboard Navigation**
   - Support Tab navigation through inputs
   - Enable appropriate keyboard interactions
   - Provide keyboard shortcuts where applicable

3. **Screen Reader Compatibility**
   - Announce validation errors and state changes
   - Provide meaningful labels and descriptions
   - Use semantic markup for form structure

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all states
   - Provide clear focus indicators
   - Support high contrast and reduced motion preferences

## Related Components

- **SafTextarea**: Multi-line text input alternative
- **SafSelect**: Dropdown selection for predefined options
- **SafAutocomplete**: Text input with suggestions
- **SafLabel**: Standalone labels for custom layouts
- **SafButton**: Form submission and actions

## Notes

- Text input automatically handles common input scenarios and edge cases
- Custom CSS variables available for comprehensive theming
- Built-in support for form validation and integration libraries
- Optimized for mobile touch interactions and responsive design
- Compatible with popular form libraries and state management solutions
- Supports both controlled and uncontrolled usage patterns
- Performance optimized with efficient validation and formatting
