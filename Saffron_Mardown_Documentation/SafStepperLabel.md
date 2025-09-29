# SafStepperLabel

## Overview

SafStepperLabel is a navigation component that provides step indicators for multi-step processes such as wizards, onboarding flows, or form sequences. It displays the current progress, allows navigation between steps, and shows completion states with clear visual indicators and accessibility support.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `steps` | `StepperStep[]` | `[]` | Array of stepper step configurations |
| `currentStep` | `number` | `0` | Current active step index |
| `completedSteps` | `number[]` | `[]` | Array of completed step indices |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `variant` | `'default' \| 'compact' \| 'minimal'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `clickable` | `boolean` | `true` | Allow clicking on steps to navigate |
| `allowSkipping` | `boolean` | `false` | Allow navigation to future steps |
| `showNumbers` | `boolean` | `true` | Show step numbers in indicators |
| `showConnectors` | `boolean` | `true` | Show connecting lines between steps |
| `disabled` | `boolean` | `false` | Disable all step interactions |
| `error` | `boolean` | `false` | Show error state for current step |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### StepperStep Interface

```typescript
interface StepperStep {
  id: string;
  label: string;
  description?: string;
  icon?: ReactElement;
  optional?: boolean;
  disabled?: boolean;
  error?: boolean;
  completed?: boolean;
  href?: string;
  status?: 'pending' | 'current' | 'completed' | 'error' | 'skipped';
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onStepClick` | `(stepIndex: number, step: StepperStep) => void` | Fired when step is clicked |
| `onStepChange` | `(stepIndex: number, step: StepperStep) => void` | Fired when current step changes |
| `onStepComplete` | `(stepIndex: number, step: StepperStep) => void` | Fired when step is marked complete |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `steps` | `StepperStep[]` | `[]` | Array of stepper step configurations |
| `currentStep` | `number` | `0` | Current active step index |
| `completedSteps` | `number[]` | `[]` | Array of completed step indices |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `variant` | `'default' \| 'compact' \| 'minimal'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `clickable` | `boolean` | `true` | Allow clicking on steps to navigate |
| `allowSkipping` | `boolean` | `false` | Allow navigation to future steps |
| `showNumbers` | `boolean` | `true` | Show step numbers in indicators |
| `showConnectors` | `boolean` | `true` | Show connecting lines between steps |
| `disabled` | `boolean` | `false` | Disable all step interactions |
| `error` | `boolean` | `false` | Show error state for current step |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `stepClick` | `EventEmitter<{stepIndex: number, step: StepperStep}>` | Fired when step is clicked |
| `stepChange` | `EventEmitter<{stepIndex: number, step: StepperStep}>` | Fired when current step changes |
| `stepComplete` | `EventEmitter<{stepIndex: number, step: StepperStep}>` | Fired when step is marked complete |

## Usage Examples

### Basic Horizontal Stepper

```typescript
// React
const BasicStepper = ({ currentStep, onStepChange }) => {
  const steps = [
    {
      id: 'personal',
      label: 'Personal Information',
      description: 'Enter your basic details'
    },
    {
      id: 'contact',
      label: 'Contact Details',
      description: 'Phone and email information'
    },
    {
      id: 'preferences',
      label: 'Preferences',
      description: 'Choose your settings'
    },
    {
      id: 'review',
      label: 'Review',
      description: 'Review and submit'
    }
  ];

  const handleStepClick = (stepIndex, step) => {
    if (stepIndex <= currentStep) {
      onStepChange(stepIndex);
    }
  };

  return (
    <SafStepperLabel 
      steps={steps}
      currentStep={currentStep}
      completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
      onStepClick={handleStepClick}
      orientation="horizontal"
    />
  );
};
```

```html
<!-- Angular -->
<saf-stepper-label 
  [steps]="steps"
  [currentStep]="currentStep"
  [completedSteps]="completedSteps"
  (stepClick)="onStepClick($event)"
  orientation="horizontal">
</saf-stepper-label>
```

### Vertical Stepper with Icons

```typescript
// React
const VerticalStepperWithIcons = ({ currentStep, onStepChange }) => {
  const steps = [
    {
      id: 'account',
      label: 'Create Account',
      description: 'Set up your user account',
      icon: <SafIcon name="user-plus" />
    },
    {
      id: 'verify',
      label: 'Verify Email',
      description: 'Confirm your email address',
      icon: <SafIcon name="mail" />
    },
    {
      id: 'profile',
      label: 'Complete Profile',
      description: 'Add your profile information',
      icon: <SafIcon name="edit" />
    },
    {
      id: 'preferences',
      label: 'Set Preferences',
      description: 'Choose your settings',
      icon: <SafIcon name="settings" />,
      optional: true
    },
    {
      id: 'welcome',
      label: 'Welcome',
      description: 'You\'re all set!',
      icon: <SafIcon name="check-circle" />
    }
  ];

  return (
    <div className="onboarding-flow">
      <SafStepperLabel 
        steps={steps}
        currentStep={currentStep}
        completedSteps={[0, 1]} // Account and verify completed
        onStepClick={onStepChange}
        orientation="vertical"
        variant="default"
        size="medium"
      />
    </div>
  );
};
```

### Compact Stepper

```typescript
// React
const CompactStepper = ({ currentStep, totalSteps, onStepChange }) => {
  const steps = Array.from({ length: totalSteps }, (_, i) => ({
    id: `step-${i + 1}`,
    label: `Step ${i + 1}`,
    description: `Complete step ${i + 1}`
  }));

  return (
    <SafStepperLabel 
      steps={steps}
      currentStep={currentStep}
      completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
      onStepChange={onStepChange}
      variant="compact"
      size="small"
      showConnectors={false}
    />
  );
};
```

### Error State Stepper

```typescript
// React
const ErrorStateStepper = ({ currentStep, errorStep, onStepChange, onRetryStep }) => {
  const steps = [
    {
      id: 'upload',
      label: 'Upload Files',
      description: 'Select and upload your documents'
    },
    {
      id: 'process',
      label: 'Process Data',
      description: 'Analyze uploaded files',
      error: errorStep === 1
    },
    {
      id: 'validate',
      label: 'Validate Results',
      description: 'Review processing results'
    },
    {
      id: 'complete',
      label: 'Complete',
      description: 'Finalize your submission'
    }
  ];

  const handleStepClick = (stepIndex, step) => {
    if (step.error) {
      onRetryStep(stepIndex);
    } else if (stepIndex <= currentStep) {
      onStepChange(stepIndex);
    }
  };

  return (
    <div className="upload-wizard">
      <SafStepperLabel 
        steps={steps}
        currentStep={currentStep}
        completedSteps={[0]} // Only first step completed
        onStepClick={handleStepClick}
        error={errorStep !== null}
      />
      
      {errorStep !== null && (
        <SafMessageBox 
          type="error"
          title="Processing Error"
          message="Failed to process uploaded files. Click the step to retry."
          dismissible
        />
      )}
    </div>
  );
};
```

### Minimal Progress Stepper

```typescript
// React
const MinimalProgressStepper = ({ progress, steps }) => {
  const stepItems = steps.map((step, index) => ({
    id: step.id,
    label: step.label,
    status: index < progress ? 'completed' : 
            index === progress ? 'current' : 'pending'
  }));

  return (
    <div className="progress-indicator">
      <div className="progress-header">
        <h3>Setup Progress</h3>
        <span className="progress-text">
          {progress + 1} of {steps.length}
        </span>
      </div>
      
      <SafStepperLabel 
        steps={stepItems}
        currentStep={progress}
        completedSteps={Array.from({ length: progress }, (_, i) => i)}
        variant="minimal"
        clickable={false}
        showNumbers={false}
      />
    </div>
  );
};
```

### Branching Stepper

```typescript
// React
const BranchingStepper = ({ currentPath, currentStep, onStepChange }) => {
  const getSteps = (path) => {
    const baseSteps = [
      {
        id: 'start',
        label: 'Getting Started',
        description: 'Choose your setup path'
      }
    ];

    if (path === 'individual') {
      return [
        ...baseSteps,
        {
          id: 'personal',
          label: 'Personal Info',
          description: 'Your personal details'
        },
        {
          id: 'preferences',
          label: 'Preferences',
          description: 'Set your preferences'
        }
      ];
    } else if (path === 'business') {
      return [
        ...baseSteps,
        {
          id: 'company',
          label: 'Company Info',
          description: 'Your business details'
        },
        {
          id: 'team',
          label: 'Team Setup',
          description: 'Invite team members'
        },
        {
          id: 'billing',
          label: 'Billing',
          description: 'Payment information'
        }
      ];
    }

    return baseSteps;
  };

  const steps = getSteps(currentPath);

  return (
    <SafStepperLabel 
      steps={steps}
      currentStep={currentStep}
      completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
      onStepClick={onStepChange}
      allowSkipping={false}
    />
  );
};
```

### Mobile-Optimized Stepper

```typescript
// React
const MobileOptimizedStepper = ({ currentStep, steps, onStepChange }) => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  if (isMobile) {
    // Show compact version on mobile
    return (
      <div className="mobile-stepper">
        <div className="step-counter">
          Step {currentStep + 1} of {steps.length}
        </div>
        <div className="current-step">
          <h3>{steps[currentStep].label}</h3>
          <p>{steps[currentStep].description}</p>
        </div>
        <SafStepperLabel 
          steps={steps}
          currentStep={currentStep}
          completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
          variant="compact"
          size="small"
          clickable={false}
          showNumbers={false}
          showConnectors
        />
      </div>
    );
  }

  return (
    <SafStepperLabel 
      steps={steps}
      currentStep={currentStep}
      completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
      onStepClick={onStepChange}
      orientation="horizontal"
    />
  );
};
```

### Interactive Stepper with Validation

```typescript
// React
const InteractiveStepperWithValidation = ({ 
  currentStep, 
  stepData, 
  validationErrors,
  onStepChange,
  onValidateStep 
}) => {
  const steps = [
    {
      id: 'basic',
      label: 'Basic Information',
      description: 'Name, email, phone',
      error: validationErrors.basic?.length > 0
    },
    {
      id: 'address',
      label: 'Address',
      description: 'Shipping and billing address',
      error: validationErrors.address?.length > 0
    },
    {
      id: 'payment',
      label: 'Payment Method',
      description: 'Credit card information',
      error: validationErrors.payment?.length > 0
    },
    {
      id: 'confirmation',
      label: 'Confirmation',
      description: 'Review your order'
    }
  ];

  const handleStepClick = async (stepIndex, step) => {
    // Validate current step before allowing navigation
    if (stepIndex > currentStep) {
      const isValid = await onValidateStep(currentStep);
      if (!isValid) return;
    }
    
    onStepChange(stepIndex);
  };

  const getCompletedSteps = () => {
    const completed = [];
    for (let i = 0; i < currentStep; i++) {
      const stepKey = steps[i].id;
      if (!validationErrors[stepKey]?.length) {
        completed.push(i);
      }
    }
    return completed;
  };

  return (
    <div className="checkout-stepper">
      <SafStepperLabel 
        steps={steps}
        currentStep={currentStep}
        completedSteps={getCompletedSteps()}
        onStepClick={handleStepClick}
        allowSkipping={false}
        error={validationErrors[steps[currentStep]?.id]?.length > 0}
      />
      
      {/* Show validation errors for current step */}
      {validationErrors[steps[currentStep]?.id]?.map((error, index) => (
        <SafAlert 
          key={index}
          type="error" 
          message={error}
          className="step-error"
        />
      ))}
    </div>
  );
};
```

### Animated Progress Stepper

```typescript
// React
const AnimatedProgressStepper = ({ progress, steps, onStepChange }) => {
  const [animationClass, setAnimationClass] = useState('');

  useEffect(() => {
    setAnimationClass('step-transition');
    const timer = setTimeout(() => setAnimationClass(''), 300);
    return () => clearTimeout(timer);
  }, [progress]);

  const stepItems = steps.map((step, index) => ({
    ...step,
    status: index < progress ? 'completed' :
            index === progress ? 'current' :
            'pending'
  }));

  return (
    <div className={`animated-stepper ${animationClass}`}>
      <div className="step-progress-bar">
        <div 
          className="progress-fill"
          style={{ 
            width: `${(progress / (steps.length - 1)) * 100}%` 
          }}
        />
      </div>
      
      <SafStepperLabel 
        steps={stepItems}
        currentStep={progress}
        completedSteps={Array.from({ length: progress }, (_, i) => i)}
        onStepClick={onStepChange}
        className="animated-steps"
      />
      
      <div className="step-content">
        <h2>{steps[progress].label}</h2>
        <p>{steps[progress].description}</p>
      </div>
    </div>
  );
};
```

### Accessibility-Enhanced Stepper

```typescript
// React
const AccessibilityEnhancedStepper = ({ 
  currentStep, 
  steps, 
  onStepChange,
  announcements 
}) => {
  const [liveRegionContent, setLiveRegionContent] = useState('');

  useEffect(() => {
    const currentStepData = steps[currentStep];
    const announcement = `Step ${currentStep + 1} of ${steps.length}: ${currentStepData.label}. ${currentStepData.description}`;
    setLiveRegionContent(announcement);
  }, [currentStep, steps]);

  const handleStepClick = (stepIndex, step) => {
    onStepChange(stepIndex);
    
    // Announce step change
    const announcement = `Navigated to step ${stepIndex + 1}: ${step.label}`;
    setLiveRegionContent(announcement);
  };

  return (
    <div className="accessible-stepper">
      <div 
        role="progressbar"
        aria-valuenow={currentStep + 1}
        aria-valuemin={1}
        aria-valuemax={steps.length}
        aria-label={`Step ${currentStep + 1} of ${steps.length}`}
        className="sr-only"
      />
      
      <SafStepperLabel 
        steps={steps}
        currentStep={currentStep}
        completedSteps={Array.from({ length: currentStep }, (_, i) => i)}
        onStepClick={handleStepClick}
        aria-label="Form progress steps"
      />
      
      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {liveRegionContent}
      </div>
      
      {announcements && (
        <div 
          aria-live="assertive"
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

### Navigation
- **Linear Flow**: Use linear progression for mandatory sequential steps
- **Skip Prevention**: Prevent skipping required steps unless explicitly allowed
- **Back Navigation**: Always allow users to go back to previous steps
- **Clear States**: Provide clear visual feedback for current, completed, and error states

### User Experience
- **Progress Indication**: Show clear progress through the overall process
- **Step Labels**: Use concise, descriptive labels for each step
- **Visual Hierarchy**: Maintain consistent visual hierarchy across all steps
- **Mobile Optimization**: Adapt layout and interaction for mobile devices

### Accessibility
- **Keyboard Navigation**: Support Tab, Enter, and arrow key navigation
- **Screen Readers**: Provide proper ARIA labels and live region updates
- **Focus Management**: Maintain logical focus order and visible focus indicators
- **Progress Announcements**: Announce step changes and progress updates

### Performance
- **Lazy Loading**: Load step content on demand when possible
- **State Management**: Efficiently manage step state and validation
- **Animation Performance**: Use performant CSS animations for transitions
- **Memory Management**: Clean up event listeners and timers

## Accessibility Considerations

- Uses proper ARIA roles including `progressbar` and `tablist` patterns
- Supports keyboard navigation with Tab, Enter, and arrow keys
- Provides screen reader announcements for step changes and progress
- Maintains proper focus management and visible focus indicators
- Includes aria-labels and descriptions for step context
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML elements for proper document structure

## Related Components

- **SafStepperLabelIndicator**: Individual step indicator component
- **SafBreadcrumb**: Alternative navigation for hierarchical paths
- **SafProgressRing**: Circular progress indicator
- **SafTab**: Tab-based navigation component
- **SafWizard**: Full wizard container component

## Notes

- SafStepperLabel automatically manages step state transitions
- The component supports both linear and non-linear step navigation
- Error states are prominently displayed with appropriate styling
- Optional steps are clearly indicated with different visual treatment
- The component adapts to different screen sizes and orientations
- Custom icons and content can be provided for each step
- Validation integration allows for step-by-step form validation
- Progress tracking helps users understand their position in the process
