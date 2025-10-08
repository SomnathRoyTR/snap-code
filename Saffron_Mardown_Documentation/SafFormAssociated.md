# SafFormAssociated

A foundational mixin and base class that provides Custom Element Form Association capabilities to Saffron Design System components. SafFormAssociated enables custom elements to participate in HTML forms with full validation, submission, and accessibility support, bridging the gap between custom components and native form controls.

## Overview

SafFormAssociated is not a standalone component but a mixin class that other form components extend to gain form association capabilities. It provides both modern ElementInternals API support and fallback proxy element support for older browsers, ensuring consistent form behavior across all platforms.

## React

### API (When Extended by Components)

When a component extends SafFormAssociated, it gains access to the following properties and methods:

| Property | Type | Description |
|----------|------|-------------|
| `name` | `string` | Name of the form control, submitted as part of name/value pair |
| `value` | `string` | Current value of the form control |
| `initialValue` | `string` | The initial value of the control when the form loads |
| `currentValue` | `string` | The current value, potentially different from the initial value |
| `disabled` | `boolean` | Prevents user interaction with the component |
| `required` | `boolean` | Indicates if a value is required for form submission |
| `checked` | `boolean` | For checkable elements, indicates checked state |
| `dirtyValue` | `boolean` | Indicates if the value has been modified from initial state |
| `dirtyChecked` | `boolean` | For checkable elements, indicates if checked state has been modified |
| `validity` | `ValidityState` | Browser validation state object |
| `validationMessage` | `string` | Localized validation message |
| `willValidate` | `boolean` | Whether element will be validated on form submission |
| `form` | `HTMLFormElement \| null` | Reference to the associated form element |
| `labels` | `ReadonlyArray<Node>` | Array of associated label elements |

### Methods

| Method | Parameters | Description |
|--------|------------|-------------|
| `checkValidity()` | - | Returns true if element has no validity problems |
| `reportValidity()` | - | Validates and reports validity to user if invalid |
| `setFormValue()` | `value: string \| FormData \| null, state?: string \| FormData \| null` | Sets the form submission value |
| `setValidity()` | `flags: ValidityStateFlags, message?: string, anchor?: HTMLElement` | Sets custom validity state |
| `validate()` | `anchor?: HTMLElement` | Validates the element and updates validity state |

### Examples

#### Custom Form-Associated Component
```jsx
import React, { useEffect, useRef, useState } from 'react';
import { SafFormAssociated } from '@saffron/core-components/react';

// Example of how a component would extend FormAssociated
function CustomInput({ name, value, onChange, required, disabled, ...props }) {
  const elementRef = useRef(null);
  const [internalValue, setInternalValue] = useState(value || '');
  const [isValid, setIsValid] = useState(true);

  // Simulate form association behavior
  useEffect(() => {
    if (elementRef.current) {
      // The actual component would use ElementInternals or proxy
      const element = elementRef.current;
      
      // Set form value
      if (element.setFormValue) {
        element.setFormValue(internalValue);
      }
      
      // Validate
      const isRequired = required && !internalValue;
      setIsValid(!isRequired);
      
      if (element.setValidity) {
        element.setValidity(
          isRequired ? { valueMissing: true } : {},
          isRequired ? 'This field is required' : ''
        );
      }
    }
  }, [internalValue, required]);

  const handleChange = (e) => {
    const newValue = e.target.value;
    setInternalValue(newValue);
    onChange?.(e);
  };

  return (
    <input
      ref={elementRef}
      name={name}
      value={internalValue}
      onChange={handleChange}
      required={required}
      disabled={disabled}
      aria-invalid={!isValid}
      {...props}
    />
  );
}
```

#### Form with Form-Associated Components
```jsx
import { SafTextField, SafTextArea, SafCheckbox, SafButton } from '@saffron/core-components/react';

function FormWithAssociatedComponents() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: '',
    newsletter: false
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    
    // Get form data using FormData API
    const formDataObj = new FormData(e.target);
    const data = Object.fromEntries(formDataObj.entries());
    
    console.log('Form submission data:', data);
    
    // Validate all form-associated elements
    const formElements = e.target.querySelectorAll('[name]');
    let isFormValid = true;
    
    formElements.forEach(element => {
      if (element.checkValidity && !element.checkValidity()) {
        isFormValid = false;
        element.reportValidity();
      }
    });
    
    if (isFormValid) {
      console.log('Form is valid, submitting:', data);
      // Handle form submission
    }
  };

  const handleReset = (e) => {
    // Form-associated elements will automatically reset to initial values
    setFormData({
      name: '',
      email: '',
      message: '',
      newsletter: false
    });
  };

  return (
    <form onSubmit={handleSubmit} onReset={handleReset}>
      <SafTextField
        name="name"
        label="Full Name"
        value={formData.name}
        required
        onChange={(e) => setFormData(prev => ({ ...prev, name: e.target.value }))}
      />
      
      <SafTextField
        name="email"
        label="Email Address"
        type="email"
        value={formData.email}
        required
        onChange={(e) => setFormData(prev => ({ ...prev, email: e.target.value }))}
      />
      
      <SafTextArea
        name="message"
        label="Message"
        value={formData.message}
        required
        minLength={10}
        onChange={(e) => setFormData(prev => ({ ...prev, message: e.target.value }))}
      />
      
      <SafCheckbox
        name="newsletter"
        checked={formData.newsletter}
        onChange={(e) => setFormData(prev => ({ ...prev, newsletter: e.target.checked }))}>
        Subscribe to newsletter
      </SafCheckbox>
      
      <div style={{ marginTop: '16px' }}>
        <SafButton type="submit" appearance="primary">
          Submit
        </SafButton>
        <SafButton type="reset" appearance="secondary" style={{ marginLeft: '8px' }}>
          Reset
        </SafButton>
      </div>
    </form>
  );
}
```

#### Custom Validation with Form Association
```jsx
import { SafTextField, SafButton } from '@saffron/core-components/react';

function AdvancedValidationForm() {
  const [errors, setErrors] = useState({});

  const validateField = (name, value, element) => {
    let errorMessage = '';
    let validityFlags = {};

    switch (name) {
      case 'username':
        if (!value) {
          errorMessage = 'Username is required';
          validityFlags.valueMissing = true;
        } else if (value.length < 3) {
          errorMessage = 'Username must be at least 3 characters';
          validityFlags.tooShort = true;
        } else if (!/^[a-zA-Z0-9_]+$/.test(value)) {
          errorMessage = 'Username can only contain letters, numbers, and underscores';
          validityFlags.patternMismatch = true;
        }
        break;
        
      case 'password':
        if (!value) {
          errorMessage = 'Password is required';
          validityFlags.valueMissing = true;
        } else if (value.length < 8) {
          errorMessage = 'Password must be at least 8 characters';
          validityFlags.tooShort = true;
        } else if (!/(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/.test(value)) {
          errorMessage = 'Password must contain uppercase, lowercase, and number';
          validityFlags.patternMismatch = true;
        }
        break;
    }

    // Set custom validity using form association API
    if (element && element.setValidity) {
      element.setValidity(validityFlags, errorMessage);
    }

    return errorMessage;
  };

  const handleFieldChange = (name, value, element) => {
    const error = validateField(name, value, element);
    setErrors(prev => ({ ...prev, [name]: error }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    
    // Check validity of all form-associated elements
    const formElements = Array.from(e.target.elements);
    let hasErrors = false;
    
    formElements.forEach(element => {
      if (element.name && element.checkValidity) {
        if (!element.checkValidity()) {
          hasErrors = true;
          element.reportValidity();
        }
      }
    });
    
    if (!hasErrors) {
      const formData = new FormData(e.target);
      console.log('Valid form submission:', Object.fromEntries(formData));
    }
  };

  return (
    <form onSubmit={handleSubmit} noValidate>
      <SafTextField
        name="username"
        label="Username"
        required
        minLength={3}
        pattern="^[a-zA-Z0-9_]+$"
        validationMessage={errors.username}
        invalid={!!errors.username}
        onChange={(e) => handleFieldChange('username', e.target.value, e.target)}
      />
      
      <SafTextField
        name="password"
        label="Password"
        type="password"
        required
        minLength={8}
        validationMessage={errors.password}
        invalid={!!errors.password}
        onChange={(e) => handleFieldChange('password', e.target.value, e.target)}
      />
      
      <SafButton type="submit" appearance="primary">
        Create Account
      </SafButton>
    </form>
  );
}
```

## Angular

### Examples

#### Form with Form-Associated Components
```html
<form (ngSubmit)="handleSubmit($event)" (reset)="handleReset()" #userForm="ngForm">
  <saf-text-field
    name="name"
    label="Full Name"
    [(ngModel)]="formData.name"
    required
    #nameField="ngModel">
  </saf-text-field>
  <div *ngIf="nameField.invalid && nameField.touched" class="error-message">
    Name is required
  </div>
  
  <saf-text-field
    name="email"
    label="Email Address"
    type="email"
    [(ngModel)]="formData.email"
    required
    email
    #emailField="ngModel">
  </saf-text-field>
  <div *ngIf="emailField.invalid && emailField.touched" class="error-message">
    <span *ngIf="emailField.errors?.['required']">Email is required</span>
    <span *ngIf="emailField.errors?.['email']">Please enter a valid email</span>
  </div>
  
  <saf-text-area
    name="message"
    label="Message"
    [(ngModel)]="formData.message"
    required
    minlength="10"
    #messageField="ngModel">
  </saf-text-area>
  <div *ngIf="messageField.invalid && messageField.touched" class="error-message">
    <span *ngIf="messageField.errors?.['required']">Message is required</span>
    <span *ngIf="messageField.errors?.['minlength']">Message must be at least 10 characters</span>
  </div>
  
  <saf-checkbox
    name="newsletter"
    [(ngModel)]="formData.newsletter">
    Subscribe to newsletter
  </saf-checkbox>
  
  <div class="form-actions">
    <saf-button 
      type="submit" 
      appearance="primary"
      [disabled]="!userForm.valid">
      Submit
    </saf-button>
    <saf-button type="reset" appearance="secondary">
      Reset
    </saf-button>
  </div>
</form>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-form-with-associated-components',
  templateUrl: './form-with-associated-components.component.html',
  styleUrls: ['./form-with-associated-components.component.scss']
})
export class FormWithAssociatedComponentsComponent {
  formData = {
    name: '',
    email: '',
    message: '',
    newsletter: false
  };

  handleSubmit(event: Event) {
    event.preventDefault();
    
    const form = event.target as HTMLFormElement;
    const formData = new FormData(form);
    const data = Object.fromEntries(formData.entries());
    
    console.log('Form submission data:', data);
    
    // Validate using form association API
    const formElements = Array.from(form.elements) as HTMLElement[];
    let isFormValid = true;
    
    formElements.forEach(element => {
      if ('checkValidity' in element && typeof element.checkValidity === 'function') {
        if (!element.checkValidity()) {
          isFormValid = false;
          if ('reportValidity' in element && typeof element.reportValidity === 'function') {
            element.reportValidity();
          }
        }
      }
    });
    
    if (isFormValid) {
      console.log('Form is valid, submitting:', data);
      // Handle form submission
    }
  }

  handleReset() {
    this.formData = {
      name: '',
      email: '',
      message: '',
      newsletter: false
    };
  }
}
```

#### Custom Validation Service
```typescript
import { Injectable } from '@angular/core';

interface ValidationRule {
  required?: boolean;
  minLength?: number;
  maxLength?: number;
  pattern?: RegExp;
  email?: boolean;
  custom?: (value: string) => string | null;
}

@Injectable({
  providedIn: 'root'
})
export class FormAssociationService {
  
  validateField(element: HTMLElement & { setValidity?: Function }, value: string, rules: ValidationRule): string | null {
    let errorMessage: string | null = null;
    const validityFlags: any = {};

    // Required validation
    if (rules.required && !value) {
      errorMessage = 'This field is required';
      validityFlags.valueMissing = true;
    }
    
    // Length validation
    else if (rules.minLength && value.length < rules.minLength) {
      errorMessage = `Minimum length is ${rules.minLength} characters`;
      validityFlags.tooShort = true;
    }
    else if (rules.maxLength && value.length > rules.maxLength) {
      errorMessage = `Maximum length is ${rules.maxLength} characters`;
      validityFlags.tooLong = true;
    }
    
    // Pattern validation
    else if (rules.pattern && !rules.pattern.test(value)) {
      errorMessage = 'Invalid format';
      validityFlags.patternMismatch = true;
    }
    
    // Email validation
    else if (rules.email && value && !this.isValidEmail(value)) {
      errorMessage = 'Please enter a valid email address';
      validityFlags.typeMismatch = true;
    }
    
    // Custom validation
    else if (rules.custom) {
      errorMessage = rules.custom(value);
      if (errorMessage) {
        validityFlags.customError = true;
      }
    }

    // Set validity using form association API
    if (element.setValidity) {
      element.setValidity(validityFlags, errorMessage || '');
    }

    return errorMessage;
  }

  private isValidEmail(email: string): boolean {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }

  getFormData(form: HTMLFormElement): Record<string, any> {
    const formData = new FormData(form);
    return Object.fromEntries(formData.entries());
  }

  validateForm(form: HTMLFormElement): boolean {
    const elements = Array.from(form.elements) as HTMLElement[];
    let isValid = true;

    elements.forEach(element => {
      if ('checkValidity' in element && typeof element.checkValidity === 'function') {
        if (!element.checkValidity()) {
          isValid = false;
        }
      }
    });

    return isValid;
  }
}
```

## Best Practices

- **Use for form controls**: Extend SafFormAssociated for any component that needs to participate in HTML forms.
- **Implement proper validation**: Use the `setValidity()` method to provide custom validation messages and states.
- **Handle form lifecycle**: Implement `formResetCallback()` and `formDisabledCallback()` when extending the mixin.
- **Provide accessible labels**: Ensure form-associated elements have proper labels for screen readers.
- **Test across browsers**: The mixin provides fallbacks for older browsers, but test thoroughly.
- **Use semantic HTML**: The proxy element approach maintains semantic form behavior.
- **Handle dirty state**: Track when values change from initial state for better UX.
- **Progressive enhancement**: Components work as regular form elements even without JavaScript.

## Notes

- SafFormAssociated provides both modern ElementInternals API support and legacy proxy element fallback.
- The mixin automatically handles form submission, validation, and reset behaviors.
- Components extending this mixin become first-class citizens in HTML forms.
- The implementation includes TypeScript definitions for ElementInternals APIs.
- Form association enables custom elements to work with form validation APIs.
- The mixin supports both regular form controls and checkable form controls.
- Accessibility features are built-in, including proper label association and validation feedback.
- The component bridges the gap between custom elements and native form controls seamlessly.
