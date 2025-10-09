# SafStepper Component

The `SafStepper` component provides a visual progress indicator for multi-step processes in the Saffron Design System. Built on FAST Element with ResponsiveElement mixin, it displays sequential steps with status indicators and automatically adapts between horizontal and vertical orientations based on viewport size.

## Table of Contents

- [Overview](#overview)
- [Component Properties](#component-properties)
- [Events](#events)
- [Methods](#methods)
- [Parts](#parts)
- [Slots](#slots)
- [CSS Custom Properties](#css-custom-properties)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Step Component](#step-component)
- [Accessibility](#accessibility)
- [Best Practices](#best-practices)

## Overview

The SafStepper component provides a comprehensive solution for displaying multi-step workflows with clear visual progress indicators. It automatically manages step states, supports responsive behavior, and provides full accessibility support.

Key Features:
- **Step Management**: Automatic step numbering and status management
- **Responsive Behavior**: Automatic orientation switching based on viewport size
- **Status Indicators**: Visual indicators for completed, active, and inactive states
- **Accessibility**: Full ARIA support with proper navigation semantics
- **Customizable**: Configurable orientation, breakpoints, and step content
- **Event Emission**: Progress tracking through step change events

## Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `orientation` | `StepperOrientation` | `"horizontal"` | Visual orientation of the stepper |
| `ariaLabel` | `string` | `"progress"` | ARIA label for the stepper region |
| `observeResize` | `boolean` | `true` | Whether to enable responsive behavior |
| `activeStep` | `number` | `0` | Index of currently active step (0-based) |

### Orientation Options

The `orientation` property accepts these values:
- `"horizontal"` - Steps arranged in a horizontal row
- `"vertical"` - Steps arranged in a vertical column

### Read-Only Properties

| Property | Type | Description |
|----------|------|-------------|
| `steps` | `SafStepInstance[]` | Array of step elements within the stepper |
| `mode` | `'desktop' \| 'mobile'` | Current responsive mode (inherited from ResponsiveElement) |

## Events

| Event | Bubbles | Cancelable | Detail | Description |
|-------|---------|------------|--------|-------------|
| `step-change` | `true` | `false` | `number` | Fired when active step changes |
| `mode-change` | `true` | `false` | `string` | Fired when responsive mode changes |

## Methods

### Step Management

```typescript
// Find and initialize all step elements
stepper.findSteps(): void

// Update active step and status
stepper.updateStepper(step: number): void

// Add orientation class to step element
stepper.addOrientationClass(step: Element): void
```

### Internal Methods

```typescript
// Update step numbers based on current index
stepper.updateStepNumbers(step: SafStepInstance, index: number): void

// Update status of all steps based on active step
stepper.updateStepStatus(): void
```

## Parts

| Part | Description |
|------|-------------|
| `list` | The main stepper container |

## Slots

| Slot | Description |
|------|-------------|
| `(default)` | Container for `saf-step` elements |

## CSS Custom Properties

The SafStepper component uses the design system's spacing and responsive tokens:

```css
saf-stepper {
  /* Responsive breakpoint */
  --stepper-breakpoint: 768px;
  
  /* Orientation classes */
  --horizontal-gap: var(--space-lg);
  --vertical-gap: var(--space-md);
}
```

## React Integration

### Basic Usage

```tsx
import SafStepper from '@saffron/react/stepper';
import SafStep from '@saffron/react/step';

function BasicStepper() {
  return (
    <SafStepper>
      <SafStep status="completed" stepTitle="Setup">
        Complete your account setup
      </SafStep>
      <SafStep status="active" stepTitle="Configuration">
        Configure your preferences
      </SafStep>
      <SafStep status="inactive" stepTitle="Review">
        Review and confirm settings
      </SafStep>
    </SafStepper>
  );
}
```

### Controlled Stepper

```tsx
import SafStepper from '@saffron/react/stepper';
import SafStep from '@saffron/react/step';
import SafButton from '@saffron/react/button';
import { useState } from 'react';

function ControlledStepper() {
  const [currentStep, setCurrentStep] = useState(0);
  
  const steps = [
    { title: 'Personal Info', content: 'Enter your personal information' },
    { title: 'Account Details', content: 'Set up your account details' },
    { title: 'Confirmation', content: 'Review and confirm your information' }
  ];
  
  const handleStepChange = (event: CustomEvent) => {
    setCurrentStep(event.detail);
  };
  
  const nextStep = () => {
    if (currentStep < steps.length - 1) {
      setCurrentStep(currentStep + 1);
    }
  };
  
  const prevStep = () => {
    if (currentStep > 0) {
      setCurrentStep(currentStep - 1);
    }
  };
  
  return (
    <div>
      <SafStepper 
        activeStep={currentStep}
        onStepChange={handleStepChange}
        ariaLabel="Registration process"
      >
        {steps.map((step, index) => (
          <SafStep
            key={index}
            status={
              index < currentStep ? 'completed' :
              index === currentStep ? 'active' : 'inactive'
            }
            stepTitle={step.title}
          >
            {step.content}
          </SafStep>
        ))}
      </SafStepper>
      
      <div style={{ marginTop: '20px' }}>
        <SafButton 
          onClick={prevStep} 
          disabled={currentStep === 0}
        >
          Previous
        </SafButton>
        <SafButton 
          onClick={nextStep} 
          disabled={currentStep === steps.length - 1}
        >
          Next
        </SafButton>
      </div>
    </div>
  );
}
```

### Vertical Stepper

```tsx
import SafStepper from '@saffron/react/stepper';
import SafStep from '@saffron/react/step';

function VerticalStepper() {
  return (
    <SafStepper 
      orientation="vertical" 
      observeResize={false}
      ariaLabel="Setup wizard"
    >
      <SafStep status="completed" stepTitle="Account Created">
        Your account has been successfully created
      </SafStep>
      <SafStep status="completed" stepTitle="Profile Setup">
        Your profile information has been saved
      </SafStep>
      <SafStep status="active" stepTitle="Preferences">
        Configure your notification preferences
      </SafStep>
      <SafStep status="inactive" stepTitle="Complete">
        Finish setup and start using the application
      </SafStep>
    </SafStepper>
  );
}
```

### Responsive Stepper

```tsx
import SafStepper from '@saffron/react/stepper';
import SafStep from '@saffron/react/step';
import { useState } from 'react';

function ResponsiveStepper() {
  const [currentMode, setCurrentMode] = useState<'desktop' | 'mobile'>('desktop');
  
  const handleModeChange = (event: CustomEvent) => {
    setCurrentMode(event.detail);
  };
  
  return (
    <div>
      <p>Current mode: {currentMode}</p>
      <SafStepper 
        observeResize={true}
        onModeChange={handleModeChange}
        ariaLabel="Responsive workflow"
      >
        <SafStep status="completed" stepTitle="Start">
          Begin the process
        </SafStep>
        <SafStep status="active" stepTitle="Progress">
          Work in progress
        </SafStep>
        <SafStep status="inactive" stepTitle="Finish">
          Complete the process
        </SafStep>
      </SafStepper>
    </div>
  );
}
```

### With Custom Step Headers

```tsx
import SafStepper from '@saffron/react/stepper';
import SafStep from '@saffron/react/step';

function CustomHeaderStepper() {
  return (
    <SafStepper ariaLabel="Custom header workflow">
      <SafStep status="completed">
        <div slot="step-header">
          Step 1 of 3: Initial Setup
        </div>
        <div>
          <h3>Welcome to the setup process</h3>
          <p>This step helps you get started with the application.</p>
        </div>
      </SafStep>
      
      <SafStep status="active">
        <div slot="step-header">
          Step 2 of 3: Configuration
        </div>
        <div>
          <h3>Configure your settings</h3>
          <p>Customize the application to meet your needs.</p>
        </div>
      </SafStep>
      
      <SafStep status="inactive">
        <div slot="step-header">
          Step 3 of 3: Completion
        </div>
        <div>
          <h3>Finalize your setup</h3>
          <p>Review and complete your configuration.</p>
        </div>
      </SafStep>
    </SafStepper>
  );
}
```

## Angular Integration

### Basic Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-stepper',
  template: `
    <saf-stepper>
      <saf-step status="completed" step-title="Setup">
        Complete your account setup
      </saf-step>
      <saf-step status="active" step-title="Configuration">
        Configure your preferences
      </saf-step>
      <saf-step status="inactive" step-title="Review">
        Review and confirm settings
      </saf-step>
    </saf-stepper>
  `
})
export class BasicStepperComponent {}
```

### Controlled Stepper Service

```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject, Observable } from 'rxjs';

export interface StepData {
  title: string;
  content: string;
  completed: boolean;
}

@Injectable({
  providedIn: 'root'
})
export class StepperService {
  private currentStepSubject = new BehaviorSubject<number>(0);
  public currentStep$: Observable<number> = this.currentStepSubject.asObservable();
  
  private stepsSubject = new BehaviorSubject<StepData[]>([
    { title: 'Personal Info', content: 'Enter personal information', completed: false },
    { title: 'Account Setup', content: 'Configure account settings', completed: false },
    { title: 'Verification', content: 'Verify your information', completed: false }
  ]);
  public steps$: Observable<StepData[]> = this.stepsSubject.asObservable();
  
  get currentStep(): number {
    return this.currentStepSubject.value;
  }
  
  get steps(): StepData[] {
    return this.stepsSubject.value;
  }
  
  nextStep(): void {
    const current = this.currentStep;
    if (current < this.steps.length - 1) {
      // Mark current step as completed
      this.markStepCompleted(current);
      this.currentStepSubject.next(current + 1);
    }
  }
  
  previousStep(): void {
    const current = this.currentStep;
    if (current > 0) {
      this.currentStepSubject.next(current - 1);
    }
  }
  
  goToStep(stepIndex: number): void {
    if (stepIndex >= 0 && stepIndex < this.steps.length) {
      this.currentStepSubject.next(stepIndex);
    }
  }
  
  markStepCompleted(stepIndex: number): void {
    const steps = [...this.steps];
    if (steps[stepIndex]) {
      steps[stepIndex].completed = true;
      this.stepsSubject.next(steps);
    }
  }
  
  resetStepper(): void {
    this.currentStepSubject.next(0);
    const steps = this.steps.map(step => ({ ...step, completed: false }));
    this.stepsSubject.next(steps);
  }
}
```

### Controlled Stepper Component

```typescript
import { Component, OnInit } from '@angular/core';
import { StepperService } from './stepper.service';

@Component({
  selector: 'app-controlled-stepper',
  template: `
    <saf-stepper 
      [active-step]="currentStep"
      [aria-label]="'Registration process'"
      (step-change)="onStepChange($event)">
      
      <saf-step 
        *ngFor="let step of steps; let i = index"
        [status]="getStepStatus(i)"
        [step-title]="step.title">
        {{ step.content }}
      </saf-step>
    </saf-stepper>
    
    <div class="stepper-controls">
      <button 
        type="button"
        (click)="previousStep()"
        [disabled]="currentStep === 0">
        Previous
      </button>
      
      <button 
        type="button"
        (click)="nextStep()"
        [disabled]="currentStep === steps.length - 1">
        Next
      </button>
      
      <button 
        type="button"
        (click)="resetStepper()">
        Reset
      </button>
    </div>
    
    <div class="step-info">
      <p>Current step: {{ currentStep + 1 }} of {{ steps.length }}</p>
      <p>Step: {{ steps[currentStep]?.title }}</p>
    </div>
  `
})
export class ControlledStepperComponent implements OnInit {
  currentStep = 0;
  steps: any[] = [];
  
  constructor(private stepperService: StepperService) {}
  
  ngOnInit() {
    this.stepperService.currentStep$.subscribe(step => {
      this.currentStep = step;
    });
    
    this.stepperService.steps$.subscribe(steps => {
      this.steps = steps;
    });
  }
  
  getStepStatus(index: number): string {
    if (index < this.currentStep || this.steps[index]?.completed) {
      return 'completed';
    } else if (index === this.currentStep) {
      return 'active';
    } else {
      return 'inactive';
    }
  }
  
  onStepChange(event: CustomEvent) {
    this.stepperService.goToStep(event.detail);
  }
  
  nextStep() {
    this.stepperService.nextStep();
  }
  
  previousStep() {
    this.stepperService.previousStep();
  }
  
  resetStepper() {
    this.stepperService.resetStepper();
  }
}
```

### Responsive Stepper

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-responsive-stepper',
  template: `
    <div>
      <p>Current mode: {{ currentMode }}</p>
      <p>Current orientation: {{ currentOrientation }}</p>
      
      <saf-stepper 
        [observe-resize]="true"
        [aria-label]="'Responsive workflow'"
        (mode-change)="onModeChange($event)">
        
        <saf-step 
          *ngFor="let step of workflowSteps; let i = index"
          [status]="step.status"
          [step-title]="step.title">
          <div [innerHTML]="step.content"></div>
        </saf-step>
      </saf-stepper>
    </div>
  `,
  styles: [`
    .mobile-layout {
      padding: 10px;
    }
    
    .desktop-layout {
      padding: 20px;
    }
  `]
})
export class ResponsiveStepperComponent {
  currentMode: 'desktop' | 'mobile' = 'desktop';
  currentOrientation: 'horizontal' | 'vertical' = 'horizontal';
  
  workflowSteps = [
    {
      title: 'Analysis',
      status: 'completed',
      content: '<h3>Data Analysis</h3><p>Analyze the provided data set.</p>'
    },
    {
      title: 'Processing',
      status: 'active',
      content: '<h3>Data Processing</h3><p>Process and transform the data.</p>'
    },
    {
      title: 'Validation',
      status: 'inactive',
      content: '<h3>Validation</h3><p>Validate the processed results.</p>'
    },
    {
      title: 'Export',
      status: 'inactive',
      content: '<h3>Export Results</h3><p>Export the final results.</p>'
    }
  ];
  
  onModeChange(event: CustomEvent) {
    this.currentMode = event.detail;
    this.currentOrientation = this.currentMode === 'mobile' ? 'vertical' : 'horizontal';
  }
}
```

### Form Integration

```typescript
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-form-stepper',
  template: `
    <form [formGroup]="registrationForm" (ngSubmit)="onSubmit()">
      <saf-stepper 
        [active-step]="currentFormStep"
        [aria-label]="'Registration form'">
        
        <!-- Personal Information Step -->
        <saf-step 
          [status]="getStepStatus(0)" 
          step-title="Personal Info">
          <div formGroupName="personalInfo">
            <label>
              First Name:
              <input 
                type="text" 
                formControlName="firstName" 
                required>
            </label>
            <label>
              Last Name:
              <input 
                type="text" 
                formControlName="lastName" 
                required>
            </label>
            <label>
              Email:
              <input 
                type="email" 
                formControlName="email" 
                required>
            </label>
          </div>
        </saf-step>
        
        <!-- Account Setup Step -->
        <saf-step 
          [status]="getStepStatus(1)" 
          step-title="Account Setup">
          <div formGroupName="accountInfo">
            <label>
              Username:
              <input 
                type="text" 
                formControlName="username" 
                required>
            </label>
            <label>
              Password:
              <input 
                type="password" 
                formControlName="password" 
                required>
            </label>
          </div>
        </saf-step>
        
        <!-- Review Step -->
        <saf-step 
          [status]="getStepStatus(2)" 
          step-title="Review">
          <div class="review-section">
            <h3>Review Your Information</h3>
            <p><strong>Name:</strong> {{ getFullName() }}</p>
            <p><strong>Email:</strong> {{ registrationForm.get('personalInfo.email')?.value }}</p>
            <p><strong>Username:</strong> {{ registrationForm.get('accountInfo.username')?.value }}</p>
          </div>
        </saf-step>
      </saf-stepper>
      
      <div class="form-controls">
        <button 
          type="button" 
          (click)="previousFormStep()"
          [disabled]="currentFormStep === 0">
          Previous
        </button>
        
        <button 
          type="button" 
          (click)="nextFormStep()"
          [disabled]="!canProceedToNextStep()"
          *ngIf="currentFormStep < 2">
          Next
        </button>
        
        <button 
          type="submit"
          [disabled]="!registrationForm.valid"
          *ngIf="currentFormStep === 2">
          Submit Registration
        </button>
      </div>
    </form>
  `
})
export class FormStepperComponent {
  currentFormStep = 0;
  registrationForm: FormGroup;
  
  constructor(private fb: FormBuilder) {
    this.registrationForm = this.fb.group({
      personalInfo: this.fb.group({
        firstName: ['', Validators.required],
        lastName: ['', Validators.required],
        email: ['', [Validators.required, Validators.email]]
      }),
      accountInfo: this.fb.group({
        username: ['', Validators.required],
        password: ['', [Validators.required, Validators.minLength(8)]]
      })
    });
  }
  
  getStepStatus(stepIndex: number): string {
    if (stepIndex < this.currentFormStep) {
      return 'completed';
    } else if (stepIndex === this.currentFormStep) {
      return 'active';
    } else {
      return 'inactive';
    }
  }
  
  canProceedToNextStep(): boolean {
    switch (this.currentFormStep) {
      case 0:
        return this.registrationForm.get('personalInfo')?.valid || false;
      case 1:
        return this.registrationForm.get('accountInfo')?.valid || false;
      default:
        return true;
    }
  }
  
  nextFormStep() {
    if (this.canProceedToNextStep() && this.currentFormStep < 2) {
      this.currentFormStep++;
    }
  }
  
  previousFormStep() {
    if (this.currentFormStep > 0) {
      this.currentFormStep--;
    }
  }
  
  getFullName(): string {
    const firstName = this.registrationForm.get('personalInfo.firstName')?.value || '';
    const lastName = this.registrationForm.get('personalInfo.lastName')?.value || '';
    return `${firstName} ${lastName}`.trim();
  }
  
  onSubmit() {
    if (this.registrationForm.valid) {
      console.log('Registration submitted:', this.registrationForm.value);
      // Handle form submission
    }
  }
}
```

## Usage Examples

### Basic Horizontal Stepper

```html
<saf-stepper>
  <saf-step status="completed" step-title="Setup">
    Complete initial setup
  </saf-step>
  <saf-step status="active" step-title="Configure">
    Configure your settings
  </saf-step>
  <saf-step status="inactive" step-title="Finish">
    Review and finish
  </saf-step>
</saf-stepper>
```

### Vertical Stepper

```html
<saf-stepper orientation="vertical" observe-resize="false">
  <saf-step status="completed" step-title="Download">
    Download the application
  </saf-step>
  <saf-step status="completed" step-title="Install">
    Install on your device
  </saf-step>
  <saf-step status="active" step-title="Setup">
    Complete the setup process
  </saf-step>
</saf-stepper>
```

### Responsive Stepper

```html
<saf-stepper observe-resize="true" aria-label="Installation process">
  <saf-step status="completed" step-title="Preparation">
    Prepare your environment
  </saf-step>
  <saf-step status="active" step-title="Installation">
    Installing components
  </saf-step>
  <saf-step status="inactive" step-title="Configuration">
    Configure settings
  </saf-step>
</saf-stepper>
```

### With Custom Headers

```html
<saf-stepper aria-label="Custom workflow">
  <saf-step status="completed">
    <div slot="step-header">Step 1 of 4: Initial Analysis</div>
    <div>
      <h3>Data Analysis Complete</h3>
      <p>Successfully analyzed the input data.</p>
    </div>
  </saf-step>
  
  <saf-step status="active">
    <div slot="step-header">Step 2 of 4: Processing</div>
    <div>
      <h3>Processing Data</h3>
      <p>Currently processing the analyzed data.</p>
    </div>
  </saf-step>
  
  <saf-step status="inactive">
    <div slot="step-header">Step 3 of 4: Validation</div>
    <div>
      <h3>Validation Pending</h3>
      <p>Validation will begin after processing.</p>
    </div>
  </saf-step>
</saf-stepper>
```

### Stepper with Event Handling

```javascript
const stepper = document.querySelector('saf-stepper');

// Listen for step changes
stepper.addEventListener('step-change', (event) => {
  console.log('Active step changed to:', event.detail);
  updateUI(event.detail);
});

// Listen for responsive mode changes
stepper.addEventListener('mode-change', (event) => {
  console.log('Mode changed to:', event.detail);
  adjustLayout(event.detail);
});

// Programmatically update stepper
function nextStep() {
  const currentStep = stepper.activeStep;
  stepper.updateStepper(currentStep + 1);
}
```

## Step Component

The SafStep component is used within SafStepper to represent individual steps:

### Step Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `status` | `StepStatus` | `"active"` | Status of the step |
| `statusLabel` | `string` | - | ARIA label for step status |
| `stepTitle` | `string` | - | Title of the step |
| `stepNumber` | `number` | `0` | Step number (auto-assigned) |
| `totalSteps` | `number` | `0` | Total number of steps (auto-assigned) |

### Step Status Values

- `"active"` - Currently active step
- `"completed"` - Completed step
- `"inactive"` - Future/inactive step

### Step Slots

| Slot | Description |
|------|-------------|
| `step-header` | Custom step header content |
| `(default)` | Main step content |

## Accessibility

The SafStepper component provides comprehensive accessibility support:

### ARIA Implementation
- **role="list"**: Applied to stepper container
- **role="listitem"**: Applied to each step
- **aria-label**: Configurable label for the entire stepper
- **Step Headers**: Automatically generated or custom step headers
- **Status Indicators**: Clear status communication for screen readers

### Keyboard Support
- **Tab Navigation**: Move between interactive elements within steps
- **Arrow Keys**: Navigate between steps (when interactive)
- **Enter/Space**: Activate step controls
- **Focus Management**: Proper focus indicators and management

### Screen Reader Support
- **Progressive Disclosure**: Steps announced as user progresses
- **Status Updates**: Step completion and activation announced
- **Context Information**: Step numbers and total count provided
- **Orientation Awareness**: Layout changes announced appropriately

### Focus Management
- **Visible Focus**: Clear focus indicators on interactive elements
- **Logical Order**: Tab order follows visual step sequence
- **Focus Restoration**: Focus maintained during orientation changes

## Best Practices

### Step Management
- Use meaningful step titles that clearly describe the action or content
- Provide step content that gives clear instructions or information
- Keep step count reasonable (typically 3-7 steps for optimal UX)

### Status Management
- Update step status based on actual completion, not just progression
- Use "completed" status only for fully finished steps
- Maintain consistent status logic throughout the workflow

### Responsive Design
- Enable `observeResize` for most use cases to provide optimal mobile experience
- Test stepper behavior at various screen sizes
- Consider content complexity when designing for mobile vertical layout

### Content Guidelines
- Keep step titles concise but descriptive
- Provide clear step content that guides users
- Use progressive disclosure to avoid overwhelming users
- Include helpful context or instructions in each step

### Event Handling
- Listen for `step-change` events to coordinate with application state
- Handle `mode-change` events if custom responsive behavior is needed
- Provide appropriate feedback when users complete steps

### Accessibility
- Always provide a meaningful `aria-label` for the stepper
- Use semantic HTML within step content
- Ensure sufficient color contrast for all step states
- Test with keyboard navigation and screen readers

### Performance
- Avoid complex computations in step content that could affect responsiveness
- Use efficient event handling for step changes
- Consider lazy loading for steps with heavy content

The SafStepper component provides a robust solution for multi-step workflows while maintaining excellent user experience and accessibility standards across all devices and interaction modes.
