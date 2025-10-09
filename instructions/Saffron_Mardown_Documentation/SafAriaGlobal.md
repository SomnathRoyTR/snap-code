# SafAriaGlobal

A mixin class that provides comprehensive ARIA (Accessible Rich Internet Applications) global states and properties to enhance accessibility for web components. SafAriaGlobal implements all global ARIA attributes as defined in the ARIA 1.1 specification, enabling any component to support the full range of accessibility features.

## Overview

SafAriaGlobal is not a standalone component but a mixin class designed to be extended by other Saffron components. It provides a standardized way to implement ARIA attributes across the design system, ensuring consistent accessibility patterns.

## React

### API

When a component extends SafAriaGlobal, it gains access to all the following ARIA properties:

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `ariaAtomic` | `'true' \| 'false' \| string \| null` | `null` | Indicates whether assistive technologies present all or parts of changed region |
| `ariaBusy` | `'true' \| 'false' \| string \| null` | `null` | Indicates an element is being modified and assistive technologies should wait |
| `ariaControls` | `string \| null` | `null` | Identifies elements whose contents or presence are controlled by current element |
| `ariaCurrent` | `'page' \| 'step' \| 'location' \| 'date' \| 'time' \| 'true' \| 'false' \| string \| null` | `null` | Indicates the current item within a container or set |
| `ariaDescribedby` | `string \| null` | `null` | Identifies elements that describe the object |
| `ariaDetails` | `string \| null` | `null` | Identifies element providing detailed, extended description |
| `ariaDisabled` | `'true' \| 'false' \| string \| null` | `null` | Indicates the element is perceivable but disabled |
| `ariaErrormessage` | `string \| null` | `null` | Identifies element providing error message for the object |
| `ariaFlowto` | `string \| null` | `null` | Identifies next elements in alternate reading order |
| `ariaHaspopup` | `'false' \| 'true' \| 'menu' \| 'listbox' \| 'tree' \| 'grid' \| 'dialog' \| string \| null` | `null` | Indicates availability and type of interactive popup element |
| `ariaHidden` | `'false' \| 'true' \| string \| null` | `null` | Indicates whether element is exposed to screen reader |
| `ariaInvalid` | `'false' \| 'true' \| 'grammar' \| 'spelling' \| string \| null` | `null` | Indicates entered value doesn't conform to expected format |
| `ariaKeyshortcuts` | `string \| null` | `null` | Indicates keyboard shortcuts to activate or focus element |
| `ariaLabel` | `string \| null` | `null` | Defines string value that labels the current element |
| `ariaLabelledby` | `string \| null` | `null` | Identifies elements that label the current element |
| `ariaLive` | `'assertive' \| 'off' \| 'polite' \| string \| null` | `null` | Indicates element will be updated and describes update types |
| `ariaOwns` | `string \| null` | `null` | Defines visual, functional, or contextual parent/child relationship |
| `ariaRelevant` | `'additions' \| 'additions text' \| 'all' \| 'removals' \| 'text' \| string \| null` | `null` | Indicates notifications when accessibility tree is modified |
| `ariaRoledescription` | `string \| null` | `null` | Defines human-readable description for the role of element |

### Examples

#### Basic Usage with Live Region
```jsx
import { SafButton, SafAlert } from '@saffron/core-components/react';

function LiveRegionExample() {
  const [message, setMessage] = useState('');
  const [messageType, setMessageType] = useState('polite');

  const announceMessage = (msg, type = 'polite') => {
    setMessageType(type);
    setMessage(msg);
    // Clear message after announcement
    setTimeout(() => setMessage(''), 100);
  };

  return (
    <div>
      <SafButton onClick={() => announceMessage('Data saved successfully!')}>
        Save Data
      </SafButton>
      
      <SafButton 
        onClick={() => announceMessage('Critical error occurred!', 'assertive')}
        appearance="danger">
        Trigger Error
      </SafButton>
      
      {/* Live region for announcements */}
      <div
        ariaLive={messageType}
        ariaAtomic="true"
        className="sr-only">
        {message}
      </div>
    </div>
  );
}
```

#### Form Validation with Error Messages
```jsx
import { SafTextField, SafButton } from '@saffron/core-components/react';

function FormValidationExample() {
  const [email, setEmail] = useState('');
  const [emailError, setEmailError] = useState('');
  const errorId = useId();

  const validateEmail = (value) => {
    if (!value) {
      setEmailError('Email is required');
      return false;
    }
    if (!/\S+@\S+\.\S+/.test(value)) {
      setEmailError('Please enter a valid email address');
      return false;
    }
    setEmailError('');
    return true;
  };

  return (
    <form>
      <SafTextField
        label="Email Address"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        onBlur={() => validateEmail(email)}
        ariaInvalid={emailError ? 'true' : 'false'}
        ariaErrormessage={emailError ? errorId : null}
        ariaDescribedby={emailError ? errorId : null}
      />
      
      {emailError && (
        <div id={errorId} role="alert" ariaLive="polite">
          {emailError}
        </div>
      )}
      
      <SafButton 
        type="submit"
        disabled={!email || !!emailError}
        ariaDisabled={!email || !!emailError ? 'true' : 'false'}>
        Submit
      </SafButton>
    </form>
  );
}
```

#### Complex Interactive Component
```jsx
import { SafButton, SafDialog } from '@saffron/core-components/react';

function ComplexComponentExample() {
  const [isDialogOpen, setIsDialogOpen] = useState(false);
  const [currentStep, setCurrentStep] = useState(1);
  const totalSteps = 3;
  const dialogId = useId();

  return (
    <div>
      <SafButton
        onClick={() => setIsDialogOpen(true)}
        ariaHaspopup="dialog"
        ariaControls={dialogId}>
        Open Wizard
      </SafButton>
      
      {isDialogOpen && (
        <SafDialog
          id={dialogId}
          onClose={() => setIsDialogOpen(false)}
          ariaLabel="Multi-step Wizard">
          
          <div ariaCurrent="step" ariaLabel={`Step ${currentStep} of ${totalSteps}`}>
            <h2>Step {currentStep}</h2>
            <p>Complete this step to continue.</p>
          </div>
          
          <div>
            {currentStep > 1 && (
              <SafButton 
                onClick={() => setCurrentStep(currentStep - 1)}
                ariaKeyshortcuts="Alt+Left">
                Previous
              </SafButton>
            )}
            
            {currentStep < totalSteps ? (
              <SafButton 
                onClick={() => setCurrentStep(currentStep + 1)}
                ariaKeyshortcuts="Alt+Right">
                Next
              </SafButton>
            ) : (
              <SafButton 
                onClick={() => setIsDialogOpen(false)}
                appearance="primary">
                Complete
              </SafButton>
            )}
          </div>
        </SafDialog>
      )}
    </div>
  );
}
```

## Angular

### API

When a component extends SafAriaGlobal, it gains access to all the following ARIA inputs:

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `ariaAtomic` | `'true' \| 'false' \| string \| null` | `null` | Indicates whether assistive technologies present all or parts of changed region |
| `ariaBusy` | `'true' \| 'false' \| string \| null` | `null` | Indicates an element is being modified and assistive technologies should wait |
| `ariaControls` | `string \| null` | `null` | Identifies elements whose contents or presence are controlled by current element |
| `ariaCurrent` | `'page' \| 'step' \| 'location' \| 'date' \| 'time' \| 'true' \| 'false' \| string \| null` | `null` | Indicates the current item within a container or set |
| `ariaDescribedby` | `string \| null` | `null` | Identifies elements that describe the object |
| `ariaDetails` | `string \| null` | `null` | Identifies element providing detailed, extended description |
| `ariaDisabled` | `'true' \| 'false' \| string \| null` | `null` | Indicates the element is perceivable but disabled |
| `ariaErrormessage` | `string \| null` | `null` | Identifies element providing error message for the object |
| `ariaFlowto` | `string \| null` | `null` | Identifies next elements in alternate reading order |
| `ariaHaspopup` | `'false' \| 'true' \| 'menu' \| 'listbox' \| 'tree' \| 'grid' \| 'dialog' \| string \| null` | `null` | Indicates availability and type of interactive popup element |
| `ariaHidden` | `'false' \| 'true' \| string \| null` | `null` | Indicates whether element is exposed to screen reader |
| `ariaInvalid` | `'false' \| 'true' \| 'grammar' \| 'spelling' \| string \| null` | `null` | Indicates entered value doesn't conform to expected format |
| `ariaKeyshortcuts` | `string \| null` | `null` | Indicates keyboard shortcuts to activate or focus element |
| `ariaLabel` | `string \| null` | `null` | Defines string value that labels the current element |
| `ariaLabelledby` | `string \| null` | `null` | Identifies elements that label the current element |
| `ariaLive` | `'assertive' \| 'off' \| 'polite' \| string \| null` | `null` | Indicates element will be updated and describes update types |
| `ariaOwns` | `string \| null` | `null` | Defines visual, functional, or contextual parent/child relationship |
| `ariaRelevant` | `'additions' \| 'additions text' \| 'all' \| 'removals' \| 'text' \| string \| null` | `null` | Indicates notifications when accessibility tree is modified |
| `ariaRoledescription` | `string \| null` | `null` | Defines human-readable description for the role of element |

### Examples

#### Basic Usage with Live Region
```html
<div>
  <saf-button (click)="announceMessage('Data saved successfully!')">
    Save Data
  </saf-button>
  
  <saf-button 
    (click)="announceMessage('Critical error occurred!', 'assertive')"
    appearance="danger">
    Trigger Error
  </saf-button>
  
  <!-- Live region for announcements -->
  <div
    [ariaLive]="messageType"
    ariaAtomic="true"
    class="sr-only">
    {{ message }}
  </div>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-live-region-example',
  templateUrl: './live-region-example.component.html'
})
export class LiveRegionExampleComponent {
  message = '';
  messageType: 'polite' | 'assertive' = 'polite';

  announceMessage(msg: string, type: 'polite' | 'assertive' = 'polite') {
    this.messageType = type;
    this.message = msg;
    // Clear message after announcement
    setTimeout(() => this.message = '', 100);
  }
}
```

#### Form Validation with Error Messages
```html
<form>
  <saf-text-field
    label="Email Address"
    [(ngModel)]="email"
    (blur)="validateEmail()"
    [ariaInvalid]="emailError ? 'true' : 'false'"
    [ariaErrormessage]="emailError ? errorId : null"
    [ariaDescribedby]="emailError ? errorId : null">
  </saf-text-field>
  
  <div 
    *ngIf="emailError" 
    [id]="errorId" 
    role="alert" 
    ariaLive="polite">
    {{ emailError }}
  </div>
  
  <saf-button 
    type="submit"
    [disabled]="!email || !!emailError"
    [ariaDisabled]="(!email || !!emailError) ? 'true' : 'false'">
    Submit
  </saf-button>
</form>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-form-validation-example',
  templateUrl: './form-validation-example.component.html'
})
export class FormValidationExampleComponent {
  email = '';
  emailError = '';
  errorId = 'email-error-' + Math.random().toString(36).substr(2, 9);

  validateEmail() {
    if (!this.email) {
      this.emailError = 'Email is required';
      return false;
    }
    if (!/\S+@\S+\.\S+/.test(this.email)) {
      this.emailError = 'Please enter a valid email address';
      return false;
    }
    this.emailError = '';
    return true;
  }
}
```

#### Complex Interactive Component
```html
<div>
  <saf-button
    (click)="openDialog()"
    ariaHaspopup="dialog"
    [ariaControls]="dialogId">
    Open Wizard
  </saf-button>
  
  <saf-dialog
    *ngIf="isDialogOpen"
    [id]="dialogId"
    (close)="closeDialog()"
    ariaLabel="Multi-step Wizard">
    
    <div 
      ariaCurrent="step" 
      [ariaLabel]="'Step ' + currentStep + ' of ' + totalSteps">
      <h2>Step {{ currentStep }}</h2>
      <p>Complete this step to continue.</p>
    </div>
    
    <div>
      <saf-button 
        *ngIf="currentStep > 1"
        (click)="previousStep()"
        ariaKeyshortcuts="Alt+Left">
        Previous
      </saf-button>
      
      <saf-button 
        *ngIf="currentStep < totalSteps; else completeBtn"
        (click)="nextStep()"
        ariaKeyshortcuts="Alt+Right">
        Next
      </saf-button>
      
      <ng-template #completeBtn>
        <saf-button 
          (click)="closeDialog()"
          appearance="primary">
          Complete
        </saf-button>
      </ng-template>
    </div>
  </saf-dialog>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-complex-component-example',
  templateUrl: './complex-component-example.component.html'
})
export class ComplexComponentExampleComponent {
  isDialogOpen = false;
  currentStep = 1;
  totalSteps = 3;
  dialogId = 'wizard-dialog-' + Math.random().toString(36).substr(2, 9);

  openDialog() {
    this.isDialogOpen = true;
  }

  closeDialog() {
    this.isDialogOpen = false;
    this.currentStep = 1;
  }

  nextStep() {
    if (this.currentStep < this.totalSteps) {
      this.currentStep++;
    }
  }

  previousStep() {
    if (this.currentStep > 1) {
      this.currentStep--;
    }
  }
}
```

## Best Practices

- **Use semantic ARIA labels**: Provide clear, descriptive `ariaLabel` values that give context about the element's purpose.
- **Reference related elements**: Use `ariaDescribedby` and `ariaLabelledby` to create relationships between elements.
- **Implement live regions carefully**: Use `ariaLive="polite"` for non-critical updates and `ariaLive="assertive"` for urgent announcements.
- **Validate with screen readers**: Test your ARIA implementation with actual assistive technologies.
- **Keep descriptions concise**: ARIA descriptions should be brief but informative.
- **Use appropriate controls**: Set `ariaControls` when elements manipulate other parts of the interface.
- **Handle invalid states**: Combine `ariaInvalid` with `ariaErrormessage` for form validation feedback.
- **Consider keyboard navigation**: Use `ariaKeyshortcuts` to document available keyboard shortcuts.

## Notes

- SafAriaGlobal is designed as a mixin and should not be used as a standalone component.
- All ARIA properties follow the ARIA 1.1 specification for maximum compatibility.
- The mixin automatically handles HTML attribute mapping for all ARIA properties.
- Components that extend SafAriaGlobal inherit all these accessibility features automatically.
- Always test ARIA implementations with screen readers and keyboard-only navigation.
- Consider using ARIA properties as progressive enhancement rather than core functionality.
- Some ARIA properties may override browser default behaviors, so use them thoughtfully.
