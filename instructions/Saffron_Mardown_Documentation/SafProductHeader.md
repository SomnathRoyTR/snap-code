# SafProductHeader Component

The `SafProductHeader` component provides a comprehensive navigation header for Thomson Reuters products in the Saffron Design System. Built on FAST Element, it offers logo placement, task navigation, global navigation, responsive menu behavior, and accessibility features for application headers.

## Table of Contents

- [Overview](#overview)
- [Component Properties](#component-properties)
- [Events](#events)
- [Methods](#methods)
- [Parts](#parts)
- [Slots](#slots)
- [CSS Custom Properties](#css-custom-properties)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Accessibility](#accessibility)
- [Best Practices](#best-practices)

## Overview

The SafProductHeader component serves as the primary navigation header for Thomson Reuters applications. It provides structured areas for branding, task-specific actions, global actions, and responsive menu behavior.

Key Features:
- **Logo Integration**: Dedicated slot for Thomson Reuters branding
- **Task Navigation**: Left-side navigation for product-specific actions
- **Global Navigation**: Right-side navigation for global actions
- **Responsive Menu**: Adaptive menu for mobile and narrow viewports
- **Side Navigation**: Integration point for side navigation triggers
- **Accessibility**: Full ARIA support with proper navigation landmarks
- **Automatic Styling**: Auto-applies styling attributes to child components

## Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `globalAriaLabel` | `string` | `"Global"` | ARIA label for global navigation region |
| `tasksAriaLabel` | `string` | `"Product"` | ARIA label for tasks navigation region |
| `isMenuOpen` | `boolean` | `false` | Controls mobile menu open state |

### Read-Only Properties

| Property | Type | Description |
|----------|------|-------------|
| `_showDivider` | `boolean` | Whether to show divider between task and global navigation |
| `_hasMenuItems` | `boolean` | Whether menu slot contains items |
| `prodHeaderMenuItems` | `HTMLElement[]` | Array of menu items for keyboard navigation |
| `menuButton` | `HTMLElement` | Reference to mobile menu trigger button |
| `anchoredRegion` | `HTMLElement` | Reference to mobile menu container |

## Events

The SafProductHeader component primarily relies on child component events rather than emitting its own events. However, it manages:

- **Menu Interactions**: Internal click and keyboard event handling
- **Focus Management**: Keyboard navigation within mobile menu
- **Outside Clicks**: Automatic menu closure when clicking outside

## Methods

### Menu Management

```typescript
// Toggle mobile menu
productHeader.handleMenuButtonClick(): void

// Close menu (internal)
productHeader.closeMenu(): void

// Remove selected state from menu items
productHeader.removeSelectedClass(): void
```

### Event Handlers

```typescript
// Handle clicks outside menu
productHeader.handleClickOutside(event: Event): void

// Handle keyboard navigation on menu button
productHeader.handleButtonKeyDown(event: KeyboardEvent): void

// Handle keyboard navigation within menu
productHeader.handleBackgroundKeyDown(event: KeyboardEvent): void
```

### Internal Methods

```typescript
// Add product-header-item attributes to child components
productHeader.addProductHeaderItemAttribute(): void

// Check if divider should be shown
productHeader.checkDivider(): void

// Check for menu items
productHeader.checkMenuItems(): void

// Configure logo elements
productHeader.checkLogo(): void
```

## Parts

| Part | Description |
|------|-------------|
| `side-nav-trigger` | Container for side navigation trigger |
| `navigation` | Main navigation container |
| `tasks-navigation` | Left-side task navigation |
| `tasks-list` | Task navigation list container |
| `global-navigation` | Right-side global navigation |
| `global-list` | Global navigation list container |
| `mobile-menu` | Mobile menu container |
| `adaptive-menu-region` | Anchored region for mobile menu |

## Slots

| Slot | Description |
|------|-------------|
| `logo` | Thomson Reuters logo or brand element |
| `side-nav-trigger` | Side navigation trigger button |
| `tasks` | Task/product-specific navigation items |
| `global` | Global application navigation items |
| `menu` | Mobile menu items (for responsive behavior) |

## CSS Custom Properties

The SafProductHeader component uses the design system's spacing and color tokens:

```css
saf-product-header {
  /* Header height */
  --header-height: 56px;
  
  /* Navigation spacing */
  --navigation-padding: var(--space-md);
  
  /* Mobile breakpoint */
  --mobile-breakpoint: 768px;
}
```

## React Integration

### Basic Usage

```tsx
import SafProductHeader from '@saffron/react/product-header';
import SafProductHeaderItem from '@saffron/react/product-header-item';
import SafLogo from '@saffron/react/logo';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';
import SafAnchor from '@saffron/react/anchor';

function ApplicationHeader() {
  return (
    <SafProductHeader>
      <SafAnchor href="/" slot="logo">
        <SafLogo 
          appearance="1-color-reversed" 
          productName="My Product" 
        />
      </SafAnchor>
      
      <div slot="tasks">
        <SafProductHeaderItem>
          <SafButton appearance="tertiary" iconOnly>
            <SafIcon iconName="magnifying-glass" size="16" />
          </SafButton>
        </SafProductHeaderItem>
      </div>
      
      <div slot="global">
        <SafProductHeaderItem>
          <SafButton appearance="tertiary" iconOnly>
            <SafIcon iconName="bell" size="16" />
          </SafButton>
        </SafProductHeaderItem>
      </div>
    </SafProductHeader>
  );
}
```

### With Side Navigation Trigger

```tsx
import SafProductHeader from '@saffron/react/product-header';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';

function HeaderWithSideNav() {
  const [sideNavOpen, setSideNavOpen] = useState(false);
  
  return (
    <SafProductHeader>
      <SafButton 
        slot="side-nav-trigger"
        appearance="tertiary" 
        iconOnly
        onClick={() => setSideNavOpen(!sideNavOpen)}
      >
        <SafIcon iconName="bars" size="16" />
      </SafButton>
      
      {/* Logo and navigation items */}
    </SafProductHeader>
  );
}
```

### With Mobile Menu

```tsx
import SafProductHeader from '@saffron/react/product-header';
import SafProductHeaderItem from '@saffron/react/product-header-item';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';

function ResponsiveHeader() {
  return (
    <SafProductHeader>
      {/* Logo slot */}
      <SafAnchor href="/" slot="logo">
        <SafLogo productName="My Product" />
      </SafAnchor>
      
      {/* Task navigation */}
      <div slot="tasks">
        <SafProductHeaderItem>
          <SafButton appearance="tertiary">Search</SafButton>
        </SafProductHeaderItem>
        <SafProductHeaderItem>
          <SafButton appearance="tertiary">Favorites</SafButton>
        </SafProductHeaderItem>
      </div>
      
      {/* Global navigation */}
      <div slot="global">
        <SafProductHeaderItem>
          <SafButton appearance="tertiary" iconOnly>
            <SafIcon iconName="bell" size="16" />
          </SafButton>
        </SafProductHeaderItem>
        <SafProductHeaderItem>
          <SafButton appearance="tertiary" iconOnly>
            <SafIcon iconName="user" size="16" />
          </SafButton>
        </SafProductHeaderItem>
      </div>
      
      {/* Mobile menu */}
      <div slot="menu">
        <SafButton appearance="tertiary">Search</SafButton>
        <SafButton appearance="tertiary">Favorites</SafButton>
        <SafButton appearance="tertiary">Notifications</SafButton>
        <SafButton appearance="tertiary">Profile</SafButton>
      </div>
    </SafProductHeader>
  );
}
```

### With Custom ARIA Labels

```tsx
import SafProductHeader from '@saffron/react/product-header';

function AccessibleHeader() {
  return (
    <SafProductHeader
      tasksAriaLabel="Document tasks"
      globalAriaLabel="Account and settings"
    >
      {/* Navigation items */}
    </SafProductHeader>
  );
}
```

### With Search Integration

```tsx
import SafProductHeader from '@saffron/react/product-header';
import SafProductHeaderItem from '@saffron/react/product-header-item';
import SafSearchField from '@saffron/react/search-field';
import SafButton from '@saffron/react/button';

function HeaderWithSearch() {
  const [searchValue, setSearchValue] = useState('');
  
  return (
    <SafProductHeader>
      <SafAnchor href="/" slot="logo">
        <SafLogo productName="Search App" />
      </SafAnchor>
      
      <div slot="tasks">
        <SafProductHeaderItem>
          <SafSearchField 
            value={searchValue}
            onInput={(e) => setSearchValue(e.target.value)}
            placeholder="Search documents..."
          />
        </SafProductHeaderItem>
      </div>
      
      <div slot="global">
        <SafProductHeaderItem>
          <SafButton appearance="tertiary" iconOnly>
            <SafIcon iconName="circle-question" size="16" />
          </SafButton>
        </SafProductHeaderItem>
      </div>
    </SafProductHeader>
  );
}
```

## Angular Integration

### Basic Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  template: `
    <saf-product-header>
      <saf-anchor href="/" slot="logo">
        <saf-logo 
          appearance="1-color-reversed" 
          product-name="My Product">
        </saf-logo>
      </saf-anchor>
      
      <div slot="tasks">
        <saf-product-header-item>
          <saf-button appearance="tertiary" icon-only>
            <saf-icon icon-name="magnifying-glass" size="16"></saf-icon>
          </saf-button>
        </saf-product-header-item>
      </div>
      
      <div slot="global">
        <saf-product-header-item>
          <saf-button appearance="tertiary" icon-only>
            <saf-icon icon-name="bell" size="16"></saf-icon>
          </saf-button>
        </saf-product-header-item>
      </div>
    </saf-product-header>
  `
})
export class HeaderComponent {}
```

### With Navigation Service

```typescript
import { Component, inject } from '@angular/core';
import { NavigationService } from './navigation.service';

@Component({
  selector: 'app-main-header',
  template: `
    <saf-product-header
      [tasks-aria-label]="tasksAriaLabel"
      [global-aria-label]="globalAriaLabel">
      
      <saf-button 
        slot="side-nav-trigger"
        appearance="tertiary" 
        icon-only
        (click)="toggleSideNav()">
        <saf-icon icon-name="bars" size="16"></saf-icon>
      </saf-button>
      
      <saf-anchor href="/" slot="logo">
        <saf-logo [product-name]="applicationName"></saf-logo>
      </saf-anchor>
      
      <div slot="tasks">
        <saf-product-header-item *ngFor="let task of taskItems">
          <saf-button 
            [appearance]="task.appearance"
            [icon-only]="task.iconOnly"
            (click)="handleTaskAction(task.action)">
            <saf-icon 
              [icon-name]="task.icon" 
              size="16">
            </saf-icon>
            <span *ngIf="!task.iconOnly">{{ task.label }}</span>
          </saf-button>
        </saf-product-header-item>
      </div>
      
      <div slot="global">
        <saf-product-header-item *ngFor="let item of globalItems">
          <saf-button 
            appearance="tertiary" 
            icon-only
            (click)="handleGlobalAction(item.action)">
            <saf-icon [icon-name]="item.icon" size="16"></saf-icon>
          </saf-button>
        </saf-product-header-item>
      </div>
    </saf-product-header>
  `
})
export class MainHeaderComponent {
  private navigationService = inject(NavigationService);
  
  applicationName = 'Document Manager';
  tasksAriaLabel = 'Document tasks';
  globalAriaLabel = 'Account and settings';
  
  taskItems = [
    { 
      icon: 'magnifying-glass', 
      action: 'search', 
      appearance: 'tertiary', 
      iconOnly: true 
    },
    { 
      icon: 'star', 
      action: 'favorites', 
      appearance: 'tertiary', 
      iconOnly: true 
    }
  ];
  
  globalItems = [
    { icon: 'circle-question', action: 'help' },
    { icon: 'bell', action: 'notifications' },
    { icon: 'user', action: 'profile' }
  ];
  
  toggleSideNav() {
    this.navigationService.toggleSideNavigation();
  }
  
  handleTaskAction(action: string) {
    this.navigationService.executeTaskAction(action);
  }
  
  handleGlobalAction(action: string) {
    this.navigationService.executeGlobalAction(action);
  }
}
```

### With Responsive Menu

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-responsive-header',
  template: `
    <saf-product-header>
      <saf-anchor href="/" slot="logo">
        <saf-logo product-name="My App"></saf-logo>
      </saf-anchor>
      
      <div slot="tasks">
        <saf-product-header-item>
          <saf-search-field 
            placeholder="Search..."
            [(ngModel)]="searchQuery">
          </saf-search-field>
        </saf-product-header-item>
      </div>
      
      <div slot="global">
        <saf-product-header-item>
          <saf-button appearance="tertiary" icon-only>
            <saf-icon icon-name="bell" size="16"></saf-icon>
          </saf-button>
        </saf-product-header-item>
      </div>
      
      <!-- Mobile menu items -->
      <div slot="menu">
        <saf-button 
          *ngFor="let item of mobileMenuItems"
          appearance="tertiary"
          (click)="handleMobileMenuAction(item.action)">
          {{ item.label }}
        </saf-button>
      </div>
    </saf-product-header>
  `
})
export class ResponsiveHeaderComponent {
  searchQuery = '';
  
  mobileMenuItems = [
    { label: 'Search', action: 'search' },
    { label: 'Favorites', action: 'favorites' },
    { label: 'Notifications', action: 'notifications' },
    { label: 'Profile', action: 'profile' }
  ];
  
  handleMobileMenuAction(action: string) {
    console.log('Mobile menu action:', action);
  }
}
```

### With Route-Based Navigation

```typescript
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-navigation-header',
  template: `
    <saf-product-header>
      <saf-anchor [href]="homeRoute" slot="logo">
        <saf-logo product-name="My Platform"></saf-logo>
      </saf-anchor>
      
      <div slot="tasks">
        <saf-product-header-item 
          *ngFor="let route of taskRoutes">
          <saf-anchor [href]="route.path">
            <saf-button appearance="tertiary">
              <saf-icon 
                slot="start" 
                [icon-name]="route.icon" 
                size="16">
              </saf-icon>
              {{ route.label }}
            </saf-button>
          </saf-anchor>
        </saf-product-header-item>
      </div>
      
      <div slot="global">
        <saf-product-header-item>
          <saf-button 
            appearance="tertiary" 
            icon-only
            (click)="logout()">
            <saf-icon icon-name="right-from-bracket" size="16"></saf-icon>
          </saf-button>
        </saf-product-header-item>
      </div>
    </saf-product-header>
  `
})
export class NavigationHeaderComponent {
  homeRoute = '/dashboard';
  
  taskRoutes = [
    { path: '/documents', label: 'Documents', icon: 'file-text' },
    { path: '/search', label: 'Search', icon: 'magnifying-glass' },
    { path: '/reports', label: 'Reports', icon: 'chart-bar' }
  ];
  
  constructor(private router: Router) {}
  
  logout() {
    // Handle logout logic
    this.router.navigate(['/login']);
  }
}
```

## Usage Examples

### Basic Product Header

```html
<saf-product-header>
  <saf-anchor href="/" slot="logo">
    <saf-logo product-name="My Product"></saf-logo>
  </saf-anchor>
  
  <div slot="tasks">
    <saf-product-header-item>
      <saf-button appearance="tertiary">Search</saf-button>
    </saf-product-header-item>
  </div>
  
  <div slot="global">
    <saf-product-header-item>
      <saf-button appearance="tertiary" icon-only>
        <saf-icon icon-name="bell" size="16"></saf-icon>
      </saf-button>
    </saf-product-header-item>
  </div>
</saf-product-header>
```

### With Side Navigation Trigger

```html
<saf-product-header>
  <saf-button slot="side-nav-trigger" appearance="tertiary" icon-only>
    <saf-icon icon-name="bars" size="16"></saf-icon>
  </saf-button>
  
  <saf-anchor href="/" slot="logo">
    <saf-logo product-name="My App"></saf-logo>
  </saf-anchor>
</saf-product-header>
```

### With Search Field

```html
<saf-product-header>
  <saf-anchor href="/" slot="logo">
    <saf-logo product-name="Search Platform"></saf-logo>
  </saf-anchor>
  
  <div slot="tasks">
    <saf-product-header-item>
      <saf-search-field placeholder="Search documents..."></saf-search-field>
    </saf-product-header-item>
  </div>
</saf-product-header>
```

### With Custom ARIA Labels

```html
<saf-product-header 
  tasks-aria-label="Document management tools"
  global-aria-label="User account and settings">
  <!-- Navigation items -->
</saf-product-header>
```

### Full Featured Header

```html
<saf-product-header>
  <saf-button slot="side-nav-trigger" appearance="tertiary" icon-only>
    <saf-icon icon-name="bars" size="16"></saf-icon>
  </saf-button>
  
  <saf-anchor href="/" slot="logo">
    <saf-logo 
      appearance="1-color-reversed" 
      product-name="Enterprise Platform">
    </saf-logo>
  </saf-anchor>
  
  <div slot="tasks">
    <saf-product-header-item>
      <saf-search-field placeholder="Search..."></saf-search-field>
    </saf-product-header-item>
    <saf-product-header-item>
      <saf-button appearance="tertiary" icon-only>
        <saf-icon icon-name="star" size="16"></saf-icon>
      </saf-button>
    </saf-product-header-item>
  </div>
  
  <div slot="global">
    <saf-product-header-item>
      <saf-button appearance="tertiary" icon-only>
        <saf-icon icon-name="circle-question" size="16"></saf-icon>
      </saf-button>
    </saf-product-header-item>
    <saf-product-header-item>
      <saf-button appearance="tertiary" icon-only>
        <saf-icon icon-name="bell" size="16"></saf-icon>
      </saf-button>
    </saf-product-header-item>
    <saf-product-header-item>
      <saf-button appearance="tertiary" icon-only>
        <saf-icon icon-name="user" size="16"></saf-icon>
      </saf-button>
    </saf-product-header-item>
  </div>
  
  <div slot="menu">
    <saf-button appearance="tertiary">Search</saf-button>
    <saf-button appearance="tertiary">Favorites</saf-button>
    <saf-button appearance="tertiary">Help</saf-button>
    <saf-button appearance="tertiary">Notifications</saf-button>
    <saf-button appearance="tertiary">Profile</saf-button>
  </div>
</saf-product-header>
```

## Accessibility

The SafProductHeader component provides comprehensive accessibility support:

### ARIA Implementation
- **role="navigation"**: Applied to task and global navigation regions
- **aria-label**: Customizable labels for each navigation region
- **role="list/listitem"**: Proper list semantics for navigation items
- **aria-expanded**: Mobile menu button state
- **aria-haspopup**: Mobile menu button popup indication
- **aria-controls**: Links menu button to menu content

### Keyboard Support
- **Tab Navigation**: All interactive elements accessible via Tab
- **Enter/Space**: Activates buttons and links
- **Arrow Keys**: Mobile menu navigation (Down arrow opens menu)
- **Escape**: Closes mobile menu and returns focus to button

### Mobile Menu Accessibility
- **Focus Management**: Automatic focus to first menu item when opened
- **Keyboard Navigation**: Full keyboard support within menu
- **Focus Return**: Returns focus to trigger button when closed
- **Outside Click**: Closes menu and manages focus appropriately

### Screen Reader Support
- **Navigation Landmarks**: Clear navigation regions for screen readers
- **Descriptive Labels**: Meaningful labels for all interactive elements
- **State Announcements**: Menu state changes announced
- **Semantic Structure**: Proper heading and list structure

## Best Practices

### Content Organization
- Use the logo slot for primary branding and home navigation
- Place task-specific actions in the tasks slot (left side)
- Place global actions in the global slot (right side)
- Provide mobile menu items that mirror desktop navigation

### Navigation Design
- Keep task navigation focused on current page/section functionality
- Use global navigation for cross-application actions
- Provide clear icons and labels for all actions
- Consider progressive disclosure for complex navigation

### Responsive Behavior
- Design mobile menu items to represent all key functionality
- Test navigation at various screen sizes
- Ensure touch targets meet minimum size requirements
- Consider gesture-based navigation on mobile devices

### Accessibility
- Provide meaningful ARIA labels for navigation regions
- Use descriptive button labels and icon alternatives
- Test keyboard navigation thoroughly
- Ensure sufficient color contrast for all states

### Performance
- Lazy load heavy navigation components when possible
- Optimize icon assets for faster loading
- Consider preloading critical navigation destinations
- Use efficient event handling for menu interactions

### Brand Consistency
- Use appropriate SafLogo configurations for your product
- Follow Thomson Reuters brand guidelines
- Maintain consistent styling across application headers
- Use standard iconography from the design system

### State Management
- Handle menu state consistently across page transitions
- Coordinate header state with side navigation if used
- Provide clear visual feedback for active navigation items
- Consider URL-based navigation state when appropriate

The SafProductHeader component provides a robust foundation for application navigation while maintaining accessibility, brand consistency, and responsive behavior across all Thomson Reuters products.
