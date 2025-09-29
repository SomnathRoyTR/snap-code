# SafDivider Component

The **SafDivider** component provides visual separation between content sections with horizontal or vertical orientations. It implements proper ARIA separator semantics and supports both decorative and semantic separation modes.

## Basic Usage

```html
<!-- Basic horizontal divider -->
<saf-divider></saf-divider>

<!-- Vertical divider -->
<saf-divider orientation="vertical"></saf-divider>

<!-- Presentational divider (decorative only) -->
<saf-divider role="presentation"></saf-divider>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `role` | `'separator' \| 'presentation'` | `'separator'` | ARIA role defining the divider's semantic meaning |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Visual orientation of the divider |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `role` | `DividerRole` | `'separator'` | Current ARIA role |
| `orientation` | `DividerOrientation` | `'horizontal'` | Current orientation |

### CSS Parts

| Part | Description |
|------|-------------|
| `divider` | Main divider element |

## Orientation Options

| Orientation | Description | Typical Use Case |
|-------------|-------------|------------------|
| `'horizontal'` | Spans width, separates vertically stacked content | Section separators, list item dividers |
| `'vertical'` | Spans height, separates horizontally arranged content | Sidebar separators, toolbar dividers |

## Role Options

| Role | Description | Screen Reader Behavior |
|------|-------------|----------------------|
| `'separator'` | Semantic separator | Announced as "separator" |
| `'presentation'` | Decorative only | Ignored by screen readers |

## Comprehensive Examples

### Basic Dividers

```html
<div class="divider-examples">
  <h3>Basic Dividers</h3>
  
  <div class="horizontal-example">
    <h4>Horizontal Dividers</h4>
    <div class="content-section">
      <p>This is the first section of content that needs to be separated from the next section.</p>
    </div>
    
    <saf-divider></saf-divider>
    
    <div class="content-section">
      <p>This is the second section of content, clearly separated from the first.</p>
    </div>
    
    <saf-divider role="presentation"></saf-divider>
    
    <div class="content-section">
      <p>This is the third section with a decorative divider above.</p>
    </div>
  </div>
  
  <div class="vertical-example">
    <h4>Vertical Dividers</h4>
    <div class="vertical-content">
      <div class="vertical-section">
        <h5>Section A</h5>
        <p>Content for the first vertical section.</p>
      </div>
      
      <saf-divider orientation="vertical"></saf-divider>
      
      <div class="vertical-section">
        <h5>Section B</h5>
        <p>Content for the second vertical section.</p>
      </div>
      
      <saf-divider orientation="vertical" role="presentation"></saf-divider>
      
      <div class="vertical-section">
        <h5>Section C</h5>
        <p>Content for the third vertical section.</p>
      </div>
    </div>
  </div>
</div>

<style>
.divider-examples {
  padding: 2rem;
}

.horizontal-example {
  margin-bottom: 3rem;
}

.content-section {
  padding: 1rem 0;
}

.vertical-example h4 {
  margin-bottom: 1rem;
}

.vertical-content {
  display: flex;
  align-items: stretch;
  min-height: 200px;
  gap: 0;
}

.vertical-section {
  flex: 1;
  padding: 1rem;
  display: flex;
  flex-direction: column;
}

.vertical-section h5 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.vertical-section p {
  margin: 0;
  color: #666;
  flex-grow: 1;
}
</style>
```

### Content Separation

```html
<div class="content-separation">
  <h3>Content Separation Examples</h3>
  
  <!-- Article sections -->
  <article class="article-example">
    <header>
      <h2>Article Title</h2>
      <p class="meta">By Author Name • Published March 15, 2024</p>
    </header>
    
    <saf-divider></saf-divider>
    
    <section class="article-content">
      <h3>Introduction</h3>
      <p>This is the introduction section of the article with important opening statements and context.</p>
    </section>
    
    <saf-divider></saf-divider>
    
    <section class="article-content">
      <h3>Main Content</h3>
      <p>This section contains the primary content of the article with detailed information and analysis.</p>
      <p>Additional paragraphs provide comprehensive coverage of the topic.</p>
    </section>
    
    <saf-divider></saf-divider>
    
    <section class="article-content">
      <h3>Conclusion</h3>
      <p>The conclusion summarizes key points and provides final thoughts on the topic.</p>
    </section>
    
    <saf-divider role="presentation"></saf-divider>
    
    <footer class="article-footer">
      <p>Article footer with additional information and links.</p>
    </footer>
  </article>
</div>

<style>
.content-separation {
  padding: 2rem;
}

.article-example {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: #fafafa;
}

.article-example header h2 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.meta {
  margin: 0;
  color: #666;
  font-size: 14px;
}

.article-content {
  padding: 1.5rem 0;
}

.article-content h3 {
  margin: 0 0 1rem 0;
  color: #333;
}

.article-content p {
  margin: 0 0 1rem 0;
  line-height: 1.6;
  color: #444;
}

.article-content p:last-child {
  margin-bottom: 0;
}

.article-footer {
  padding: 1rem 0 0 0;
  color: #666;
  font-size: 14px;
}

.article-footer p {
  margin: 0;
}
</style>
```

### Sidebar and Navigation

```html
<div class="sidebar-navigation">
  <h3>Sidebar and Navigation</h3>
  
  <div class="layout-example">
    <!-- Main navigation with vertical dividers -->
    <nav class="main-nav">
      <div class="nav-section">
        <h4>Dashboard</h4>
        <ul class="nav-list">
          <li><a href="#overview">Overview</a></li>
          <li><a href="#analytics">Analytics</a></li>
          <li><a href="#reports">Reports</a></li>
        </ul>
      </div>
      
      <saf-divider></saf-divider>
      
      <div class="nav-section">
        <h4>Management</h4>
        <ul class="nav-list">
          <li><a href="#users">Users</a></li>
          <li><a href="#settings">Settings</a></li>
          <li><a href="#permissions">Permissions</a></li>
        </ul>
      </div>
      
      <saf-divider></saf-divider>
      
      <div class="nav-section">
        <h4>Tools</h4>
        <ul class="nav-list">
          <li><a href="#import">Import Data</a></li>
          <li><a href="#export">Export Data</a></li>
          <li><a href="#backup">Backup</a></li>
        </ul>
      </div>
    </nav>
    
    <saf-divider orientation="vertical"></saf-divider>
    
    <!-- Main content area -->
    <main class="main-content">
      <header class="content-header">
        <h2>Dashboard Overview</h2>
        <p>Welcome to your dashboard. Here you'll find an overview of your data.</p>
      </header>
      
      <saf-divider role="presentation"></saf-divider>
      
      <section class="content-body">
        <div class="content-grid">
          <div class="content-card">
            <h3>Statistics</h3>
            <p>View your latest statistics and metrics.</p>
          </div>
          
          <div class="content-card">
            <h3>Recent Activity</h3>
            <p>Check your most recent activities and updates.</p>
          </div>
          
          <div class="content-card">
            <h3>Quick Actions</h3>
            <p>Access frequently used tools and functions.</p>
          </div>
        </div>
      </section>
    </main>
  </div>
</div>

<style>
.sidebar-navigation {
  padding: 2rem;
}

.layout-example {
  display: flex;
  min-height: 500px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
}

.main-nav {
  width: 250px;
  background: #f8f9fa;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
}

.nav-section {
  padding: 0.5rem 0;
}

.nav-section h4 {
  margin: 0 0 1rem 0;
  color: #333;
  font-size: 14px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.nav-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.nav-list li {
  margin-bottom: 0.5rem;
}

.nav-list a {
  color: #555;
  text-decoration: none;
  padding: 0.5rem 0;
  display: block;
  border-radius: 4px;
  transition: all 0.2s ease;
}

.nav-list a:hover {
  color: #007acc;
  background: rgba(0, 122, 204, 0.1);
  padding-left: 0.5rem;
}

.main-content {
  flex: 1;
  padding: 2rem;
  background: white;
}

.content-header h2 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.content-header p {
  margin: 0;
  color: #666;
}

.content-body {
  padding: 2rem 0;
}

.content-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.content-card {
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: #fafafa;
}

.content-card h3 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.content-card p {
  margin: 0;
  color: #666;
  line-height: 1.5;
}
</style>
```

### Lists and Data

```html
<div class="list-data-examples">
  <h3>Lists and Data Separation</h3>
  
  <!-- User list with dividers -->
  <div class="user-list-example">
    <h4>User List</h4>
    <div class="user-list">
      <div class="user-item">
        <div class="user-avatar">👤</div>
        <div class="user-info">
          <h5>John Doe</h5>
          <p>Software Engineer</p>
          <span class="user-status online">Online</span>
        </div>
        <div class="user-actions">
          <button class="action-btn">Message</button>
          <button class="action-btn secondary">Profile</button>
        </div>
      </div>
      
      <saf-divider role="presentation"></saf-divider>
      
      <div class="user-item">
        <div class="user-avatar">👤</div>
        <div class="user-info">
          <h5>Jane Smith</h5>
          <p>Product Designer</p>
          <span class="user-status away">Away</span>
        </div>
        <div class="user-actions">
          <button class="action-btn">Message</button>
          <button class="action-btn secondary">Profile</button>
        </div>
      </div>
      
      <saf-divider role="presentation"></saf-divider>
      
      <div class="user-item">
        <div class="user-avatar">👤</div>
        <div class="user-info">
          <h5>Mike Johnson</h5>
          <p>Project Manager</p>
          <span class="user-status offline">Offline</span>
        </div>
        <div class="user-actions">
          <button class="action-btn">Message</button>
          <button class="action-btn secondary">Profile</button>
        </div>
      </div>
    </div>
  </div>
  
  <!-- Toolbar with vertical dividers -->
  <div class="toolbar-example">
    <h4>Toolbar with Vertical Dividers</h4>
    <div class="toolbar">
      <div class="toolbar-group">
        <button class="toolbar-btn">New</button>
        <button class="toolbar-btn">Open</button>
        <button class="toolbar-btn">Save</button>
      </div>
      
      <saf-divider orientation="vertical" role="presentation"></saf-divider>
      
      <div class="toolbar-group">
        <button class="toolbar-btn">Cut</button>
        <button class="toolbar-btn">Copy</button>
        <button class="toolbar-btn">Paste</button>
      </div>
      
      <saf-divider orientation="vertical" role="presentation"></saf-divider>
      
      <div class="toolbar-group">
        <button class="toolbar-btn">Undo</button>
        <button class="toolbar-btn">Redo</button>
      </div>
      
      <div class="toolbar-spacer"></div>
      
      <div class="toolbar-group">
        <button class="toolbar-btn">Settings</button>
        <button class="toolbar-btn">Help</button>
      </div>
    </div>
  </div>
</div>

<style>
.list-data-examples {
  padding: 2rem;
}

.user-list-example {
  margin-bottom: 3rem;
}

.user-list {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
  overflow: hidden;
}

.user-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  gap: 1rem;
}

.user-avatar {
  width: 40px;
  height: 40px;
  background: #f0f0f0;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
}

.user-info {
  flex: 1;
}

.user-info h5 {
  margin: 0 0 0.25rem 0;
  color: #333;
  font-size: 16px;
}

.user-info p {
  margin: 0 0 0.25rem 0;
  color: #666;
  font-size: 14px;
}

.user-status {
  font-size: 12px;
  padding: 2px 8px;
  border-radius: 12px;
  text-transform: uppercase;
  font-weight: 500;
}

.user-status.online {
  background: #d4edda;
  color: #155724;
}

.user-status.away {
  background: #fff3cd;
  color: #856404;
}

.user-status.offline {
  background: #f8d7da;
  color: #721c24;
}

.user-actions {
  display: flex;
  gap: 0.5rem;
}

.action-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #007acc;
  background: #007acc;
  color: white;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
}

.action-btn.secondary {
  background: transparent;
  color: #007acc;
}

.action-btn:hover {
  background: #005a9e;
}

.action-btn.secondary:hover {
  background: #f0f8ff;
}

.toolbar-example h4 {
  margin-bottom: 1rem;
}

.toolbar {
  display: flex;
  align-items: center;
  padding: 0.5rem;
  background: #f8f9fa;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  gap: 0;
}

.toolbar-group {
  display: flex;
  align-items: center;
  gap: 0;
}

.toolbar-btn {
  padding: 0.5rem 1rem;
  border: none;
  background: transparent;
  color: #333;
  cursor: pointer;
  border-radius: 4px;
  font-size: 14px;
  transition: background-color 0.2s ease;
}

.toolbar-btn:hover {
  background: #e9ecef;
}

.toolbar-btn:active {
  background: #dee2e6;
}

.toolbar-spacer {
  flex: 1;
}
</style>
```

### Form Sections

```html
<div class="form-sections">
  <h3>Form Section Separation</h3>
  
  <form class="form-example">
    <fieldset class="form-section">
      <legend>Personal Information</legend>
      <div class="form-row">
        <div class="form-group">
          <label for="firstName">First Name</label>
          <input type="text" id="firstName" name="firstName" />
        </div>
        <div class="form-group">
          <label for="lastName">Last Name</label>
          <input type="text" id="lastName" name="lastName" />
        </div>
      </div>
      <div class="form-group">
        <label for="email">Email Address</label>
        <input type="email" id="email" name="email" />
      </div>
    </fieldset>
    
    <saf-divider></saf-divider>
    
    <fieldset class="form-section">
      <legend>Contact Information</legend>
      <div class="form-group">
        <label for="phone">Phone Number</label>
        <input type="tel" id="phone" name="phone" />
      </div>
      <div class="form-group">
        <label for="address">Address</label>
        <textarea id="address" name="address" rows="3"></textarea>
      </div>
    </fieldset>
    
    <saf-divider></saf-divider>
    
    <fieldset class="form-section">
      <legend>Preferences</legend>
      <div class="form-group">
        <label>
          <input type="checkbox" name="newsletter" />
          Subscribe to newsletter
        </label>
      </div>
      <div class="form-group">
        <label>
          <input type="checkbox" name="notifications" />
          Receive email notifications
        </label>
      </div>
    </fieldset>
    
    <saf-divider role="presentation"></saf-divider>
    
    <div class="form-actions">
      <button type="submit" class="btn-primary">Save</button>
      <button type="button" class="btn-secondary">Cancel</button>
    </div>
  </form>
</div>

<style>
.form-sections {
  padding: 2rem;
}

.form-example {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
}

.form-section {
  border: none;
  padding: 1.5rem 0;
  margin: 0;
}

.form-section legend {
  font-weight: 600;
  color: #333;
  margin-bottom: 1rem;
  font-size: 18px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  color: #333;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  box-sizing: border-box;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #007acc;
  box-shadow: 0 0 0 2px rgba(0, 122, 204, 0.2);
}

.form-group input[type="checkbox"] {
  width: auto;
  margin-right: 0.5rem;
}

.form-actions {
  padding: 1.5rem 0 0 0;
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}

.btn-primary,
.btn-secondary {
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-primary {
  background: #007acc;
  color: white;
  border: 1px solid #007acc;
}

.btn-primary:hover {
  background: #005a9e;
  border-color: #005a9e;
}

.btn-secondary {
  background: transparent;
  color: #007acc;
  border: 1px solid #007acc;
}

.btn-secondary:hover {
  background: #f0f8ff;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React from 'react';

interface DividerProps {
  orientation?: 'horizontal' | 'vertical';
  role?: 'separator' | 'presentation';
  className?: string;
  'aria-label'?: string;
}

const SafDividerComponent: React.FC<DividerProps> = ({
  orientation = 'horizontal',
  role = 'separator',
  className,
  'aria-label': ariaLabel
}) => {
  return (
    <saf-divider
      orientation={orientation}
      role={role}
      className={className}
      aria-label={ariaLabel}
    />
  );
};

// Usage in components
const ContentSections: React.FC = () => {
  return (
    <div className="content-sections">
      <section>
        <h2>First Section</h2>
        <p>Content for the first section goes here.</p>
      </section>
      
      <SafDividerComponent aria-label="Content section separator" />
      
      <section>
        <h2>Second Section</h2>
        <p>Content for the second section goes here.</p>
      </section>
      
      <SafDividerComponent role="presentation" />
      
      <section>
        <h2>Third Section</h2>
        <p>Content for the third section goes here.</p>
      </section>
    </div>
  );
};

// Sidebar layout with vertical divider
const SidebarLayout: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  return (
    <div className="sidebar-layout">
      <aside className="sidebar">
        <nav>Navigation content here</nav>
      </aside>
      
      <SafDividerComponent 
        orientation="vertical" 
        aria-label="Sidebar content separator"
      />
      
      <main className="main-content">
        {children}
      </main>
    </div>
  );
};
```

### Angular Example

```typescript
// divider.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-saf-divider',
  template: `
    <saf-divider
      [attr.orientation]="orientation"
      [attr.role]="role"
      [attr.aria-label]="ariaLabel"
      [class]="className"
    ></saf-divider>
  `
})
export class SafDividerComponent {
  @Input() orientation: 'horizontal' | 'vertical' = 'horizontal';
  @Input() role: 'separator' | 'presentation' = 'separator';
  @Input() ariaLabel?: string;
  @Input() className?: string;
}

// Usage in component template
/*
<div class="content-sections">
  <section>
    <h2>Section 1</h2>
    <p>First section content</p>
  </section>
  
  <app-saf-divider ariaLabel="Section separator"></app-saf-divider>
  
  <section>
    <h2>Section 2</h2>
    <p>Second section content</p>
  </section>
  
  <app-saf-divider 
    orientation="vertical" 
    role="presentation">
  </app-saf-divider>
</div>
*/
```

### Vue Example

```vue
<template>
  <saf-divider
    :orientation="orientation"
    :role="role"
    :aria-label="ariaLabel"
    :class="className"
  />
</template>

<script>
export default {
  name: 'SafDividerComponent',
  props: {
    orientation: {
      type: String,
      default: 'horizontal',
      validator: value => ['horizontal', 'vertical'].includes(value)
    },
    role: {
      type: String,
      default: 'separator',
      validator: value => ['separator', 'presentation'].includes(value)
    },
    ariaLabel: String,
    className: String
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div class="layout-example">
    <div class="content-sections">
      <section class="content-section">
        <h2>First Section</h2>
        <p>Content goes here</p>
      </section>
      
      <SafDividerComponent aria-label="Content separator" />
      
      <section class="content-section">
        <h2>Second Section</h2>
        <p>More content here</p>
      </section>
    </div>
    
    <SafDividerComponent orientation="vertical" />
    
    <aside class="sidebar">
      <p>Sidebar content</p>
    </aside>
  </div>
</template>
-->
```

## Accessibility Features

### ARIA Support

- **Semantic Role**: `role="separator"` provides semantic meaning for screen readers
- **Presentation Mode**: `role="presentation"` excludes decorative dividers from accessibility tree
- **Orientation**: Automatically communicates horizontal/vertical orientation to assistive technology
- **Labels**: Supports `aria-label` for additional context when needed

### Screen Reader Support

- Semantic separators are announced as "separator" by screen readers
- Presentation dividers are ignored by assistive technology
- Orientation is communicated when relevant
- Proper focus management in complex layouts

### Keyboard Navigation

- Separators don't interfere with keyboard navigation flow
- Focus moves naturally around dividers in tab order
- Vertical dividers work properly in flex/grid layouts with keyboard navigation

## Best Practices

### Semantic Usage
- Use `role="separator"` for meaningful content separation
- Use `role="presentation"` for purely visual decoration
- Provide `aria-label` when divider context isn't obvious
- Consider document structure and heading hierarchy

### Visual Design
- Ensure sufficient contrast for dividers
- Use consistent divider styles throughout your application
- Consider spacing around dividers for visual breathing room
- Test divider visibility across different themes

### Layout Considerations
- Vertical dividers require proper container height
- Consider responsive behavior for complex layouts
- Ensure dividers work well with flex and grid layouts
- Test across different screen sizes and orientations

### Performance
- Dividers have minimal performance impact
- Use CSS for styling rather than inline styles
- Consider using CSS borders instead of divider components for simple cases
- Optimize for layout shifts in dynamic content

### User Experience
- Don't overuse dividers - they can create visual noise
- Ensure dividers enhance rather than hinder content flow
- Consider alternative separation methods (spacing, backgrounds, etc.)
- Test with users to ensure dividers improve content organization

## Related Components

- **SafSpacer**: For adding spacing without visual dividers
- **SafCard**: For content grouping with visual boundaries
- **SafAccordion**: For collapsible content sections
- **SafTabs**: For tabbed content organization

---

*This documentation covers SafDivider v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
