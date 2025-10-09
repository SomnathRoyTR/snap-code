# SafDisclosure

## Overview

SafDisclosure is an interactive component that allows users to show and hide content sections. It provides accessible expand/collapse functionality with customizable triggers, smooth animations, and support for nested disclosures, making it ideal for FAQs, detailed information panels, and progressive disclosure patterns.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Controls disclosure expanded state |
| `defaultExpanded` | `boolean` | `false` | Initial expanded state (uncontrolled) |
| `trigger` | `string \| ReactElement` | - | Trigger content (button text or custom element) |
| `triggerProps` | `object` | `{}` | Additional props for trigger button |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting trigger button |
| `variant` | `'default' \| 'bordered' \| 'filled' \| 'ghost'` | `'default'` | Visual style variant |
| `icon` | `string \| ReactElement \| boolean` | `true` | Expand/collapse icon or custom icon |
| `iconPosition` | `'start' \| 'end'` | `'end'` | Position of expand/collapse icon |
| `animationDuration` | `number` | `200` | Animation duration in milliseconds |
| `disabled` | `boolean` | `false` | Disables interaction |
| `level` | `number` | `1` | Semantic heading level for trigger |
| `className` | `string` | - | Additional CSS classes |
| `triggerClassName` | `string` | - | Additional CSS classes for trigger |
| `contentClassName` | `string` | - | Additional CSS classes for content |
| `children` | `ReactNode` | - | Disclosure content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onExpandedChange` | `(expanded: boolean) => void` | Fired when expanded state changes |
| `onExpand` | `() => void` | Fired when disclosure expands |
| `onCollapse` | `() => void` | Fired when disclosure collapses |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Controls disclosure expanded state |
| `trigger` | `string` | - | Trigger button text |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant affecting trigger button |
| `variant` | `'default' \| 'bordered' \| 'filled' \| 'ghost'` | `'default'` | Visual style variant |
| `icon` | `string \| boolean` | `true` | Expand/collapse icon name or false to hide |
| `iconPosition` | `'start' \| 'end'` | `'end'` | Position of expand/collapse icon |
| `animationDuration` | `number` | `200` | Animation duration in milliseconds |
| `disabled` | `boolean` | `false` | Disables interaction |
| `level` | `number` | `1` | Semantic heading level for trigger |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `expandedChange` | `EventEmitter<boolean>` | Fired when expanded state changes |
| `expand` | `EventEmitter<void>` | Fired when disclosure expands |
| `collapse` | `EventEmitter<void>` | Fired when disclosure collapses |

## Usage Examples

### Basic Disclosure

```typescript
// React
<SafDisclosure trigger="Show Details">
  <p>This is additional content that can be shown or hidden.</p>
  <p>It supports multiple paragraphs and rich content.</p>
</SafDisclosure>

<SafDisclosure trigger="Advanced Settings" defaultExpanded>
  <div>
    <SafFormField label="API Endpoint">
      <SafTextField placeholder="Enter API endpoint" />
    </SafFormField>
    <SafFormField label="Timeout (seconds)">
      <SafNumberField placeholder="30" />
    </SafFormField>
  </div>
</SafDisclosure>
```

```html
<!-- Angular -->
<saf-disclosure trigger="Show Details">
  <p>This is additional content that can be shown or hidden.</p>
  <p>It supports multiple paragraphs and rich content.</p>
</saf-disclosure>

<saf-disclosure trigger="Advanced Settings" [expanded]="true">
  <div>
    <saf-form-field label="API Endpoint">
      <saf-text-field placeholder="Enter API endpoint"></saf-text-field>
    </saf-form-field>
    <saf-form-field label="Timeout (seconds)">
      <saf-number-field placeholder="30"></saf-number-field>
    </saf-form-field>
  </div>
</saf-disclosure>
```

### Controlled Disclosure

```typescript
// React
const [isExpanded, setIsExpanded] = useState(false);

<SafDisclosure 
  trigger="System Information" 
  expanded={isExpanded}
  onExpandedChange={setIsExpanded}
  onExpand={() => logEvent('system_info_expanded')}
>
  <div>
    <p>Version: 2.1.0</p>
    <p>Build: 2024.09.26.1</p>
    <p>Environment: Production</p>
  </div>
</SafDisclosure>

<SafButton 
  variant="text" 
  onClick={() => setIsExpanded(!isExpanded)}
>
  {isExpanded ? 'Hide' : 'Show'} System Info
</SafButton>
```

```html
<!-- Angular -->
<saf-disclosure 
  trigger="System Information" 
  [expanded]="isExpanded"
  (expandedChange)="setIsExpanded($event)"
  (expand)="logEvent('system_info_expanded')"
>
  <div>
    <p>Version: 2.1.0</p>
    <p>Build: 2024.09.26.1</p>
    <p>Environment: Production</p>
  </div>
</saf-disclosure>

<saf-button 
  variant="text" 
  (click)="setIsExpanded(!isExpanded)"
>
  {{isExpanded ? 'Hide' : 'Show'}} System Info
</saf-button>
```

### Size Variants

```typescript
// React
<SafDisclosure trigger="Small Disclosure" size="small">
  <p>Content with small trigger button.</p>
</SafDisclosure>

<SafDisclosure trigger="Medium Disclosure" size="medium">
  <p>Content with medium trigger button.</p>
</SafDisclosure>

<SafDisclosure trigger="Large Disclosure" size="large">
  <p>Content with large trigger button.</p>
</SafDisclosure>
```

```html
<!-- Angular -->
<saf-disclosure trigger="Small Disclosure" size="small">
  <p>Content with small trigger button.</p>
</saf-disclosure>

<saf-disclosure trigger="Medium Disclosure" size="medium">
  <p>Content with medium trigger button.</p>
</saf-disclosure>

<saf-disclosure trigger="Large Disclosure" size="large">
  <p>Content with large trigger button.</p>
</saf-disclosure>
```

### Visual Variants

```typescript
// React
<SafDisclosure trigger="Default Style" variant="default">
  <p>Default appearance with minimal styling.</p>
</SafDisclosure>

<SafDisclosure trigger="Bordered Style" variant="bordered">
  <p>Bordered appearance with visible boundaries.</p>
</SafDisclosure>

<SafDisclosure trigger="Filled Style" variant="filled">
  <p>Filled appearance with background color.</p>
</SafDisclosure>

<SafDisclosure trigger="Ghost Style" variant="ghost">
  <p>Minimal appearance with subtle styling.</p>
</SafDisclosure>
```

```html
<!-- Angular -->
<saf-disclosure trigger="Default Style" variant="default">
  <p>Default appearance with minimal styling.</p>
</saf-disclosure>

<saf-disclosure trigger="Bordered Style" variant="bordered">
  <p>Bordered appearance with visible boundaries.</p>
</saf-disclosure>

<saf-disclosure trigger="Filled Style" variant="filled">
  <p>Filled appearance with background color.</p>
</saf-disclosure>

<saf-disclosure trigger="Ghost Style" variant="ghost">
  <p>Minimal appearance with subtle styling.</p>
</saf-disclosure>
```

### Icon Customization

```typescript
// React
<SafDisclosure 
  trigger="Custom Icon" 
  icon="info"
  iconPosition="start"
>
  <p>Disclosure with custom icon at start position.</p>
</SafDisclosure>

<SafDisclosure 
  trigger="No Icon" 
  icon={false}
>
  <p>Disclosure without expand/collapse icon.</p>
</SafDisclosure>

<SafDisclosure 
  trigger="Custom React Icon" 
  icon={<SafIcon name="settings" />}
>
  <p>Disclosure with custom React element icon.</p>
</SafDisclosure>
```

```html
<!-- Angular -->
<saf-disclosure 
  trigger="Custom Icon" 
  icon="info"
  iconPosition="start"
>
  <p>Disclosure with custom icon at start position.</p>
</saf-disclosure>

<saf-disclosure 
  trigger="No Icon" 
  [icon]="false"
>
  <p>Disclosure without expand/collapse icon.</p>
</saf-disclosure>
```

### Custom Trigger

```typescript
// React
<SafDisclosure 
  trigger={
    <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
      <SafAvatar name="John Doe" size="small" />
      <span>View Profile Details</span>
    </div>
  }
>
  <div>
    <SafDescriptionList>
      <SafDescriptionTerm>Email</SafDescriptionTerm>
      <SafDescriptionDetails>john.doe@example.com</SafDescriptionDetails>
      <SafDescriptionTerm>Department</SafDescriptionTerm>
      <SafDescriptionDetails>Engineering</SafDescriptionDetails>
      <SafDescriptionTerm>Role</SafDescriptionTerm>
      <SafDescriptionDetails>Senior Developer</SafDescriptionDetails>
    </SafDescriptionList>
  </div>
</SafDisclosure>
```

### FAQ Section

```typescript
// React
const FAQSection = ({ faqs }) => (
  <div className="faq-section">
    <h2>Frequently Asked Questions</h2>
    {faqs.map((faq, index) => (
      <SafDisclosure 
        key={faq.id} 
        trigger={faq.question}
        variant="bordered"
        level={3}
      >
        <div dangerouslySetInnerHTML={{ __html: faq.answer }} />
      </SafDisclosure>
    ))}
  </div>
);

// Usage
const faqs = [
  {
    id: 1,
    question: "How do I reset my password?",
    answer: "<p>You can reset your password by clicking the 'Forgot Password' link on the login page.</p>"
  },
  {
    id: 2,
    question: "What payment methods do you accept?",
    answer: "<p>We accept all major credit cards, PayPal, and bank transfers.</p>"
  }
];
```

### Nested Disclosures

```typescript
// React
<SafDisclosure trigger="Account Settings" variant="filled">
  <div>
    <SafDisclosure trigger="Profile Information" size="small">
      <div>
        <SafFormField label="Display Name">
          <SafTextField placeholder="Enter display name" />
        </SafFormField>
        <SafFormField label="Bio">
          <SafTextArea placeholder="Tell us about yourself" />
        </SafFormField>
      </div>
    </SafDisclosure>
    
    <SafDisclosure trigger="Privacy Settings" size="small">
      <div>
        <SafCheckbox label="Make profile public" />
        <SafCheckbox label="Allow search engines to index" />
        <SafCheckbox label="Show activity status" />
      </div>
    </SafDisclosure>
    
    <SafDisclosure trigger="Notification Preferences" size="small">
      <div>
        <SafRadioGroup label="Email frequency">
          <SafRadio value="daily">Daily digest</SafRadio>
          <SafRadio value="weekly">Weekly summary</SafRadio>
          <SafRadio value="never">Never</SafRadio>
        </SafRadioGroup>
      </div>
    </SafDisclosure>
  </div>
</SafDisclosure>
```

### Data Table Row Details

```typescript
// React
const DataTableWithDetails = ({ data }) => (
  <SafTable>
    <SafTableHead>
      <SafTableRow>
        <SafTableHeaderCell>Name</SafTableHeaderCell>
        <SafTableHeaderCell>Status</SafTableHeaderCell>
        <SafTableHeaderCell>Actions</SafTableHeaderCell>
      </SafTableRow>
    </SafTableHead>
    <SafTableBody>
      {data.map(item => (
        <React.Fragment key={item.id}>
          <SafTableRow>
            <SafTableCell>{item.name}</SafTableCell>
            <SafTableCell>
              <SafStatus variant={item.status}>{item.statusText}</SafStatus>
            </SafTableCell>
            <SafTableCell>
              <SafDisclosure 
                trigger="Details" 
                size="small" 
                variant="ghost"
              >
                <div style={{ padding: '16px' }}>
                  <SafDescriptionList size="small">
                    <SafDescriptionTerm>Created</SafDescriptionTerm>
                    <SafDescriptionDetails>{item.createdDate}</SafDescriptionDetails>
                    <SafDescriptionTerm>Last Modified</SafDescriptionTerm>
                    <SafDescriptionDetails>{item.modifiedDate}</SafDescriptionDetails>
                    <SafDescriptionTerm>Description</SafDescriptionTerm>
                    <SafDescriptionDetails>{item.description}</SafDescriptionDetails>
                  </SafDescriptionList>
                </div>
              </SafDisclosure>
            </SafTableCell>
          </SafTableRow>
        </React.Fragment>
      ))}
    </SafTableBody>
  </SafTable>
);
```

### Form Sections

```typescript
// React
const MultiSectionForm = () => (
  <form>
    <SafDisclosure trigger="Personal Information" defaultExpanded variant="bordered">
      <div>
        <SafFormField label="First Name" required>
          <SafTextField placeholder="Enter first name" />
        </SafFormField>
        <SafFormField label="Last Name" required>
          <SafTextField placeholder="Enter last name" />
        </SafFormField>
        <SafFormField label="Email" required>
          <SafTextField type="email" placeholder="Enter email" />
        </SafFormField>
      </div>
    </SafDisclosure>

    <SafDisclosure trigger="Address Information" variant="bordered">
      <div>
        <SafFormField label="Street Address">
          <SafTextField placeholder="Enter street address" />
        </SafFormField>
        <SafFormField label="City">
          <SafTextField placeholder="Enter city" />
        </SafFormField>
        <SafFormField label="State">
          <SafSelect placeholder="Select state">
            <SafOption value="ny">New York</SafOption>
            <SafOption value="ca">California</SafOption>
          </SafSelect>
        </SafFormField>
      </div>
    </SafDisclosure>

    <SafDisclosure trigger="Additional Options" variant="bordered">
      <div>
        <SafCheckbox label="Subscribe to newsletter" />
        <SafCheckbox label="Enable notifications" />
        <SafFormField label="Comments">
          <SafTextArea placeholder="Additional comments" />
        </SafFormField>
      </div>
    </SafDisclosure>
  </form>
);
```

### Card Content Disclosure

```typescript
// React
<SafCard>
  <SafCardHeader>
    <SafCardTitle>Project Alpha</SafCardTitle>
    <SafStatus variant="success">Active</SafStatus>
  </SafCardHeader>
  <SafCardContent>
    <p>A comprehensive project management solution.</p>
    
    <SafDisclosure trigger="View Technical Details" variant="ghost">
      <div>
        <SafDescriptionList size="small">
          <SafDescriptionTerm>Technology Stack</SafDescriptionTerm>
          <SafDescriptionDetails>React, Node.js, PostgreSQL</SafDescriptionDetails>
          <SafDescriptionTerm>Repository</SafDescriptionTerm>
          <SafDescriptionDetails>
            <SafLink href="https://github.com/company/project-alpha">
              github.com/company/project-alpha
            </SafLink>
          </SafDescriptionDetails>
          <SafDescriptionTerm>Deployment</SafDescriptionTerm>
          <SafDescriptionDetails>AWS ECS with auto-scaling</SafDescriptionDetails>
        </SafDescriptionList>
        
        <div style={{ marginTop: '16px' }}>
          <SafButton variant="outline" size="small">
            View Repository
          </SafButton>
          <SafButton variant="text" size="small">
            View Deployment
          </SafButton>
        </div>
      </div>
    </SafDisclosure>
  </SafCardContent>
</SafCard>
```

### Animation Customization

```typescript
// React
<SafDisclosure 
  trigger="Fast Animation" 
  animationDuration={100}
>
  <p>This disclosure opens and closes quickly.</p>
</SafDisclosure>

<SafDisclosure 
  trigger="Slow Animation" 
  animationDuration={500}
>
  <p>This disclosure has a slower, more deliberate animation.</p>
</SafDisclosure>
```

```html
<!-- Angular -->
<saf-disclosure 
  trigger="Fast Animation" 
  [animationDuration]="100"
>
  <p>This disclosure opens and closes quickly.</p>
</saf-disclosure>

<saf-disclosure 
  trigger="Slow Animation" 
  [animationDuration]="500"
>
  <p>This disclosure has a slower, more deliberate animation.</p>
</saf-disclosure>
```

## Best Practices

### Content Organization
- **Logical Grouping**: Group related information that users might want to explore
- **Progressive Disclosure**: Use for secondary or detailed information
- **Clear Triggers**: Make trigger text descriptive and action-oriented
- **Appropriate Nesting**: Limit nesting depth to maintain clarity

### User Experience
- **Default States**: Set appropriate default expanded states based on content importance
- **Animation Timing**: Use moderate animation speeds for smooth transitions
- **Visual Hierarchy**: Use variants and sizes to establish content hierarchy
- **Keyboard Support**: Ensure full keyboard accessibility

### Performance
- **Content Loading**: Consider lazy loading for heavy content within disclosures
- **Animation Performance**: Use CSS transforms for smooth animations
- **State Management**: Manage expanded states efficiently in lists
- **Memory Usage**: Clean up event listeners and animations properly

### Accessibility
- **Semantic Structure**: Use appropriate heading levels for content hierarchy
- **Screen Readers**: Ensure expanded/collapsed states are announced
- **Keyboard Navigation**: Support Enter and Space key activation
- **Focus Management**: Maintain logical focus flow

## Accessibility Considerations

- Uses semantic button element for trigger with proper ARIA attributes
- Provides `aria-expanded` state for screen readers
- Supports keyboard navigation (Enter and Space keys)
- Maintains logical heading hierarchy with configurable levels
- Ensures content is properly associated with trigger
- Respects user preferences for reduced motion

## Related Components

- **SafAccordion**: Multi-item disclosure component
- **SafAccordionItem**: Individual accordion sections
- **SafCard**: Container component that may include disclosures
- **SafCollapse**: Low-level collapse animation component
- **SafButton**: Trigger button styling reference
- **SafDetails**: HTML details-based alternative

## Notes

- SafDisclosure automatically manages ARIA attributes for accessibility
- Animation duration can be customized but should remain reasonable for UX
- Custom triggers receive proper event handlers and accessibility attributes
- The component supports both controlled and uncontrolled usage patterns
- Nested disclosures automatically inherit appropriate styling context
- Icon rotation is handled automatically for expand/collapse states
- Content area receives proper semantic markup for screen readers
