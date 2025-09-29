# SafMenu Component

The **SafMenu** component provides a keyboard-navigable menu interface that supports hierarchical menu structures with submenus. Built on the ARIA menu pattern, it offers comprehensive keyboard navigation and focus management.

## Basic Usage

```html
<!-- Basic menu -->
<saf-menu>
  <saf-menu-item>File</saf-menu-item>
  <saf-menu-item>Edit</saf-menu-item>
  <saf-menu-item>View</saf-menu-item>
  <saf-menu-item>Help</saf-menu-item>
</saf-menu>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `density` | `'compact' \| 'normal' \| 'relaxed' \| 'inherit'` | `'inherit'` | Controls the spacing and sizing of the menu |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `density` | `ComponentDensity` | `'inherit'` | Controls the spacing in and around the component |
| `items` | `MenuItem[]` | `[]` | Array of menu items (read-only) |
| `focusIndex` | `number` | `-1` | Current focused item index |

### Methods

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `focus()` | `options?: FocusOptions` | `void` | Focus the menu and first focusable item |
| `setItems()` | `items: MenuItem[]` | `void` | Update the menu items array |
| `moveToFirstItem()` | - | `void` | Move focus to first menu item |
| `moveToLastItem()` | - | `void` | Move focus to last menu item |
| `moveToNextItem()` | - | `void` | Move focus to next menu item |
| `moveToPreviousItem()` | - | `void` | Move focus to previous menu item |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Menu items and content |

### CSS Parts

| Part | Description |
|------|-------------|
| `positioning-region` | The container for positioning menu items |

## Comprehensive Examples

### Menu with Submenus

```html
<saf-menu>
  <saf-menu-item>
    File
    <saf-menu slot="submenu">
      <saf-menu-item>New</saf-menu-item>
      <saf-menu-item>Open</saf-menu-item>
      <saf-menu-item>Save</saf-menu-item>
      <saf-menu-divider></saf-menu-divider>
      <saf-menu-item>Exit</saf-menu-item>
    </saf-menu>
  </saf-menu-item>
  <saf-menu-item>
    Edit
    <saf-menu slot="submenu">
      <saf-menu-item>Cut</saf-menu-item>
      <saf-menu-item>Copy</saf-menu-item>
      <saf-menu-item>Paste</saf-menu-item>
    </saf-menu>
  </saf-menu-item>
  <saf-menu-item>View</saf-menu-item>
</saf-menu>
```

### Menu with Different Densities

```html
<!-- Compact menu -->
<saf-menu density="compact">
  <saf-menu-item>Compact Item 1</saf-menu-item>
  <saf-menu-item>Compact Item 2</saf-menu-item>
  <saf-menu-item>Compact Item 3</saf-menu-item>
</saf-menu>

<!-- Normal menu -->
<saf-menu density="normal">
  <saf-menu-item>Normal Item 1</saf-menu-item>
  <saf-menu-item>Normal Item 2</saf-menu-item>
  <saf-menu-item>Normal Item 3</saf-menu-item>
</saf-menu>

<!-- Relaxed menu -->
<saf-menu density="relaxed">
  <saf-menu-item>Relaxed Item 1</saf-menu-item>
  <saf-menu-item>Relaxed Item 2</saf-menu-item>
  <saf-menu-item>Relaxed Item 3</saf-menu-item>
</saf-menu>
```

### Context Menu Implementation

```html
<div id="context-area">
  Right-click for context menu
</div>

<saf-menu id="context-menu" style="display: none; position: fixed;">
  <saf-menu-item>Cut</saf-menu-item>
  <saf-menu-item>Copy</saf-menu-item>
  <saf-menu-item>Paste</saf-menu-item>
  <saf-menu-divider></saf-menu-divider>
  <saf-menu-item>Delete</saf-menu-item>
</saf-menu>

<script>
const contextArea = document.getElementById('context-area');
const contextMenu = document.getElementById('context-menu');

contextArea.addEventListener('contextmenu', (e) => {
  e.preventDefault();
  contextMenu.style.display = 'block';
  contextMenu.style.left = `${e.pageX}px`;
  contextMenu.style.top = `${e.pageY}px`;
  contextMenu.focus();
});

document.addEventListener('click', () => {
  contextMenu.style.display = 'none';
});
</script>
```

## Framework Integration

### React Example

```tsx
import React, { useRef, useEffect } from 'react';

interface MenuProps {
  items: Array<{
    label: string;
    action?: () => void;
    submenu?: Array<{ label: string; action?: () => void }>;
  }>;
  density?: 'compact' | 'normal' | 'relaxed';
}

const SafMenuComponent: React.FC<MenuProps> = ({ items, density = 'normal' }) => {
  const menuRef = useRef<HTMLElement>(null);

  const handleItemClick = (action?: () => void) => {
    if (action) {
      action();
    }
  };

  return (
    <saf-menu ref={menuRef} density={density}>
      {items.map((item, index) => (
        <saf-menu-item
          key={index}
          onClick={() => handleItemClick(item.action)}
        >
          {item.label}
          {item.submenu && (
            <saf-menu slot="submenu">
              {item.submenu.map((subItem, subIndex) => (
                <saf-menu-item
                  key={subIndex}
                  onClick={() => handleItemClick(subItem.action)}
                >
                  {subItem.label}
                </saf-menu-item>
              ))}
            </saf-menu>
          )}
        </saf-menu-item>
      ))}
    </saf-menu>
  );
};

// Usage
const menuItems = [
  {
    label: 'File',
    submenu: [
      { label: 'New', action: () => console.log('New file') },
      { label: 'Open', action: () => console.log('Open file') },
      { label: 'Save', action: () => console.log('Save file') }
    ]
  },
  { label: 'Edit' },
  { label: 'View' }
];

export default function App() {
  return <SafMenuComponent items={menuItems} density="normal" />;
}
```

### Angular Example

```typescript
// menu.component.ts
import { Component, Input } from '@angular/core';

interface MenuItem {
  label: string;
  action?: () => void;
  submenu?: MenuItem[];
}

@Component({
  selector: 'app-saf-menu',
  template: `
    <saf-menu [attr.density]="density">
      <saf-menu-item 
        *ngFor="let item of items"
        (click)="handleItemClick(item.action)"
      >
        {{ item.label }}
        <saf-menu slot="submenu" *ngIf="item.submenu">
          <saf-menu-item 
            *ngFor="let subItem of item.submenu"
            (click)="handleItemClick(subItem.action)"
          >
            {{ subItem.label }}
          </saf-menu-item>
        </saf-menu>
      </saf-menu-item>
    </saf-menu>
  `
})
export class SafMenuComponent {
  @Input() items: MenuItem[] = [];
  @Input() density: 'compact' | 'normal' | 'relaxed' = 'normal';

  handleItemClick(action?: () => void): void {
    if (action) {
      action();
    }
  }
}

// app.component.ts
export class AppComponent {
  menuItems: MenuItem[] = [
    {
      label: 'File',
      submenu: [
        { label: 'New', action: () => console.log('New file') },
        { label: 'Open', action: () => console.log('Open file') },
        { label: 'Save', action: () => console.log('Save file') }
      ]
    },
    { label: 'Edit' },
    { label: 'View' }
  ];
}
```

### Vue Example

```vue
<template>
  <saf-menu :density="density">
    <saf-menu-item
      v-for="(item, index) in items"
      :key="index"
      @click="handleItemClick(item.action)"
    >
      {{ item.label }}
      <saf-menu
        slot="submenu"
        v-if="item.submenu"
      >
        <saf-menu-item
          v-for="(subItem, subIndex) in item.submenu"
          :key="subIndex"
          @click="handleItemClick(subItem.action)"
        >
          {{ subItem.label }}
        </saf-menu-item>
      </saf-menu>
    </saf-menu-item>
  </saf-menu>
</template>

<script>
export default {
  name: 'SafMenuComponent',
  props: {
    items: {
      type: Array,
      required: true
    },
    density: {
      type: String,
      default: 'normal',
      validator: value => ['compact', 'normal', 'relaxed'].includes(value)
    }
  },
  methods: {
    handleItemClick(action) {
      if (action) {
        action();
      }
    }
  }
};
</script>
```

## Accessibility Features

### Keyboard Navigation

The SafMenu component implements comprehensive keyboard navigation:

- **Arrow Keys**: Navigate between menu items
- **Home/End**: Move to first/last menu item
- **Enter/Space**: Activate menu item or toggle submenu
- **Right Arrow**: Open submenu
- **Left Arrow/Escape**: Close submenu
- **Escape**: Close entire menu

### Screen Reader Support

- Implements ARIA menu pattern with proper roles
- Provides accessible descriptions for menu states
- Announces menu item selection and navigation
- Supports screen reader navigation modes

### Focus Management

- Maintains focus within menu during keyboard navigation
- Restores focus appropriately when submenus are opened/closed
- Provides visual focus indicators
- Manages tab order correctly

## Best Practices

### Menu Structure
- Keep menu hierarchies shallow (2-3 levels maximum)
- Group related items together
- Use menu dividers to separate logical sections
- Provide clear, descriptive labels

### Performance
- Lazy load submenu content when possible
- Limit the number of menu items per level
- Use virtualization for very long menus
- Cache menu structures for frequently accessed menus

### User Experience
- Show hover states for better visual feedback
- Provide keyboard shortcuts for frequently used items
- Consider context and user workflows when designing menu structure
- Test with keyboard-only navigation

### Integration
- Use semantic menu item roles appropriately
- Implement proper event handling for menu actions
- Consider mobile responsiveness and touch interactions
- Test across different browsers and assistive technologies

## Related Components

- **SafMenuItem**: Individual menu item component
- **SafMenuDivider**: Visual separator between menu groups
- **SafPopover**: For dropdown menu positioning
- **SafContextMenu**: Specialized context menu implementation

---

*This documentation covers SafMenu v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
