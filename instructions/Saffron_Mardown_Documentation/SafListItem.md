# SafListItem Component

## Overview
The `SafListItem` component represents an individual item within a list container. It provides flexible content layout, interactive states, and accessibility features. This component is designed to work within list containers like `SafList` or `SafListBox` and supports various content types including text, icons, actions, and metadata.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the list item is selected |
| `disabled` | `boolean` | `false` | Whether the list item is disabled |
| `active` | `boolean` | `false` | Whether the list item is in an active state |
| `value` | `string \| number` | `undefined` | The value associated with this list item |
| `role` | `'listitem' \| 'option' \| 'menuitem'` | `'listitem'` | The ARIA role for the list item |
| `tabindex` | `number` | `undefined` | The tab index for keyboard navigation |
| `href` | `string` | `undefined` | If provided, renders the item as a link |
| `target` | `string` | `undefined` | Link target when href is provided |
| `onClick` | `(event: MouseEvent) => void` | `undefined` | Click event handler |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Focus event handler |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Blur event handler |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Content to display in the list item |

### Events
- `onClick`: Fired when the list item is clicked
- `onFocus`: Fired when the list item receives focus
- `onBlur`: Fired when the list item loses focus
- `onSelect`: Fired when the list item is selected (in selectable lists)

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the list item is selected |
| `disabled` | `boolean` | `false` | Whether the list item is disabled |
| `active` | `boolean` | `false` | Whether the list item is in an active state |
| `value` | `string \| number` | `undefined` | The value associated with this list item |
| `role` | `'listitem' \| 'option' \| 'menuitem'` | `'listitem'` | The ARIA role for the list item |
| `tabindex` | `number` | `undefined` | The tab index for keyboard navigation |
| `href` | `string` | `undefined` | If provided, renders the item as a link |
| `target` | `string` | `undefined` | Link target when href is provided |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(click)` | `EventEmitter<MouseEvent>` | Emitted when the list item is clicked |
| `(focus)` | `EventEmitter<FocusEvent>` | Emitted when the list item receives focus |
| `(blur)` | `EventEmitter<FocusEvent>` | Emitted when the list item loses focus |
| `(itemSelect)` | `EventEmitter<any>` | Emitted when the list item is selected |

### Content Projection
- **Default slot**: Main content of the list item
- **`start` slot**: Content displayed at the start (e.g., icons, avatars)
- **`end` slot**: Content displayed at the end (e.g., actions, status)

## Usage Examples

### Basic List Item

#### React
```jsx
import { SafList, SafListItem } from '@saffron/core-components';

function BasicExample() {
  return (
    <SafList>
      <SafListItem>Item 1</SafListItem>
      <SafListItem>Item 2</SafListItem>
      <SafListItem disabled>Item 3 (Disabled)</SafListItem>
    </SafList>
  );
}
```

#### Angular
```html
<saf-list>
  <saf-list-item>Item 1</saf-list-item>
  <saf-list-item>Item 2</saf-list-item>
  <saf-list-item disabled>Item 3 (Disabled)</saf-list-item>
</saf-list>
```

### Interactive List with Selection

#### React
```jsx
import { SafList, SafListItem } from '@saffron/core-components';
import { useState } from 'react';

function SelectableList() {
  const [selectedItem, setSelectedItem] = useState(null);

  const handleItemClick = (value) => {
    setSelectedItem(value);
  };

  return (
    <SafList role="listbox">
      <SafListItem 
        role="option"
        value="item1"
        selected={selectedItem === 'item1'}
        onClick={() => handleItemClick('item1')}
      >
        First Item
      </SafListItem>
      <SafListItem 
        role="option"
        value="item2"
        selected={selectedItem === 'item2'}
        onClick={() => handleItemClick('item2')}
      >
        Second Item
      </SafListItem>
      <SafListItem 
        role="option"
        value="item3"
        selected={selectedItem === 'item3'}
        onClick={() => handleItemClick('item3')}
      >
        Third Item
      </SafListItem>
    </SafList>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-selectable-list',
  template: `
    <saf-list role="listbox">
      <saf-list-item 
        role="option"
        [value]="'item1'"
        [selected]="selectedItem === 'item1'"
        (click)="selectItem('item1')"
      >
        First Item
      </saf-list-item>
      <saf-list-item 
        role="option"
        [value]="'item2'"
        [selected]="selectedItem === 'item2'"
        (click)="selectItem('item2')"
      >
        Second Item
      </saf-list-item>
      <saf-list-item 
        role="option"
        [value]="'item3'"
        [selected]="selectedItem === 'item3'"
        (click)="selectItem('item3')"
      >
        Third Item
      </saf-list-item>
    </saf-list>
  `
})
export class SelectableListComponent {
  selectedItem: string | null = null;

  selectItem(value: string) {
    this.selectedItem = value;
  }
}
```

### List Items with Icons and Actions

#### React
```jsx
import { SafList, SafListItem, SafIcon, SafButton } from '@saffron/core-components';

function RichListExample() {
  const handleDelete = (id) => {
    console.log(`Delete item ${id}`);
  };

  const handleEdit = (id) => {
    console.log(`Edit item ${id}`);
  };

  return (
    <SafList>
      <SafListItem>
        <div slot="start">
          <SafIcon name="document" />
        </div>
        <div>
          <h4>Document Title</h4>
          <p>Document description and metadata</p>
        </div>
        <div slot="end">
          <SafButton 
            variant="ghost" 
            size="small"
            onClick={() => handleEdit(1)}
          >
            Edit
          </SafButton>
          <SafButton 
            variant="ghost" 
            size="small"
            onClick={() => handleDelete(1)}
          >
            Delete
          </SafButton>
        </div>
      </SafListItem>
      
      <SafListItem>
        <div slot="start">
          <SafIcon name="folder" />
        </div>
        <div>
          <h4>Folder Name</h4>
          <p>Contains 12 items</p>
        </div>
        <div slot="end">
          <SafButton 
            variant="ghost" 
            size="small"
            onClick={() => handleEdit(2)}
          >
            Edit
          </SafButton>
          <SafButton 
            variant="ghost" 
            size="small"
            onClick={() => handleDelete(2)}
          >
            Delete
          </SafButton>
        </div>
      </SafListItem>
    </SafList>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-rich-list',
  template: `
    <saf-list>
      <saf-list-item>
        <saf-icon slot="start" name="document"></saf-icon>
        <div>
          <h4>Document Title</h4>
          <p>Document description and metadata</p>
        </div>
        <div slot="end">
          <saf-button 
            variant="ghost" 
            size="small"
            (click)="handleEdit(1)"
          >
            Edit
          </saf-button>
          <saf-button 
            variant="ghost" 
            size="small"
            (click)="handleDelete(1)"
          >
            Delete
          </saf-button>
        </div>
      </saf-list-item>
      
      <saf-list-item>
        <saf-icon slot="start" name="folder"></saf-icon>
        <div>
          <h4>Folder Name</h4>
          <p>Contains 12 items</p>
        </div>
        <div slot="end">
          <saf-button 
            variant="ghost" 
            size="small"
            (click)="handleEdit(2)"
          >
            Edit
          </saf-button>
          <saf-button 
            variant="ghost" 
            size="small"
            (click)="handleDelete(2)"
          >
            Delete
          </saf-button>
        </div>
      </saf-list-item>
    </saf-list>
  `
})
export class RichListComponent {
  handleEdit(id: number) {
    console.log(`Edit item ${id}`);
  }

  handleDelete(id: number) {
    console.log(`Delete item ${id}`);
  }
}
```

### Navigational List Items

#### React
```jsx
import { SafList, SafListItem, SafIcon } from '@saffron/core-components';

function NavigationList() {
  return (
    <SafList role="menu">
      <SafListItem 
        role="menuitem"
        href="/dashboard"
        tabindex={0}
      >
        <SafIcon slot="start" name="dashboard" />
        Dashboard
      </SafListItem>
      
      <SafListItem 
        role="menuitem"
        href="/reports"
        tabindex={0}
      >
        <SafIcon slot="start" name="chart" />
        Reports
      </SafListItem>
      
      <SafListItem 
        role="menuitem"
        href="/settings"
        tabindex={0}
      >
        <SafIcon slot="start" name="settings" />
        Settings
      </SafListItem>
      
      <SafListItem 
        role="menuitem"
        href="/help"
        target="_blank"
        tabindex={0}
      >
        <SafIcon slot="start" name="help" />
        Help Center
        <SafIcon slot="end" name="external-link" />
      </SafListItem>
    </SafList>
  );
}
```

#### Angular
```html
<saf-list role="menu">
  <saf-list-item 
    role="menuitem"
    href="/dashboard"
    [tabindex]="0"
  >
    <saf-icon slot="start" name="dashboard"></saf-icon>
    Dashboard
  </saf-list-item>
  
  <saf-list-item 
    role="menuitem"
    href="/reports"
    [tabindex]="0"
  >
    <saf-icon slot="start" name="chart"></saf-icon>
    Reports
  </saf-list-item>
  
  <saf-list-item 
    role="menuitem"
    href="/settings"
    [tabindex]="0"
  >
    <saf-icon slot="start" name="settings"></saf-icon>
    Settings
  </saf-list-item>
  
  <saf-list-item 
    role="menuitem"
    href="/help"
    target="_blank"
    [tabindex]="0"
  >
    <saf-icon slot="start" name="help"></saf-icon>
    Help Center
    <saf-icon slot="end" name="external-link"></saf-icon>
  </saf-list-item>
</saf-list>
```

### Dynamic List with Data Binding

#### React
```jsx
import { SafList, SafListItem, SafBadge, SafIcon } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicList() {
  const [items, setItems] = useState([]);
  const [selectedItems, setSelectedItems] = useState(new Set());

  useEffect(() => {
    // Simulate loading data
    setItems([
      { id: 1, name: 'Task 1', status: 'completed', priority: 'high' },
      { id: 2, name: 'Task 2', status: 'in-progress', priority: 'medium' },
      { id: 3, name: 'Task 3', status: 'pending', priority: 'low' },
      { id: 4, name: 'Task 4', status: 'completed', priority: 'high' }
    ]);
  }, []);

  const toggleSelection = (itemId) => {
    const newSelection = new Set(selectedItems);
    if (newSelection.has(itemId)) {
      newSelection.delete(itemId);
    } else {
      newSelection.add(itemId);
    }
    setSelectedItems(newSelection);
  };

  const getStatusIcon = (status) => {
    switch (status) {
      case 'completed': return 'check-circle';
      case 'in-progress': return 'clock';
      case 'pending': return 'circle';
      default: return 'circle';
    }
  };

  const getStatusColor = (status) => {
    switch (status) {
      case 'completed': return 'success';
      case 'in-progress': return 'warning';
      case 'pending': return 'neutral';
      default: return 'neutral';
    }
  };

  return (
    <SafList>
      {items.map((item) => (
        <SafListItem
          key={item.id}
          value={item.id}
          selected={selectedItems.has(item.id)}
          onClick={() => toggleSelection(item.id)}
        >
          <SafIcon 
            slot="start" 
            name={getStatusIcon(item.status)}
            color={getStatusColor(item.status)}
          />
          
          <div>
            <h4>{item.name}</h4>
            <p>Status: {item.status}</p>
          </div>
          
          <SafBadge 
            slot="end"
            variant={item.priority === 'high' ? 'error' : 
                   item.priority === 'medium' ? 'warning' : 'neutral'}
          >
            {item.priority}
          </SafBadge>
        </SafListItem>
      ))}
    </SafList>
  );
}
```

#### Angular
```typescript
// Component
import { Component, OnInit } from '@angular/core';

interface TaskItem {
  id: number;
  name: string;
  status: 'completed' | 'in-progress' | 'pending';
  priority: 'high' | 'medium' | 'low';
}

@Component({
  selector: 'app-dynamic-list',
  template: `
    <saf-list>
      <saf-list-item
        *ngFor="let item of items"
        [value]="item.id"
        [selected]="selectedItems.has(item.id)"
        (click)="toggleSelection(item.id)"
      >
        <saf-icon 
          slot="start" 
          [name]="getStatusIcon(item.status)"
          [attr.color]="getStatusColor(item.status)"
        ></saf-icon>
        
        <div>
          <h4>{{item.name}}</h4>
          <p>Status: {{item.status}}</p>
        </div>
        
        <saf-badge 
          slot="end"
          [variant]="getPriorityVariant(item.priority)"
        >
          {{item.priority}}
        </saf-badge>
      </saf-list-item>
    </saf-list>
  `
})
export class DynamicListComponent implements OnInit {
  items: TaskItem[] = [];
  selectedItems = new Set<number>();

  ngOnInit() {
    // Simulate loading data
    this.items = [
      { id: 1, name: 'Task 1', status: 'completed', priority: 'high' },
      { id: 2, name: 'Task 2', status: 'in-progress', priority: 'medium' },
      { id: 3, name: 'Task 3', status: 'pending', priority: 'low' },
      { id: 4, name: 'Task 4', status: 'completed', priority: 'high' }
    ];
  }

  toggleSelection(itemId: number) {
    if (this.selectedItems.has(itemId)) {
      this.selectedItems.delete(itemId);
    } else {
      this.selectedItems.add(itemId);
    }
  }

  getStatusIcon(status: string): string {
    switch (status) {
      case 'completed': return 'check-circle';
      case 'in-progress': return 'clock';
      case 'pending': return 'circle';
      default: return 'circle';
    }
  }

  getStatusColor(status: string): string {
    switch (status) {
      case 'completed': return 'success';
      case 'in-progress': return 'warning';
      case 'pending': return 'neutral';
      default: return 'neutral';
    }
  }

  getPriorityVariant(priority: string): string {
    switch (priority) {
      case 'high': return 'error';
      case 'medium': return 'warning';
      case 'low': return 'neutral';
      default: return 'neutral';
    }
  }
}
```

## Best Practices

1. **Semantic Roles**: Use appropriate ARIA roles (`listitem`, `option`, `menuitem`) based on the list context
2. **Keyboard Navigation**: Implement proper tabindex management for keyboard accessibility
3. **Visual States**: Clearly indicate selected, active, and disabled states
4. **Content Structure**: Use slots effectively to organize content (start icons, main content, end actions)
5. **Selection Patterns**: Implement consistent selection behavior across similar list interactions
6. **Performance**: For large lists, consider virtualization techniques
7. **Responsive Design**: Ensure list items work well on different screen sizes
8. **Loading States**: Show appropriate loading indicators for dynamic content

## Accessibility Considerations

- Use proper ARIA roles and properties
- Ensure keyboard navigation support with arrow keys
- Provide clear focus indicators
- Use appropriate contrast ratios for text and backgrounds
- Include screen reader announcements for state changes
- Support high contrast mode and reduced motion preferences

## Related Components

- `SafList`: Container component for list items
- `SafListBox`: Selectable list container
- `SafIcon`: For displaying icons in list items
- `SafButton`: For action buttons within list items
- `SafBadge`: For status indicators and labels
- `SafCheckbox`: For multi-select functionality
- `SafRadio`: For single-select functionality

## Notes

- List items must be used within appropriate list containers
- The component automatically handles focus management within lists
- Selection behavior depends on the parent list component's configuration
- Link functionality (href) takes precedence over click handlers
- Custom styling should maintain accessibility requirements
