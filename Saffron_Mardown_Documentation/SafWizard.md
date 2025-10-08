# SafWizard

The `SafWizard` component is a comprehensive multi-step interface that guides users through complex processes or data entry workflows. It combines a visual stepper with content panels and provides responsive behavior that adapts to different screen sizes automatically.

## Table of Contents

- [Overview](#overview)
- [Component Structure](#component-structure)
- [API Reference](#api-reference)
- [Usage Examples](#usage-examples)
- [Responsive Behavior](#responsive-behavior)
- [Accessibility](#accessibility)
- [Styling](#styling)
- [Integration](#integration)
- [Best Practices](#best-practices)

## Overview

SafWizard is a composite component that includes:
- **SafWizard**: Main container that manages the wizard flow and responsive behavior
- **SafStepper**: Progress indicator showing current step and available steps
- **SafWizardStepContent**: Individual content panels for each step
- **Responsive Layout**: Automatic adaptation between desktop and mobile layouts

The wizard automatically integrates with the ResponsiveElement mixin to provide seamless responsive behavior, switching between horizontal and vertical layouts based on screen size.

### Key Features

- **Responsive Design**: Automatically adapts layout for mobile and desktop
- **Progressive Disclosure**: Shows only current step content
- **Accessible Navigation**: Full keyboard and screen reader support
- **Customizable Steps**: Flexible step configuration with custom content
- **Heading Management**: Configurable heading levels for content hierarchy
- **Focus Management**: Automatic focus handling during step transitions

## Component Structure

```
SafWizard (ResponsiveElement)
├── SafStepper (horizontal/vertical based on screen size)
│   ├── SafStep (status: active, completed, inactive)
│   ├── SafStep
│   └── SafStep
├── Step Header (desktop) / Mobile Header (mobile)
├── SafWizardStepContent (visible for active step)
│   └── Step Content
└── Footer Slot (for navigation buttons)
```

## API Reference

### SafWizard

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `a11yAriaLabel` | `string` | `"Wizard Stepper"` | Accessible label for the wizard complementary region |
| `headingLevel` | `number` | `1` | Heading level (1-6) for step titles |
| `mode` | `"desktop" \| "mobile" \| "auto"` | `"auto"` | Layout mode (auto switches based on screen size) |

#### Events

| Event | Type | Description |
|-------|------|-------------|
| `step-change` | `CustomEvent<{ detail: number }>` | Fired when the active step changes |

#### Parts

| Part | Description |
|------|-------------|
| `wizard-container` | Main wizard container |
| `wizard-content-container` | Container for step content |
| `wizard-content` | Step content wrapper |
| `step-header` | Step title header (desktop mode) |
| `step-header-mobile` | Step title and description header (mobile mode) |
| `step-content` | Container for step content |

#### Slots

| Slot | Description |
|------|-------------|
| `stepper` | SafStepper component |
| `(default)` | SafWizardStepContent components |
| `footer` | Navigation buttons and controls |
| `step-header-mobile` | Custom mobile header content |

### SafWizardStepContent

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `step` | `number` | `undefined` | Step number (1-based) |
| `hidden` | `boolean` | `true` | Whether the step content is hidden |

#### Slots

| Slot | Description |
|------|-------------|
| `(default)` | Step content |

## Usage Examples

### Basic Wizard

```html
<!-- HTML -->
<saf-wizard a11y-aria-label="Account Setup Wizard" heading-level="2">
  <!-- Stepper -->
  <saf-stepper slot="stepper" active-step="1" orientation="horizontal">
    <saf-step status="active" step-title="Personal Info">
      <div>Enter your personal information</div>
    </saf-step>
    <saf-step status="inactive" step-title="Account Details">
      <div>Configure your account</div>
    </saf-step>
    <saf-step status="inactive" step-title="Confirmation">
      <div>Review and confirm</div>
    </saf-step>
  </saf-stepper>

  <!-- Step Content -->
  <saf-wizard-step-content step="1">
    <saf-form>
      <saf-form-field label="First Name">
        <saf-text-input name="firstName"></saf-text-input>
      </saf-form-field>
      <saf-form-field label="Last Name">
        <saf-text-input name="lastName"></saf-text-input>
      </saf-form-field>
    </saf-form>
  </saf-wizard-step-content>

  <saf-wizard-step-content step="2">
    <saf-form>
      <saf-form-field label="Email">
        <saf-text-input type="email" name="email"></saf-text-input>
      </saf-form-field>
      <saf-form-field label="Password">
        <saf-text-input type="password" name="password"></saf-text-input>
      </saf-form-field>
    </saf-form>
  </saf-wizard-step-content>

  <saf-wizard-step-content step="3">
    <div class="confirmation-content">
      <h3>Review Your Information</h3>
      <p>Please review the information below and confirm to create your account.</p>
      <!-- Summary content -->
    </div>
  </saf-wizard-step-content>

  <!-- Navigation -->
  <div slot="footer">
    <saf-button appearance="tertiary" id="cancel-btn">Cancel</saf-button>
    <saf-button appearance="secondary" id="back-btn" disabled>Back</saf-button>
    <saf-button appearance="primary" id="next-btn">Next</saf-button>
  </div>
</saf-wizard>
```

### React Implementation

```tsx
import React, { useState } from 'react';

interface WizardStep {
  number: number;
  title: string;
  description: string;
  status: 'active' | 'completed' | 'inactive';
  content: React.ReactNode;
}

function SetupWizard() {
  const [currentStep, setCurrentStep] = useState(1);
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: '',
    password: '',
    preferences: {
      newsletter: false,
      notifications: true,
    },
  });

  const steps: WizardStep[] = [
    {
      number: 1,
      title: 'Personal Information',
      description: 'Tell us about yourself',
      status: currentStep === 1 ? 'active' : currentStep > 1 ? 'completed' : 'inactive',
      content: (
        <div className="step-content">
          <saf-form>
            <saf-form-field label="First Name" required>
              <saf-text-input
                value={formData.firstName}
                onInput={(e) => 
                  setFormData(prev => ({ ...prev, firstName: e.target.value }))
                }
              />
            </saf-form-field>
            <saf-form-field label="Last Name" required>
              <saf-text-input
                value={formData.lastName}
                onInput={(e) => 
                  setFormData(prev => ({ ...prev, lastName: e.target.value }))
                }
              />
            </saf-form-field>
          </saf-form>
        </div>
      ),
    },
    {
      number: 2,
      title: 'Account Details',
      description: 'Set up your account credentials',
      status: currentStep === 2 ? 'active' : currentStep > 2 ? 'completed' : 'inactive',
      content: (
        <div className="step-content">
          <saf-form>
            <saf-form-field label="Email Address" required>
              <saf-text-input
                type="email"
                value={formData.email}
                onInput={(e) => 
                  setFormData(prev => ({ ...prev, email: e.target.value }))
                }
              />
            </saf-form-field>
            <saf-form-field label="Password" required>
              <saf-text-input
                type="password"
                value={formData.password}
                onInput={(e) => 
                  setFormData(prev => ({ ...prev, password: e.target.value }))
                }
              />
            </saf-form-field>
          </saf-form>
        </div>
      ),
    },
    {
      number: 3,
      title: 'Preferences',
      description: 'Configure your preferences',
      status: currentStep === 3 ? 'active' : currentStep > 3 ? 'completed' : 'inactive',
      content: (
        <div className="step-content">
          <saf-form>
            <saf-form-field>
              <saf-toggle-switch
                checked={formData.preferences.newsletter}
                onChange={(e) => 
                  setFormData(prev => ({
                    ...prev,
                    preferences: { ...prev.preferences, newsletter: e.target.checked }
                  }))
                }
              >
                Subscribe to newsletter
              </saf-toggle-switch>
            </saf-form-field>
            <saf-form-field>
              <saf-toggle-switch
                checked={formData.preferences.notifications}
                onChange={(e) => 
                  setFormData(prev => ({
                    ...prev,
                    preferences: { ...prev.preferences, notifications: e.target.checked }
                  }))
                }
              >
                Enable notifications
              </saf-toggle-switch>
            </saf-form-field>
          </saf-form>
        </div>
      ),
    },
    {
      number: 4,
      title: 'Confirmation',
      description: 'Review and complete setup',
      status: currentStep === 4 ? 'active' : 'inactive',
      content: (
        <div className="step-content">
          <div className="confirmation-summary">
            <h3>Review Your Information</h3>
            <div className="summary-section">
              <h4>Personal Information</h4>
              <p>Name: {formData.firstName} {formData.lastName}</p>
              <p>Email: {formData.email}</p>
            </div>
            <div className="summary-section">
              <h4>Preferences</h4>
              <p>Newsletter: {formData.preferences.newsletter ? 'Enabled' : 'Disabled'}</p>
              <p>Notifications: {formData.preferences.notifications ? 'Enabled' : 'Disabled'}</p>
            </div>
          </div>
        </div>
      ),
    },
  ];

  const handleStepChange = (event: CustomEvent) => {
    setCurrentStep(event.detail);
  };

  const handleNext = () => {
    if (currentStep < steps.length) {
      setCurrentStep(currentStep + 1);
    }
  };

  const handleBack = () => {
    if (currentStep > 1) {
      setCurrentStep(currentStep - 1);
    }
  };

  const handleComplete = () => {
    console.log('Wizard completed with data:', formData);
    // Handle completion logic
  };

  const isStepValid = (stepNumber: number): boolean => {
    switch (stepNumber) {
      case 1:
        return formData.firstName.trim() !== '' && formData.lastName.trim() !== '';
      case 2:
        return formData.email.trim() !== '' && formData.password.length >= 8;
      case 3:
        return true; // Preferences are optional
      default:
        return true;
    }
  };

  return (
    <saf-wizard
      a11y-aria-label="Account Setup Wizard"
      heading-level={2}
      onStepChange={handleStepChange}
    >
      <saf-stepper slot="stepper" active-step={currentStep} orientation="horizontal">
        {steps.map(step => (
          <saf-step
            key={step.number}
            status={step.status}
            step-title={step.title}
          >
            <div>{step.description}</div>
          </saf-step>
        ))}
      </saf-stepper>

      {steps.map(step => (
        <saf-wizard-step-content key={step.number} step={step.number}>
          {step.content}
        </saf-wizard-step-content>
      ))}

      <div slot="footer" className="wizard-footer">
        <saf-button appearance="tertiary" onClick={() => window.history.back()}>
          Cancel
        </saf-button>
        
        <div className="nav-buttons">
          <saf-button
            appearance="secondary"
            disabled={currentStep === 1}
            onClick={handleBack}
          >
            <saf-icon slot="start" icon-name="chevron-left" />
            Back
          </saf-button>
          
          {currentStep < steps.length ? (
            <saf-button
              appearance="primary"
              disabled={!isStepValid(currentStep)}
              onClick={handleNext}
            >
              Next
              <saf-icon slot="end" icon-name="chevron-right" />
            </saf-button>
          ) : (
            <saf-button
              appearance="primary"
              onClick={handleComplete}
            >
              Complete Setup
              <saf-icon slot="end" icon-name="check" />
            </saf-button>
          )}
        </div>
      </div>
    </saf-wizard>
  );
}
```

### Angular Implementation

```typescript
import { Component } from '@angular/core';

interface StepData {
  number: number;
  title: string;
  description: string;
  isValid: boolean;
}

@Component({
  selector: 'app-onboarding-wizard',
  template: `
    <saf-wizard
      [a11y-aria-label]="'Employee Onboarding Wizard'"
      [heading-level]="2"
      (step-change)="handleStepChange($event)">
      
      <saf-stepper
        slot="stepper"
        [active-step]="currentStep"
        orientation="horizontal">
        
        <saf-step
          *ngFor="let step of steps"
          [status]="getStepStatus(step.number)"
          [step-title]="step.title">
          <div>{{ step.description }}</div>
        </saf-step>
      </saf-stepper>

      <!-- Step 1: Personal Info -->
      <saf-wizard-step-content [step]="1">
        <saf-form>
          <saf-form-field label="Employee ID" required>
            <saf-text-input
              [(ngModel)]="formData.employeeId"
              name="employeeId">
            </saf-text-input>
          </saf-form-field>
          
          <saf-form-field label="Department" required>
            <saf-select
              [(ngModel)]="formData.department"
              name="department">
              <saf-option value="engineering">Engineering</saf-option>
              <saf-option value="design">Design</saf-option>
              <saf-option value="product">Product</saf-option>
              <saf-option value="marketing">Marketing</saf-option>
            </saf-select>
          </saf-form-field>
        </saf-form>
      </saf-wizard-step-content>

      <!-- Step 2: Equipment -->
      <saf-wizard-step-content [step]="2">
        <saf-form>
          <saf-form-field label="Laptop Preference">
            <saf-select
              [(ngModel)]="formData.laptop"
              name="laptop">
              <saf-option value="windows">Windows Laptop</saf-option>
              <saf-option value="mac">MacBook</saf-option>
            </saf-select>
          </saf-form-field>
          
          <saf-form-field>
            <saf-toggle-switch
              [(ngModel)]="formData.needsMonitor"
              name="needsMonitor">
              External Monitor Required
            </saf-toggle-switch>
          </saf-form-field>
        </saf-form>
      </saf-wizard-step-content>

      <!-- Step 3: Access -->
      <saf-wizard-step-content [step]="3">
        <div class="access-content">
          <h3>System Access Requirements</h3>
          <saf-form>
            <saf-form-field>
              <saf-toggle-switch
                [(ngModel)]="formData.access.email"
                name="email">
                Email Access
              </saf-toggle-switch>
            </saf-form-field>
            
            <saf-form-field>
              <saf-toggle-switch
                [(ngModel)]="formData.access.vpn"
                name="vpn">
                VPN Access
              </saf-toggle-switch>
            </saf-form-field>
            
            <saf-form-field>
              <saf-toggle-switch
                [(ngModel)]="formData.access.adminRights"
                name="adminRights">
                Administrator Rights
              </saf-toggle-switch>
            </saf-form-field>
          </saf-form>
        </div>
      </saf-wizard-step-content>

      <!-- Step 4: Summary -->
      <saf-wizard-step-content [step]="4">
        <div class="summary-content">
          <h3>Onboarding Summary</h3>
          <div class="summary-grid">
            <div class="summary-section">
              <h4>Employee Details</h4>
              <p>ID: {{ formData.employeeId }}</p>
              <p>Department: {{ formData.department }}</p>
            </div>
            
            <div class="summary-section">
              <h4>Equipment</h4>
              <p>Laptop: {{ formData.laptop }}</p>
              <p>Monitor: {{ formData.needsMonitor ? 'Required' : 'Not needed' }}</p>
            </div>
            
            <div class="summary-section">
              <h4>Access Rights</h4>
              <ul>
                <li *ngIf="formData.access.email">Email Access</li>
                <li *ngIf="formData.access.vpn">VPN Access</li>
                <li *ngIf="formData.access.adminRights">Administrator Rights</li>
              </ul>
            </div>
          </div>
        </div>
      </saf-wizard-step-content>

      <!-- Footer Navigation -->
      <div slot="footer" class="wizard-footer">
        <saf-button appearance="tertiary" (click)="handleCancel()">
          Cancel
        </saf-button>
        
        <div class="nav-buttons">
          <saf-button
            appearance="secondary"
            [disabled]="currentStep === 1"
            (click)="handleBack()">
            <saf-icon slot="start" icon-name="chevron-left"></saf-icon>
            Back
          </saf-button>
          
          <saf-button
            *ngIf="currentStep < steps.length"
            appearance="primary"
            [disabled]="!isCurrentStepValid()"
            (click)="handleNext()">
            Next
            <saf-icon slot="end" icon-name="chevron-right"></saf-icon>
          </saf-button>
          
          <saf-button
            *ngIf="currentStep === steps.length"
            appearance="primary"
            (click)="handleComplete()">
            Complete Onboarding
            <saf-icon slot="end" icon-name="check"></saf-icon>
          </saf-button>
        </div>
      </div>
    </saf-wizard>
  `,
  styles: [`
    .wizard-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: var(--spacing-3);
      padding-top: var(--spacing-4);
      border-top: 1px solid var(--color-neutral-stroke-2);
    }
    
    .nav-buttons {
      display: flex;
      gap: var(--spacing-2);
    }
    
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: var(--spacing-4);
    }
    
    .summary-section h4 {
      margin-bottom: var(--spacing-2);
      color: var(--color-neutral-foreground-1);
    }
  `]
})
export class OnboardingWizardComponent {
  currentStep = 1;
  
  steps: StepData[] = [
    { number: 1, title: 'Personal Info', description: 'Employee details', isValid: false },
    { number: 2, title: 'Equipment', description: 'Hardware requirements', isValid: true },
    { number: 3, title: 'Access', description: 'System permissions', isValid: true },
    { number: 4, title: 'Summary', description: 'Review information', isValid: true },
  ];

  formData = {
    employeeId: '',
    department: '',
    laptop: 'windows',
    needsMonitor: false,
    access: {
      email: true,
      vpn: false,
      adminRights: false,
    },
  };

  getStepStatus(stepNumber: number): 'active' | 'completed' | 'inactive' {
    if (stepNumber === this.currentStep) return 'active';
    if (stepNumber < this.currentStep) return 'completed';
    return 'inactive';
  }

  isCurrentStepValid(): boolean {
    switch (this.currentStep) {
      case 1:
        return this.formData.employeeId.trim() !== '' && this.formData.department !== '';
      case 2:
      case 3:
      case 4:
        return true;
      default:
        return false;
    }
  }

  handleStepChange(event: CustomEvent) {
    this.currentStep = event.detail;
  }

  handleNext() {
    if (this.currentStep < this.steps.length && this.isCurrentStepValid()) {
      this.currentStep++;
    }
  }

  handleBack() {
    if (this.currentStep > 1) {
      this.currentStep--;
    }
  }

  handleCancel() {
    // Handle cancellation
    console.log('Wizard cancelled');
  }

  handleComplete() {
    console.log('Onboarding completed:', this.formData);
    // Submit the form data
  }
}
```

### Vertical Layout

```html
<saf-wizard
  a11y-aria-label="Configuration Wizard"
  heading-level="2"
  mode="desktop">
  
  <saf-stepper slot="stepper" active-step="1" orientation="vertical">
    <saf-step status="active" step-title="Basic Settings">
      <div>Configure basic application settings</div>
    </saf-step>
    <saf-step status="inactive" step-title="Advanced Options">
      <div>Set up advanced features</div>
    </saf-step>
    <saf-step status="inactive" step-title="Integration">
      <div>Connect external services</div>
    </saf-step>
  </saf-stepper>

  <saf-wizard-step-content step="1">
    <div class="settings-content">
      <!-- Configuration form -->
    </div>
  </saf-wizard-step-content>

  <saf-wizard-step-content step="2">
    <div class="advanced-content">
      <!-- Advanced options -->
    </div>
  </saf-wizard-step-content>

  <saf-wizard-step-content step="3">
    <div class="integration-content">
      <!-- Integration settings -->
    </div>
  </saf-wizard-step-content>

  <div slot="footer">
    <saf-button appearance="tertiary">Cancel</saf-button>
    <saf-button appearance="secondary">Back</saf-button>
    <saf-button appearance="primary">Next</saf-button>
  </div>
</saf-wizard>
```

## Responsive Behavior

SafWizard automatically adapts its layout based on screen size using the ResponsiveElement mixin:

### Desktop Layout (>768px)
- **Horizontal Stepper**: Steps displayed horizontally at the top
- **Side-by-Side**: Stepper and content displayed simultaneously
- **Step Header**: Dedicated header area for current step title
- **Full Navigation**: All navigation controls visible

### Mobile Layout (≤768px)
- **Vertical Layout**: Optimized for touch interaction
- **Compact Header**: Combined step title and description
- **Hidden Stepper**: Stepper can be hidden to save space
- **Touch-Friendly**: Larger touch targets and spacing

### Breakpoint Configuration

```typescript
// The wizard uses a default breakpoint of 768px
// This can be customized when initializing the responsive behavior

class CustomWizard extends Wizard {
  connectedCallback(): void {
    super.connectedCallback();
    // Custom breakpoint
    this.initializeResponsiveness({ breakpoint: 1024 });
  }
}
```

## Accessibility

SafWizard provides comprehensive accessibility support:

### ARIA Implementation

- **Complementary Region**: The wizard uses `role="complementary"` with descriptive label
- **Step Navigation**: Integrated with SafStepper's ARIA implementation
- **Heading Hierarchy**: Configurable heading levels for proper document structure
- **Focus Management**: Automatic focus handling during step transitions

### Keyboard Navigation

| Key | Action |
|-----|--------|
| **Tab** | Navigate through interactive elements |
| **Arrow Keys** | Navigate between steps (when stepper is focused) |
| **Enter/Space** | Activate focused step or button |
| **Home/End** | Jump to first/last step (when stepper is focused) |

### Screen Reader Support

- **Step Progress**: Current step and total steps announced
- **Content Changes**: Step content changes are announced
- **Button Context**: Navigation buttons have descriptive labels
- **Heading Focus**: Step titles receive focus for context

### Required Accessibility Attributes

```html
<saf-wizard a11y-aria-label="Multi-step Process Wizard" heading-level="2">
  <!-- Stepper with proper step labels -->
  <saf-stepper slot="stepper" active-step="1">
    <saf-step status="active" step-title="Personal Information">
      <div>Enter your personal details</div>
    </saf-step>
    <!-- More steps -->
  </saf-stepper>
  
  <!-- Content with clear structure -->
  <saf-wizard-step-content step="1">
    <div class="step-intro">
      <p>Please provide your personal information to continue.</p>
    </div>
    <!-- Form content -->
  </saf-wizard-step-content>
</saf-wizard>
```

## Styling

### CSS Custom Properties

```css
saf-wizard {
  /* Container spacing */
  --wizard-container-gap: var(--spacing-6);
  --wizard-content-padding: var(--spacing-4);
  
  /* Step header styling */
  --step-header-margin: var(--spacing-4) 0;
  --step-header-border: 1px solid var(--color-neutral-stroke-2);
  
  /* Mobile header styling */
  --mobile-header-padding: var(--spacing-3);
  --mobile-header-bg: var(--color-neutral-layer-2);
  
  /* Content area styling */
  --step-content-min-height: 300px;
  --step-content-background: var(--color-neutral-layer-1);
}
```

### Component Parts Styling

```css
/* Style the main wizard container */
saf-wizard::part(wizard-container) {
  display: grid;
  gap: var(--wizard-container-gap);
  min-height: 500px;
}

/* Horizontal layout (desktop) */
saf-wizard::part(wizard-container).horizontal.desktop {
  grid-template-columns: auto 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "stepper stepper"
    "content content"
    "footer footer";
}

/* Vertical layout */
saf-wizard::part(wizard-container).vertical {
  grid-template-columns: 250px 1fr;
  grid-template-areas:
    "stepper content"
    "stepper footer";
}

/* Mobile layout */
saf-wizard::part(wizard-container).mobile {
  grid-template-columns: 1fr;
  grid-template-areas:
    "header"
    "content"
    "footer";
}

/* Step header styling */
saf-wizard::part(step-header) {
  padding-bottom: var(--spacing-3);
  border-bottom: 1px solid var(--color-neutral-stroke-2);
  margin-bottom: var(--spacing-4);
}

/* Mobile header styling */
saf-wizard::part(step-header-mobile) {
  background: var(--color-neutral-layer-2);
  padding: var(--spacing-3);
  border-radius: var(--border-radius-2);
}

/* Content container */
saf-wizard::part(wizard-content-container) {
  grid-area: content;
  display: flex;
  flex-direction: column;
  min-height: var(--step-content-min-height);
}

/* Step content area */
saf-wizard::part(step-content) {
  flex: 1;
  padding: var(--spacing-4);
  background: var(--step-content-background);
  border-radius: var(--border-radius-2);
}
```

### Step Content Styling

```css
/* Hide inactive step content */
saf-wizard-step-content[hidden] {
  display: none !important;
}

/* Visible step content */
saf-wizard-step-content:not([hidden]) {
  display: block;
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

## Integration

### With Form Validation

```typescript
class ValidatedWizard extends Wizard {
  private validationRules = new Map<number, () => boolean>();
  
  addStepValidation(stepNumber: number, validator: () => boolean) {
    this.validationRules.set(stepNumber, validator);
  }
  
  isStepValid(stepNumber: number): boolean {
    const validator = this.validationRules.get(stepNumber);
    return validator ? validator() : true;
  }
  
  canProceedToNextStep(): boolean {
    return this.isStepValid(this.stepper?.activeStep || 1);
  }
}
```

### With State Management

```typescript
// Redux/NgRx integration example
interface WizardState {
  currentStep: number;
  completedSteps: number[];
  formData: Record<string, any>;
  isLoading: boolean;
}

const wizardSlice = createSlice({
  name: 'wizard',
  initialState: {
    currentStep: 1,
    completedSteps: [],
    formData: {},
    isLoading: false,
  } as WizardState,
  reducers: {
    setCurrentStep: (state, action) => {
      state.currentStep = action.payload;
    },
    completeStep: (state, action) => {
      if (!state.completedSteps.includes(action.payload)) {
        state.completedSteps.push(action.payload);
      }
    },
    updateFormData: (state, action) => {
      state.formData = { ...state.formData, ...action.payload };
    },
  },
});
```

### With Data Loading

```html
<saf-wizard a11y-aria-label="Data-Driven Wizard">
  <saf-stepper slot="stepper" active-step="${currentStep}">
    <!-- Dynamic steps from API -->
  </saf-stepper>
  
  <saf-wizard-step-content step="1">
    ${when(
      x => x.isLoading,
      html`<saf-progress-ring></saf-progress-ring>`,
      html`<div class="loaded-content">${stepContent}</div>`
    )}
  </saf-wizard-step-content>
</saf-wizard>
```

## Best Practices

### Content Design
- **Clear Step Titles**: Use descriptive, action-oriented step titles
- **Logical Flow**: Organize steps in a logical sequence
- **Progress Indication**: Show clear progress through the wizard
- **Content Length**: Keep individual steps manageable in length

### User Experience
- **Validation Feedback**: Provide immediate validation feedback
- **Save Progress**: Consider saving progress for long wizards
- **Exit Confirmation**: Warn users before losing progress
- **Skip Options**: Allow skipping of optional steps when appropriate

### Accessibility
- **Heading Hierarchy**: Use proper heading levels for content structure
- **Focus Management**: Ensure focus moves logically through the wizard
- **Screen Reader Testing**: Test with actual assistive technologies
- **Keyboard Navigation**: Ensure all functionality is keyboard accessible

### Performance
- **Lazy Loading**: Load step content only when needed
- **Progressive Enhancement**: Start with basic functionality, enhance with JavaScript
- **Memory Management**: Clean up resources when steps are no longer needed
- **Responsive Images**: Use appropriate image sizes for different screen sizes

### Error Handling
- **Validation States**: Show clear validation states for form fields
- **Error Messages**: Provide specific, actionable error messages
- **Recovery Options**: Offer ways to recover from errors
- **Graceful Degradation**: Handle network failures gracefully

SafWizard provides a comprehensive solution for complex multi-step workflows while maintaining accessibility and responsive design principles throughout the user experience.
