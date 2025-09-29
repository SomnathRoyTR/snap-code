# SafTextField

A versatile text input component that supports various input types, validation states, and accessibility features. SafTextField provides comprehensive form field functionality with built-in validation, labeling, and user guidance.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `type` | `'text' \| 'email' \| 'password' \| 'tel' \| 'url'` | `'text'` | The type of text input |
| `value` | `string` | `''` | The current value of the text field |
| `label` | `string` | - | Text that describes the input |
| `placeholder` | `string` | - | Placeholder text displayed when field is empty |
| `disabled` | `boolean` | `false` | Prevents user interaction with the component |
| `readonly` | `boolean` | `false` | Makes the input immutable by user interaction |
| `required` | `boolean` | `false` | Indicates that the field must be filled out |
| `autofocus` | `boolean` | `false` | Determines if element should receive focus on page load |
| `autocomplete` | `string` | - | Controls browser autofill behavior |
| `density` | `'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |
| `invalid` | `boolean` | `false` | Indicates the entered value does not conform to expected format |
| `isSuccess` | `boolean` | - | Specifies that the control is valid and should display success state |
| `validationMessage` | `string` | - | The message displayed when the control is valid or invalid |
| `instructionalText` | `string` | - | Additional guidance text for the input |
| `optionalText` | `string` | - | Additional text to indicate if field is optional (e.g., "(Optional)") |
| `requiredText` | `string` | `'*'` | Additional character to add when field is required |
| `maxlength` | `number` | - | Maximum number of characters a user can enter |
| `minlength` | `number` | - | Minimum number of characters a user can enter |
| `pattern` | `string` | - | Regular expression that the value must match to pass validation |
| `size` | `number` | - | Sets the width of the element to specified number of characters |
| `spellcheck` | `boolean` | - | Controls whether to enable spell checking |
| `list` | `string` | - | Associates a datalist element by ID |
| `enterKeyHint` | `'enter' \| 'done' \| 'go' \| 'next' \| 'previous' \| 'search' \| 'send'` | - | Defines action label for enter key on virtual keyboards |
| `a11yAriaDescription` | `string` | - | Description for screen readers only |
| `successAriaLabel` | `string` | `'Success'` | Labels the success icon for screen readers |
| `errorAriaLabel` | `string` | `'Error'` | Labels the error icon for screen readers |

### Examples

#### Basic Usage
```jsx
import { SafTextField } from '@saffron/core-components/react';

function BasicTextField() {
  const [value, setValue] = useState('');
  
  return (
    <SafTextField
      label="First Name"
      value={value}
      onInput={(e) => setValue(e.target.value)}
      placeholder="Enter your first name"
    />
  );
}
```

#### Advanced Usage
```jsx
import { SafTextField, SafIcon } from '@saffron/core-components/react';
import { useState } from 'react';

// Different input types
function InputTypes() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    phone: '',
    website: '',
    password: ''
  });
  
  const handleInputChange = (field) => (e) => {
    setFormData(prev => ({
      ...prev,
      [field]: e.target.value
    }));
  };
  
  return (
    <div className="form-grid">
      <SafTextField
        type="text"
        label="Full Name"
        value={formData.name}
        onInput={handleInputChange('name')}
        required={true}
        requiredText=" *"
        instructionalText="Enter your full legal name"
      />
      
      <SafTextField
        type="email"
        label="Email Address"
        value={formData.email}
        onInput={handleInputChange('email')}
        required={true}
        autocomplete="email"
        instructionalText="We'll use this to send you updates"
      />
      
      <SafTextField
        type="tel"
        label="Phone Number"
        value={formData.phone}
        onInput={handleInputChange('phone')}
        optionalText=" (Optional)"
        pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
        placeholder="123-456-7890"
      />
      
      <SafTextField
        type="url"
        label="Website"
        value={formData.website}
        onInput={handleInputChange('website')}
        placeholder="https://example.com"
        optionalText=" (Optional)"
      />
      
      <SafTextField
        type="password"
        label="Password"
        value={formData.password}
        onInput={handleInputChange('password')}
        required={true}
        minlength={8}
        instructionalText="Must be at least 8 characters"
      />
    </div>
  );
}

// Validation states
function ValidationStates() {
  const [email, setEmail] = useState('');
  const [validationState, setValidationState] = useState({
    invalid: false,
    isSuccess: false,
    validationMessage: ''
  });
  
  const validateEmail = (value) => {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    
    if (!value) {
      setValidationState({
        invalid: false,
        isSuccess: false,
        validationMessage: ''
      });
    } else if (!emailRegex.test(value)) {
      setValidationState({
        invalid: true,
        isSuccess: false,
        validationMessage: 'Please enter a valid email address'
      });
    } else {
      setValidationState({
        invalid: false,
        isSuccess: true,
        validationMessage: 'Email address is valid'
      });
    }
  };
  
  const handleEmailChange = (e) => {
    const value = e.target.value;
    setEmail(value);
    validateEmail(value);
  };
  
  return (
    <SafTextField
      type="email"
      label="Email Address"
      value={email}
      onInput={handleEmailChange}
      onBlur={handleEmailChange}
      invalid={validationState.invalid}
      isSuccess={validationState.isSuccess}
      validationMessage={validationState.validationMessage}
      instructionalText="Enter your email address for account verification"
    />
  );
}

// Text field with icons
function TextFieldWithIcons() {
  const [searchTerm, setSearchTerm] = useState('');
  const [showPassword, setShowPassword] = useState(false);
  const [password, setPassword] = useState('');
  
  return (
    <div>
      {/* Search field with icon */}
      <SafTextField
        type="text"
        label="Search"
        value={searchTerm}
        onInput={(e) => setSearchTerm(e.target.value)}
        placeholder="Search for items..."
        enterKeyHint="search"
      >
        <SafIcon slot="start" iconName="search" />
      </SafTextField>
      
      {/* Password field with show/hide toggle */}
      <SafTextField
        type={showPassword ? "text" : "password"}
        label="Password"
        value={password}
        onInput={(e) => setPassword(e.target.value)}
        placeholder="Enter password"
      >
        <button
          slot="end"
          type="button"
          onClick={() => setShowPassword(!showPassword)}
          aria-label={showPassword ? "Hide password" : "Show password"}
        >
          <SafIcon iconName={showPassword ? "eye-off" : "eye"} />
        </button>
      </SafTextField>
    </div>
  );
}

// Different densities
function DensityVariations() {
  const [value, setValue] = useState('');
  
  return (
    <div className="density-examples">
      <SafTextField
        density="compact"
        label="Compact Field"
        value={value}
        onInput={(e) => setValue(e.target.value)}
      />
      
      <SafTextField
        density="standard"
        label="Standard Field"
        value={value}
        onInput={(e) => setValue(e.target.value)}
      />
      
      <SafTextField
        density="relaxed"
        label="Relaxed Field"
        value={value}
        onInput={(e) => setValue(e.target.value)}
      />
    </div>
  );
}

// Datalist integration
function DatalistExample() {
  const [browser, setBrowser] = useState('');
  
  return (
    <div>
      <SafTextField
        label="Preferred Browser"
        value={browser}
        onInput={(e) => setBrowser(e.target.value)}
        list="browsers"
        instructionalText="Type to see suggestions or select from the list"
      />
      
      <datalist id="browsers" slot="datalist">
        <option value="Chrome" />
        <option value="Firefox" />
        <option value="Safari" />
        <option value="Edge" />
        <option value="Opera" />
      </datalist>
    </div>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `type` | `'text' \| 'email' \| 'password' \| 'tel' \| 'url'` | `'text'` | The type of text input |
| `value` | `string` | `''` | The current value of the text field |
| `label` | `string` | - | Text that describes the input |
| `placeholder` | `string` | - | Placeholder text displayed when field is empty |
| `disabled` | `boolean` | `false` | Prevents user interaction with the component |
| `readonly` | `boolean` | `false` | Makes the input immutable by user interaction |
| `required` | `boolean` | `false` | Indicates that the field must be filled out |
| `autofocus` | `boolean` | `false` | Determines if element should receive focus on page load |
| `autocomplete` | `string` | - | Controls browser autofill behavior |
| `density` | `'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |
| `invalid` | `boolean` | `false` | Indicates the entered value does not conform to expected format |
| `is-success` | `boolean` | - | Specifies that the control is valid and should display success state |
| `validation-message` | `string` | - | The message displayed when the control is valid or invalid |
| `instructional-text` | `string` | - | Additional guidance text for the input |
| `optional-text` | `string` | - | Additional text to indicate if field is optional |
| `required-text` | `string` | `'*'` | Additional character to add when field is required |
| `maxlength` | `number` | - | Maximum number of characters a user can enter |
| `minlength` | `number` | - | Minimum number of characters a user can enter |
| `pattern` | `string` | - | Regular expression that the value must match to pass validation |
| `size` | `number` | - | Sets the width of the element to specified number of characters |
| `spellcheck` | `boolean` | - | Controls whether to enable spell checking |
| `list` | `string` | - | Associates a datalist element by ID |
| `enterkeyhint` | `'enter' \| 'done' \| 'go' \| 'next' \| 'previous' \| 'search' \| 'send'` | - | Defines action label for enter key on virtual keyboards |
| `a11y-aria-description` | `string` | - | Description for screen readers only |
| `success-aria-label` | `string` | `'Success'` | Labels the success icon for screen readers |
| `error-aria-label` | `string` | `'Error'` | Labels the error icon for screen readers |

### Examples

#### Basic Usage
```html
<saf-text-field
  label="First Name"
  [(value)]="firstName"
  placeholder="Enter your first name">
</saf-text-field>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-text-field',
  template: `
    <saf-text-field
      label="First Name"
      [(value)]="firstName"
      placeholder="Enter your first name"
      (input)="onInputChange($event)">
    </saf-text-field>
  `
})
export class BasicTextFieldComponent {
  firstName = '';
  
  onInputChange(event: Event): void {
    const target = event.target as HTMLInputElement;
    console.log('Input value:', target.value);
  }
}
```

#### Advanced Usage
```html
<!-- Different input types -->
<div class="form-grid">
  <saf-text-field
    type="text"
    label="Full Name"
    [(value)]="formData.name"
    [required]="true"
    required-text=" *"
    instructional-text="Enter your full legal name">
  </saf-text-field>
  
  <saf-text-field
    type="email"
    label="Email Address"
    [(value)]="formData.email"
    [required]="true"
    autocomplete="email"
    instructional-text="We'll use this to send you updates">
  </saf-text-field>
  
  <saf-text-field
    type="tel"
    label="Phone Number"
    [(value)]="formData.phone"
    optional-text=" (Optional)"
    pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
    placeholder="123-456-7890">
  </saf-text-field>
  
  <saf-text-field
    type="url"
    label="Website"
    [(value)]="formData.website"
    placeholder="https://example.com"
    optional-text=" (Optional)">
  </saf-text-field>
  
  <saf-text-field
    type="password"
    label="Password"
    [(value)]="formData.password"
    [required]="true"
    [minlength]="8"
    instructional-text="Must be at least 8 characters">
  </saf-text-field>
</div>

<!-- Validation states -->
<saf-text-field
  type="email"
  label="Email Address"
  [(value)]="email"
  [invalid]="validationState.invalid"
  [is-success]="validationState.isSuccess"
  [validation-message]="validationState.validationMessage"
  instructional-text="Enter your email address for account verification"
  (input)="validateEmail($event)"
  (blur)="validateEmail($event)">
</saf-text-field>

<!-- Text field with icons -->
<div>
  <!-- Search field with icon -->
  <saf-text-field
    type="text"
    label="Search"
    [(value)]="searchTerm"
    placeholder="Search for items..."
    enterkeyhint="search">
    <saf-icon slot="start" icon-name="search"></saf-icon>
  </saf-text-field>
  
  <!-- Password field with show/hide toggle -->
  <saf-text-field
    [type]="showPassword ? 'text' : 'password'"
    label="Password"
    [(value)]="password"
    placeholder="Enter password">
    <button
      slot="end"
      type="button"
      (click)="togglePasswordVisibility()"
      [attr.aria-label]="showPassword ? 'Hide password' : 'Show password'">
      <saf-icon [icon-name]="showPassword ? 'eye-off' : 'eye'"></saf-icon>
    </button>
  </saf-text-field>
</div>

<!-- Different densities -->
<div class="density-examples">
  <saf-text-field
    density="compact"
    label="Compact Field"
    [(value)]="value">
  </saf-text-field>
  
  <saf-text-field
    density="standard"
    label="Standard Field"
    [(value)]="value">
  </saf-text-field>
  
  <saf-text-field
    density="relaxed"
    label="Relaxed Field"
    [(value)]="value">
  </saf-text-field>
</div>

<!-- Datalist integration -->
<saf-text-field
  label="Preferred Browser"
  [(value)]="browser"
  list="browsers"
  instructional-text="Type to see suggestions or select from the list">
  <datalist id="browsers" slot="datalist">
    <option value="Chrome"></option>
    <option value="Firefox"></option>
    <option value="Safari"></option>
    <option value="Edge"></option>
    <option value="Opera"></option>
  </datalist>
</saf-text-field>
```

```typescript
import { Component } from '@angular/core';

interface FormData {
  name: string;
  email: string;
  phone: string;
  website: string;
  password: string;
}

interface ValidationState {
  invalid: boolean;
  isSuccess: boolean;
  validationMessage: string;
}

@Component({
  selector: 'app-advanced-text-field',
  template: `
    <!-- Template content shown above -->
  `
})
export class AdvancedTextFieldComponent {
  formData: FormData = {
    name: '',
    email: '',
    phone: '',
    website: '',
    password: ''
  };
  
  email = '';
  validationState: ValidationState = {
    invalid: false,
    isSuccess: false,
    validationMessage: ''
  };
  
  searchTerm = '';
  showPassword = false;
  password = '';
  value = '';
  browser = '';
  
  validateEmail(event: Event): void {
    const target = event.target as HTMLInputElement;
    const value = target.value;
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    
    if (!value) {
      this.validationState = {
        invalid: false,
        isSuccess: false,
        validationMessage: ''
      };
    } else if (!emailRegex.test(value)) {
      this.validationState = {
        invalid: true,
        isSuccess: false,
        validationMessage: 'Please enter a valid email address'
      };
    } else {
      this.validationState = {
        invalid: false,
        isSuccess: true,
        validationMessage: 'Email address is valid'
      };
    }
  }
  
  togglePasswordVisibility(): void {
    this.showPassword = !this.showPassword;
  }
}
```

### Best Practices

1. **Label and guidance:**
   - Always provide meaningful labels that describe the expected input
   - Use `instructionalText` to provide additional guidance when needed
   - Use `optionalText` and `requiredText` to clearly indicate field requirements

2. **Validation and feedback:**
   - Provide real-time validation feedback for better user experience
   - Use `validationMessage` to explain validation errors clearly
   - Consider using `isSuccess` to confirm valid input

3. **Accessibility:**
   - Use appropriate `type` attributes for better mobile experience
   - Provide `a11yAriaDescription` for additional screen reader context
   - Ensure proper labeling for icon buttons in slots

4. **Input types and constraints:**
   - Choose appropriate `type` for the expected data (email, tel, url)
   - Use `pattern`, `minlength`, and `maxlength` for client-side validation
   - Set appropriate `autocomplete` values for better user experience

5. **Mobile considerations:**
   - Use `enterKeyHint` to customize virtual keyboard behavior
   - Test touch interactions and ensure adequate touch targets
   - Consider density adjustments for mobile interfaces

### Notes

- **Form integration:** SafTextField integrates seamlessly with HTML forms and supports all standard form validation attributes.
- **Password handling:** For password fields, the component automatically handles security considerations and doesn't expose the actual value.
- **Datalist support:** Use the datalist slot to provide autocomplete suggestions that work across different browsers.
- **Validation announcements:** The component automatically announces validation messages to screen readers for better accessibility.
- **Value binding:** The component supports both controlled and uncontrolled patterns, adapting to your framework's data binding approach.
