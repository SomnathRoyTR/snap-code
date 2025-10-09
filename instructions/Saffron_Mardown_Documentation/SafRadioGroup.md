# SafRadioGroup

The SafRadioGroup component provides a container for organizing SafRadio buttons into a cohesive group with shared state management. It ensures proper accessibility, keyboard navigation, and mutual exclusivity between radio options.

## React

### API

| Prop           | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `name`         | `string`                | `undefined` | Name attribute for the radio group            |
| `value`        | `string`                | `undefined` | Currently selected radio value                 |
| `defaultValue` | `string`                | `undefined` | Default selected radio value (uncontrolled)   |
| `orientation`  | `"horizontal" \| "vertical"` | `"vertical"` | Layout orientation of radio buttons      |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Size of radio buttons                    |
| `disabled`     | `boolean`               | `false`     | Whether the entire group is disabled          |
| `required`     | `boolean`               | `false`     | Whether selection is required                  |
| `readOnly`     | `boolean`               | `false`     | Whether the group is read-only                 |
| `legend`       | `string`                | `undefined` | Legend text for the fieldset                   |
| `description`  | `string`                | `undefined` | Description text below the legend              |
| `errorMessage` | `string`                | `undefined` | Error message to display                       |
| `className`    | `string`                | `undefined` | Additional CSS class names                     |
| `onChange`     | `(value: string, event: ChangeEvent) => void` | `undefined` | Handler for value changes |
| `onFocus`      | `(event: FocusEvent) => void` | `undefined` | Handler for group focus              |
| `onBlur`       | `(event: FocusEvent) => void` | `undefined` | Handler for group blur               |
| `children`     | `ReactNode`             | `undefined` | SafRadio components                            |

### Examples

#### Basic Usage

```jsx
import { SafRadioGroup, SafRadio } from '@saffron/core-components';
import { useState } from 'react';

function BasicRadioGroup() {
  const [selectedValue, setSelectedValue] = useState('');

  const handleChange = (value, event) => {
    setSelectedValue(value);
    console.log('Selected:', value);
  };

  return (
    <SafRadioGroup
      name="basic-options"
      value={selectedValue}
      onChange={handleChange}
      legend="Choose an option"
    >
      <SafRadio value="option1" label="Option 1" />
      <SafRadio value="option2" label="Option 2" />
      <SafRadio value="option3" label="Option 3" />
    </SafRadioGroup>
  );
}
```

#### Horizontal Layout with Description

```jsx
import { SafRadioGroup, SafRadio } from '@saffron/core-components';
import { useState } from 'react';

function HorizontalRadioGroup() {
  const [preference, setPreference] = useState('email');

  return (
    <SafRadioGroup
      name="notification-preference"
      value={preference}
      onChange={(value) => setPreference(value)}
      orientation="horizontal"
      legend="Notification Preference"
      description="Choose how you'd like to receive notifications"
      size="large"
    >
      <SafRadio 
        value="email" 
        label="Email" 
        description="Receive notifications via email"
      />
      <SafRadio 
        value="sms" 
        label="SMS" 
        description="Receive notifications via text message"
      />
      <SafRadio 
        value="push" 
        label="Push Notifications" 
        description="Receive browser push notifications"
      />
    </SafRadioGroup>
  );
}
```

#### With Validation and Error Handling

```jsx
import { SafRadioGroup, SafRadio } from '@saffron/core-components';
import { useState } from 'react';

function ValidatedRadioGroup() {
  const [selectedPlan, setSelectedPlan] = useState('');
  const [error, setError] = useState('');
  const [touched, setTouched] = useState(false);

  const plans = [
    { value: 'basic', label: 'Basic Plan', price: '$9/month' },
    { value: 'professional', label: 'Professional Plan', price: '$29/month' },
    { value: 'enterprise', label: 'Enterprise Plan', price: '$99/month' }
  ];

  const handleChange = (value) => {
    setSelectedPlan(value);
    if (error && value) {
      setError('');
    }
  };

  const handleBlur = () => {
    setTouched(true);
    if (!selectedPlan) {
      setError('Please select a subscription plan');
    }
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    if (!selectedPlan) {
      setError('Please select a subscription plan');
      setTouched(true);
      return;
    }
    console.log('Selected plan:', selectedPlan);
  };

  return (
    <form onSubmit={handleSubmit}>
      <SafRadioGroup
        name="subscription-plan"
        value={selectedPlan}
        onChange={handleChange}
        onBlur={handleBlur}
        legend="Subscription Plan"
        description="Select your preferred subscription plan"
        required={true}
        errorMessage={touched ? error : ''}
        className={error ? 'has-error' : ''}
      >
        {plans.map(plan => (
          <SafRadio
            key={plan.value}
            value={plan.value}
            label={plan.label}
            description={plan.price}
          />
        ))}
      </SafRadioGroup>
      
      <button type="submit" style={{ marginTop: '16px' }}>
        Continue
      </button>
    </form>
  );
}
```

#### Disabled and Read-Only States

```jsx
import { SafRadioGroup, SafRadio } from '@saffron/core-components';
import { useState } from 'react';

function DisabledRadioGroup() {
  const [settings, setSettings] = useState({
    theme: 'light',
    language: 'en',
    notifications: 'enabled'
  });

  const [isEditing, setIsEditing] = useState(false);

  return (
    <div>
      <div style={{ marginBottom: '20px' }}>
        <button onClick={() => setIsEditing(!isEditing)}>
          {isEditing ? 'Save Changes' : 'Edit Settings'}
        </button>
      </div>

      <SafRadioGroup
        name="theme-preference"
        value={settings.theme}
        onChange={(value) => setSettings(prev => ({ ...prev, theme: value }))}
        legend="Theme Preference"
        readOnly={!isEditing}
        orientation="horizontal"
      >
        <SafRadio value="light" label="Light Theme" />
        <SafRadio value="dark" label="Dark Theme" />
        <SafRadio value="auto" label="Auto (System)" />
      </SafRadioGroup>

      <SafRadioGroup
        name="language-preference"
        value={settings.language}
        onChange={(value) => setSettings(prev => ({ ...prev, language: value }))}
        legend="Language"
        disabled={true}
        description="Language settings are managed by your administrator"
      >
        <SafRadio value="en" label="English" />
        <SafRadio value="es" label="Spanish" />
        <SafRadio value="fr" label="French" />
      </SafRadioGroup>
    </div>
  );
}
```

#### Dynamic Radio Options

```jsx
import { SafRadioGroup, SafRadio } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicRadioGroup() {
  const [selectedCountry, setSelectedCountry] = useState('');
  const [countries, setCountries] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulate API call
    const fetchCountries = async () => {
      setLoading(true);
      try {
        // Mock data - replace with actual API call
        const mockCountries = [
          { code: 'us', name: 'United States', flag: '🇺🇸' },
          { code: 'ca', name: 'Canada', flag: '🇨🇦' },
          { code: 'uk', name: 'United Kingdom', flag: '🇬🇧' },
          { code: 'de', name: 'Germany', flag: '🇩🇪' },
          { code: 'fr', name: 'France', flag: '🇫🇷' }
        ];
        
        await new Promise(resolve => setTimeout(resolve, 1000));
        setCountries(mockCountries);
      } catch (error) {
        console.error('Failed to fetch countries:', error);
      } finally {
        setLoading(false);
      }
    };

    fetchCountries();
  }, []);

  if (loading) {
    return <div>Loading countries...</div>;
  }

  return (
    <SafRadioGroup
      name="country-selection"
      value={selectedCountry}
      onChange={setSelectedCountry}
      legend="Select your country"
      description="Choose your country of residence"
      required={true}
    >
      {countries.map(country => (
        <SafRadio
          key={country.code}
          value={country.code}
          label={`${country.flag} ${country.name}`}
        />
      ))}
    </SafRadioGroup>
  );
}
```

## Angular

### API

| Input          | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `name`         | `string`                | `undefined` | Name attribute for the radio group            |
| `value`        | `string`                | `undefined` | Currently selected radio value                 |
| `orientation`  | `"horizontal" \| "vertical"` | `"vertical"` | Layout orientation of radio buttons      |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Size of radio buttons                    |
| `disabled`     | `boolean`               | `false`     | Whether the entire group is disabled          |
| `required`     | `boolean`               | `false`     | Whether selection is required                  |
| `readOnly`     | `boolean`               | `false`     | Whether the group is read-only                 |
| `legend`       | `string`                | `undefined` | Legend text for the fieldset                   |
| `description`  | `string`                | `undefined` | Description text below the legend              |
| `errorMessage` | `string`                | `undefined` | Error message to display                       |

### Events

| Output         | Type                    | Description                                    |
| -------------- | ----------------------- | ---------------------------------------------- |
| `valueChange`  | `EventEmitter<string>`  | Emitted when the selected value changes       |
| `focus`        | `EventEmitter<FocusEvent>` | Emitted when the group receives focus      |
| `blur`         | `EventEmitter<FocusEvent>` | Emitted when the group loses focus         |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-radio-group
  name="basic-options"
  [value]="selectedValue"
  (valueChange)="onValueChange($event)"
  legend="Choose an option">
  <saf-radio value="option1" label="Option 1"></saf-radio>
  <saf-radio value="option2" label="Option 2"></saf-radio>
  <saf-radio value="option3" label="Option 3"></saf-radio>
</saf-radio-group>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-radio-group',
  template: `
    <saf-radio-group
      name="basic-options"
      [value]="selectedValue"
      (valueChange)="onValueChange($event)"
      legend="Choose an option">
      <saf-radio value="option1" label="Option 1"></saf-radio>
      <saf-radio value="option2" label="Option 2"></saf-radio>
      <saf-radio value="option3" label="Option 3"></saf-radio>
    </saf-radio-group>
  `
})
export class BasicRadioGroupComponent {
  selectedValue = '';

  onValueChange(value: string): void {
    this.selectedValue = value;
    console.log('Selected:', value);
  }
}
```

#### Horizontal Layout with Description

```html
<!-- Angular template -->
<saf-radio-group
  name="notification-preference"
  [value]="preference"
  (valueChange)="preference = $event"
  orientation="horizontal"
  legend="Notification Preference"
  description="Choose how you'd like to receive notifications"
  size="large">
  <saf-radio 
    value="email" 
    label="Email" 
    description="Receive notifications via email">
  </saf-radio>
  <saf-radio 
    value="sms" 
    label="SMS" 
    description="Receive notifications via text message">
  </saf-radio>
  <saf-radio 
    value="push" 
    label="Push Notifications" 
    description="Receive browser push notifications">
  </saf-radio>
</saf-radio-group>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-horizontal-radio-group',
  template: `
    <saf-radio-group
      name="notification-preference"
      [value]="preference"
      (valueChange)="preference = $event"
      orientation="horizontal"
      legend="Notification Preference"
      description="Choose how you'd like to receive notifications"
      size="large">
      <saf-radio 
        value="email" 
        label="Email" 
        description="Receive notifications via email">
      </saf-radio>
      <saf-radio 
        value="sms" 
        label="SMS" 
        description="Receive notifications via text message">
      </saf-radio>
      <saf-radio 
        value="push" 
        label="Push Notifications" 
        description="Receive browser push notifications">
      </saf-radio>
    </saf-radio-group>
  `
})
export class HorizontalRadioGroupComponent {
  preference = 'email';
}
```

#### With Validation and Error Handling

```html
<!-- Angular template -->
<form (ngSubmit)="onSubmit()" #form="ngForm">
  <saf-radio-group
    name="subscription-plan"
    [value]="selectedPlan"
    (valueChange)="onPlanChange($event)"
    (blur)="onBlur()"
    legend="Subscription Plan"
    description="Select your preferred subscription plan"
    [required]="true"
    [errorMessage]="touched && error ? error : ''"
    [class]="error ? 'has-error' : ''">
    <saf-radio 
      *ngFor="let plan of plans"
      [value]="plan.value"
      [label]="plan.label"
      [description]="plan.price">
    </saf-radio>
  </saf-radio-group>
  
  <button type="submit" style="margin-top: 16px;">
    Continue
  </button>
</form>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface Plan {
  value: string;
  label: string;
  price: string;
}

@Component({
  selector: 'app-validated-radio-group',
  template: `
    <form (ngSubmit)="onSubmit()" #form="ngForm">
      <saf-radio-group
        name="subscription-plan"
        [value]="selectedPlan"
        (valueChange)="onPlanChange($event)"
        (blur)="onBlur()"
        legend="Subscription Plan"
        description="Select your preferred subscription plan"
        [required]="true"
        [errorMessage]="touched && error ? error : ''"
        [class]="error ? 'has-error' : ''">
        <saf-radio 
          *ngFor="let plan of plans"
          [value]="plan.value"
          [label]="plan.label"
          [description]="plan.price">
        </saf-radio>
      </saf-radio-group>
      
      <button type="submit" style="margin-top: 16px;">
        Continue
      </button>
    </form>
  `
})
export class ValidatedRadioGroupComponent {
  selectedPlan = '';
  error = '';
  touched = false;

  plans: Plan[] = [
    { value: 'basic', label: 'Basic Plan', price: '$9/month' },
    { value: 'professional', label: 'Professional Plan', price: '$29/month' },
    { value: 'enterprise', label: 'Enterprise Plan', price: '$99/month' }
  ];

  onPlanChange(value: string): void {
    this.selectedPlan = value;
    if (this.error && value) {
      this.error = '';
    }
  }

  onBlur(): void {
    this.touched = true;
    if (!this.selectedPlan) {
      this.error = 'Please select a subscription plan';
    }
  }

  onSubmit(): void {
    if (!this.selectedPlan) {
      this.error = 'Please select a subscription plan';
      this.touched = true;
      return;
    }
    console.log('Selected plan:', this.selectedPlan);
  }
}
```

#### Dynamic Radio Options

```html
<!-- Angular template -->
<div *ngIf="loading; else radioGroup">
  Loading countries...
</div>

<ng-template #radioGroup>
  <saf-radio-group
    name="country-selection"
    [value]="selectedCountry"
    (valueChange)="selectedCountry = $event"
    legend="Select your country"
    description="Choose your country of residence"
    [required]="true">
    <saf-radio 
      *ngFor="let country of countries; trackBy: trackByCountry"
      [value]="country.code"
      [label]="country.flag + ' ' + country.name">
    </saf-radio>
  </saf-radio-group>
</ng-template>
```

```typescript
// Angular component
import { Component, OnInit } from '@angular/core';

interface Country {
  code: string;
  name: string;
  flag: string;
}

@Component({
  selector: 'app-dynamic-radio-group',
  template: `
    <div *ngIf="loading; else radioGroup">
      Loading countries...
    </div>

    <ng-template #radioGroup>
      <saf-radio-group
        name="country-selection"
        [value]="selectedCountry"
        (valueChange)="selectedCountry = $event"
        legend="Select your country"
        description="Choose your country of residence"
        [required]="true">
        <saf-radio 
          *ngFor="let country of countries; trackBy: trackByCountry"
          [value]="country.code"
          [label]="country.flag + ' ' + country.name">
        </saf-radio>
      </saf-radio-group>
    </ng-template>
  `
})
export class DynamicRadioGroupComponent implements OnInit {
  selectedCountry = '';
  countries: Country[] = [];
  loading = true;

  ngOnInit(): void {
    this.fetchCountries();
  }

  private async fetchCountries(): Promise<void> {
    this.loading = true;
    try {
      // Mock data - replace with actual service call
      const mockCountries: Country[] = [
        { code: 'us', name: 'United States', flag: '🇺🇸' },
        { code: 'ca', name: 'Canada', flag: '🇨🇦' },
        { code: 'uk', name: 'United Kingdom', flag: '🇬🇧' },
        { code: 'de', name: 'Germany', flag: '🇩🇪' },
        { code: 'fr', name: 'France', flag: '🇫🇷' }
      ];
      
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.countries = mockCountries;
    } catch (error) {
      console.error('Failed to fetch countries:', error);
    } finally {
      this.loading = false;
    }
  }

  trackByCountry(index: number, country: Country): string {
    return country.code;
  }
}
```

#### Form Integration with Reactive Forms

```html
<!-- Angular template -->
<form [formGroup]="userForm" (ngSubmit)="onSubmit()">
  <saf-radio-group
    formControlName="accountType"
    name="account-type"
    legend="Account Type"
    description="Select the type of account you want to create"
    [required]="true"
    [errorMessage]="getErrorMessage('accountType')">
    <saf-radio value="personal" label="Personal Account" description="For individual use"></saf-radio>
    <saf-radio value="business" label="Business Account" description="For business use"></saf-radio>
    <saf-radio value="nonprofit" label="Non-profit Account" description="For non-profit organizations"></saf-radio>
  </saf-radio-group>

  <saf-radio-group
    formControlName="plan"
    name="plan-type"
    legend="Plan Type"
    orientation="horizontal"
    [required]="true"
    [errorMessage]="getErrorMessage('plan')">
    <saf-radio value="free" label="Free" description="Basic features"></saf-radio>
    <saf-radio value="premium" label="Premium" description="Advanced features"></saf-radio>
  </saf-radio-group>

  <button type="submit" [disabled]="userForm.invalid">
    Create Account
  </button>
</form>
```

```typescript
// Angular component
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-reactive-radio-group',
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <saf-radio-group
        formControlName="accountType"
        name="account-type"
        legend="Account Type"
        description="Select the type of account you want to create"
        [required]="true"
        [errorMessage]="getErrorMessage('accountType')">
        <saf-radio value="personal" label="Personal Account" description="For individual use"></saf-radio>
        <saf-radio value="business" label="Business Account" description="For business use"></saf-radio>
        <saf-radio value="nonprofit" label="Non-profit Account" description="For non-profit organizations"></saf-radio>
      </saf-radio-group>

      <saf-radio-group
        formControlName="plan"
        name="plan-type"
        legend="Plan Type"
        orientation="horizontal"
        [required]="true"
        [errorMessage]="getErrorMessage('plan')">
        <saf-radio value="free" label="Free" description="Basic features"></saf-radio>
        <saf-radio value="premium" label="Premium" description="Advanced features"></saf-radio>
      </saf-radio-group>

      <button type="submit" [disabled]="userForm.invalid">
        Create Account
      </button>
    </form>
  `
})
export class ReactiveRadioGroupComponent {
  userForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.userForm = this.fb.group({
      accountType: ['', Validators.required],
      plan: ['', Validators.required]
    });
  }

  getErrorMessage(controlName: string): string {
    const control = this.userForm.get(controlName);
    if (control?.errors?.['required'] && control?.touched) {
      return `Please select a ${controlName}`;
    }
    return '';
  }

  onSubmit(): void {
    if (this.userForm.valid) {
      console.log('Form submitted:', this.userForm.value);
    } else {
      // Mark all fields as touched to show validation errors
      this.userForm.markAllAsTouched();
    }
  }
}
```

### Best Practices

- **Meaningful labels**: Use clear, descriptive labels for each radio option
- **Logical grouping**: Group related options together and use appropriate legends
- **Keyboard navigation**: Ensure proper arrow key navigation between radio buttons within the group
- **Validation feedback**: Provide clear validation messages at the group level
- **Default selection**: Consider providing sensible default selections for better UX
- **Responsive design**: Adjust orientation based on screen size and available space
- **Accessibility**: Use proper fieldset/legend structure and ARIA attributes
- **Performance**: Use trackBy functions in Angular for efficient rendering of dynamic options

### Notes

- SafRadioGroup automatically manages the mutual exclusivity of radio buttons within the group
- The component provides built-in keyboard navigation (arrow keys) between options
- Form integration works seamlessly with both template-driven and reactive forms in Angular
- The `name` attribute is automatically applied to all child SafRadio components
- Error states are managed at the group level and propagated to individual radio buttons
- The component handles focus management and ensures proper accessibility attributes
- Radio groups should always have a visible legend for screen reader users
