# SafContainer - Layout Container Component

## Overview
`SafContainer` is a responsive layout container component that provides consistent spacing, centering, and maximum width constraints for content layout. It uses CSS container queries for responsive behavior and supports flexible padding management.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `max-width` | `Breakpoint` | `undefined` | Maximum width constraint (xs, sm, md, lg, xl, xxl) |
| `centered` | `boolean` | `false` | Whether content should be horizontally centered |
| `disable-padding` | `boolean` | `false` | Disables default padding (useful for nested components) |

### CSS Custom Properties
| Property | Default | Description |
|----------|---------|-------------|
| `--saf-container-padding-x` | `16px` | Horizontal padding |
| `--saf-container-padding-y` | `32px` | Vertical padding |
| `--saf-container-max-width-xs` | `480px` | Extra small breakpoint max width |
| `--saf-container-max-width-sm` | `768px` | Small breakpoint max width |
| `--saf-container-max-width-md` | `1024px` | Medium breakpoint max width |
| `--saf-container-max-width-lg` | `1280px` | Large breakpoint max width |
| `--saf-container-max-width-xl` | `1440px` | Extra large breakpoint max width |
| `--saf-container-max-width-xxl` | `1920px` | Extra extra large breakpoint max width |

## Usage Examples

### Basic Container
```typescript
// React
import { SafContainer } from '@saffron/react';

export const BasicContainer = () => {
  return (
    <SafContainer>
      <h1>Page Title</h1>
      <p>This content is contained within the default container constraints.</p>
    </SafContainer>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-container>
      <h1>Page Title</h1>
      <p>This content is contained within the default container constraints.</p>
    </saf-container>
  `
})
export class BasicContainerComponent {}
```

### Centered Container with Max Width
```typescript
// React
export const CenteredContainer = () => {
  return (
    <SafContainer max-width="lg" centered={true}>
      <div style={{ textAlign: 'center' }}>
        <h1>Centered Content</h1>
        <p>This container is centered and constrained to a maximum width of 'lg'.</p>
        <button>Call to Action</button>
      </div>
    </SafContainer>
  );
};

// Angular
@Component({
  template: `
    <saf-container max-width="lg" centered="true">
      <div style="text-align: center">
        <h1>Centered Content</h1>
        <p>This container is centered and constrained to a maximum width of 'lg'.</p>
        <button>Call to Action</button>
      </div>
    </saf-container>
  `
})
export class CenteredContainerComponent {}
```

### Container Without Padding
```typescript
// React - Useful for components that provide their own spacing
export const NoPaddingContainer = () => {
  return (
    <SafContainer disable-padding={true}>
      <saf-tabs>
        <saf-tab>Tab 1</saf-tab>
        <saf-tab>Tab 2</saf-tab>
        <saf-tab-panel>
          <p>Tab content with its own internal padding</p>
        </saf-tab-panel>
        <saf-tab-panel>
          <p>Another tab panel</p>
        </saf-tab-panel>
      </saf-tabs>
    </SafContainer>
  );
};
```

### Responsive Layout with Multiple Containers
```typescript
// React
export const ResponsiveLayout = () => {
  return (
    <div>
      {/* Header container - full width */}
      <SafContainer max-width="xxl" disable-padding={true}>
        <header style={{ padding: '16px' }}>
          <saf-product-header>
            <span slot="title">Application Title</span>
          </saf-product-header>
        </header>
      </SafContainer>
      
      {/* Main content - constrained width */}
      <SafContainer max-width="xl" centered={true}>
        <main>
          <h1>Main Content</h1>
          <saf-card>
            <h2>Article Title</h2>
            <p>Article content goes here...</p>
          </saf-card>
        </main>
      </SafContainer>
      
      {/* Footer - full width */}
      <SafContainer max-width="xxl">
        <footer>
          <p>&copy; 2024 Company Name</p>
        </footer>
      </SafContainer>
    </div>
  );
};
```

### Nested Containers
```typescript
// React
export const NestedContainers = () => {
  return (
    <SafContainer max-width="xl">
      <section>
        <h1>Section Title</h1>
        
        {/* Nested container with different constraints */}
        <SafContainer max-width="md" centered={true} disable-padding={true}>
          <saf-card>
            <h2>Focused Content</h2>
            <p>This card is in a nested container with tighter width constraints.</p>
          </saf-card>
        </SafContainer>
        
        <p>This paragraph is back in the outer container scope.</p>
      </section>
    </SafContainer>
  );
};
```

### Custom Spacing
```typescript
// React with custom CSS properties
export const CustomSpacingContainer = () => {
  return (
    <SafContainer 
      max-width="lg" 
      centered={true}
      style={{
        '--saf-container-padding-x': '24px',
        '--saf-container-padding-y': '48px'
      }}
    >
      <h1>Custom Spaced Content</h1>
      <p>This container has custom horizontal and vertical padding.</p>
    </SafContainer>
  );
};
```

### Page Layout Pattern
```typescript
// React - Common page layout structure
export const PageLayout = ({ children }: { children: React.ReactNode }) => {
  return (
    <div className="page-layout">
      {/* Navigation */}
      <SafContainer max-width="xxl" disable-padding={true}>
        <nav>
          <saf-breadcrumb>
            <saf-breadcrumb-item href="/">Home</saf-breadcrumb-item>
            <saf-breadcrumb-item href="/products">Products</saf-breadcrumb-item>
            <saf-breadcrumb-item>Details</saf-breadcrumb-item>
          </saf-breadcrumb>
        </nav>
      </SafContainer>
      
      {/* Main content area */}
      <SafContainer max-width="xl" centered={true}>
        <main className="main-content">
          {children}
        </main>
      </SafContainer>
      
      {/* Aside content */}
      <SafContainer max-width="sm" centered={true}>
        <aside>
          <saf-card>
            <h3>Related Information</h3>
            <p>Sidebar content here...</p>
          </saf-card>
        </aside>
      </SafContainer>
    </div>
  );
};
```

## Breakpoint System

The container supports the following breakpoint values for `max-width`:

- **xs**: 480px - Mobile devices
- **sm**: 768px - Small tablets
- **md**: 1024px - Tablets and small desktops
- **lg**: 1280px - Standard desktop
- **xl**: 1440px - Large desktop
- **xxl**: 1920px - Extra large screens

## Best Practices

1. **Semantic Structure**: Use containers to create logical content boundaries
2. **Responsive Design**: Choose appropriate max-width values for your content
3. **Consistent Spacing**: Leverage the default padding system or disable it for special cases
4. **Nesting**: Use nested containers sparingly and with different constraints
5. **Performance**: Containers use CSS container queries for optimal performance
6. **Accessibility**: Ensure content remains accessible at all breakpoints

## Advanced Usage

### Dynamic Container Properties
```typescript
// React
interface ContentContainerProps {
  variant: 'narrow' | 'wide' | 'full';
  children: React.ReactNode;
}

export const ContentContainer: React.FC<ContentContainerProps> = ({ variant, children }) => {
  const getMaxWidth = () => {
    switch (variant) {
      case 'narrow': return 'md';
      case 'wide': return 'xl';
      case 'full': return 'xxl';
      default: return 'lg';
    }
  };
  
  return (
    <SafContainer 
      max-width={getMaxWidth()} 
      centered={variant !== 'full'}
    >
      {children}
    </SafContainer>
  );
};
```

### Custom CSS Integration
```css
.custom-container {
  --saf-container-padding-x: clamp(16px, 4vw, 48px);
  --saf-container-padding-y: clamp(24px, 6vh, 64px);
}

.compact-container {
  --saf-container-padding-x: 12px;
  --saf-container-padding-y: 16px;
}

.spacious-container {
  --saf-container-padding-x: 32px;
  --saf-container-padding-y: 48px;
}
```

## Notes

- Uses CSS container queries for responsive behavior
- Provides consistent spacing across your application
- Integrates well with other Saffron layout components
- Supports both fixed and fluid layouts
- Optimized for performance with minimal DOM impact
