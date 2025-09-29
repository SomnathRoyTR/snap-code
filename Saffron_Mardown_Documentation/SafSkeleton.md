# SafSkeleton Component

The **SafSkeleton** component provides placeholder content that mimics the layout of actual content while it loads. It supports different shapes, appearances, and loading animations to create smooth loading experiences.

## Basic Usage

```html
<!-- Basic rectangular skeleton -->
<saf-skeleton></saf-skeleton>

<!-- Circular skeleton for avatars -->
<saf-skeleton shape="circle"></saf-skeleton>

<!-- Skeleton with shimmer animation -->
<saf-skeleton shimmer></saf-skeleton>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `shape` | `'rect' \| 'circle'` | `'rect'` | Shape of the skeleton |
| `appearance` | `'small' \| 'large' \| 'table'` | `'small'` | Size and style variant |
| `background` | `'transparent' \| 'card'` | `'card'` | Background style |
| `shimmer` | `boolean` | `false` | Whether to show loading animation |
| `fill` | `string` | - | Custom fill color or pattern |
| `pattern` | `string` | - | URL pattern for custom skeleton texture |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `shape` | `SkeletonShape` | `'rect'` | Current shape setting |
| `appearance` | `SkeletonAppearance` | `'small'` | Current appearance variant |
| `background` | `SkeletonBackground` | `'card'` | Current background type |
| `shimmer` | `boolean` | `false` | Animation state |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Custom skeleton content or nested elements |

### CSS Parts

| Part | Description |
|------|-------------|
| `skeleton` | Main skeleton container |

## Shape Options

| Shape | Description | Best Used For |
|-------|-------------|---------------|
| `'rect'` | Rectangular shape | Text, cards, images, buttons |
| `'circle'` | Circular shape | Avatars, profile pictures, icons |

## Appearance Options

| Appearance | Description | Best Used For |
|------------|-------------|---------------|
| `'small'` | Compact size | List items, small text blocks |
| `'large'` | Larger size | Headers, hero sections, images |
| `'table'` | Table-optimized | Data tables, structured layouts |

## Background Options

| Background | Description | Best Used For |
|------------|-------------|---------------|
| `'card'` | Solid background | Cards, panels, distinct sections |
| `'transparent'` | Transparent background | Inline content, subtle placeholders |

## Comprehensive Examples

### Basic Skeletons

```html
<div class="skeleton-examples">
  <!-- Small rectangular skeleton -->
  <saf-skeleton appearance="small"></saf-skeleton>
  
  <!-- Large rectangular skeleton -->
  <saf-skeleton appearance="large"></saf-skeleton>
  
  <!-- Circular skeleton -->
  <saf-skeleton shape="circle" appearance="small"></saf-skeleton>
  
  <!-- Skeleton with shimmer animation -->
  <saf-skeleton shimmer appearance="large"></saf-skeleton>
</div>

<style>
.skeleton-examples {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1rem;
}

saf-skeleton {
  height: 20px;
}

saf-skeleton[appearance="large"] {
  height: 40px;
}

saf-skeleton[shape="circle"] {
  width: 40px;
  height: 40px;
}
</style>
```

### Card Layout Skeleton

```html
<div class="card-skeleton">
  <div class="avatar-section">
    <saf-skeleton shape="circle" shimmer style="width: 48px; height: 48px;"></saf-skeleton>
    <div class="user-info">
      <saf-skeleton appearance="small" style="width: 120px; height: 16px;"></saf-skeleton>
      <saf-skeleton appearance="small" style="width: 80px; height: 14px; margin-top: 4px;"></saf-skeleton>
    </div>
  </div>
  
  <div class="content-section">
    <saf-skeleton appearance="large" style="width: 100%; height: 20px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 100%; height: 16px; margin-top: 8px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 75%; height: 16px; margin-top: 4px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 50%; height: 16px; margin-top: 4px;"></saf-skeleton>
  </div>
  
  <div class="image-section">
    <saf-skeleton appearance="large" style="width: 100%; height: 200px; margin: 12px 0;"></saf-skeleton>
  </div>
  
  <div class="actions-section">
    <saf-skeleton appearance="small" style="width: 80px; height: 32px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 100px; height: 32px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 60px; height: 32px;"></saf-skeleton>
  </div>
</div>

<style>
.card-skeleton {
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
  max-width: 400px;
}

.avatar-section {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 16px;
}

.user-info {
  flex: 1;
}

.content-section {
  margin-bottom: 16px;
}

.actions-section {
  display: flex;
  gap: 8px;
}
</style>
```

### Table Skeleton

```html
<div class="table-skeleton">
  <div class="table-header">
    <saf-skeleton appearance="table" style="width: 120px; height: 24px;"></saf-skeleton>
    <saf-skeleton appearance="table" style="width: 150px; height: 24px;"></saf-skeleton>
    <saf-skeleton appearance="table" style="width: 100px; height: 24px;"></saf-skeleton>
    <saf-skeleton appearance="table" style="width: 80px; height: 24px;"></saf-skeleton>
  </div>
  
  <div class="table-row" data-repeat="5">
    <saf-skeleton appearance="table" background="transparent" style="width: 120px; height: 20px;"></saf-skeleton>
    <saf-skeleton appearance="table" background="transparent" style="width: 150px; height: 20px;"></saf-skeleton>
    <saf-skeleton appearance="table" background="transparent" style="width: 100px; height: 20px;"></saf-skeleton>
    <saf-skeleton appearance="table" background="transparent" style="width: 80px; height: 20px;"></saf-skeleton>
  </div>
</div>

<style>
.table-skeleton {
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  overflow: hidden;
}

.table-header {
  display: grid;
  grid-template-columns: 120px 150px 100px 80px;
  gap: 1rem;
  padding: 12px 16px;
  background: #f5f5f5;
  border-bottom: 1px solid #e0e0e0;
}

.table-row {
  display: grid;
  grid-template-columns: 120px 150px 100px 80px;
  gap: 1rem;
  padding: 12px 16px;
  border-bottom: 1px solid #f0f0f0;
}

.table-row:last-child {
  border-bottom: none;
}
</style>

<!-- JavaScript to duplicate table rows -->
<script>
document.querySelectorAll('[data-repeat]').forEach(element => {
  const count = parseInt(element.dataset.repeat);
  const parent = element.parentNode;
  
  for (let i = 1; i < count; i++) {
    const clone = element.cloneNode(true);
    clone.removeAttribute('data-repeat');
    parent.appendChild(clone);
  }
});
</script>
```

### List Skeleton

```html
<div class="list-skeleton">
  <div class="list-item">
    <saf-skeleton shape="circle" style="width: 32px; height: 32px;"></saf-skeleton>
    <div class="list-content">
      <saf-skeleton appearance="small" style="width: 200px; height: 16px;"></saf-skeleton>
      <saf-skeleton appearance="small" style="width: 150px; height: 14px; margin-top: 4px;"></saf-skeleton>
    </div>
    <saf-skeleton appearance="small" style="width: 60px; height: 14px;"></saf-skeleton>
  </div>
  
  <!-- Repeat similar structure for more items -->
  <div class="list-item">
    <saf-skeleton shape="circle" style="width: 32px; height: 32px;"></saf-skeleton>
    <div class="list-content">
      <saf-skeleton appearance="small" style="width: 180px; height: 16px;"></saf-skeleton>
      <saf-skeleton appearance="small" style="width: 120px; height: 14px; margin-top: 4px;"></saf-skeleton>
    </div>
    <saf-skeleton appearance="small" style="width: 80px; height: 14px;"></saf-skeleton>
  </div>
  
  <div class="list-item">
    <saf-skeleton shape="circle" style="width: 32px; height: 32px;"></saf-skeleton>
    <div class="list-content">
      <saf-skeleton appearance="small" style="width: 220px; height: 16px;"></saf-skeleton>
      <saf-skeleton appearance="small" style="width: 100px; height: 14px; margin-top: 4px;"></saf-skeleton>
    </div>
    <saf-skeleton appearance="small" style="width: 70px; height: 14px;"></saf-skeleton>
  </div>
</div>

<style>
.list-skeleton {
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: white;
}

.list-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  border-bottom: 1px solid #f0f0f0;
}

.list-item:last-child {
  border-bottom: none;
}

.list-content {
  flex: 1;
}
</style>
```

### Progressive Loading Skeleton

```html
<div class="progressive-skeleton" id="progressive-demo">
  <div class="skeleton-phase" data-phase="1">
    <saf-skeleton appearance="large" shimmer style="width: 100%; height: 40px;"></saf-skeleton>
    <saf-skeleton appearance="small" shimmer style="width: 75%; height: 20px; margin-top: 12px;"></saf-skeleton>
  </div>
  
  <div class="skeleton-phase" data-phase="2" style="display: none;">
    <h2>Content Loaded!</h2>
    <p>This demonstrates progressive loading where skeleton is replaced by actual content.</p>
    
    <div class="content-with-skeleton">
      <div class="loaded-content">
        <p>Some content has loaded...</p>
      </div>
      <div class="still-loading">
        <saf-skeleton appearance="small" shimmer style="width: 100%; height: 16px;"></saf-skeleton>
        <saf-skeleton appearance="small" shimmer style="width: 80%; height: 16px; margin-top: 4px;"></saf-skeleton>
      </div>
    </div>
  </div>
  
  <div class="skeleton-phase" data-phase="3" style="display: none;">
    <h2>Fully Loaded!</h2>
    <p>All content has finished loading.</p>
    <p>The skeleton components have been completely replaced with actual content.</p>
    
    <div class="final-content">
      <p>Here's your fully loaded content with all the data you requested.</p>
      <button onclick="restartDemo()">Restart Demo</button>
    </div>
  </div>
</div>

<style>
.progressive-skeleton {
  padding: 2rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
  min-height: 200px;
}

.content-with-skeleton {
  margin-top: 1rem;
  padding: 1rem;
  border: 1px solid #f0f0f0;
  border-radius: 4px;
}

.still-loading {
  margin-top: 1rem;
}

.final-content {
  margin-top: 1rem;
  padding: 1rem;
  background: #f9f9f9;
  border-radius: 4px;
}
</style>

<script>
let currentPhase = 1;

function showPhase(phase) {
  document.querySelectorAll('.skeleton-phase').forEach((el, index) => {
    el.style.display = index + 1 === phase ? 'block' : 'none';
  });
}

function nextPhase() {
  currentPhase++;
  if (currentPhase <= 3) {
    showPhase(currentPhase);
    if (currentPhase < 3) {
      setTimeout(nextPhase, 2000);
    }
  }
}

function restartDemo() {
  currentPhase = 1;
  showPhase(currentPhase);
  setTimeout(nextPhase, 1000);
}

// Start the demo
setTimeout(nextPhase, 2000);
</script>
```

### Custom Pattern Skeleton

```html
<div class="custom-skeleton-examples">
  <!-- Custom fill color -->
  <saf-skeleton 
    fill="linear-gradient(90deg, #f0f0f0 25%, transparent 50%, #f0f0f0 75%)"
    style="width: 100%; height: 60px; margin-bottom: 1rem;">
  </saf-skeleton>
  
  <!-- Multiple skeleton sizes -->
  <div class="skeleton-group">
    <saf-skeleton appearance="large" shimmer style="width: 100%; height: 24px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 80%; height: 16px; margin-top: 8px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 60%; height: 16px; margin-top: 4px;"></saf-skeleton>
    <saf-skeleton appearance="small" style="width: 40%; height: 16px; margin-top: 4px;"></saf-skeleton>
  </div>
</div>

<style>
.custom-skeleton-examples {
  padding: 1rem;
}

.skeleton-group {
  margin-top: 1rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React, { useState, useEffect } from 'react';

interface SkeletonProps {
  shape?: 'rect' | 'circle';
  appearance?: 'small' | 'large' | 'table';
  background?: 'transparent' | 'card';
  shimmer?: boolean;
  width?: string;
  height?: string;
  className?: string;
  style?: React.CSSProperties;
}

const SafSkeletonComponent: React.FC<SkeletonProps> = ({
  shape = 'rect',
  appearance = 'small',
  background = 'card',
  shimmer = false,
  width,
  height,
  className,
  style
}) => {
  const skeletonStyle = {
    width,
    height,
    ...style
  };

  return (
    <saf-skeleton
      shape={shape}
      appearance={appearance}
      background={background}
      shimmer={shimmer}
      className={className}
      style={skeletonStyle}
    />
  );
};

// Usage examples
const SkeletonExample: React.FC = () => {
  const [loading, setLoading] = useState(true);
  const [data, setData] = useState<any[]>([]);

  useEffect(() => {
    // Simulate data loading
    setTimeout(() => {
      setData([
        { id: 1, name: 'John Doe', email: 'john@example.com' },
        { id: 2, name: 'Jane Smith', email: 'jane@example.com' },
        { id: 3, name: 'Bob Johnson', email: 'bob@example.com' }
      ]);
      setLoading(false);
    }, 3000);
  }, []);

  if (loading) {
    return (
      <div className="skeleton-list">
        {[...Array(3)].map((_, index) => (
          <div key={index} className="skeleton-item">
            <SafSkeletonComponent
              shape="circle"
              width="40px"
              height="40px"
              shimmer
            />
            <div className="skeleton-content">
              <SafSkeletonComponent
                appearance="small"
                width="150px"
                height="16px"
              />
              <SafSkeletonComponent
                appearance="small"
                width="200px"
                height="14px"
                style={{ marginTop: '4px' }}
              />
            </div>
          </div>
        ))}
      </div>
    );
  }

  return (
    <div className="data-list">
      {data.map(item => (
        <div key={item.id} className="data-item">
          <div className="avatar">👤</div>
          <div className="content">
            <div className="name">{item.name}</div>
            <div className="email">{item.email}</div>
          </div>
        </div>
      ))}
    </div>
  );
};

// Skeleton Loader Hook
const useSkeletonLoader = (delay: number = 2000) => {
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const timer = setTimeout(() => {
      setLoading(false);
    }, delay);

    return () => clearTimeout(timer);
  }, [delay]);

  return loading;
};
```

### Angular Example

```typescript
// skeleton.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-saf-skeleton',
  template: `
    <saf-skeleton
      [attr.shape]="shape"
      [attr.appearance]="appearance"
      [attr.background]="background"
      [attr.shimmer]="shimmer"
      [style.width]="width"
      [style.height]="height"
      [class]="className"
    >
      <ng-content></ng-content>
    </saf-skeleton>
  `
})
export class SafSkeletonComponent {
  @Input() shape: 'rect' | 'circle' = 'rect';
  @Input() appearance: 'small' | 'large' | 'table' = 'small';
  @Input() background: 'transparent' | 'card' = 'card';
  @Input() shimmer: boolean = false;
  @Input() width?: string;
  @Input() height?: string;
  @Input() className?: string;
}

// Usage in component
/*
@Component({
  template: `
    <div *ngIf="loading; else content">
      <div class="skeleton-list">
        <div class="skeleton-item" *ngFor="let item of skeletonItems">
          <app-saf-skeleton
            shape="circle"
            width="40px"
            height="40px"
            [shimmer]="true">
          </app-saf-skeleton>
          <div class="skeleton-content">
            <app-saf-skeleton
              appearance="small"
              width="150px"
              height="16px">
            </app-saf-skeleton>
            <app-saf-skeleton
              appearance="small"
              width="200px"
              height="14px"
              style="margin-top: 4px">
            </app-saf-skeleton>
          </div>
        </div>
      </div>
    </div>
    
    <ng-template #content>
      <div class="data-list">
        <div class="data-item" *ngFor="let item of data">
          <div class="avatar">👤</div>
          <div class="content">
            <div class="name">{{ item.name }}</div>
            <div class="email">{{ item.email }}</div>
          </div>
        </div>
      </div>
    </ng-template>
  `
})
*/
```

### Vue Example

```vue
<template>
  <saf-skeleton
    :shape="shape"
    :appearance="appearance"
    :background="background"
    :shimmer="shimmer"
    :style="skeletonStyle"
    :class="className"
  >
    <slot></slot>
  </saf-skeleton>
</template>

<script>
export default {
  name: 'SafSkeletonComponent',
  props: {
    shape: {
      type: String,
      default: 'rect',
      validator: value => ['rect', 'circle'].includes(value)
    },
    appearance: {
      type: String,
      default: 'small',
      validator: value => ['small', 'large', 'table'].includes(value)
    },
    background: {
      type: String,
      default: 'card',
      validator: value => ['transparent', 'card'].includes(value)
    },
    shimmer: {
      type: Boolean,
      default: false
    },
    width: String,
    height: String,
    className: String
  },
  computed: {
    skeletonStyle() {
      return {
        width: this.width,
        height: this.height
      };
    }
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div>
    <div v-if="loading" class="skeleton-list">
      <div v-for="n in 3" :key="n" class="skeleton-item">
        <SafSkeletonComponent
          shape="circle"
          width="40px"
          height="40px"
          :shimmer="true"
        />
        <div class="skeleton-content">
          <SafSkeletonComponent
            appearance="small"
            width="150px"
            height="16px"
          />
          <SafSkeletonComponent
            appearance="small"
            width="200px"
            height="14px"
            style="margin-top: 4px"
          />
        </div>
      </div>
    </div>
    
    <div v-else class="data-list">
      <div v-for="item in data" :key="item.id" class="data-item">
        <div class="avatar">👤</div>
        <div class="content">
          <div class="name">{{ item.name }}</div>
          <div class="email">{{ item.email }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
-->
```

## Accessibility Features

### Screen Reader Support

- Skeletons are automatically hidden from screen readers using `aria-hidden="true"`
- Loading states should be announced via separate live regions
- Proper semantic structure maintained when content loads

### Visual Accessibility

- Sufficient contrast ratios for visibility
- Respects user preferences for reduced motion
- Works with high contrast modes
- Shimmer animation can be disabled for motion sensitivity

## Best Practices

### Performance
- Use appropriate skeleton complexity for content type
- Avoid excessive shimmer animations on slow devices
- Clean up skeleton elements when content loads
- Consider skeleton caching for repeated patterns

### User Experience
- Match skeleton dimensions closely to actual content
- Use progressive disclosure for complex loading states
- Provide loading indicators for long operations
- Test skeleton timing with real network conditions

### Design Guidelines
- Keep skeleton shapes simple and recognizable
- Use consistent spacing and proportions
- Match the visual hierarchy of actual content
- Consider dark mode and theme variations

### Implementation
- Remove skeletons completely when content loads
- Handle error states gracefully
- Provide fallbacks for unsupported features
- Test across different screen sizes and orientations

## Related Components

- **SafProgress**: For determinate loading progress
- **SafSpinner**: For indeterminate loading states
- **SafAlert**: For loading state messages

---

*This documentation covers SafSkeleton v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
