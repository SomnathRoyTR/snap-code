# SafDescriptionList

## Overview

SafDescriptionList is a semantic HTML component for displaying structured pairs of terms and their descriptions. It provides an accessible and well-formatted way to present definition lists, glossaries, metadata, and other name-value pairs with proper semantic markup and flexible styling options.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `orientation` | `'vertical' \| 'horizontal'` | `'vertical'` | Layout direction of term-description pairs |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting spacing and typography |
| `density` | `'compact' \| 'normal' \| 'relaxed'` | `'normal'` | Spacing density between pairs |
| `variant` | `'default' \| 'bordered' \| 'zebra'` | `'default'` | Visual style variant |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | SafDescriptionTerm and SafDescriptionDetails components |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onTermClick` | `(termId: string) => void` | Fired when a term is clicked (if interactive) |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `orientation` | `'vertical' \| 'horizontal'` | `'vertical'` | Layout direction of term-description pairs |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting spacing and typography |
| `density` | `'compact' \| 'normal' \| 'relaxed'` | `'normal'` | Spacing density between pairs |
| `variant` | `'default' \| 'bordered' \| 'zebra'` | `'default'` | Visual style variant |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `termClick` | `EventEmitter<string>` | Fired when a term is clicked (if interactive) |

## Usage Examples

### Basic Description List

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Name</SafDescriptionTerm>
  <SafDescriptionDetails>John Smith</SafDescriptionDetails>
  
  <SafDescriptionTerm>Email</SafDescriptionTerm>
  <SafDescriptionDetails>john.smith@example.com</SafDescriptionDetails>
  
  <SafDescriptionTerm>Department</SafDescriptionTerm>
  <SafDescriptionDetails>Engineering</SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term>Name</saf-description-term>
  <saf-description-details>John Smith</saf-description-details>
  
  <saf-description-term>Email</saf-description-term>
  <saf-description-details>john.smith@example.com</saf-description-details>
  
  <saf-description-term>Department</saf-description-term>
  <saf-description-details>Engineering</saf-description-details>
</saf-description-list>
```

### Horizontal Layout

```typescript
// React
<SafDescriptionList orientation="horizontal">
  <SafDescriptionTerm>Status</SafDescriptionTerm>
  <SafDescriptionDetails>Active</SafDescriptionDetails>
  
  <SafDescriptionTerm>Priority</SafDescriptionTerm>
  <SafDescriptionDetails>High</SafDescriptionDetails>
  
  <SafDescriptionTerm>Assigned to</SafDescriptionTerm>
  <SafDescriptionDetails>Development Team</SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list orientation="horizontal">
  <saf-description-term>Status</saf-description-term>
  <saf-description-details>Active</saf-description-details>
  
  <saf-description-term>Priority</saf-description-term>
  <saf-description-details>High</saf-description-details>
  
  <saf-description-term>Assigned to</saf-description-term>
  <saf-description-details>Development Team</saf-description-details>
</saf-description-list>
```

### Size Variants

```typescript
// React
<SafDescriptionList size="small">
  <SafDescriptionTerm>Compact View</SafDescriptionTerm>
  <SafDescriptionDetails>Smaller text and reduced spacing</SafDescriptionDetails>
</SafDescriptionList>

<SafDescriptionList size="medium">
  <SafDescriptionTerm>Default View</SafDescriptionTerm>
  <SafDescriptionDetails>Standard text size and spacing</SafDescriptionDetails>
</SafDescriptionList>

<SafDescriptionList size="large">
  <SafDescriptionTerm>Prominent View</SafDescriptionTerm>
  <SafDescriptionDetails>Larger text for enhanced readability</SafDescriptionDetails>
</SafDescriptionList>
```

### Density Options

```typescript
// React
<SafDescriptionList density="compact">
  <SafDescriptionTerm>Tight Spacing</SafDescriptionTerm>
  <SafDescriptionDetails>Minimal space between items</SafDescriptionDetails>
</SafDescriptionList>

<SafDescriptionList density="relaxed">
  <SafDescriptionTerm>Spacious Layout</SafDescriptionTerm>
  <SafDescriptionDetails>Extra breathing room between items</SafDescriptionDetails>
</SafDescriptionList>
```

### Visual Variants

```typescript
// React
<SafDescriptionList variant="bordered">
  <SafDescriptionTerm>Bordered Style</SafDescriptionTerm>
  <SafDescriptionDetails>Each pair has visual separation</SafDescriptionDetails>
  
  <SafDescriptionTerm>Clear Structure</SafDescriptionTerm>
  <SafDescriptionDetails>Helps distinguish individual items</SafDescriptionDetails>
</SafDescriptionList>

<SafDescriptionList variant="zebra">
  <SafDescriptionTerm>Alternating Rows</SafDescriptionTerm>
  <SafDescriptionDetails>Zebra striping for better readability</SafDescriptionDetails>
  
  <SafDescriptionTerm>Enhanced Scanning</SafDescriptionTerm>
  <SafDescriptionDetails>Easier to follow across long lists</SafDescriptionDetails>
</SafDescriptionList>
```

### Complex Descriptions with Rich Content

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>User Profile</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafAvatar name="Jane Doe" size="small" />
    <span>Jane Doe - Senior Developer</span>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Project Status</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafStatus variant="success">In Progress</SafStatus>
    <SafProgressBar value={75} />
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Tags</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafChip variant="primary">Frontend</SafChip>
    <SafChip variant="secondary">React</SafChip>
    <SafChip variant="outline">TypeScript</SafChip>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Interactive Terms with Click Handlers

```typescript
// React
<SafDescriptionList onTermClick={(termId) => handleTermClick(termId)}>
  <SafDescriptionTerm id="location">Location</SafDescriptionTerm>
  <SafDescriptionDetails>
    New York Office
    <SafButton variant="text" size="small">View Map</SafButton>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm id="contact">Contact Info</SafDescriptionTerm>
  <SafDescriptionDetails>
    +1 (555) 123-4567
    <SafButton variant="text" size="small">Call Now</SafButton>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Multi-line and Formatted Descriptions

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Description</SafDescriptionTerm>
  <SafDescriptionDetails>
    <p>A comprehensive project management tool designed to streamline 
    team collaboration and boost productivity.</p>
    <p>Features include real-time updates, automated reporting, 
    and integrated communication channels.</p>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Requirements</SafDescriptionTerm>
  <SafDescriptionDetails>
    <ul>
      <li>Node.js 16.0 or higher</li>
      <li>Modern web browser</li>
      <li>Active internet connection</li>
    </ul>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Mixed Layout with Different Term Types

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm required>Required Field</SafDescriptionTerm>
  <SafDescriptionDetails>This field must be completed</SafDescriptionDetails>
  
  <SafDescriptionTerm optional>Optional Field</SafDescriptionTerm>
  <SafDescriptionDetails>This field is not required</SafDescriptionDetails>
  
  <SafDescriptionTerm interactive onClick={() => showDetails()}>
    Expandable Field
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    Click the term above to see more details
  </SafDescriptionDetails>
</SafDescriptionList>
```

## Best Practices

### Content Organization
- **Logical Grouping**: Group related terms together for better comprehension
- **Consistent Terminology**: Use consistent naming conventions for terms
- **Clear Hierarchy**: Order terms by importance or logical sequence
- **Appropriate Length**: Keep descriptions concise but informative

### Layout Selection
- **Vertical Layout**: Use for detailed descriptions and when screen space permits
- **Horizontal Layout**: Choose for compact displays and simple key-value pairs
- **Size Appropriately**: Match size to content importance and available space
- **Consider Context**: Align density with overall page design patterns

### Accessibility
- **Semantic Structure**: Maintain proper term-description relationships
- **Screen Reader Support**: Ensure descriptions are properly associated with terms
- **Keyboard Navigation**: Support tab navigation through interactive elements
- **Focus Management**: Provide clear focus indicators for interactive terms

### Responsive Design
- **Flexible Layout**: Consider how horizontal layouts adapt on smaller screens
- **Content Priority**: Show most important information first on mobile
- **Touch Targets**: Ensure interactive elements meet minimum touch target sizes
- **Readable Text**: Maintain readability across all device sizes

## Accessibility Considerations

- Uses semantic `<dl>`, `<dt>`, and `<dd>` HTML elements
- Maintains proper term-description associations for screen readers
- Supports keyboard navigation for interactive elements
- Provides appropriate ARIA labels and descriptions
- Ensures sufficient color contrast for all text content
- Respects user preferences for reduced motion and high contrast

## Related Components

- **SafDescriptionTerm**: Individual term component within description lists
- **SafDescriptionDetails**: Individual description component for term details
- **SafMetadata**: Alternative component for simple key-value displays
- **SafMetadataItem**: Individual metadata items for basic information display
- **SafList**: General list component for non-definition content
- **SafCard**: Container component for grouping related description lists

## Notes

- SafDescriptionList automatically handles proper semantic markup
- The component supports both simple text and rich HTML content in descriptions
- Interactive terms can be made clickable for additional functionality
- Visual variants can be combined with different orientations and sizes
- The component maintains accessibility standards while providing flexible styling options
- Consider using SafMetadata for simpler key-value displays without semantic requirements
