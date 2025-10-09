# SafButtonEmbedded

A container component that enables embedding buttons directly within form input components like text fields, creating integrated input-action combinations commonly used for search fields, filters, and quick actions.

## Usage

```html
<saf-button-embedded>
  <saf-text-field label="Search" placeholder="Enter search terms..."></saf-text-field>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

## API

### SafButtonEmbedded

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |

#### Slots

| Name | Description |
|------|-------------|
| default | Container for input field and button components |

#### Behavior

- Automatically applies `embedded-item` attribute to child components for proper styling
- Dynamically adjusts button positioning based on field label presence
- Hides button when input field is in readonly mode
- Supports text fields, number fields, search fields, and date masked input components

## Examples

### Search Field with Button

```html
<saf-button-embedded>
  <saf-text-field 
    label="Search Products" 
    placeholder="Enter product name..."
  ></saf-text-field>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Number Input with Increment Button

```html
<saf-button-embedded>
  <saf-number-field 
    label="Quantity" 
    value="1" 
    min="1" 
    max="99"
  ></saf-number-field>
  <saf-button appearance="neutral" icon-only>
    <saf-icon icon-name="plus" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Date Input with Calendar Button

```html
<saf-button-embedded>
  <saf-date-masked-input 
    label="Select Date" 
    placeholder="MM/DD/YYYY"
  ></saf-date-masked-input>
  <saf-button appearance="subtle" icon-only>
    <saf-icon icon-name="calendar" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Search without Label (Compact)

```html
<saf-button-embedded>
  <saf-search-field 
    placeholder="Search..."
  ></saf-search-field>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Multiple Actions

```html
<saf-button-embedded>
  <saf-text-field 
    label="Filter Results" 
    placeholder="Type to filter..."
  ></saf-text-field>
  <saf-button appearance="subtle" icon-only>
    <saf-icon icon-name="filter" appearance="solid"></saf-icon>
  </saf-button>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Different Button Appearances

```html
<!-- Accent button -->
<saf-button-embedded>
  <saf-text-field placeholder="Primary action..."></saf-text-field>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="send" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>

<!-- Neutral button -->
<saf-button-embedded>
  <saf-text-field placeholder="Secondary action..."></saf-text-field>
  <saf-button appearance="neutral" icon-only>
    <saf-icon icon-name="copy" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>

<!-- Subtle button -->
<saf-button-embedded>
  <saf-text-field placeholder="Subtle action..."></saf-text-field>
  <saf-button appearance="subtle" icon-only>
    <saf-icon icon-name="more-horizontal" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### With Clear and Submit Actions

```html
<saf-button-embedded>
  <saf-text-field 
    label="Email Address" 
    type="email" 
    placeholder="Enter your email..."
    value="user@example.com"
  ></saf-text-field>
  <saf-button appearance="subtle" icon-only>
    <saf-icon icon-name="x" appearance="solid"></saf-icon>
  </saf-button>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="check" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Compact Density

```html
<saf-button-embedded density="compact">
  <saf-text-field 
    label="Compact Search" 
    placeholder="Search..."
  ></saf-text-field>
  <saf-button appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Readonly State (Button Hidden)

```html
<saf-button-embedded>
  <saf-text-field 
    label="Read Only Field" 
    value="This field is readonly"
    readonly
  ></saf-text-field>
  <saf-button appearance="accent" icon-only>
    <!-- This button will be automatically hidden -->
    <saf-icon icon-name="edit" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>
```

### Form Integration

```html
<form>
  <saf-button-embedded>
    <saf-text-field 
      name="query"
      label="Search Query" 
      placeholder="Enter search terms..."
      required
    ></saf-text-field>
    <saf-button type="submit" appearance="accent" icon-only>
      <saf-icon icon-name="search" appearance="solid"></saf-icon>
    </saf-button>
  </saf-button-embedded>

  <saf-button-embedded>
    <saf-number-field 
      name="limit"
      label="Results Limit" 
      value="10"
      min="1"
      max="100"
    ></saf-number-field>
    <saf-button type="button" appearance="subtle" icon-only>
      <saf-icon icon-name="info" appearance="solid"></saf-icon>
    </saf-button>
  </saf-button-embedded>
</form>
```

### Event Handling

```html
<saf-button-embedded id="search-container">
  <saf-text-field 
    id="search-input"
    placeholder="Type to search..."
  ></saf-text-field>
  <saf-button id="search-button" appearance="accent" icon-only>
    <saf-icon icon-name="search" appearance="solid"></saf-icon>
  </saf-button>
</saf-button-embedded>

<script>
  const searchInput = document.getElementById('search-input');
  const searchButton = document.getElementById('search-button');

  // Handle search button click
  searchButton.addEventListener('click', () => {
    const query = searchInput.value;
    if (query.trim()) {
      console.log('Searching for:', query);
      // Perform search logic here
    }
  });

  // Handle Enter key in input
  searchInput.addEventListener('keydown', (event) => {
    if (event.key === 'Enter') {
      searchButton.click();
    }
  });

  // Live search as user types
  searchInput.addEventListener('input', (event) => {
    const query = event.target.value;
    if (query.length > 2) {
      console.log('Live search:', query);
      // Perform live search logic here
    }
  });
</script>
```

### Advanced Filter Interface

```html
<div style="display: grid; gap: 16px; max-width: 400px;">
  <saf-button-embedded>
    <saf-text-field 
      label="Product Name" 
      placeholder="Filter by name..."
    ></saf-text-field>
    <saf-button appearance="subtle" icon-only>
      <saf-icon icon-name="filter" appearance="solid"></saf-icon>
    </saf-button>
  </saf-button-embedded>

  <saf-button-embedded>
    <saf-number-field 
      label="Min Price" 
      placeholder="0.00"
      step="0.01"
    ></saf-number-field>
    <saf-button appearance="subtle" icon-only>
      <saf-icon icon-name="dollar-sign" appearance="solid"></saf-icon>
    </saf-button>
  </saf-button-embedded>

  <saf-button-embedded>
    <saf-date-masked-input 
      label="Created After" 
      placeholder="MM/DD/YYYY"
    ></saf-date-masked-input>
    <saf-button appearance="subtle" icon-only>
      <saf-icon icon-name="calendar" appearance="solid"></saf-icon>
    </saf-button>
  </saf-button-embedded>

  <saf-button appearance="accent">Apply Filters</saf-button>
</div>
```

## Framework Integration

### React

```jsx
import { SafButtonEmbedded, SafTextField, SafButton, SafIcon } from '@saffron/core-components-react';
import { useState } from 'react';

function SearchComponent() {
  const [searchQuery, setSearchQuery] = useState('');
  const [isSearching, setIsSearching] = useState(false);

  const handleSearch = async () => {
    if (!searchQuery.trim()) return;
    
    setIsSearching(true);
    try {
      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1000));
      console.log('Search results for:', searchQuery);
    } finally {
      setIsSearching(false);
    }
  };

  const handleKeyPress = (event) => {
    if (event.key === 'Enter') {
      handleSearch();
    }
  };

  const handleClear = () => {
    setSearchQuery('');
  };

  return (
    <SafButtonEmbedded>
      <SafTextField
        label="Search Products"
        placeholder="Enter product name..."
        value={searchQuery}
        onChange={(e) => setSearchQuery(e.target.value)}
        onKeyPress={handleKeyPress}
      />
      
      {searchQuery && (
        <SafButton
          appearance="subtle"
          iconOnly
          onClick={handleClear}
        >
          <SafIcon iconName="x" appearance="solid" />
        </SafButton>
      )}
      
      <SafButton
        appearance="accent"
        iconOnly
        disabled={!searchQuery.trim() || isSearching}
        onClick={handleSearch}
      >
        <SafIcon 
          iconName={isSearching ? "loading" : "search"} 
          appearance="solid" 
        />
      </SafButton>
    </SafButtonEmbedded>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-embedded-button-demo',
  template: `
    <saf-button-embedded [density]="density">
      <saf-text-field
        [label]="fieldLabel"
        [placeholder]="placeholder"
        [value]="inputValue"
        (input)="onInputChange($event)"
        (keydown.enter)="onAction()"
      ></saf-text-field>
      
      <saf-button
        [appearance]="buttonAppearance"
        icon-only
        [disabled]="isActionDisabled"
        (click)="onAction()"
      >
        <saf-icon [icon-name]="buttonIcon" appearance="solid"></saf-icon>
      </saf-button>
    </saf-button-embedded>

    <div class="controls" style="margin-top: 16px;">
      <label>
        <input type="checkbox" [(ngModel)]="showLabel">
        Show Label
      </label>
      
      <label>
        Button Appearance:
        <select [(ngModel)]="buttonAppearance">
          <option value="accent">Accent</option>
          <option value="neutral">Neutral</option>
          <option value="subtle">Subtle</option>
        </select>
      </label>
    </div>

    <p *ngIf="lastAction">Last Action: {{ lastAction }}</p>
  `
})
export class EmbeddedButtonDemoComponent {
  inputValue = '';
  density = 'normal';
  buttonAppearance = 'accent';
  buttonIcon = 'search';
  showLabel = true;
  lastAction = '';

  get fieldLabel() {
    return this.showLabel ? 'Search Field' : null;
  }

  get placeholder() {
    return 'Type to search...';
  }

  get isActionDisabled() {
    return !this.inputValue.trim();
  }

  onInputChange(event: any) {
    this.inputValue = event.target.value;
  }

  onAction() {
    if (this.inputValue.trim()) {
      this.lastAction = `Searched for: "${this.inputValue}"`;
      console.log('Action performed with value:', this.inputValue);
    }
  }
}
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support for both input field and embedded buttons
- **Focus Management**: Proper tab order and focus indicators
- **Screen Reader Support**: Button purpose is announced correctly by screen readers
- **ARIA Labels**: Buttons should include appropriate ARIA labels or accessible names
- **Form Integration**: Works seamlessly with form submission and validation

## Best Practices

1. **Icon-Only Buttons**: Use icon-only buttons to save space while maintaining clear meaning
2. **Meaningful Icons**: Choose icons that clearly represent the action being performed
3. **Consistent Placement**: Place primary actions (like search/submit) on the right
4. **Button Grouping**: When using multiple buttons, group related actions together
5. **State Management**: Disable buttons when actions aren't available or during loading
6. **Responsive Design**: Ensure embedded buttons work well on smaller screens
7. **Action Feedback**: Provide appropriate feedback when embedded actions are performed
8. **Form Validation**: Integrate with form validation to show appropriate button states

## Related Components

- `saf-button`: The button component used within the embedded container
- `saf-text-field`: Text input component commonly embedded with buttons
- `saf-search-field`: Search-specific input component for embedded scenarios
- `saf-number-field`: Numeric input component for embedded scenarios
- `saf-date-masked-input`: Date input component for embedded scenarios
