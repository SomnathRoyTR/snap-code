# SafStatus

## Overview

SafStatus is a versatile component for displaying status information with appropriate visual styling and semantic meaning. It provides consistent status indicators across applications with support for various states, sizes, and customization options including icons and interactive behaviors.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'success' \| 'warning' \| 'error' \| 'info' \| 'neutral' \| 'pending'` | `'neutral'` | Status type determining color and icon |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting dimensions and typography |
| `appearance` | `'filled' \| 'outline' \| 'text' \| 'dot'` | `'filled'` | Visual appearance style |
| `icon` | `string \| ReactElement` | - | Custom icon (overrides default variant icon) |
| `showIcon` | `boolean` | `true` | Whether to display status icon |
| `interactive` | `boolean` | `false` | Makes status clickable and focusable |
| `disabled` | `boolean` | `false` | Disables interaction and applies disabled styling |
| `loading` | `boolean` | `false` | Shows loading spinner instead of status icon |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Status text content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(event: MouseEvent) => void` | Fired when interactive status is clicked |
| `onFocus` | `(event: FocusEvent) => void` | Fired when status receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when status loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'success' \| 'warning' \| 'error' \| 'info' \| 'neutral' \| 'pending'` | `'neutral'` | Status type determining color and icon |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting dimensions and typography |
| `appearance` | `'filled' \| 'outline' \| 'text' \| 'dot'` | `'filled'` | Visual appearance style |
| `icon` | `string` | - | Custom icon name (overrides default variant icon) |
| `showIcon` | `boolean` | `true` | Whether to display status icon |
| `interactive` | `boolean` | `false` | Makes status clickable and focusable |
| `disabled` | `boolean` | `false` | Disables interaction and applies disabled styling |
| `loading` | `boolean` | `false` | Shows loading spinner instead of status icon |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `click` | `EventEmitter<MouseEvent>` | Fired when interactive status is clicked |
| `focus` | `EventEmitter<FocusEvent>` | Fired when status receives focus |
| `blur` | `EventEmitter<FocusEvent>` | Fired when status loses focus |

## Usage Examples

### Basic Status Indicators

```typescript
// React
<SafStatus variant="success">Completed</SafStatus>
<SafStatus variant="warning">Pending Review</SafStatus>
<SafStatus variant="error">Failed</SafStatus>
<SafStatus variant="info">Processing</SafStatus>
<SafStatus variant="neutral">Draft</SafStatus>
<SafStatus variant="pending">In Queue</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="success">Completed</saf-status>
<saf-status variant="warning">Pending Review</saf-status>
<saf-status variant="error">Failed</saf-status>
<saf-status variant="info">Processing</saf-status>
<saf-status variant="neutral">Draft</saf-status>
<saf-status variant="pending">In Queue</saf-status>
```

### Size Variants

```typescript
// React
<SafStatus variant="success" size="small">Complete</SafStatus>
<SafStatus variant="warning" size="medium">In Progress</SafStatus>
<SafStatus variant="error" size="large">Critical Error</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="success" size="small">Complete</saf-status>
<saf-status variant="warning" size="medium">In Progress</saf-status>
<saf-status variant="error" size="large">Critical Error</saf-status>
```

### Appearance Variants

```typescript
// React
<SafStatus variant="success" appearance="filled">Filled Style</SafStatus>
<SafStatus variant="warning" appearance="outline">Outline Style</SafStatus>
<SafStatus variant="error" appearance="text">Text Only</SafStatus>
<SafStatus variant="info" appearance="dot">With Dot</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="success" appearance="filled">Filled Style</saf-status>
<saf-status variant="warning" appearance="outline">Outline Style</saf-status>
<saf-status variant="error" appearance="text">Text Only</saf-status>
<saf-status variant="info" appearance="dot">With Dot</saf-status>
```

### Custom Icons

```typescript
// React
<SafStatus variant="success" icon="check-circle">Custom Success</SafStatus>
<SafStatus variant="warning" icon="alert-triangle">Custom Warning</SafStatus>
<SafStatus variant="error" icon={<CustomErrorIcon />}>JSX Icon</SafStatus>
<SafStatus variant="info" showIcon={false}>No Icon</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="success" icon="check-circle">Custom Success</saf-status>
<saf-status variant="warning" icon="alert-triangle">Custom Warning</saf-status>
<saf-status variant="info" [showIcon]="false">No Icon</saf-status>
```

### Interactive Status

```typescript
// React
<SafStatus 
  variant="warning" 
  interactive 
  onClick={() => showDetails()}
>
  Click for Details
</SafStatus>

<SafStatus 
  variant="error" 
  interactive 
  onClick={() => retryOperation()}
>
  Retry Failed Operation
</SafStatus>

<SafStatus 
  variant="pending" 
  interactive 
  onClick={() => cancelOperation()}
>
  Cancel Process
</SafStatus>
```

```html
<!-- Angular -->
<saf-status 
  variant="warning" 
  [interactive]="true"
  (click)="showDetails()"
>
  Click for Details
</saf-status>

<saf-status 
  variant="error" 
  [interactive]="true"
  (click)="retryOperation()"
>
  Retry Failed Operation
</saf-status>
```

### Loading States

```typescript
// React
<SafStatus variant="pending" loading>Loading...</SafStatus>
<SafStatus variant="info" loading>Processing Request</SafStatus>
<SafStatus variant="neutral" loading>Initializing</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="pending" [loading]="true">Loading...</saf-status>
<saf-status variant="info" [loading]="true">Processing Request</saf-status>
<saf-status variant="neutral" [loading]="true">Initializing</saf-status>
```

### Disabled States

```typescript
// React
<SafStatus variant="success" disabled>Disabled Success</SafStatus>
<SafStatus variant="warning" interactive disabled>Disabled Interactive</SafStatus>
```

```html
<!-- Angular -->
<saf-status variant="success" [disabled]="true">Disabled Success</saf-status>
<saf-status variant="warning" [interactive]="true" [disabled]="true">
  Disabled Interactive
</saf-status>
```

### Data Table Status Column

```typescript
// React
const TaskTable = () => {
  const tasks = [
    { id: 1, name: 'Setup Database', status: 'success' },
    { id: 2, name: 'API Integration', status: 'pending' },
    { id: 3, name: 'UI Polish', status: 'warning' },
    { id: 4, name: 'Testing', status: 'error' }
  ];

  return (
    <SafTable>
      <SafTableHead>
        <SafTableRow>
          <SafTableHeaderCell>Task</SafTableHeaderCell>
          <SafTableHeaderCell>Status</SafTableHeaderCell>
        </SafTableRow>
      </SafTableHead>
      <SafTableBody>
        {tasks.map(task => (
          <SafTableRow key={task.id}>
            <SafTableCell>{task.name}</SafTableCell>
            <SafTableCell>
              <SafStatus 
                variant={task.status}
                size="small"
                interactive
                onClick={() => viewTaskDetails(task.id)}
              >
                {getStatusText(task.status)}
              </SafStatus>
            </SafTableCell>
          </SafTableRow>
        ))}
      </SafTableBody>
    </SafTable>
  );
};
```

### Card Status Headers

```typescript
// React
<SafCard>
  <SafCardHeader>
    <SafCardTitle>Project Alpha</SafCardTitle>
    <SafStatus variant="success" appearance="outline">
      Active
    </SafStatus>
  </SafCardHeader>
  <SafCardContent>
    Project details and information...
  </SafCardContent>
</SafCard>

<SafCard>
  <SafCardHeader>
    <SafCardTitle>Project Beta</SafCardTitle>
    <SafStatus variant="warning" appearance="outline">
      Under Review
    </SafStatus>
  </SafCardHeader>
  <SafCardContent>
    Project details and information...
  </SafCardContent>
</SafCard>
```

### Form Field Status

```typescript
// React
<SafFormField>
  <SafFieldLabel>
    Email Address
    <SafStatus variant="success" size="small" appearance="text">
      Verified
    </SafStatus>
  </SafFieldLabel>
  <SafTextField 
    value="user@example.com"
    helperText="Email has been verified"
  />
</SafFormField>

<SafFormField>
  <SafFieldLabel>
    Phone Number
    <SafStatus variant="warning" size="small" appearance="text">
      Pending Verification
    </SafStatus>
  </SafFieldLabel>
  <SafTextField 
    value="+1 555-123-4567"
    helperText="Verification code sent"
  />
</SafFormField>
```

### List Item Status

```typescript
// React
<SafList>
  <SafListItem>
    <SafListItemText 
      primary="Database Migration"
      secondary="Completed at 3:45 PM"
    />
    <SafStatus variant="success" size="small">Done</SafStatus>
  </SafListItem>
  
  <SafListItem>
    <SafListItemText 
      primary="API Deployment"
      secondary="Started 5 minutes ago"
    />
    <SafStatus variant="pending" size="small" loading>
      In Progress
    </SafStatus>
  </SafListItem>
  
  <SafListItem>
    <SafListItemText 
      primary="Security Scan"
      secondary="Failed with 3 issues"
    />
    <SafStatus 
      variant="error" 
      size="small" 
      interactive 
      onClick={() => viewIssues()}
    >
      Failed
    </SafStatus>
  </SafListItem>
</SafList>
```

### Notification Status

```typescript
// React
<SafNotification>
  <SafStatus variant="success" appearance="text">
    Operation completed successfully
  </SafStatus>
  <SafButton variant="text" size="small">Dismiss</SafButton>
</SafNotification>

<SafNotification>
  <SafStatus variant="error" appearance="text">
    Failed to save changes
  </SafStatus>
  <SafButton variant="text" size="small">Retry</SafButton>
</SafNotification>
```

### Complex Status with Timestamp

```typescript
// React
const StatusWithTime = ({ variant, children, timestamp }) => (
  <div className="status-container">
    <SafStatus variant={variant} size="small">
      {children}
    </SafStatus>
    <time className="status-timestamp">
      {new Date(timestamp).toLocaleString()}
    </time>
  </div>
);

<StatusWithTime variant="success" timestamp="2024-01-15T10:30:00Z">
  Deployed
</StatusWithTime>

<StatusWithTime variant="error" timestamp="2024-01-15T09:15:00Z">
  Build Failed
</StatusWithTime>
```

## Best Practices

### Status Selection
- **Semantic Meaning**: Choose variants that accurately reflect the actual status
- **Consistency**: Use consistent status meanings across your application
- **User Understanding**: Ensure status meanings are clear to your users
- **Color Independence**: Don't rely solely on color to convey meaning

### Visual Hierarchy
- **Size Appropriately**: Match status size to its importance and context
- **Appearance Selection**: Choose appearances that fit the overall design
- **Icon Usage**: Use icons to reinforce meaning, especially for accessibility
- **Layout Consideration**: Position status appropriately within layouts

### Interaction Design
- **Meaningful Actions**: Only make status interactive when it provides value
- **Clear Affordances**: Indicate interactive status with appropriate styling
- **Consistent Behavior**: Maintain consistent interaction patterns
- **Loading States**: Use loading states for operations that take time

### Content Guidelines
- **Concise Text**: Keep status text brief and descriptive
- **Active Voice**: Use active language that clearly communicates state
- **User-Friendly**: Avoid technical jargon in user-facing status messages
- **Actionable Information**: When possible, indicate what users can do

## Accessibility Considerations

- Uses appropriate semantic markup and ARIA attributes
- Provides sufficient color contrast for all variants
- Supports keyboard navigation for interactive status
- Includes screen reader announcements for status changes
- Uses icons and text together to convey meaning
- Respects user preferences for reduced motion in loading states

## Related Components

- **SafBadge**: Alternative component for notification counts and labels
- **SafChip**: Related component for categorization and tagging
- **SafProgressBar**: Complementary component for showing progress
- **SafSpinner**: Loading indicator component
- **SafAlert**: Comprehensive component for status messages with actions
- **SafToast**: Temporary status notifications

## Notes

- SafStatus automatically provides appropriate default icons for each variant
- Loading states replace the status icon with a spinner animation
- Interactive status components receive proper focus management
- The component supports both string icons (by name) and React elements
- Visual appearances can be mixed with different variants for flexible styling
- Disabled states maintain visual hierarchy while preventing interaction
- The component is optimized for use in data-dense interfaces like tables and lists
