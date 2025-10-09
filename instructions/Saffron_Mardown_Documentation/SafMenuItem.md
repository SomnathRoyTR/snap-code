# SafMenuItem Component

The **SafMenuItem** component represents an individual item within a SafMenu. It supports multiple ARIA roles (menuitem, menuitemcheckbox, menuitemradio), link functionality, submenus, and comprehensive keyboard navigation.

## Basic Usage

```html
<!-- Basic menu item -->
<saf-menu-item>Save File</saf-menu-item>

<!-- Menu item with icon -->
<saf-menu-item>
  <saf-icon slot="start" name="save"></saf-icon>
  Save File
</saf-menu-item>

<!-- Disabled menu item -->
<saf-menu-item disabled>Unavailable Option</saf-menu-item>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `id` | `string` | auto-generated | Unique identifier for the menu item |
| `disabled` | `boolean` | `false` | Whether the menu item is disabled |
| `expanded` | `boolean` | `false` | Whether submenu is expanded (for items with submenus) |
| `role` | `'menuitem' \| 'menuitemcheckbox' \| 'menuitemradio'` | `'menuitem'` | ARIA role for the menu item |
| `checked` | `boolean` | `false` | Checked state (for checkbox/radio roles) |
| `url` | `string` | - | URL for link menu items |
| `has-link` | `boolean` | `false` | Whether the item should render as a link |
| `router-link` | `boolean` | `false` | Whether to use router navigation instead of standard links |
| `link-target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `'_self'` (router) / `'_blank'` (link) | Link target behavior |
| `density` | `'compact' \| 'normal' \| 'relaxed' \| 'inherit'` | `'inherit'` | Controls spacing and sizing |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `navigate` | `(path: string) => void` | `() => {}` | Function called for router link navigation |
| `hasSubmenu` | `boolean` | computed | Whether the item has a submenu (read-only) |
| `hasLinkOrRouterLink` | `boolean` | computed | Whether item has link or router link functionality |
| `submenu` | `HTMLElement` | - | Reference to submenu element |

### Events

| Event | Detail | Description |
|-------|--------|-------------|
| `expanded-change` | `MenuItem` | Fired when submenu expanded state changes |
| `change` | - | Fired when menu item is invoked or checked state changes |

### Slots

| Slot | Description |
|------|-------------|
| `start` | Content before the menu item text (icons, indicators) |
| `end` | Content after the menu item text |
| (default) | Main menu item content |
| `submenu` | Submenu content |
| `checked-indicator` | Custom checked indicator for checkbox items |
| `radio-indicator` | Custom radio indicator for radio items |
| `expand-collapse-indicator` | Custom expand/collapse indicator |

### CSS Parts

| Part | Description |
|------|-------------|
| `input-container` | Container for checkbox/radio indicators |
| `checkbox` | Checkbox indicator wrapper |
| `radio` | Radio indicator wrapper |
| `content` | Main content wrapper |
| `expand-collapse-glyph-container` | Expand/collapse indicator container |
| `expand-collapse` | Expand/collapse indicator element |
| `submenu-region` | Submenu positioning container |

## Comprehensive Examples

### Basic Menu Items

```html
<saf-menu>
  <saf-menu-item>Regular Item</saf-menu-item>
  <saf-menu-item disabled>Disabled Item</saf-menu-item>
  <saf-menu-item>
    <saf-icon slot="start" name="home"></saf-icon>
    With Start Icon
  </saf-menu-item>
  <saf-menu-item>
    With End Content
    <span slot="end">Ctrl+S</span>
  </saf-menu-item>
</saf-menu>
```

### Checkbox Menu Items

```html
<saf-menu>
  <saf-menu-item role="menuitemcheckbox" checked>
    Show Toolbar
  </saf-menu-item>
  <saf-menu-item role="menuitemcheckbox">
    Show Status Bar
  </saf-menu-item>
  <saf-menu-item role="menuitemcheckbox" checked>
    Word Wrap
  </saf-menu-item>
</saf-menu>

<script>
document.querySelectorAll('saf-menu-item[role="menuitemcheckbox"]').forEach(item => {
  item.addEventListener('change', (e) => {
    console.log(`${e.target.textContent.trim()}: ${e.target.checked}`);
  });
});
</script>
```

### Radio Menu Items

```html
<saf-menu>
  <saf-menu-item role="menuitemradio" checked name="view-mode">
    List View
  </saf-menu-item>
  <saf-menu-item role="menuitemradio" name="view-mode">
    Grid View
  </saf-menu-item>
  <saf-menu-item role="menuitemradio" name="view-mode">
    Card View
  </saf-menu-item>
</saf-menu>

<script>
document.querySelectorAll('saf-menu-item[role="menuitemradio"]').forEach(item => {
  item.addEventListener('change', (e) => {
    if (e.target.checked) {
      console.log(`Selected: ${e.target.textContent.trim()}`);
      // Uncheck other radio items in the same group
      document.querySelectorAll(`saf-menu-item[role="menuitemradio"][name="${e.target.name}"]`)
        .forEach(otherItem => {
          if (otherItem !== e.target) {
            otherItem.checked = false;
          }
        });
    }
  });
});
</script>
```

### Menu Items with Submenus

```html
<saf-menu>
  <saf-menu-item>
    File
    <saf-menu slot="submenu">
      <saf-menu-item>New File</saf-menu-item>
      <saf-menu-item>Open File</saf-menu-item>
      <saf-menu-item>
        Recent Files
        <saf-menu slot="submenu">
          <saf-menu-item>document1.txt</saf-menu-item>
          <saf-menu-item>document2.txt</saf-menu-item>
          <saf-menu-item>document3.txt</saf-menu-item>
        </saf-menu>
      </saf-menu-item>
    </saf-menu>
  </saf-menu-item>
</saf-menu>
```

### Link Menu Items

```html
<saf-menu>
  <!-- Regular link -->
  <saf-menu-item has-link url="https://example.com" link-target="_blank">
    External Link
    <saf-icon slot="end" name="external-link"></saf-icon>
  </saf-menu-item>
  
  <!-- Internal link -->
  <saf-menu-item has-link url="/dashboard" link-target="_self">
    Dashboard
  </saf-menu-item>
</saf-menu>
```

### Router Link Menu Items

```html
<saf-menu id="router-menu">
  <saf-menu-item router-link url="/home">
    Home
  </saf-menu-item>
  <saf-menu-item router-link url="/profile">
    Profile
  </saf-menu-item>
  <saf-menu-item router-link url="/settings">
    Settings
  </saf-menu-item>
</saf-menu>

<script>
// Set up router navigation function
document.querySelectorAll('saf-menu-item[router-link]').forEach(item => {
  item.navigate = (path) => {
    // Your router navigation logic
    window.history.pushState(null, '', path);
    console.log(`Navigated to: ${path}`);
  };
});
</script>
```

### Different Densities

```html
<saf-menu>
  <saf-menu-item density="compact">Compact Item</saf-menu-item>
  <saf-menu-item density="normal">Normal Item</saf-menu-item>
  <saf-menu-item density="relaxed">Relaxed Item</saf-menu-item>
</saf-menu>
```

## Framework Integration

### React Example

```tsx
import React, { useState } from 'react';

interface MenuItemProps {
  children: React.ReactNode;
  role?: 'menuitem' | 'menuitemcheckbox' | 'menuitemradio';
  checked?: boolean;
  disabled?: boolean;
  url?: string;
  hasLink?: boolean;
  routerLink?: boolean;
  target?: '_self' | '_blank' | '_parent' | '_top';
  startIcon?: string;
  endContent?: string;
  submenu?: React.ReactNode;
  onSelectionChange?: (checked: boolean) => void;
  onNavigate?: (url: string) => void;
}

const SafMenuItemComponent: React.FC<MenuItemProps> = ({
  children,
  role = 'menuitem',
  checked = false,
  disabled = false,
  url,
  hasLink = false,
  routerLink = false,
  target,
  startIcon,
  endContent,
  submenu,
  onSelectionChange,
  onNavigate
}) => {
  const [isChecked, setIsChecked] = useState(checked);

  const handleChange = () => {
    if (role === 'menuitemcheckbox' || role === 'menuitemradio') {
      const newChecked = !isChecked;
      setIsChecked(newChecked);
      onSelectionChange?.(newChecked);
    }
  };

  const handleNavigate = (path: string) => {
    if (onNavigate) {
      onNavigate(path);
    }
  };

  return (
    <saf-menu-item
      role={role}
      checked={role !== 'menuitem' ? isChecked : undefined}
      disabled={disabled}
      url={url}
      has-link={hasLink}
      router-link={routerLink}
      link-target={target}
      onChange={handleChange}
      ref={(el) => {
        if (el && routerLink) {
          el.navigate = handleNavigate;
        }
      }}
    >
      {startIcon && (
        <saf-icon slot="start" name={startIcon}></saf-icon>
      )}
      {children}
      {endContent && (
        <span slot="end">{endContent}</span>
      )}
      {submenu && (
        <div slot="submenu">{submenu}</div>
      )}
    </saf-menu-item>
  );
};

// Usage examples
const MenuExample: React.FC = () => {
  const [toolbarVisible, setToolbarVisible] = useState(true);
  const [viewMode, setViewMode] = useState('list');

  return (
    <saf-menu>
      <SafMenuItemComponent>Regular Item</SafMenuItemComponent>
      
      <SafMenuItemComponent
        role="menuitemcheckbox"
        checked={toolbarVisible}
        onSelectionChange={setToolbarVisible}
      >
        Show Toolbar
      </SafMenuItemComponent>

      <SafMenuItemComponent
        routerLink
        url="/dashboard"
        onNavigate={(url) => console.log('Navigate to:', url)}
        startIcon="dashboard"
      >
        Dashboard
      </SafMenuItemComponent>

      <SafMenuItemComponent
        submenu={
          <saf-menu>
            <SafMenuItemComponent>New File</SafMenuItemComponent>
            <SafMenuItemComponent>Open File</SafMenuItemComponent>
          </saf-menu>
        }
      >
        File
      </SafMenuItemComponent>
    </saf-menu>
  );
};
```

### Angular Example

```typescript
// menu-item.component.ts
import { Component, Input, Output, EventEmitter, ViewChild, ElementRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-saf-menu-item',
  template: `
    <saf-menu-item
      #menuItemRef
      [attr.role]="role"
      [attr.checked]="role !== 'menuitem' ? checked : null"
      [attr.disabled]="disabled"
      [attr.url]="url"
      [attr.has-link]="hasLink"
      [attr.router-link]="routerLink"
      [attr.link-target]="target"
      (change)="handleChange()"
    >
      <saf-icon *ngIf="startIcon" slot="start" [attr.name]="startIcon"></saf-icon>
      <ng-content></ng-content>
      <span *ngIf="endContent" slot="end">{{ endContent }}</span>
      <ng-content select="[slot=submenu]" slot="submenu"></ng-content>
    </saf-menu-item>
  `
})
export class SafMenuItemComponent implements AfterViewInit {
  @ViewChild('menuItemRef') menuItemRef!: ElementRef<HTMLElement>;
  
  @Input() role: 'menuitem' | 'menuitemcheckbox' | 'menuitemradio' = 'menuitem';
  @Input() checked: boolean = false;
  @Input() disabled: boolean = false;
  @Input() url?: string;
  @Input() hasLink: boolean = false;
  @Input() routerLink: boolean = false;
  @Input() target?: '_self' | '_blank' | '_parent' | '_top';
  @Input() startIcon?: string;
  @Input() endContent?: string;
  
  @Output() selectionChange = new EventEmitter<boolean>();
  @Output() navigate = new EventEmitter<string>();

  ngAfterViewInit() {
    if (this.routerLink && this.menuItemRef?.nativeElement) {
      (this.menuItemRef.nativeElement as any).navigate = (path: string) => {
        this.navigate.emit(path);
      };
    }
  }

  handleChange(): void {
    if (this.role === 'menuitemcheckbox' || this.role === 'menuitemradio') {
      this.checked = !this.checked;
      this.selectionChange.emit(this.checked);
    }
  }
}

// Usage in template
/*
<saf-menu>
  <app-saf-menu-item>Regular Item</app-saf-menu-item>
  
  <app-saf-menu-item
    role="menuitemcheckbox"
    [checked]="toolbarVisible"
    (selectionChange)="toolbarVisible = $event"
  >
    Show Toolbar
  </app-saf-menu-item>

  <app-saf-menu-item
    routerLink="true"
    url="/dashboard"
    (navigate)="router.navigate([$event])"
    startIcon="dashboard"
  >
    Dashboard
  </app-saf-menu-item>

  <app-saf-menu-item>
    File
    <saf-menu slot="submenu">
      <app-saf-menu-item>New File</app-saf-menu-item>
      <app-saf-menu-item>Open File</app-saf-menu-item>
    </saf-menu>
  </app-saf-menu-item>
</saf-menu>
*/
```

### Vue Example

```vue
<template>
  <saf-menu-item
    :role="role"
    :checked="role !== 'menuitem' ? checked : null"
    :disabled="disabled"
    :url="url"
    :has-link="hasLink"
    :router-link="routerLink"
    :link-target="target"
    ref="menuItemRef"
    @change="handleChange"
  >
    <saf-icon
      v-if="startIcon"
      slot="start"
      :name="startIcon"
    ></saf-icon>
    <slot></slot>
    <span v-if="endContent" slot="end">{{ endContent }}</span>
    <slot name="submenu" slot="submenu"></slot>
  </saf-menu-item>
</template>

<script>
export default {
  name: 'SafMenuItemComponent',
  props: {
    role: {
      type: String,
      default: 'menuitem',
      validator: value => ['menuitem', 'menuitemcheckbox', 'menuitemradio'].includes(value)
    },
    checked: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    url: String,
    hasLink: {
      type: Boolean,
      default: false
    },
    routerLink: {
      type: Boolean,
      default: false
    },
    target: {
      type: String,
      validator: value => ['_self', '_blank', '_parent', '_top'].includes(value)
    },
    startIcon: String,
    endContent: String
  },
  emits: ['selection-change', 'navigate'],
  mounted() {
    if (this.routerLink && this.$refs.menuItemRef) {
      this.$refs.menuItemRef.navigate = (path) => {
        this.$emit('navigate', path);
      };
    }
  },
  methods: {
    handleChange() {
      if (this.role === 'menuitemcheckbox' || this.role === 'menuitemradio') {
        this.$emit('selection-change', !this.checked);
      }
    }
  }
};
</script>
```

## Accessibility Features

### ARIA Roles and States

- **menuitem**: Standard menu item
- **menuitemcheckbox**: Checkable menu item with aria-checked state
- **menuitemradio**: Radio button menu item within a group
- **aria-expanded**: Indicates submenu expansion state
- **aria-disabled**: Indicates disabled state

### Keyboard Navigation

- **Enter/Space**: Activate menu item
- **Right Arrow**: Open submenu (if present)
- **Left Arrow/Escape**: Close submenu
- **Mouse hover**: Expand submenus automatically

### Focus Management

- Proper focus indicators for keyboard navigation
- Focus restoration when submenus are closed
- Prevents focus from leaving menu during navigation

## Best Practices

### Menu Item Design
- Use clear, concise labels
- Group related items logically
- Provide keyboard shortcuts where appropriate
- Include helpful icons for better recognition

### Accessibility
- Test with screen readers
- Ensure sufficient color contrast
- Provide alternative text for icons
- Use semantic roles appropriately

### Performance
- Lazy load submenu content
- Limit nesting depth to 2-3 levels
- Use event delegation for large menus
- Cache menu state when appropriate

### User Experience
- Provide visual feedback for interactions
- Use consistent interaction patterns
- Consider mobile touch interactions
- Test across different devices and browsers

## Related Components

- **SafMenu**: Container for menu items
- **SafMenuDivider**: Visual separator between menu groups
- **SafIcon**: Icons for menu items
- **SafPopover**: Positioning for dropdown menus

---

*This documentation covers SafMenuItem v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
