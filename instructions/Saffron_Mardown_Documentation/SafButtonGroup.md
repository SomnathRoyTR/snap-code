# SafButtonGroup - Button Container Component

## Overview
`SafButtonGroup` is a container component that groups related buttons together with consistent spacing and visual treatment. It supports horizontal and vertical orientations and applies appropriate styling to child buttons.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `aria-label` | `string` | `undefined` | Label to identify the button group |
| `role` | `string` | `'group'` | ARIA role for the container |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `density` | `'compact' \| 'standard'` | `'inherit'` | Size density |

### Slots
| Slot | Description |
|------|-------------|
| (default) | Buttons to group together |

### CSS Parts
| Part | Description |
|------|-------------|
| `base` | The root container element |

## Usage Examples

### Basic Horizontal Button Group
```typescript
// React
import { SafButtonGroup, SafButton } from '@saffron/react';

export const BasicButtonGroup = () => {
  return (
    <SafButtonGroup aria-label="Text formatting options">
      <SafButton appearance="ghost">Bold</SafButton>
      <SafButton appearance="ghost">Italic</SafButton>
      <SafButton appearance="ghost">Underline</SafButton>
    </SafButtonGroup>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-button-group aria-label="Text formatting options">
      <saf-button appearance="ghost">Bold</saf-button>
      <saf-button appearance="ghost">Italic</saf-button>
      <saf-button appearance="ghost">Underline</saf-button>
    </saf-button-group>
  `
})
export class BasicButtonGroupComponent {}
```

### Vertical Button Group
```typescript
// React
export const VerticalButtonGroup = () => {
  return (
    <SafButtonGroup 
      orientation="vertical" 
      aria-label="Navigation options"
    >
      <SafButton appearance="outline">Dashboard</SafButton>
      <SafButton appearance="outline">Reports</SafButton>
      <SafButton appearance="outline">Settings</SafButton>
      <SafButton appearance="outline">Help</SafButton>
    </SafButtonGroup>
  );
};
```

### Action Button Group
```typescript
// React
export const ActionButtonGroup = () => {
  const [selectedAction, setSelectedAction] = useState<string | null>(null);
  
  return (
    <SafButtonGroup aria-label="Document actions">
      <SafButton 
        appearance={selectedAction === 'edit' ? 'primary' : 'ghost'}
        onClick={() => setSelectedAction('edit')}
      >
        Edit
      </SafButton>
      <SafButton 
        appearance={selectedAction === 'share' ? 'primary' : 'ghost'}
        onClick={() => setSelectedAction('share')}
      >
        Share
      </SafButton>
      <SafButton 
        appearance={selectedAction === 'download' ? 'primary' : 'ghost'}
        onClick={() => setSelectedAction('download')}
      >
        Download
      </SafButton>
      <SafButton 
        appearance="ghost" 
        onClick={() => setSelectedAction('delete')}
      >
        Delete
      </SafButton>
    </SafButtonGroup>
  );
};
```

### Toolbar Button Group
```typescript
// React
export const ToolbarButtonGroup = () => {
  return (
    <SafButtonGroup 
      aria-label="Text formatting toolbar"
      density="compact"
    >
      <SafButton appearance="ghost" title="Bold">
        <saf-icon icon-name="text-bold" />
      </SafButton>
      <SafButton appearance="ghost" title="Italic">
        <saf-icon icon-name="text-italic" />
      </SafButton>
      <SafButton appearance="ghost" title="Underline">
        <saf-icon icon-name="text-underline" />
      </SafButton>
      <SafButton appearance="ghost" title="Strike through">
        <saf-icon icon-name="text-strikethrough" />
      </SafButton>
    </SafButtonGroup>
  );
};
```

### Form Button Group
```typescript
// React
export const FormButtonGroup = () => {
  const handleSave = () => console.log('Saving...');
  const handleCancel = () => console.log('Cancelled');
  const handleReset = () => console.log('Reset form');
  
  return (
    <SafButtonGroup aria-label="Form actions">
      <SafButton 
        appearance="primary" 
        onClick={handleSave}
        type="submit"
      >
        Save Changes
      </SafButton>
      <SafButton 
        appearance="outline" 
        onClick={handleCancel}
        type="button"
      >
        Cancel
      </SafButton>
      <SafButton 
        appearance="ghost" 
        onClick={handleReset}
        type="reset"
      >
        Reset
      </SafButton>
    </SafButtonGroup>
  );
};
```

### Toggle Button Group
```typescript
// React
export const ToggleButtonGroup = () => {
  const [selectedView, setSelectedView] = useState('list');
  
  const views = [
    { value: 'list', label: 'List View', icon: 'list' },
    { value: 'grid', label: 'Grid View', icon: 'grid' },
    { value: 'card', label: 'Card View', icon: 'card' }
  ];
  
  return (
    <SafButtonGroup aria-label="View options" role="radiogroup">
      {views.map(view => (
        <SafButton
          key={view.value}
          appearance={selectedView === view.value ? 'primary' : 'ghost'}
          onClick={() => setSelectedView(view.value)}
          role="radio"
          aria-checked={selectedView === view.value}
          aria-label={view.label}
        >
          <saf-icon icon-name={view.icon} />
          {view.label}
        </SafButton>
      ))}
    </SafButtonGroup>
  );
};
```

### Split Button Group
```typescript
// React
export const SplitButtonGroup = () => {
  const [showDropdown, setShowDropdown] = useState(false);
  
  const handlePrimaryAction = () => {
    console.log('Primary action executed');
  };
  
  const handleMenuToggle = () => {
    setShowDropdown(!showDropdown);
  };
  
  return (
    <div style={{ position: 'relative' }}>
      <SafButtonGroup aria-label="Split button actions">
        <SafButton 
          appearance="primary" 
          onClick={handlePrimaryAction}
        >
          Send Email
        </SafButton>
        <SafButton 
          appearance="primary" 
          onClick={handleMenuToggle}
          aria-expanded={showDropdown}
          aria-haspopup="menu"
        >
          <saf-icon icon-name="chevron-down" />
        </SafButton>
      </SafButtonGroup>
      
      {showDropdown && (
        <SafMenu>
          <SafMenuItem>Send Later</SafMenuItem>
          <SafMenuItem>Schedule</SafMenuItem>
          <SafMenuItem>Save as Draft</SafMenuItem>
        </SafMenu>
      )}
    </div>
  );
};
```

### Pagination Button Group
```typescript
// React
export const PaginationButtonGroup = () => {
  const [currentPage, setCurrentPage] = useState(3);
  const totalPages = 10;
  
  const goToPage = (page: number) => {
    setCurrentPage(Math.max(1, Math.min(totalPages, page)));
  };
  
  return (
    <SafButtonGroup aria-label="Pagination navigation">
      <SafButton 
        appearance="ghost"
        onClick={() => goToPage(currentPage - 1)}
        disabled={currentPage === 1}
        aria-label="Previous page"
      >
        <saf-icon icon-name="chevron-left" />
        Previous
      </SafButton>
      
      {[1, 2, 3, 4, 5].map(page => (
        <SafButton
          key={page}
          appearance={currentPage === page ? 'primary' : 'ghost'}
          onClick={() => goToPage(page)}
          aria-label={`Go to page ${page}`}
          aria-current={currentPage === page ? 'page' : undefined}
        >
          {page}
        </SafButton>
      ))}
      
      <SafButton 
        appearance="ghost"
        onClick={() => goToPage(currentPage + 1)}
        disabled={currentPage === totalPages}
        aria-label="Next page"
      >
        Next
        <saf-icon icon-name="chevron-right" />
      </SafButton>
    </SafButtonGroup>
  );
};
```

## Accessibility Features

- **ARIA Labeling**: Requires aria-label for screen reader identification
- **Role Support**: Supports group, toolbar, radiogroup roles
- **Focus Management**: Maintains logical tab order between buttons
- **Keyboard Navigation**: Arrow keys for radio group behavior when appropriate
- **Screen Reader Support**: Announces group context and relationships
- **High Contrast**: Maintains button visibility in high contrast mode

## Best Practices

1. **Labeling**: Always provide meaningful aria-label
2. **Related Actions**: Only group logically related buttons
3. **Button Count**: Keep groups to 2-7 buttons for optimal UX
4. **Visual Hierarchy**: Use consistent button appearances within groups
5. **Spacing**: Let the component handle spacing automatically
6. **Responsive**: Consider orientation changes on smaller screens
7. **State Management**: Coordinate button states when appropriate

## Advanced Usage

### Responsive Button Group
```typescript
// React
export const ResponsiveButtonGroup = () => {
  const [orientation, setOrientation] = useState('horizontal');
  
  useEffect(() => {
    const handleResize = () => {
      setOrientation(window.innerWidth < 600 ? 'vertical' : 'horizontal');
    };
    
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);
  
  return (
    <SafButtonGroup 
      orientation={orientation}
      aria-label="Responsive actions"
    >
      <SafButton appearance="primary">Action 1</SafButton>
      <SafButton appearance="outline">Action 2</SafButton>
      <SafButton appearance="ghost">Action 3</SafButton>
    </SafButtonGroup>
  );
};
```

### Dynamic Button Group
```typescript
// React
export const DynamicButtonGroup = () => {
  const [actions, setActions] = useState([
    { id: 1, label: 'Edit', enabled: true },
    { id: 2, label: 'Share', enabled: true },
    { id: 3, label: 'Delete', enabled: false }
  ]);
  
  const toggleAction = (id: number) => {
    setActions(prev => prev.map(action => 
      action.id === id ? { ...action, enabled: !action.enabled } : action
    ));
  };
  
  return (
    <SafButtonGroup aria-label="Dynamic actions">
      {actions.map(action => (
        <SafButton
          key={action.id}
          appearance={action.enabled ? 'primary' : 'ghost'}
          onClick={() => toggleAction(action.id)}
          disabled={!action.enabled}
        >
          {action.label}
        </SafButton>
      ))}
    </SafButtonGroup>
  );
};
```

## Styling

### Custom CSS Properties
```css
saf-button-group {
  --button-group-gap: 0; /* Space between buttons */
  --button-group-border-radius: 4px; /* Corner radius */
}

/* Vertical orientation */
saf-button-group[orientation="vertical"] {
  --button-group-gap: 1px;
}
```

### Button Group Variants
```css
/* Toolbar style */
.toolbar saf-button-group {
  --button-group-gap: 1px;
  border: 1px solid var(--neutral-stroke-divider);
  border-radius: 4px;
}

/* Segmented control style */
.segmented saf-button-group {
  --button-group-gap: 0;
  background: var(--neutral-layer-2);
  border-radius: 8px;
  padding: 2px;
}
```

## Notes

- Automatically applies group-specific styling to child buttons
- Maintains semantic button relationships for assistive technology
- Supports both horizontal and vertical layouts
- Handles focus management and keyboard navigation
- Integrates with existing button appearance and state management
- Provides consistent spacing and visual treatment
