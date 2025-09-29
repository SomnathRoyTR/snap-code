# SafFlipper

## Overview

SafFlipper is a simple two-state toggle component that allows users to flip between two pieces of content or views. It provides smooth transitions, customizable triggers, and support for both automatic and manual flipping, making it ideal for before/after comparisons, card flips, and simple content switching.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `flipped` | `boolean` | `false` | Controls the flipped state (controlled) |
| `defaultFlipped` | `boolean` | `false` | Initial flipped state (uncontrolled) |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | Flip animation direction |
| `trigger` | `'click' \| 'hover' \| 'manual'` | `'click'` | How to trigger the flip |
| `frontContent` | `ReactNode` | - | Content for the front side |
| `backContent` | `ReactNode` | - | Content for the back side |
| `duration` | `number` | `300` | Animation duration in milliseconds |
| `easing` | `string` | `'ease'` | CSS easing function |
| `disabled` | `boolean` | `false` | Disables interaction |
| `perspective` | `number` | `1000` | CSS perspective for 3D effect |
| `showTrigger` | `boolean` | `true` | Shows flip trigger button |
| `triggerPosition` | `'top-right' \| 'top-left' \| 'bottom-right' \| 'bottom-left' \| 'center'` | `'top-right'` | Position of trigger button |
| `triggerIcon` | `string \| ReactElement` | `'flip'` | Icon for trigger button |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onFlip` | `(flipped: boolean) => void` | Fired when flip state changes |
| `onFlipStart` | `() => void` | Fired when flip animation starts |
| `onFlipEnd` | `() => void` | Fired when flip animation completes |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `flipped` | `boolean` | `false` | Controls the flipped state |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | Flip animation direction |
| `trigger` | `'click' \| 'hover' \| 'manual'` | `'click'` | How to trigger the flip |
| `duration` | `number` | `300` | Animation duration in milliseconds |
| `easing` | `string` | `'ease'` | CSS easing function |
| `disabled` | `boolean` | `false` | Disables interaction |
| `perspective` | `number` | `1000` | CSS perspective for 3D effect |
| `showTrigger` | `boolean` | `true` | Shows flip trigger button |
| `triggerPosition` | `'top-right' \| 'top-left' \| 'bottom-right' \| 'bottom-left' \| 'center'` | `'top-right'` | Position of trigger button |
| `triggerIcon` | `string` | `'flip'` | Icon name for trigger button |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `flip` | `EventEmitter<boolean>` | Fired when flip state changes |
| `flipStart` | `EventEmitter<void>` | Fired when flip animation starts |
| `flipEnd` | `EventEmitter<void>` | Fired when flip animation completes |

## Usage Examples

### Basic Card Flip

```typescript
// React
<SafFlipper 
  frontContent={
    <SafCard>
      <SafCardContent>
        <h3>Front Side</h3>
        <p>This is the front content of the card.</p>
      </SafCardContent>
    </SafCard>
  }
  backContent={
    <SafCard>
      <SafCardContent>
        <h3>Back Side</h3>
        <p>This is the back content with additional details.</p>
      </SafCardContent>
    </SafCard>
  }
/>
```

```html
<!-- Angular -->
<saf-flipper>
  <div slot="front">
    <saf-card>
      <saf-card-content>
        <h3>Front Side</h3>
        <p>This is the front content of the card.</p>
      </saf-card-content>
    </saf-card>
  </div>
  <div slot="back">
    <saf-card>
      <saf-card-content>
        <h3>Back Side</h3>
        <p>This is the back content with additional details.</p>
      </saf-card-content>
    </saf-card>
  </div>
</saf-flipper>
```

### Team Member Card

```typescript
// React
const TeamMemberCard = ({ member }) => (
  <SafFlipper 
    trigger="hover"
    frontContent={
      <SafCard className="team-card">
        <SafCardContent style={{ textAlign: 'center' }}>
          <SafAvatar 
            name={member.name} 
            src={member.photo} 
            size="large" 
          />
          <h3>{member.name}</h3>
          <p>{member.position}</p>
        </SafCardContent>
      </SafCard>
    }
    backContent={
      <SafCard className="team-card">
        <SafCardContent>
          <h3>Contact Info</h3>
          <SafDescriptionList size="small">
            <SafDescriptionTerm>Email</SafDescriptionTerm>
            <SafDescriptionDetails>{member.email}</SafDescriptionDetails>
            <SafDescriptionTerm>Phone</SafDescriptionTerm>
            <SafDescriptionDetails>{member.phone}</SafDescriptionDetails>
            <SafDescriptionTerm>Department</SafDescriptionTerm>
            <SafDescriptionDetails>{member.department}</SafDescriptionDetails>
          </SafDescriptionList>
        </SafCardContent>
      </SafCard>
    }
    showTrigger={false}
  />
);
```

### Product Comparison

```typescript
// React
const ProductComparison = ({ product }) => (
  <SafFlipper 
    direction="vertical"
    frontContent={
      <div className="product-front">
        <img src={product.image} alt={product.name} />
        <h3>{product.name}</h3>
        <SafStatus variant="success">${product.price}</SafStatus>
      </div>
    }
    backContent={
      <div className="product-back">
        <h3>Specifications</h3>
        <ul>
          {product.specs.map(spec => (
            <li key={spec.name}>
              <strong>{spec.name}:</strong> {spec.value}
            </li>
          ))}
        </ul>
        <div style={{ marginTop: '16px' }}>
          <SafButton onClick={() => addToCart(product.id)}>
            Add to Cart
          </SafButton>
        </div>
      </div>
    }
    triggerPosition="bottom-right"
  />
);
```

### Image Before/After

```typescript
// React
<SafFlipper 
  frontContent={
    <div className="image-container">
      <img src="/images/before.jpg" alt="Before renovation" />
      <div className="image-label">Before</div>
    </div>
  }
  backContent={
    <div className="image-container">
      <img src="/images/after.jpg" alt="After renovation" />
      <div className="image-label">After</div>
    </div>
  }
  triggerPosition="center"
  triggerIcon="swap"
/>
```

### Controlled Flipper

```typescript
// React
const [isFlipped, setIsFlipped] = useState(false);

<div>
  <SafFlipper 
    flipped={isFlipped}
    onFlip={setIsFlipped}
    trigger="manual"
    frontContent={
      <SafCard>
        <SafCardContent>
          <SafIcon name="question" size="large" />
          <h3>Question</h3>
          <p>What is the capital of France?</p>
        </SafCardContent>
      </SafCard>
    }
    backContent={
      <SafCard>
        <SafCardContent>
          <SafIcon name="lightbulb" size="large" />
          <h3>Answer</h3>
          <p>Paris is the capital of France.</p>
        </SafCardContent>
      </SafCard>
    }
    showTrigger={false}
  />
  
  <div style={{ marginTop: '16px', textAlign: 'center' }}>
    <SafButton onClick={() => setIsFlipped(!isFlipped)}>
      {isFlipped ? 'Show Question' : 'Show Answer'}
    </SafButton>
  </div>
</div>
```

### Quiz Card

```typescript
// React
const QuizCard = ({ question, answer, onAnswer }) => {
  const [revealed, setRevealed] = useState(false);
  
  return (
    <SafFlipper 
      flipped={revealed}
      onFlip={setRevealed}
      duration={400}
      frontContent={
        <SafCard className="quiz-card">
          <SafCardHeader>
            <SafBadge variant="primary">Question</SafBadge>
          </SafCardHeader>
          <SafCardContent>
            <p>{question.text}</p>
            {question.options && (
              <div className="quiz-options">
                {question.options.map(option => (
                  <SafButton 
                    key={option.id}
                    variant="outline"
                    onClick={() => {
                      onAnswer(option.id);
                      setRevealed(true);
                    }}
                  >
                    {option.text}
                  </SafButton>
                ))}
              </div>
            )}
          </SafCardContent>
        </SafCard>
      }
      backContent={
        <SafCard className="quiz-card">
          <SafCardHeader>
            <SafBadge variant="success">Answer</SafBadge>
          </SafCardHeader>
          <SafCardContent>
            <p>{answer.explanation}</p>
            <div style={{ marginTop: '16px' }}>
              <SafButton 
                onClick={() => setRevealed(false)}
                variant="outline"
              >
                Back to Question
              </SafButton>
            </div>
          </SafCardContent>
        </SafCard>
      }
      trigger="manual"
      showTrigger={false}
    />
  );
};
```

### Settings Toggle

```typescript
// React
const SettingsToggle = ({ settings, onUpdateSettings }) => (
  <SafFlipper 
    trigger="click"
    frontContent={
      <SafCard>
        <SafCardHeader>
          <SafCardTitle>Current Settings</SafCardTitle>
        </SafCardHeader>
        <SafCardContent>
          <SafDescriptionList>
            <SafDescriptionTerm>Theme</SafDescriptionTerm>
            <SafDescriptionDetails>{settings.theme}</SafDescriptionDetails>
            <SafDescriptionTerm>Language</SafDescriptionTerm>
            <SafDescriptionDetails>{settings.language}</SafDescriptionDetails>
            <SafDescriptionTerm>Notifications</SafDescriptionTerm>
            <SafDescriptionDetails>
              {settings.notifications ? 'Enabled' : 'Disabled'}
            </SafDescriptionDetails>
          </SafDescriptionList>
        </SafCardContent>
      </SafCard>
    }
    backContent={
      <SafCard>
        <SafCardHeader>
          <SafCardTitle>Edit Settings</SafCardTitle>
        </SafCardHeader>
        <SafCardContent>
          <SafFormField label="Theme">
            <SafSelect 
              value={settings.theme}
              onChange={(theme) => onUpdateSettings({...settings, theme})}
            >
              <SafOption value="light">Light</SafOption>
              <SafOption value="dark">Dark</SafOption>
            </SafSelect>
          </SafFormField>
          
          <SafFormField label="Language">
            <SafSelect 
              value={settings.language}
              onChange={(language) => onUpdateSettings({...settings, language})}
            >
              <SafOption value="en">English</SafOption>
              <SafOption value="es">Spanish</SafOption>
            </SafSelect>
          </SafFormField>
          
          <SafCheckbox 
            checked={settings.notifications}
            onChange={(notifications) => onUpdateSettings({...settings, notifications})}
            label="Enable notifications"
          />
        </SafCardContent>
      </SafCard>
    }
    triggerIcon="settings"
  />
);
```

### Dashboard Widget

```typescript
// React
const DashboardWidget = ({ data }) => (
  <SafFlipper 
    trigger="hover"
    duration={250}
    frontContent={
      <SafCard className="dashboard-widget">
        <SafCardContent>
          <div className="widget-header">
            <h3>Sales</h3>
            <SafProgressRing value={data.progress} size="small" />
          </div>
          <div className="widget-value">
            ${data.value.toLocaleString()}
          </div>
          <SafStatus variant={data.trend > 0 ? 'success' : 'error'}>
            {data.trend > 0 ? '+' : ''}{data.trend}%
          </SafStatus>
        </SafCardContent>
      </SafCard>
    }
    backContent={
      <SafCard className="dashboard-widget">
        <SafCardContent>
          <h3>Details</h3>
          <SafDescriptionList size="small">
            <SafDescriptionTerm>This Month</SafDescriptionTerm>
            <SafDescriptionDetails>${data.thisMonth}</SafDescriptionDetails>
            <SafDescriptionTerm>Last Month</SafDescriptionTerm>
            <SafDescriptionDetails>${data.lastMonth}</SafDescriptionDetails>
            <SafDescriptionTerm>Target</SafDescriptionTerm>
            <SafDescriptionDetails>${data.target}</SafDescriptionDetails>
          </SafDescriptionList>
          <SafButton variant="text" size="small">
            View Report
          </SafButton>
        </SafCardContent>
      </SafCard>
    }
    showTrigger={false}
  />
);
```

### Feature Showcase

```typescript
// React
const FeatureShowcase = ({ features }) => (
  <div className="feature-grid">
    {features.map(feature => (
      <SafFlipper 
        key={feature.id}
        trigger="click"
        direction="vertical"
        frontContent={
          <div className="feature-front">
            <SafIcon name={feature.icon} size="large" />
            <h3>{feature.title}</h3>
            <p>{feature.summary}</p>
          </div>
        }
        backContent={
          <div className="feature-back">
            <h3>How it works</h3>
            <ol>
              {feature.steps.map(step => (
                <li key={step.id}>{step.description}</li>
              ))}
            </ol>
            <SafButton 
              variant="primary" 
              onClick={() => tryFeature(feature.id)}
            >
              Try it now
            </SafButton>
          </div>
        }
        triggerPosition="bottom-left"
        triggerIcon="info"
      />
    ))}
  </div>
);
```

### Custom Animation

```typescript
// React
<SafFlipper 
  frontContent={<div className="custom-front">Front</div>}
  backContent={<div className="custom-back">Back</div>}
  duration={500}
  easing="cubic-bezier(0.68, -0.55, 0.265, 1.55)"
  perspective={1200}
  onFlipStart={() => console.log('Flip animation started')}
  onFlipEnd={() => console.log('Flip animation completed')}
/>
```

### Data Visualization Toggle

```typescript
// React
const DataVisualization = ({ data }) => (
  <SafFlipper 
    frontContent={
      <div className="chart-container">
        <h3>Chart View</h3>
        <SafChart data={data} type="bar" />
      </div>
    }
    backContent={
      <div className="table-container">
        <h3>Table View</h3>
        <SafTable>
          <SafTableHead>
            <SafTableRow>
              <SafTableHeaderCell>Category</SafTableHeaderCell>
              <SafTableHeaderCell>Value</SafTableHeaderCell>
            </SafTableRow>
          </SafTableHead>
          <SafTableBody>
            {data.map(item => (
              <SafTableRow key={item.category}>
                <SafTableCell>{item.category}</SafTableCell>
                <SafTableCell>{item.value}</SafTableCell>
              </SafTableRow>
            ))}
          </SafTableBody>
        </SafTable>
      </div>
    }
    triggerIcon="swap-horizontal"
    triggerPosition="top-left"
  />
);
```

## Best Practices

### Content Design
- **Balanced Content**: Ensure both sides have appropriate content density
- **Consistent Dimensions**: Maintain consistent sizing between front and back
- **Clear Purpose**: Make it obvious why users would want to flip
- **Visual Hierarchy**: Use consistent typography and spacing

### Animation
- **Appropriate Duration**: Use reasonable animation speeds (200-400ms)
- **Smooth Easing**: Choose easing functions that feel natural
- **Performance**: Optimize for smooth animations on all devices
- **Reduced Motion**: Respect user preferences for reduced motion

### Interaction
- **Clear Triggers**: Make it obvious how to activate the flip
- **Trigger Positioning**: Place triggers where users expect to find them
- **Hover Behavior**: Use hover triggers sparingly and appropriately
- **Feedback**: Provide clear visual feedback during interactions

### Accessibility
- **Keyboard Support**: Ensure keyboard users can trigger flips
- **Screen Readers**: Provide appropriate announcements for state changes
- **Focus Management**: Handle focus appropriately during flips
- **Content Discovery**: Make it clear that additional content exists

## Accessibility Considerations

- Uses appropriate ARIA attributes to announce state changes
- Supports keyboard navigation (Enter and Space keys)
- Provides screen reader announcements when content flips
- Maintains focus management during flip animations
- Respects user preferences for reduced motion
- Ensures both sides of content are accessible to screen readers

## Related Components

- **SafCarousel**: Multi-item navigation component
- **SafDisclosure**: Expandable content component  
- **SafTabs**: Multi-panel content switching
- **SafAccordion**: Vertical expandable sections
- **SafModal**: Overlay content display
- **SafCard**: Content container component

## Notes

- SafFlipper uses CSS 3D transforms for smooth flip animations
- The component automatically handles perspective and backface visibility
- Trigger buttons are positioned absolutely and can be customized
- Animation performance is optimized using hardware acceleration
- Both controlled and uncontrolled usage patterns are supported
- Content on both sides maintains equal dimensions automatically
- The component handles touch events for mobile interaction
- Custom easing functions can be used for unique animation effects
