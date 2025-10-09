# SafText

A flexible text component that provides consistent typography styles across the design system with various appearance options for different text hierarchies.

## Usage

```html
<saf-text appearance="heading-lg">This is a large heading</saf-text>
<saf-text appearance="body-default-md">This is regular body text.</saf-text>
```

## API

### SafText

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `appearance` | [TextAppearance](#text-appearances) | `'body-default-md'` | The visual style/typography level to apply |
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |

#### Slots

| Name | Description |
|------|-------------|
| default | The text content to display |

## Text Appearances

### Display Text
- `display-lg` - Largest display text for hero sections
- `display-sm` - Smaller display text for section headers

### Headings
- `heading-4xl` - Extra extra extra large heading
- `heading-3xl` - Extra extra large heading  
- `heading-2xl` - Extra large heading
- `heading-xl` - Large heading
- `heading-lg` - Large heading (page/section titles)
- `heading-md` - Medium heading (subsection titles)

### Body Text
- `body-default-lg` - Large body text (regular weight)
- `body-strong-lg` - Large body text (bold weight)
- `body-default-md` - Medium body text (regular weight) - Default
- `body-strong-md` - Medium body text (bold weight)
- `body-default-sm` - Small body text (regular weight)
- `body-strong-sm` - Small body text (bold weight)
- `body-default-xs` - Extra small body text (regular weight)
- `body-strong-xs` - Extra small body text (bold weight)

### Eyebrow Text
- `eyebrow-heavy-md` - Medium eyebrow text (overlines/category labels)
- `eyebrow-heavy-sm` - Small eyebrow text (overlines/category labels)

## Examples

### Display Text

```html
<saf-text appearance="display-lg">Welcome to Our Platform</saf-text>
<saf-text appearance="display-sm">Discover powerful features designed for you</saf-text>
```

### Headings Hierarchy

```html
<saf-text appearance="heading-4xl">Main Page Title</saf-text>
<saf-text appearance="heading-3xl">Major Section</saf-text>
<saf-text appearance="heading-2xl">Important Subsection</saf-text>
<saf-text appearance="heading-xl">Large Section Header</saf-text>
<saf-text appearance="heading-lg">Section Title</saf-text>
<saf-text appearance="heading-md">Subsection Title</saf-text>
```

### Body Text Variations

```html
<saf-text appearance="body-default-lg">
  This is large body text suitable for introductory paragraphs or when you need text to be more prominent.
</saf-text>

<saf-text appearance="body-strong-lg">
  This is large body text with strong/bold weight for emphasis.
</saf-text>

<saf-text appearance="body-default-md">
  This is the standard body text size used for most content. It provides good readability while maintaining efficient space usage.
</saf-text>

<saf-text appearance="body-strong-md">
  This is standard body text with bold weight for highlighting important information.
</saf-text>

<saf-text appearance="body-default-sm">
  This is small body text often used for secondary information, captions, or supplementary content.
</saf-text>

<saf-text appearance="body-strong-sm">
  This is small body text with bold weight.
</saf-text>

<saf-text appearance="body-default-xs">
  This is extra small body text for fine print, legal text, or minimal space contexts.
</saf-text>

<saf-text appearance="body-strong-xs">
  This is extra small body text with bold weight.
</saf-text>
```

### Eyebrow Text

```html
<saf-text appearance="eyebrow-heavy-md">FEATURED ARTICLE</saf-text>
<saf-text appearance="heading-lg">The Future of Web Development</saf-text>
<saf-text appearance="body-default-md">
  Exploring emerging trends and technologies that will shape how we build for the web...
</saf-text>

<saf-text appearance="eyebrow-heavy-sm">CATEGORY: TECHNOLOGY</saf-text>
<saf-text appearance="heading-md">Latest Updates</saf-text>
```

### Different Density Settings

```html
<div style="border: 1px solid #ccc; padding: 16px; margin: 8px;">
  <saf-text appearance="heading-md" density="compact">Compact Heading</saf-text>
  <saf-text appearance="body-default-md" density="compact">
    This text uses compact density for tighter spacing.
  </saf-text>
</div>

<div style="border: 1px solid #ccc; padding: 16px; margin: 8px;">
  <saf-text appearance="heading-md" density="normal">Normal Heading</saf-text>
  <saf-text appearance="body-default-md" density="normal">
    This text uses normal density for standard spacing.
  </saf-text>
</div>

<div style="border: 1px solid #ccc; padding: 16px; margin: 8px;">
  <saf-text appearance="heading-md" density="spacious">Spacious Heading</saf-text>
  <saf-text appearance="body-default-md" density="spacious">
    This text uses spacious density for more generous spacing.
  </saf-text>
</div>
```

### Article Layout Example

```html
<article>
  <saf-text appearance="eyebrow-heavy-sm">TECHNOLOGY</saf-text>
  
  <saf-text appearance="heading-2xl">
    The Evolution of Design Systems
  </saf-text>
  
  <saf-text appearance="body-default-lg">
    Design systems have revolutionized how teams approach product development, 
    creating consistency and efficiency across digital experiences.
  </saf-text>
  
  <saf-text appearance="heading-lg">Why Design Systems Matter</saf-text>
  
  <saf-text appearance="body-default-md">
    In today's fast-paced development environment, design systems provide the 
    foundation for scalable, consistent user interfaces. They enable teams to:
  </saf-text>
  
  <ul>
    <li><saf-text appearance="body-default-md">Maintain visual consistency across products</saf-text></li>
    <li><saf-text appearance="body-default-md">Accelerate development cycles</saf-text></li>
    <li><saf-text appearance="body-default-md">Improve accessibility compliance</saf-text></li>
  </ul>
  
  <saf-text appearance="heading-md">Implementation Strategies</saf-text>
  
  <saf-text appearance="body-default-md">
    Successful design system implementation requires careful planning and 
    stakeholder alignment. Here are key considerations:
  </saf-text>
  
  <saf-text appearance="body-strong-md">Start Small and Scale</saf-text>
  <saf-text appearance="body-default-md">
    Begin with core components and gradually expand the system based on actual needs.
  </saf-text>
  
  <saf-text appearance="body-default-sm">
    Last updated: March 2024 | Reading time: 5 minutes
  </saf-text>
</article>
```

### Card Layout Example

```html
<div style="border: 1px solid #e1e5e9; border-radius: 8px; padding: 24px; max-width: 400px;">
  <saf-text appearance="eyebrow-heavy-md">NEW FEATURE</saf-text>
  
  <saf-text appearance="heading-lg" style="margin: 12px 0;">
    Advanced Analytics Dashboard
  </saf-text>
  
  <saf-text appearance="body-default-md" style="margin-bottom: 16px;">
    Get deeper insights into your data with our new analytics dashboard featuring 
    real-time metrics and customizable reports.
  </saf-text>
  
  <div style="display: flex; justify-content: space-between; align-items: center;">
    <saf-text appearance="body-strong-sm">Available Now</saf-text>
    <saf-text appearance="body-default-xs" style="color: #666;">
      2 min read
    </saf-text>
  </div>
</div>
```

### Status Message Examples

```html
<div style="padding: 12px; background: #f0f9f0; border: 1px solid #4caf50; border-radius: 4px; margin: 8px;">
  <saf-text appearance="body-strong-sm" style="color: #2e7d32;">Success:</saf-text>
  <saf-text appearance="body-default-sm" style="color: #2e7d32;">
    Your changes have been saved successfully.
  </saf-text>
</div>

<div style="padding: 12px; background: #fff3e0; border: 1px solid #ff9800; border-radius: 4px; margin: 8px;">
  <saf-text appearance="body-strong-sm" style="color: #ef6c00;">Warning:</saf-text>
  <saf-text appearance="body-default-sm" style="color: #ef6c00;">
    This action cannot be undone. Please proceed with caution.
  </saf-text>
</div>

<div style="padding: 12px; background: #ffebee; border: 1px solid #f44336; border-radius: 4px; margin: 8px;">
  <saf-text appearance="body-strong-sm" style="color: #c62828;">Error:</saf-text>
  <saf-text appearance="body-default-sm" style="color: #c62828;">
    Unable to save changes. Please try again.
  </saf-text>
</div>
```

### Navigation Example

```html
<nav style="display: flex; gap: 24px; align-items: center; padding: 16px 0; border-bottom: 1px solid #e1e5e9;">
  <saf-text appearance="heading-md">Brand Name</saf-text>
  
  <div style="display: flex; gap: 16px; margin-left: auto;">
    <saf-text appearance="body-default-md">
      <a href="/" style="text-decoration: none; color: inherit;">Home</a>
    </saf-text>
    <saf-text appearance="body-default-md">
      <a href="/about" style="text-decoration: none; color: inherit;">About</a>
    </saf-text>
    <saf-text appearance="body-default-md">
      <a href="/services" style="text-decoration: none; color: inherit;">Services</a>
    </saf-text>
    <saf-text appearance="body-strong-md">
      <a href="/contact" style="text-decoration: none; color: inherit;">Contact</a>
    </saf-text>
  </div>
</nav>
```

### Data Table Headers

```html
<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="text-align: left; padding: 12px; border-bottom: 2px solid #e1e5e9;">
        <saf-text appearance="body-strong-sm">Product Name</saf-text>
      </th>
      <th style="text-align: left; padding: 12px; border-bottom: 2px solid #e1e5e9;">
        <saf-text appearance="body-strong-sm">Price</saf-text>
      </th>
      <th style="text-align: left; padding: 12px; border-bottom: 2px solid #e1e5e9;">
        <saf-text appearance="body-strong-sm">Status</saf-text>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f0f0f0;">
        <saf-text appearance="body-default-md">Premium Widget</saf-text>
      </td>
      <td style="padding: 12px; border-bottom: 1px solid #f0f0f0;">
        <saf-text appearance="body-default-md">$29.99</saf-text>
      </td>
      <td style="padding: 12px; border-bottom: 1px solid #f0f0f0;">
        <saf-text appearance="body-strong-sm" style="color: #4caf50;">Available</saf-text>
      </td>
    </tr>
  </tbody>
</table>
```

## Framework Integration

### React

```jsx
import { SafText } from '@saffron/core-components-react';

function TypographyExample() {
  const article = {
    category: 'Technology',
    title: 'Understanding Design Systems',
    summary: 'A comprehensive guide to implementing design systems in modern development.',
    content: 'Design systems provide the foundation for consistent, scalable user interfaces...',
    metadata: 'Published March 15, 2024 • 3 min read'
  };

  return (
    <article>
      <SafText appearance="eyebrow-heavy-sm">
        {article.category.toUpperCase()}
      </SafText>
      
      <SafText appearance="heading-2xl">
        {article.title}
      </SafText>
      
      <SafText appearance="body-default-lg">
        {article.summary}
      </SafText>
      
      <SafText appearance="body-default-md">
        {article.content}
      </SafText>
      
      <SafText appearance="body-default-xs" style={{ color: '#666' }}>
        {article.metadata}
      </SafText>
    </article>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-text-demo',
  template: `
    <div class="content-layout">
      <saf-text appearance="eyebrow-heavy-md">
        {{ eyebrow }}
      </saf-text>
      
      <saf-text [appearance]="titleAppearance">
        {{ title }}
      </saf-text>
      
      <saf-text 
        appearance="body-default-md" 
        [density]="textDensity"
        [innerHTML]="formattedContent">
      </saf-text>
      
      <saf-text 
        *ngFor="let item of listItems" 
        appearance="body-default-sm">
        • {{ item }}
      </saf-text>
      
      <saf-text appearance="body-default-xs" class="metadata">
        Last updated: {{ lastUpdated | date }}
      </saf-text>
    </div>
  `,
  styles: [`
    .content-layout {
      max-width: 600px;
      margin: 0 auto;
    }
    .metadata {
      color: #666;
      margin-top: 24px;
    }
  `]
})
export class TextDemoComponent {
  eyebrow = 'FEATURED CONTENT';
  title = 'Advanced Component Patterns';
  titleAppearance = 'heading-xl';
  textDensity = 'normal';
  lastUpdated = new Date();

  formattedContent = `
    Learn how to build scalable and maintainable component architectures 
    using modern development practices and design system principles.
  `;

  listItems = [
    'Component composition patterns',
    'State management strategies', 
    'Performance optimization techniques',
    'Accessibility best practices'
  ];
}
```

## Accessibility Features

- **Semantic HTML**: Renders as appropriate semantic elements based on appearance
- **Screen Reader Support**: Text content is properly announced by screen readers
- **Color Contrast**: Designed to meet WCAG color contrast requirements
- **Responsive Typography**: Text scales appropriately across different screen sizes

## Best Practices

1. **Establish Hierarchy**: Use heading appearances to create clear information hierarchy
2. **Consistent Usage**: Use the same appearances consistently for similar content types
3. **Appropriate Context**: Choose appearances that match the semantic importance of content
4. **Density Consistency**: Apply consistent density settings within related content areas
5. **Readability**: Ensure sufficient color contrast and appropriate line spacing
6. **Responsive Behavior**: Consider how text will scale on different devices
7. **Content Strategy**: Use eyebrow text to provide context and category information

## Related Components

- `saf-heading`: For semantic heading elements with built-in hierarchy
- `saf-paragraph`: For paragraph content with consistent spacing
- `saf-link`: For linked text content
- `saf-list`: For structured text content in list format
