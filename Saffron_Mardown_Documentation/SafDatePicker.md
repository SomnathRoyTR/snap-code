# SafDatePicker - Date Selection Component

## Overview
`SafDatePicker` is a comprehensive date input component that combines a masked text input with a calendar popup. It supports localization, date validation, min/max constraints, and accessibility features.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `name` | `string` | `undefined` | Form field name |
| `id` | `string` | `undefined` | Unique identifier |
| `value` | `string` | `undefined` | Current date value in format |
| `label` | `string` | `undefined` | Label text |
| `placeholder` | `string` | `undefined` | Placeholder text |
| `format` | `string` | `'MM/DD/YYYY'` | Date format string |
| `locale` | `string` | `navigator.language` | Locale for formatting |
| `min-date` | `string` | `'1900-01-01'` | Minimum selectable date |
| `max-date` | `string` | `'2099-12-31'` | Maximum selectable date |
| `default-date` | `string` | `undefined` | Default date value |
| `default-picker-date` | `string` | `undefined` | Initial calendar focus date |
| `required` | `boolean` | `false` | Whether date is required |
| `disabled` | `boolean` | `false` | Whether picker is disabled |
| `readonly` | `boolean` | `false` | Whether input is read-only |
| `invalid` | `boolean` | `false` | Whether in error state |
| `is-success` | `boolean` | `false` | Whether in success state |
| `autocorrect` | `boolean` | `true` | Auto-correct invalid dates |
| `required-text` | `string` | `'*'` | Required indicator text |
| `optional-text` | `string` | `undefined` | Optional indicator text |
| `instructional-text` | `string` | `undefined` | Help text |
| `validation-message` | `string` | `undefined` | Validation feedback |
| `date-picker-aria-label` | `string` | `'date picker'` | ARIA label for calendar |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `change` | `CustomEvent<string>` | Fired when date value changes |
| `input` | `CustomEvent<string>` | Fired during input |
| `focus` | `FocusEvent` | Fired when input gains focus |
| `blur` | `FocusEvent` | Fired when input loses focus |
| `calendar-open` | `CustomEvent<void>` | Fired when calendar opens |
| `calendar-close` | `CustomEvent<void>` | Fired when calendar closes |

### Methods
| Method | Description |
|--------|-------------|
| `focus()` | Focus the date input |
| `blur()` | Remove focus from input |
| `openCalendar()` | Open the calendar popup |
| `closeCalendar()` | Close the calendar popup |
| `setCustomValidity(message)` | Set custom validation message |
| `checkValidity()` | Check if date is valid |

## Usage Examples

### Basic Date Picker
```typescript
// React
import { SafDatePicker } from '@saffron/react';

export const BasicDatePicker = () => {
  const [date, setDate] = useState('');
  
  return (
    <SafDatePicker
      label="Select Date"
      value={date}
      onChange={(e) => setDate(e.target.value)}
      required
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-date-picker
      label="Select Date"
      [value]="selectedDate"
      (change)="onDateChange($event)"
      required>
    </saf-date-picker>
  `
})
export class BasicDatePickerComponent {
  selectedDate = '';
  
  onDateChange(event: CustomEvent<string>) {
    this.selectedDate = event.detail;
  }
}
```

### Date Picker with Custom Format
```typescript
// React
export const CustomFormatDatePicker = () => {
  const [birthdate, setBirthdate] = useState('');
  
  return (
    <SafDatePicker
      label="Date of Birth"
      value={birthdate}
      onChange={(e) => setBirthdate(e.target.value)}
      format="DD/MM/YYYY"
      locale="en-GB"
      placeholder="DD/MM/YYYY"
      required
    />
  );
};
```

### Date Range Constraints
```typescript
// React
export const ConstrainedDatePicker = () => {
  const [appointmentDate, setAppointmentDate] = useState('');
  
  // Next 30 days only
  const today = new Date();
  const maxDate = new Date();
  maxDate.setDate(today.getDate() + 30);
  
  return (
    <SafDatePicker
      label="Appointment Date"
      value={appointmentDate}
      onChange={(e) => setAppointmentDate(e.target.value)}
      min-date={today.toISOString().split('T')[0]}
      max-date={maxDate.toISOString().split('T')[0]}
      instructional-text="Select a date within the next 30 days"
      required
    />
  );
};
```

### Localized Date Picker
```typescript
// React
export const LocalizedDatePicker = () => {
  const [locale, setLocale] = useState('en-US');
  const [date, setDate] = useState('');
  
  const locales = [
    { value: 'en-US', label: 'English (US)', format: 'MM/DD/YYYY' },
    { value: 'en-GB', label: 'English (UK)', format: 'DD/MM/YYYY' },
    { value: 'de-DE', label: 'Deutsch', format: 'DD.MM.YYYY' },
    { value: 'fr-FR', label: 'Français', format: 'DD/MM/YYYY' }
  ];
  
  const currentLocale = locales.find(l => l.value === locale);
  
  return (
    <div>
      <SafSelect
        label="Locale"
        value={locale}
        onChange={(e) => setLocale(e.target.value)}
      >
        {locales.map(loc => (
          <SafOption key={loc.value} value={loc.value}>
            {loc.label}
          </SafOption>
        ))}
      </SafSelect>
      
      <SafDatePicker
        label="Date"
        value={date}
        onChange={(e) => setDate(e.target.value)}
        locale={locale}
        format={currentLocale?.format}
        placeholder={currentLocale?.format}
      />
    </div>
  );
};
```

### Validation and Error States
```typescript
// React
export const ValidatedDatePicker = () => {
  const [startDate, setStartDate] = useState('');
  const [endDate, setEndDate] = useState('');
  const [errors, setErrors] = useState({ start: '', end: '' });
  
  const validateDates = (start: string, end: string) => {
    const errors = { start: '', end: '' };
    
    if (!start) {
      errors.start = 'Start date is required';
    }
    
    if (!end) {
      errors.end = 'End date is required';
    }
    
    if (start && end && new Date(start) >= new Date(end)) {
      errors.end = 'End date must be after start date';
    }
    
    setErrors(errors);
    return !errors.start && !errors.end;
  };
  
  return (
    <form>
      <SafDatePicker
        label="Start Date"
        value={startDate}
        onChange={(e) => {
          setStartDate(e.target.value);
          validateDates(e.target.value, endDate);
        }}
        required
        invalid={!!errors.start}
        validation-message={errors.start}
      />
      
      <SafDatePicker
        label="End Date"
        value={endDate}
        onChange={(e) => {
          setEndDate(e.target.value);
          validateDates(startDate, e.target.value);
        }}
        min-date={startDate || undefined}
        required
        invalid={!!errors.end}
        validation-message={errors.end}
      />
    </form>
  );
};
```

### Success State with Confirmation
```typescript
// React
export const ConfirmedDatePicker = () => {
  const [deliveryDate, setDeliveryDate] = useState('');
  const [confirmed, setConfirmed] = useState(false);
  
  const handleDateChange = (value: string) => {
    setDeliveryDate(value);
    setConfirmed(false);
  };
  
  const confirmDate = () => {
    setConfirmed(true);
    // API call to confirm delivery date
  };
  
  return (
    <div>
      <SafDatePicker
        label="Delivery Date"
        value={deliveryDate}
        onChange={(e) => handleDateChange(e.target.value)}
        is-success={confirmed}
        validation-message={confirmed ? 'Delivery date confirmed' : undefined}
        required
      />
      
      {deliveryDate && !confirmed && (
        <SafButton onClick={confirmDate} appearance="primary">
          Confirm Date
        </SafButton>
      )}
    </div>
  );
};
```

### Birthday Picker
```typescript
// React
export const BirthdayPicker = () => {
  const [birthday, setBirthday] = useState('');
  
  const maxDate = new Date();
  maxDate.setFullYear(maxDate.getFullYear() - 13); // Must be at least 13 years old
  
  const minDate = new Date();
  minDate.setFullYear(minDate.getFullYear() - 120); // Reasonable maximum age
  
  return (
    <SafDatePicker
      label="Date of Birth"
      value={birthday}
      onChange={(e) => setBirthdate(e.target.value)}
      min-date={minDate.toISOString().split('T')[0]}
      max-date={maxDate.toISOString().split('T')[0]}
      default-picker-date={maxDate.toISOString().split('T')[0]}
      instructional-text="You must be at least 13 years old"
      required
    />
  );
};
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support for input and calendar
- **Screen Reader Support**: Proper ARIA labeling and announcements
- **Date Validation**: Clear validation messages for invalid dates
- **Focus Management**: Predictable focus behavior between input and calendar
- **High Contrast**: Full high contrast mode support
- **Localization**: Supports multiple locales and date formats
- **Error Announcements**: Live regions for validation feedback

## Best Practices

1. **Clear Labels**: Always provide descriptive labels
2. **Format Indication**: Show expected date format in placeholder
3. **Validation**: Provide immediate feedback for invalid dates
4. **Date Constraints**: Set appropriate min/max dates for context
5. **Localization**: Use appropriate locale for target audience
6. **Error Messages**: Provide clear, actionable error messages
7. **Default Values**: Consider setting sensible default dates

## Advanced Usage

### Custom Date Format Validation
```typescript
// React
export const CustomValidationDatePicker = () => {
  const [date, setDate] = useState('');
  const [error, setError] = useState('');
  
  const validateBusinessDay = (dateString: string) => {
    if (!dateString) return '';
    
    const date = new Date(dateString);
    const dayOfWeek = date.getDay();
    
    if (dayOfWeek === 0 || dayOfWeek === 6) {
      return 'Please select a business day (Monday-Friday)';
    }
    
    return '';
  };
  
  return (
    <SafDatePicker
      label="Meeting Date"
      value={date}
      onChange={(e) => {
        const value = e.target.value;
        setDate(value);
        setError(validateBusinessDay(value));
      }}
      invalid={!!error}
      validation-message={error}
      instructional-text="Business days only"
    />
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  eventDate: string;
}

export const HookFormDatePicker = () => {
  const { control, handleSubmit } = useForm<FormData>();
  
  return (
    <form onSubmit={handleSubmit(console.log)}>
      <Controller
        name="eventDate"
        control={control}
        rules={{
          required: 'Event date is required',
          validate: value => {
            const date = new Date(value);
            const today = new Date();
            return date > today || 'Event date must be in the future';
          }
        }}
        render={({ field, fieldState }) => (
          <SafDatePicker
            {...field}
            label="Event Date"
            min-date={new Date().toISOString().split('T')[0]}
            invalid={!!fieldState.error}
            validation-message={fieldState.error?.message}
            required
          />
        )}
      />
    </form>
  );
};
```

## Notes

- Combines masked text input with calendar popup
- Supports full localization and custom date formats
- Provides comprehensive date validation and constraints
- Implements accessibility best practices
- Integrates seamlessly with form validation libraries
- Auto-correction helps users enter valid dates
