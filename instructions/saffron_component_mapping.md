# Saffron Design System - Complete Component Mapping Guide

## Overview

This comprehensive guide maps ALL 117+ Saffron Design System components to their corresponding HTML patterns, providing a complete reference for consistent design system usage. Use this to identify the correct Saffron component for any UI pattern and avoid creating custom HTML when Saffron alternatives exist.

---

## 🚀 Quick Component Finder

| Need to... | Use This Component | Replace This HTML |
|------------|-------------------|-------------------|
| Display any text | `<saf-text>` | `<p>`, `<h1-h6>`, `<span>` |
| Create a button | `<saf-button>` | `<button>`, `<a>` (for actions) |
| Show a modal | `<saf-dialog>` | `<div class="modal">` |
| Create a card/panel | `<saf-card>` | `<div class="card">` |
| Display icons | `<saf-icon>` | `<i class="fa-*">`, SVGs |
| Show tags/badges | `<saf-chip>` | `<span class="badge">` |
| Display messages | `<saf-alert>` | `<div class="alert">` |
| Input text | `<saf-text-field>` | `<input type="text">` |
| Select dates | `<saf-date-picker>` | Custom date inputs |
| Show data tables | `<saf-data-grid>` | `<table>` |
| Create navigation | `<saf-navigation>` | Custom nav menus |
| Build forms | `<saf-form>` | `<form>` with custom validation |
| Show progress | `<saf-progress>` | Custom progress bars |
| Create tooltips | `<saf-tooltip>` | Custom tooltip divs |

---

## 📚 Complete Component Categories

### 🎨 **Typography & Text Display**

#### SafText - Universal Text Component
**Replaces:** `<p>`, `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`, `<span>`, `<div>` (for text), `<label>`

```html
<!-- ❌ DON'T -->
<h1>Page Title</h1>
<h2>Section Header</h2>
<p>Body content</p>
<span class="caption">Small text</span>
<label>Form label</label>

<!-- ✅ DO -->
<saf-text appearance="heading-4xl">Page Title</saf-text>
<saf-text appearance="heading-lg">Section Header</saf-text>
<saf-text appearance="body-default-md">Body content</saf-text>
<saf-text appearance="body-default-xs">Small text</saf-text>
<saf-text appearance="body-strong-sm">Form label</saf-text>
```

**Text Hierarchy:**
- `display-lg/sm` - Hero banners, marketing headers
- `heading-4xl/3xl/2xl/xl/lg/md` - Page/section titles (h1-h6 equivalent)
- `body-default-lg/md/sm/xs` - Regular content (p equivalent)
- `body-strong-lg/md/sm/xs` - Emphasized content (bold equivalent)
- `eyebrow-heavy-md/sm` - Overlines, category labels

---

### 🎯 **Interactive Controls**

#### SafButton - All Button Interactions
**Replaces:** `<button>`, `<input type="submit">`, `<input type="button">`, `<a>` (for actions)

```html
<!-- ❌ DON'T -->
<button type="submit" class="btn btn-primary">Save</button>
<button type="button" class="btn btn-secondary">Cancel</button>
<a href="#" onclick="action()">Link Action</a>
<input type="submit" value="Submit">

<!-- ✅ DO -->
<saf-button type="submit" appearance="primary">Save</saf-button>
<saf-button appearance="secondary" (click)="cancel()">Cancel</saf-button>
<saf-button appearance="tertiary" (click)="action()">Link Action</saf-button>
<saf-button type="submit" appearance="primary">Submit</saf-button>
```

**Button Types:**
- `primary` - Main actions (save, create, submit)
- `secondary` - Secondary actions (cancel, back)
- `tertiary` - Subtle actions (edit, delete, links)
- `inline` - Text-like actions within content

#### SafButtonGroup - Button Collections
**Replaces:** `<div class="btn-group">`, button toolbars

```html
<!-- ❌ DON'T -->
<div class="btn-group">
  <button class="btn">Left</button>
  <button class="btn active">Center</button>
  <button class="btn">Right</button>
</div>

<!-- ✅ DO -->
<saf-button-group>
  <saf-button>Left</saf-button>
  <saf-button pressed="true">Center</saf-button>
  <saf-button>Right</saf-button>
</saf-button-group>
```

---

### 📋 **Form Controls**

#### SafTextField - Text Input
**Replaces:** `<input type="text">`, `<input type="email">`, `<input type="password">`, `<input type="search">`

```html
<!-- ❌ DON'T -->
<input type="text" placeholder="Enter name" required>
<input type="email" id="email" class="form-control">
<input type="password" autocomplete="current-password">

<!-- ✅ DO -->
<saf-text-field placeholder="Enter name" required></saf-text-field>
<saf-text-field type="email" id="email"></saf-text-field>
<saf-text-field type="password" autocomplete="current-password"></saf-text-field>
```

#### SafTextArea - Multi-line Input
**Replaces:** `<textarea>`

```html
<!-- ❌ DON'T -->
<textarea rows="4" placeholder="Enter description"></textarea>

<!-- ✅ DO -->
<saf-text-area rows="4" placeholder="Enter description"></saf-text-area>
```

#### SafSelect - Dropdown Selection
**Replaces:** `<select>`, custom dropdown implementations

```html
<!-- ❌ DON'T -->
<select name="country">
  <option value="us">United States</option>
  <option value="ca">Canada</option>
</select>

<!-- ✅ DO -->
<saf-select name="country">
  <saf-option value="us">United States</saf-option>
  <saf-option value="ca">Canada</saf-option>
</saf-select>
```

#### SafCheckbox - Boolean Selection
**Replaces:** `<input type="checkbox">`

```html
<!-- ❌ DON'T -->
<input type="checkbox" id="agree" name="agree">
<label for="agree">I agree to terms</label>

<!-- ✅ DO -->
<saf-checkbox id="agree" name="agree">I agree to terms</saf-checkbox>
```

#### SafRadio & SafRadioGroup - Exclusive Selection
**Replaces:** `<input type="radio">` groups

```html
<!-- ❌ DON'T -->
<input type="radio" name="size" value="small" id="small">
<label for="small">Small</label>
<input type="radio" name="size" value="large" id="large">
<label for="large">Large</label>

<!-- ✅ DO -->
<saf-radio-group name="size">
  <saf-radio value="small">Small</saf-radio>
  <saf-radio value="large">Large</saf-radio>
</saf-radio-group>
```

#### SafSwitch - Toggle Control
**Replaces:** Toggle switches, `<input type="checkbox">` (for on/off states)

```html
<!-- ❌ DON'T -->
<input type="checkbox" class="toggle" id="notifications">
<label for="notifications">Enable notifications</label>

<!-- ✅ DO -->
<saf-switch id="notifications">Enable notifications</saf-switch>
```

#### SafDatePicker - Date Selection
**Replaces:** `<input type="date">`, custom date inputs

```html
<!-- ❌ DON'T -->
<input type="date" name="birthdate">

<!-- ✅ DO -->
<saf-date-picker name="birthdate" format="MM/DD/YYYY"></saf-date-picker>
```

#### SafNumberField - Numeric Input
**Replaces:** `<input type="number">`

```html
<!-- ❌ DON'T -->
<input type="number" min="0" max="100" step="1">

<!-- ✅ DO -->
<saf-number-field min="0" max="100" step="1"></saf-number-field>
```

#### SafSlider - Range Selection
**Replaces:** `<input type="range">`, custom sliders

```html
<!-- ❌ DON'T -->
<input type="range" min="0" max="100" value="50">

<!-- ✅ DO -->
<saf-slider min="0" max="100" value="50"></saf-slider>
```

#### SafCombobox - Searchable Selection
**Replaces:** `<select>` with search, custom autocomplete

```html
<!-- ❌ DON'T -->
<input type="text" list="countries">
<datalist id="countries">
  <option value="United States">
  <option value="Canada">
</datalist>

<!-- ✅ DO -->
<saf-combobox>
  <saf-combobox-option value="us">United States</saf-combobox-option>
  <saf-combobox-option value="ca">Canada</saf-combobox-option>
</saf-combobox>
```

#### SafForm - Complete Form Management
**Replaces:** `<form>` with custom validation, form builders

```html
<!-- ❌ DON'T -->
<form onsubmit="handleSubmit()">
  <div class="form-group">
    <label>Name:</label>
    <input type="text" required>
    <div class="error-message"></div>
  </div>
  <button type="submit">Submit</button>
</form>

<!-- ✅ DO -->
<saf-form (submit)="handleSubmit($event)" [validation-schema]="schema">
  <saf-text-field name="name" label="Name" required></saf-text-field>
  <saf-button type="submit" slot="actions">Submit</saf-button>
</saf-form>
```

#### SafFileUpload - File Upload Control
**Replaces:** `<input type="file">`, custom file upload implementations

```html
<!-- ❌ DON'T -->
<input type="file" accept=".pdf,.doc" multiple>
<div class="upload-progress" style="display:none;">
  <div class="progress-bar"></div>
</div>

<!-- ✅ DO -->
<saf-file-upload 
  accept=".pdf,.doc" 
  multiple 
  [progress-value]="uploadProgress"
  status="info">
</saf-file-upload>
```

---

### 🗂️ **Data Display**

#### SafDataGrid - Advanced Data Tables
**Replaces:** `<table>`, custom data grids, spreadsheet-like components

```html
<!-- ❌ DON'T -->
<table class="data-table sortable">
  <thead>
    <tr>
      <th data-sort="name">Name</th>
      <th data-sort="email">Email</th>
    </tr>
  </thead>
  <tbody>
    <!-- rows -->
  </tbody>
</table>

<!-- ✅ DO -->
<saf-data-grid 
  [data]="users" 
  [columns]="columns" 
  sortable 
  filterable 
  [pagination]="true">
</saf-data-grid>
```

#### SafTable - Simple Data Tables
**Replaces:** Basic `<table>` implementations

```html
<!-- ❌ DON'T -->
<table>
  <thead>
    <tr><th>Name</th><th>Value</th></tr>
  </thead>
  <tbody>
    <tr><td>Item 1</td><td>100</td></tr>
  </tbody>
</table>

<!-- ✅ DO -->
<saf-table>
  <saf-table-header>
    <saf-table-header-cell>Name</saf-table-header-cell>
    <saf-table-header-cell>Value</saf-table-header-cell>
  </saf-table-header>
  <saf-table-body>
    <saf-table-row>
      <saf-table-cell>Item 1</saf-table-cell>
      <saf-table-cell>100</saf-table-cell>
    </saf-table-row>
  </saf-table-body>
</saf-table>
```

#### SafList - Structured Lists
**Replaces:** `<ul>`, `<ol>`, `<dl>`, custom list implementations

```html
<!-- ❌ DON'T -->
<ul class="item-list">
  <li class="item">
    <span class="title">Item 1</span>
    <span class="description">Description</span>
  </li>
</ul>

<!-- ✅ DO -->
<saf-list>
  <saf-list-item>
    <saf-text slot="title">Item 1</saf-text>
    <saf-text slot="description">Description</saf-text>
  </saf-list-item>
</saf-list>
```

#### SafMetadata - Key-Value Pairs
**Replaces:** `<dl>`, custom metadata displays

```html
<!-- ❌ DON'T -->
<dl class="metadata">
  <dt>Created:</dt>
  <dd>2024-01-15</dd>
  <dt>Status:</dt>
  <dd>Active</dd>
</dl>

<!-- ✅ DO -->
<saf-metadata>
  <saf-metadata-item label="Created" value="2024-01-15"></saf-metadata-item>
  <saf-metadata-item label="Status" value="Active"></saf-metadata-item>
</saf-metadata>
```

---

### 🔔 **Feedback & Status**

#### SafAlert - Messages & Notifications
**Replaces:** `<div class="alert">`, `<div class="notification">`, toast messages

```html
<!-- ❌ DON'T -->
<div class="alert alert-success">
  <i class="fa fa-check"></i>
  Success message
</div>
<div class="alert alert-error">
  <i class="fa fa-times"></i>
  Error occurred
</div>

<!-- ✅ DO -->
<saf-alert appearance="success" alert-type="inline">
  <saf-icon slot="icon" name="action/check"></saf-icon>
  Success message
</saf-alert>
<saf-alert appearance="error" alert-type="inline">
  <saf-icon slot="icon" name="action/times"></saf-icon>
  Error occurred
</saf-alert>
```

#### SafToast - Temporary Notifications
**Replaces:** Custom toast/snackbar implementations

```html
<!-- ❌ DON'T -->
<div class="toast" style="position: fixed; top: 20px;">
  Message sent successfully!
</div>

<!-- ✅ DO -->
<saf-toast 
  message="Message sent successfully!" 
  duration="3000" 
  appearance="success">
</saf-toast>
```

#### SafProgress - Progress Indicators
**Replaces:** `<progress>`, custom progress bars

```html
<!-- ❌ DON'T -->
<progress value="32" max="100">32%</progress>
<div class="progress">
  <div class="progress-bar" style="width: 32%"></div>
</div>

<!-- ✅ DO -->
<saf-progress value="32" max="100"></saf-progress>
```

#### SafProgressRing - Circular Progress
**Replaces:** Custom circular progress indicators

```html
<!-- ❌ DON'T -->
<div class="spinner">
  <div class="circle"></div>
</div>

<!-- ✅ DO -->
<saf-progress-ring value="75"></saf-progress-ring>
```

#### SafBadge - Status Indicators
**Replaces:** `<span class="badge">`, notification dots

```html
<!-- ❌ DON'T -->
<span class="badge badge-primary">3</span>
<span class="status-dot active"></span>

<!-- ✅ DO -->
<saf-badge>3</saf-badge>
<saf-badge appearance="dot" status="active"></saf-badge>
```

#### SafStatus - Status Display
**Replaces:** Custom status indicators

```html
<!-- ❌ DON'T -->
<span class="status status-active">
  <i class="status-icon"></i>
  Active
</span>

<!-- ✅ DO -->
<saf-status state="active">Active</saf-status>
```

---

### 🏷️ **Labels & Tags**

#### SafChip - Tags, Pills, Badges
**Replaces:** `<span class="tag">`, `<span class="pill">`, `<span class="badge">`

```html
<!-- ❌ DON'T -->
<span class="tag tag-removable">
  High Priority
  <button class="remove">×</button>
</span>
<span class="pill">Category</span>

<!-- ✅ DO -->
<saf-chip type="closable-with-icon" (remove)="onRemove()">
  <saf-icon slot="startSlot" name="action/flag"></saf-icon>
  High Priority
</saf-chip>
<saf-chip type="basic">Category</saf-chip>
```

#### SafFilterChip - Filter Tags
**Replaces:** Filter badges, toggle chips

```html
<!-- ❌ DON'T -->
<div class="filter-chips">
  <span class="filter active" data-filter="active">Active</span>
  <span class="filter" data-filter="completed">Completed</span>
</div>

<!-- ✅ DO -->
<saf-filter-group>
  <saf-filter-chip active="true" value="active">Active</saf-filter-chip>
  <saf-filter-chip value="completed">Completed</saf-filter-chip>
</saf-filter-group>
```

---

### 🎭 **Visual Elements**

#### SafIcon - All Icons
**Replaces:** `<i class="fa-*">`, `<svg>`, custom icon implementations

```html
<!-- ❌ DON'T -->
<i class="fa fa-home"></i>
<i class="fas fa-star"></i>
<svg class="icon">...</svg>

<!-- ✅ DO -->
<saf-icon name="action/home"></saf-icon>
<saf-icon name="action/star" appearance="solid"></saf-icon>
```

#### SafAvatar - User Profile Images
**Replaces:** Custom profile picture implementations

```html
<!-- ❌ DON'T -->
<div class="avatar">
  <img src="user.jpg" alt="John Doe">
</div>
<div class="avatar-initials">JD</div>

<!-- ✅ DO -->
<saf-avatar src="user.jpg" alt="John Doe"></saf-avatar>
<saf-avatar initials="JD"></saf-avatar>
```

#### SafLogo - Brand Logos
**Replaces:** Custom logo implementations

```html
<!-- ❌ DON'T -->
<div class="logo">
  <img src="logo.svg" alt="Company">
</div>

<!-- ✅ DO -->
<saf-logo src="logo.svg" alt="Company"></saf-logo>
```

#### SafDivider - Section Separators
**Replaces:** `<hr>`, custom divider lines

```html
<!-- ❌ DON'T -->
<hr>
<div class="divider"></div>

<!-- ✅ DO -->
<saf-divider></saf-divider>
```

---

### 📦 **Layout & Containers**

#### SafDialog - Modal Dialogs
**Replaces:** `<div class="modal">`, custom popup implementations

```html
<!-- ❌ DON'T -->
<div class="modal-overlay" *ngIf="showModal">
  <div class="modal">
    <div class="modal-header">
      <h2>Title</h2>
      <button class="close">×</button>
    </div>
    <div class="modal-body">Content</div>
    <div class="modal-footer">
      <button>Cancel</button>
      <button>OK</button>
    </div>
  </div>
</div>

<!-- ✅ DO -->
<saf-dialog 
  *ngIf="showModal"
  [open]="showModal"
  dialog-title="Title"
  (closeDialog)="onClose()">
  
  <div slot="content">Content</div>
  
  <div slot="footer">
    <saf-button appearance="secondary">Cancel</saf-button>
    <saf-button appearance="primary">OK</saf-button>
  </div>
</saf-dialog>
```

#### SafCard - Content Containers
**Replaces:** `<div class="card">`, `<section>`, `<article>`

```html
<!-- ❌ DON'T -->
<div class="card">
  <div class="card-header">
    <h3>Card Title</h3>
  </div>
  <div class="card-body">
    <p>Content goes here</p>
  </div>
  <div class="card-footer">
    <button>Action</button>
  </div>
</div>

<!-- ✅ DO -->
<saf-card appearance="vertical" density="comfortable">
  <saf-text slot="header" appearance="heading-md">Card Title</saf-text>
  <saf-text slot="content" appearance="body-default-md">Content goes here</saf-text>
  <div slot="actions">
    <saf-button appearance="primary">Action</saf-button>
  </div>
</saf-card>
```

#### SafContainer - Layout Wrapper
**Replaces:** `<div class="container">`, wrapper divs

```html
<!-- ❌ DON'T -->
<div class="container">
  <div class="row">
    <div class="col">Content</div>
  </div>
</div>

<!-- ✅ DO -->
<saf-container max-width="lg">
  <saf-layout-grid>
    <saf-layout-grid-item>Content</saf-layout-grid-item>
  </saf-layout-grid>
</saf-container>
```

#### SafLayoutGrid - Grid Layouts
**Replaces:** CSS Grid, Flexbox layouts, Bootstrap grid

```html
<!-- ❌ DON'T -->
<div class="row">
  <div class="col-md-6">Left</div>
  <div class="col-md-6">Right</div>
</div>

<!-- ✅ DO -->
<saf-layout-grid>
  <saf-layout-grid-item span="6">Left</saf-layout-grid-item>
  <saf-layout-grid-item span="6">Right</saf-layout-grid-item>
</saf-layout-grid>
```

#### SafDrawer - Side Panels
**Replaces:** Custom sidebar implementations

```html
<!-- ❌ DON'T -->
<div class="sidebar" [class.open]="sidebarOpen">
  <div class="sidebar-content">
    Navigation items
  </div>
</div>

<!-- ✅ DO -->
<saf-drawer [open]="sidebarOpen" position="left">
  Navigation items
</saf-drawer>
```

---

### 🧭 **Navigation**

#### SafNavigation - Navigation Menus
**Replaces:** `<nav>`, custom navigation implementations

```html
<!-- ❌ DON'T -->
<nav class="main-nav">
  <ul>
    <li><a href="/home">Home</a></li>
    <li><a href="/about">About</a></li>
    <li class="dropdown">
      <a href="/products">Products</a>
      <ul class="submenu">
        <li><a href="/product-a">Product A</a></li>
      </ul>
    </li>
  </ul>
</nav>

<!-- ✅ DO -->
<saf-navigation [items]="navigationItems" variant="primary">
</saf-navigation>
```

#### SafBreadcrumb - Navigation Paths
**Replaces:** Custom breadcrumb implementations

```html
<!-- ❌ DON'T -->
<nav class="breadcrumb">
  <a href="/home">Home</a>
  <span class="separator">/</span>
  <a href="/products">Products</a>
  <span class="separator">/</span>
  <span class="current">Current Page</span>
</nav>

<!-- ✅ DO -->
<saf-breadcrumb>
  <saf-breadcrumb-item href="/home">Home</saf-breadcrumb-item>
  <saf-breadcrumb-item href="/products">Products</saf-breadcrumb-item>
  <saf-breadcrumb-item>Current Page</saf-breadcrumb-item>
</saf-breadcrumb>
```

#### SafMenu - Dropdown Menus
**Replaces:** Custom dropdown implementations

```html
<!-- ❌ DON'T -->
<div class="dropdown">
  <button class="dropdown-toggle">Menu</button>
  <ul class="dropdown-menu">
    <li><a href="#">Action 1</a></li>
    <li><a href="#">Action 2</a></li>
  </ul>
</div>

<!-- ✅ DO -->
<saf-menu>
  <saf-button slot="trigger">Menu</saf-button>
  <saf-menu-item>Action 1</saf-menu-item>
  <saf-menu-item>Action 2</saf-menu-item>
</saf-menu>
```

#### SafContextMenu - Right-Click Menus
**Replaces:** Custom context menu implementations

```html
<!-- ❌ DON'T -->
<div oncontextmenu="showContextMenu(event)">
  Right-click me
</div>
<div class="context-menu" style="display: none;">
  <div class="menu-item">Copy</div>
  <div class="menu-item">Paste</div>
</div>

<!-- ✅ DO -->
<div>
  Right-click me
  <saf-context-menu [items]="contextMenuItems">
  </saf-context-menu>
</div>
```

#### SafTabs - Tab Navigation
**Replaces:** Custom tab implementations

```html
<!-- ❌ DON'T -->
<div class="tabs">
  <div class="tab-list">
    <button class="tab active">Tab 1</button>
    <button class="tab">Tab 2</button>
  </div>
  <div class="tab-content">
    <div class="tab-panel active">Panel 1</div>
    <div class="tab-panel">Panel 2</div>
  </div>
</div>

<!-- ✅ DO -->
<saf-tabs>
  <saf-tab id="tab1">Tab 1</saf-tab>
  <saf-tab id="tab2">Tab 2</saf-tab>
  <saf-tab-panel id="panel1">Panel 1</saf-tab-panel>
  <saf-tab-panel id="panel2">Panel 2</saf-tab-panel>
</saf-tabs>
```

---

### 📅 **Date & Time**

#### SafCalendar - Calendar Display
**Replaces:** Custom calendar implementations

```html
<!-- ❌ DON'T -->
<div class="calendar">
  <div class="calendar-header">
    <button class="prev">‹</button>
    <span class="month-year">January 2024</span>
    <button class="next">›</button>
  </div>
  <div class="calendar-grid">
    <!-- date cells -->
  </div>
</div>

<!-- ✅ DO -->
<saf-calendar 
  [selected-date]="selectedDate"
  (date-select)="onDateSelect($event)">
</saf-calendar>
```

---

### 🔧 **Specialized Components**

#### SafWizard - Multi-Step Processes
**Replaces:** Custom step-by-step implementations

```html
<!-- ❌ DON'T -->
<div class="wizard">
  <div class="steps">
    <div class="step active">Step 1</div>
    <div class="step">Step 2</div>
  </div>
  <div class="step-content">
    <!-- Current step content -->
  </div>
  <div class="step-actions">
    <button>Previous</button>
    <button>Next</button>
  </div>
</div>

<!-- ✅ DO -->
<saf-wizard [steps]="wizardSteps">
  <saf-wizard-step-content step="1">
    Step 1 content
  </saf-wizard-step-content>
  <saf-wizard-step-content step="2">
    Step 2 content
  </saf-wizard-step-content>
</saf-wizard>
```

#### SafStepper - Progress Steps
**Replaces:** Custom step indicators

```html
<!-- ❌ DON'T -->
<div class="stepper">
  <div class="step completed">
    <span class="step-number">1</span>
    <span class="step-label">Completed</span>
  </div>
  <div class="step active">
    <span class="step-number">2</span>
    <span class="step-label">Current</span>
  </div>
</div>

<!-- ✅ DO -->
<saf-stepper [steps]="steps" [current-step]="currentStep">
</saf-stepper>
```

#### SafAccordion - Collapsible Sections
**Replaces:** Custom accordion implementations

```html
<!-- ❌ DON'T -->
<div class="accordion">
  <div class="accordion-item">
    <button class="accordion-header">Section 1</button>
    <div class="accordion-content">Content 1</div>
  </div>
  <div class="accordion-item">
    <button class="accordion-header">Section 2</button>
    <div class="accordion-content">Content 2</div>
  </div>
</div>

<!-- ✅ DO -->
<saf-accordion>
  <saf-accordion-item>
    <saf-text slot="header">Section 1</saf-text>
    <div slot="content">Content 1</div>
  </saf-accordion-item>
  <saf-accordion-item>
    <saf-text slot="header">Section 2</saf-text>
    <div slot="content">Content 2</div>
  </saf-accordion-item>
</saf-accordion>
```

#### SafTimeline - Event Sequences
**Replaces:** Custom timeline implementations

```html
<!-- ❌ DON'T -->
<div class="timeline">
  <div class="timeline-item">
    <div class="timeline-marker"></div>
    <div class="timeline-content">
      <h4>Event 1</h4>
      <p>Description</p>
    </div>
  </div>
</div>

<!-- ✅ DO -->
<saf-timeline [items]="timelineItems">
</saf-timeline>
```

#### SafCarousel - Image/Content Sliders
**Replaces:** Custom slider/carousel implementations

```html
<!-- ❌ DON'T -->
<div class="carousel">
  <div class="slides">
    <div class="slide active">Slide 1</div>
    <div class="slide">Slide 2</div>
  </div>
  <button class="prev">‹</button>
  <button class="next">›</button>
</div>

<!-- ✅ DO -->
<saf-carousel [slides]="slides" auto-play="true">
</saf-carousel>
```

---

### 🔍 **Search & Filtering**

#### SafSearchField - Search Input
**Replaces:** `<input type="search">`, custom search implementations

```html
<!-- ❌ DON'T -->
<div class="search-box">
  <input type="search" placeholder="Search...">
  <button class="search-btn">🔍</button>
</div>

<!-- ✅ DO -->
<saf-search-field placeholder="Search..." (search)="onSearch($event)">
</saf-search-field>
```

#### SafFacetedFilter - Advanced Filtering
**Replaces:** Custom filter interfaces

```html
<!-- ❌ DON'T -->
<div class="filters">
  <div class="filter-group">
    <label>Category</label>
    <select multiple>
      <option>Category 1</option>
    </select>
  </div>
</div>

<!-- ✅ DO -->
<saf-faceted-filter [facets]="filterFacets" (change)="onFilterChange($event)">
</saf-faceted-filter>
```

---

### 💡 **Utility Components**

#### SafTooltip - Hover Information
**Replaces:** Custom tooltip implementations

```html
<!-- ❌ DON'T -->
<span class="tooltip-trigger" title="Tooltip text">
  Hover me
</span>

<!-- ✅ DO -->
<saf-tooltip content="Tooltip text">
  <span>Hover me</span>
</saf-tooltip>
```

#### SafSkipLink - Accessibility Navigation
**Replaces:** Custom skip link implementations

```html
<!-- ❌ DON'T -->
<a href="#main" class="skip-link">Skip to main content</a>

<!-- ✅ DO -->
<saf-skip-link href="#main">Skip to main content</saf-skip-link>
```

#### SafSrOnly - Screen Reader Only Content
**Replaces:** `.sr-only`, `.visually-hidden` classes

```html
<!-- ❌ DON'T -->
<span class="sr-only">Screen reader only text</span>

<!-- ✅ DO -->
<saf-sr-only>Screen reader only text</saf-sr-only>
```

#### SafInfiniteScroll - Infinite Loading
**Replaces:** Custom infinite scroll implementations

```html
<!-- ❌ DON'T -->
<div class="content" onscroll="checkScroll()">
  <!-- items -->
</div>

<!-- ✅ DO -->
<saf-infinite-scroll (loadMore)="loadMoreItems()">
  <!-- items -->
</saf-infinite-scroll>
```

---

## 🚫 **Critical Anti-Patterns to Avoid**

### ❌ Never Use These When Saffron Exists

```html
<!-- DON'T - Use saf-text instead -->
<p>Any text content</p>
<h1>Headings</h1>
<span>Labels</span>

<!-- DON'T - Use saf-button instead -->
<button>Any button</button>
<a onclick="action()">Action links</a>

<!-- DON'T - Use saf-dialog instead -->
<div class="modal">Custom modals</div>

<!-- DON'T - Use saf-icon instead -->
<i class="fa fa-icon"></i>
<svg>Custom icons</svg>

<!-- DON'T - Use saf-card instead -->
<div class="card">Content containers</div>

<!-- DON'T - Use saf-alert instead -->
<div class="alert">Messages</div>

<!-- DON'T - Use form components instead -->
<input type="text">
<select></select>
<textarea></textarea>

<!-- DON'T - Use saf-chip instead -->
<span class="badge">Tags</span>
<span class="tag">Labels</span>

<!-- DON'T - Use saf-table/saf-data-grid instead -->
<table>Data tables</table>
```

---

## ✅ **Component Selection Decision Tree**

### 1. **Need to display text?**
→ Always use `<saf-text>` with appropriate `appearance`

### 2. **Need user interaction?**
- **Button/action** → `<saf-button>`
- **Form input** → `<saf-text-field>`, `<saf-text-area>`, `<saf-select>`, etc.
- **Selection** → `<saf-checkbox>`, `<saf-radio>`, `<saf-chip>` (filters)

### 3. **Need layout/container?**
- **Modal/popup** → `<saf-dialog>`
- **Content card** → `<saf-card>`
- **Grid layout** → `<saf-layout-grid>`
- **Side panel** → `<saf-drawer>`

### 4. **Need data display?**
- **Simple table** → `<saf-table>`
- **Advanced table** → `<saf-data-grid>`
- **Lists** → `<saf-list>`
- **Key-value pairs** → `<saf-metadata>`

### 5. **Need feedback/status?**
- **Messages** → `<saf-alert>`
- **Progress** → `<saf-progress>`, `<saf-progress-ring>`
- **Status** → `<saf-status>`, `<saf-badge>`
- **Notifications** → `<saf-toast>`

### 6. **Need navigation?**
- **Main navigation** → `<saf-navigation>`
- **Breadcrumbs** → `<saf-breadcrumb>`
- **Tabs** → `<saf-tabs>`
- **Menus** → `<saf-menu>`, `<saf-context-menu>`

### 7. **Need specialized functionality?**
- **Multi-step process** → `<saf-wizard>`
- **Date selection** → `<saf-date-picker>`, `<saf-calendar>`
- **File upload** → `<saf-file-upload>`
- **Search** → `<saf-search-field>`

---

## 📋 **Implementation Checklist**

When creating any new component, verify:

- [ ] **Text content** uses `<saf-text>` with proper `appearance`
- [ ] **Interactive elements** use appropriate Saffron components
- [ ] **Icons** use `<saf-icon>` instead of FontAwesome classes
- [ ] **Containers** use `<saf-card>`, `<saf-dialog>`, or layout components
- [ ] **Form elements** use Saffron form components
- [ ] **Messages/feedback** use `<saf-alert>` or status components
- [ ] **Navigation** uses Saffron navigation components
- [ ] **Data display** uses `<saf-table>` or `<saf-data-grid>`
- [ ] **No generic divs** are used where Saffron components exist
- [ ] **ARIA labels** included for accessibility
- [ ] **Density attributes** used for consistent spacing
- [ ] **Proper semantic structure** maintained

---

## 🔍 **Quick Search Index**

**A-D:** Avatar, Alert, Accordion, Badge, Button, Breadcrumb, Calendar, Card, Carousel, Checkbox, Chip, Combobox, Container, ContextMenu, DataGrid, DatePicker, Dialog, Divider

**E-L:** FileUpload, Form, Icon, InfiniteScroll, Layout, List

**M-P:** Menu, Metadata, Navigation, NumberField, Progress, Picker

**R-S:** Radio, SearchField, Select, Slider, Status, Stepper, Switch

**T-Z:** Table, Tabs, Text, TextArea, TextField, Timeline, Toast, Tooltip, Wizard

---

## 🎯 **Key Principles**

1. **Text First:** Every piece of text should use `<saf-text>`
2. **Interaction Second:** Every user action should use appropriate Saffron components
3. **Layout Third:** Use Saffron containers instead of generic divs
4. **No Reinventing:** Check this guide before creating custom implementations
5. **Accessibility Always:** Include proper ARIA labels and semantic structure
6. **Consistency Everywhere:** Use Saffron components for visual consistency

**Remember:** When in doubt, search this guide or check the Saffron documentation. There's likely a component for your use case!
