# SafDrawer Component

The **SafDrawer** component is a slide-out panel that displays content over or alongside the main interface. It extends the dialog functionality with specific positioning and interaction patterns suitable for navigation, filters, or supplementary content.

## Basic Usage

```html
<!-- Basic drawer -->
<button onclick="openDrawer()">Open Drawer</button>
<saf-drawer id="my-drawer" drawer-title="Settings">
  <p>Drawer content goes here</p>
  <button slot="footer" onclick="closeDrawer()">Close</button>
</saf-drawer>

<script>
function openDrawer() {
  document.getElementById('my-drawer').show();
}

function closeDrawer() {
  document.getElementById('my-drawer').hide();
}
</script>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `hidden` | `boolean` | `true` | Whether the drawer is hidden |
| `modal` | `boolean` | `true` | Whether drawer is modal with overlay |
| `placement` | `'right' \| 'bottom'` | `'right'` | Position where drawer slides from |
| `drawer-title` | `string` | - | Title displayed in drawer header |
| `drawer-subtitle` | `string` | - | Subtitle displayed in drawer header |
| `aria-title-level` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `2` | Heading level for drawer title |
| `aria-subtitle-level` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `3` | Heading level for drawer subtitle |
| `is-header` | `boolean` | `true` | Whether to show the drawer header |
| `is-footer` | `boolean` | `false` | Whether to show the drawer footer |
| `close-aria-label` | `string` | - | Accessible label for close button |
| `a11y-aria-label` | `string` | - | Aria label when no title is present |
| `no-focus-trap` | `boolean` | `false` | Whether to disable focus trapping |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `hidden` | `boolean` | `true` | Current visibility state |
| `modal` | `boolean` | `true` | Whether drawer has modal overlay |
| `placement` | `DrawerPlacement` | `'right'` | Drawer slide direction |

### Methods

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `show()` | - | `void` | Shows the drawer |
| `hide()` | - | `void` | Hides the drawer |
| `dismiss()` | - | `void` | Dismisses drawer and emits events |

### Events

| Event | Detail | Description |
|-------|--------|-------------|
| `show` | - | Fired when drawer is shown |
| `hide` | - | Fired when drawer is hidden |
| `dismiss` | - | Fired when drawer is dismissed |
| `cancel` | - | Fired when drawer is cancelled (Escape key) |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Main drawer content |
| `header` | Custom header content |
| `footer` | Footer content (buttons, actions) |

### CSS Parts

| Part | Description |
|------|-------------|
| `positioning-region` | Main drawer container |
| `overlay` | Modal overlay background |
| `control` | Drawer panel element |
| `header` | Header section |
| `title` | Title element |
| `subtitle` | Subtitle element |
| `close` | Close button |
| `content` | Content area |
| `footer` | Footer section |

## Comprehensive Examples

### Right-Placed Drawer (Default)

```html
<div class="drawer-demo">
  <button id="open-right-drawer" onclick="openRightDrawer()">Open Right Drawer</button>
  
  <saf-drawer 
    id="right-drawer" 
    placement="right" 
    drawer-title="Navigation" 
    drawer-subtitle="App Settings"
    close-aria-label="Close navigation drawer"
  >
    <nav class="drawer-nav">
      <a href="/dashboard" class="nav-item">
        <saf-icon name="dashboard"></saf-icon>
        Dashboard
      </a>
      <a href="/projects" class="nav-item">
        <saf-icon name="folder"></saf-icon>
        Projects
      </a>
      <a href="/settings" class="nav-item">
        <saf-icon name="settings"></saf-icon>
        Settings
      </a>
      <a href="/help" class="nav-item">
        <saf-icon name="help"></saf-icon>
        Help
      </a>
    </nav>
    
    <div slot="footer">
      <saf-button appearance="secondary" onclick="closeRightDrawer()">
        Cancel
      </saf-button>
      <saf-button onclick="closeRightDrawer()">
        Apply
      </saf-button>
    </div>
  </saf-drawer>
</div>

<script>
function openRightDrawer() {
  document.getElementById('right-drawer').show();
}

function closeRightDrawer() {
  document.getElementById('right-drawer').hide();
}
</script>

<style>
.drawer-nav {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem;
  text-decoration: none;
  color: inherit;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.nav-item:hover {
  background-color: #f5f5f5;
}
</style>
```

### Bottom-Placed Drawer

```html
<div class="bottom-drawer-demo">
  <button onclick="openBottomDrawer()">Show Filters</button>
  
  <saf-drawer 
    id="bottom-drawer" 
    placement="bottom" 
    drawer-title="Advanced Filters"
    is-footer="true"
  >
    <div class="filter-content">
      <div class="filter-group">
        <label>Date Range</label>
        <div class="date-inputs">
          <input type="date" placeholder="Start date">
          <input type="date" placeholder="End date">
        </div>
      </div>
      
      <div class="filter-group">
        <label>Category</label>
        <saf-select>
          <option value="">All Categories</option>
          <option value="documents">Documents</option>
          <option value="images">Images</option>
          <option value="videos">Videos</option>
        </saf-select>
      </div>
      
      <div class="filter-group">
        <label>Size</label>
        <div class="size-options">
          <saf-checkbox>Small (< 1MB)</saf-checkbox>
          <saf-checkbox>Medium (1-10MB)</saf-checkbox>
          <saf-checkbox>Large (> 10MB)</saf-checkbox>
        </div>
      </div>
    </div>
    
    <div slot="footer" class="filter-actions">
      <saf-button appearance="secondary" onclick="clearFilters()">
        Clear All
      </saf-button>
      <saf-button onclick="applyFilters()">
        Apply Filters
      </saf-button>
    </div>
  </saf-drawer>
</div>

<script>
function openBottomDrawer() {
  document.getElementById('bottom-drawer').show();
}

function clearFilters() {
  // Clear all filter inputs
  console.log('Filters cleared');
}

function applyFilters() {
  // Apply filters and close drawer
  document.getElementById('bottom-drawer').hide();
  console.log('Filters applied');
}
</script>

<style>
.filter-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  padding: 1rem 0;
}

.filter-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.filter-group label {
  font-weight: 500;
  font-size: 14px;
}

.date-inputs {
  display: flex;
  gap: 0.5rem;
}

.size-options {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.filter-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}
</style>
```

### Non-Modal Drawer

```html
<div class="non-modal-demo">
  <div class="layout">
    <aside class="sidebar">
      <button onclick="toggleSidebar()">Toggle Sidebar</button>
      <p>Main sidebar content</p>
    </aside>
    
    <main class="main-content">
      <h1>Main Content</h1>
      <p>This content remains interactive when the non-modal drawer is open.</p>
      <button onclick="openNonModalDrawer()">Open Non-Modal Drawer</button>
    </main>
  </div>
  
  <saf-drawer 
    id="non-modal-drawer" 
    modal="false"
    drawer-title="Quick Actions"
    is-footer="true"
  >
    <div class="quick-actions">
      <button class="action-btn">
        <saf-icon name="save"></saf-icon>
        Quick Save
      </button>
      <button class="action-btn">
        <saf-icon name="share"></saf-icon>
        Share
      </button>
      <button class="action-btn">
        <saf-icon name="print"></saf-icon>
        Print
      </button>
      <button class="action-btn">
        <saf-icon name="download"></saf-icon>
        Download
      </button>
    </div>
    
    <div slot="footer">
      <saf-button appearance="secondary" onclick="closeNonModalDrawer()">
        Close
      </saf-button>
    </div>
  </saf-drawer>
</div>

<script>
function openNonModalDrawer() {
  document.getElementById('non-modal-drawer').show();
}

function closeNonModalDrawer() {
  document.getElementById('non-modal-drawer').hide();
}
</script>

<style>
.layout {
  display: flex;
  height: 400px;
  border: 1px solid #ccc;
}

.sidebar {
  width: 200px;
  background: #f0f0f0;
  padding: 1rem;
}

.main-content {
  flex: 1;
  padding: 1rem;
}

.quick-actions {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1rem;
}

.action-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
}

.action-btn:hover {
  background: #f5f5f5;
}
</style>
```

### Drawer with Form Content

```html
<div class="form-drawer-demo">
  <button onclick="openFormDrawer()">Add New Item</button>
  
  <saf-drawer 
    id="form-drawer" 
    drawer-title="Add New Product"
    drawer-subtitle="Fill in the product details"
    is-footer="true"
  >
    <form id="product-form" class="drawer-form">
      <div class="form-row">
        <saf-text-field label="Product Name" required></saf-text-field>
      </div>
      
      <div class="form-row">
        <saf-text-area label="Description" rows="3"></saf-text-area>
      </div>
      
      <div class="form-row-group">
        <saf-number-field label="Price" step="0.01"></saf-number-field>
        <saf-number-field label="Quantity"></saf-number-field>
      </div>
      
      <div class="form-row">
        <saf-select label="Category">
          <option value="">Select a category</option>
          <option value="electronics">Electronics</option>
          <option value="clothing">Clothing</option>
          <option value="books">Books</option>
        </saf-select>
      </div>
      
      <div class="form-row">
        <saf-checkbox-group label="Features">
          <saf-checkbox value="featured">Featured Product</saf-checkbox>
          <saf-checkbox value="new">New Arrival</saf-checkbox>
          <saf-checkbox value="sale">On Sale</saf-checkbox>
        </saf-checkbox-group>
      </div>
      
      <div class="form-row">
        <saf-file-upload 
          label="Product Images"
          accept="image/*"
          multiple
        ></saf-file-upload>
      </div>
    </form>
    
    <div slot="footer" class="form-actions">
      <saf-button appearance="secondary" onclick="cancelForm()">
        Cancel
      </saf-button>
      <saf-button onclick="saveProduct()">
        Save Product
      </saf-button>
    </div>
  </saf-drawer>
</div>

<script>
function openFormDrawer() {
  document.getElementById('form-drawer').show();
}

function cancelForm() {
  if (confirm('Are you sure you want to cancel? Unsaved changes will be lost.')) {
    document.getElementById('form-drawer').hide();
    document.getElementById('product-form').reset();
  }
}

function saveProduct() {
  const form = document.getElementById('product-form');
  if (form.checkValidity()) {
    // Save the product
    console.log('Product saved');
    form.reset();
    document.getElementById('form-drawer').hide();
  } else {
    form.reportValidity();
  }
}
</script>

<style>
.drawer-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  max-width: 400px;
}

.form-row-group {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}
</style>
```

### Drawer with Event Handling

```html
<div class="event-demo">
  <button onclick="openEventDrawer()">Open Event Drawer</button>
  <div id="event-log" class="event-log"></div>
  
  <saf-drawer 
    id="event-drawer" 
    drawer-title="Event Demonstration"
  >
    <p>This drawer demonstrates event handling.</p>
    <p>Check the event log below to see fired events.</p>
    
    <div slot="footer">
      <saf-button onclick="dismissEventDrawer()">Dismiss</saf-button>
    </div>
  </saf-drawer>
</div>

<script>
const eventDrawer = document.getElementById('event-drawer');
const eventLog = document.getElementById('event-log');

function logEvent(eventName, detail = {}) {
  const time = new Date().toLocaleTimeString();
  const entry = document.createElement('div');
  entry.className = 'event-entry';
  entry.innerHTML = `<strong>${time}</strong>: ${eventName} ${JSON.stringify(detail)}`;
  eventLog.appendChild(entry);
  eventLog.scrollTop = eventLog.scrollHeight;
}

function openEventDrawer() {
  eventDrawer.show();
  logEvent('Opening drawer programmatically');
}

function dismissEventDrawer() {
  eventDrawer.dismiss();
  logEvent('Dismissing drawer programmatically');
}

// Add event listeners
eventDrawer.addEventListener('show', (e) => {
  logEvent('show event fired', { target: e.target.tagName });
});

eventDrawer.addEventListener('hide', (e) => {
  logEvent('hide event fired', { target: e.target.tagName });
});

eventDrawer.addEventListener('dismiss', (e) => {
  logEvent('dismiss event fired', { target: e.target.tagName });
});

eventDrawer.addEventListener('cancel', (e) => {
  logEvent('cancel event fired (Escape key)', { target: e.target.tagName });
});
</script>

<style>
.event-log {
  margin-top: 1rem;
  padding: 1rem;
  background: #f5f5f5;
  border-radius: 4px;
  max-height: 200px;
  overflow-y: auto;
  font-family: monospace;
  font-size: 12px;
}

.event-entry {
  margin-bottom: 0.5rem;
  padding: 0.25rem;
  background: white;
  border-radius: 2px;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React, { useState, useRef, useEffect } from 'react';

interface DrawerProps {
  isOpen: boolean;
  onClose: () => void;
  title?: string;
  subtitle?: string;
  placement?: 'right' | 'bottom';
  modal?: boolean;
  hasFooter?: boolean;
  children: React.ReactNode;
  footer?: React.ReactNode;
}

const SafDrawerComponent: React.FC<DrawerProps> = ({
  isOpen,
  onClose,
  title,
  subtitle,
  placement = 'right',
  modal = true,
  hasFooter = false,
  children,
  footer
}) => {
  const drawerRef = useRef<HTMLElement>(null);

  useEffect(() => {
    const drawer = drawerRef.current;
    if (!drawer) return;

    if (isOpen) {
      drawer.show();
    } else {
      drawer.hide();
    }
  }, [isOpen]);

  useEffect(() => {
    const drawer = drawerRef.current;
    if (!drawer) return;

    const handleHide = () => onClose();
    const handleDismiss = () => onClose();
    const handleCancel = () => onClose();

    drawer.addEventListener('hide', handleHide);
    drawer.addEventListener('dismiss', handleDismiss);
    drawer.addEventListener('cancel', handleCancel);

    return () => {
      drawer.removeEventListener('hide', handleHide);
      drawer.removeEventListener('dismiss', handleDismiss);
      drawer.removeEventListener('cancel', handleCancel);
    };
  }, [onClose]);

  return (
    <saf-drawer
      ref={drawerRef}
      drawer-title={title}
      drawer-subtitle={subtitle}
      placement={placement}
      modal={modal.toString()}
      is-footer={hasFooter.toString()}
      hidden="true"
    >
      {children}
      {footer && <div slot="footer">{footer}</div>}
    </saf-drawer>
  );
};

// Usage example
const DrawerExample: React.FC = () => {
  const [isSettingsOpen, setIsSettingsOpen] = useState(false);
  const [isFiltersOpen, setIsFiltersOpen] = useState(false);

  return (
    <div className="drawer-examples">
      <button onClick={() => setIsSettingsOpen(true)}>
        Open Settings
      </button>
      <button onClick={() => setIsFiltersOpen(true)}>
        Open Filters
      </button>

      <SafDrawerComponent
        isOpen={isSettingsOpen}
        onClose={() => setIsSettingsOpen(false)}
        title="Application Settings"
        subtitle="Customize your experience"
        hasFooter={true}
        footer={
          <div style={{ display: 'flex', gap: '1rem' }}>
            <button onClick={() => setIsSettingsOpen(false)}>
              Cancel
            </button>
            <button onClick={() => setIsSettingsOpen(false)}>
              Save Settings
            </button>
          </div>
        }
      >
        <div>Settings content goes here</div>
      </SafDrawerComponent>

      <SafDrawerComponent
        isOpen={isFiltersOpen}
        onClose={() => setIsFiltersOpen(false)}
        title="Filters"
        placement="bottom"
        hasFooter={true}
        footer={
          <button onClick={() => setIsFiltersOpen(false)}>
            Apply Filters
          </button>
        }
      >
        <div>Filter options go here</div>
      </SafDrawerComponent>
    </div>
  );
};
```

### Angular Example

```typescript
// drawer.component.ts
import { Component, Input, Output, EventEmitter, ViewChild, ElementRef, OnChanges, OnInit } from '@angular/core';

@Component({
  selector: 'app-saf-drawer',
  template: `
    <saf-drawer
      #drawerRef
      [attr.drawer-title]="title"
      [attr.drawer-subtitle]="subtitle"
      [attr.placement]="placement"
      [attr.modal]="modal"
      [attr.is-footer]="hasFooter"
      hidden="true"
      (show)="onShow()"
      (hide)="onHide()"
      (dismiss)="onDismiss()"
      (cancel)="onCancel()"
    >
      <ng-content></ng-content>
      <ng-content select="[slot=footer]" slot="footer"></ng-content>
    </saf-drawer>
  `
})
export class SafDrawerComponent implements OnChanges, OnInit {
  @ViewChild('drawerRef') drawerRef!: ElementRef<HTMLElement>;
  
  @Input() isOpen: boolean = false;
  @Input() title?: string;
  @Input() subtitle?: string;
  @Input() placement: 'right' | 'bottom' = 'right';
  @Input() modal: boolean = true;
  @Input() hasFooter: boolean = false;
  
  @Output() close = new EventEmitter<void>();
  @Output() show = new EventEmitter<void>();
  @Output() hide = new EventEmitter<void>();
  @Output() dismiss = new EventEmitter<void>();
  @Output() cancel = new EventEmitter<void>();

  ngOnChanges(changes: any) {
    if (changes.isOpen && this.drawerRef?.nativeElement) {
      if (this.isOpen) {
        (this.drawerRef.nativeElement as any).show();
      } else {
        (this.drawerRef.nativeElement as any).hide();
      }
    }
  }

  onShow() {
    this.show.emit();
  }

  onHide() {
    this.close.emit();
    this.hide.emit();
  }

  onDismiss() {
    this.close.emit();
    this.dismiss.emit();
  }

  onCancel() {
    this.close.emit();
    this.cancel.emit();
  }
}

// Usage in template
/*
<button (click)="openSettings()">Open Settings</button>

<app-saf-drawer
  [isOpen]="isSettingsOpen"
  (close)="closeSettings()"
  title="Settings"
  subtitle="Configure your preferences"
  [hasFooter]="true"
>
  <div>Settings content</div>
  <div slot="footer">
    <button (click)="closeSettings()">Close</button>
  </div>
</app-saf-drawer>
*/
```

### Vue Example

```vue
<template>
  <saf-drawer
    ref="drawerRef"
    :drawer-title="title"
    :drawer-subtitle="subtitle"
    :placement="placement"
    :modal="modal"
    :is-footer="hasFooter"
    hidden="true"
    @show="handleShow"
    @hide="handleHide"
    @dismiss="handleDismiss"
    @cancel="handleCancel"
  >
    <slot></slot>
    <template #footer>
      <slot name="footer"></slot>
    </template>
  </saf-drawer>
</template>

<script>
export default {
  name: 'SafDrawerComponent',
  props: {
    isOpen: {
      type: Boolean,
      default: false
    },
    title: String,
    subtitle: String,
    placement: {
      type: String,
      default: 'right',
      validator: value => ['right', 'bottom'].includes(value)
    },
    modal: {
      type: Boolean,
      default: true
    },
    hasFooter: {
      type: Boolean,
      default: false
    }
  },
  emits: ['close', 'show', 'hide', 'dismiss', 'cancel'],
  watch: {
    isOpen: {
      handler(newVal) {
        if (this.$refs.drawerRef) {
          if (newVal) {
            this.$refs.drawerRef.show();
          } else {
            this.$refs.drawerRef.hide();
          }
        }
      },
      immediate: true
    }
  },
  methods: {
    handleShow() {
      this.$emit('show');
    },
    handleHide() {
      this.$emit('close');
      this.$emit('hide');
    },
    handleDismiss() {
      this.$emit('close');
      this.$emit('dismiss');
    },
    handleCancel() {
      this.$emit('close');
      this.$emit('cancel');
    }
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div>
    <button @click="openSettings">Open Settings</button>
    
    <SafDrawerComponent
      :is-open="isSettingsOpen"
      @close="closeSettings"
      title="Settings"
      subtitle="Configure your preferences"
      :has-footer="true"
    >
      <div>Settings content</div>
      <template #footer>
        <button @click="closeSettings">Close</button>
      </template>
    </SafDrawerComponent>
  </div>
</template>
-->
```

## Accessibility Features

### ARIA Support

- Proper dialog role and labeling
- Configurable heading levels for title and subtitle
- Focus management and restoration
- Keyboard navigation support

### Keyboard Navigation

- **Escape**: Closes the drawer and emits cancel event
- **Tab**: Moves focus within drawer (focus trap enabled by default)
- **Shift+Tab**: Moves focus backward within drawer

### Screen Reader Support

- Announces drawer opening and closing
- Proper heading structure with configurable levels
- Accessible close button with customizable label
- Supports aria-label when no title is present

## Best Practices

### Content Organization
- Use clear, descriptive titles and subtitles
- Organize content in logical sections
- Include relevant actions in the footer
- Keep content focused and task-oriented

### User Experience
- Use appropriate placement based on content type
- Consider modal vs. non-modal based on context
- Provide clear ways to close the drawer
- Test across different screen sizes

### Performance
- Lazy load drawer content when possible
- Clean up event listeners and resources
- Minimize drawer content for better rendering
- Use appropriate placement for mobile devices

### Visual Design
- Follow consistent spacing and typography
- Ensure sufficient color contrast
- Consider reduced motion preferences
- Test with different content lengths

## Related Components

- **SafDialog**: For modal dialogs and confirmations
- **SafSideNav**: For persistent navigation panels  
- **SafPopover**: For smaller contextual content overlays

---

*This documentation covers SafDrawer v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
