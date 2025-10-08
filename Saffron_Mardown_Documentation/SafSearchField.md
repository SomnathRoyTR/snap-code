# SafSearchField - Search Input Component

## Overview
`SafSearchField` is a specialized input component for search queries. It provides a clear button, optional start/end slots, and supports accessibility, validation, and integration with datalist for suggestions.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `value` | `string` | `undefined` | Current search value |
| `placeholder` | `string` | `undefined` | Placeholder text |
| `readonly` | `boolean` | `false` | Whether field is read-only |
| `disabled` | `boolean` | `false` | Whether field is disabled |
| `required` | `boolean` | `false` | Whether field is required |
| `autofocus` | `boolean` | `false` | Autofocus on page load |
| `maxlength` | `number` | `undefined` | Maximum character length |
| `minlength` | `number` | `undefined` | Minimum character length |
| `pattern` | `string` | `undefined` | Validation regex pattern |
| `size` | `number` | `undefined` | Visual width in characters |
| `list` | `string` | `undefined` | Associated datalist ID |
| `appearance` | `'filled' \| 'outline'` | `'outline'` | Visual style variant |
| `density` | `'compact' \| 'standard'` | `'standard'` | Size density |

### Slots
| Slot | Description |
|------|-------------|
| `start` | Content before the input (icon, label, etc.) |
| `end` | Content after the clear button |
| `clear-button` | Custom clear button |
| `clear-icon` | Custom clear icon |
| (default) | Label or help text |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `change` | `CustomEvent<string>` | Fired when value changes |
| `input` | `CustomEvent<string>` | Fired during input |
| `focus` | `FocusEvent` | Fired when field gains focus |
| `blur` | `FocusEvent` | Fired when field loses focus |
| `clear` | `CustomEvent<void>` | Fired when clear button is pressed |

### Methods
| Method | Description |
|--------|-------------|
| `focus()` | Focus the input element |
| `blur()` | Remove focus from input |
| `select()` | Select all text in input |
| `setCustomValidity(message)` | Set custom validation message |
| `checkValidity()` | Check if input is valid |

## Usage Examples

### Basic Search Field
```typescript
// React
import { SafSearchField } from '@saffron/react';

export const BasicSearch = () => {
  const [query, setQuery] = useState('');
  
  return (
    <SafSearchField
      label="Search"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Type to search..."
      required
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-search-field
      label="Search"
      [value]="query"
      (change)="onQueryChange($event)"
      placeholder="Type to search..."
      required>
    </saf-search-field>
  `
})
export class BasicSearchComponent {
  query = '';
  onQueryChange(event: CustomEvent<string>) {
    this.query = event.detail;
  }
}
```

### Search with Icon and Clear Button
```typescript
// React
export const SearchWithIcon = () => {
  const [query, setQuery] = useState('');
  
  return (
    <SafSearchField
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search products..."
    >
      <saf-icon icon-name="search" slot="start" />
      <saf-icon icon-name="close" slot="clear-icon" />
    </SafSearchField>
  );
};
```

### Search with Suggestions
```typescript
// React
export const SearchWithSuggestions = () => {
  return (
    <>
      <SafSearchField
        label="Search"
        list="suggestions"
        placeholder="Type to search..."
      />
      <datalist id="suggestions">
        <option value="Apple" />
        <option value="Banana" />
        <option value="Cherry" />
        <option value="Date" />
        <option value="Elderberry" />
      </datalist>
    </>
  );
};
```

### Search with Validation
```typescript
// React
export const ValidatedSearch = () => {
  const [query, setQuery] = useState('');
  const [error, setError] = useState('');
  
  const handleChange = (e) => {
    const value = e.target.value;
    setQuery(value);
    if (value.length < 3) {
      setError('Search must be at least 3 characters');
    } else {
      setError('');
    }
  };
  
  return (
    <SafSearchField
      label="Search"
      value={query}
      onChange={handleChange}
      minlength={3}
      error={error}
      required
    />
  );
};
```

### Search with End Slot
```typescript
// React
export const SearchWithEndSlot = () => {
  return (
    <SafSearchField placeholder="Search...">
      <saf-button slot="end" appearance="primary">Go</saf-button>
    </SafSearchField>
  );
};
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support
- **Screen Reader Support**: Proper labeling and state announcements
- **Clear Button**: Accessible clear button with ARIA label
- **Validation Messages**: Clear error messaging for invalid inputs
- **Focus Management**: Appropriate focus indicators and behavior
- **High Contrast**: Full high contrast mode support
- **ARIA Attributes**: Proper ARIA labeling for assistive technologies

## Best Practices

1. **Clear Labels**: Always provide a label for search fields
2. **Minimum Length**: Use minlength for meaningful search queries
3. **Suggestions**: Use datalist for common search terms
4. **Error Handling**: Show clear, actionable error messages
5. **Accessibility**: Ensure clear button and input are accessible
6. **Performance**: Debounce search queries for better performance

## Advanced Usage

### Debounced Search
```typescript
// React
import { useState, useEffect } from 'react';

export const DebouncedSearch = () => {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  
  useEffect(() => {
    const handler = setTimeout(() => {
      // Simulate search API call
      setResults([`Result for "${query}"`]);
    }, 300);
    return () => clearTimeout(handler);
  }, [query]);
  
  return (
    <div>
      <SafSearchField
        label="Search"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Type to search..."
      />
      <ul>
        {results.map((r, i) => <li key={i}>{r}</li>)}
      </ul>
    </div>
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  search: string;
}

export const HookFormSearch = () => {
  const { control, handleSubmit } = useForm<FormData>({
    defaultValues: { search: '' }
  });
  
  const onSubmit = (data: FormData) => {
    console.log('Search:', data.search);
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="search"
        control={control}
        rules={{ required: 'Search is required', minLength: 3 }}
        render={({ field, fieldState }) => (
          <SafSearchField
            {...field}
            label="Search"
            minlength={3}
            error={fieldState.error?.message}
          />
        )}
      />
      <SafButton type="submit" appearance="primary">Search</SafButton>
    </form>
  );
};
```

## Notes

- Provides a clear button for quick input reset
- Supports datalist for search suggestions
- Integrates with native form validation
- Optimized for accessibility and performance
- Supports all standard HTML input attributes where applicable
