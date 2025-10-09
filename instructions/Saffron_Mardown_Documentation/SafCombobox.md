# SafCombobox - Advanced Select Component

## Overview
`SafCombobox` is a sophisticated dropdown component that combines an input field with a listbox. It supports single/multiple selection, searching, virtualization, remote data loading, and extensive customization options.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `value` | `string` | `''` | Current selected value(s) |
| `placeholder` | `string` | `undefined` | Placeholder text for input |
| `label` | `string` | `undefined` | Label text for the combobox |
| `required` | `boolean` | `false` | Whether selection is required |
| `disabled` | `boolean` | `false` | Whether combobox is disabled |
| `invalid` | `boolean` | `false` | Whether combobox is in error state |
| `is-success` | `boolean` | `false` | Whether combobox is in success state |
| `multiple` | `boolean` | `false` | Enable multiple selection mode |
| `clearable` | `boolean` | `false` | Show clear button |
| `loading` | `boolean` | `false` | Show loading state |
| `open` | `boolean` | `false` | Whether listbox is open |
| `search-offline` | `boolean` | `true` | Enable client-side filtering |
| `search-mode` | `'includes' \| 'startsWith'` | `'includes'` | Search algorithm mode |
| `autocomplete` | `boolean` | `true` | Enable autocomplete functionality |
| `browser-autocomplete` | `string` | `undefined` | Native autocomplete attribute |
| `open-on-focus` | `boolean` | `false` | Open listbox on input focus |
| `close-on-select` | `boolean` | `!multiple` | Close listbox after selection |
| `clear-on-escape` | `boolean` | `false` | Clear on escape key |
| `virtualized` | `boolean` | `false` | Enable virtualization for large lists |
| `estimated-item-height` | `number` | `40` | Height estimate for virtualized items |
| `virtualization-padding` | `number` | `3` | Buffer items for virtualization |
| `density` | `'compact' \| 'standard'` | `'standard'` | Size density |
| `validation-message` | `string` | `undefined` | Error/success message |
| `instructional-text` | `string` | `undefined` | Help text |
| `empty-option-text` | `string` | `undefined` | Text when no options available |

### Slots
| Slot | Description |
|------|-------------|
| (default) | Options to display in the listbox |
| `start` | Content before the input field |
| `end` | Content after the input field |
| `clear` | Custom clear button |
| `loading` | Custom loading indicator |
| `chips` | Custom chip rendering for multiple mode |
| `success` | Custom success validation feedback |
| `error` | Custom error validation feedback |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `input` | `CustomEvent<string>` | Fired when user types in input |
| `change` | `CustomEvent<string \| string[]>` | Fired when selection changes |
| `open` | `CustomEvent<void>` | Fired when listbox opens |
| `close` | `CustomEvent<void>` | Fired when listbox closes |
| `clear` | `CustomEvent<void>` | Fired when clear button is clicked |
| `scroll-end` | `CustomEvent<void>` | Fired when listbox scrolled to end |

### Methods
| Method | Description |
|--------|-------------|
| `focus()` | Focus the input element |
| `blur()` | Remove focus from input |
| `open()` | Open the listbox |
| `close()` | Close the listbox |
| `selectValue(value)` | Programmatically select a value |
| `deselectValue(value)` | Programmatically deselect a value |
| `clearSelection()` | Clear all selections |
| `setAutocomplete(text)` | Set autocomplete text |

## Usage Examples

### Basic Single Selection
```typescript
// React
import { SafCombobox, SafOption } from '@saffron/react';

export const BasicCombobox = () => {
  const [value, setValue] = useState('');
  
  return (
    <SafCombobox
      label="Choose Option"
      value={value}
      onChange={(e) => setValue(e.target.value)}
      placeholder="Select an option..."
    >
      <SafOption value="apple">Apple</SafOption>
      <SafOption value="banana">Banana</SafOption>
      <SafOption value="cherry">Cherry</SafOption>
    </SafCombobox>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-combobox
      label="Choose Option"
      [value]="value"
      (change)="onSelectionChange($event)"
      placeholder="Select an option...">
      <saf-option value="apple">Apple</saf-option>
      <saf-option value="banana">Banana</saf-option>
      <saf-option value="cherry">Cherry</saf-option>
    </saf-combobox>
  `
})
export class BasicComboboxComponent {
  value = '';
  onSelectionChange(event: CustomEvent<string>) {
    this.value = event.detail;
  }
}
```

### Multiple Selection with Chips
```typescript
// React
export const MultipleCombobox = () => {
  const [values, setValues] = useState<string[]>([]);
  
  return (
    <SafCombobox
      label="Choose Multiple"
      multiple
      value={values}
      onChange={(e) => setValues(e.target.value)}
      clearable
    >
      <SafOption value="js">JavaScript</SafOption>
      <SafOption value="ts">TypeScript</SafOption>
      <SafOption value="py">Python</SafOption>
      <SafOption value="java">Java</SafOption>
      <SafOption value="csharp">C#</SafOption>
    </SafCombobox>
  );
};
```

### Remote Data with Loading
```typescript
// React
export const RemoteCombobox = () => {
  const [options, setOptions] = useState([]);
  const [loading, setLoading] = useState(false);
  const [query, setQuery] = useState('');
  
  useEffect(() => {
    if (query.length < 2) return;
    
    setLoading(true);
    fetchOptions(query).then(data => {
      setOptions(data);
      setLoading(false);
    });
  }, [query]);
  
  return (
    <SafCombobox
      label="Search Users"
      search-offline={false}
      loading={loading}
      onInput={(e) => setQuery(e.target.value)}
      placeholder="Type to search users..."
    >
      {options.map(user => (
        <SafOption key={user.id} value={user.id}>
          {user.name}
        </SafOption>
      ))}
    </SafCombobox>
  );
};
```

### Virtualized Large Dataset
```typescript
// React
export const VirtualizedCombobox = () => {
  const largeDataset = useMemo(() => 
    Array.from({ length: 10000 }, (_, i) => ({
      value: `item-${i}`,
      label: `Item ${i + 1}`
    })), []
  );
  
  return (
    <SafCombobox
      label="Large Dataset"
      virtualized
      estimated-item-height={40}
      virtualization-padding={5}
      placeholder="Search in 10,000 items..."
    >
      {largeDataset.map(item => (
        <SafOption key={item.value} value={item.value}>
          {item.label}
        </SafOption>
      ))}
    </SafCombobox>
  );
};
```

### Custom Start/End Slots
```typescript
// React
export const ComboboxWithSlots = () => {
  return (
    <SafCombobox label="Search with Icon" clearable>
      <saf-icon icon-name="search" slot="start" />
      <SafOption value="option1">Option 1</SafOption>
      <SafOption value="option2">Option 2</SafOption>
      <saf-button slot="end" appearance="ghost">
        Advanced
      </saf-button>
    </SafCombobox>
  );
};
```

### Validation and Error States
```typescript
// React
export const ValidatedCombobox = () => {
  const [value, setValue] = useState('');
  const [error, setError] = useState('');
  
  const validate = (selectedValue: string) => {
    if (!selectedValue) {
      setError('Selection is required');
    } else {
      setError('');
    }
  };
  
  return (
    <SafCombobox
      label="Required Selection"
      value={value}
      onChange={(e) => {
        setValue(e.target.value);
        validate(e.target.value);
      }}
      required
      invalid={!!error}
      validation-message={error}
      instructional-text="Please select an option from the list"
    >
      <SafOption value="">-- Select Option --</SafOption>
      <SafOption value="low">Low Priority</SafOption>
      <SafOption value="medium">Medium Priority</SafOption>
      <SafOption value="high">High Priority</SafOption>
    </SafCombobox>
  );
};
```

## Accessibility Features

- **ARIA Combobox Pattern**: Implements WAI-ARIA combobox specification
- **Keyboard Navigation**: Full arrow key, Enter, Escape, Tab support
- **Screen Reader Support**: Proper announcements for selections and state changes
- **Focus Management**: Predictable focus behavior between input and options
- **High Contrast**: Full high contrast mode support
- **Option Highlighting**: Visual and programmatic indication of focused options
- **Live Regions**: Dynamic content changes announced to assistive technology

## Best Practices

1. **Performance**: Use virtualization for lists over 100 items
2. **Search**: Implement debouncing for remote search queries
3. **Labels**: Always provide descriptive labels
4. **Loading States**: Show loading indicators for async operations
5. **Error Handling**: Provide clear validation messages
6. **Empty States**: Handle and communicate empty option lists
7. **Keyboard UX**: Ensure all functionality works via keyboard

## Advanced Usage

### Custom Search Mode
```typescript
// React
export const CustomSearchCombobox = () => {
  const [options, setOptions] = useState(allOptions);
  const [query, setQuery] = useState('');
  
  const customSearch = (query: string) => {
    // Custom search logic - fuzzy matching, multiple fields, etc.
    return allOptions.filter(option => 
      option.name.includes(query) || 
      option.category.includes(query) ||
      option.tags.some(tag => tag.includes(query))
    );
  };
  
  useEffect(() => {
    setOptions(customSearch(query));
  }, [query]);
  
  return (
    <SafCombobox
      label="Custom Search"
      search-offline={false}
      onInput={(e) => setQuery(e.target.value)}
    >
      {options.map(option => (
        <SafOption key={option.id} value={option.id}>
          {option.name} - {option.category}
        </SafOption>
      ))}
    </SafCombobox>
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  languages: string[];
}

export const HookFormCombobox = () => {
  const { control, handleSubmit } = useForm<FormData>();
  
  return (
    <form onSubmit={handleSubmit(console.log)}>
      <Controller
        name="languages"
        control={control}
        rules={{ required: 'Please select at least one language' }}
        render={({ field, fieldState }) => (
          <SafCombobox
            {...field}
            label="Programming Languages"
            multiple
            clearable
            invalid={!!fieldState.error}
            validation-message={fieldState.error?.message}
          >
            <SafOption value="javascript">JavaScript</SafOption>
            <SafOption value="typescript">TypeScript</SafOption>
            <SafOption value="python">Python</SafOption>
          </SafCombobox>
        )}
      />
    </form>
  );
};
```

## Notes

- Supports both single and multiple selection modes
- Provides extensive customization through slots and attributes
- Optimized for performance with virtualization support
- Implements full ARIA combobox pattern for accessibility
- Integrates seamlessly with form validation libraries
- Supports both client-side and server-side filtering
