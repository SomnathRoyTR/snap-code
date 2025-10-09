# SafWindows

The `SafWindows` component is a specialized tabbed interface designed for managing multiple document windows or panels in enterprise applications. Built on the foundation of tabs, it provides additional functionality for adding and closing windows, making it ideal for applications where users work with multiple documents simultaneously.

## Table of Contents

- [Overview](#overview)
- [Component Structure](#component-structure)
- [API Reference](#api-reference)
- [Usage Examples](#usage-examples)
- [Accessibility](#accessibility)
- [Styling](#styling)
- [Integration](#integration)
- [Best Practices](#best-practices)

## Overview

SafWindows is a multi-component system consisting of:
- **SafWindows**: Main container component that manages window tabs
- **SafWindow**: Individual window tab component with optional close functionality
- **SafWindowPanel**: Content area component for each window

This component extends the functionality of SafTabs to provide a more document-centric interface where users can dynamically add and remove windows.

### Key Features

- **Dynamic Window Management**: Add and remove windows at runtime
- **Closeable Windows**: Optional close buttons on individual windows
- **Full-Width Support**: Windows can contain full-width content without padding
- **Keyboard Navigation**: Full keyboard support with arrow keys and tab navigation
- **Accessibility**: Comprehensive ARIA support and screen reader compatibility
- **Customizable Labels**: Configurable aria-labels for add and close buttons

## Component Structure

```
SafWindows
├── Window Tabs (SafWindow components)
│   ├── Window Label
│   └── Close Button (optional)
├── Add Button (optional)
└── Window Panels (SafWindowPanel components)
    └── Panel Content
```

## API Reference

### SafWindows

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `addable` | `boolean` | `true` | Whether users can add new windows |
| `addAriaLabel` | `string` | `"Add new window"` | Accessible label for the add button |
| `a11yAriaLabel` | `string` | `undefined` | Label for the entire windows container |
| `activeid` | `string` | `undefined` | ID of the currently active window |
| `orientation` | `"horizontal" \| "vertical"` | `"horizontal"` | Layout orientation of windows |

#### Events

| Event | Type | Description |
|-------|------|-------------|
| `add` | `CustomEvent` | Fired when the add button is clicked |
| `change` | `CustomEvent<{ oldTab: HTMLElement, newTab: HTMLElement }>` | Fired when active window changes |

#### Parts

| Part | Description |
|------|-------------|
| `windows` | The main windows container |
| `tablist` | The container for window tabs |
| `add-window-button` | The add new window button |
| `add-tooltip` | Tooltip for the add button |
| `tabpanel` | The container for window panels |

#### Slots

| Slot | Description |
|------|-------------|
| `tab` | Window tab components (SafWindow) |
| `tabpanel` | Window panel components (SafWindowPanel) |
| `start` | Content before the first window tab |
| `end` | Content after the last window tab |

### SafWindow

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `closeable` | `boolean` | `true` | Whether the window can be closed |
| `closeAriaLabel` | `string` | `"Close"` | Accessible label for the close button |
| `disabled` | `boolean` | `false` | Whether the window is disabled |
| `id` | `string` | `undefined` | Unique identifier for the window |

#### Events

| Event | Type | Description |
|-------|------|-------------|
| `close` | `CustomEvent` | Fired when the close button is clicked |

#### Parts

| Part | Description |
|------|-------------|
| `window-label` | The clickable window label area |
| `close-window-button` | The close button |
| `close-tooltip` | Tooltip for the close button |

### SafWindowPanel

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `isFullWidth` | `boolean` | `false` | Whether panel content is full-width without padding |

## Usage Examples

### Basic Windows Interface

```html
<!-- HTML -->
<saf-windows a11y-aria-label="Document Windows">
  <!-- Window Tabs -->
  <saf-window slot="tab" id="doc1">Document 1</saf-window>
  <saf-window slot="tab" id="doc2">Document 2</saf-window>
  <saf-window slot="tab" id="doc3" closeable="false">Document 3</saf-window>
  
  <!-- Window Panels -->
  <saf-window-panel slot="tabpanel">
    <p>Content for document 1...</p>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <p>Content for document 2...</p>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <p>Content for document 3...</p>
  </saf-window-panel>
</saf-windows>
```

### React Implementation

```tsx
import React, { useState } from 'react';

interface WindowData {
  id: string;
  title: string;
  content: string;
  closeable?: boolean;
}

function DocumentWindows() {
  const [windows, setWindows] = useState<WindowData[]>([
    { id: 'doc1', title: 'Document 1', content: 'Content 1', closeable: true },
    { id: 'doc2', title: 'Document 2', content: 'Content 2', closeable: true },
    { id: 'doc3', title: 'Home', content: 'Home content', closeable: false },
  ]);
  
  const [activeWindow, setActiveWindow] = useState('doc1');

  const handleAddWindow = () => {
    const newId = `doc${Date.now()}`;
    const newWindow: WindowData = {
      id: newId,
      title: `Document ${windows.length + 1}`,
      content: `New document content`,
      closeable: true,
    };
    
    setWindows([...windows, newWindow]);
    setActiveWindow(newId);
  };

  const handleCloseWindow = (windowId: string) => {
    const updatedWindows = windows.filter(w => w.id !== windowId);
    setWindows(updatedWindows);
    
    // Switch to first window if closing active window
    if (windowId === activeWindow && updatedWindows.length > 0) {
      setActiveWindow(updatedWindows[0].id);
    }
  };

  const handleWindowChange = (event: CustomEvent) => {
    const newTab = event.detail.newTab;
    const windowId = newTab?.id;
    if (windowId) {
      setActiveWindow(windowId);
    }
  };

  return (
    <saf-windows
      a11y-aria-label="Document Editor"
      addable={true}
      add-aria-label="Add new document"
      activeid={activeWindow}
      onAdd={handleAddWindow}
      onChange={handleWindowChange}
    >
      {windows.map(window => (
        <saf-window
          key={window.id}
          slot="tab"
          id={window.id}
          closeable={window.closeable}
          close-aria-label={`Close ${window.title}`}
          onClose={() => handleCloseWindow(window.id)}
        >
          {window.title}
        </saf-window>
      ))}
      
      {windows.map(window => (
        <saf-window-panel key={`panel-${window.id}`} slot="tabpanel">
          <div className="window-content">
            <h2>{window.title}</h2>
            <p>{window.content}</p>
          </div>
        </saf-window-panel>
      ))}
    </saf-windows>
  );
}
```

### Angular Implementation

```typescript
import { Component } from '@angular/core';

interface WindowData {
  id: string;
  title: string;
  content: string;
  closeable?: boolean;
}

@Component({
  selector: 'app-document-windows',
  template: `
    <saf-windows
      [a11y-aria-label]="'Document Manager'"
      [addable]="true"
      [add-aria-label]="'Add new document'"
      [activeid]="activeWindow"
      (add)="handleAddWindow()"
      (change)="handleWindowChange($event)">
      
      <saf-window
        *ngFor="let window of windows"
        slot="tab"
        [id]="window.id"
        [closeable]="window.closeable"
        [close-aria-label]="'Close ' + window.title"
        (close)="handleCloseWindow(window.id)">
        {{ window.title }}
      </saf-window>
      
      <saf-window-panel
        *ngFor="let window of windows"
        slot="tabpanel">
        <div class="window-content">
          <h2>{{ window.title }}</h2>
          <p>{{ window.content }}</p>
        </div>
      </saf-window-panel>
    </saf-windows>
  `
})
export class DocumentWindowsComponent {
  windows: WindowData[] = [
    { id: 'doc1', title: 'Document 1', content: 'Content 1', closeable: true },
    { id: 'doc2', title: 'Document 2', content: 'Content 2', closeable: true },
    { id: 'home', title: 'Home', content: 'Home content', closeable: false },
  ];
  
  activeWindow = 'doc1';

  handleAddWindow() {
    const newId = `doc${Date.now()}`;
    const newWindow: WindowData = {
      id: newId,
      title: `Document ${this.windows.length + 1}`,
      content: 'New document content',
      closeable: true,
    };
    
    this.windows = [...this.windows, newWindow];
    this.activeWindow = newId;
  }

  handleCloseWindow(windowId: string) {
    this.windows = this.windows.filter(w => w.id !== windowId);
    
    // Switch to first window if closing active window
    if (windowId === this.activeWindow && this.windows.length > 0) {
      this.activeWindow = this.windows[0].id;
    }
  }

  handleWindowChange(event: CustomEvent) {
    const newTab = event.detail.newTab;
    const windowId = newTab?.id;
    if (windowId) {
      this.activeWindow = windowId;
    }
  }
}
```

### Full-Width Content

```html
<saf-windows a11y-aria-label="Application Views">
  <saf-window slot="tab" id="dashboard">Dashboard</saf-window>
  <saf-window slot="tab" id="charts">Charts</saf-window>
  
  <!-- Regular panel with padding -->
  <saf-window-panel slot="tabpanel">
    <div class="padded-content">
      <h2>Dashboard</h2>
      <p>Regular content with padding...</p>
    </div>
  </saf-window-panel>
  
  <!-- Full-width panel without padding -->
  <saf-window-panel slot="tabpanel" is-full-width="true">
    <div class="chart-container">
      <!-- Charts or maps that need full width -->
    </div>
  </saf-window-panel>
</saf-windows>
```

### With Custom Controls

```html
<saf-windows a11y-aria-label="Code Editor">
  <!-- Custom start content -->
  <div slot="start">
    <saf-button appearance="tertiary" icon-only="true">
      <saf-icon icon-name="folder-open"></saf-icon>
    </saf-button>
  </div>
  
  <saf-window slot="tab" id="file1" closeable="false">main.ts</saf-window>
  <saf-window slot="tab" id="file2">component.ts</saf-window>
  
  <!-- Custom end content -->
  <div slot="end">
    <saf-button appearance="tertiary" icon-only="true">
      <saf-icon icon-name="ellipsis"></saf-icon>
    </saf-button>
  </div>
  
  <saf-window-panel slot="tabpanel" is-full-width="true">
    <div class="code-editor">
      <!-- Code editor content -->
    </div>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel" is-full-width="true">
    <div class="code-editor">
      <!-- Another file content -->
    </div>
  </saf-window-panel>
</saf-windows>
```

### Vertical Windows

```html
<saf-windows 
  orientation="vertical" 
  a11y-aria-label="Side Panel Windows"
  addable="false">
  
  <saf-window slot="tab" id="explorer">Explorer</saf-window>
  <saf-window slot="tab" id="search">Search</saf-window>
  <saf-window slot="tab" id="git">Source Control</saf-window>
  
  <saf-window-panel slot="tabpanel">
    <div class="explorer-content">
      <!-- File explorer content -->
    </div>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <div class="search-content">
      <!-- Search results -->
    </div>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <div class="git-content">
      <!-- Git status and controls -->
    </div>
  </saf-window-panel>
</saf-windows>
```

## Accessibility

SafWindows provides comprehensive accessibility support:

### ARIA Implementation

- **Container Role**: The windows container uses `role="tablist"`
- **Window Roles**: Each window uses `role="tab"` with proper `aria-selected` state
- **Panel Roles**: Window panels use `role="tabpanel"` with proper `aria-labelledby`
- **Group Context**: Windows provide `role="group"` with descriptive labels

### Keyboard Navigation

| Key | Action |
|-----|--------|
| **Arrow Keys** | Navigate between windows |
| **Tab** | Move focus to next focusable element |
| **Enter/Space** | Activate focused window |
| **Home** | Move to first window |
| **End** | Move to last window |
| **Escape** | Move focus away from windows (context-dependent) |

### Screen Reader Support

- **Descriptive Labels**: All interactive elements have meaningful labels
- **State Announcements**: Window selection and focus changes are announced
- **Button Context**: Add and close buttons have descriptive labels
- **Content Association**: Panels are properly associated with their windows

### Required Accessibility Attributes

```html
<saf-windows a11y-aria-label="Document Editor Windows">
  <saf-window 
    slot="tab" 
    id="doc1"
    close-aria-label="Close Document 1">
    Document 1
  </saf-window>
</saf-windows>
```

## Styling

### CSS Custom Properties

```css
saf-windows {
  /* Window container spacing */
  --windows-gap: var(--spacing-2);
  
  /* Window tab styling */
  --window-padding: var(--spacing-3) var(--spacing-4);
  --window-border-radius: var(--border-radius-2);
  
  /* Active window styling */
  --window-active-bg: var(--color-neutral-layer-1);
  --window-active-border: var(--color-accent-primary);
  
  /* Close button styling */
  --close-button-size: 20px;
  --close-button-hover-bg: var(--color-neutral-layer-3);
}
```

### Component Parts Styling

```css
/* Style the windows container */
saf-windows::part(windows) {
  border-bottom: 1px solid var(--color-neutral-stroke-2);
  background: var(--color-neutral-layer-2);
}

/* Style individual window tabs */
saf-window::part(window-label) {
  padding: var(--spacing-2) var(--spacing-3);
  border-radius: var(--border-radius-1);
  transition: background-color 150ms ease;
}

/* Style the close button */
saf-window::part(close-window-button) {
  margin-left: var(--spacing-1);
  opacity: 0.7;
  transition: opacity 150ms ease;
}

saf-window:hover::part(close-window-button) {
  opacity: 1;
}

/* Style the add button */
saf-windows::part(add-window-button) {
  margin-left: var(--spacing-2);
  color: var(--color-neutral-foreground-2);
}
```

### Window Panel Styling

```css
/* Regular window panel */
saf-window-panel {
  padding: var(--spacing-4);
  background: var(--color-neutral-layer-1);
}

/* Full-width window panel */
saf-window-panel[is-full-width] {
  padding: 0;
}
```

## Integration

### With Form Components

```html
<saf-windows a11y-aria-label="Form Sections">
  <saf-window slot="tab" id="basic">Basic Info</saf-window>
  <saf-window slot="tab" id="advanced">Advanced</saf-window>
  
  <saf-window-panel slot="tabpanel">
    <saf-form>
      <saf-form-field label="Name">
        <saf-text-input name="name"></saf-text-input>
      </saf-form-field>
      <!-- More basic fields -->
    </saf-form>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <saf-form>
      <!-- Advanced form fields -->
    </saf-form>
  </saf-window-panel>
</saf-windows>
```

### With Data Components

```html
<saf-windows a11y-aria-label="Data Views">
  <saf-window slot="tab" id="table">Table View</saf-window>
  <saf-window slot="tab" id="chart">Chart View</saf-window>
  
  <saf-window-panel slot="tabpanel" is-full-width="true">
    <saf-data-grid>
      <!-- Data grid content -->
    </saf-data-grid>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel" is-full-width="true">
    <div class="chart-container">
      <!-- Chart component -->
    </div>
  </saf-window-panel>
</saf-windows>
```

### With Navigation

```html
<saf-windows a11y-aria-label="Application Sections">
  <saf-window slot="tab" id="overview" closeable="false">Overview</saf-window>
  <saf-window slot="tab" id="details">Details</saf-window>
  
  <saf-window-panel slot="tabpanel">
    <saf-navigation>
      <!-- Sub-navigation for overview -->
    </saf-navigation>
    <div class="overview-content">
      <!-- Overview content -->
    </div>
  </saf-window-panel>
  
  <saf-window-panel slot="tabpanel">
    <div class="details-content">
      <!-- Detailed content -->
    </div>
  </saf-window-panel>
</saf-windows>
```

## Best Practices

### Content Organization
- **Logical Grouping**: Group related content in windows
- **Consistent Labeling**: Use clear, descriptive window titles
- **Reasonable Limits**: Avoid too many windows (typically 5-8 maximum)
- **Essential vs Optional**: Mark critical windows as non-closeable

### User Experience
- **Default States**: Provide reasonable default active window
- **Confirmation**: Consider confirmation for closing unsaved content
- **State Persistence**: Remember user's window preferences when possible
- **Loading States**: Handle loading content gracefully

### Accessibility
- **Descriptive Labels**: Provide meaningful `a11y-aria-label` for the container
- **Button Labels**: Use specific labels for add/close buttons
- **Focus Management**: Ensure proper focus handling after window operations
- **Screen Reader Testing**: Test with actual screen readers

### Performance
- **Lazy Loading**: Load window content only when needed
- **Memory Management**: Clean up resources when windows are closed
- **Efficient Updates**: Use efficient state management for dynamic windows
- **Content Virtualization**: Consider virtualization for many windows

### Visual Design
- **Consistent Styling**: Use consistent visual patterns across windows
- **Clear States**: Make active/inactive states visually distinct
- **Icon Usage**: Use appropriate icons for different window types
- **Responsive Behavior**: Handle window overflow appropriately

SafWindows provides a powerful and accessible solution for managing multiple document windows in enterprise applications while maintaining consistency with the Saffron Design System.
