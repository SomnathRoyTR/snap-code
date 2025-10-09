# SafCheckboxGroup - Checkbox Collection Component

## Overview
`SafCheckboxGroup` is a container component that groups related checkboxes together with shared labeling, validation, and layout. It provides consistent spacing, orientation options, and form integration.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `label` | `string` | `undefined` | Label text for the checkbox group |
| `required` | `boolean` | `false` | Whether at least one selection is required |
| `disabled` | `boolean` | `false` | Whether all checkboxes are disabled |
| `invalid` | `boolean` | `false` | Whether group is in error state |
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Layout orientation |
| `instructional-text` | `string` | `undefined` | Help text for the group |
| `optional-text` | `string` | `undefined` | Optional indicator text |
| `required-text` | `string` | `'*'` | Required indicator text |
| `required-aria-text` | `string` | `'Please select an option'` | ARIA text for required state |
| `validation-message` | `string` | `undefined` | Error or validation message |
| `error-aria-label` | `string` | `'Error'` | ARIA label for error icon |

### Slots
| Slot | Description |
|------|-------------|
| (default) | Checkbox elements |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `change` | `CustomEvent<string[]>` | Fired when selection changes |

### Properties
| Property | Type | Description |
|----------|------|-------------|
| `value` | `string[]` | Array of selected checkbox values |

## Usage Examples

### Basic Checkbox Group
```typescript
// React
import { SafCheckboxGroup, SafCheckbox } from '@saffron/react';

export const BasicCheckboxGroup = () => {
  const [selected, setSelected] = useState([]);
  
  return (
    <SafCheckboxGroup
      label="Select your interests"
      value={selected}
      onChange={(e) => setSelected(e.detail)}
    >
      <SafCheckbox value="technology">Technology</SafCheckbox>
      <SafCheckbox value="design">Design</SafCheckbox>
      <SafCheckbox value="business">Business</SafCheckbox>
      <SafCheckbox value="science">Science</SafCheckbox>
    </SafCheckboxGroup>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-checkbox-group
      label="Select your interests"
      [value]="selectedInterests"
      (change)="onSelectionChange($event)">
      <saf-checkbox value="technology">Technology</saf-checkbox>
      <saf-checkbox value="design">Design</saf-checkbox>
      <saf-checkbox value="business">Business</saf-checkbox>
      <saf-checkbox value="science">Science</saf-checkbox>
    </saf-checkbox-group>
  `
})
export class BasicCheckboxGroupComponent {
  selectedInterests: string[] = [];
  
  onSelectionChange(event: CustomEvent<string[]>) {
    this.selectedInterests = event.detail;
  }
}
```

### Required Checkbox Group with Validation
```typescript
// React
export const RequiredCheckboxGroup = () => {
  const [skills, setSkills] = useState([]);
  const [error, setError] = useState('');
  
  const validateSelection = (values: string[]) => {
    if (values.length === 0) {
      setError('Please select at least one skill');
    } else if (values.length > 3) {
      setError('Please select no more than 3 skills');
    } else {
      setError('');
    }
  };
  
  const handleChange = (values: string[]) => {
    setSkills(values);
    validateSelection(values);
  };
  
  return (
    <SafCheckboxGroup
      label="Technical Skills"
      value={skills}
      onChange={(e) => handleChange(e.detail)}
      required
      invalid={!!error}
      validation-message={error}
      instructional-text="Select 1-3 skills that best describe your expertise"
    >
      <SafCheckbox value="javascript">JavaScript</SafCheckbox>
      <SafCheckbox value="typescript">TypeScript</SafCheckbox>
      <SafCheckbox value="react">React</SafCheckbox>
      <SafCheckbox value="angular">Angular</SafCheckbox>
      <SafCheckbox value="vue">Vue.js</SafCheckbox>
      <SafCheckbox value="node">Node.js</SafCheckbox>
    </SafCheckboxGroup>
  );
};
```

### Horizontal Layout
```typescript
// React
export const HorizontalCheckboxGroup = () => {
  const [preferences, setPreferences] = useState([]);
  
  return (
    <SafCheckboxGroup
      label="Communication Preferences"
      orientation="horizontal"
      value={preferences}
      onChange={(e) => setPreferences(e.detail)}
    >
      <SafCheckbox value="email">Email</SafCheckbox>
      <SafCheckbox value="sms">SMS</SafCheckbox>
      <SafCheckbox value="phone">Phone</SafCheckbox>
      <SafCheckbox value="push">Push Notifications</SafCheckbox>
    </SafCheckboxGroup>
  );
};
```

### Disabled State
```typescript
// React
export const DisabledCheckboxGroup = () => {
  return (
    <SafCheckboxGroup
      label="Unavailable Features"
      disabled
      instructional-text="These features are not available in your current plan"
    >
      <SafCheckbox value="analytics">Advanced Analytics</SafCheckbox>
      <SafCheckbox value="reports">Custom Reports</SafCheckbox>
      <SafCheckbox value="api">API Access</SafCheckbox>
    </SafCheckboxGroup>
  );
};
```

### Permissions Management
```typescript
// React
export const PermissionsCheckboxGroup = () => {
  const [permissions, setPermissions] = useState(['read']);
  
  const permissionOptions = [
    { value: 'read', label: 'Read', description: 'View content' },
    { value: 'write', label: 'Write', description: 'Create and edit content' },
    { value: 'delete', label: 'Delete', description: 'Remove content' },
    { value: 'admin', label: 'Admin', description: 'Full administrative access' }
  ];
  
  return (
    <SafCheckboxGroup
      label="User Permissions"
      value={permissions}
      onChange={(e) => setPermissions(e.detail)}
      required
      instructional-text="Select the permissions for this user role"
    >
      {permissionOptions.map(permission => (
        <SafCheckbox key={permission.value} value={permission.value}>
          <strong>{permission.label}</strong>
          <div style={{ fontSize: '0.875rem', color: '#666' }}>
            {permission.description}
          </div>
        </SafCheckbox>
      ))}
    </SafCheckboxGroup>
  );
};
```

### Multi-Category Selection
```typescript
// React
export const CategoryCheckboxGroup = () => {
  const [categories, setCategories] = useState([]);
  
  const categoryGroups = [
    {
      title: 'Content Types',
      options: [
        { value: 'articles', label: 'Articles' },
        { value: 'videos', label: 'Videos' },
        { value: 'podcasts', label: 'Podcasts' }
      ]
    },
    {
      title: 'Topics',
      options: [
        { value: 'tech', label: 'Technology' },
        { value: 'business', label: 'Business' },
        { value: 'science', label: 'Science' }
      ]
    }
  ];
  
  return (
    <div>
      <h3>Newsletter Preferences</h3>
      {categoryGroups.map(group => (
        <SafCheckboxGroup
          key={group.title}
          label={group.title}
          value={categories}
          onChange={(e) => setCategories(e.detail)}
          style={{ marginBottom: '24px' }}
        >
          {group.options.map(option => (
            <SafCheckbox key={option.value} value={option.value}>
              {option.label}
            </SafCheckbox>
          ))}
        </SafCheckboxGroup>
      ))}
    </div>
  );
};
```

### Form Integration with All/None Options
```typescript
// React
export const FormCheckboxGroup = () => {
  const [selectedFeatures, setSelectedFeatures] = useState([]);
  
  const features = [
    'email-notifications',
    'push-notifications',
    'weekly-digest',
    'promotional-emails',
    'product-updates'
  ];
  
  const selectAll = () => setSelectedFeatures([...features]);
  const selectNone = () => setSelectedFeatures([]);
  const isAllSelected = selectedFeatures.length === features.length;
  const isNoneSelected = selectedFeatures.length === 0;
  
  return (
    <div>
      <div style={{ marginBottom: '16px' }}>
        <SafButton 
          appearance="ghost" 
          onClick={selectAll}
          disabled={isAllSelected}
        >
          Select All
        </SafButton>
        <SafButton 
          appearance="ghost" 
          onClick={selectNone}
          disabled={isNoneSelected}
        >
          Select None
        </SafButton>
      </div>
      
      <SafCheckboxGroup
        label="Notification Preferences"
        value={selectedFeatures}
        onChange={(e) => setSelectedFeatures(e.detail)}
        instructional-text="Choose which notifications you'd like to receive"
      >
        <SafCheckbox value="email-notifications">Email Notifications</SafCheckbox>
        <SafCheckbox value="push-notifications">Push Notifications</SafCheckbox>
        <SafCheckbox value="weekly-digest">Weekly Digest</SafCheckbox>
        <SafCheckbox value="promotional-emails">Promotional Emails</SafCheckbox>
        <SafCheckbox value="product-updates">Product Updates</SafCheckbox>
      </SafCheckboxGroup>
    </div>
  );
};
```

### Conditional Logic
```typescript
// React
export const ConditionalCheckboxGroup = () => {
  const [subscriptions, setSubscriptions] = useState([]);
  const [showAdvanced, setShowAdvanced] = useState(false);
  
  const hasBasicSubscription = subscriptions.includes('basic');
  
  useEffect(() => {
    setShowAdvanced(hasBasicSubscription);
    if (!hasBasicSubscription) {
      // Remove advanced options if basic is unchecked
      setSubscriptions(prev => prev.filter(s => !['premium', 'enterprise'].includes(s)));
    }
  }, [hasBasicSubscription]);
  
  return (
    <div>
      <SafCheckboxGroup
        label="Subscription Plans"
        value={subscriptions}
        onChange={(e) => setSubscriptions(e.detail)}
        required
      >
        <SafCheckbox value="basic">Basic Plan ($9/month)</SafCheckbox>
        {showAdvanced && (
          <>
            <SafCheckbox value="premium">Premium Plan ($19/month)</SafCheckbox>
            <SafCheckbox value="enterprise">Enterprise Plan ($49/month)</SafCheckbox>
          </>
        )}
      </SafCheckboxGroup>
    </div>
  );
};
```

## Accessibility Features

- **Fieldset/Legend**: Uses proper fieldset and legend semantics
- **ARIA Labeling**: Comprehensive ARIA support for screen readers
- **Keyboard Navigation**: Full keyboard support with arrow keys
- **Focus Management**: Logical focus order between checkboxes
- **Error Announcements**: Live regions for validation feedback
- **Required Indication**: Clear indication of required fields
- **Group Context**: Screen readers understand checkbox relationships

## Best Practices

1. **Clear Labels**: Provide descriptive group labels
2. **Logical Grouping**: Only group related checkboxes together
3. **Validation**: Provide immediate feedback for selection rules
4. **Limit Options**: Keep groups to reasonable size (5-10 items)
5. **Layout**: Use vertical for most cases, horizontal for few options
6. **Help Text**: Provide guidance when selection rules apply
7. **Progressive Disclosure**: Consider conditional logic for complex groups

## Advanced Usage

### Dynamic Options
```typescript
// React
export const DynamicCheckboxGroup = () => {
  const [options, setOptions] = useState([]);
  const [selected, setSelected] = useState([]);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      setOptions([
        { id: '1', name: 'Option 1', enabled: true },
        { id: '2', name: 'Option 2', enabled: true },
        { id: '3', name: 'Option 3', enabled: false }
      ]);
      setLoading(false);
    }, 1000);
  }, []);
  
  if (loading) return <SafSkeleton />;
  
  return (
    <SafCheckboxGroup
      label="Dynamic Options"
      value={selected}
      onChange={(e) => setSelected(e.detail)}
    >
      {options.map(option => (
        <SafCheckbox 
          key={option.id} 
          value={option.id}
          disabled={!option.enabled}
        >
          {option.name}
        </SafCheckbox>
      ))}
    </SafCheckboxGroup>
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  interests: string[];
}

export const HookFormCheckboxGroup = () => {
  const { control, handleSubmit } = useForm<FormData>();
  
  return (
    <form onSubmit={handleSubmit(console.log)}>
      <Controller
        name="interests"
        control={control}
        rules={{ 
          required: 'Please select at least one interest',
          validate: value => value.length <= 3 || 'Select no more than 3 interests'
        }}
        render={({ field, fieldState }) => (
          <SafCheckboxGroup
            {...field}
            label="Your Interests"
            required
            invalid={!!fieldState.error}
            validation-message={fieldState.error?.message}
          >
            <SafCheckbox value="tech">Technology</SafCheckbox>
            <SafCheckbox value="design">Design</SafCheckbox>
            <SafCheckbox value="business">Business</SafCheckbox>
            <SafCheckbox value="science">Science</SafCheckbox>
          </SafCheckboxGroup>
        )}
      />
    </form>
  );
};
```

## Notes

- Groups related checkboxes with shared validation and labeling
- Supports both horizontal and vertical orientations
- Provides comprehensive accessibility features
- Integrates seamlessly with form validation libraries
- Handles complex selection rules and conditional logic
- Maintains proper semantic structure for screen readers
