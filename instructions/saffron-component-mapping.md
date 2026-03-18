# Saffron Component Mapping Guide

## Overview
This document maps standard HTML elements to their Saffron Design System equivalents. Saffron components are web components using shadow DOM, referenced in Angular templates with kebab-case names (e.g., `saf-button`, `saf-text-field`).

## Component Naming Conventions
- **Angular/Web Components**: kebab-case with `saf-` prefix (e.g., `saf-button`)
- **React**: PascalCase with `Saf` prefix (e.g., `SafButton`)
- **CSS Custom Properties**: `--saffron-` prefix (e.g., `--saffron-color-primary`)

## HTML to Saffron Component Mapping

### Form Controls
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<input type="text">` | `<saf-text-field>` | Use `type` attribute for variants |
| `<input type="number">` | `<saf-text-field type="number">` | Numeric input with formatting |
| `<input type="password">` | `<saf-text-field type="password">` | Password with visibility toggle |
| `<input type="email">` | `<saf-text-field type="email">` | Email validation built-in |
| `<textarea>` | `<saf-text-area>` | Multi-line text input |
| `<select>` | `<saf-select>` | Dropdown selection |
| `<input type="checkbox">` | `<saf-checkbox>` | Single checkbox |
| `<input type="radio">` | `<saf-radio-button>` | Use within `<saf-radio-group>` |
| `<input type="date">` | `<saf-date-picker>` | Date selection with calendar |
| `<input type="time">` | `<saf-time-picker>` | Time selection |
| `<input type="file">` | `<saf-file-upload>` | File upload with drag-and-drop |
| `<input type="range">` | `<saf-slider>` | Range slider |
| `<input type="search">` | `<saf-search>` | Search with suggestions |

### Buttons & Actions
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<button>` | `<saf-button>` | Primary, secondary, ghost variants |
| `<a>` (as button) | `<saf-button>` | Use `appearance` prop for style |
| `<button>` (icon only) | `<saf-icon-button>` | Icon-only action button |
| `<button>` (toggle) | `<saf-toggle-button>` | On/off toggle |
| `<button>` (split) | `<saf-split-button>` | Button with dropdown actions |

### Layout & Containers
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<div>` (card) | `<saf-card>` | Content card with header/body/footer |
| `<div>` (panel) | `<saf-panel>` | Collapsible panel |
| `<div>` (dialog) | `<saf-dialog>` | Modal dialog |
| `<div>` (drawer) | `<saf-drawer>` | Side drawer/panel |
| `<div>` (accordion) | `<saf-accordion>` | Expandable sections |
| `<div>` (tabs) | `<saf-tab-strip>` | Tabbed content |
| `<div>` (toolbar) | `<saf-toolbar>` | Action toolbar |
| `<div>` (tooltip) | `<saf-tooltip>` | Hover tooltip |
| `<div>` (popover) | `<saf-popover>` | Click popover |

### Navigation
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<nav>` | `<saf-navigation>` | Main navigation |
| `<ul>` (menu) | `<saf-menu>` | Dropdown/context menu |
| `<ol>` (breadcrumb) | `<saf-breadcrumb>` | Breadcrumb navigation |
| `<ul>` (stepper) | `<saf-stepper>` | Multi-step wizard |
| `<a>` | `<saf-link>` | Styled hyperlink |
| `<ul>` (pagination) | `<saf-pager>` | Pagination controls |

### Data Display
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<table>` | `<saf-grid>` | Data grid with sorting/filtering |
| `<ul>`/`<ol>` | `<saf-list>` | Styled list |
| `<ul>` (tree) | `<saf-tree-view>` | Hierarchical tree |
| `<span>` (badge) | `<saf-badge>` | Status badge/counter |
| `<span>` (chip) | `<saf-chip>` | Tag/chip element |
| `<span>` (tag) | `<saf-tag>` | Categorization tag |
| `<img>` (avatar) | `<saf-avatar>` | User avatar |
| `<progress>` | `<saf-progress-bar>` | Progress indicator |
| `<div>` (spinner) | `<saf-loader>` | Loading spinner |

### Feedback & Notifications
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<div>` (alert) | `<saf-alert>` | Inline alert message |
| `<div>` (banner) | `<saf-banner>` | Page-level banner |
| `<div>` (toast) | `<saf-notification>` | Toast notification |
| `<div>` (snackbar) | `<saf-snackbar>` | Brief feedback message |

### Typography & Content
| HTML Element | Saffron Component | Notes |
|---|---|---|
| `<label>` | `<saf-label>` | Form label |
| `<span>` (icon) | `<saf-icon>` | Icon from Saffron icon set |
| `<hr>` | `<saf-divider>` | Content divider |

## Component Groupings (Common Patterns)

### Form Pattern
```html
<saf-card>
  <saf-label>Field Label</saf-label>
  <saf-text-field placeholder="Enter value"></saf-text-field>
  <saf-select>
    <saf-option value="1">Option 1</saf-option>
  </saf-select>
  <saf-button appearance="primary">Submit</saf-button>
</saf-card>
```

### Data Table Pattern
```html
<saf-card>
  <saf-toolbar>
    <saf-search></saf-search>
    <saf-button>Add New</saf-button>
  </saf-toolbar>
  <saf-grid [data]="gridData">
    <!-- column definitions -->
  </saf-grid>
  <saf-pager></saf-pager>
</saf-card>
```

### Dialog Pattern
```html
<saf-dialog [opened]="isOpen">
  <saf-dialog-titlebar>Title</saf-dialog-titlebar>
  <div class="dialog-content">
    <!-- content -->
  </div>
  <saf-dialog-actions>
    <saf-button appearance="secondary">Cancel</saf-button>
    <saf-button appearance="primary">Confirm</saf-button>
  </saf-dialog-actions>
</saf-dialog>
```

## MCP Server Integration
Use the Saffron MCP server tools to get accurate, up-to-date component information:
- `get-saffron-code-equivalent` - Map HTML elements to Saffron components
- `get-saffron-code` - Get complete component code with imports
- `get-saffron-a11y-attributes` - Get accessibility attributes
- `get-saffron-tokens` - Map CSS values to design tokens
- `get-saffron-image` - Get visual screenshots of components

**Always verify component names and APIs with the MCP server before generating code.**
