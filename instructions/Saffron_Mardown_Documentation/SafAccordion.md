# SafAccordion

A collapsible content container component that allows users to show and hide sections of related information.

## Usage

```html
<saf-accordion expand-mode="single">
  <saf-accordion-item>
    <span slot="heading">Section 1</span>
    <p>Content for the first section goes here.</p>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Section 2</span>
    <p>Content for the second section goes here.</p>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Section 3</span>
    <p>Content for the third section goes here.</p>
  </saf-accordion-item>
</saf-accordion>
```

## API

### SafAccordion

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `expand-mode` | `'single' \| 'multi'` | `'multi'` | Controls how many accordion items can be expanded at once. 'single' allows only one item to be expanded, 'multi' allows multiple items to be expanded simultaneously |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `change` | `CustomEvent` | Fires when an accordion item is expanded or collapsed |

#### Slots

| Name | Description |
|------|-------------|
| default | Container for accordion items |

### SafAccordionItem

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the accordion item is expanded |
| `disabled` | `boolean` | `false` | Whether the accordion item is disabled |
| `heading-level` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `2` | The heading level for accessibility (affects aria-level) |
| `heading-size` | `'fill' \| 'hug'` | `'fill'` | Whether the heading element should fill available width or hug its content |
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |
| `id` | `string` | auto-generated | The item ID (auto-generated if not provided) |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `toggle` | `CustomEvent` | Fires when the accordion item is toggled (used internally by parent accordion) |
| `click` | `CustomEvent` | Fires when the accordion item button is clicked (deprecated, will be removed in v4) |

#### Slots

| Name | Description |
|------|-------------|
| `heading` | Content for the accordion item heading/button |
| default | Content that is shown/hidden when the item is expanded/collapsed |
| `start` | Content positioned before the heading content |
| `end` | Content positioned after the heading content |
| `expanded-icon` | Custom icon to show when the item is expanded (defaults to chevron-up) |
| `collapsed-icon` | Custom icon to show when the item is collapsed (defaults to chevron-down) |

## Examples

### Basic Accordion

```html
<saf-accordion>
  <saf-accordion-item>
    <span slot="heading">Personal Information</span>
    <div>
      <p>Name: John Doe</p>
      <p>Email: john.doe@example.com</p>
      <p>Phone: (555) 123-4567</p>
    </div>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Address Information</span>
    <div>
      <p>123 Main Street</p>
      <p>Anytown, ST 12345</p>
    </div>
  </saf-accordion-item>
</saf-accordion>
```

### Single Expand Mode

```html
<saf-accordion expand-mode="single">
  <saf-accordion-item>
    <span slot="heading">Option 1</span>
    <p>Only one item can be expanded at a time in single mode.</p>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Option 2</span>
    <p>Expanding this will collapse other items.</p>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Option 3</span>
    <p>This maintains focus and keyboard accessibility.</p>
  </saf-accordion-item>
</saf-accordion>
```

### Pre-expanded Item

```html
<saf-accordion>
  <saf-accordion-item expanded>
    <span slot="heading">Already Expanded</span>
    <p>This item starts in the expanded state.</p>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Click to Expand</span>
    <p>This item starts collapsed.</p>
  </saf-accordion-item>
</saf-accordion>
```

### With Custom Icons

```html
<saf-accordion>
  <saf-accordion-item>
    <span slot="heading">Custom Icons</span>
    <saf-icon slot="expanded-icon" icon-name="minus" appearance="solid"></saf-icon>
    <saf-icon slot="collapsed-icon" icon-name="plus" appearance="solid"></saf-icon>
    <p>This accordion item uses custom expand/collapse icons.</p>
  </saf-accordion-item>
</saf-accordion>
```

### With Start/End Content

```html
<saf-accordion>
  <saf-accordion-item>
    <saf-icon slot="start" icon-name="user" appearance="solid"></saf-icon>
    <span slot="heading">User Profile</span>
    <saf-badge slot="end" appearance="accent">New</saf-badge>
    <div>
      <p>User profile information and settings.</p>
    </div>
  </saf-accordion-item>
</saf-accordion>
```

### Disabled Item

```html
<saf-accordion>
  <saf-accordion-item>
    <span slot="heading">Available Option</span>
    <p>This item can be expanded normally.</p>
  </saf-accordion-item>
  <saf-accordion-item disabled>
    <span slot="heading">Disabled Option</span>
    <p>This content cannot be accessed.</p>
  </saf-accordion-item>
</saf-accordion>
```

### Different Heading Levels

```html
<saf-accordion>
  <saf-accordion-item heading-level="3">
    <span slot="heading">Level 3 Heading</span>
    <p>This accordion item has a heading level of 3 for proper document structure.</p>
  </saf-accordion-item>
  <saf-accordion-item heading-level="4">
    <span slot="heading">Level 4 Heading</span>
    <p>This accordion item has a heading level of 4.</p>
  </saf-accordion-item>
</saf-accordion>
```

### Compact Density

```html
<saf-accordion>
  <saf-accordion-item density="compact">
    <span slot="heading">Compact Item</span>
    <p>This accordion item uses compact spacing.</p>
  </saf-accordion-item>
  <saf-accordion-item density="spacious">
    <span slot="heading">Spacious Item</span>
    <p>This accordion item uses spacious spacing.</p>
  </saf-accordion-item>
</saf-accordion>
```

### Event Handling

```html
<saf-accordion id="my-accordion">
  <saf-accordion-item>
    <span slot="heading">Click Me</span>
    <p>Check the console for change events.</p>
  </saf-accordion-item>
</saf-accordion>

<script>
  const accordion = document.getElementById('my-accordion');
  accordion.addEventListener('change', (event) => {
    console.log('Accordion changed:', event.detail);
  });
</script>
```

### Complex Content

```html
<saf-accordion expand-mode="single">
  <saf-accordion-item>
    <span slot="heading">Form Section</span>
    <form>
      <saf-text-field label="Name" required></saf-text-field>
      <saf-text-field label="Email" type="email"></saf-text-field>
      <saf-button appearance="accent">Submit</saf-button>
    </form>
  </saf-accordion-item>
  <saf-accordion-item>
    <span slot="heading">Data Table</span>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Value</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Item 1</td>
          <td>100</td>
        </tr>
        <tr>
          <td>Item 2</td>
          <td>200</td>
        </tr>
      </tbody>
    </table>
  </saf-accordion-item>
</saf-accordion>
```

## Framework Integration

### React

```jsx
import { SafAccordion, SafAccordionItem } from '@saffron/core-components-react';

function MyComponent() {
  const handleAccordionChange = (event) => {
    console.log('Accordion changed:', event.detail);
  };

  return (
    <SafAccordion expandMode="single" onChange={handleAccordionChange}>
      <SafAccordionItem>
        <span slot="heading">Section 1</span>
        <div>
          <p>React content for section 1</p>
        </div>
      </SafAccordionItem>
      <SafAccordionItem disabled>
        <span slot="heading">Disabled Section</span>
        <div>
          <p>This section is disabled</p>
        </div>
      </SafAccordionItem>
    </SafAccordion>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-accordion-demo',
  template: `
    <saf-accordion expand-mode="single" (change)="onAccordionChange($event)">
      <saf-accordion-item [expanded]="true">
        <span slot="heading">Angular Section</span>
        <div>
          <p>Angular content goes here</p>
        </div>
      </saf-accordion-item>
      <saf-accordion-item [disabled]="isDisabled">
        <span slot="heading">Conditional Section</span>
        <div>
          <p>This section can be conditionally disabled</p>
        </div>
      </saf-accordion-item>
    </saf-accordion>
  `
})
export class AccordionDemoComponent {
  isDisabled = false;

  onAccordionChange(event: CustomEvent) {
    console.log('Accordion changed:', event.detail);
  }
}
```

## Accessibility Features

- **ARIA Accordion Pattern**: Implements the WAI-ARIA accordion pattern with proper roles and states
- **Keyboard Navigation**: 
  - `Enter` or `Space`: Toggle expanded/collapsed state
  - `Arrow Up/Down`: Navigate between accordion items
  - `Home/End`: Move to first/last accordion item
- **Screen Reader Support**: Proper labeling with `aria-expanded`, `aria-controls`, and `aria-labelledby`
- **Focus Management**: Maintains focus on accordion buttons for keyboard users
- **Heading Levels**: Configurable heading levels for proper document structure

## Best Practices

1. **Use semantic heading content**: Place meaningful text in the heading slot
2. **Set appropriate heading levels**: Use `heading-level` to maintain document outline
3. **Consider expand mode**: Use `single` mode for mutually exclusive content, `multi` for independent sections
4. **Provide context**: Include icons or badges in start/end slots for additional context
5. **Handle long content**: Accordion items can contain complex content including forms and tables
6. **Test keyboard navigation**: Ensure all functionality is accessible via keyboard
7. **Use consistent density**: Apply density settings consistently across related accordions

## Related Components

- `saf-collapsible`: For simpler show/hide functionality
- `saf-details`: For disclosure widgets
- `saf-tabs`: For switching between content panels
- `saf-card`: For grouped content that doesn't need collapse functionality
