# SafSideNav - Side Navigation Component

## Overview
`SafSideNav` is a collapsible side navigation panel component that provides hierarchical navigation functionality. It extends DialogBase and supports both collapsed and expanded states with responsive fullscreen behavior on mobile devices.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `state` | `'closed' \| 'collapsed' \| 'expanded'` | `'closed'` | Current state of the side navigation |
| `open-icon-name` | `string` | `'arrow-right-from-line'` | Icon displayed when side nav is expanded |
| `close-icon-name` | `string` | `'arrow-left-from-line'` | Icon displayed when side nav is collapsed |
| `aria-label` | `string` | `'Side navigation'` | Accessibility label for the side navigation |
| `close-aria-label` | `string` | `undefined` | Aria label for the close/collapse button |
| `open-aria-label` | `string` | `undefined` | Aria label for the open/expand button |
| `fullscreen` | `boolean` | `false` | Whether to display in fullscreen mode on mobile |
| `trigger-id` | `string` | `undefined` | ID of element that triggers the side navigation |

### Properties
| Property | Type | Description |
|----------|------|-------------|
| `activeIndex` | `number` | Currently active menu item index |
| `items` | `HTMLElement[]` | Menu items within the side navigation |
| `titleNodes` | `HTMLElement[]` | Title elements in the header |
| `shouldShowFullscreen` | `boolean` | Whether fullscreen mode should be active |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `close` | `CustomEvent` | Fired when side navigation closes |
| `open` | `CustomEvent` | Fired when side navigation opens |

### Methods
| Method | Description |
|--------|-------------|
| `open()` | Opens the side navigation |
| `close()` | Closes the side navigation |
| `toggle()` | Toggles the side navigation state |

## Usage Examples

### Basic Side Navigation
```typescript
// React
import { SafSideNav } from '@saffron/react';

export const BasicSideNav = () => {
  return (
    <SafSideNav 
      state="collapsed" 
      aria-label="Main navigation"
      onOpen={() => console.log('Side nav opened')}
      onClose={() => console.log('Side nav closed')}
    >
      <div slot="title">Navigation</div>
      <saf-menu-item>Dashboard</saf-menu-item>
      <saf-menu-item>Projects</saf-menu-item>
      <saf-menu-item>Settings</saf-menu-item>
    </SafSideNav>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-side-nav 
      state="collapsed" 
      aria-label="Main navigation"
      (open)="onSideNavOpen()"
      (close)="onSideNavClose()">
      <div slot="title">Navigation</div>
      <saf-menu-item>Dashboard</saf-menu-item>
      <saf-menu-item>Projects</saf-menu-item>
      <saf-menu-item>Settings</saf-menu-item>
    </saf-side-nav>
  `
})
export class BasicSideNavComponent {
  onSideNavOpen() {
    console.log('Side nav opened');
  }
  
  onSideNavClose() {
    console.log('Side nav closed');
  }
}
```

### Hierarchical Navigation
```typescript
// React
export const HierarchicalSideNav = () => {
  return (
    <SafSideNav state="expanded" aria-label="Application navigation">
      <div slot="title">
        <saf-icon icon-name="logo"></saf-icon>
        <span>My App</span>
      </div>
      
      <saf-menu-item role="menuitem">
        <saf-icon icon-name="dashboard" slot="start"></saf-icon>
        Dashboard
      </saf-menu-item>
      
      <saf-menu-item role="menuitem" expanded>
        <saf-icon icon-name="folder" slot="start"></saf-icon>
        Projects
        <saf-menu-item role="menuitem">
          <saf-icon icon-name="file" slot="start"></saf-icon>
          Active Projects
        </saf-menu-item>
        <saf-menu-item role="menuitem">
          <saf-icon icon-name="archive" slot="start"></saf-icon>
          Archived Projects
        </saf-menu-item>
      </saf-menu-item>
      
      <saf-menu-item role="menuitem">
        <saf-icon icon-name="users" slot="start"></saf-icon>
        Team
      </saf-menu-item>
    </SafSideNav>
  );
};
```

### Responsive Side Navigation with Product Header
```typescript
// React
export const ResponsiveSideNav = () => {
  const [sideNavState, setSideNavState] = useState('collapsed');
  
  return (
    <div>
      <saf-product-header>
        <button 
          id="nav-trigger" 
          onClick={() => setSideNavState(prev => 
            prev === 'closed' ? 'expanded' : 'closed'
          )}
        >
          <saf-icon icon-name="menu"></saf-icon>
        </button>
        <div slot="title">Application Title</div>
      </saf-product-header>
      
      <SafSideNav 
        state={sideNavState}
        trigger-id="nav-trigger"
        fullscreen={true}
        aria-label="Main navigation"
        open-aria-label="Expand navigation"
        close-aria-label="Collapse navigation"
      >
        <div slot="title">Navigation Menu</div>
        
        <saf-menu-item>
          <saf-icon icon-name="home" slot="start"></saf-icon>
          Home
        </saf-menu-item>
        
        <saf-menu-item>
          <saf-icon icon-name="chart-line" slot="start"></saf-icon>
          Analytics
        </saf-menu-item>
        
        <saf-menu-item>
          <saf-icon icon-name="settings" slot="start"></saf-icon>
          Settings
        </saf-menu-item>
      </SafSideNav>
    </div>
  );
};
```

### Custom Icons and Labels
```typescript
// React
export const CustomizedSideNav = () => {
  return (
    <SafSideNav 
      state="collapsed"
      open-icon-name="chevron-right"
      close-icon-name="chevron-left"
      aria-label="Application sidebar"
      open-aria-label="Show full navigation"
      close-aria-label="Hide navigation details"
    >
      <div slot="title">
        <saf-icon icon-name="brand-logo"></saf-icon>
        <span>Brand Name</span>
      </div>
      
      <saf-menu-item>
        <saf-icon icon-name="speedometer" slot="start"></saf-icon>
        Performance
        <saf-badge slot="end" appearance="accent">New</saf-badge>
      </saf-menu-item>
      
      <saf-menu-item>
        <saf-icon icon-name="database" slot="start"></saf-icon>
        Data Sources
      </saf-menu-item>
      
      <saf-menu-item>
        <saf-icon icon-name="shield" slot="start"></saf-icon>
        Security
      </saf-menu-item>
    </SafSideNav>
  );
};
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support with arrow keys, Home, End, Enter, and Space
- **Screen Reader Support**: Proper ARIA labels and roles
- **Focus Management**: Maintains focus within navigation when expanded
- **State Announcements**: Screen readers announce state changes
- **High Contrast**: Supports high contrast mode
- **Responsive**: Adapts to mobile with fullscreen overlay

## Best Practices

1. **Clear Navigation Structure**: Use logical hierarchy with menu items
2. **Consistent Icons**: Use consistent iconography for similar functions
3. **Proper Labels**: Provide descriptive aria-labels for accessibility
4. **Responsive Design**: Configure fullscreen mode for mobile experiences
5. **State Management**: Handle state changes appropriately in your application
6. **Focus Management**: Ensure proper focus handling when opening/closing
7. **Performance**: Use resize observer carefully to avoid performance issues

## Advanced Usage

### Programmatic Control
```typescript
// React
const sideNavRef = useRef<SafSideNavInstance>(null);

const handleToggle = () => {
  const sideNav = sideNavRef.current;
  if (sideNav) {
    if (sideNav.state === 'closed') {
      sideNav.open();
    } else {
      sideNav.close();
    }
  }
};

return (
  <SafSideNav ref={sideNavRef} state="collapsed">
    {/* Navigation content */}
  </SafSideNav>
);
```

### Custom Styling
```css
saf-side-nav {
  --saf-side-nav-width: 280px;
  --saf-side-nav-collapsed-width: 64px;
  --saf-side-nav-background: var(--neutral-layer-1);
  --saf-side-nav-border-color: var(--neutral-stroke-divider-rest);
}

saf-side-nav[state="expanded"] {
  --saf-side-nav-box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
```

## Notes

- Automatically adapts to mobile viewport with fullscreen overlay
- Integrates with SafProductHeader for responsive behavior
- Supports nested menu items with proper keyboard navigation
- Uses ResizeObserver for responsive behavior monitoring
- Extends DialogBase for modal-like behavior in fullscreen mode
