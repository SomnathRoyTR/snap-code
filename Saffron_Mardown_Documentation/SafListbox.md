# SafListbox

An interactive listbox component that allows users to select one or more options from a list. Implements the WAI-ARIA listbox pattern for optimal accessibility.

## Usage

```html
<saf-listbox>
  <saf-option>Option 1</saf-option>
  <saf-option>Option 2</saf-option>
  <saf-option>Option 3</saf-option>
</saf-listbox>
```

## API

### SafListbox

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `multiple` | `boolean` | `false` | Enables multiple selection mode |
| `size` | `number` | - | Maximum number of options to display (enables scrolling) |
| `disabled` | `boolean` | `false` | Whether the listbox is disabled |
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `activeOption` | `Option \| null` | The currently active (focused) option |
| `firstSelectedOption` | `Option \| null` | The first selected option |
| `selectedOptions` | `Option[]` | Array of all selected options |
| `value` | `string \| string[]` | The selected value(s) |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `change` | `CustomEvent` | Fires when the selection changes |
| `input` | `CustomEvent` | Fires during selection changes |

#### Slots

| Name | Description |
|------|-------------|
| default | Container for option elements |

### SafOption

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether this option is selected |
| `disabled` | `boolean` | `false` | Whether this option is disabled |
| `value` | `string` | - | The value associated with this option |
| `checked` | `boolean` | `false` | Whether this option is checked (multi-select mode only) |
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `textContent` | `string` | The text content of the option |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `contentchange` | `CustomEvent` | Fires when the option content changes |

#### Slots

| Name | Description |
|------|-------------|
| default | The option text content |
| `start` | Content positioned before the option text |
| `end` | Content positioned after the option text |

#### Parts

| Name | Description |
|------|-------------|
| `content` | Wraps the option content |

## Examples

### Basic Single Selection

```html
<saf-listbox>
  <saf-option value="red">Red</saf-option>
  <saf-option value="green">Green</saf-option>
  <saf-option value="blue">Blue</saf-option>
  <saf-option value="yellow">Yellow</saf-option>
</saf-listbox>
```

### Multiple Selection

```html
<saf-listbox multiple>
  <saf-option value="apple">Apple</saf-option>
  <saf-option value="banana">Banana</saf-option>
  <saf-option value="orange">Orange</saf-option>
  <saf-option value="grape" checked>Grape</saf-option>
  <saf-option value="mango" checked>Mango</saf-option>
</saf-listbox>
```

### With Size Limit and Scrolling

```html
<saf-listbox size="4">
  <saf-option value="item1">Item 1</saf-option>
  <saf-option value="item2">Item 2</saf-option>
  <saf-option value="item3">Item 3</saf-option>
  <saf-option value="item4">Item 4</saf-option>
  <saf-option value="item5">Item 5</saf-option>
  <saf-option value="item6">Item 6</saf-option>
  <saf-option value="item7">Item 7</saf-option>
  <saf-option value="item8">Item 8</saf-option>
</saf-listbox>
```

### Pre-selected Options

```html
<saf-listbox>
  <saf-option value="option1">Option 1</saf-option>
  <saf-option value="option2" selected>Option 2 (Selected)</saf-option>
  <saf-option value="option3">Option 3</saf-option>
  <saf-option value="option4">Option 4</saf-option>
</saf-listbox>
```

### Disabled Options

```html
<saf-listbox>
  <saf-option value="available1">Available Option 1</saf-option>
  <saf-option value="disabled1" disabled>Disabled Option</saf-option>
  <saf-option value="available2">Available Option 2</saf-option>
  <saf-option value="disabled2" disabled>Another Disabled Option</saf-option>
</saf-listbox>
```

### Options with Icons and Additional Content

```html
<saf-listbox>
  <saf-option value="home">
    <saf-icon slot="start" icon-name="home" appearance="solid"></saf-icon>
    Home
    <saf-badge slot="end" appearance="accent">New</saf-badge>
  </saf-option>
  <saf-option value="profile">
    <saf-icon slot="start" icon-name="user" appearance="solid"></saf-icon>
    Profile
  </saf-option>
  <saf-option value="settings">
    <saf-icon slot="start" icon-name="settings" appearance="solid"></saf-icon>
    Settings
    <saf-icon slot="end" icon-name="chevron-right" appearance="solid"></saf-icon>
  </saf-option>
  <saf-option value="logout">
    <saf-icon slot="start" icon-name="logout" appearance="solid"></saf-icon>
    Logout
  </saf-option>
</saf-listbox>
```

### Compact Density

```html
<saf-listbox density="compact">
  <saf-option value="compact1">Compact Option 1</saf-option>
  <saf-option value="compact2">Compact Option 2</saf-option>
  <saf-option value="compact3">Compact Option 3</saf-option>
</saf-listbox>
```

### Rich Content Options

```html
<saf-listbox size="3">
  <saf-option value="user1">
    <div style="display: flex; align-items: center; gap: 12px;">
      <div style="width: 32px; height: 32px; border-radius: 50%; background: #ddd; display: flex; align-items: center; justify-content: center;">
        👤
      </div>
      <div>
        <div style="font-weight: 600;">John Smith</div>
        <div style="font-size: 0.875rem; color: #666;">john.smith@example.com</div>
      </div>
    </div>
  </saf-option>
  <saf-option value="user2">
    <div style="display: flex; align-items: center; gap: 12px;">
      <div style="width: 32px; height: 32px; border-radius: 50%; background: #ddd; display: flex; align-items: center; justify-content: center;">
        👩
      </div>
      <div>
        <div style="font-weight: 600;">Jane Doe</div>
        <div style="font-size: 0.875rem; color: #666;">jane.doe@example.com</div>
      </div>
    </div>
  </saf-option>
  <saf-option value="user3">
    <div style="display: flex; align-items: center; gap: 12px;">
      <div style="width: 32px; height: 32px; border-radius: 50%; background: #ddd; display: flex; align-items: center; justify-content: center;">
        👨
      </div>
      <div>
        <div style="font-weight: 600;">Bob Johnson</div>
        <div style="font-size: 0.875rem; color: #666;">bob.johnson@example.com</div>
      </div>
    </div>
  </saf-option>
</saf-listbox>
```

### Event Handling

```html
<saf-listbox id="event-listbox">
  <saf-option value="option1">Option 1</saf-option>
  <saf-option value="option2">Option 2</saf-option>
  <saf-option value="option3">Option 3</saf-option>
</saf-listbox>

<p id="selected-value">Selected: None</p>

<script>
  const listbox = document.getElementById('event-listbox');
  const selectedDisplay = document.getElementById('selected-value');

  listbox.addEventListener('change', (event) => {
    selectedDisplay.textContent = `Selected: ${event.target.value || 'None'}`;
  });
</script>
```

### Multiple Selection with Event Handling

```html
<saf-listbox id="multi-listbox" multiple>
  <saf-option value="red">Red</saf-option>
  <saf-option value="green">Green</saf-option>
  <saf-option value="blue">Blue</saf-option>
  <saf-option value="yellow">Yellow</saf-option>
</saf-listbox>

<p id="selected-values">Selected: None</p>

<script>
  const multiListbox = document.getElementById('multi-listbox');
  const selectedValuesDisplay = document.getElementById('selected-values');

  multiListbox.addEventListener('change', (event) => {
    const values = Array.isArray(event.target.value) 
      ? event.target.value.join(', ')
      : event.target.value || 'None';
    selectedValuesDisplay.textContent = `Selected: ${values}`;
  });
</script>
```

### Programmatic Control

```html
<saf-listbox id="programmable-listbox">
  <saf-option value="item1" id="opt1">Item 1</saf-option>
  <saf-option value="item2" id="opt2">Item 2</saf-option>
  <saf-option value="item3" id="opt3">Item 3</saf-option>
  <saf-option value="item4" id="opt4">Item 4</saf-option>
</saf-listbox>

<div style="margin-top: 16px;">
  <saf-button onclick="selectItem('item2')">Select Item 2</saf-button>
  <saf-button onclick="clearSelection()">Clear Selection</saf-button>
  <saf-button onclick="getSelectedValue()">Get Selected</saf-button>
</div>

<script>
  function selectItem(value) {
    const listbox = document.getElementById('programmable-listbox');
    const options = listbox.querySelectorAll('saf-option');
    
    options.forEach(option => {
      option.selected = option.value === value;
    });
  }
  
  function clearSelection() {
    const options = document.querySelectorAll('#programmable-listbox saf-option');
    options.forEach(option => {
      option.selected = false;
    });
  }
  
  function getSelectedValue() {
    const listbox = document.getElementById('programmable-listbox');
    alert(`Selected value: ${listbox.value || 'None'}`);
  }
</script>
```

### Categorized Options

```html
<saf-listbox size="6">
  <saf-option disabled style="font-weight: bold; background: #f5f5f5;">
    — Fruits —
  </saf-option>
  <saf-option value="apple">Apple</saf-option>
  <saf-option value="banana">Banana</saf-option>
  <saf-option value="orange">Orange</saf-option>
  
  <saf-option disabled style="font-weight: bold; background: #f5f5f5;">
    — Vegetables —
  </saf-option>
  <saf-option value="carrot">Carrot</saf-option>
  <saf-option value="broccoli">Broccoli</saf-option>
  <saf-option value="spinach">Spinach</saf-option>
</saf-listbox>
```

## Framework Integration

### React

```jsx
import { SafListbox, SafOption } from '@saffron/core-components-react';
import { useState } from 'react';

function ListboxExample() {
  const [selectedValue, setSelectedValue] = useState('');
  const [multipleValues, setMultipleValues] = useState([]);

  const options = [
    { value: 'react', label: 'React' },
    { value: 'vue', label: 'Vue.js' },
    { value: 'angular', label: 'Angular' },
    { value: 'svelte', label: 'Svelte' }
  ];

  const handleSingleChange = (event) => {
    setSelectedValue(event.target.value);
  };

  const handleMultipleChange = (event) => {
    setMultipleValues(event.target.value);
  };

  return (
    <div>
      <h3>Single Selection</h3>
      <SafListbox value={selectedValue} onChange={handleSingleChange}>
        {options.map(option => (
          <SafOption key={option.value} value={option.value}>
            {option.label}
          </SafOption>
        ))}
      </SafListbox>

      <h3>Multiple Selection</h3>
      <SafListbox multiple value={multipleValues} onChange={handleMultipleChange}>
        {options.map(option => (
          <SafOption key={option.value} value={option.value}>
            {option.label}
          </SafOption>
        ))}
      </SafListbox>
    </div>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-listbox-demo',
  template: `
    <saf-listbox 
      [multiple]="isMultiple" 
      [size]="displaySize"
      (change)="onSelectionChange($event)"
    >
      <saf-option 
        *ngFor="let option of options" 
        [value]="option.value"
        [selected]="selectedValues.includes(option.value)"
        [disabled]="option.disabled"
      >
        <span [innerHTML]="option.label"></span>
      </saf-option>
    </saf-listbox>

    <div class="controls">
      <label>
        <input type="checkbox" [(ngModel)]="isMultiple">
        Multiple Selection
      </label>
      <label>
        Display Size:
        <input type="number" [(ngModel)]="displaySize" min="1" max="10">
      </label>
    </div>

    <p>Selected: {{ selectedValues.join(', ') || 'None' }}</p>
  `
})
export class ListboxDemoComponent {
  isMultiple = false;
  displaySize = 4;
  selectedValues: string[] = [];

  options = [
    { value: 'option1', label: 'First Option', disabled: false },
    { value: 'option2', label: 'Second Option', disabled: false },
    { value: 'option3', label: 'Third Option', disabled: true },
    { value: 'option4', label: 'Fourth Option', disabled: false },
    { value: 'option5', label: 'Fifth Option', disabled: false }
  ];

  onSelectionChange(event: CustomEvent) {
    const value = event.detail?.value || event.target?.value;
    this.selectedValues = Array.isArray(value) ? value : (value ? [value] : []);
  }
}
```

## Accessibility Features

- **ARIA Listbox Pattern**: Implements the complete WAI-ARIA listbox pattern
- **Keyboard Navigation**: 
  - `Arrow Up/Down`: Navigate between options
  - `Home/End`: Move to first/last option
  - `Space`: Select/deselect the focused option
  - `Ctrl+A` (multiple mode): Select all options
  - `Escape`: Clear selection and close focus
- **Screen Reader Support**: Proper labeling with `aria-activedescendant`, `aria-multiselectable`
- **Focus Management**: Clear visual focus indicators and proper focus handling
- **Selection Announcement**: Screen readers announce selection changes

## Best Practices

1. **Option Labeling**: Use clear, descriptive labels for options
2. **Logical Grouping**: Group related options together or use disabled separator options
3. **Reasonable Size**: Use the `size` attribute for long lists to enable scrolling
4. **Consistent Selection Model**: Choose single or multiple selection based on use case
5. **Loading States**: Show appropriate indicators when options are being loaded dynamically
6. **Error States**: Provide clear feedback for validation errors
7. **Responsive Design**: Consider how the listbox will behave on different screen sizes
8. **Performance**: For very large lists, consider virtualization

## Related Components

- `saf-select`: For dropdown-style selection with a collapsed view
- `saf-combobox`: For searchable selection with text input
- `saf-menu`: For action-oriented selections
- `saf-option-group`: For grouping related options (if available)
