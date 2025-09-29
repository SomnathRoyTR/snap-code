# SafDescriptionTerm

## Overview

SafDescriptionTerm is a semantic component that represents the term or label part of a description list item. It works in conjunction with SafDescriptionDetails to create accessible and well-structured definition lists, providing proper semantic markup and flexible styling for term elements.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `required` | `boolean` | `false` | Indicates if the term represents a required field |
| `optional` | `boolean` | `false` | Indicates if the term represents an optional field |
| `interactive` | `boolean` | `false` | Makes the term clickable and focusable |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting typography |
| `variant` | `'default' \| 'emphasized' \| 'subtle'` | `'default'` | Visual style variant |
| `id` | `string` | - | Unique identifier for the term |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Term content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `() => void` | Fired when interactive term is clicked |
| `onFocus` | `(event: FocusEvent) => void` | Fired when term receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when term loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `required` | `boolean` | `false` | Indicates if the term represents a required field |
| `optional` | `boolean` | `false` | Indicates if the term represents an optional field |
| `interactive` | `boolean` | `false` | Makes the term clickable and focusable |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting typography |
| `variant` | `'default' \| 'emphasized' \| 'subtle'` | `'default'` | Visual style variant |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `click` | `EventEmitter<void>` | Fired when interactive term is clicked |
| `focus` | `EventEmitter<FocusEvent>` | Fired when term receives focus |
| `blur` | `EventEmitter<FocusEvent>` | Fired when term loses focus |

## Usage Examples

### Basic Terms

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

### Required and Optional Field Indicators

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm required>Full Name</SafDescriptionTerm>
  <SafDescriptionDetails>This field is required</SafDescriptionDetails>
  
  <SafDescriptionTerm>Job Title</SafDescriptionTerm>
  <SafDescriptionDetails>Required field without explicit indicator</SafDescriptionDetails>
  
  <SafDescriptionTerm optional>Middle Name</SafDescriptionTerm>
  <SafDescriptionDetails>This field is optional</SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term [required]="true">Full Name</saf-description-term>
  <saf-description-details>This field is required</saf-description-details>
  
  <saf-description-term>Job Title</saf-description-term>
  <saf-description-details>Required field without explicit indicator</saf-description-details>
  
  <saf-description-term [optional]="true">Middle Name</saf-description-term>
  <saf-description-details>This field is optional</saf-description-details>
</saf-description-list>
```

### Interactive Terms

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm 
    interactive 
    onClick={() => showLocationDetails()}
  >
    Office Location
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    New York Office - Click term for map
  </SafDescriptionDetails>
  
  <SafDescriptionTerm 
    interactive 
    onClick={() => expandContactInfo()}
  >
    Contact Information
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    Multiple contact methods available
  </SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term 
    [interactive]="true"
    (click)="showLocationDetails()"
  >
    Office Location
  </saf-description-term>
  <saf-description-details>
    New York Office - Click term for map
  </saf-description-details>
  
  <saf-description-term 
    [interactive]="true"
    (click)="expandContactInfo()"
  >
    Contact Information
  </saf-description-term>
  <saf-description-details>
    Multiple contact methods available
  </saf-description-details>
</saf-description-list>
```

### Size Variants

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm size="small">Compact Term</SafDescriptionTerm>
  <SafDescriptionDetails>Smaller text for secondary information</SafDescriptionDetails>
  
  <SafDescriptionTerm size="medium">Standard Term</SafDescriptionTerm>
  <SafDescriptionDetails>Default size for most content</SafDescriptionDetails>
  
  <SafDescriptionTerm size="large">Prominent Term</SafDescriptionTerm>
  <SafDescriptionDetails>Larger text for important headings</SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term size="small">Compact Term</saf-description-term>
  <saf-description-details>Smaller text for secondary information</saf-description-details>
  
  <saf-description-term size="medium">Standard Term</saf-description-term>
  <saf-description-details>Default size for most content</saf-description-details>
  
  <saf-description-term size="large">Prominent Term</saf-description-term>
  <saf-description-details>Larger text for important headings</saf-description-details>
</saf-description-list>
```

### Visual Variants

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm variant="default">Standard Appearance</SafDescriptionTerm>
  <SafDescriptionDetails>Normal term styling</SafDescriptionDetails>
  
  <SafDescriptionTerm variant="emphasized">Important Field</SafDescriptionTerm>
  <SafDescriptionDetails>Bold or highlighted term styling</SafDescriptionDetails>
  
  <SafDescriptionTerm variant="subtle">Secondary Information</SafDescriptionTerm>
  <SafDescriptionDetails>Muted term styling for less important content</SafDescriptionDetails>
</SafDescriptionList>
```

```html
<!-- Angular -->
<saf-description-list>
  <saf-description-term variant="default">Standard Appearance</saf-description-term>
  <saf-description-details>Normal term styling</saf-description-details>
  
  <saf-description-term variant="emphasized">Important Field</saf-description-term>
  <saf-description-details>Bold or highlighted term styling</saf-description-details>
  
  <saf-description-term variant="subtle">Secondary Information</saf-description-term>
  <saf-description-details>Muted term styling for less important content</saf-description-details>
</saf-description-list>
```

### Complex Terms with Icons and Indicators

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm required>
    <SafIcon name="user" size="small" />
    User Account
  </SafDescriptionTerm>
  <SafDescriptionDetails>Active user with full privileges</SafDescriptionDetails>
  
  <SafDescriptionTerm interactive onClick={() => toggleDetails()}>
    <SafIcon name="settings" size="small" />
    Configuration
    <SafIcon name="chevron-down" size="small" />
  </SafDescriptionTerm>
  <SafDescriptionDetails>Click to expand configuration options</SafDescriptionDetails>
  
  <SafDescriptionTerm variant="emphasized">
    <SafIcon name="warning" size="small" color="warning" />
    Security Status
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafStatus variant="warning">Requires Attention</SafStatus>
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Terms with Custom IDs for Navigation

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm id="personal-info">Personal Information</SafDescriptionTerm>
  <SafDescriptionDetails>Basic user profile data</SafDescriptionDetails>
  
  <SafDescriptionTerm id="work-info">Work Information</SafDescriptionTerm>
  <SafDescriptionDetails>Employment and role details</SafDescriptionDetails>
  
  <SafDescriptionTerm id="contact-info">Contact Details</SafDescriptionTerm>
  <SafDescriptionDetails>Phone, email, and address information</SafDescriptionDetails>
</SafDescriptionList>

// Navigate to specific term
const scrollToTerm = (termId: string) => {
  document.getElementById(termId)?.scrollIntoView({ behavior: 'smooth' });
};
```

### Form Field Terms

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm required>
    <label htmlFor="firstName">First Name</label>
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafTextField id="firstName" placeholder="Enter first name" />
  </SafDescriptionDetails>
  
  <SafDescriptionTerm optional>
    <label htmlFor="middleName">Middle Name</label>
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafTextField id="middleName" placeholder="Optional middle name" />
  </SafDescriptionDetails>
  
  <SafDescriptionTerm required>
    <label htmlFor="email">Email Address</label>
  </SafDescriptionTerm>
  <SafDescriptionDetails>
    <SafTextField 
      id="email" 
      type="email" 
      placeholder="Enter email address"
      helperText="Must be a valid email format"
    />
  </SafDescriptionDetails>
</SafDescriptionList>
```

### Responsive Terms with Abbreviations

```typescript
// React
<SafDescriptionList>
  <SafDescriptionTerm>
    <abbr title="Social Security Number">SSN</abbr>
  </SafDescriptionTerm>
  <SafDescriptionDetails>***-**-1234</SafDescriptionDetails>
  
  <SafDescriptionTerm>
    <abbr title="Date of Birth">DOB</abbr>
  </SafDescriptionTerm>
  <SafDescriptionDetails>January 15, 1990</SafDescriptionDetails>
  
  <SafDescriptionTerm>
    <abbr title="Emergency Contact">Emergency Contact</abbr>
  </SafDescriptionTerm>
  <SafDescriptionDetails>Jane Smith - (555) 123-4567</SafDescriptionDetails>
</SafDescriptionList>
```

## Best Practices

### Content Guidelines
- **Clear Labels**: Use descriptive, unambiguous terms
- **Consistent Style**: Maintain consistent terminology and capitalization
- **Logical Order**: Arrange terms in logical or hierarchical sequence
- **Appropriate Length**: Keep terms concise while remaining descriptive

### Interaction Design
- **Interactive Indicators**: Clearly indicate when terms are clickable
- **Feedback**: Provide visual feedback for interactive states
- **Accessibility**: Ensure interactive terms are keyboard accessible
- **Purpose**: Use interactivity only when it adds meaningful functionality

### Visual Hierarchy
- **Required Fields**: Clearly mark required terms when appropriate
- **Emphasis**: Use variants to create proper information hierarchy
- **Sizing**: Match term size to content importance and context
- **Consistency**: Maintain visual consistency within description lists

### Form Integration
- **Label Association**: Properly associate terms with form controls
- **Validation States**: Reflect field validation states in term appearance
- **Help Text**: Use descriptions to provide additional guidance
- **Error Handling**: Consider how terms should appear during error states

## Accessibility Considerations

- Uses semantic `<dt>` HTML element for proper document structure
- Maintains proper association with corresponding description details
- Supports keyboard navigation and focus management
- Provides appropriate ARIA attributes for interactive terms
- Ensures sufficient color contrast for all visual variants
- Supports screen reader announcements for required/optional indicators

## Related Components

- **SafDescriptionDetails**: Companion component for description content
- **SafDescriptionList**: Container component for organizing term-detail pairs
- **SafMetadataItem**: Alternative component for simple key-value displays
- **SafFieldLabel**: Dedicated component for form field labeling
- **SafFormField**: Complete form field component with integrated labeling

## Notes

- SafDescriptionTerm should always be used within a SafDescriptionList
- Interactive terms automatically receive appropriate ARIA attributes
- Required and optional indicators are automatically announced by screen readers
- The component maintains semantic structure while providing flexible styling
- Visual variants can be combined with size and interaction properties
- Consider using SafFieldLabel for dedicated form field scenarios
