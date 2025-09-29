# SafDateMaskedInput

The SafDateMaskedInput component provides a specialized input field for date entry with automatic formatting and masking. It helps users enter dates in a consistent format while providing visual guidance and validation.

## React

### API

| Prop           | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `value`        | `string \| Date`        | `undefined` | Current date value                             |
| `defaultValue` | `string \| Date`        | `undefined` | Default date value (uncontrolled)             |
| `format`       | `string`                | `"MM/DD/YYYY"` | Date format pattern                         |
| `placeholder`  | `string`                | `undefined` | Placeholder text (auto-generated from format) |
| `mask`         | `string`                | `undefined` | Custom mask pattern                            |
| `separator`    | `string`                | `"/"` | Date separator character                             |
| `minDate`      | `string \| Date`        | `undefined` | Minimum allowed date                           |
| `maxDate`      | `string \| Date`        | `undefined` | Maximum allowed date                           |
| `disabled`     | `boolean`               | `false`     | Whether the input is disabled                  |
| `readOnly`     | `boolean`               | `false`     | Whether the input is read-only                 |
| `required`     | `boolean`               | `false`     | Whether the field is required                  |
| `autoComplete` | `string`                | `"off"`     | HTML autocomplete attribute                    |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Input field size                      |
| `variant`      | `"outline" \| "filled" \| "underline"` | `"outline"` | Input field style variant        |
| `label`        | `string`                | `undefined` | Label text for the input                       |
| `description`  | `string`                | `undefined` | Description text below the input               |
| `errorMessage` | `string`                | `undefined` | Error message to display                       |
| `className`    | `string`                | `undefined` | Additional CSS class names                     |
| `onChange`     | `(value: string, isValid: boolean, event: ChangeEvent) => void` | `undefined` | Change handler |
| `onFocus`      | `(event: FocusEvent) => void` | `undefined` | Focus handler                        |
| `onBlur`       | `(event: FocusEvent) => void` | `undefined` | Blur handler                         |
| `onValidation` | `(isValid: boolean, errors: string[]) => void` | `undefined` | Validation handler        |

### Examples

#### Basic Usage

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState } from 'react';

function BasicDateInput() {
  const [date, setDate] = useState('');

  const handleDateChange = (value, isValid, event) => {
    setDate(value);
    console.log('Date changed:', value, 'Valid:', isValid);
  };

  return (
    <SafDateMaskedInput
      value={date}
      onChange={handleDateChange}
      label="Birth Date"
      placeholder="MM/DD/YYYY"
    />
  );
}
```

#### Different Date Formats

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState } from 'react';

function DifferentFormats() {
  const [usDate, setUsDate] = useState('');
  const [europeanDate, setEuropeanDate] = useState('');
  const [isoDate, setIsoDate] = useState('');

  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '20px' }}>
      <SafDateMaskedInput
        value={usDate}
        onChange={(value) => setUsDate(value)}
        format="MM/DD/YYYY"
        label="US Format"
        description="Month/Day/Year format"
      />
      
      <SafDateMaskedInput
        value={europeanDate}
        onChange={(value) => setEuropeanDate(value)}
        format="DD/MM/YYYY"
        separator="/"
        label="European Format"
        description="Day/Month/Year format"
      />
      
      <SafDateMaskedInput
        value={isoDate}
        onChange={(value) => setIsoDate(value)}
        format="YYYY-MM-DD"
        separator="-"
        label="ISO Format"
        description="Year-Month-Day format"
      />
    </div>
  );
}
```

#### With Date Validation

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState } from 'react';

function ValidatedDateInput() {
  const [startDate, setStartDate] = useState('');
  const [endDate, setEndDate] = useState('');
  const [errors, setErrors] = useState({});

  const today = new Date();
  const maxDate = new Date();
  maxDate.setFullYear(maxDate.getFullYear() + 1); // One year from now

  const handleStartDateChange = (value, isValid, event) => {
    setStartDate(value);
    
    if (isValid && endDate) {
      const start = new Date(value);
      const end = new Date(endDate);
      
      if (start >= end) {
        setErrors(prev => ({
          ...prev,
          startDate: 'Start date must be before end date'
        }));
      } else {
        setErrors(prev => ({ ...prev, startDate: '', endDate: '' }));
      }
    }
  };

  const handleEndDateChange = (value, isValid, event) => {
    setEndDate(value);
    
    if (isValid && startDate) {
      const start = new Date(startDate);
      const end = new Date(value);
      
      if (end <= start) {
        setErrors(prev => ({
          ...prev,
          endDate: 'End date must be after start date'
        }));
      } else {
        setErrors(prev => ({ ...prev, startDate: '', endDate: '' }));
      }
    }
  };

  const handleValidation = (field) => (isValid, validationErrors) => {
    if (!isValid) {
      setErrors(prev => ({
        ...prev,
        [field]: validationErrors[0] || 'Invalid date'
      }));
    } else {
      setErrors(prev => ({ ...prev, [field]: '' }));
    }
  };

  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '20px' }}>
      <SafDateMaskedInput
        value={startDate}
        onChange={handleStartDateChange}
        onValidation={handleValidation('startDate')}
        minDate={today}
        maxDate={maxDate}
        label="Start Date"
        description="Select a start date (today or later)"
        errorMessage={errors.startDate}
        required
      />
      
      <SafDateMaskedInput
        value={endDate}
        onChange={handleEndDateChange}
        onValidation={handleValidation('endDate')}
        minDate={startDate || today}
        maxDate={maxDate}
        label="End Date"
        description="Select an end date (after start date)"
        errorMessage={errors.endDate}
        required
      />
    </div>
  );
}
```

#### Custom Mask and Formatting

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState } from 'react';

function CustomMaskDateInput() {
  const [shortDate, setShortDate] = useState('');
  const [longDate, setLongDate] = useState('');
  const [timeDate, setTimeDate] = useState('');

  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '20px' }}>
      <SafDateMaskedInput
        value={shortDate}
        onChange={(value) => setShortDate(value)}
        format="MM/YY"
        mask="99/99"
        label="Expiry Date"
        description="Credit card expiry date (MM/YY)"
        placeholder="MM/YY"
      />
      
      <SafDateMaskedInput
        value={longDate}
        onChange={(value) => setLongDate(value)}
        format="DD MMM YYYY"
        separator=" "
        label="Verbose Date"
        description="Day Month Year format"
        placeholder="DD MMM YYYY"
      />
      
      <SafDateMaskedInput
        value={timeDate}
        onChange={(value) => setTimeDate(value)}
        format="MM/DD/YYYY HH:mm"
        mask="99/99/9999 99:99"
        separator="/"
        label="Date and Time"
        description="Date with time (24-hour format)"
        placeholder="MM/DD/YYYY HH:mm"
      />
    </div>
  );
}
```

#### Advanced Usage with Form Integration

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState, useCallback } from 'react';

function AdvancedDateForm() {
  const [formData, setFormData] = useState({
    birthDate: '',
    joinDate: '',
    expiryDate: ''
  });
  const [validationState, setValidationState] = useState({});
  const [touched, setTouched] = useState({});

  const updateFormField = useCallback((field, value, isValid) => {
    setFormData(prev => ({ ...prev, [field]: value }));
    setValidationState(prev => ({ ...prev, [field]: isValid }));
  }, []);

  const handleFieldBlur = useCallback((field) => () => {
    setTouched(prev => ({ ...prev, [field]: true }));
  }, []);

  const calculateAge = (birthDate) => {
    if (!birthDate) return null;
    
    try {
      const birth = new Date(birthDate);
      const today = new Date();
      let age = today.getFullYear() - birth.getFullYear();
      const monthDiff = today.getMonth() - birth.getMonth();
      
      if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birth.getDate())) {
        age--;
      }
      
      return age;
    } catch (error) {
      return null;
    }
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    
    const allFieldsTouched = Object.keys(formData).reduce((acc, field) => ({
      ...acc,
      [field]: true
    }), {});
    setTouched(allFieldsTouched);
    
    const isFormValid = Object.values(validationState).every(isValid => isValid);
    
    if (isFormValid) {
      console.log('Form submitted:', formData);
    } else {
      console.log('Form validation failed');
    }
  };

  const age = calculateAge(formData.birthDate);

  return (
    <form onSubmit={handleSubmit} style={{ display: 'flex', flexDirection: 'column', gap: '20px' }}>
      <SafDateMaskedInput
        value={formData.birthDate}
        onChange={(value, isValid) => updateFormField('birthDate', value, isValid)}
        onBlur={handleFieldBlur('birthDate')}
        onValidation={(isValid, errors) => {
          if (touched.birthDate) {
            setValidationState(prev => ({ ...prev, birthDate: isValid }));
          }
        }}
        maxDate={new Date()}
        label="Date of Birth"
        description={age !== null ? `Age: ${age} years` : 'Enter your birth date'}
        errorMessage={touched.birthDate && !validationState.birthDate ? 'Please enter a valid birth date' : ''}
        required
        size="large"
      />
      
      <SafDateMaskedInput
        value={formData.joinDate}
        onChange={(value, isValid) => updateFormField('joinDate', value, isValid)}
        onBlur={handleFieldBlur('joinDate')}
        onValidation={(isValid) => {
          if (touched.joinDate) {
            setValidationState(prev => ({ ...prev, joinDate: isValid }));
          }
        }}
        minDate={formData.birthDate}
        maxDate={new Date()}
        label="Join Date"
        description="When did you join the organization?"
        errorMessage={touched.joinDate && !validationState.joinDate ? 'Please enter a valid join date' : ''}
        required
      />
      
      <SafDateMaskedInput
        value={formData.expiryDate}
        onChange={(value, isValid) => updateFormField('expiryDate', value, isValid)}
        onBlur={handleFieldBlur('expiryDate')}
        format="MM/YY"
        mask="99/99"
        placeholder="MM/YY"
        label="Card Expiry"
        description="Credit card expiration date"
        errorMessage={touched.expiryDate && !validationState.expiryDate ? 'Please enter a valid expiry date' : ''}
        required
      />
      
      <button 
        type="submit"
        style={{ 
          padding: '12px 24px',
          backgroundColor: '#007bff',
          color: 'white',
          border: 'none',
          borderRadius: '4px',
          cursor: 'pointer'
        }}
      >
        Submit Form
      </button>
    </form>
  );
}
```

#### Disabled and Read-Only States

```jsx
import { SafDateMaskedInput } from '@saffron/core-components';
import { useState } from 'react';

function DisabledReadOnlyStates() {
  const [editableDate, setEditableDate] = useState('');
  const [isEditing, setIsEditing] = useState(false);

  const systemDate = new Date().toLocaleDateString('en-US');
  const lockedDate = '12/25/2024';

  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '20px' }}>
      <SafDateMaskedInput
        value={systemDate}
        label="System Date"
        description="Current system date (disabled)"
        disabled={true}
        variant="filled"
      />
      
      <SafDateMaskedInput
        value={lockedDate}
        label="Locked Date"
        description="This date cannot be modified (read-only)"
        readOnly={true}
        variant="outline"
      />
      
      <div>
        <div style={{ marginBottom: '8px' }}>
          <button 
            onClick={() => setIsEditing(!isEditing)}
            style={{ 
              padding: '8px 16px',
              backgroundColor: isEditing ? '#28a745' : '#007bff',
              color: 'white',
              border: 'none',
              borderRadius: '4px',
              cursor: 'pointer'
            }}
          >
            {isEditing ? 'Save Changes' : 'Edit Date'}
          </button>
        </div>
        
        <SafDateMaskedInput
          value={editableDate}
          onChange={(value) => setEditableDate(value)}
          label="Conditional Edit Date"
          description={isEditing ? 'You can now edit this date' : 'Click "Edit Date" to modify'}
          readOnly={!isEditing}
          variant={isEditing ? 'outline' : 'filled'}
        />
      </div>
    </div>
  );
}
```

## Angular

### API

| Input          | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `value`        | `string \| Date`        | `undefined` | Current date value                             |
| `format`       | `string`                | `"MM/DD/YYYY"` | Date format pattern                         |
| `placeholder`  | `string`                | `undefined` | Placeholder text                               |
| `mask`         | `string`                | `undefined` | Custom mask pattern                            |
| `separator`    | `string`                | `"/"` | Date separator character                             |
| `minDate`      | `string \| Date`        | `undefined` | Minimum allowed date                           |
| `maxDate`      | `string \| Date`        | `undefined` | Maximum allowed date                           |
| `disabled`     | `boolean`               | `false`     | Whether the input is disabled                  |
| `readOnly`     | `boolean`               | `false`     | Whether the input is read-only                 |
| `required`     | `boolean`               | `false`     | Whether the field is required                  |
| `autoComplete` | `string`                | `"off"`     | HTML autocomplete attribute                    |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Input field size                      |
| `variant`      | `"outline" \| "filled" \| "underline"` | `"outline"` | Input field style variant        |
| `label`        | `string`                | `undefined` | Label text for the input                       |
| `description`  | `string`                | `undefined` | Description text below the input               |
| `errorMessage` | `string`                | `undefined` | Error message to display                       |

### Events

| Output         | Type                    | Description                                    |
| -------------- | ----------------------- | ---------------------------------------------- |
| `valueChange`  | `EventEmitter<string>`  | Emitted when the value changes                 |
| `validationChange` | `EventEmitter<{isValid: boolean, errors: string[]}>` | Emitted when validation state changes |
| `focus`        | `EventEmitter<FocusEvent>` | Emitted when input receives focus          |
| `blur`         | `EventEmitter<FocusEvent>` | Emitted when input loses focus             |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-date-masked-input
  [value]="date"
  (valueChange)="onDateChange($event)"
  label="Birth Date"
  placeholder="MM/DD/YYYY">
</saf-date-masked-input>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-date-input',
  template: `
    <saf-date-masked-input
      [value]="date"
      (valueChange)="onDateChange($event)"
      label="Birth Date"
      placeholder="MM/DD/YYYY">
    </saf-date-masked-input>
  `
})
export class BasicDateInputComponent {
  date = '';

  onDateChange(value: string): void {
    this.date = value;
    console.log('Date changed:', value);
  }
}
```

#### Different Date Formats

```html
<!-- Angular template -->
<div style="display: flex; flex-direction: column; gap: 20px;">
  <saf-date-masked-input
    [value]="usDate"
    (valueChange)="usDate = $event"
    format="MM/DD/YYYY"
    label="US Format"
    description="Month/Day/Year format">
  </saf-date-masked-input>
  
  <saf-date-masked-input
    [value]="europeanDate"
    (valueChange)="europeanDate = $event"
    format="DD/MM/YYYY"
    separator="/"
    label="European Format"
    description="Day/Month/Year format">
  </saf-date-masked-input>
  
  <saf-date-masked-input
    [value]="isoDate"
    (valueChange)="isoDate = $event"
    format="YYYY-MM-DD"
    separator="-"
    label="ISO Format"
    description="Year-Month-Day format">
  </saf-date-masked-input>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-different-formats',
  template: `
    <div style="display: flex; flex-direction: column; gap: 20px;">
      <saf-date-masked-input
        [value]="usDate"
        (valueChange)="usDate = $event"
        format="MM/DD/YYYY"
        label="US Format"
        description="Month/Day/Year format">
      </saf-date-masked-input>
      
      <saf-date-masked-input
        [value]="europeanDate"
        (valueChange)="europeanDate = $event"
        format="DD/MM/YYYY"
        separator="/"
        label="European Format"
        description="Day/Month/Year format">
      </saf-date-masked-input>
      
      <saf-date-masked-input
        [value]="isoDate"
        (valueChange)="isoDate = $event"
        format="YYYY-MM-DD"
        separator="-"
        label="ISO Format"
        description="Year-Month-Day format">
      </saf-date-masked-input>
    </div>
  `
})
export class DifferentFormatsComponent {
  usDate = '';
  europeanDate = '';
  isoDate = '';
}
```

#### With Date Validation

```html
<!-- Angular template -->
<div style="display: flex; flex-direction: column; gap: 20px;">
  <saf-date-masked-input
    [value]="startDate"
    (valueChange)="onStartDateChange($event)"
    (validationChange)="onStartDateValidation($event)"
    [minDate]="today"
    [maxDate]="maxDate"
    label="Start Date"
    description="Select a start date (today or later)"
    [errorMessage]="errors.startDate"
    [required]="true">
  </saf-date-masked-input>
  
  <saf-date-masked-input
    [value]="endDate"
    (valueChange)="onEndDateChange($event)"
    (validationChange)="onEndDateValidation($event)"
    [minDate]="startDate || today"
    [maxDate]="maxDate"
    label="End Date"
    description="Select an end date (after start date)"
    [errorMessage]="errors.endDate"
    [required]="true">
  </saf-date-masked-input>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface ValidationResult {
  isValid: boolean;
  errors: string[];
}

@Component({
  selector: 'app-validated-date-input',
  template: `
    <div style="display: flex; flex-direction: column; gap: 20px;">
      <saf-date-masked-input
        [value]="startDate"
        (valueChange)="onStartDateChange($event)"
        (validationChange)="onStartDateValidation($event)"
        [minDate]="today"
        [maxDate]="maxDate"
        label="Start Date"
        description="Select a start date (today or later)"
        [errorMessage]="errors.startDate"
        [required]="true">
      </saf-date-masked-input>
      
      <saf-date-masked-input
        [value]="endDate"
        (valueChange)="onEndDateChange($event)"
        (validationChange)="onEndDateValidation($event)"
        [minDate]="startDate || today"
        [maxDate]="maxDate"
        label="End Date"
        description="Select an end date (after start date)"
        [errorMessage]="errors.endDate"
        [required]="true">
      </saf-date-masked-input>
    </div>
  `
})
export class ValidatedDateInputComponent {
  startDate = '';
  endDate = '';
  today = new Date();
  maxDate = new Date(new Date().setFullYear(new Date().getFullYear() + 1));
  
  errors = {
    startDate: '',
    endDate: ''
  };

  onStartDateChange(value: string): void {
    this.startDate = value;
    this.validateDateRange();
  }

  onEndDateChange(value: string): void {
    this.endDate = value;
    this.validateDateRange();
  }

  onStartDateValidation(result: ValidationResult): void {
    if (!result.isValid) {
      this.errors.startDate = result.errors[0] || 'Invalid date';
    } else {
      this.errors.startDate = '';
    }
  }

  onEndDateValidation(result: ValidationResult): void {
    if (!result.isValid) {
      this.errors.endDate = result.errors[0] || 'Invalid date';
    } else {
      this.errors.endDate = '';
    }
  }

  private validateDateRange(): void {
    if (this.startDate && this.endDate) {
      const start = new Date(this.startDate);
      const end = new Date(this.endDate);
      
      if (start >= end) {
        this.errors.startDate = 'Start date must be before end date';
        this.errors.endDate = 'End date must be after start date';
      } else {
        if (!this.errors.startDate) this.errors.startDate = '';
        if (!this.errors.endDate) this.errors.endDate = '';
      }
    }
  }
}
```

#### Custom Mask and Formatting

```html
<!-- Angular template -->
<div style="display: flex; flex-direction: column; gap: 20px;">
  <saf-date-masked-input
    [value]="shortDate"
    (valueChange)="shortDate = $event"
    format="MM/YY"
    mask="99/99"
    label="Expiry Date"
    description="Credit card expiry date (MM/YY)"
    placeholder="MM/YY">
  </saf-date-masked-input>
  
  <saf-date-masked-input
    [value]="timeDate"
    (valueChange)="timeDate = $event"
    format="MM/DD/YYYY HH:mm"
    mask="99/99/9999 99:99"
    separator="/"
    label="Date and Time"
    description="Date with time (24-hour format)"
    placeholder="MM/DD/YYYY HH:mm">
  </saf-date-masked-input>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-custom-mask-date-input',
  template: `
    <div style="display: flex; flex-direction: column; gap: 20px;">
      <saf-date-masked-input
        [value]="shortDate"
        (valueChange)="shortDate = $event"
        format="MM/YY"
        mask="99/99"
        label="Expiry Date"
        description="Credit card expiry date (MM/YY)"
        placeholder="MM/YY">
      </saf-date-masked-input>
      
      <saf-date-masked-input
        [value]="timeDate"
        (valueChange)="timeDate = $event"
        format="MM/DD/YYYY HH:mm"
        mask="99/99/9999 99:99"
        separator="/"
        label="Date and Time"
        description="Date with time (24-hour format)"
        placeholder="MM/DD/YYYY HH:mm">
      </saf-date-masked-input>
    </div>
  `
})
export class CustomMaskDateInputComponent {
  shortDate = '';
  timeDate = '';
}
```

#### Form Integration with Reactive Forms

```html
<!-- Angular template -->
<form [formGroup]="dateForm" (ngSubmit)="onSubmit()">
  <div style="display: flex; flex-direction: column; gap: 20px;">
    <saf-date-masked-input
      formControlName="birthDate"
      [maxDate]="today"
      label="Date of Birth"
      [description]="getAgeDescription()"
      [errorMessage]="getErrorMessage('birthDate')"
      [required]="true"
      size="large">
    </saf-date-masked-input>
    
    <saf-date-masked-input
      formControlName="joinDate"
      [minDate]="dateForm.get('birthDate')?.value"
      [maxDate]="today"
      label="Join Date"
      description="When did you join the organization?"
      [errorMessage]="getErrorMessage('joinDate')"
      [required]="true">
    </saf-date-masked-input>
    
    <saf-date-masked-input
      formControlName="expiryDate"
      format="MM/YY"
      mask="99/99"
      placeholder="MM/YY"
      label="Card Expiry"
      description="Credit card expiration date"
      [errorMessage]="getErrorMessage('expiryDate')"
      [required]="true">
    </saf-date-masked-input>
    
    <button 
      type="submit" 
      [disabled]="dateForm.invalid"
      style="padding: 12px 24px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer;">
      Submit Form
    </button>
  </div>
</form>
```

```typescript
// Angular component
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-reactive-date-form',
  template: `
    <form [formGroup]="dateForm" (ngSubmit)="onSubmit()">
      <div style="display: flex; flex-direction: column; gap: 20px;">
        <saf-date-masked-input
          formControlName="birthDate"
          [maxDate]="today"
          label="Date of Birth"
          [description]="getAgeDescription()"
          [errorMessage]="getErrorMessage('birthDate')"
          [required]="true"
          size="large">
        </saf-date-masked-input>
        
        <saf-date-masked-input
          formControlName="joinDate"
          [minDate]="dateForm.get('birthDate')?.value"
          [maxDate]="today"
          label="Join Date"
          description="When did you join the organization?"
          [errorMessage]="getErrorMessage('joinDate')"
          [required]="true">
        </saf-date-masked-input>
        
        <saf-date-masked-input
          formControlName="expiryDate"
          format="MM/YY"
          mask="99/99"
          placeholder="MM/YY"
          label="Card Expiry"
          description="Credit card expiration date"
          [errorMessage]="getErrorMessage('expiryDate')"
          [required]="true">
        </saf-date-masked-input>
        
        <button 
          type="submit" 
          [disabled]="dateForm.invalid"
          style="padding: 12px 24px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer;">
          Submit Form
        </button>
      </div>
    </form>
  `
})
export class ReactiveDateFormComponent {
  dateForm: FormGroup;
  today = new Date();

  constructor(private fb: FormBuilder) {
    this.dateForm = this.fb.group({
      birthDate: ['', [Validators.required]],
      joinDate: ['', [Validators.required]],
      expiryDate: ['', [Validators.required]]
    });
  }

  getErrorMessage(controlName: string): string {
    const control = this.dateForm.get(controlName);
    if (control?.errors && control?.touched) {
      if (control.errors['required']) {
        return `${controlName} is required`;
      }
      if (control.errors['invalidDate']) {
        return 'Please enter a valid date';
      }
    }
    return '';
  }

  getAgeDescription(): string {
    const birthDate = this.dateForm.get('birthDate')?.value;
    if (birthDate) {
      const age = this.calculateAge(birthDate);
      return age !== null ? `Age: ${age} years` : 'Enter your birth date';
    }
    return 'Enter your birth date';
  }

  private calculateAge(birthDate: string): number | null {
    if (!birthDate) return null;
    
    try {
      const birth = new Date(birthDate);
      const today = new Date();
      let age = today.getFullYear() - birth.getFullYear();
      const monthDiff = today.getMonth() - birth.getMonth();
      
      if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birth.getDate())) {
        age--;
      }
      
      return age;
    } catch (error) {
      return null;
    }
  }

  onSubmit(): void {
    if (this.dateForm.valid) {
      console.log('Form submitted:', this.dateForm.value);
    } else {
      this.dateForm.markAllAsTouched();
    }
  }
}
```

### Best Practices

- **Clear format indication**: Always provide clear placeholder text or descriptions showing the expected date format
- **Appropriate date ranges**: Set reasonable min/max dates to prevent invalid entries
- **Validation feedback**: Provide immediate and clear feedback for invalid dates
- **Consistent formatting**: Use consistent date formats throughout your application
- **Accessibility**: Ensure proper labeling and error message association for screen readers
- **Locale consideration**: Consider user's locale when choosing default date formats
- **Mobile optimization**: Test on mobile devices to ensure mask input works properly with virtual keyboards
- **Error handling**: Handle edge cases like leap years, invalid dates, and boundary conditions

### Notes

- The component automatically applies input masking based on the specified format
- Date validation occurs in real-time as the user types
- The mask pattern uses standard characters: 9 for digits, A for letters, * for alphanumeric
- Custom separators can be used to match regional date format preferences
- The component works seamlessly with both template-driven and reactive forms in Angular
- Minimum and maximum date validation helps prevent invalid date selections
- The component handles various date format patterns including abbreviated months and time components
