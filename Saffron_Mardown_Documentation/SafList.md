# SafList

A flexible list component for displaying ordered and unordered lists with various styling options and sizes.

## Usage

```html
<saf-list>
  <saf-list-item>First item</saf-list-item>
  <saf-list-item>Second item</saf-list-item>
  <saf-list-item>Third item</saf-list-item>
</saf-list>
```

## API

### SafList

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `order` | `'ordered' \| 'unordered'` | `'unordered'` | Whether to render as an ordered (`<ol>`) or unordered (`<ul>`) list |
| `size` | `'small' \| 'medium' \| 'large'` | - | The size of the list text |
| `list-style` | `'disc' \| 'circle' \| 'square' \| 'decimal' \| 'lower-alpha' \| 'lower-roman' \| 'ticked' \| 'none'` | - | The visual style for the list markers |
| `inline` | `boolean` | `false` | Whether to display list items inline horizontally |

#### Slots

| Name | Description |
|------|-------------|
| default | Container for list items |

#### Parts

| Name | Description |
|------|-------------|
| `list` | The underlying `<ul>` or `<ol>` element |

### SafListItem

#### Slots

| Name | Description |
|------|-------------|
| default | The list item content |

## Examples

### Basic Unordered List

```html
<saf-list>
  <saf-list-item>Apple</saf-list-item>
  <saf-list-item>Orange</saf-list-item>
  <saf-list-item>Banana</saf-list-item>
  <saf-list-item>Grape</saf-list-item>
</saf-list>
```

### Ordered List

```html
<saf-list order="ordered">
  <saf-list-item>First step: Gather ingredients</saf-list-item>
  <saf-list-item>Second step: Mix ingredients</saf-list-item>
  <saf-list-item>Third step: Bake for 25 minutes</saf-list-item>
  <saf-list-item>Fourth step: Let cool and enjoy</saf-list-item>
</saf-list>
```

### Different List Styles

```html
<!-- Disc style (default for unordered) -->
<saf-list list-style="disc">
  <saf-list-item>Disc bullet item</saf-list-item>
  <saf-list-item>Another disc item</saf-list-item>
</saf-list>

<!-- Circle style -->
<saf-list list-style="circle">
  <saf-list-item>Circle bullet item</saf-list-item>
  <saf-list-item>Another circle item</saf-list-item>
</saf-list>

<!-- Square style -->
<saf-list list-style="square">
  <saf-list-item>Square bullet item</saf-list-item>
  <saf-list-item>Another square item</saf-list-item>
</saf-list>

<!-- Ticked style -->
<saf-list list-style="ticked">
  <saf-list-item>✓ Completed task</saf-list-item>
  <saf-list-item>✓ Another completed task</saf-list-item>
</saf-list>

<!-- No style -->
<saf-list list-style="none">
  <saf-list-item>Item without bullet</saf-list-item>
  <saf-list-item>Another item without bullet</saf-list-item>
</saf-list>
```

### Ordered List Styles

```html
<!-- Decimal (default for ordered) -->
<saf-list order="ordered" list-style="decimal">
  <saf-list-item>First numbered item</saf-list-item>
  <saf-list-item>Second numbered item</saf-list-item>
  <saf-list-item>Third numbered item</saf-list-item>
</saf-list>

<!-- Lower alpha -->
<saf-list order="ordered" list-style="lower-alpha">
  <saf-list-item>First alphabetic item (a)</saf-list-item>
  <saf-list-item>Second alphabetic item (b)</saf-list-item>
  <saf-list-item>Third alphabetic item (c)</saf-list-item>
</saf-list>

<!-- Lower roman -->
<saf-list order="ordered" list-style="lower-roman">
  <saf-list-item>First roman item (i)</saf-list-item>
  <saf-list-item>Second roman item (ii)</saf-list-item>
  <saf-list-item>Third roman item (iii)</saf-list-item>
</saf-list>
```

### Different Sizes

```html
<!-- Small size -->
<saf-list size="small">
  <saf-list-item>Small text item</saf-list-item>
  <saf-list-item>Another small item</saf-list-item>
</saf-list>

<!-- Medium size (default) -->
<saf-list size="medium">
  <saf-list-item>Medium text item</saf-list-item>
  <saf-list-item>Another medium item</saf-list-item>
</saf-list>

<!-- Large size -->
<saf-list size="large">
  <saf-list-item>Large text item</saf-list-item>
  <saf-list-item>Another large item</saf-list-item>
</saf-list>
```

### Inline Lists

```html
<saf-list inline>
  <saf-list-item>Home</saf-list-item>
  <saf-list-item>About</saf-list-item>
  <saf-list-item>Services</saf-list-item>
  <saf-list-item>Contact</saf-list-item>
</saf-list>

<!-- Inline with custom separator -->
<saf-list inline list-style="none">
  <saf-list-item>Item 1</saf-list-item>
  <saf-list-item>Item 2</saf-list-item>
  <saf-list-item>Item 3</saf-list-item>
</saf-list>
```

### Lists with Rich Content

```html
<saf-list>
  <saf-list-item>
    <strong>Project Alpha</strong>
    <p>A comprehensive redesign of the user interface with modern styling and improved accessibility.</p>
  </saf-list-item>
  <saf-list-item>
    <strong>Project Beta</strong>
    <p>Backend infrastructure improvements focusing on performance and scalability.</p>
  </saf-list-item>
  <saf-list-item>
    <strong>Project Gamma</strong>
    <p>Mobile application development for iOS and Android platforms.</p>
  </saf-list-item>
</saf-list>
```

### Lists with Icons and Actions

```html
<saf-list>
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <saf-icon icon-name="file-text" appearance="solid"></saf-icon>
      <span>Document.pdf</span>
      <div style="margin-left: auto;">
        <saf-button appearance="subtle" size="small">
          <saf-icon icon-name="download" appearance="solid"></saf-icon>
        </saf-button>
        <saf-button appearance="subtle" size="small">
          <saf-icon icon-name="share" appearance="solid"></saf-icon>
        </saf-button>
      </div>
    </div>
  </saf-list-item>
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <saf-icon icon-name="image" appearance="solid"></saf-icon>
      <span>Image.jpg</span>
      <div style="margin-left: auto;">
        <saf-button appearance="subtle" size="small">
          <saf-icon icon-name="download" appearance="solid"></saf-icon>
        </saf-button>
        <saf-button appearance="subtle" size="small">
          <saf-icon icon-name="share" appearance="solid"></saf-icon>
        </saf-button>
      </div>
    </div>
  </saf-list-item>
</saf-list>
```

### Nested Lists

```html
<saf-list>
  <saf-list-item>
    Main Category 1
    <saf-list style="margin-top: 8px;">
      <saf-list-item>Subcategory A</saf-list-item>
      <saf-list-item>Subcategory B</saf-list-item>
    </saf-list>
  </saf-list-item>
  <saf-list-item>
    Main Category 2
    <saf-list order="ordered" style="margin-top: 8px;">
      <saf-list-item>First sub-item</saf-list-item>
      <saf-list-item>Second sub-item</saf-list-item>
      <saf-list-item>Third sub-item</saf-list-item>
    </saf-list>
  </saf-list-item>
</saf-list>
```

### Task Lists

```html
<h3>Project Tasks</h3>
<saf-list list-style="ticked">
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox" checked>
      <span style="text-decoration: line-through;">Complete wireframes</span>
      <saf-badge appearance="positive">Done</saf-badge>
    </div>
  </saf-list-item>
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox" checked>
      <span style="text-decoration: line-through;">Review design mockups</span>
      <saf-badge appearance="positive">Done</saf-badge>
    </div>
  </saf-list-item>
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox">
      <span>Implement responsive design</span>
      <saf-badge appearance="warning">In Progress</saf-badge>
    </div>
  </saf-list-item>
  <saf-list-item>
    <div style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox">
      <span>Conduct user testing</span>
      <saf-badge appearance="neutral">Pending</saf-badge>
    </div>
  </saf-list-item>
</saf-list>
```

### Navigation Lists

```html
<nav>
  <saf-list list-style="none">
    <saf-list-item>
      <a href="/" style="text-decoration: none; color: inherit;">
        <div style="display: flex; align-items: center; gap: 8px; padding: 8px;">
          <saf-icon icon-name="home" appearance="solid"></saf-icon>
          Dashboard
        </div>
      </a>
    </saf-list-item>
    <saf-list-item>
      <a href="/projects" style="text-decoration: none; color: inherit;">
        <div style="display: flex; align-items: center; gap: 8px; padding: 8px;">
          <saf-icon icon-name="folder" appearance="solid"></saf-icon>
          Projects
        </div>
      </a>
    </saf-list-item>
    <saf-list-item>
      <a href="/settings" style="text-decoration: none; color: inherit;">
        <div style="display: flex; align-items: center; gap: 8px; padding: 8px;">
          <saf-icon icon-name="settings" appearance="solid"></saf-icon>
          Settings
        </div>
      </a>
    </saf-list-item>
  </saf-list>
</nav>
```

### Comparison Lists

```html
<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px;">
  <div>
    <h3>Free Plan</h3>
    <saf-list list-style="ticked">
      <saf-list-item>✓ Up to 5 projects</saf-list-item>
      <saf-list-item>✓ 1GB storage</saf-list-item>
      <saf-list-item>✓ Email support</saf-list-item>
      <saf-list-item>✗ Advanced analytics</saf-list-item>
      <saf-list-item>✗ Priority support</saf-list-item>
    </saf-list>
  </div>
  <div>
    <h3>Pro Plan</h3>
    <saf-list list-style="ticked">
      <saf-list-item>✓ Unlimited projects</saf-list-item>
      <saf-list-item>✓ 100GB storage</saf-list-item>
      <saf-list-item>✓ Priority support</saf-list-item>
      <saf-list-item>✓ Advanced analytics</saf-list-item>
      <saf-list-item>✓ Custom integrations</saf-list-item>
    </saf-list>
  </div>
</div>
```

## Framework Integration

### React

```jsx
import { SafList, SafListItem } from '@saffron/core-components-react';

function TaskListExample() {
  const tasks = [
    { id: 1, text: 'Complete documentation', done: true },
    { id: 2, text: 'Review pull request', done: false },
    { id: 3, text: 'Update dependencies', done: false }
  ];

  return (
    <SafList listStyle="none">
      {tasks.map(task => (
        <SafListItem key={task.id}>
          <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
            <input 
              type="checkbox" 
              checked={task.done}
              onChange={() => toggleTask(task.id)}
            />
            <span style={{ 
              textDecoration: task.done ? 'line-through' : 'none' 
            }}>
              {task.text}
            </span>
          </div>
        </SafListItem>
      ))}
    </SafList>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-list-demo',
  template: `
    <saf-list [order]="listType" [size]="listSize" [list-style]="listStyle">
      <saf-list-item *ngFor="let item of listItems">
        <div class="list-item-content">
          <span>{{ item.title }}</span>
          <small>{{ item.description }}</small>
        </div>
      </saf-list-item>
    </saf-list>
  `,
  styles: [`
    .list-item-content {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }
  `]
})
export class ListDemoComponent {
  listType = 'unordered';
  listSize = 'medium';
  listStyle = 'disc';

  listItems = [
    { title: 'First Item', description: 'Description for first item' },
    { title: 'Second Item', description: 'Description for second item' },
    { title: 'Third Item', description: 'Description for third item' }
  ];
}
```

## Accessibility Features

- **Semantic HTML**: Uses native `<ul>` and `<ol>` elements for proper semantics
- **Screen Reader Support**: List structure is announced correctly by screen readers
- **Keyboard Navigation**: Standard tab navigation through interactive elements within list items
- **ARIA Support**: Inherits standard list ARIA properties from native HTML elements

## Best Practices

1. **Choose Appropriate List Type**: Use ordered lists for sequential content, unordered for non-sequential
2. **Consistent Content**: Keep list items at a similar level of detail and importance
3. **Meaningful Order**: Arrange items in a logical order (alphabetical, chronological, importance)
4. **Avoid Too Many Items**: Consider pagination or grouping for very long lists
5. **Interactive Elements**: Ensure interactive elements within list items are properly accessible
6. **Responsive Design**: Consider how lists will appear on different screen sizes
7. **Visual Hierarchy**: Use size and styling to establish clear information hierarchy

## Related Components

- `saf-tree-view`: For hierarchical data with expandable/collapsible nodes
- `saf-menu`: For interactive navigation lists
- `saf-accordion`: For collapsible list sections
- `saf-card`: For more complex list item layouts
