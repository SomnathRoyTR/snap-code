# SafTreeView

A hierarchical tree component that displays data in a tree structure with expandable and collapsible nodes. Implements the WAI-ARIA tree pattern for optimal accessibility.

## Usage

```html
<saf-tree-view>
  <saf-tree-item>
    Root Item 1
    <saf-tree-item>Child Item 1.1</saf-tree-item>
    <saf-tree-item>
      Child Item 1.2
      <saf-tree-item>Grandchild Item 1.2.1</saf-tree-item>
      <saf-tree-item>Grandchild Item 1.2.2</saf-tree-item>
    </saf-tree-item>
  </saf-tree-item>
  <saf-tree-item>
    Root Item 2
    <saf-tree-item>Child Item 2.1</saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

## API

### SafTreeView

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `currentSelected` | `HTMLElement \| TreeItem \| null` | The currently selected tree item |
| `currentFocused` | `HTMLElement \| TreeItem \| null` | The tree item that has focus (internal) |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `selected-change` | `CustomEvent<TreeItem>` | Fires when a tree item's selected state changes |

#### Slots

| Name | Description |
|------|-------------|
| default | Container for tree items |

### SafTreeItem

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the tree item is expanded (shows children) |
| `selected` | `boolean` | `false` | Whether the tree item is selected |
| `disabled` | `boolean` | `false` | Whether the tree item is disabled and cannot be interacted with |

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `childItemLength` | `number` | The number of child tree items |
| `isTreeItem` | `boolean` | Readonly property identifying the element as a tree item |
| `focusable` | `boolean` | Whether the item can receive focus (internal) |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `expanded-change` | `CustomEvent<TreeItem>` | Fires when the expanded state changes |
| `selected-change` | `CustomEvent<TreeItem>` | Fires when the selected state changes |

#### Slots

| Name | Description |
|------|-------------|
| default | The tree item text content |
| `start` | Content positioned before the tree item content |
| `end` | Content positioned after the tree item content |
| `item` | Container for child tree items (automatically managed) |
| `expand-collapse-glyph` | Custom expand/collapse icon (defaults to caret icons) |

#### Parts

| Name | Description |
|------|-------------|
| `positioning-region` | The element used to position the tree item content |
| `content-region` | The element containing the expand/collapse, start, and end content |
| `items` | The element wrapping any child items |
| `expand-collapse-button` | The expand/collapse button |

## Examples

### Basic Tree

```html
<saf-tree-view>
  <saf-tree-item>
    Documents
    <saf-tree-item>Reports</saf-tree-item>
    <saf-tree-item>Presentations</saf-tree-item>
    <saf-tree-item>Spreadsheets</saf-tree-item>
  </saf-tree-item>
  <saf-tree-item>
    Media
    <saf-tree-item>Images</saf-tree-item>
    <saf-tree-item>Videos</saf-tree-item>
    <saf-tree-item>Audio</saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### Tree with Icons

```html
<saf-tree-view>
  <saf-tree-item>
    <saf-icon slot="start" icon-name="folder" appearance="solid"></saf-icon>
    Projects
    <saf-tree-item>
      <saf-icon slot="start" icon-name="folder-open" appearance="solid"></saf-icon>
      Project Alpha
      <saf-tree-item>
        <saf-icon slot="start" icon-name="file-text" appearance="solid"></saf-icon>
        README.md
      </saf-tree-item>
      <saf-tree-item>
        <saf-icon slot="start" icon-name="file-code" appearance="solid"></saf-icon>
        index.js
      </saf-tree-item>
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="folder" appearance="solid"></saf-icon>
      Project Beta
    </saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### Pre-expanded and Selected Items

```html
<saf-tree-view>
  <saf-tree-item expanded>
    Organization
    <saf-tree-item selected>
      <saf-icon slot="start" icon-name="user" appearance="solid"></saf-icon>
      Employees
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="users" appearance="solid"></saf-icon>
      Teams
      <saf-tree-item>Development</saf-tree-item>
      <saf-tree-item>Design</saf-tree-item>
      <saf-tree-item>Marketing</saf-tree-item>
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="building" appearance="solid"></saf-icon>
      Departments
    </saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### Disabled Items

```html
<saf-tree-view>
  <saf-tree-item>
    Available Features
    <saf-tree-item>
      <saf-icon slot="start" icon-name="check" appearance="solid"></saf-icon>
      Basic Plan
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="check" appearance="solid"></saf-icon>
      Standard Plan
    </saf-tree-item>
    <saf-tree-item disabled>
      <saf-icon slot="start" icon-name="lock" appearance="solid"></saf-icon>
      Premium Plan (Coming Soon)
      <saf-tree-item disabled>Advanced Analytics</saf-tree-item>
      <saf-tree-item disabled>Priority Support</saf-tree-item>
    </saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### Tree with Badges and Actions

```html
<saf-tree-view>
  <saf-tree-item>
    <saf-icon slot="start" icon-name="inbox" appearance="solid"></saf-icon>
    Inbox
    <saf-badge slot="end" appearance="accent">12</saf-badge>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="mail" appearance="solid"></saf-icon>
      Unread Messages
      <saf-badge slot="end" appearance="important">5</saf-badge>
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="star" appearance="solid"></saf-icon>
      Starred Messages
      <saf-badge slot="end" appearance="brand">3</saf-badge>
    </saf-tree-item>
  </saf-tree-item>
  <saf-tree-item>
    <saf-icon slot="start" icon-name="send" appearance="solid"></saf-icon>
    Sent Items
    <saf-button slot="end" appearance="subtle" size="small">
      <saf-icon icon-name="more-horizontal" appearance="solid"></saf-icon>
    </saf-button>
  </saf-tree-item>
</saf-tree-view>
```

### Custom Expand/Collapse Icons

```html
<saf-tree-view>
  <saf-tree-item>
    Custom Icons
    <saf-icon slot="expand-collapse-glyph" icon-name="minus" appearance="solid"></saf-icon>
    <saf-tree-item>Child with default icons</saf-tree-item>
  </saf-tree-item>
  <saf-tree-item>
    Plus/Minus Style
    <saf-icon slot="expand-collapse-glyph" icon-name="plus" appearance="solid"></saf-icon>
    <saf-tree-item>Nested item</saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### File Explorer Example

```html
<saf-tree-view id="file-explorer">
  <saf-tree-item expanded>
    <saf-icon slot="start" icon-name="folder-open" appearance="solid"></saf-icon>
    src
    <saf-tree-item expanded>
      <saf-icon slot="start" icon-name="folder-open" appearance="solid"></saf-icon>
      components
      <saf-tree-item>
        <saf-icon slot="start" icon-name="file-code" appearance="solid"></saf-icon>
        Button.tsx
        <span slot="end">2.1 KB</span>
      </saf-tree-item>
      <saf-tree-item selected>
        <saf-icon slot="start" icon-name="file-code" appearance="solid"></saf-icon>
        TreeView.tsx
        <span slot="end">5.7 KB</span>
      </saf-tree-item>
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="folder" appearance="solid"></saf-icon>
      styles
      <saf-tree-item>
        <saf-icon slot="start" icon-name="file-text" appearance="solid"></saf-icon>
        main.css
      </saf-tree-item>
    </saf-tree-item>
    <saf-tree-item>
      <saf-icon slot="start" icon-name="file-code" appearance="solid"></saf-icon>
      App.tsx
      <span slot="end">1.8 KB</span>
    </saf-tree-item>
  </saf-tree-item>
</saf-tree-view>
```

### Event Handling

```html
<saf-tree-view id="event-tree">
  <saf-tree-item>
    Root Item
    <saf-tree-item>Child Item 1</saf-tree-item>
    <saf-tree-item>Child Item 2</saf-tree-item>
  </saf-tree-item>
</saf-tree-view>

<script>
  const treeView = document.getElementById('event-tree');
  
  treeView.addEventListener('selected-change', (event) => {
    console.log('Selected changed:', event.detail);
  });
  
  // Listen for expand/collapse events on individual tree items
  const treeItems = treeView.querySelectorAll('saf-tree-item');
  treeItems.forEach(item => {
    item.addEventListener('expanded-change', (event) => {
      console.log('Expanded changed:', event.detail);
    });
  });
</script>
```

### Programmatic Control

```html
<saf-tree-view id="programmable-tree">
  <saf-tree-item id="root-1">
    Item 1
    <saf-tree-item id="child-1-1">Child 1.1</saf-tree-item>
    <saf-tree-item id="child-1-2">Child 1.2</saf-tree-item>
  </saf-tree-item>
  <saf-tree-item id="root-2">
    Item 2
    <saf-tree-item id="child-2-1">Child 2.1</saf-tree-item>
  </saf-tree-item>
</saf-tree-view>

<div>
  <saf-button onclick="expandAll()">Expand All</saf-button>
  <saf-button onclick="collapseAll()">Collapse All</saf-button>
  <saf-button onclick="selectItem('child-1-1')">Select Child 1.1</saf-button>
</div>

<script>
  function expandAll() {
    const treeItems = document.querySelectorAll('#programmable-tree saf-tree-item');
    treeItems.forEach(item => {
      if (item.childItemLength > 0) {
        item.expanded = true;
      }
    });
  }
  
  function collapseAll() {
    const treeItems = document.querySelectorAll('#programmable-tree saf-tree-item');
    treeItems.forEach(item => {
      item.expanded = false;
    });
  }
  
  function selectItem(id) {
    // First deselect all items
    const treeItems = document.querySelectorAll('#programmable-tree saf-tree-item');
    treeItems.forEach(item => {
      item.selected = false;
    });
    
    // Select the target item
    const targetItem = document.getElementById(id);
    if (targetItem) {
      targetItem.selected = true;
    }
  }
</script>
```

## Framework Integration

### React

```jsx
import { SafTreeView, SafTreeItem } from '@saffron/core-components-react';
import { useState } from 'react';

function FileTreeExample() {
  const [selectedItem, setSelectedItem] = useState(null);
  const [expandedItems, setExpandedItems] = useState(new Set(['root']));

  const handleSelectedChange = (event) => {
    setSelectedItem(event.detail);
    console.log('Selected item:', event.detail);
  };

  const handleExpandedChange = (event) => {
    const item = event.detail;
    const newExpanded = new Set(expandedItems);
    if (item.expanded) {
      newExpanded.add(item.id);
    } else {
      newExpanded.delete(item.id);
    }
    setExpandedItems(newExpanded);
  };

  return (
    <SafTreeView onSelectedChange={handleSelectedChange}>
      <SafTreeItem 
        expanded={expandedItems.has('root')} 
        onExpandedChange={handleExpandedChange}
        id="root"
      >
        <span slot="start">📁</span>
        Project Files
        <SafTreeItem selected={selectedItem?.id === 'readme'} id="readme">
          <span slot="start">📄</span>
          README.md
        </SafTreeItem>
        <SafTreeItem selected={selectedItem?.id === 'app'} id="app">
          <span slot="start">⚛️</span>
          App.jsx
        </SafTreeItem>
      </SafTreeItem>
    </SafTreeView>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-tree-demo',
  template: `
    <saf-tree-view (selected-change)="onSelectionChange($event)">
      <saf-tree-item 
        [expanded]="isExpanded('documents')" 
        (expanded-change)="onExpandedChange($event, 'documents')"
      >
        Documents
        <saf-tree-item 
          *ngFor="let doc of documents"
          [selected]="selectedDocument === doc.id"
          (click)="selectDocument(doc.id)"
        >
          {{ doc.name }}
        </saf-tree-item>
      </saf-tree-item>
    </saf-tree-view>
  `
})
export class TreeDemoComponent {
  selectedDocument: string | null = null;
  expandedNodes = new Set(['documents']);

  documents = [
    { id: 'doc1', name: 'Report.pdf' },
    { id: 'doc2', name: 'Presentation.pptx' },
    { id: 'doc3', name: 'Spreadsheet.xlsx' }
  ];

  isExpanded(nodeId: string): boolean {
    return this.expandedNodes.has(nodeId);
  }

  onExpandedChange(event: CustomEvent, nodeId: string) {
    if (event.detail.expanded) {
      this.expandedNodes.add(nodeId);
    } else {
      this.expandedNodes.delete(nodeId);
    }
  }

  selectDocument(docId: string) {
    this.selectedDocument = docId;
  }

  onSelectionChange(event: CustomEvent) {
    console.log('Selection changed:', event.detail);
  }
}
```

## Accessibility Features

- **ARIA Tree Pattern**: Implements the complete WAI-ARIA tree pattern with proper roles
- **Keyboard Navigation**: 
  - `Arrow Up/Down`: Navigate between visible tree items
  - `Arrow Right`: Expand focused item or move to first child
  - `Arrow Left`: Collapse focused item or move to parent
  - `Home`: Move to first tree item
  - `End`: Move to last visible tree item
  - `Enter/Space`: Toggle selection (if selectable)
- **Screen Reader Support**: Proper labeling with `aria-expanded`, `aria-selected`, and `aria-disabled`
- **Focus Management**: Maintains focus within the tree and provides visual focus indicators
- **Hierarchical Structure**: Properly nested structure for screen readers to understand relationships

## Best Practices

1. **Meaningful Labels**: Use clear, descriptive text for tree items
2. **Consistent Icons**: Use consistent iconography to represent different item types
3. **Logical Hierarchy**: Structure the tree in a logical, intuitive way
4. **Performance**: For large trees, consider virtualization or lazy loading
5. **Selection Model**: Decide whether single or multiple selection is appropriate
6. **Expand/Collapse State**: Consider persisting expand/collapse state for better UX
7. **Loading States**: Show appropriate loading indicators for dynamically loaded content
8. **Context Actions**: Provide context menus or action buttons for tree items when needed

## Related Components

- `saf-accordion`: For simple collapsible content sections
- `saf-menu`: For hierarchical menu navigation
- `saf-breadcrumb`: For showing the current location within a tree structure
- `saf-icon`: For representing different types of tree items
