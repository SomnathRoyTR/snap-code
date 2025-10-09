# SafAccordionItem Component

## Overview
The `SafAccordionItem` component represents an individual collapsible item within an accordion container. It provides an expandable/collapsible content section with a header that users can interact with to show or hide the associated content. This component is designed to work within `SafAccordion` containers and supports various content types, animations, and accessibility features.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the accordion item is expanded |
| `disabled` | `boolean` | `false` | Whether the accordion item is disabled |
| `expandIcon` | `string` | `'chevron-down'` | Icon name for the expand/collapse indicator |
| `hideIcon` | `boolean` | `false` | Whether to hide the expand/collapse icon |
| `headingLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `3` | Heading level for accessibility |
| `id` | `string` | `undefined` | Unique identifier for the accordion item |
| `startExpanded` | `boolean` | `false` | Whether the item should start in expanded state |
| `onToggle` | `(expanded: boolean) => void` | `undefined` | Callback fired when expansion state changes |
| `onExpand` | `() => void` | `undefined` | Callback fired when item expands |
| `onCollapse` | `() => void` | `undefined` | Callback fired when item collapses |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Content to display in the accordion item |

### Events
- `onToggle`: Fired when the accordion item is expanded or collapsed
- `onExpand`: Fired when the accordion item is expanded
- `onCollapse`: Fired when the accordion item is collapsed
- `onFocus`: Fired when the accordion header receives focus
- `onBlur`: Fired when the accordion header loses focus

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the accordion item is expanded |
| `disabled` | `boolean` | `false` | Whether the accordion item is disabled |
| `expandIcon` | `string` | `'chevron-down'` | Icon name for the expand/collapse indicator |
| `hideIcon` | `boolean` | `false` | Whether to hide the expand/collapse icon |
| `headingLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `3` | Heading level for accessibility |
| `id` | `string` | `undefined` | Unique identifier for the accordion item |
| `startExpanded` | `boolean` | `false` | Whether the item should start in expanded state |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(toggle)` | `EventEmitter<boolean>` | Emitted when expansion state changes |
| `(expand)` | `EventEmitter<void>` | Emitted when item expands |
| `(collapse)` | `EventEmitter<void>` | Emitted when item collapses |
| `(focus)` | `EventEmitter<FocusEvent>` | Emitted when header receives focus |
| `(blur)` | `EventEmitter<FocusEvent>` | Emitted when header loses focus |

### Content Projection
- **`heading` slot**: Header content for the accordion item
- **Default slot**: Body content that expands/collapses
- **`start` slot**: Content at the start of the header (e.g., icons)
- **`end` slot**: Content at the end of the header (before expand icon)

## Usage Examples

### Basic Accordion Item

#### React
```jsx
import { SafAccordion, SafAccordionItem } from '@saffron/core-components';

function BasicExample() {
  return (
    <SafAccordion>
      <SafAccordionItem>
        <div slot="heading">What is Saffron Design System?</div>
        <p>
          Saffron is a comprehensive design system that provides 
          consistent UI components and patterns for building 
          modern web applications.
        </p>
      </SafAccordionItem>
      
      <SafAccordionItem>
        <div slot="heading">How do I get started?</div>
        <div>
          <p>Getting started is easy:</p>
          <ol>
            <li>Install the components package</li>
            <li>Import the components you need</li>
            <li>Follow the documentation examples</li>
          </ol>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem disabled>
        <div slot="heading">Advanced Topics (Coming Soon)</div>
        <p>Advanced documentation is currently being developed.</p>
      </SafAccordionItem>
    </SafAccordion>
  );
}
```

#### Angular
```html
<saf-accordion>
  <saf-accordion-item>
    <div slot="heading">What is Saffron Design System?</div>
    <p>
      Saffron is a comprehensive design system that provides 
      consistent UI components and patterns for building 
      modern web applications.
    </p>
  </saf-accordion-item>
  
  <saf-accordion-item>
    <div slot="heading">How do I get started?</div>
    <div>
      <p>Getting started is easy:</p>
      <ol>
        <li>Install the components package</li>
        <li>Import the components you need</li>
        <li>Follow the documentation examples</li>
      </ol>
    </div>
  </saf-accordion-item>
  
  <saf-accordion-item disabled>
    <div slot="heading">Advanced Topics (Coming Soon)</div>
    <p>Advanced documentation is currently being developed.</p>
  </saf-accordion-item>
</saf-accordion>
```

### Controlled Accordion Items

#### React
```jsx
import { SafAccordion, SafAccordionItem } from '@saffron/core-components';
import { useState } from 'react';

function ControlledExample() {
  const [expandedItems, setExpandedItems] = useState(new Set(['item1']));

  const handleToggle = (itemId, isExpanded) => {
    const newExpanded = new Set(expandedItems);
    if (isExpanded) {
      newExpanded.add(itemId);
    } else {
      newExpanded.delete(itemId);
    }
    setExpandedItems(newExpanded);
  };

  return (
    <SafAccordion multiselectable>
      <SafAccordionItem
        id="item1"
        expanded={expandedItems.has('item1')}
        onToggle={(expanded) => handleToggle('item1', expanded)}
      >
        <div slot="heading">Account Settings</div>
        <div>
          <p>Manage your account preferences and personal information.</p>
          <button>Edit Profile</button>
          <button>Change Password</button>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem
        id="item2"
        expanded={expandedItems.has('item2')}
        onToggle={(expanded) => handleToggle('item2', expanded)}
      >
        <div slot="heading">Notification Preferences</div>
        <div>
          <p>Configure how you receive notifications.</p>
          <label>
            <input type="checkbox" /> Email notifications
          </label>
          <label>
            <input type="checkbox" /> Push notifications
          </label>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem
        id="item3"
        expanded={expandedItems.has('item3')}
        onToggle={(expanded) => handleToggle('item3', expanded)}
      >
        <div slot="heading">Privacy Settings</div>
        <div>
          <p>Control your privacy and data sharing preferences.</p>
          <button>Manage Data</button>
          <button>Download Data</button>
        </div>
      </SafAccordionItem>
    </SafAccordion>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-controlled-accordion',
  template: `
    <saf-accordion multiselectable>
      <saf-accordion-item
        id="item1"
        [expanded]="expandedItems.has('item1')"
        (toggle)="handleToggle('item1', $event)"
      >
        <div slot="heading">Account Settings</div>
        <div>
          <p>Manage your account preferences and personal information.</p>
          <button>Edit Profile</button>
          <button>Change Password</button>
        </div>
      </saf-accordion-item>
      
      <saf-accordion-item
        id="item2"
        [expanded]="expandedItems.has('item2')"
        (toggle)="handleToggle('item2', $event)"
      >
        <div slot="heading">Notification Preferences</div>
        <div>
          <p>Configure how you receive notifications.</p>
          <label>
            <input type="checkbox" /> Email notifications
          </label>
          <label>
            <input type="checkbox" /> Push notifications
          </label>
        </div>
      </saf-accordion-item>
      
      <saf-accordion-item
        id="item3"
        [expanded]="expandedItems.has('item3')"
        (toggle)="handleToggle('item3', $event)"
      >
        <div slot="heading">Privacy Settings</div>
        <div>
          <p>Control your privacy and data sharing preferences.</p>
          <button>Manage Data</button>
          <button>Download Data</button>
        </div>
      </saf-accordion-item>
    </saf-accordion>
  `
})
export class ControlledAccordionComponent {
  expandedItems = new Set(['item1']);

  handleToggle(itemId: string, isExpanded: boolean) {
    if (isExpanded) {
      this.expandedItems.add(itemId);
    } else {
      this.expandedItems.delete(itemId);
    }
    this.expandedItems = new Set(this.expandedItems);
  }
}
```

### Rich Header Content with Icons

#### React
```jsx
import { SafAccordion, SafAccordionItem, SafIcon, SafBadge } from '@saffron/core-components';

function RichHeaderExample() {
  return (
    <SafAccordion>
      <SafAccordionItem startExpanded>
        <div slot="start">
          <SafIcon name="user" />
        </div>
        <div slot="heading">
          <span>User Management</span>
        </div>
        <div slot="end">
          <SafBadge variant="success">5 Active</SafBadge>
        </div>
        <div>
          <p>Manage user accounts, roles, and permissions.</p>
          <ul>
            <li>Add new users</li>
            <li>Assign roles and permissions</li>
            <li>View user activity</li>
            <li>Deactivate accounts</li>
          </ul>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem expandIcon="plus">
        <div slot="start">
          <SafIcon name="chart" />
        </div>
        <div slot="heading">
          <span>Analytics Dashboard</span>
        </div>
        <div slot="end">
          <SafBadge variant="warning">2 Issues</SafBadge>
        </div>
        <div>
          <p>View comprehensive analytics and reporting data.</p>
          <button>View Reports</button>
          <button>Export Data</button>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem hideIcon>
        <div slot="start">
          <SafIcon name="settings" />
        </div>
        <div slot="heading">
          <span>System Configuration</span>
        </div>
        <div slot="end">
          <SafBadge variant="neutral">Stable</SafBadge>
        </div>
        <div>
          <p>Configure system-wide settings and preferences.</p>
          <div>
            <label>
              <input type="checkbox" /> Enable feature flags
            </label>
            <label>
              <input type="checkbox" /> Debug mode
            </label>
          </div>
        </div>
      </SafAccordionItem>
    </SafAccordion>
  );
}
```

#### Angular
```html
<saf-accordion>
  <saf-accordion-item [startExpanded]="true">
    <saf-icon slot="start" name="user"></saf-icon>
    <div slot="heading">
      <span>User Management</span>
    </div>
    <saf-badge slot="end" variant="success">5 Active</saf-badge>
    <div>
      <p>Manage user accounts, roles, and permissions.</p>
      <ul>
        <li>Add new users</li>
        <li>Assign roles and permissions</li>
        <li>View user activity</li>
        <li>Deactivate accounts</li>
      </ul>
    </div>
  </saf-accordion-item>
  
  <saf-accordion-item expandIcon="plus">
    <saf-icon slot="start" name="chart"></saf-icon>
    <div slot="heading">
      <span>Analytics Dashboard</span>
    </div>
    <saf-badge slot="end" variant="warning">2 Issues</saf-badge>
    <div>
      <p>View comprehensive analytics and reporting data.</p>
      <button>View Reports</button>
      <button>Export Data</button>
    </div>
  </saf-accordion-item>
  
  <saf-accordion-item [hideIcon]="true">
    <saf-icon slot="start" name="settings"></saf-icon>
    <div slot="heading">
      <span>System Configuration</span>
    </div>
    <saf-badge slot="end" variant="neutral">Stable</saf-badge>
    <div>
      <p>Configure system-wide settings and preferences.</p>
      <div>
        <label>
          <input type="checkbox" /> Enable feature flags
        </label>
        <label>
          <input type="checkbox" /> Debug mode
        </label>
      </div>
    </div>
  </saf-accordion-item>
</saf-accordion>
```

### Dynamic Accordion with Data

#### React
```jsx
import { SafAccordion, SafAccordionItem, SafIcon, SafSpinner } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicAccordionExample() {
  const [sections, setSections] = useState([]);
  const [loading, setLoading] = useState(true);
  const [expandedSections, setExpandedSections] = useState(new Set());

  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      setSections([
        {
          id: 'section1',
          title: 'Getting Started',
          icon: 'play',
          content: 'Learn the basics of our platform',
          items: ['Installation', 'Configuration', 'First Steps']
        },
        {
          id: 'section2',
          title: 'Advanced Features',
          icon: 'star',
          content: 'Explore advanced functionality',
          items: ['Custom Workflows', 'Integrations', 'API Usage']
        },
        {
          id: 'section3',
          title: 'Troubleshooting',
          icon: 'help',
          content: 'Common issues and solutions',
          items: ['Connection Problems', 'Performance Issues', 'Error Codes']
        }
      ]);
      setLoading(false);
    }, 1000);
  }, []);

  const handleToggle = (sectionId, expanded) => {
    const newExpanded = new Set(expandedSections);
    if (expanded) {
      newExpanded.add(sectionId);
    } else {
      newExpanded.delete(sectionId);
    }
    setExpandedSections(newExpanded);
  };

  if (loading) {
    return <SafSpinner size="medium" />;
  }

  return (
    <SafAccordion>
      {sections.map((section) => (
        <SafAccordionItem
          key={section.id}
          id={section.id}
          expanded={expandedSections.has(section.id)}
          onToggle={(expanded) => handleToggle(section.id, expanded)}
        >
          <div slot="start">
            <SafIcon name={section.icon} />
          </div>
          <div slot="heading">{section.title}</div>
          
          <div>
            <p>{section.content}</p>
            <ul>
              {section.items.map((item, index) => (
                <li key={index}>{item}</li>
              ))}
            </ul>
          </div>
        </SafAccordionItem>
      ))}
    </SafAccordion>
  );
}
```

#### Angular
```typescript
// Component
import { Component, OnInit } from '@angular/core';

interface AccordionSection {
  id: string;
  title: string;
  icon: string;
  content: string;
  items: string[];
}

@Component({
  selector: 'app-dynamic-accordion',
  template: `
    <saf-spinner *ngIf="loading" size="medium"></saf-spinner>
    
    <saf-accordion *ngIf="!loading">
      <saf-accordion-item
        *ngFor="let section of sections"
        [id]="section.id"
        [expanded]="expandedSections.has(section.id)"
        (toggle)="handleToggle(section.id, $event)"
      >
        <saf-icon slot="start" [name]="section.icon"></saf-icon>
        <div slot="heading">{{section.title}}</div>
        
        <div>
          <p>{{section.content}}</p>
          <ul>
            <li *ngFor="let item of section.items">{{item}}</li>
          </ul>
        </div>
      </saf-accordion-item>
    </saf-accordion>
  `
})
export class DynamicAccordionComponent implements OnInit {
  sections: AccordionSection[] = [];
  loading = true;
  expandedSections = new Set<string>();

  ngOnInit() {
    // Simulate API call
    setTimeout(() => {
      this.sections = [
        {
          id: 'section1',
          title: 'Getting Started',
          icon: 'play',
          content: 'Learn the basics of our platform',
          items: ['Installation', 'Configuration', 'First Steps']
        },
        {
          id: 'section2',
          title: 'Advanced Features',
          icon: 'star',
          content: 'Explore advanced functionality',
          items: ['Custom Workflows', 'Integrations', 'API Usage']
        },
        {
          id: 'section3',
          title: 'Troubleshooting',
          icon: 'help',
          content: 'Common issues and solutions',
          items: ['Connection Problems', 'Performance Issues', 'Error Codes']
        }
      ];
      this.loading = false;
    }, 1000);
  }

  handleToggle(sectionId: string, expanded: boolean) {
    if (expanded) {
      this.expandedSections.add(sectionId);
    } else {
      this.expandedSections.delete(sectionId);
    }
    this.expandedSections = new Set(this.expandedSections);
  }
}
```

### Nested Accordion Items

#### React
```jsx
import { SafAccordion, SafAccordionItem } from '@saffron/core-components';

function NestedAccordionExample() {
  return (
    <SafAccordion>
      <SafAccordionItem>
        <div slot="heading">Main Category 1</div>
        <div>
          <p>This category contains subcategories:</p>
          
          <SafAccordion>
            <SafAccordionItem>
              <div slot="heading">Subcategory 1.1</div>
              <p>Content for subcategory 1.1</p>
            </SafAccordionItem>
            
            <SafAccordionItem>
              <div slot="heading">Subcategory 1.2</div>
              <div>
                <p>This has even more nested content:</p>
                <SafAccordion>
                  <SafAccordionItem>
                    <div slot="heading">Sub-subcategory 1.2.1</div>
                    <p>Deeply nested content</p>
                  </SafAccordionItem>
                </SafAccordion>
              </div>
            </SafAccordionItem>
          </SafAccordion>
        </div>
      </SafAccordionItem>
      
      <SafAccordionItem>
        <div slot="heading">Main Category 2</div>
        <div>
          <p>Another main category with different content.</p>
          <ul>
            <li>Simple list item 1</li>
            <li>Simple list item 2</li>
          </ul>
        </div>
      </SafAccordionItem>
    </SafAccordion>
  );
}
```

#### Angular
```html
<saf-accordion>
  <saf-accordion-item>
    <div slot="heading">Main Category 1</div>
    <div>
      <p>This category contains subcategories:</p>
      
      <saf-accordion>
        <saf-accordion-item>
          <div slot="heading">Subcategory 1.1</div>
          <p>Content for subcategory 1.1</p>
        </saf-accordion-item>
        
        <saf-accordion-item>
          <div slot="heading">Subcategory 1.2</div>
          <div>
            <p>This has even more nested content:</p>
            <saf-accordion>
              <saf-accordion-item>
                <div slot="heading">Sub-subcategory 1.2.1</div>
                <p>Deeply nested content</p>
              </saf-accordion-item>
            </saf-accordion>
          </div>
        </saf-accordion-item>
      </saf-accordion>
    </div>
  </saf-accordion-item>
  
  <saf-accordion-item>
    <div slot="heading">Main Category 2</div>
    <div>
      <p>Another main category with different content.</p>
      <ul>
        <li>Simple list item 1</li>
        <li>Simple list item 2</li>
      </ul>
    </div>
  </saf-accordion-item>
</saf-accordion>
```

## Best Practices

1. **Content Organization**: Group related information logically within accordion items
2. **Header Clarity**: Use clear, descriptive headings that indicate the content within
3. **Initial State**: Consider which items should be expanded by default for better UX
4. **Icon Usage**: Use consistent icons that clearly indicate expandable content
5. **Nested Accordions**: Use sparingly and avoid deep nesting that may confuse users
6. **Loading States**: Show loading indicators when content is being fetched dynamically
7. **Keyboard Navigation**: Ensure proper keyboard support for accessibility
8. **Content Length**: Avoid extremely long content that makes scrolling difficult

## Accessibility Considerations

- Use appropriate heading levels for proper document structure
- Implement proper ARIA attributes for screen readers
- Support keyboard navigation (Space/Enter to toggle, Arrow keys to navigate)
- Provide clear focus indicators
- Use semantic HTML structure within content
- Ensure sufficient color contrast for all states
- Announce state changes to assistive technologies

## Related Components

- `SafAccordion`: Container component for accordion items
- `SafIcon`: For header icons and expand/collapse indicators
- `SafBadge`: For status indicators in headers
- `SafButton`: For interactive elements within content
- `SafSpinner`: For loading states in dynamic content

## Notes

- Accordion items must be used within `SafAccordion` containers
- The component handles smooth expand/collapse animations automatically
- Header content should be concise and descriptive
- Content can include any valid HTML or components
- Use controlled mode for complex state management scenarios
- Consider performance implications with large amounts of nested content
