# SafButton

A versatile button component that supports multiple appearances, types, and configurations. SafButton can be used for form submission, user interactions, and navigation actions.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `type` | `'button' \| 'submit' \| 'reset'` | `button` | The button's behavior type |
| `appearance` | `'primary' \| 'secondary' \| 'tertiary' \| 'inline'` | `primary` | Visual appearance variant |
| `shape` | `'rectangle' \| 'circle'` | `rectangle` | Button shape (circle only affects icon buttons) |
| `layout` | `'block' \| undefined` | `undefined` | If set to 'block', expands to full width of container |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `inherit` | Spacing in and around the component |
| `disabled` | `boolean` | `false` | Prevents user interaction with the component |
| `autofocus` | `boolean` | `false` | Determines if element should receive focus on page load |
| `iconOnly` | `boolean` | `false` | Renders as icon-only button with appropriate styling |
| `nestedItem` | `boolean` | `false` | Adds styles for buttons used within other components |
| `formId` | `string` | - | The ID of a form to associate the element to |
| `formaction` | `string` | - | URL that processes the information submitted by the button |
| `formenctype` | `string` | - | Specifies how to encode the form data that is submitted |
| `formmethod` | `string` | - | Specifies the HTTP method used to submit the form |
| `formnovalidate` | `boolean` | `false` | Specifies that form is not to be validated when submitted |
| `formtarget` | `'_self' \| '_blank' \| '_parent' \| '_top'` | - | Indicates where to display the response from submitting the form |
| `a11yAriaDescription` | `string` | - | Additional information for screen readers |
| `a11yAriaControls` | `string` | - | IDs of elements controlled by this button |
| `a11yAriaExpanded` | `'true' \| 'false' \| string` | - | Indicates if controlled element is expanded or collapsed |
| `a11yAriaHaspopup` | `'false' \| 'true' \| 'menu' \| 'listbox' \| 'tree' \| 'grid' \| 'dialog'` | - | Indicates availability of interactive popup element |
| `a11yAriaPressed` | `'true' \| 'false' \| 'mixed' \| string` | - | Current "pressed" state for toggle buttons |
| `ariaSelected` | `'true' \| 'false' \| string` | - | Current "selected" state |

### Examples

#### Basic Usage
```jsx
import { SafButton } from '@saffron/core-components/react';

function BasicButtons() {
  return (
    <div>
      {/* Primary button */}
      <SafButton appearance="primary" onClick={handlePrimaryAction}>
        Primary Action
      </SafButton>
      
      {/* Secondary button */}
      <SafButton appearance="secondary" onClick={handleSecondaryAction}>
        Secondary Action
      </SafButton>
      
      {/* Tertiary button */}
      <SafButton appearance="tertiary" onClick={handleTertiaryAction}>
        Tertiary Action
      </SafButton>
      
      {/* Inline button */}
      <SafButton appearance="inline" onClick={handleInlineAction}>
        Inline Action
      </SafButton>
    </div>
  );
}
```

#### Advanced Usage
```jsx
import { SafButton, SafIcon } from '@saffron/core-components/react';

// Form submission buttons
function FormButtons() {
  return (
    <form onSubmit={handleSubmit}>
      <SafButton type="submit" appearance="primary">
        Submit Form
      </SafButton>
      
      <SafButton type="reset" appearance="secondary">
        Reset Form
      </SafButton>
      
      <SafButton type="button" appearance="tertiary" onClick={handleCancel}>
        Cancel
      </SafButton>
    </form>
  );
}

// Icon buttons
function IconButtons() {
  return (
    <div>
      {/* Button with start icon */}
      <SafButton appearance="primary">
        <SafIcon slot="start" iconName="plus" />
        Add Item
      </SafButton>
      
      {/* Button with end icon */}
      <SafButton appearance="secondary">
        Continue
        <SafIcon slot="end" iconName="arrow-right" />
      </SafButton>
      
      {/* Icon-only buttons */}
      <SafButton 
        iconOnly={true} 
        shape="circle" 
        appearance="tertiary"
        aria-label="Settings"
        a11yAriaDescription="Open settings panel"
      >
        <SafIcon iconName="settings" />
      </SafButton>
      
      <SafButton 
        iconOnly={true} 
        appearance="primary"
        aria-label="Delete"
        a11yAriaDescription="Delete selected item"
      >
        <SafIcon iconName="trash" />
      </SafButton>
    </div>
  );
}

// Different densities and layouts
function ButtonVariations() {
  return (
    <div>
      {/* Different densities */}
      <SafButton density="extra-compact" appearance="primary">
        Extra Compact
      </SafButton>
      
      <SafButton density="compact" appearance="primary">
        Compact
      </SafButton>
      
      <SafButton density="standard" appearance="primary">
        Standard
      </SafButton>
      
      <SafButton density="relaxed" appearance="primary">
        Relaxed
      </SafButton>
      
      {/* Block layout */}
      <SafButton layout="block" appearance="primary">
        Full Width Button
      </SafButton>
    </div>
  );
}

// Toggle button with state
function ToggleButton() {
  const [isPressed, setIsPressed] = useState(false);
  
  return (
    <SafButton
      appearance="secondary"
      a11yAriaPressed={isPressed ? 'true' : 'false'}
      onClick={() => setIsPressed(!isPressed)}
      aria-label={isPressed ? 'Turn off' : 'Turn on'}
    >
      <SafIcon iconName={isPressed ? 'toggle-on' : 'toggle-off'} />
      {isPressed ? 'On' : 'Off'}
    </SafButton>
  );
}

// Dropdown trigger button
function DropdownButton() {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <SafButton
      appearance="secondary"
      a11yAriaHaspopup="menu"
      a11yAriaExpanded={isOpen ? 'true' : 'false'}
      a11yAriaControls="dropdown-menu"
      onClick={() => setIsOpen(!isOpen)}
    >
      Options
      <SafIcon slot="end" iconName="chevron-down" />
    </SafButton>
  );
}

// Disabled and loading states
function ButtonStates() {
  const [loading, setLoading] = useState(false);
  
  const handleAsyncAction = async () => {
    setLoading(true);
    try {
      await performAsyncAction();
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <div>
      {/* Disabled button */}
      <SafButton disabled={true} appearance="primary">
        Disabled Button
      </SafButton>
      
      {/* Loading button */}
      <SafButton 
        disabled={loading} 
        appearance="primary"
        onClick={handleAsyncAction}
      >
        {loading ? (
          <>
            <SafIcon slot="start" iconName="spinner" />
            Loading...
          </>
        ) : (
          'Submit'
        )}
      </SafButton>
    </div>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `type` | `'button' \| 'submit' \| 'reset'` | `button` | The button's behavior type |
| `appearance` | `'primary' \| 'secondary' \| 'tertiary' \| 'inline'` | `primary` | Visual appearance variant |
| `shape` | `'rectangle' \| 'circle'` | `rectangle` | Button shape (circle only affects icon buttons) |
| `layout` | `'block' \| undefined` | `undefined` | If set to 'block', expands to full width of container |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `inherit` | Spacing in and around the component |
| `disabled` | `boolean` | `false` | Prevents user interaction with the component |
| `autofocus` | `boolean` | `false` | Determines if element should receive focus on page load |
| `icon-only` | `boolean` | `false` | Renders as icon-only button with appropriate styling |
| `nested-item` | `boolean` | `false` | Adds styles for buttons used within other components |
| `form` | `string` | - | The ID of a form to associate the element to |
| `formaction` | `string` | - | URL that processes the information submitted by the button |
| `formenctype` | `string` | - | Specifies how to encode the form data that is submitted |
| `formmethod` | `string` | - | Specifies the HTTP method used to submit the form |
| `formnovalidate` | `boolean` | `false` | Specifies that form is not to be validated when submitted |
| `formtarget` | `'_self' \| '_blank' \| '_parent' \| '_top'` | - | Indicates where to display the response from submitting the form |
| `a11y-aria-description` | `string` | - | Additional information for screen readers |
| `a11y-aria-controls` | `string` | - | IDs of elements controlled by this button |
| `a11y-aria-expanded` | `'true' \| 'false' \| string` | - | Indicates if controlled element is expanded or collapsed |
| `a11y-aria-haspopup` | `'false' \| 'true' \| 'menu' \| 'listbox' \| 'tree' \| 'grid' \| 'dialog'` | - | Indicates availability of interactive popup element |
| `a11y-aria-pressed` | `'true' \| 'false' \| 'mixed' \| string` | - | Current "pressed" state for toggle buttons |
| `aria-selected` | `'true' \| 'false' \| string` | - | Current "selected" state |

### Examples

#### Basic Usage
```html
<!-- Primary button -->
<saf-button appearance="primary" (click)="handlePrimaryAction()">
  Primary Action
</saf-button>

<!-- Secondary button -->
<saf-button appearance="secondary" (click)="handleSecondaryAction()">
  Secondary Action
</saf-button>

<!-- Tertiary button -->
<saf-button appearance="tertiary" (click)="handleTertiaryAction()">
  Tertiary Action
</saf-button>

<!-- Inline button -->
<saf-button appearance="inline" (click)="handleInlineAction()">
  Inline Action
</saf-button>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-buttons',
  template: `
    <!-- Template content shown above -->
  `
})
export class BasicButtonsComponent {
  handlePrimaryAction(): void {
    console.log('Primary action clicked');
  }
  
  handleSecondaryAction(): void {
    console.log('Secondary action clicked');
  }
  
  handleTertiaryAction(): void {
    console.log('Tertiary action clicked');
  }
  
  handleInlineAction(): void {
    console.log('Inline action clicked');
  }
}
```

#### Advanced Usage
```html
<!-- Form submission buttons -->
<form (ngSubmit)="handleSubmit()">
  <saf-button type="submit" appearance="primary">
    Submit Form
  </saf-button>
  
  <saf-button type="reset" appearance="secondary">
    Reset Form
  </saf-button>
  
  <saf-button type="button" appearance="tertiary" (click)="handleCancel()">
    Cancel
  </saf-button>
</form>

<!-- Icon buttons -->
<div class="icon-buttons">
  <!-- Button with start icon -->
  <saf-button appearance="primary">
    <saf-icon slot="start" icon-name="plus"></saf-icon>
    Add Item
  </saf-button>
  
  <!-- Button with end icon -->
  <saf-button appearance="secondary">
    Continue
    <saf-icon slot="end" icon-name="arrow-right"></saf-icon>
  </saf-button>
  
  <!-- Icon-only buttons -->
  <saf-button 
    [icon-only]="true" 
    shape="circle" 
    appearance="tertiary"
    aria-label="Settings"
    a11y-aria-description="Open settings panel">
    <saf-icon icon-name="settings"></saf-icon>
  </saf-button>
  
  <saf-button 
    [icon-only]="true" 
    appearance="primary"
    aria-label="Delete"
    a11y-aria-description="Delete selected item">
    <saf-icon icon-name="trash"></saf-icon>
  </saf-button>
</div>

<!-- Different densities and layouts -->
<div class="button-variations">
  <saf-button density="extra-compact" appearance="primary">
    Extra Compact
  </saf-button>
  
  <saf-button density="compact" appearance="primary">
    Compact
  </saf-button>
  
  <saf-button density="standard" appearance="primary">
    Standard
  </saf-button>
  
  <saf-button density="relaxed" appearance="primary">
    Relaxed
  </saf-button>
  
  <saf-button layout="block" appearance="primary">
    Full Width Button
  </saf-button>
</div>

<!-- Toggle button with state -->
<saf-button
  appearance="secondary"
  [a11y-aria-pressed]="isPressed ? 'true' : 'false'"
  (click)="toggleState()"
  [aria-label]="isPressed ? 'Turn off' : 'Turn on'">
  <saf-icon [icon-name]="isPressed ? 'toggle-on' : 'toggle-off'"></saf-icon>
  {{ isPressed ? 'On' : 'Off' }}
</saf-button>

<!-- Dropdown trigger button -->
<saf-button
  appearance="secondary"
  a11y-aria-haspopup="menu"
  [a11y-aria-expanded]="isOpen ? 'true' : 'false'"
  a11y-aria-controls="dropdown-menu"
  (click)="toggleDropdown()">
  Options
  <saf-icon slot="end" icon-name="chevron-down"></saf-icon>
</saf-button>

<!-- Disabled and loading states -->
<div class="button-states">
  <saf-button [disabled]="true" appearance="primary">
    Disabled Button
  </saf-button>
  
  <saf-button 
    [disabled]="loading" 
    appearance="primary"
    (click)="handleAsyncAction()">
    <saf-icon *ngIf="loading" slot="start" icon-name="spinner"></saf-icon>
    {{ loading ? 'Loading...' : 'Submit' }}
  </saf-button>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-buttons',
  template: `
    <!-- Template content shown above -->
  `
})
export class AdvancedButtonsComponent {
  isPressed = false;
  isOpen = false;
  loading = false;
  
  handleSubmit(): void {
    console.log('Form submitted');
  }
  
  handleCancel(): void {
    console.log('Action cancelled');
  }
  
  toggleState(): void {
    this.isPressed = !this.isPressed;
  }
  
  toggleDropdown(): void {
    this.isOpen = !this.isOpen;
  }
  
  async handleAsyncAction(): Promise<void> {
    this.loading = true;
    try {
      await this.performAsyncAction();
    } finally {
      this.loading = false;
    }
  }
  
  private async performAsyncAction(): Promise<void> {
    // Simulate async operation
    return new Promise(resolve => setTimeout(resolve, 2000));
  }
}
```

### Best Practices

1. **Button hierarchy and visual weight:**
   - Use `primary` for the main action on a page or section
   - Use `secondary` for secondary actions or alternatives
   - Use `tertiary` for less important actions
   - Use `inline` for text-like actions within content

2. **Button placement and spacing:**
   - Place primary actions in prominent positions (bottom-right in dialogs)
   - Maintain consistent spacing between button groups
   - Use appropriate density for the context

3. **Accessibility guidelines:**
   - Always provide meaningful button text or aria-label for icon-only buttons
   - Use `a11yAriaDescription` for additional context
   - Indicate state changes with appropriate ARIA attributes
   - Ensure sufficient color contrast and touch target size

4. **Icon usage:**
   - Use icons to enhance understanding, not replace clear text
   - Ensure icon-only buttons have proper labels
   - Use consistent icon placement (start/end slots)

5. **Form integration:**
   - Use appropriate `type` attribute for form buttons
   - Handle form validation and submission properly
   - Provide clear feedback for loading states

6. **Responsive considerations:**
   - Use `layout="block"` for full-width buttons on mobile
   - Adjust density based on screen size
   - Ensure buttons remain accessible on touch devices

### Notes

- **Button vs Anchor:** Use SafButton for actions that affect the current page or application state. Use SafAnchor for navigation to different pages or external resources.
- **Form association:** The `formId` prop allows associating the button with a form element outside the current form context.
- **Focus management:** The `autofocus` attribute should be used sparingly and only when it improves the user experience.
- **Loading states:** When performing async operations, disable the button and provide visual feedback to prevent multiple submissions.
- **Nested usage:** The `nestedItem` prop provides special styling when buttons are used within other components like toolbars or card actions.
