# SafOption Component

The `SafOption` component is a selectable item used within listboxes, comboboxes, and select elements in the Saffron Design System. Built on FAST Element, it implements the ARIA option role and provides comprehensive selection states, value management, and accessibility features.

## Table of Contents

- [Overview](#overview)
- [Component Properties](#component-properties)
- [Events](#events)
- [Methods](#methods)
- [Parts](#parts)
- [Slots](#slots)
- [CSS Custom Properties](#css-custom-properties)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Accessibility](#accessibility)
- [Best Practices](#best-practices)

## Overview

The SafOption component provides a comprehensive implementation of selectable options for various container components. It supports single and multiple selection modes, maintains selection state, and provides proper ARIA attributes for accessibility.

Key Features:
- **Selection Management**: Comprehensive support for selected, checked, and default states
- **Value Handling**: Separate label and value support with automatic text extraction
- **Multi-Selection**: Checkbox indicators for multi-select scenarios
- **Accessibility**: Full ARIA implementation with proper selection states
- **Density Control**: Configurable spacing and sizing
- **Form Integration**: HTMLOptionElement proxy for form compatibility

## Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `checked` | `boolean \| undefined` | `undefined` | The checked state for multiple selection mode |
| `content` | `Node[]` | `[]` | Observable array of default slot content nodes |
| `defaultSelected` | `boolean` | `false` | Default selected state of the option |
| `disabled` | `boolean` | `false` | Disables the option |
| `selected` | `boolean` | `defaultSelected` | Current selected state of the option |
| `selectedAttribute` | `boolean` | `false` | The HTML selected attribute value |
| `value` | `string` | `text` | The value of the option (uses text content if not set) |
| `initialValue` | `string` | `""` | Initial value from HTML attribute |
| `density` | `ComponentDensity` | `inherit` | Controls spacing and sizing |
| `isMultiple` | `boolean` | `false` | Flag indicating if parent allows multiple selection |

### Read-Only Properties

| Property | Type | Description |
|----------|------|-------------|
| `label` | `string` | Returns value or text content for display |
| `text` | `string` | Normalized text content (trimmed whitespace) |
| `form` | `HTMLFormElement \| null` | Associated form element via proxy |
| `dirtyValue` | `boolean` | Tracks if value has been programmatically changed |
| `dirtySelected` | `boolean` | Tracks if selected state has been changed |
| `isSlottedInSafCombobox` | `boolean` | Detects if option is within a SafCombobox |
| `ariaCurrentComputed` | `string \| null` | Computed aria-current for combobox scenarios |

### ARIA Properties

| Property | Type | Description |
|----------|------|-------------|
| `ariaChecked` | `string \| null` | ARIA checked state for multiple selection |
| `ariaPosInSet` | `string \| null` | Position within the option set |
| `ariaSelected` | `string \| null` | ARIA selected state |
| `ariaSetSize` | `string \| null` | Total number of options in set |

## Events

| Event | Bubbles | Cancelable | Detail | Description |
|-------|---------|------------|--------|-------------|
| `contentchange` | `true` | `false` | `null` | Fired when the default slot content changes |

## Methods

### Constructor
```typescript
constructor(
  text?: string,
  value?: string, 
  defaultSelected?: boolean,
  selected?: boolean
)
```

Creates a new Option instance with optional initial values.

### Utility Functions

```typescript
isListboxOption(el: Element): el is Option
```
Type guard to check if an element is a listbox option.

## Parts

| Part | Description |
|------|-------------|
| `root` | The root container div |
| `content` | The content span wrapper |
| `square-check-icon` | Checkbox icon for selected multi-select options |
| `square-icon` | Empty checkbox icon for unselected multi-select options |

## Slots

| Slot | Description |
|------|-------------|
| `start` | Content before the main option text (single-select only) |
| `end` | Content after the main option text |
| `(default)` | The main option content/text |

## CSS Custom Properties

The SafOption component uses the design system's spacing and density tokens:

```css
saf-option {
  /* Density affects internal spacing */
  --density: inherit;
}
```

## React Integration

### Basic Usage

```tsx
import SafOption from '@saffron/react/option';

function MyComponent() {
  return (
    <SafOption value="apple">
      Apple
    </SafOption>
  );
}
```

### With Selection States

```tsx
import SafOption from '@saffron/react/option';

function SelectableOptions() {
  const [selected, setSelected] = useState('apple');
  
  return (
    <div>
      <SafOption 
        value="apple" 
        selected={selected === 'apple'}
        onSelect={(e) => setSelected(e.target.value)}
      >
        Apple
      </SafOption>
      <SafOption 
        value="banana" 
        selected={selected === 'banana'}
        onSelect={(e) => setSelected(e.target.value)}
      >
        Banana
      </SafOption>
    </div>
  );
}
```

### With Start and End Content

```tsx
import SafOption from '@saffron/react/option';
import SafIcon from '@saffron/react/icon';

function OptionWithIcons() {
  return (
    <SafOption value="settings">
      <SafIcon slot="start" iconName="cog" />
      Settings
      <SafIcon slot="end" iconName="external-link" />
    </SafOption>
  );
}
```

### Multi-Select Options

```tsx
import SafOption from '@saffron/react/option';

function MultiSelectOptions() {
  const [checkedItems, setCheckedItems] = useState(['apple', 'banana']);
  
  const handleToggle = (value: string) => {
    setCheckedItems(prev => 
      prev.includes(value) 
        ? prev.filter(item => item !== value)
        : [...prev, value]
    );
  };
  
  return (
    <div>
      {['apple', 'banana', 'orange'].map(fruit => (
        <SafOption
          key={fruit}
          value={fruit}
          checked={checkedItems.includes(fruit)}
          isMultiple={true}
          onClick={() => handleToggle(fruit)}
        >
          {fruit.charAt(0).toUpperCase() + fruit.slice(1)}
        </SafOption>
      ))}
    </div>
  );
}
```

### Disabled Options

```tsx
import SafOption from '@saffron/react/option';

function DisabledOption() {
  return (
    <SafOption value="unavailable" disabled>
      Unavailable Option
    </SafOption>
  );
}
```

## Angular Integration

### Basic Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <saf-option value="apple">
      Apple
    </saf-option>
  `
})
export class ExampleComponent {}
```

### With Property Binding

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-selectable-options',
  template: `
    <div>
      <saf-option 
        *ngFor="let option of options"
        [value]="option.value"
        [selected]="option.value === selectedValue"
        [disabled]="option.disabled"
        (click)="selectOption(option.value)"
      >
        {{ option.label }}
      </saf-option>
    </div>
  `
})
export class SelectableOptionsComponent {
  options = [
    { value: 'apple', label: 'Apple', disabled: false },
    { value: 'banana', label: 'Banana', disabled: false },
    { value: 'orange', label: 'Orange', disabled: true }
  ];
  
  selectedValue = 'apple';
  
  selectOption(value: string) {
    this.selectedValue = value;
  }
}
```

### Multi-Select with NgModel

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-multi-select',
  template: `
    <div>
      <saf-option 
        *ngFor="let option of options"
        [value]="option.value"
        [checked]="isChecked(option.value)"
        [isMultiple]="true"
        (click)="toggleOption(option.value)"
      >
        {{ option.label }}
      </saf-option>
    </div>
  `
})
export class MultiSelectComponent {
  options = [
    { value: 'apple', label: 'Apple' },
    { value: 'banana', label: 'Banana' },
    { value: 'orange', label: 'Orange' }
  ];
  
  selectedValues: string[] = [];
  
  isChecked(value: string): boolean {
    return this.selectedValues.includes(value);
  }
  
  toggleOption(value: string) {
    if (this.isChecked(value)) {
      this.selectedValues = this.selectedValues.filter(v => v !== value);
    } else {
      this.selectedValues = [...this.selectedValues, value];
    }
  }
}
```

### With Density Control

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-density-options',
  template: `
    <div>
      <label>
        Density:
        <select [(ngModel)]="density">
          <option value="tight">Tight</option>
          <option value="normal">Normal</option>
          <option value="loose">Loose</option>
        </select>
      </label>
      
      <saf-option 
        *ngFor="let option of options"
        [value]="option.value"
        [density]="density"
      >
        {{ option.label }}
      </saf-option>
    </div>
  `
})
export class DensityOptionsComponent {
  density = 'normal';
  options = [
    { value: 'option1', label: 'Option 1' },
    { value: 'option2', label: 'Option 2' },
    { value: 'option3', label: 'Option 3' }
  ];
}
```

## Usage Examples

### Basic Single-Select Option

```html
<saf-option value="apple">Apple</saf-option>
```

### Option with Start Icon

```html
<saf-option value="settings">
  <saf-icon slot="start" icon-name="cog"></saf-icon>
  Settings
</saf-option>
```

### Pre-Selected Option

```html
<saf-option value="default" selected>Default Option</saf-option>
```

### Multi-Select Checkbox Option

```html
<saf-option value="feature1" checked is-multiple="true">
  Feature 1
</saf-option>
```

### Disabled Option

```html
<saf-option value="unavailable" disabled>
  Unavailable
</saf-option>
```

### Option with Custom Value

```html
<saf-option value="custom-id">
  Display Text Different from Value
</saf-option>
```

### High Density Option

```html
<saf-option value="compact" density="tight">
  Compact Option
</saf-option>
```

### Option in Combobox Context

```html
<saf-combobox>
  <saf-option value="search-result-1">
    Search Result 1
  </saf-option>
  <saf-option value="search-result-2">
    Search Result 2
  </saf-option>
</saf-combobox>
```

## Accessibility

The SafOption component provides comprehensive accessibility support:

### ARIA Implementation
- **Role**: Always set to `option`
- **aria-selected**: Reflects selection state
- **aria-checked**: Used for multi-selection scenarios
- **aria-disabled**: Reflects disabled state
- **aria-current**: Set for selected combobox options
- **aria-posinset/aria-setsize**: Position within option set

### Keyboard Support
- Relies on parent container for keyboard navigation
- Supports standard option selection patterns
- Maintains focus management through parent components

### Screen Reader Support
- Announces selection states correctly
- Provides clear distinction between single and multi-select modes
- Properly announces disabled states

### Focus Management
- Participates in parent container's focus management
- Visual focus indicators through parent styling
- Maintains focus visibility in all interaction modes

## Best Practices

### Value Management
- Always provide explicit `value` attributes for form submission
- Use meaningful values that identify the option uniquely
- Keep display text and values separate when needed

### Selection States
- Use `selected` for initial state, let parent manage runtime selection
- Implement proper event handling for selection changes
- Consider using `defaultSelected` for form reset scenarios

### Multi-Select Considerations
- Set `isMultiple` appropriately based on parent container
- Use `checked` property instead of `selected` for multi-select
- Provide clear visual indicators for checked state

### Performance
- Avoid frequent changes to content that trigger proxy updates
- Use value-based selection rather than text matching
- Consider virtualization for large option lists

### Accessibility
- Ensure parent containers provide proper ARIA context
- Don't override ARIA properties unless necessary
- Test with screen readers in context of parent components

### Styling
- Use CSS parts for consistent styling across themes
- Respect density settings for spacing consistency
- Ensure sufficient color contrast for all states

The SafOption component is designed to work seamlessly within various container components while providing robust selection management and accessibility features. Always test options within their intended parent containers to ensure proper behavior and accessibility.
