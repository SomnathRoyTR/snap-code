# SafLayoutGrid & SafLayoutGridItem - Grid Layout System

## Overview
`SafLayoutGrid` and `SafLayoutGridItem` provide a flexible, responsive grid layout system based on a 12-column grid. The system supports multiple breakpoints and various sizing options for creating responsive layouts.

## SafLayoutGrid API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `justify-content` | `'start' \| 'center' \| 'end'` | `'start'` | Horizontal alignment of grid items |

### CSS Custom Properties
| Property | Default | Description |
|----------|---------|-------------|
| `--saf-layout-grid-gap` | `16px` | Gap between grid items |
| `--saf-layout-grid-columns` | `12` | Number of columns in the grid |

## SafLayoutGridItem API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `auto-height` | `boolean` | `false` | Allow item to grow to match tallest item in row |
| `justify-content` | `'start' \| 'center' \| 'end'` | `'start'` | Horizontal alignment of item content |
| `xs` | `LayoutGridItemSize` | `undefined` | Column span at extra small breakpoint |
| `sm` | `LayoutGridItemSize` | `undefined` | Column span at small breakpoint |
| `md` | `LayoutGridItemSize` | `undefined` | Column span at medium breakpoint |
| `lg` | `LayoutGridItemSize` | `undefined` | Column span at large breakpoint |
| `xl` | `LayoutGridItemSize` | `undefined` | Column span at extra large breakpoint |
| `xxl` | `LayoutGridItemSize` | `undefined` | Column span at 2x extra large breakpoint |
| `xxxl` | `LayoutGridItemSize` | `undefined` | Column span at 3x extra large breakpoint |
| `xxxxl` | `LayoutGridItemSize` | `undefined` | Column span at 4x extra large breakpoint |

### LayoutGridItemSize Values
- Numbers `0-12`: Fixed column spans
- `'auto'`: Size based on content
- `'fit'`: Fit available space
- `undefined`: Inherit from smaller breakpoint

## Usage Examples

### Basic Grid Layout
```typescript
// React
import { SafLayoutGrid, SafLayoutGridItem } from '@saffron/react';

export const BasicGrid = () => {
  return (
    <SafLayoutGrid>
      <SafLayoutGridItem xs={12} md={6} lg={4}>
        <saf-card>
          <h3>Column 1</h3>
          <p>Content for the first column</p>
        </saf-card>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} md={6} lg={4}>
        <saf-card>
          <h3>Column 2</h3>
          <p>Content for the second column</p>
        </saf-card>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} md={12} lg={4}>
        <saf-card>
          <h3>Column 3</h3>
          <p>Content for the third column</p>
        </saf-card>
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-layout-grid>
      <saf-layout-grid-item xs="12" md="6" lg="4">
        <saf-card>
          <h3>Column 1</h3>
          <p>Content for the first column</p>
        </saf-card>
      </saf-layout-grid-item>
      
      <saf-layout-grid-item xs="12" md="6" lg="4">
        <saf-card>
          <h3>Column 2</h3>
          <p>Content for the second column</p>
        </saf-card>
      </saf-layout-grid-item>
      
      <saf-layout-grid-item xs="12" md="12" lg="4">
        <saf-card>
          <h3>Column 3</h3>
          <p>Content for the third column</p>
        </saf-card>
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class BasicGridComponent {}
```

### Responsive Dashboard Layout
```typescript
// React
export const DashboardLayout = () => {
  return (
    <SafLayoutGrid justify-content="start">
      {/* Header spans full width */}
      <SafLayoutGridItem xs={12}>
        <saf-card>
          <h1>Dashboard Title</h1>
          <p>Welcome to your dashboard</p>
        </saf-card>
      </SafLayoutGridItem>
      
      {/* Main content area */}
      <SafLayoutGridItem xs={12} lg={8}>
        <saf-card auto-height>
          <h2>Main Content</h2>
          <saf-table>
            {/* Table content */}
          </saf-table>
        </saf-card>
      </SafLayoutGridItem>
      
      {/* Sidebar */}
      <SafLayoutGridItem xs={12} lg={4}>
        <saf-card auto-height>
          <h3>Quick Actions</h3>
          <saf-button appearance="primary">Add Item</saf-button>
          <saf-button appearance="secondary">Export Data</saf-button>
        </saf-card>
      </SafLayoutGridItem>
      
      {/* Footer widgets */}
      <SafLayoutGridItem xs={12} sm={6} lg={4}>
        <saf-card>
          <h4>Statistics</h4>
          <p>Total Items: 1,234</p>
        </saf-card>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} sm={6} lg={4}>
        <saf-card>
          <h4>Recent Activity</h4>
          <p>Last updated: Today</p>
        </saf-card>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} sm={12} lg={4}>
        <saf-card>
          <h4>System Status</h4>
          <saf-badge appearance="success">Online</saf-badge>
        </saf-card>
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
};
```

### Centered Layout with Auto Sizing
```typescript
// React
export const CenteredLayout = () => {
  return (
    <SafLayoutGrid justify-content="center">
      <SafLayoutGridItem xs={12} sm={8} md={6} lg={4} justify-content="center">
        <saf-card>
          <h2>Login Form</h2>
          <saf-text-field label="Username" required></saf-text-field>
          <saf-text-field label="Password" type="password" required></saf-text-field>
          <saf-button appearance="primary" style={{ width: '100%' }}>
            Sign In
          </saf-button>
        </saf-card>
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
};
```

### Complex Multi-Section Layout
```typescript
// React
export const ComplexLayout = () => {
  return (
    <div>
      {/* Hero section */}
      <SafLayoutGrid justify-content="center">
        <SafLayoutGridItem xs={12} lg={10} xl={8}>
          <saf-card>
            <h1>Product Features</h1>
            <p>Discover what makes our product unique</p>
          </saf-card>
        </SafLayoutGridItem>
      </SafLayoutGrid>
      
      {/* Feature cards */}
      <SafLayoutGrid>
        <SafLayoutGridItem xs={12} md={6} lg={4} auto-height>
          <saf-card>
            <saf-icon icon-name="shield" size="large"></saf-icon>
            <h3>Security</h3>
            <p>Enterprise-grade security features</p>
          </saf-card>
        </SafLayoutGridItem>
        
        <SafLayoutGridItem xs={12} md={6} lg={4} auto-height>
          <saf-card>
            <saf-icon icon-name="gauge" size="large"></saf-icon>
            <h3>Performance</h3>
            <p>Lightning-fast performance</p>
          </saf-card>
        </SafLayoutGridItem>
        
        <SafLayoutGridItem xs={12} md={12} lg={4} auto-height>
          <saf-card>
            <saf-icon icon-name="users" size="large"></saf-icon>
            <h3>Collaboration</h3>
            <p>Built for team collaboration</p>
          </saf-card>
        </SafLayoutGridItem>
      </SafLayoutGrid>
      
      {/* Content with sidebar */}
      <SafLayoutGrid>
        <SafLayoutGridItem xs={12} lg={8}>
          <saf-card>
            <h2>Detailed Information</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
            
            {/* Nested grid for sub-content */}
            <SafLayoutGrid style={{ marginTop: '24px' }}>
              <SafLayoutGridItem xs={12} sm={6}>
                <h4>Technical Specs</h4>
                <ul>
                  <li>Feature A</li>
                  <li>Feature B</li>
                  <li>Feature C</li>
                </ul>
              </SafLayoutGridItem>
              
              <SafLayoutGridItem xs={12} sm={6}>
                <h4>Requirements</h4>
                <ul>
                  <li>Requirement 1</li>
                  <li>Requirement 2</li>
                  <li>Requirement 3</li>
                </ul>
              </SafLayoutGridItem>
            </SafLayoutGrid>
          </saf-card>
        </SafLayoutGridItem>
        
        <SafLayoutGridItem xs={12} lg={4}>
          <saf-card auto-height>
            <h3>Related Links</h3>
            <saf-anchor href="/documentation">Documentation</saf-anchor>
            <saf-anchor href="/support">Support</saf-anchor>
            <saf-anchor href="/contact">Contact</saf-anchor>
          </saf-card>
        </SafLayoutGridItem>
      </SafLayoutGrid>
    </div>
  );
};
```

### Auto-sizing and Flexible Layouts
```typescript
// React
export const FlexibleLayout = () => {
  return (
    <SafLayoutGrid>
      {/* Auto-sized items */}
      <SafLayoutGridItem xs="auto">
        <saf-button appearance="primary">Auto Width Button</saf-button>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs="fit">
        <saf-text-field placeholder="This field takes remaining space"></saf-text-field>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs="auto">
        <saf-button appearance="secondary">Another Button</saf-button>
      </SafLayoutGridItem>
      
      {/* Form layout with different sizes */}
      <SafLayoutGridItem xs={12} md={8}>
        <saf-text-field label="Full Name" required></saf-text-field>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} md={4}>
        <saf-select label="Country">
          <saf-option value="us">United States</saf-option>
          <saf-option value="ca">Canada</saf-option>
          <saf-option value="uk">United Kingdom</saf-option>
        </saf-select>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} sm={6}>
        <saf-text-field label="Email" type="email"></saf-text-field>
      </SafLayoutGridItem>
      
      <SafLayoutGridItem xs={12} sm={6}>
        <saf-text-field label="Phone" type="tel"></saf-text-field>
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
};
```

## Breakpoint System

The grid system supports the following breakpoints:

- **xs**: 0px+ (all devices)
- **sm**: 576px+ (small tablets and phones in landscape)
- **md**: 768px+ (tablets)
- **lg**: 1024px+ (desktops)
- **xl**: 1200px+ (large desktops)
- **xxl**: 1400px+ (extra large screens)
- **xxxl**: 1600px+ (ultra-wide screens)
- **xxxxl**: 1920px+ (4K displays)

## Best Practices

1. **Mobile-First**: Always define `xs` breakpoint first, then enhance for larger screens
2. **Progressive Enhancement**: Use larger breakpoints to optimize for bigger screens
3. **Content-Aware**: Consider your content when choosing column spans
4. **Auto Height**: Use `auto-height` for cards that should match height in a row
5. **Semantic HTML**: Maintain proper heading hierarchy within grid items
6. **Performance**: Avoid deeply nested grids for better performance
7. **Accessibility**: Ensure content remains accessible at all breakpoints

## Advanced Usage

### Custom Grid Spacing
```typescript
// React with custom spacing
export const CustomSpacingGrid = () => {
  return (
    <SafLayoutGrid 
      style={{
        '--saf-layout-grid-gap': '32px'
      }}
    >
      <SafLayoutGridItem xs={12} md={6}>
        <saf-card>Large gap between items</saf-card>
      </SafLayoutGridItem>
      <SafLayoutGridItem xs={12} md={6}>
        <saf-card>More breathing room</saf-card>
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
};
```

### Responsive Utilities
```typescript
// React component for responsive grid items
interface ResponsiveGridItemProps {
  children: React.ReactNode;
  mobile?: LayoutGridItemSize;
  tablet?: LayoutGridItemSize;
  desktop?: LayoutGridItemSize;
}

export const ResponsiveGridItem: React.FC<ResponsiveGridItemProps> = ({
  children,
  mobile = 12,
  tablet = 6,
  desktop = 4
}) => {
  return (
    <SafLayoutGridItem xs={mobile} md={tablet} lg={desktop}>
      {children}
    </SafLayoutGridItem>
  );
};
```

### CSS Grid Integration
```css
.custom-grid-container {
  --saf-layout-grid-gap: 24px;
  --saf-layout-grid-columns: 16; /* Custom column count */
}

.full-height-grid-item {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.centered-content {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 200px;
}
```

## Notes

- Based on CSS Grid for modern browser support
- Supports nested grids for complex layouts
- Responsive by default with mobile-first approach  
- Integrates seamlessly with other Saffron components
- Optimized for performance with minimal DOM manipulation
- Follows CSS Grid specification for consistent behavior
