# SafCalendar - Calendar Display Component

## Overview
`SafCalendar` is a comprehensive calendar component for date selection and navigation. It provides month/year navigation, date range constraints, localization support, and full keyboard accessibility.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `locale` | `string` | `navigator.language` | Locale for date formatting |
| `format` | `string` | `'MM/DD/YYYY'` | Date format string |
| `selected-date` | `string` | `null` | Currently selected date (yyyy-MM-dd) |
| `min-date` | `string` | `'1900-01-01'` | Minimum selectable date |
| `max-date` | `string` | `'2099-12-31'` | Maximum selectable date |
| `default-picker-date` | `string` | `undefined` | Initial focus date (yyyy-MM-dd) |
| `first-day-of-the-week` | `number` | `0` | Starting day of week (0=Sunday, 6=Saturday) |
| `open` | `boolean` | `false` | Whether calendar is visible |
| `weekdays-short` | `string[]` | `computed` | Custom short weekday names |
| `weekdays-full` | `string[]` | `computed` | Custom full weekday names |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `date-select` | `CustomEvent<string>` | Fired when a date is selected |
| `month-change` | `CustomEvent<{month: number, year: number}>` | Fired when month changes |
| `year-change` | `CustomEvent<number>` | Fired when year changes |

### Methods
| Method | Description |
|--------|-------------|
| `selectDate(date)` | Programmatically select a date |
| `navigateToMonth(month, year)` | Navigate to specific month/year |
| `goToPreviousMonth()` | Navigate to previous month |
| `goToNextMonth()` | Navigate to next month |
| `goToToday()` | Navigate to today's date |

## Usage Examples

### Basic Calendar
```typescript
// React
import { SafCalendar } from '@saffron/react';

export const BasicCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  
  return (
    <SafCalendar
      selected-date={selectedDate}
      onDateSelect={(e) => setSelectedDate(e.detail)}
      open
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-calendar
      [selected-date]="selectedDate"
      (date-select)="onDateSelect($event)"
      [open]="true">
    </saf-calendar>
  `
})
export class BasicCalendarComponent {
  selectedDate = '';
  
  onDateSelect(event: CustomEvent<string>) {
    this.selectedDate = event.detail;
  }
}
```

### Date Range Restricted Calendar
```typescript
// React
export const RestrictedCalendar = () => {
  const [appointmentDate, setAppointmentDate] = useState('');
  
  // Next 30 days only
  const today = new Date();
  const maxDate = new Date();
  maxDate.setDate(today.getDate() + 30);
  
  return (
    <SafCalendar
      selected-date={appointmentDate}
      min-date={today.toISOString().split('T')[0]}
      max-date={maxDate.toISOString().split('T')[0]}
      onDateSelect={(e) => setAppointmentDate(e.detail)}
      open
    />
  );
};
```

### Localized Calendar
```typescript
// React
export const LocalizedCalendar = () => {
  const [locale, setLocale] = useState('en-US');
  const [selectedDate, setSelectedDate] = useState('');
  
  const locales = [
    { value: 'en-US', label: 'English (US)', firstDay: 0 },
    { value: 'en-GB', label: 'English (UK)', firstDay: 1 },
    { value: 'de-DE', label: 'Deutsch', firstDay: 1 },
    { value: 'fr-FR', label: 'Français', firstDay: 1 },
    { value: 'es-ES', label: 'Español', firstDay: 1 }
  ];
  
  const currentLocale = locales.find(l => l.value === locale);
  
  return (
    <div>
      <SafSelect
        label="Language"
        value={locale}
        onChange={(e) => setLocale(e.target.value)}
      >
        {locales.map(loc => (
          <SafOption key={loc.value} value={loc.value}>
            {loc.label}
          </SafOption>
        ))}
      </SafSelect>
      
      <SafCalendar
        locale={locale}
        selected-date={selectedDate}
        first-day-of-the-week={currentLocale?.firstDay}
        onDateSelect={(e) => setSelectedDate(e.detail)}
        open
      />
    </div>
  );
};
```

### Calendar with Month/Year Navigation
```typescript
// React
export const NavigableCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  const [currentMonth, setCurrentMonth] = useState(new Date().getMonth());
  const [currentYear, setCurrentYear] = useState(new Date().getFullYear());
  
  const goToToday = () => {
    const today = new Date();
    setCurrentMonth(today.getMonth());
    setCurrentYear(today.getFullYear());
  };
  
  return (
    <div>
      <div style={{ marginBottom: '16px' }}>
        <SafButton onClick={goToToday} appearance="outline">
          Today
        </SafButton>
        <span style={{ margin: '0 16px' }}>
          {new Date(currentYear, currentMonth).toLocaleDateString('en-US', { 
            month: 'long', 
            year: 'numeric' 
          })}
        </span>
      </div>
      
      <SafCalendar
        selected-date={selectedDate}
        default-picker-date={`${currentYear}-${String(currentMonth + 1).padStart(2, '0')}-01`}
        onDateSelect={(e) => setSelectedDate(e.detail)}
        onMonthChange={(e) => {
          setCurrentMonth(e.detail.month);
          setCurrentYear(e.detail.year);
        }}
        open
      />
    </div>
  );
};
```

### Business Days Only Calendar
```typescript
// React
export const BusinessDaysCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  
  // Custom validation to disable weekends
  const isBusinessDay = (date: string) => {
    const dayOfWeek = new Date(date).getDay();
    return dayOfWeek !== 0 && dayOfWeek !== 6; // Not Sunday or Saturday
  };
  
  const handleDateSelect = (e: CustomEvent<string>) => {
    const date = e.detail;
    if (isBusinessDay(date)) {
      setSelectedDate(date);
    } else {
      // Show error message or prevent selection
      console.log('Please select a business day (Monday-Friday)');
    }
  };
  
  return (
    <SafCalendar
      selected-date={selectedDate}
      onDateSelect={handleDateSelect}
      open
      // Note: Actual weekend disabling would require custom styling
      style={{
        '--weekend-day-opacity': '0.3',
        '--weekend-day-pointer-events': 'none'
      }}
    />
  );
};
```

### Multi-Month Calendar View
```typescript
// React
export const MultiMonthCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  const [baseDate, setBaseDate] = useState(new Date());
  
  const months = Array.from({ length: 3 }, (_, i) => {
    const date = new Date(baseDate);
    date.setMonth(date.getMonth() + i);
    return date;
  });
  
  return (
    <div style={{ display: 'flex', gap: '16px' }}>
      {months.map((month, index) => (
        <SafCalendar
          key={index}
          selected-date={selectedDate}
          default-picker-date={`${month.getFullYear()}-${String(month.getMonth() + 1).padStart(2, '0')}-01`}
          onDateSelect={(e) => setSelectedDate(e.detail)}
          open
        />
      ))}
    </div>
  );
};
```

### Event Calendar
```typescript
// React
export const EventCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  const [events] = useState({
    '2024-01-15': ['Meeting at 10 AM'],
    '2024-01-20': ['Project deadline'],
    '2024-01-25': ['Team lunch', 'Code review']
  });
  
  const hasEvents = (date: string) => events[date]?.length > 0;
  
  return (
    <div>
      <SafCalendar
        selected-date={selectedDate}
        onDateSelect={(e) => setSelectedDate(e.detail)}
        open
        // Custom styling would highlight dates with events
        style={{
          '--event-day-background': '#e3f2fd',
          '--event-day-border': '2px solid #1976d2'
        }}
      />
      
      {selectedDate && events[selectedDate] && (
        <div style={{ marginTop: '16px' }}>
          <h4>Events on {new Date(selectedDate).toLocaleDateString()}</h4>
          <ul>
            {events[selectedDate].map((event, index) => (
              <li key={index}>{event}</li>
            ))}
          </ul>
        </div>
      )}
    </div>
  );
};
```

### Inline Calendar with Form
```typescript
// React
export const InlineFormCalendar = () => {
  const [formData, setFormData] = useState({
    eventName: '',
    eventDate: '',
    eventTime: ''
  });
  
  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    console.log('Event created:', formData);
  };
  
  return (
    <form onSubmit={handleSubmit} style={{ maxWidth: '600px' }}>
      <SafTextField
        label="Event Name"
        value={formData.eventName}
        onChange={(e) => setFormData(prev => ({ 
          ...prev, 
          eventName: e.target.value 
        }))}
        required
      />
      
      <div style={{ margin: '24px 0' }}>
        <label style={{ display: 'block', marginBottom: '8px' }}>
          Select Date
        </label>
        <SafCalendar
          selected-date={formData.eventDate}
          onDateSelect={(e) => setFormData(prev => ({ 
            ...prev, 
            eventDate: e.detail 
          }))}
          min-date={new Date().toISOString().split('T')[0]}
          open
        />
      </div>
      
      <SafTextField
        label="Event Time"
        type="time"
        value={formData.eventTime}
        onChange={(e) => setFormData(prev => ({ 
          ...prev, 
          eventTime: e.target.value 
        }))}
        required
      />
      
      <SafButton type="submit" appearance="primary">
        Create Event
      </SafButton>
    </form>
  );
};
```

## Accessibility Features

- **ARIA Calendar Pattern**: Implements WAI-ARIA calendar specification
- **Keyboard Navigation**: Full arrow key, Enter, Space, Home, End support
- **Screen Reader Support**: Proper date announcements and navigation
- **Focus Management**: Logical focus movement between dates and controls
- **High Contrast**: Full high contrast mode support
- **Date Context**: Clear indication of selected, today, and disabled dates
- **Month/Year Navigation**: Accessible dropdown controls

## Best Practices

1. **Date Constraints**: Set appropriate min/max dates for context
2. **Localization**: Use proper locale for target audience
3. **Initial Focus**: Set default-picker-date for better UX
4. **Event Handling**: Provide immediate feedback for date selection
5. **Validation**: Clearly indicate invalid or disabled dates
6. **Context**: Show current selection and today's date clearly
7. **Responsive**: Consider mobile-friendly layouts

## Advanced Usage

### Custom Date Validation
```typescript
// React
export const ValidatedCalendar = () => {
  const [selectedDate, setSelectedDate] = useState('');
  const [holidays] = useState(['2024-01-01', '2024-07-04', '2024-12-25']);
  
  const isHoliday = (date: string) => holidays.includes(date);
  const isWeekend = (date: string) => {
    const day = new Date(date).getDay();
    return day === 0 || day === 6;
  };
  
  const handleDateSelect = (e: CustomEvent<string>) => {
    const date = e.detail;
    
    if (isHoliday(date)) {
      alert('This is a holiday. Please select a different date.');
      return;
    }
    
    if (isWeekend(date)) {
      alert('Weekend dates are not available. Please select a weekday.');
      return;
    }
    
    setSelectedDate(date);
  };
  
  return (
    <SafCalendar
      selected-date={selectedDate}
      onDateSelect={handleDateSelect}
      open
    />
  );
};
```

### Integration with Date Range
```typescript
// React
export const DateRangeCalendar = () => {
  const [startDate, setStartDate] = useState('');
  const [endDate, setEndDate] = useState('');
  const [selectingEnd, setSelectingEnd] = useState(false);
  
  const handleDateSelect = (e: CustomEvent<string>) => {
    const date = e.detail;
    
    if (!startDate || selectingEnd) {
      if (!startDate) {
        setStartDate(date);
        setSelectingEnd(true);
      } else {
        setEndDate(date);
        setSelectingEnd(false);
      }
    } else {
      // Reset and start new range
      setStartDate(date);
      setEndDate('');
      setSelectingEnd(true);
    }
  };
  
  return (
    <div>
      <p>
        {!startDate ? 'Select start date' : 
         selectingEnd ? 'Select end date' : 
         'Range selected. Click to start new range.'}
      </p>
      <SafCalendar
        selected-date={selectingEnd ? endDate : startDate}
        onDateSelect={handleDateSelect}
        min-date={startDate && selectingEnd ? startDate : undefined}
        open
      />
      {startDate && endDate && (
        <p>Selected range: {startDate} to {endDate}</p>
      )}
    </div>
  );
};
```

## Notes

- Provides full calendar navigation and date selection
- Supports comprehensive localization and formatting
- Implements complete keyboard accessibility
- Allows extensive customization through attributes and styling
- Integrates well with form components and validation
- Optimized for both mouse and keyboard interaction
