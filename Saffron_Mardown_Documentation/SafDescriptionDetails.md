# SafDescriptionDetails

## Overview

SafDescriptionDetails is a semantic component that represents the description or definition part of a description list item. It works in conjunction with SafDescriptionTerm to create accessible and well-structured definition lists, providing proper semantic markup and flexible content support for detailed descriptions.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting typography and spacing |
| `variant` | `'default' \| 'highlighted' \| 'muted'` | `'default'` | Visual style variant |
| `multiline` | `boolean` | `false` | Optimizes layout for multi-line content |
| `copyable` | `boolean` | `false` | Adds copy-to-clipboard functionality |
| `editable` | `boolean` | `false` | Makes content inline editable |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Description content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onCopy` | `(content: string) => void` | Fired when content is copied to clipboard |
| `onEdit` | `(newContent: string) => void` | Fired when inline editing is completed |
| `onEditStart` | `() => void` | Fired when inline editing begins |
| `onEditCancel` | `() => void` | Fired when inline editing is cancelled |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting typography and spacing |
| `variant` | `'default' \| 'highlighted' \| 'muted'` | `'default'` | Visual style variant |
| `multiline` | `boolean` | `false` | Optimizes layout for multi-line content |
| `copyable` | `boolean` | `false` | Adds copy-to-clipboard functionality |
| `editable` | `boolean` | `false` | Makes content inline editable |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `copy` | `EventEmitter<string>` | Fired when content is copied to clipboard |
| `edit` | `EventEmitter<string>` | Fired when inline editing is completed |
| `editStart` | `EventEmitter<void>` | Fired when inline editing begins |
| `editCancel` | `EventEmitter<void>` | Fired when inline editing is cancelled |

## Usage Examples

### Basic Description Details

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

### Multi-line Content

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Project Description</SafDescriptionTerm>
  <SafDescriptionDetails multiline>
    A comprehensive project management tool designed to streamline 
    team collaboration and boost productivity. The application includes 
    features for task tracking, real-time communication, automated 
    reporting, and integration with popular development tools.
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Key Features</SafDescriptionTerm>
  <SafDescriptionDetails multiline>
    <ul>
      <li>Real-time collaboration</li>
      <li>Advanced task management</li>
      <li>Automated reporting</li>
      <li>Third-party integrations</li>
    </ul>
  </SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term>Project Description</saf-description-term>
  <saf-description-details [multiline]="true">
    A comprehensive project management tool designed to streamline 
    team collaboration and boost productivity. The application includes 
    features for task tracking, real-time communication, automated 
    reporting, and integration with popular development tools.
  </saf-description-details>
</saf-description-list>
```

### Copyable Content

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>API Key</SafDescriptionTerm>
  <SafDescriptionDetails 
    copyable 
    onCopy={(content) => showCopyNotification(content)}
  >
    sk-1234567890abcdef
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Repository URL</SafDescriptionTerm>
  <SafDescriptionDetails copyable>
    https://github.com/company/project-name.git
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Server Address</SafDescriptionTerm>
  <SafDescriptionDetails copyable>
    192.168.1.100:8080
  </SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term>API Key</saf-description-term>
  <saf-description-details 
    [copyable]="true"
    (copy)="showCopyNotification($event)"
  >
    sk-1234567890abcdef
  </saf-description-details>
  
  <saf-description-term>Repository URL</saf-description-term>
  <saf-description-details [copyable]="true">
    https://github.com/company/project-name.git
  </saf-description-details>
</saf-description-list>
```

### Editable Content

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Display Name</SafDescriptionTerm>
  <SafDescriptionDetails 
    editable
    onEdit={(newValue) => updateDisplayName(newValue)}
    onEditStart={() => setIsEditing(true)}
    onEditCancel={() => setIsEditing(false)}
  >
    John Smith
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Bio</SafDescriptionTerm>
  <SafDescriptionDetails 
    editable
    multiline
    onEdit={(newValue) => updateBio(newValue)}
  >
    Senior Software Engineer with 8 years of experience 
    in full-stack development and team leadership.
  </SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term>Display Name</saf-description-term>
  <saf-description-details 
    [editable]="true"
    (edit)="updateDisplayName($event)"
    (editStart)="setIsEditing(true)"
    (editCancel)="setIsEditing(false)"
  >
    John Smith
  </saf-description-details>
</saf-description-list>
```

### Size Variants

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm size="small">Small Details</SafDescriptionTerm>
  <SafDescriptionDetails size="small">
    Compact text for secondary information
  </SafDescriptionDetails>
  
  <SafDescriptionTerm size="medium">Standard Details</SafDescriptionTerm>
  <SafDescriptionDetails size="medium">
    Default size for most content descriptions
  </SafDescriptionDetails>
  
  <SafDescriptionTerm size="large">Large Details</SafDescriptionTerm>
  <SafDescriptionDetails size="large">
    Prominent text for important information
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Visual Variants

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Standard Information</SafDescriptionTerm>
  <SafDescriptionDetails variant="default">
    Normal appearance for regular content
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Important Notice</SafDescriptionTerm>
  <SafDescriptionDetails variant="highlighted">
    Emphasized content that draws attention
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Additional Notes</SafDescriptionTerm>
  <SafDescriptionDetails variant="muted">
    Less prominent content for supplementary information
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Rich Content with Components

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>User Profile</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafAvatar name="Jane Doe" size="small" />
    <span>Jane Doe - Senior Developer</span>
    <SafButton variant="text" size="small">View Profile</SafButton>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Project Status</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafStatus variant="success">Active</SafStatus>
    <SafProgressBar value={75} size="small" />
    <span>75% Complete</span>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Tags</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafChip variant="primary" size="small">Frontend</SafChip>
    <SafChip variant="secondary" size="small">React</SafChip>
    <SafChip variant="outline" size="small">TypeScript</SafChip>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Complex Layout with Multiple Content Types

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Contact Information</SafDescriptionTerm>
  <SafDescriptionDetails multiline>
    <div>
      <strong>Email:</strong> 
      <SafDescriptionDetails copyable inline>
        contact@example.com
      </SafDescriptionDetails>
    </div>
    <div>
      <strong>Phone:</strong> 
      <SafDescriptionDetails copyable inline>
        +1 (555) 123-4567
      </SafDescriptionDetails>
    </div>
    <div>
      <strong>Address:</strong>
      <address>
        123 Main Street<br/>
        New York, NY 10001<br/>
        United States
      </address>
    </div>
  </SafDescriptionDetails>
  
  <SafDescriptionTerm>Social Media</SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafLink href="https://twitter.com/example" target="_blank">
      <SafIcon name="twitter" size="small" /> @example
    </SafLink>
    <SafLink href="https://linkedin.com/company/example" target="_blank">
      <SafIcon name="linkedin" size="small" /> LinkedIn
    </SafLink>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Form Integration

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>Current Settings</SafDescriptionTerm>
  <SafDescriptionDetails multiline>
    <SafFormField label="Notification Preference">
      <SafSelect value="email" onChange={handleNotificationChange}>
        <SafOption value="email">Email Only</SafOption>
        <SafOption value="sms">SMS Only</SafOption>
        <SafOption value="both">Email and SMS</SafOption>
      </SafSelect>
    </SafFormField>
    
    <SafFormField label="Theme">
      <SafRadioGroup value="light" onChange={handleThemeChange}>
        <SafRadio value="light">Light</SafRadio>
        <SafRadio value="dark">Dark</SafRadio>
        <SafRadio value="auto">Auto</SafRadio>
      </SafRadioGroup>
    </SafFormField>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Conditional Content Display

```typescript
// React
const [showDetails, setShowDetails] = useState(false);

<SafDescriptionList>
  <SafDescriptionTerm interactive onClick={() => setShowDetails(!showDetails)}>
    Advanced Configuration
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    {showDetails ? (
      <SafDescriptionDetails multiline>
        <SafCode language="json">
{`{
  "timeout": 30000,
  "retries": 3,
  "caching": true,
  "compression": "gzip"
}`}
        </SafCode>
      </SafDescriptionDetails>
    ) : (
      <SafDescriptionDetails variant="muted">
        Click term to view configuration details
      </SafDescriptionDetails>
    )}
  </SafDescriptionDetails>
</SafDescriptionList>
```

## Best Practices

### Content Organization
- **Structured Information**: Use clear, well-organized content structure
- **Appropriate Length**: Balance detail with readability
- **Scannable Format**: Use lists, paragraphs, and formatting for easy scanning
- **Consistent Style**: Maintain consistent formatting across similar content types

### Interactive Features
- **Purposeful Interactivity**: Only make content copyable/editable when beneficial
- **Clear Indicators**: Provide visual cues for interactive capabilities
- **Feedback**: Show confirmation when actions are completed
- **Error Handling**: Gracefully handle editing and copying failures

### Typography and Layout
- **Readable Text**: Ensure appropriate text size and spacing
- **Visual Hierarchy**: Use variants to establish content importance
- **Multi-line Handling**: Optimize spacing for longer content
- **Responsive Design**: Ensure content works well across screen sizes

### Accessibility
- **Screen Reader Support**: Ensure content is properly announced
- **Keyboard Navigation**: Support keyboard access for interactive features
- **Focus Management**: Provide clear focus indicators
- **Content Association**: Maintain proper semantic relationships

## Accessibility Considerations

- Uses semantic `<dd>` HTML element for proper document structure
- Maintains association with corresponding description terms
- Supports keyboard navigation for interactive elements
- Provides appropriate ARIA attributes for copyable and editable content
- Ensures sufficient color contrast for all visual variants
- Announces content changes to screen readers during editing

## Related Components

- **SafDescriptionTerm**: Companion component for term labels
- **SafDescriptionList**: Container component for organizing term-detail pairs
- **SafMetadataItem**: Alternative component for simple key-value displays
- **SafCode**: Specialized component for code content display
- **SafText**: General text component for body content

## Notes

- SafDescriptionDetails should always be used within a SafDescriptionList
- Copyable functionality automatically handles clipboard operations
- Editable content supports both single-line and multi-line editing
- Rich content support allows embedding of other Saffron components
- The component maintains semantic structure while providing flexible content options
- Visual variants can be combined with size and interactive properties
- Multi-line optimization improves layout for longer descriptions
