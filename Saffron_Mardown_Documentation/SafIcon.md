# SafIcon Component

The **SafIcon** component provides a consistent way to display icons throughout your application. It supports Font Awesome icons with multiple appearance styles, customizable sizes, colors, and proper accessibility features.

## Basic Usage

```html
<!-- Basic icon -->
<saf-icon icon-name="home"></saf-icon>

<!-- Icon with different appearance -->
<saf-icon icon-name="star" appearance="solid"></saf-icon>

<!-- Icon with custom size and color -->
<saf-icon icon-name="heart" size="24" color="red"></saf-icon>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `icon-name` | `string` | - | Font Awesome icon name (without fa- prefix) |
| `appearance` | `'light' \| 'solid' \| 'brands'` | `'light'` | Font Awesome icon style |
| `size` | `number` | `16` | Icon size in specified units |
| `size-unit` | `'px' \| 'em' \| 'rem'` | `'px'` | Unit for the size value |
| `color` | `string` | `'currentColor'` | Icon color (CSS color value) |
| `color-type` | `'fill' \| 'outline'` | - | Predefined color type |
| `presentation` | `boolean` | `true` | Whether icon is decorative (affects ARIA attributes) |
| `aria-label` | `string` | - | Accessible label for the icon |
| `aria-labelledby` | `string` | - | References to elements that label the icon |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `iconName` | `string` | - | Current icon name |
| `appearance` | `IconAppearance` | `'light'` | Current appearance style |
| `size` | `number` | `16` | Current size value |
| `color` | `string` | - | Current color value |
| `presentation` | `boolean` | `true` | Current presentation mode |

### Methods

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `checkForLabel()` | - | `void` | Validates accessibility labeling (internal) |

### CSS Custom Properties

| Property | Default | Description |
|----------|---------|-------------|
| `--saf-icon-size` | `16px` | Icon size (set automatically based on size attribute) |

## Appearance Options

| Appearance | Description | Font Awesome Classes |
|------------|-------------|---------------------|
| `'light'` | Light weight icons | `fa-light fa-sharp` |
| `'solid'` | Solid filled icons | `fa-solid fa-sharp` |
| `'brands'` | Brand/logo icons | `fa-brands` |

## Size Units

| Unit | Description | Best Used For |
|------|-------------|---------------|
| `'px'` | Fixed pixel size | Precise icon sizing |
| `'em'` | Relative to element font size | Icons that scale with text |
| `'rem'` | Relative to root font size | Consistent sizing across app |

## Comprehensive Examples

### Basic Icon Variations

```html
<div class="icon-examples">
  <!-- Different appearances -->
  <div class="icon-group">
    <h3>Appearances</h3>
    <saf-icon icon-name="star" appearance="light"></saf-icon>
    <saf-icon icon-name="star" appearance="solid"></saf-icon>
    <saf-icon icon-name="github" appearance="brands"></saf-icon>
  </div>

  <!-- Different sizes -->
  <div class="icon-group">
    <h3>Sizes</h3>
    <saf-icon icon-name="home" size="12"></saf-icon>
    <saf-icon icon-name="home" size="16"></saf-icon>
    <saf-icon icon-name="home" size="24"></saf-icon>
    <saf-icon icon-name="home" size="32"></saf-icon>
    <saf-icon icon-name="home" size="48"></saf-icon>
  </div>

  <!-- Different colors -->
  <div class="icon-group">
    <h3>Colors</h3>
    <saf-icon icon-name="heart" appearance="solid" color="red"></saf-icon>
    <saf-icon icon-name="leaf" appearance="solid" color="green"></saf-icon>
    <saf-icon icon-name="water" appearance="solid" color="blue"></saf-icon>
    <saf-icon icon-name="sun" appearance="solid" color="orange"></saf-icon>
    <saf-icon icon-name="moon" appearance="solid" color="purple"></saf-icon>
  </div>
</div>

<style>
.icon-examples {
  padding: 2rem;
}

.icon-group {
  margin-bottom: 2rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}

.icon-group h3 {
  margin-top: 0;
  margin-bottom: 1rem;
}

.icon-group saf-icon {
  margin-right: 1rem;
  vertical-align: middle;
}
</style>
```

### Icons in Context

```html
<div class="contextual-icons">
  <!-- In buttons -->
  <div class="context-group">
    <h3>In Buttons</h3>
    <button class="icon-button">
      <saf-icon icon-name="plus" size="16"></saf-icon>
      Add Item
    </button>
    <button class="icon-button">
      <saf-icon icon-name="edit" size="16"></saf-icon>
      Edit
    </button>
    <button class="icon-button secondary">
      <saf-icon icon-name="trash" size="16"></saf-icon>
      Delete
    </button>
  </div>

  <!-- In navigation -->
  <div class="context-group">
    <h3>In Navigation</h3>
    <nav class="icon-nav">
      <a href="#" class="nav-item">
        <saf-icon icon-name="home" size="20"></saf-icon>
        <span>Home</span>
      </a>
      <a href="#" class="nav-item">
        <saf-icon icon-name="user" size="20"></saf-icon>
        <span>Profile</span>
      </a>
      <a href="#" class="nav-item">
        <saf-icon icon-name="cog" size="20"></saf-icon>
        <span>Settings</span>
      </a>
      <a href="#" class="nav-item">
        <saf-icon icon-name="envelope" size="20"></saf-icon>
        <span>Messages</span>
      </a>
    </nav>
  </div>

  <!-- In lists -->
  <div class="context-group">
    <h3>In Lists</h3>
    <ul class="icon-list">
      <li>
        <saf-icon icon-name="check" appearance="solid" color="green" size="16"></saf-icon>
        Task completed successfully
      </li>
      <li>
        <saf-icon icon-name="exclamation-triangle" appearance="solid" color="orange" size="16"></saf-icon>
        Warning: Check configuration
      </li>
      <li>
        <saf-icon icon-name="times-circle" appearance="solid" color="red" size="16"></saf-icon>
        Error: Process failed
      </li>
      <li>
        <saf-icon icon-name="info-circle" appearance="solid" color="blue" size="16"></saf-icon>
        Information: Update available
      </li>
    </ul>
  </div>
</div>

<style>
.contextual-icons {
  padding: 2rem;
}

.context-group {
  margin-bottom: 2rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}

.context-group h3 {
  margin-top: 0;
  margin-bottom: 1rem;
}

.icon-button {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  margin-right: 0.5rem;
  border: 1px solid #007acc;
  background: #007acc;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

.icon-button.secondary {
  background: transparent;
  color: #007acc;
}

.icon-button:hover {
  background: #005a9e;
}

.icon-button.secondary:hover {
  background: #f0f8ff;
}

.icon-nav {
  display: flex;
  gap: 1rem;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem;
  text-decoration: none;
  color: inherit;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.nav-item:hover {
  background-color: #f5f5f5;
}

.nav-item span {
  font-size: 12px;
}

.icon-list {
  list-style: none;
  padding: 0;
}

.icon-list li {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #f0f0f0;
}

.icon-list li:last-child {
  border-bottom: none;
}
</style>
```

### Status and Feedback Icons

```html
<div class="status-icons">
  <h3>Status Indicators</h3>
  <div class="status-grid">
    <div class="status-item success">
      <saf-icon icon-name="check-circle" appearance="solid" color="var(--success-color)" size="24"></saf-icon>
      <div class="status-content">
        <h4>Success</h4>
        <p>Operation completed successfully</p>
      </div>
    </div>

    <div class="status-item warning">
      <saf-icon icon-name="exclamation-triangle" appearance="solid" color="var(--warning-color)" size="24"></saf-icon>
      <div class="status-content">
        <h4>Warning</h4>
        <p>Please review your settings</p>
      </div>
    </div>

    <div class="status-item error">
      <saf-icon icon-name="times-circle" appearance="solid" color="var(--error-color)" size="24"></saf-icon>
      <div class="status-content">
        <h4>Error</h4>
        <p>Something went wrong</p>
      </div>
    </div>

    <div class="status-item info">
      <saf-icon icon-name="info-circle" appearance="solid" color="var(--info-color)" size="24"></saf-icon>
      <div class="status-content">
        <h4>Information</h4>
        <p>New features available</p>
      </div>
    </div>
  </div>
</div>

<style>
:root {
  --success-color: #28a745;
  --warning-color: #ffc107;
  --error-color: #dc3545;
  --info-color: #17a2b8;
}

.status-icons {
  padding: 2rem;
}

.status-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.status-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: white;
}

.status-item.success {
  border-left: 4px solid var(--success-color);
}

.status-item.warning {
  border-left: 4px solid var(--warning-color);
}

.status-item.error {
  border-left: 4px solid var(--error-color);
}

.status-item.info {
  border-left: 4px solid var(--info-color);
}

.status-content h4 {
  margin: 0 0 0.5rem 0;
  font-size: 16px;
}

.status-content p {
  margin: 0;
  font-size: 14px;
  color: #666;
}
</style>
```

### Interactive Icons

```html
<div class="interactive-icons">
  <h3>Interactive Icons</h3>
  
  <!-- Toggle icons -->
  <div class="toggle-examples">
    <h4>Toggle Icons</h4>
    <button class="toggle-btn" onclick="toggleFavorite(this)">
      <saf-icon icon-name="heart" appearance="light" size="20" class="toggle-icon"></saf-icon>
      <span>Add to Favorites</span>
    </button>
    
    <button class="toggle-btn" onclick="toggleBookmark(this)">
      <saf-icon icon-name="bookmark" appearance="light" size="20" class="toggle-icon"></saf-icon>
      <span>Bookmark</span>
    </button>
    
    <button class="toggle-btn" onclick="toggleVisibility(this)">
      <saf-icon icon-name="eye" appearance="light" size="20" class="toggle-icon"></saf-icon>
      <span>Show</span>
    </button>
  </div>

  <!-- Loading states -->
  <div class="loading-examples">
    <h4>Loading States</h4>
    <button class="loading-btn" onclick="simulateLoading(this)">
      <saf-icon icon-name="spinner" appearance="solid" size="16" class="loading-icon"></saf-icon>
      <span>Process Data</span>
    </button>
    
    <button class="refresh-btn" onclick="simulateRefresh(this)">
      <saf-icon icon-name="refresh" appearance="solid" size="16" class="refresh-icon"></saf-icon>
      <span>Refresh</span>
    </button>
  </div>
</div>

<style>
.interactive-icons {
  padding: 2rem;
}

.toggle-examples,
.loading-examples {
  margin-bottom: 2rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}

.toggle-examples h4,
.loading-examples h4 {
  margin-top: 0;
  margin-bottom: 1rem;
}

.toggle-btn,
.loading-btn,
.refresh-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
  border: 1px solid #ccc;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s;
}

.toggle-btn:hover,
.loading-btn:hover,
.refresh-btn:hover {
  background: #f5f5f5;
}

.toggle-btn.active {
  background: #007acc;
  color: white;
  border-color: #007acc;
}

.loading-icon {
  animation: spin 1s linear infinite;
}

.refresh-icon.spinning {
  animation: spin 0.5s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.toggle-btn.active .toggle-icon {
  color: white;
}
</style>

<script>
function toggleFavorite(button) {
  const icon = button.querySelector('.toggle-icon');
  const span = button.querySelector('span');
  const isActive = button.classList.contains('active');
  
  if (isActive) {
    button.classList.remove('active');
    icon.setAttribute('appearance', 'light');
    icon.setAttribute('color', '');
    span.textContent = 'Add to Favorites';
  } else {
    button.classList.add('active');
    icon.setAttribute('appearance', 'solid');
    icon.setAttribute('color', 'white');
    span.textContent = 'Remove from Favorites';
  }
}

function toggleBookmark(button) {
  const icon = button.querySelector('.toggle-icon');
  const span = button.querySelector('span');
  const isActive = button.classList.contains('active');
  
  if (isActive) {
    button.classList.remove('active');
    icon.setAttribute('appearance', 'light');
    icon.setAttribute('color', '');
    span.textContent = 'Bookmark';
  } else {
    button.classList.add('active');
    icon.setAttribute('appearance', 'solid');
    icon.setAttribute('color', 'white');
    span.textContent = 'Bookmarked';
  }
}

function toggleVisibility(button) {
  const icon = button.querySelector('.toggle-icon');
  const span = button.querySelector('span');
  const isVisible = icon.getAttribute('icon-name') === 'eye';
  
  if (isVisible) {
    icon.setAttribute('icon-name', 'eye-slash');
    span.textContent = 'Hide';
  } else {
    icon.setAttribute('icon-name', 'eye');
    span.textContent = 'Show';
  }
}

function simulateLoading(button) {
  const icon = button.querySelector('.loading-icon');
  const span = button.querySelector('span');
  
  button.disabled = true;
  icon.classList.add('loading-icon');
  span.textContent = 'Processing...';
  
  setTimeout(() => {
    button.disabled = false;
    icon.classList.remove('loading-icon');
    span.textContent = 'Process Data';
  }, 3000);
}

function simulateRefresh(button) {
  const icon = button.querySelector('.refresh-icon');
  
  icon.classList.add('spinning');
  
  setTimeout(() => {
    icon.classList.remove('spinning');
  }, 1000);
}
</script>
```

### Accessible Icons

```html
<div class="accessible-icons">
  <h3>Accessibility Examples</h3>
  
  <!-- Decorative icons (presentation=true) -->
  <div class="example-group">
    <h4>Decorative Icons</h4>
    <p>These icons are purely decorative and hidden from screen readers:</p>
    <div class="decorative-examples">
      <span>
        <saf-icon icon-name="star" appearance="solid" color="gold" presentation="true"></saf-icon>
        Premium Feature
      </span>
      <span>
        <saf-icon icon-name="fire" appearance="solid" color="red" presentation="true"></saf-icon>
        Hot Deal
      </span>
    </div>
  </div>

  <!-- Semantic icons (presentation=false) -->
  <div class="example-group">
    <h4>Semantic Icons</h4>
    <p>These icons convey meaning and should be labeled for screen readers:</p>
    <div class="semantic-examples">
      <button class="semantic-btn">
        <saf-icon 
          icon-name="download" 
          appearance="solid" 
          presentation="false"
          aria-label="Download file"
          size="16">
        </saf-icon>
      </button>
      
      <a href="#" class="semantic-link">
        <saf-icon 
          icon-name="external-link" 
          appearance="solid" 
          presentation="false"
          aria-label="Opens in new window"
          size="14">
        </saf-icon>
        External Link
      </a>
      
      <div class="status-message">
        <saf-icon 
          icon-name="exclamation-triangle" 
          appearance="solid" 
          color="orange"
          presentation="false"
          aria-label="Warning"
          size="20">
        </saf-icon>
        <span id="warning-text">Your session will expire soon</span>
      </div>
    </div>
  </div>

  <!-- Icons with labelledby -->
  <div class="example-group">
    <h4>Icons with Labelledby</h4>
    <div class="labelledby-examples">
      <div class="metric-card">
        <saf-icon 
          icon-name="users" 
          appearance="solid" 
          color="blue"
          presentation="false"
          aria-labelledby="users-label users-count"
          size="24">
        </saf-icon>
        <div class="metric-content">
          <h5 id="users-label">Active Users</h5>
          <span id="users-count">1,234</span>
        </div>
      </div>
      
      <div class="metric-card">
        <saf-icon 
          icon-name="chart-line" 
          appearance="solid" 
          color="green"
          presentation="false"
          aria-labelledby="revenue-label revenue-amount"
          size="24">
        </saf-icon>
        <div class="metric-content">
          <h5 id="revenue-label">Monthly Revenue</h5>
          <span id="revenue-amount">$45,678</span>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
.accessible-icons {
  padding: 2rem;
}

.example-group {
  margin-bottom: 2rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}

.example-group h4 {
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.example-group p {
  margin-bottom: 1rem;
  color: #666;
  font-size: 14px;
}

.decorative-examples span {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  margin-right: 1rem;
  padding: 0.5rem;
  background: #f8f9fa;
  border-radius: 4px;
}

.semantic-examples {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.semantic-btn {
  padding: 0.75rem;
  border: 1px solid #007acc;
  background: #007acc;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

.semantic-btn:hover {
  background: #005a9e;
}

.semantic-link {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  color: #007acc;
  text-decoration: none;
}

.semantic-link:hover {
  text-decoration: underline;
}

.status-message {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem;
  background: #fff3cd;
  border: 1px solid #ffeaa7;
  border-radius: 4px;
}

.labelledby-examples {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.metric-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: white;
}

.metric-content h5 {
  margin: 0 0 0.25rem 0;
  font-size: 14px;
  color: #666;
}

.metric-content span {
  font-size: 18px;
  font-weight: bold;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React from 'react';

interface IconProps {
  iconName: string;
  appearance?: 'light' | 'solid' | 'brands';
  size?: number;
  sizeUnit?: 'px' | 'em' | 'rem';
  color?: string;
  colorType?: 'fill' | 'outline';
  presentation?: boolean;
  ariaLabel?: string;
  ariaLabelledBy?: string;
  className?: string;
  onClick?: () => void;
}

const SafIconComponent: React.FC<IconProps> = ({
  iconName,
  appearance = 'light',
  size = 16,
  sizeUnit = 'px',
  color,
  colorType,
  presentation = true,
  ariaLabel,
  ariaLabelledBy,
  className,
  onClick
}) => {
  return (
    <saf-icon
      icon-name={iconName}
      appearance={appearance}
      size={size}
      size-unit={sizeUnit}
      color={color}
      color-type={colorType}
      presentation={presentation}
      aria-label={ariaLabel}
      aria-labelledby={ariaLabelledBy}
      className={className}
      onClick={onClick}
    />
  );
};

// Usage examples
const IconExample: React.FC = () => {
  const [isFavorite, setIsFavorite] = React.useState(false);

  return (
    <div className="icon-examples">
      {/* Basic icons */}
      <SafIconComponent iconName="home" size={24} />
      <SafIconComponent iconName="star" appearance="solid" color="gold" />
      
      {/* Interactive icon */}
      <button onClick={() => setIsFavorite(!isFavorite)}>
        <SafIconComponent
          iconName="heart"
          appearance={isFavorite ? 'solid' : 'light'}
          color={isFavorite ? 'red' : undefined}
          presentation={false}
          ariaLabel={isFavorite ? 'Remove from favorites' : 'Add to favorites'}
        />
        {isFavorite ? 'Favorited' : 'Favorite'}
      </button>
      
      {/* Status icons */}
      <div className="status-list">
        <SafIconComponent
          iconName="check-circle"
          appearance="solid"
          color="green"
          presentation={false}
          ariaLabel="Success"
        />
        <SafIconComponent
          iconName="exclamation-triangle"
          appearance="solid"
          color="orange"
          presentation={false}
          ariaLabel="Warning"
        />
      </div>
    </div>
  );
};

// Icon Button Component
interface IconButtonProps {
  icon: string;
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  size?: 'small' | 'medium' | 'large';
  onClick?: () => void;
  disabled?: boolean;
}

const IconButton: React.FC<IconButtonProps> = ({
  icon,
  children,
  variant = 'primary',
  size = 'medium',
  onClick,
  disabled = false
}) => {
  const iconSize = size === 'small' ? 14 : size === 'large' ? 20 : 16;
  
  return (
    <button
      className={`icon-button ${variant} ${size}`}
      onClick={onClick}
      disabled={disabled}
    >
      <SafIconComponent iconName={icon} size={iconSize} />
      {children}
    </button>
  );
};
```

### Angular Example

```typescript
// icon.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-saf-icon',
  template: `
    <saf-icon
      [attr.icon-name]="iconName"
      [attr.appearance]="appearance"
      [attr.size]="size"
      [attr.size-unit]="sizeUnit"
      [attr.color]="color"
      [attr.color-type]="colorType"
      [attr.presentation]="presentation"
      [attr.aria-label]="ariaLabel"
      [attr.aria-labelledby]="ariaLabelledBy"
      [class]="className"
      (click)="handleClick()"
    ></saf-icon>
  `
})
export class SafIconComponent {
  @Input() iconName: string = '';
  @Input() appearance: 'light' | 'solid' | 'brands' = 'light';
  @Input() size: number = 16;
  @Input() sizeUnit: 'px' | 'em' | 'rem' = 'px';
  @Input() color?: string;
  @Input() colorType?: 'fill' | 'outline';
  @Input() presentation: boolean = true;
  @Input() ariaLabel?: string;
  @Input() ariaLabelledBy?: string;
  @Input() className?: string;
  @Input() clickable: boolean = false;

  handleClick() {
    if (this.clickable) {
      // Handle click event
    }
  }
}

// Usage in component template
/*
<app-saf-icon
  iconName="home"
  [size]="24"
  appearance="solid">
</app-saf-icon>

<app-saf-icon
  iconName="heart"
  [appearance]="isFavorite ? 'solid' : 'light'"
  [color]="isFavorite ? 'red' : undefined"
  [presentation]="false"
  [ariaLabel]="isFavorite ? 'Remove from favorites' : 'Add to favorites'">
</app-saf-icon>
*/
```

### Vue Example

```vue
<template>
  <saf-icon
    :icon-name="iconName"
    :appearance="appearance"
    :size="size"
    :size-unit="sizeUnit"
    :color="color"
    :color-type="colorType"
    :presentation="presentation"
    :aria-label="ariaLabel"
    :aria-labelledby="ariaLabelledBy"
    :class="className"
    @click="handleClick"
  ></saf-icon>
</template>

<script>
export default {
  name: 'SafIconComponent',
  props: {
    iconName: {
      type: String,
      required: true
    },
    appearance: {
      type: String,
      default: 'light',
      validator: value => ['light', 'solid', 'brands'].includes(value)
    },
    size: {
      type: Number,
      default: 16
    },
    sizeUnit: {
      type: String,
      default: 'px',
      validator: value => ['px', 'em', 'rem'].includes(value)
    },
    color: String,
    colorType: {
      type: String,
      validator: value => ['fill', 'outline'].includes(value)
    },
    presentation: {
      type: Boolean,
      default: true
    },
    ariaLabel: String,
    ariaLabelledBy: String,
    className: String,
    clickable: {
      type: Boolean,
      default: false
    }
  },
  emits: ['click'],
  methods: {
    handleClick() {
      if (this.clickable) {
        this.$emit('click');
      }
    }
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div class="icon-examples">
    <SafIconComponent
      icon-name="home"
      :size="24"
      appearance="solid"
    />
    
    <SafIconComponent
      icon-name="heart"
      :appearance="isFavorite ? 'solid' : 'light'"
      :color="isFavorite ? 'red' : undefined"
      :presentation="false"
      :aria-label="isFavorite ? 'Remove from favorites' : 'Add to favorites'"
      :clickable="true"
      @click="toggleFavorite"
    />
  </div>
</template>
-->
```

## Accessibility Features

### ARIA Support

- **Presentation Mode**: When `presentation="true"` (default), icons are hidden from screen readers with `aria-hidden="true"` and `role="presentation"`
- **Semantic Mode**: When `presentation="false"`, icons have `role="img"` and require proper labeling
- **Labeling**: Support for both `aria-label` and `aria-labelledby` attributes
- **Validation**: Warns developers when semantic icons lack proper labels

### Best Practices

#### When to Use Presentation Mode
- Decorative icons that don't convey essential information
- Icons paired with descriptive text
- Visual embellishments and design elements

#### When to Use Semantic Mode
- Icons that convey important information without text
- Interactive icons (buttons with only icons)
- Status indicators and alerts
- Icons in data visualizations

### Keyboard Navigation

- Icons themselves are not focusable by default
- Interactive icons should be wrapped in focusable elements (buttons, links)
- Proper focus indicators should be provided for interactive containers

## Best Practices

### Performance
- Use consistent icon libraries (Font Awesome)
- Cache icon fonts and assets
- Consider icon bundling for frequently used icons
- Optimize icon sizes for different contexts

### Design Guidelines
- Maintain consistent icon sizing within contexts
- Use appropriate icon weights (light, solid) for hierarchy
- Ensure sufficient color contrast for visibility
- Test icons across different screen sizes

### Accessibility
- Always provide labels for semantic icons
- Use consistent icon meanings throughout the application
- Test with screen readers and keyboard navigation
- Consider user preferences for reduced motion

### Development
- Use meaningful icon names that match their purpose
- Document icon usage patterns in your design system
- Provide fallbacks for missing or failed icon loads
- Consider internationalization and cultural differences

## Related Components

- **SafButton**: Often contains icons with text
- **SafBadge**: May include status icons
- **SafAlert**: Uses icons for different alert types
- **SafMenuItem**: Can include start/end icons

---

*This documentation covers SafIcon v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
