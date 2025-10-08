# SafTooltip Component

The **SafTooltip** component provides contextual information in a small popup overlay. It supports both hover-triggered and click-triggered modes, with intelligent positioning and accessibility features.

## Basic Usage

```html
<!-- Basic tooltip -->
<button id="save-btn">Save</button>
<saf-tooltip anchor="save-btn">Save your document</saf-tooltip>

<!-- Tooltip with placement -->
<button id="delete-btn">Delete</button>
<saf-tooltip anchor="delete-btn" placement="top">
  This action cannot be undone
</saf-tooltip>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `anchor` | `string` | - | ID of the element the tooltip is anchored to |
| `placement` | `TooltipPosition` | `'bottom'` | Position of the tooltip relative to anchor |
| `show` | `boolean` | - | Controls tooltip visibility (when set, overrides hover behavior) |
| `trigger-on-click` | `boolean` | `false` | Whether to trigger tooltip on click instead of hover |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `boolean` | `false` | Current visibility state (read-only) |
| `anchorElement` | `HTMLElement \| null` | `null` | Reference to the anchor element |
| `placement` | `TooltipPosition` | `'bottom'` | Current placement position |

### Methods

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `setPositioning()` | - | `void` | Manually recalculate and apply positioning |

### Events

| Event | Detail | Description |
|-------|--------|-------------|
| `dismiss` | - | Fired when tooltip is dismissed via Escape key |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Tooltip content |

### CSS Parts

| Part | Description |
|------|-------------|
| `tooltip` | Main tooltip container |

## Placement Options

The `placement` attribute accepts the following values:

| Value | Description |
|-------|-------------|
| `'top'` | Above the anchor element |
| `'top-start'` | Above and to the left of the anchor |
| `'top-end'` | Above and to the right of the anchor |
| `'bottom'` | Below the anchor element |
| `'bottom-start'` | Below and to the left of the anchor |
| `'bottom-end'` | Below and to the right of the anchor |
| `'left'` | To the left of the anchor element |
| `'right'` | To the right of the anchor element |

## Comprehensive Examples

### Basic Tooltips with Different Placements

```html
<div class="tooltip-demo">
  <!-- Top placement -->
  <button id="btn-top">Top</button>
  <saf-tooltip anchor="btn-top" placement="top">
    Tooltip positioned on top
  </saf-tooltip>

  <!-- Bottom placement -->
  <button id="btn-bottom">Bottom</button>
  <saf-tooltip anchor="btn-bottom" placement="bottom">
    Tooltip positioned on bottom
  </saf-tooltip>

  <!-- Left placement -->
  <button id="btn-left">Left</button>
  <saf-tooltip anchor="btn-left" placement="left">
    Tooltip positioned on left
  </saf-tooltip>

  <!-- Right placement -->
  <button id="btn-right">Right</button>
  <saf-tooltip anchor="btn-right" placement="right">
    Tooltip positioned on right
  </saf-tooltip>
</div>

<style>
.tooltip-demo {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  padding: 2rem;
}

button {
  padding: 0.5rem 1rem;
}
</style>
```

### Click-Triggered Tooltips

```html
<div class="click-tooltip-demo">
  <button id="info-btn">Click for Info</button>
  <saf-tooltip anchor="info-btn" trigger-on-click placement="top">
    <strong>Important Information</strong><br>
    This is a click-triggered tooltip with rich content.
    Click outside or press Escape to dismiss.
  </saf-tooltip>

  <button id="help-btn">Need Help?</button>
  <saf-tooltip anchor="help-btn" trigger-on-click placement="bottom">
    <div style="max-width: 250px;">
      <h4 style="margin-top: 0;">Getting Started</h4>
      <p>Click the button to perform the action. You can also use keyboard shortcuts:</p>
      <ul>
        <li><kbd>Ctrl+S</kbd> - Save</li>
        <li><kbd>Ctrl+Z</kbd> - Undo</li>
      </ul>
    </div>
  </saf-tooltip>
</div>

<script>
// Handle dismiss events
document.querySelectorAll('saf-tooltip[trigger-on-click]').forEach(tooltip => {
  tooltip.addEventListener('dismiss', () => {
    console.log('Tooltip dismissed');
  });
});
</script>
```

### Controlled Tooltip Visibility

```html
<div class="controlled-demo">
  <button id="toggle-btn">Toggle Tooltip</button>
  <saf-tooltip id="controlled-tooltip" anchor="toggle-btn" show="false">
    This tooltip is controlled programmatically
  </saf-tooltip>
</div>

<script>
const toggleBtn = document.getElementById('toggle-btn');
const tooltip = document.getElementById('controlled-tooltip');
let isVisible = false;

toggleBtn.addEventListener('click', () => {
  isVisible = !isVisible;
  tooltip.setAttribute('show', isVisible.toString());
  toggleBtn.textContent = isVisible ? 'Hide Tooltip' : 'Show Tooltip';
});
</script>
```

### Tooltips with Rich Content

```html
<div class="rich-content-demo">
  <button id="status-btn">System Status</button>
  <saf-tooltip anchor="status-btn" placement="top" trigger-on-click>
    <div class="status-tooltip">
      <div class="status-header">
        <saf-icon name="check-circle" style="color: green;"></saf-icon>
        <strong>All Systems Operational</strong>
      </div>
      <div class="status-details">
        <div class="service">
          <span class="service-name">API</span>
          <span class="service-status operational">Operational</span>
        </div>
        <div class="service">
          <span class="service-name">Database</span>
          <span class="service-status operational">Operational</span>
        </div>
        <div class="service">
          <span class="service-name">CDN</span>
          <span class="service-status operational">Operational</span>
        </div>
      </div>
      <div class="last-updated">
        Last updated: 2 minutes ago
      </div>
    </div>
  </saf-tooltip>
</div>

<style>
.status-tooltip {
  max-width: 300px;
  font-size: 14px;
}

.status-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.service {
  display: flex;
  justify-content: space-between;
  padding: 0.25rem 0;
}

.service-status.operational {
  color: green;
  font-weight: 500;
}

.last-updated {
  margin-top: 0.5rem;
  color: #666;
  font-size: 12px;
}
</style>
```

### Form Field Tooltips

```html
<form class="form-with-tooltips">
  <div class="field-group">
    <label for="username">Username</label>
    <input type="text" id="username" name="username" required>
    <button type="button" id="username-help" class="help-btn" aria-label="Username help">?</button>
    <saf-tooltip anchor="username-help" placement="right">
      Username must be 3-20 characters long and contain only letters, numbers, and underscores.
    </saf-tooltip>
  </div>

  <div class="field-group">
    <label for="password">Password</label>
    <input type="password" id="password" name="password" required>
    <button type="button" id="password-help" class="help-btn" aria-label="Password requirements">?</button>
    <saf-tooltip anchor="password-help" placement="right">
      <div class="password-requirements">
        <strong>Password Requirements:</strong>
        <ul>
          <li>At least 8 characters long</li>
          <li>Contains uppercase and lowercase letters</li>
          <li>Contains at least one number</li>
          <li>Contains at least one special character</li>
        </ul>
      </div>
    </saf-tooltip>
  </div>
</form>

<style>
.field-group {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.help-btn {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 1px solid #ccc;
  background: #f5f5f5;
  cursor: pointer;
  font-size: 12px;
}

.password-requirements {
  max-width: 250px;
}

.password-requirements ul {
  margin: 0.5rem 0 0 0;
  padding-left: 1rem;
}
</style>
```

### Dynamic Tooltip Content

```html
<div class="dynamic-demo">
  <div class="progress-container">
    <div class="progress-bar" id="progress">
      <div class="progress-fill"></div>
    </div>
  </div>
  <saf-tooltip id="progress-tooltip" anchor="progress" placement="top">
    <span id="progress-text">0% complete</span>
  </saf-tooltip>
  
  <button onclick="startProgress()">Start Process</button>
</div>

<style>
.progress-container {
  margin: 2rem 0;
}

.progress-bar {
  width: 300px;
  height: 20px;
  background: #f0f0f0;
  border-radius: 10px;
  overflow: hidden;
  cursor: pointer;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #4CAF50, #45a049);
  width: 0%;
  transition: width 0.3s ease;
}
</style>

<script>
function startProgress() {
  const progressFill = document.querySelector('.progress-fill');
  const progressText = document.getElementById('progress-text');
  let progress = 0;
  
  const interval = setInterval(() => {
    progress += 2;
    progressFill.style.width = progress + '%';
    progressText.textContent = progress + '% complete';
    
    if (progress >= 100) {
      clearInterval(interval);
      progressText.textContent = 'Process completed!';
    }
  }, 100);
}
</script>
```

## Framework Integration

### React Example

```tsx
import React, { useState, useRef, useEffect } from 'react';

interface TooltipProps {
  anchor: string;
  children: React.ReactNode;
  placement?: 'top' | 'bottom' | 'left' | 'right' | 'top-start' | 'top-end' | 'bottom-start' | 'bottom-end';
  triggerOnClick?: boolean;
  show?: boolean;
  onDismiss?: () => void;
}

const SafTooltipComponent: React.FC<TooltipProps> = ({
  anchor,
  children,
  placement = 'bottom',
  triggerOnClick = false,
  show,
  onDismiss
}) => {
  const tooltipRef = useRef<HTMLElement>(null);

  useEffect(() => {
    const tooltip = tooltipRef.current;
    if (!tooltip) return;

    const handleDismiss = () => {
      onDismiss?.();
    };

    tooltip.addEventListener('dismiss', handleDismiss);
    return () => tooltip.removeEventListener('dismiss', handleDismiss);
  }, [onDismiss]);

  return (
    <saf-tooltip
      ref={tooltipRef}
      anchor={anchor}
      placement={placement}
      trigger-on-click={triggerOnClick}
      show={show?.toString()}
    >
      {children}
    </saf-tooltip>
  );
};

// Usage examples
const TooltipExample: React.FC = () => {
  const [showControlled, setShowControlled] = useState(false);

  return (
    <div className="tooltip-examples">
      {/* Basic tooltip */}
      <button id="react-btn-1">Hover me</button>
      <SafTooltipComponent anchor="react-btn-1" placement="top">
        This is a React tooltip
      </SafTooltipComponent>

      {/* Click-triggered tooltip */}
      <button id="react-btn-2">Click me</button>
      <SafTooltipComponent
        anchor="react-btn-2"
        placement="bottom"
        triggerOnClick={true}
        onDismiss={() => console.log('Tooltip dismissed')}
      >
        Click-triggered tooltip with rich content
      </SafTooltipComponent>

      {/* Controlled tooltip */}
      <button 
        id="react-btn-3"
        onClick={() => setShowControlled(!showControlled)}
      >
        Toggle Controlled Tooltip
      </button>
      <SafTooltipComponent
        anchor="react-btn-3"
        placement="right"
        show={showControlled}
      >
        Controlled tooltip: {showControlled ? 'Visible' : 'Hidden'}
      </SafTooltipComponent>
    </div>
  );
};
```

### Angular Example

```typescript
// tooltip.component.ts
import { Component, Input, Output, EventEmitter, ViewChild, ElementRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-saf-tooltip',
  template: `
    <saf-tooltip
      #tooltipRef
      [attr.anchor]="anchor"
      [attr.placement]="placement"
      [attr.trigger-on-click]="triggerOnClick"
      [attr.show]="show?.toString()"
      (dismiss)="onDismiss()"
    >
      <ng-content></ng-content>
    </saf-tooltip>
  `
})
export class SafTooltipComponent implements AfterViewInit {
  @ViewChild('tooltipRef') tooltipRef!: ElementRef<HTMLElement>;
  
  @Input() anchor: string = '';
  @Input() placement: string = 'bottom';
  @Input() triggerOnClick: boolean = false;
  @Input() show?: boolean;
  
  @Output() dismiss = new EventEmitter<void>();

  ngAfterViewInit() {
    this.tooltipRef.nativeElement.addEventListener('dismiss', () => {
      this.dismiss.emit();
    });
  }

  onDismiss() {
    this.dismiss.emit();
  }
}

// Usage in template
/*
<button id="angular-btn">Hover me</button>
<app-saf-tooltip 
  anchor="angular-btn" 
  placement="top"
  (dismiss)="handleTooltipDismiss()"
>
  Angular tooltip content
</app-saf-tooltip>

<button id="click-btn">Click me</button>
<app-saf-tooltip 
  anchor="click-btn" 
  placement="bottom"
  [triggerOnClick]="true"
>
  <div>
    <strong>Rich Content</strong>
    <p>This tooltip supports HTML content</p>
  </div>
</app-saf-tooltip>
*/
```

### Vue Example

```vue
<template>
  <saf-tooltip
    :anchor="anchor"
    :placement="placement"
    :trigger-on-click="triggerOnClick"
    :show="show?.toString()"
    @dismiss="handleDismiss"
  >
    <slot></slot>
  </saf-tooltip>
</template>

<script>
export default {
  name: 'SafTooltipComponent',
  props: {
    anchor: {
      type: String,
      required: true
    },
    placement: {
      type: String,
      default: 'bottom',
      validator: value => [
        'top', 'top-start', 'top-end',
        'bottom', 'bottom-start', 'bottom-end',
        'left', 'right'
      ].includes(value)
    },
    triggerOnClick: {
      type: Boolean,
      default: false
    },
    show: {
      type: Boolean
    }
  },
  emits: ['dismiss'],
  methods: {
    handleDismiss() {
      this.$emit('dismiss');
    }
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div>
    <button id="vue-btn">Hover me</button>
    <SafTooltipComponent 
      anchor="vue-btn" 
      placement="top"
      @dismiss="onTooltipDismiss"
    >
      Vue tooltip content
    </SafTooltipComponent>
    
    <button id="vue-click-btn">Click me</button>
    <SafTooltipComponent 
      anchor="vue-click-btn" 
      placement="bottom"
      :trigger-on-click="true"
    >
      <div>
        <h4>Rich Content</h4>
        <p>Supports complex HTML structures</p>
      </div>
    </SafTooltipComponent>
  </div>
</template>
-->
```

## Accessibility Features

### ARIA Support

- Automatically adds `aria-describedby` to anchor elements
- Supports screen reader announcements for click-triggered tooltips
- Maintains proper focus management
- Uses semantic HTML structure

### Keyboard Navigation

- **Escape**: Dismisses visible tooltips
- **Focus management**: Shows tooltip on focus, hides on blur
- **Tab navigation**: Integrates with natural tab order
- **Click support**: Alternative interaction method for touch devices

### Screen Reader Support

- Content is announced when tooltip becomes visible
- Proper association between tooltip and anchor element
- Respects screen reader preferences and settings
- Works with high contrast modes

## Best Practices

### Content Guidelines
- Keep tooltip text concise and helpful
- Use tooltips for supplementary information, not critical content
- Avoid interactive elements within tooltips (except for click-triggered ones)
- Ensure tooltip content is accessible to screen readers

### Performance
- Minimize tooltip content for better rendering performance
- Use controlled visibility sparingly for dynamic content
- Avoid excessive DOM manipulation within tooltip content
- Clean up event listeners when components are destroyed

### User Experience
- Position tooltips to avoid covering important content
- Use consistent trigger patterns throughout your application
- Provide alternative ways to access tooltip information
- Test with both mouse and keyboard interactions

### Visual Design
- Ensure sufficient color contrast for tooltip text
- Use appropriate font sizes for readability
- Consider tooltip positioning on mobile devices
- Test across different viewport sizes

## Related Components

- **SafPopover**: For more complex overlay content
- **SafDialog**: For modal interactions requiring user response
- **SafAlert**: For system messages and notifications

---

*This documentation covers SafTooltip v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
