# SafStepperLabelIndicator

## Overview

SafStepperLabelIndicator is a navigation component that represents an individual step status indicator within multi-step processes. It provides visual feedback for step states including pending, current, completed, error, and optional states with customizable icons, numbers, and interactive behavior.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `stepIndex` | `number` | - | Zero-based index of the step |
| `stepNumber` | `number` | - | One-based display number for the step |
| `status` | `'pending' \| 'current' \| 'completed' \| 'error' \| 'skipped'` | `'pending'` | Current status of the step |
| `label` | `string` | - | Step label text |
| `description` | `string` | - | Optional step description |
| `icon` | `ReactElement` | - | Custom icon for the step |
| `showNumber` | `boolean` | `true` | Show step number in indicator |
| `clickable` | `boolean` | `true` | Allow clicking on the indicator |
| `disabled` | `boolean` | `false` | Disable the indicator |
| `optional` | `boolean` | `false` | Mark step as optional |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Indicator size |
| `variant` | `'default' \| 'compact' \| 'minimal'` | `'default'` | Visual style variant |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `showConnector` | `boolean` | `true` | Show connecting line to next step |
| `connectorPosition` | `'before' \| 'after' \| 'both'` | `'after'` | Position of connector line |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(stepIndex: number, event: MouseEvent) => void` | Fired when indicator is clicked |
| `onKeyDown` | `(stepIndex: number, event: KeyboardEvent) => void` | Fired when key is pressed |
| `onFocus` | `(stepIndex: number, event: FocusEvent) => void` | Fired when indicator receives focus |
| `onBlur` | `(stepIndex: number, event: FocusEvent) => void` | Fired when indicator loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `stepIndex` | `number` | - | Zero-based index of the step |
| `stepNumber` | `number` | - | One-based display number for the step |
| `status` | `'pending' \| 'current' \| 'completed' \| 'error' \| 'skipped'` | `'pending'` | Current status of the step |
| `label` | `string` | - | Step label text |
| `description` | `string` | - | Optional step description |
| `showNumber` | `boolean` | `true` | Show step number in indicator |
| `clickable` | `boolean` | `true` | Allow clicking on the indicator |
| `disabled` | `boolean` | `false` | Disable the indicator |
| `optional` | `boolean` | `false` | Mark step as optional |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Indicator size |
| `variant` | `'default' \| 'compact' \| 'minimal'` | `'default'` | Visual style variant |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `showConnector` | `boolean` | `true` | Show connecting line to next step |
| `connectorPosition` | `'before' \| 'after' \| 'both'` | `'after'` | Position of connector line |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `indicatorClick` | `EventEmitter<{stepIndex: number, event: MouseEvent}>` | Fired when indicator is clicked |
| `indicatorKeyDown` | `EventEmitter<{stepIndex: number, event: KeyboardEvent}>` | Fired when key is pressed |
| `indicatorFocus` | `EventEmitter<{stepIndex: number, event: FocusEvent}>` | Fired when indicator receives focus |
| `indicatorBlur` | `EventEmitter<{stepIndex: number, event: FocusEvent}>` | Fired when indicator loses focus |

## Usage Examples

### Basic Step Indicator

```typescript
// React
const BasicStepIndicator = ({ step, index, currentStep, onStepClick }) => {
  const getStatus = () => {
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  return (
    <SafStepperLabelIndicator 
      stepIndex={index}
      stepNumber={index + 1}
      status={getStatus()}
      label={step.label}
      description={step.description}
      onClick={(stepIndex) => onStepClick(stepIndex)}
      clickable={index <= currentStep}
    />
  );
};
```

```html
<!-- Angular -->
<saf-stepper-label-indicator 
  [stepIndex]="index"
  [stepNumber]="index + 1"
  [status]="getStatus()"
  [label]="step.label"
  [description]="step.description"
  [clickable]="index <= currentStep"
  (indicatorClick)="onStepClick($event.stepIndex)">
</saf-stepper-label-indicator>
```

### Icon-Based Indicators

```typescript
// React
const IconBasedIndicators = ({ steps, currentStep, onStepClick }) => {
  const getStepIcon = (step, status) => {
    if (status === 'completed') {
      return <SafIcon name="check" />;
    }
    if (status === 'error') {
      return <SafIcon name="alert-circle" />;
    }
    if (step.icon) {
      return step.icon;
    }
    return null;
  };

  const getStatus = (index) => {
    if (steps[index].error) return 'error';
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  return (
    <div className="icon-stepper">
      {steps.map((step, index) => (
        <SafStepperLabelIndicator 
          key={step.id}
          stepIndex={index}
          stepNumber={index + 1}
          status={getStatus(index)}
          label={step.label}
          description={step.description}
          icon={getStepIcon(step, getStatus(index))}
          showNumber={getStatus(index) === 'pending'}
          onClick={onStepClick}
          showConnector={index < steps.length - 1}
        />
      ))}
    </div>
  );
};
```

### Compact Indicators

```typescript
// React
const CompactIndicators = ({ totalSteps, currentStep, onStepClick }) => {
  return (
    <div className="compact-stepper">
      {Array.from({ length: totalSteps }, (_, index) => (
        <SafStepperLabelIndicator 
          key={index}
          stepIndex={index}
          stepNumber={index + 1}
          status={index < currentStep ? 'completed' : 
                  index === currentStep ? 'current' : 'pending'}
          label={`Step ${index + 1}`}
          variant="compact"
          size="small"
          onClick={onStepClick}
          showConnector={index < totalSteps - 1}
        />
      ))}
    </div>
  );
};
```

### Vertical Step Indicators

```typescript
// React
const VerticalStepIndicators = ({ steps, currentStep, completedSteps, onStepClick }) => {
  const getStatus = (index) => {
    if (completedSteps.includes(index)) return 'completed';
    if (index === currentStep) return 'current';
    if (steps[index].skipped) return 'skipped';
    if (steps[index].error) return 'error';
    return 'pending';
  };

  return (
    <div className="vertical-stepper">
      {steps.map((step, index) => (
        <SafStepperLabelIndicator 
          key={step.id}
          stepIndex={index}
          stepNumber={index + 1}
          status={getStatus(index)}
          label={step.label}
          description={step.description}
          optional={step.optional}
          orientation="vertical"
          size="large"
          onClick={onStepClick}
          showConnector={index < steps.length - 1}
          connectorPosition="after"
        />
      ))}
    </div>
  );
};
```

### Error State Indicators

```typescript
// React
const ErrorStateIndicators = ({ steps, currentStep, errors, onStepClick, onRetry }) => {
  const getStatus = (index) => {
    if (errors[index]) return 'error';
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  const handleClick = (stepIndex) => {
    if (errors[stepIndex]) {
      onRetry(stepIndex);
    } else {
      onStepClick(stepIndex);
    }
  };

  return (
    <div className="error-stepper">
      {steps.map((step, index) => (
        <div key={step.id} className="step-container">
          <SafStepperLabelIndicator 
            stepIndex={index}
            stepNumber={index + 1}
            status={getStatus(index)}
            label={step.label}
            description={step.description}
            icon={errors[index] ? <SafIcon name="alert-triangle" /> : null}
            onClick={handleClick}
            showConnector={index < steps.length - 1}
          />
          
          {errors[index] && (
            <SafTooltip 
              content={`Error: ${errors[index]}`}
              position="top"
              trigger="hover"
            >
              <SafButton 
                variant="ghost"
                size="small"
                icon={<SafIcon name="info" />}
                aria-label="View error details"
              />
            </SafTooltip>
          )}
        </div>
      ))}
    </div>
  );
};
```

### Optional Step Indicators

```typescript
// React
const OptionalStepIndicators = ({ steps, currentStep, onStepClick, onSkipStep }) => {
  const getStatus = (index) => {
    if (steps[index].skipped) return 'skipped';
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  const handleClick = (stepIndex) => {
    if (steps[stepIndex].optional && stepIndex === currentStep) {
      // Show skip option for optional current step
      return;
    }
    onStepClick(stepIndex);
  };

  return (
    <div className="optional-stepper">
      {steps.map((step, index) => (
        <div key={step.id} className="step-with-actions">
          <SafStepperLabelIndicator 
            stepIndex={index}
            stepNumber={index + 1}
            status={getStatus(index)}
            label={step.label}
            description={step.description}
            optional={step.optional}
            onClick={handleClick}
            showConnector={index < steps.length - 1}
          />
          
          {step.optional && index === currentStep && (
            <SafButton 
              variant="link"
              size="small"
              onClick={() => onSkipStep(index)}
              className="skip-button"
            >
              Skip this step
            </SafButton>
          )}
          
          {step.skipped && (
            <SafBadge 
              variant="neutral"
              size="small"
              className="skipped-badge"
            >
              Skipped
            </SafBadge>
          )}
        </div>
      ))}
    </div>
  );
};
```

### Minimal Progress Indicators

```typescript
// React
const MinimalProgressIndicators = ({ totalSteps, currentStep }) => {
  return (
    <div className="minimal-progress">
      {Array.from({ length: totalSteps }, (_, index) => (
        <SafStepperLabelIndicator 
          key={index}
          stepIndex={index}
          status={index < currentStep ? 'completed' : 
                  index === currentStep ? 'current' : 'pending'}
          variant="minimal"
          size="small"
          showNumber={false}
          clickable={false}
          showConnector={index < totalSteps - 1}
        />
      ))}
    </div>
  );
};
```

### Custom Styled Indicators

```typescript
// React
const CustomStyledIndicators = ({ steps, currentStep, onStepClick, theme }) => {
  const getCustomIcon = (step, status) => {
    const iconMap = {
      account: 'user',
      profile: 'edit-2',
      settings: 'settings',
      complete: 'check-circle'
    };

    if (status === 'completed') {
      return <SafIcon name="check" className="completed-icon" />;
    }
    
    return <SafIcon name={iconMap[step.type] || 'circle'} />;
  };

  const getCustomClassName = (status, index) => {
    const baseClass = 'custom-indicator';
    const statusClass = `${baseClass}--${status}`;
    const themeClass = `${baseClass}--${theme}`;
    
    return `${baseClass} ${statusClass} ${themeClass}`;
  };

  return (
    <div className={`custom-stepper theme-${theme}`}>
      {steps.map((step, index) => (
        <SafStepperLabelIndicator 
          key={step.id}
          stepIndex={index}
          stepNumber={index + 1}
          status={index < currentStep ? 'completed' : 
                  index === currentStep ? 'current' : 'pending'}
          label={step.label}
          description={step.description}
          icon={getCustomIcon(step, index < currentStep ? 'completed' : 
                             index === currentStep ? 'current' : 'pending')}
          onClick={onStepClick}
          className={getCustomClassName(index < currentStep ? 'completed' : 
                                       index === currentStep ? 'current' : 'pending', index)}
          showConnector={index < steps.length - 1}
        />
      ))}
    </div>
  );
};
```

### Interactive Indicators with Tooltips

```typescript
// React
const InteractiveIndicatorsWithTooltips = ({ steps, currentStep, onStepClick }) => {
  const [hoveredStep, setHoveredStep] = useState(null);

  const getTooltipContent = (step, index, status) => {
    const statusText = {
      completed: 'Completed',
      current: 'Current step',
      pending: 'Not started',
      error: 'Error occurred',
      skipped: 'Skipped'
    };

    return (
      <div className="step-tooltip">
        <div className="step-status">
          {statusText[status]} • Step {index + 1}
        </div>
        <div className="step-title">{step.label}</div>
        {step.description && (
          <div className="step-description">{step.description}</div>
        )}
        {step.optional && (
          <div className="step-optional">Optional</div>
        )}
      </div>
    );
  };

  const getStatus = (index) => {
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  return (
    <div className="interactive-stepper">
      {steps.map((step, index) => (
        <SafTooltip 
          key={step.id}
          content={getTooltipContent(step, index, getStatus(index))}
          position="top"
          trigger="hover"
          delay={500}
        >
          <SafStepperLabelIndicator 
            stepIndex={index}
            stepNumber={index + 1}
            status={getStatus(index)}
            label={step.label}
            optional={step.optional}
            onClick={onStepClick}
            onFocus={() => setHoveredStep(index)}
            onBlur={() => setHoveredStep(null)}
            showConnector={index < steps.length - 1}
            className={hoveredStep === index ? 'hovered' : ''}
          />
        </SafTooltip>
      ))}
    </div>
  );
};
```

### Animated Status Transitions

```typescript
// React
const AnimatedStatusTransitions = ({ steps, currentStep, onStepClick }) => {
  const [animatingSteps, setAnimatingSteps] = useState(new Set());

  const getStatus = (index) => {
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  useEffect(() => {
    // Animate status changes
    const newAnimating = new Set();
    steps.forEach((_, index) => {
      if (index === currentStep || index === currentStep - 1) {
        newAnimating.add(index);
      }
    });
    
    setAnimatingSteps(newAnimating);
    
    const timer = setTimeout(() => {
      setAnimatingSteps(new Set());
    }, 600);
    
    return () => clearTimeout(timer);
  }, [currentStep, steps]);

  return (
    <div className="animated-stepper">
      {steps.map((step, index) => (
        <SafStepperLabelIndicator 
          key={step.id}
          stepIndex={index}
          stepNumber={index + 1}
          status={getStatus(index)}
          label={step.label}
          description={step.description}
          onClick={onStepClick}
          showConnector={index < steps.length - 1}
          className={`
            animated-indicator
            ${animatingSteps.has(index) ? 'transitioning' : ''}
            ${getStatus(index) === 'completed' ? 'slide-in' : ''}
          `}
        />
      ))}
    </div>
  );
};
```

### Accessibility-Enhanced Indicators

```typescript
// React
const AccessibilityEnhancedIndicators = ({ 
  steps, 
  currentStep, 
  onStepClick,
  announcements 
}) => {
  const [focusedStep, setFocusedStep] = useState(null);

  const getAriaLabel = (step, index, status) => {
    const statusText = {
      completed: 'completed',
      current: 'current',
      pending: 'pending',
      error: 'has error',
      skipped: 'skipped'
    };

    let label = `Step ${index + 1} of ${steps.length}: ${step.label}. Status: ${statusText[status]}.`;
    
    if (step.optional) {
      label += ' Optional step.';
    }
    
    if (step.description) {
      label += ` ${step.description}`;
    }
    
    return label;
  };

  const getStatus = (index) => {
    if (index < currentStep) return 'completed';
    if (index === currentStep) return 'current';
    return 'pending';
  };

  const handleKeyDown = (stepIndex, event) => {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      onStepClick(stepIndex);
    }
  };

  return (
    <div 
      className="accessible-stepper"
      role="progressbar"
      aria-valuenow={currentStep + 1}
      aria-valuemin={1}
      aria-valuemax={steps.length}
      aria-label={`Step ${currentStep + 1} of ${steps.length}`}
    >
      {steps.map((step, index) => (
        <SafStepperLabelIndicator 
          key={step.id}
          stepIndex={index}
          stepNumber={index + 1}
          status={getStatus(index)}
          label={step.label}
          description={step.description}
          optional={step.optional}
          onClick={onStepClick}
          onKeyDown={handleKeyDown}
          onFocus={(stepIndex) => setFocusedStep(stepIndex)}
          onBlur={() => setFocusedStep(null)}
          showConnector={index < steps.length - 1}
          aria-label={getAriaLabel(step, index, getStatus(index))}
          role="button"
          tabIndex={0}
        />
      ))}
      
      {announcements && (
        <div 
          aria-live="polite"
          aria-atomic="true"
          className="sr-only"
        >
          {announcements}
        </div>
      )}
    </div>
  );
};
```

## Best Practices

### Visual Design
- **Consistent States**: Use consistent visual treatment for all status states
- **Clear Hierarchy**: Maintain clear visual hierarchy between different states
- **Icon Usage**: Use meaningful icons that enhance understanding
- **Color Coding**: Apply appropriate colors for different status states

### Interaction Design
- **Click Feedback**: Provide immediate visual feedback on click/tap
- **Hover States**: Show hover effects for clickable indicators
- **Focus Management**: Maintain visible focus indicators for keyboard users
- **Touch Targets**: Ensure adequate touch target size on mobile devices

### Accessibility
- **Semantic Markup**: Use appropriate ARIA roles and attributes
- **Keyboard Support**: Support Tab, Enter, and Space key interactions
- **Screen Reader Support**: Provide descriptive labels and status announcements
- **High Contrast**: Ensure indicators work in high contrast mode

### Performance
- **Lightweight Rendering**: Optimize for performance with many indicators
- **Animation Performance**: Use CSS animations over JavaScript where possible
- **Event Handling**: Efficiently manage event listeners
- **Memory Usage**: Clean up resources when components unmount

## Accessibility Considerations

- Uses appropriate ARIA roles including `button` and `progressbar` patterns
- Supports keyboard navigation with Tab, Enter, and Space key interactions
- Provides comprehensive screen reader support with descriptive labels
- Maintains proper focus management and visible focus indicators
- Includes status announcements for state changes
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafStepperLabel**: Parent stepper component
- **SafBadge**: Status badge component
- **SafIcon**: Icon component for status indicators
- **SafTooltip**: Tooltip component for additional information
- **SafButton**: Button component for interactive elements

## Notes

- SafStepperLabelIndicator automatically handles state-based styling
- The component supports both clickable and non-clickable modes
- Custom icons override default state-based icons
- Connector lines adapt to orientation and position settings
- The component integrates seamlessly with parent stepper layouts
- Status changes can trigger smooth CSS transitions
- Optional steps receive distinct visual treatment
- Error states are prominently highlighted with appropriate styling
