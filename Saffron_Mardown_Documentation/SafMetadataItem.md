# SafMetadataItem Component

## Overview
The `SafMetadataItem` component represents a single key-value pair within a metadata display. It provides a structured way to present individual pieces of information with consistent formatting, labeling, and styling. This component is designed to work within `SafMetadata` containers and supports various content types, alignment options, and interactive elements.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string` | `undefined` | The label/key for the metadata item |
| `value` | `string \| ReactNode` | `undefined` | The value/content for the metadata item |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Layout orientation of label and value |
| `labelWidth` | `string \| number` | `undefined` | Fixed width for the label (e.g., '120px', 120) |
| `alignment` | `'start' \| 'center' \| 'end'` | `'start'` | Alignment of content within the item |
| `truncate` | `boolean` | `false` | Whether to truncate long content with ellipsis |
| `copyable` | `boolean` | `false` | Whether the value can be copied to clipboard |
| `editable` | `boolean` | `false` | Whether the value is editable inline |
| `required` | `boolean` | `false` | Whether the item is required (visual indicator) |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant for text and spacing |
| `onEdit` | `(newValue: string) => void` | `undefined` | Callback for edit completion |
| `onCopy` | `(value: string) => void` | `undefined` | Callback when value is copied |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Custom content (overrides value prop) |

### Events
- `onEdit`: Fired when inline editing is completed
- `onCopy`: Fired when the copy action is triggered
- `onFocus`: Fired when the item receives focus
- `onBlur`: Fired when the item loses focus

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string` | `undefined` | The label/key for the metadata item |
| `value` | `string` | `undefined` | The value/content for the metadata item |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Layout orientation of label and value |
| `labelWidth` | `string \| number` | `undefined` | Fixed width for the label |
| `alignment` | `'start' \| 'center' \| 'end'` | `'start'` | Alignment of content within the item |
| `truncate` | `boolean` | `false` | Whether to truncate long content |
| `copyable` | `boolean` | `false` | Whether the value can be copied |
| `editable` | `boolean` | `false` | Whether the value is editable inline |
| `required` | `boolean` | `false` | Whether the item is required |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(edit)` | `EventEmitter<string>` | Emitted when editing is completed |
| `(copy)` | `EventEmitter<string>` | Emitted when copy is triggered |
| `(focus)` | `EventEmitter<FocusEvent>` | Emitted on focus |
| `(blur)` | `EventEmitter<FocusEvent>` | Emitted on blur |

### Content Projection
- **Default slot**: Custom value content
- **`label` slot**: Custom label content
- **`actions` slot**: Action buttons (copy, edit, etc.)

## Usage Examples

### Basic Metadata Items

#### React
```jsx
import { SafMetadata, SafMetadataItem } from '@saffron/core-components';

function BasicMetadataItemExample() {
  return (
    <SafMetadata>
      <SafMetadataItem 
        label="First Name" 
        value="John" 
      />
      
      <SafMetadataItem 
        label="Last Name" 
        value="Smith" 
      />
      
      <SafMetadataItem 
        label="Email Address" 
        value="john.smith@company.com" 
      />
      
      <SafMetadataItem 
        label="Phone Number" 
        value="+1 (555) 123-4567" 
      />
      
      <SafMetadataItem 
        label="Department" 
        value="Software Engineering" 
      />
    </SafMetadata>
  );
}
```

#### Angular
```html
<saf-metadata>
  <saf-metadata-item 
    label="First Name" 
    value="John">
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Last Name" 
    value="Smith">
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Email Address" 
    value="john.smith@company.com">
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Phone Number" 
    value="+1 (555) 123-4567">
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Department" 
    value="Software Engineering">
  </saf-metadata-item>
</saf-metadata>
```

### Horizontal Layout with Custom Content

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge, SafIcon, SafButton } from '@saffron/core-components';

function HorizontalMetadataItemExample() {
  return (
    <SafMetadata>
      <SafMetadataItem 
        label="Status" 
        orientation="horizontal"
        labelWidth={100}
      >
        <SafBadge variant="success">Active</SafBadge>
      </SafMetadataItem>
      
      <SafMetadataItem 
        label="Priority" 
        orientation="horizontal"
        labelWidth={100}
      >
        <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
          <SafIcon name="flag" color="error" />
          <span>High</span>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem 
        label="Assignee" 
        orientation="horizontal"
        labelWidth={100}
      >
        <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
          <SafIcon name="user" />
          <span>Jane Doe</span>
          <SafButton variant="ghost" size="small">
            Change
          </SafButton>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem 
        label="Due Date" 
        value="December 31, 2024"
        orientation="horizontal"
        labelWidth={100}
      />
    </SafMetadata>
  );
}
```

#### Angular
```html
<saf-metadata>
  <saf-metadata-item 
    label="Status" 
    orientation="horizontal"
    [labelWidth]="100">
    <saf-badge variant="success">Active</saf-badge>
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Priority" 
    orientation="horizontal"
    [labelWidth]="100">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <saf-icon name="flag" color="error"></saf-icon>
      <span>High</span>
    </div>
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Assignee" 
    orientation="horizontal"
    [labelWidth]="100">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <saf-icon name="user"></saf-icon>
      <span>Jane Doe</span>
      <saf-button variant="ghost" size="small">
        Change
      </saf-button>
    </div>
  </saf-metadata-item>
  
  <saf-metadata-item 
    label="Due Date" 
    value="December 31, 2024"
    orientation="horizontal"
    [labelWidth]="100">
  </saf-metadata-item>
</saf-metadata>
```

### Copyable and Editable Items

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafToast } from '@saffron/core-components';
import { useState } from 'react';

function CopyableEditableExample() {
  const [apiKey, setApiKey] = useState('sk-1234567890abcdef');
  const [userName, setUserName] = useState('john.smith');
  const [email, setEmail] = useState('john.smith@company.com');

  const handleCopy = (value) => {
    navigator.clipboard.writeText(value);
    SafToast.show({
      message: 'Copied to clipboard!',
      variant: 'success',
      duration: 2000
    });
  };

  const handleEdit = (field, newValue) => {
    switch (field) {
      case 'userName':
        setUserName(newValue);
        break;
      case 'email':
        setEmail(newValue);
        break;
    }
    SafToast.show({
      message: 'Updated successfully!',
      variant: 'success',
      duration: 2000
    });
  };

  return (
    <SafMetadata>
      <SafMetadataItem 
        label="API Key"
        value={apiKey}
        copyable
        truncate
        onCopy={handleCopy}
      />
      
      <SafMetadataItem 
        label="Username"
        value={userName}
        editable
        required
        onEdit={(value) => handleEdit('userName', value)}
      />
      
      <SafMetadataItem 
        label="Email"
        value={email}
        copyable
        editable
        onCopy={handleCopy}
        onEdit={(value) => handleEdit('email', value)}
      />
      
      <SafMetadataItem 
        label="Account ID"
        value="acc_9876543210"
        copyable
        onCopy={handleCopy}
      />
      
      <SafMetadataItem 
        label="Server URL"
        value="https://api.company.com/v1/users/profile"
        copyable
        truncate
        onCopy={handleCopy}
      />
    </SafMetadata>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-copyable-editable',
  template: `
    <saf-metadata>
      <saf-metadata-item 
        label="API Key"
        [value]="apiKey"
        [copyable]="true"
        [truncate]="true"
        (copy)="handleCopy($event)">
      </saf-metadata-item>
      
      <saf-metadata-item 
        label="Username"
        [value]="userName"
        [editable]="true"
        [required]="true"
        (edit)="handleEdit('userName', $event)">
      </saf-metadata-item>
      
      <saf-metadata-item 
        label="Email"
        [value]="email"
        [copyable]="true"
        [editable]="true"
        (copy)="handleCopy($event)"
        (edit)="handleEdit('email', $event)">
      </saf-metadata-item>
      
      <saf-metadata-item 
        label="Account ID"
        value="acc_9876543210"
        [copyable]="true"
        (copy)="handleCopy($event)">
      </saf-metadata-item>
      
      <saf-metadata-item 
        label="Server URL"
        value="https://api.company.com/v1/users/profile"
        [copyable]="true"
        [truncate]="true"
        (copy)="handleCopy($event)">
      </saf-metadata-item>
    </saf-metadata>
  `
})
export class CopyableEditableComponent {
  apiKey = 'sk-1234567890abcdef';
  userName = 'john.smith';
  email = 'john.smith@company.com';

  async handleCopy(value: string) {
    try {
      await navigator.clipboard.writeText(value);
      // Show success toast
      console.log('Copied to clipboard!');
    } catch (err) {
      console.error('Failed to copy:', err);
    }
  }

  handleEdit(field: string, newValue: string) {
    switch (field) {
      case 'userName':
        this.userName = newValue;
        break;
      case 'email':
        this.email = newValue;
        break;
    }
    console.log('Updated successfully!');
  }
}
```

### Different Sizes and Alignments

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge } from '@saffron/core-components';

function SizesAlignmentExample() {
  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '2rem' }}>
      <div>
        <h3>Small Size</h3>
        <SafMetadata>
          <SafMetadataItem 
            label="Compact Info" 
            value="Small text content"
            size="small"
          />
          <SafMetadataItem 
            label="Status" 
            size="small"
          >
            <SafBadge size="small" variant="info">Pending</SafBadge>
          </SafMetadataItem>
        </SafMetadata>
      </div>
      
      <div>
        <h3>Medium Size (Default)</h3>
        <SafMetadata>
          <SafMetadataItem 
            label="Standard Info" 
            value="Medium text content"
            size="medium"
          />
          <SafMetadataItem 
            label="Status" 
            size="medium"
          >
            <SafBadge variant="success">Active</SafBadge>
          </SafMetadataItem>
        </SafMetadata>
      </div>
      
      <div>
        <h3>Large Size</h3>
        <SafMetadata>
          <SafMetadataItem 
            label="Important Info" 
            value="Large text content for emphasis"
            size="large"
          />
          <SafMetadataItem 
            label="Status" 
            size="large"
          >
            <SafBadge size="large" variant="warning">Alert</SafBadge>
          </SafMetadataItem>
        </SafMetadata>
      </div>
      
      <div>
        <h3>Different Alignments</h3>
        <SafMetadata>
          <SafMetadataItem 
            label="Start Aligned" 
            value="Left aligned content"
            alignment="start"
            orientation="horizontal"
            labelWidth={120}
          />
          <SafMetadataItem 
            label="Center Aligned" 
            value="Center aligned content"
            alignment="center"
            orientation="horizontal"
            labelWidth={120}
          />
          <SafMetadataItem 
            label="End Aligned" 
            value="Right aligned content"
            alignment="end"
            orientation="horizontal"
            labelWidth={120}
          />
        </SafMetadata>
      </div>
    </div>
  );
}
```

#### Angular
```html
<div style="display: flex; flex-direction: column; gap: 2rem;">
  <div>
    <h3>Small Size</h3>
    <saf-metadata>
      <saf-metadata-item 
        label="Compact Info" 
        value="Small text content"
        size="small">
      </saf-metadata-item>
      <saf-metadata-item 
        label="Status" 
        size="small">
        <saf-badge size="small" variant="info">Pending</saf-badge>
      </saf-metadata-item>
    </saf-metadata>
  </div>
  
  <div>
    <h3>Medium Size (Default)</h3>
    <saf-metadata>
      <saf-metadata-item 
        label="Standard Info" 
        value="Medium text content"
        size="medium">
      </saf-metadata-item>
      <saf-metadata-item 
        label="Status" 
        size="medium">
        <saf-badge variant="success">Active</saf-badge>
      </saf-metadata-item>
    </saf-metadata>
  </div>
  
  <div>
    <h3>Large Size</h3>
    <saf-metadata>
      <saf-metadata-item 
        label="Important Info" 
        value="Large text content for emphasis"
        size="large">
      </saf-metadata-item>
      <saf-metadata-item 
        label="Status" 
        size="large">
        <saf-badge size="large" variant="warning">Alert</saf-badge>
      </saf-metadata-item>
    </saf-metadata>
  </div>
  
  <div>
    <h3>Different Alignments</h3>
    <saf-metadata>
      <saf-metadata-item 
        label="Start Aligned" 
        value="Left aligned content"
        alignment="start"
        orientation="horizontal"
        [labelWidth]="120">
      </saf-metadata-item>
      <saf-metadata-item 
        label="Center Aligned" 
        value="Center aligned content"
        alignment="center"
        orientation="horizontal"
        [labelWidth]="120">
      </saf-metadata-item>
      <saf-metadata-item 
        label="End Aligned" 
        value="Right aligned content"
        alignment="end"
        orientation="horizontal"
        [labelWidth]="120">
      </saf-metadata-item>
    </saf-metadata>
  </div>
</div>
```

### Complex Custom Content

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge, SafIcon, SafButton, SafProgress, SafAvatar } from '@saffron/core-components';

function ComplexContentExample() {
  const handleViewDetails = (id) => {
    console.log('View details for:', id);
  };

  return (
    <SafMetadata layout="vertical" spacing="relaxed">
      <SafMetadataItem label="Project Team">
        <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem', flexWrap: 'wrap' }}>
          <SafAvatar name="Alice Johnson" size="small" />
          <SafAvatar name="Bob Smith" size="small" />
          <SafAvatar name="Carol Davis" size="small" />
          <SafAvatar name="+3 more" size="small" variant="neutral" />
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Progress">
        <div style={{ display: 'flex', flexDirection: 'column', gap: '0.5rem' }}>
          <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
            <span>Development</span>
            <span>75%</span>
          </div>
          <SafProgress value={75} max={100} />
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Tags">
        <div style={{ display: 'flex', gap: '0.25rem', flexWrap: 'wrap' }}>
          <SafBadge size="small" variant="info">Frontend</SafBadge>
          <SafBadge size="small" variant="success">React</SafBadge>
          <SafBadge size="small" variant="warning">TypeScript</SafBadge>
          <SafBadge size="small" variant="neutral">UI/UX</SafBadge>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Files">
        <div style={{ display: 'flex', flexDirection: 'column', gap: '0.5rem' }}>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="document" />
            <span>requirements.pdf</span>
            <SafButton 
              variant="ghost" 
              size="small"
              onClick={() => handleViewDetails('requirements.pdf')}
            >
              View
            </SafButton>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="image" />
            <span>wireframes.png</span>
            <SafButton 
              variant="ghost" 
              size="small"
              onClick={() => handleViewDetails('wireframes.png')}
            >
              View
            </SafButton>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="code" />
            <span>prototype.zip</span>
            <SafButton 
              variant="ghost" 
              size="small"
              onClick={() => handleViewDetails('prototype.zip')}
            >
              Download
            </SafButton>
          </div>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Activity Timeline">
        <div style={{ display: 'flex', flexDirection: 'column', gap: '0.75rem' }}>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="check-circle" color="success" size="small" />
            <div>
              <div style={{ fontWeight: '500' }}>Design Review Completed</div>
              <div style={{ fontSize: '0.875rem', color: 'var(--neutral-600)' }}>
                2 hours ago by Alice Johnson
              </div>
            </div>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="clock" color="warning" size="small" />
            <div>
              <div style={{ fontWeight: '500' }}>Development in Progress</div>
              <div style={{ fontSize: '0.875rem', color: 'var(--neutral-600)' }}>
                Started 1 day ago by Bob Smith
              </div>
            </div>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
            <SafIcon name="circle" color="neutral" size="small" />
            <div>
              <div style={{ fontWeight: '500' }}>Testing Phase</div>
              <div style={{ fontSize: '0.875rem', color: 'var(--neutral-600)' }}>
                Scheduled for next week
              </div>
            </div>
          </div>
        </div>
      </SafMetadataItem>
    </SafMetadata>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-complex-content',
  template: `
    <saf-metadata layout="vertical" spacing="relaxed">
      <saf-metadata-item label="Project Team">
        <div style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap;">
          <saf-avatar name="Alice Johnson" size="small"></saf-avatar>
          <saf-avatar name="Bob Smith" size="small"></saf-avatar>
          <saf-avatar name="Carol Davis" size="small"></saf-avatar>
          <saf-avatar name="+3 more" size="small" variant="neutral"></saf-avatar>
        </div>
      </saf-metadata-item>
      
      <saf-metadata-item label="Progress">
        <div style="display: flex; flex-direction: column; gap: 0.5rem;">
          <div style="display: flex; justify-content: space-between; align-items: center;">
            <span>Development</span>
            <span>75%</span>
          </div>
          <saf-progress [value]="75" [max]="100"></saf-progress>
        </div>
      </saf-metadata-item>
      
      <saf-metadata-item label="Tags">
        <div style="display: flex; gap: 0.25rem; flex-wrap: wrap;">
          <saf-badge size="small" variant="info">Frontend</saf-badge>
          <saf-badge size="small" variant="success">React</saf-badge>
          <saf-badge size="small" variant="warning">TypeScript</saf-badge>
          <saf-badge size="small" variant="neutral">UI/UX</saf-badge>
        </div>
      </saf-metadata-item>
      
      <saf-metadata-item label="Files">
        <div style="display: flex; flex-direction: column; gap: 0.5rem;">
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="document"></saf-icon>
            <span>requirements.pdf</span>
            <saf-button 
              variant="ghost" 
              size="small"
              (click)="handleViewDetails('requirements.pdf')">
              View
            </saf-button>
          </div>
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="image"></saf-icon>
            <span>wireframes.png</span>
            <saf-button 
              variant="ghost" 
              size="small"
              (click)="handleViewDetails('wireframes.png')">
              View
            </saf-button>
          </div>
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="code"></saf-icon>
            <span>prototype.zip</span>
            <saf-button 
              variant="ghost" 
              size="small"
              (click)="handleViewDetails('prototype.zip')">
              Download
            </saf-button>
          </div>
        </div>
      </saf-metadata-item>
      
      <saf-metadata-item label="Activity Timeline">
        <div style="display: flex; flex-direction: column; gap: 0.75rem;">
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="check-circle" color="success" size="small"></saf-icon>
            <div>
              <div style="font-weight: 500;">Design Review Completed</div>
              <div style="font-size: 0.875rem; color: var(--neutral-600);">
                2 hours ago by Alice Johnson
              </div>
            </div>
          </div>
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="clock" color="warning" size="small"></saf-icon>
            <div>
              <div style="font-weight: 500;">Development in Progress</div>
              <div style="font-size: 0.875rem; color: var(--neutral-600);">
                Started 1 day ago by Bob Smith
              </div>
            </div>
          </div>
          <div style="display: flex; align-items: center; gap: 0.5rem;">
            <saf-icon name="circle" color="neutral" size="small"></saf-icon>
            <div>
              <div style="font-weight: 500;">Testing Phase</div>
              <div style="font-size: 0.875rem; color: var(--neutral-600);">
                Scheduled for next week
              </div>
            </div>
          </div>
        </div>
      </saf-metadata-item>
    </saf-metadata>
  `
})
export class ComplexContentComponent {
  handleViewDetails(id: string) {
    console.log('View details for:', id);
  }
}
```

## Best Practices

1. **Clear Labels**: Use descriptive, concise labels that clearly identify the content
2. **Consistent Formatting**: Maintain consistent label width and alignment for readability
3. **Appropriate Truncation**: Use truncation for long content with copy functionality
4. **Interactive Elements**: Provide copy and edit functionality where appropriate
5. **Content Hierarchy**: Use appropriate sizes and visual emphasis for important information
6. **Responsive Design**: Consider how items behave on different screen sizes
7. **Loading States**: Handle loading states gracefully for dynamic content
8. **Error Handling**: Provide feedback for copy/edit operations

## Accessibility Considerations

- Use semantic markup for label-value relationships
- Provide clear focus indicators for interactive elements
- Support keyboard navigation for copy and edit actions
- Use appropriate ARIA labels for custom content
- Ensure sufficient color contrast for all text
- Announce changes to screen readers when content is updated
- Support high contrast mode and reduced motion preferences

## Related Components

- `SafMetadata`: Container component for metadata items
- `SafBadge`: For status and category indicators
- `SafIcon`: For visual enhancements and status indicators
- `SafButton`: For interactive elements and actions
- `SafProgress`: For progress indicators within metadata
- `SafAvatar`: For user information display

## Notes

- The component automatically handles responsive behavior when layout changes
- Copy functionality requires modern browser support for Clipboard API
- Inline editing should provide clear visual feedback during edit mode
- Use appropriate content projection slots for complex custom content
- Consider performance implications with large numbers of metadata items
- Truncation works best with horizontal layouts where space is limited
