# SafLabel

A collection of template utilities and SCSS mixins for creating accessible, consistent labels across form components in the Saffron Design System. SafLabel provides standardized patterns for form field labeling, instructional text, and optional/required indicators.

## Overview

SafLabel is not a standalone component but a set of template utilities and styles that other form components use to ensure consistent labeling patterns. It includes templates for main labels, instructional text, and optional/required indicators, all with proper accessibility attributes.

## Template Components

### labelTemplate
The main label template that creates properly associated labels for form fields.

### instructionalTextTemplate  
Template for providing additional guidance or instructions below form fields.

### optionalTextTemplate
Template for indicating whether a field is optional or providing additional label context.

## React

### Usage in Form Components

SafLabel templates are used internally by form components, but understanding their structure helps with styling and customization:

```jsx
import { SafTextField, SafTextArea, SafSelect } from '@saffron/core-components/react';

function FormWithLabels() {
  return (
    <form>
      {/* Basic label */}
      <SafTextField
        id="username"
        label="Username"
        required
        requiredText="*"
      />
      
      {/* Label with instructional text */}
      <SafTextField
        id="email"
        label="Email Address"
        instructionalText="We'll use this to send you important updates"
        required
      />
      
      {/* Label with optional text */}
      <SafTextField
        id="phone"
        label="Phone Number"
        optionalText="(optional)"
      />
      
      {/* Complex label example */}
      <SafTextArea
        id="description"
        label="Project Description"
        instructionalText="Provide a detailed description of your project goals and requirements"
        optionalText="(minimum 50 characters)"
        required
        requiredText="Required"
      />
    </form>
  );
}
```

### Examples

#### Comprehensive Form with Various Label Types
```jsx
import { SafTextField, SafTextArea, SafSelect, SafCheckbox } from '@saffron/core-components/react';

function ComprehensiveForm() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    company: '',
    role: '',
    projectDescription: '',
    budget: '',
    newsletter: false
  });

  const handleInputChange = (field, value) => {
    setFormData(prev => ({ ...prev, [field]: value }));
  };

  return (
    <form className="comprehensive-form">
      {/* Required fields with asterisk */}
      <div className="form-row">
        <SafTextField
          id="firstName"
          label="First Name"
          value={formData.firstName}
          onChange={(e) => handleInputChange('firstName', e.target.value)}
          required
          requiredText="*"
        />
        
        <SafTextField
          id="lastName"
          label="Last Name"
          value={formData.lastName}
          onChange={(e) => handleInputChange('lastName', e.target.value)}
          required
          requiredText="*"
        />
      </div>
      
      {/* Field with instructional text */}
      <SafTextField
        id="email"
        label="Email Address"
        type="email"
        value={formData.email}
        onChange={(e) => handleInputChange('email', e.target.value)}
        instructionalText="We'll use this email for important project communications"
        required
        requiredText="*"
      />
      
      {/* Optional field with clear indication */}
      <SafTextField
        id="phone"
        label="Phone Number"
        type="tel"
        value={formData.phone}
        onChange={(e) => handleInputChange('phone', e.target.value)}
        optionalText="(optional)"
        instructionalText="Include country code for international numbers"
      />
      
      {/* Select with descriptive label */}
      <SafSelect
        id="role"
        label="Your Role"
        value={formData.role}
        onChange={(e) => handleInputChange('role', e.target.value)}
        instructionalText="Select the option that best describes your current position"
        required
        requiredText="Required">
        <option value="">Choose your role</option>
        <option value="developer">Software Developer</option>
        <option value="designer">UX/UI Designer</option>
        <option value="manager">Project Manager</option>
        <option value="executive">Executive</option>
        <option value="other">Other</option>
      </SafSelect>
      
      {/* Textarea with detailed guidance */}
      <SafTextArea
        id="projectDescription"
        label="Project Description"
        value={formData.projectDescription}
        onChange={(e) => handleInputChange('projectDescription', e.target.value)}
        instructionalText="Describe your project goals, timeline, and any specific requirements. The more detail you provide, the better we can assist you."
        optionalText="(minimum 100 characters recommended)"
        rows={4}
      />
      
      {/* Field with custom required text */}
      <SafSelect
        id="budget"
        label="Project Budget Range"
        value={formData.budget}
        onChange={(e) => handleInputChange('budget', e.target.value)}
        required
        requiredText="Required for quote calculation">
        <option value="">Select budget range</option>
        <option value="under-10k">Under $10,000</option>
        <option value="10k-25k">$10,000 - $25,000</option>
        <option value="25k-50k">$25,000 - $50,000</option>
        <option value="50k-plus">$50,000+</option>
      </SafSelect>
      
      {/* Checkbox with clear labeling */}
      <SafCheckbox
        id="newsletter"
        checked={formData.newsletter}
        onChange={(e) => handleInputChange('newsletter', e.target.checked)}>
        Subscribe to our newsletter for project updates and industry insights
      </SafCheckbox>
    </form>
  );
}
```

#### Conditional Label Display
```jsx
import { SafTextField, SafButton } from '@saffron/core-components/react';

function ConditionalLabelForm() {
  const [showOptionalFields, setShowOptionalFields] = useState(false);
  const [fieldMode, setFieldMode] = useState('basic'); // 'basic', 'detailed', 'expert'

  const getLabelConfig = (field, mode) => {
    const configs = {
      username: {
        basic: { label: 'Username', requiredText: '*' },
        detailed: { 
          label: 'Username', 
          instructionalText: 'Choose a unique username for your account',
          requiredText: '*' 
        },
        expert: { 
          label: 'Username', 
          instructionalText: 'Username must be 3-20 characters, alphanumeric and underscores only',
          requiredText: 'Required' 
        }
      },
      email: {
        basic: { label: 'Email', requiredText: '*' },
        detailed: { 
          label: 'Email Address', 
          instructionalText: 'We\'ll send a verification email to this address',
          requiredText: '*' 
        },
        expert: { 
          label: 'Email Address', 
          instructionalText: 'Must be a valid email format. Used for authentication and notifications.',
          requiredText: 'Required for account creation' 
        }
      }
    };
    
    return configs[field]?.[mode] || configs[field]?.basic || {};
  };

  return (
    <div>
      <div style={{ marginBottom: '20px' }}>
        <label>Form Mode: </label>
        <select value={fieldMode} onChange={(e) => setFieldMode(e.target.value)}>
          <option value="basic">Basic</option>
          <option value="detailed">Detailed</option>
          <option value="expert">Expert</option>
        </select>
      </div>
      
      <form>
        <SafTextField
          id="username"
          {...getLabelConfig('username', fieldMode)}
          required
        />
        
        <SafTextField
          id="email"
          type="email"
          {...getLabelConfig('email', fieldMode)}
          required
        />
        
        <SafTextField
          id="fullName"
          label="Full Name"
          optionalText={showOptionalFields ? "(optional)" : undefined}
          instructionalText={fieldMode === 'expert' ? "Enter your full legal name as it appears on official documents" : undefined}
        />
        
        <div style={{ marginTop: '16px' }}>
          <SafButton 
            type="button"
            appearance="tertiary"
            onClick={() => setShowOptionalFields(!showOptionalFields)}>
            {showOptionalFields ? 'Hide' : 'Show'} Optional Fields
          </SafButton>
        </div>
      </form>
    </div>
  );
}
```

#### Internationalized Labels
```jsx
import { SafTextField, SafSelect } from '@saffron/core-components/react';

function InternationalizedForm({ locale = 'en' }) {
  const translations = {
    en: {
      firstName: {
        label: 'First Name',
        instructional: 'Enter your given name',
        required: '*'
      },
      lastName: {
        label: 'Last Name', 
        instructional: 'Enter your family name',
        required: '*'
      },
      email: {
        label: 'Email Address',
        instructional: 'We will use this to contact you',
        required: 'Required'
      },
      country: {
        label: 'Country',
        instructional: 'Select your country of residence',
        optional: '(optional)'
      }
    },
    es: {
      firstName: {
        label: 'Nombre',
        instructional: 'Ingrese su nombre de pila',
        required: '*'
      },
      lastName: {
        label: 'Apellido',
        instructional: 'Ingrese su apellido',
        required: '*'
      },
      email: {
        label: 'Dirección de Email',
        instructional: 'Usaremos esto para contactarte',
        required: 'Requerido'
      },
      country: {
        label: 'País',
        instructional: 'Seleccione su país de residencia',
        optional: '(opcional)'
      }
    }
  };

  const t = translations[locale] || translations.en;

  return (
    <form>
      <SafTextField
        id="firstName"
        label={t.firstName.label}
        instructionalText={t.firstName.instructional}
        required
        requiredText={t.firstName.required}
      />
      
      <SafTextField
        id="lastName"
        label={t.lastName.label}
        instructionalText={t.lastName.instructional}
        required
        requiredText={t.lastName.required}
      />
      
      <SafTextField
        id="email"
        type="email"
        label={t.email.label}
        instructionalText={t.email.instructional}
        required
        requiredText={t.email.required}
      />
      
      <SafSelect
        id="country"
        label={t.country.label}
        instructionalText={t.country.instructional}
        optionalText={t.country.optional}>
        <option value="">Select country...</option>
        <option value="us">United States</option>
        <option value="ca">Canada</option>
        <option value="mx">Mexico</option>
      </SafSelect>
    </form>
  );
}
```

## Angular

### Examples

#### Comprehensive Form with Various Label Types
```html
<form class="comprehensive-form">
  <!-- Required fields with asterisk -->
  <div class="form-row">
    <saf-text-field
      id="firstName"
      label="First Name"
      [(ngModel)]="formData.firstName"
      required
      requiredText="*">
    </saf-text-field>
    
    <saf-text-field
      id="lastName"
      label="Last Name"
      [(ngModel)]="formData.lastName"
      required
      requiredText="*">
    </saf-text-field>
  </div>
  
  <!-- Field with instructional text -->
  <saf-text-field
    id="email"
    label="Email Address"
    type="email"
    [(ngModel)]="formData.email"
    instructionalText="We'll use this email for important project communications"
    required
    requiredText="*">
  </saf-text-field>
  
  <!-- Optional field with clear indication -->
  <saf-text-field
    id="phone"
    label="Phone Number"
    type="tel"
    [(ngModel)]="formData.phone"
    optionalText="(optional)"
    instructionalText="Include country code for international numbers">
  </saf-text-field>
  
  <!-- Select with descriptive label -->
  <saf-select
    id="role"
    label="Your Role"
    [(ngModel)]="formData.role"
    instructionalText="Select the option that best describes your current position"
    required
    requiredText="Required">
    <option value="">Choose your role</option>
    <option value="developer">Software Developer</option>
    <option value="designer">UX/UI Designer</option>
    <option value="manager">Project Manager</option>
    <option value="executive">Executive</option>
    <option value="other">Other</option>
  </saf-select>
  
  <!-- Textarea with detailed guidance -->
  <saf-text-area
    id="projectDescription"
    label="Project Description"
    [(ngModel)]="formData.projectDescription"
    instructionalText="Describe your project goals, timeline, and any specific requirements. The more detail you provide, the better we can assist you."
    optionalText="(minimum 100 characters recommended)"
    [rows]="4">
  </saf-text-area>
</form>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-comprehensive-form',
  templateUrl: './comprehensive-form.component.html',
  styleUrls: ['./comprehensive-form.component.scss']
})
export class ComprehensiveFormComponent {
  formData = {
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    role: '',
    projectDescription: ''
  };
}
```

#### Dynamic Label Configuration
```html
<div>
  <div class="form-mode-selector">
    <label>Form Mode: </label>
    <select [(ngModel)]="fieldMode">
      <option value="basic">Basic</option>
      <option value="detailed">Detailed</option>
      <option value="expert">Expert</option>
    </select>
  </div>
  
  <form>
    <saf-text-field
      id="username"
      [label]="getLabelConfig('username', fieldMode).label"
      [instructionalText]="getLabelConfig('username', fieldMode).instructional"
      [requiredText]="getLabelConfig('username', fieldMode).required"
      required>
    </saf-text-field>
    
    <saf-text-field
      id="email"
      type="email"
      [label]="getLabelConfig('email', fieldMode).label"
      [instructionalText]="getLabelConfig('email', fieldMode).instructional"
      [requiredText]="getLabelConfig('email', fieldMode).required"
      required>
    </saf-text-field>
    
    <saf-text-field
      id="fullName"
      label="Full Name"
      [optionalText]="showOptionalFields ? '(optional)' : undefined"
      [instructionalText]="fieldMode === 'expert' ? 'Enter your full legal name as it appears on official documents' : undefined">
    </saf-text-field>
  </form>
</div>
```

```typescript
import { Component } from '@angular/core';

interface LabelConfig {
  label: string;
  instructional?: string;
  required?: string;
}

@Component({
  selector: 'app-dynamic-label-form',
  templateUrl: './dynamic-label-form.component.html'
})
export class DynamicLabelFormComponent {
  fieldMode: 'basic' | 'detailed' | 'expert' = 'basic';
  showOptionalFields = false;

  private labelConfigs = {
    username: {
      basic: { label: 'Username', required: '*' },
      detailed: { 
        label: 'Username', 
        instructional: 'Choose a unique username for your account',
        required: '*' 
      },
      expert: { 
        label: 'Username', 
        instructional: 'Username must be 3-20 characters, alphanumeric and underscores only',
        required: 'Required' 
      }
    },
    email: {
      basic: { label: 'Email', required: '*' },
      detailed: { 
        label: 'Email Address', 
        instructional: "We'll send a verification email to this address",
        required: '*' 
      },
      expert: { 
        label: 'Email Address', 
        instructional: 'Must be a valid email format. Used for authentication and notifications.',
        required: 'Required for account creation' 
      }
    }
  };

  getLabelConfig(field: string, mode: string): LabelConfig {
    return this.labelConfigs[field]?.[mode] || this.labelConfigs[field]?.basic || { label: field };
  }
}
```

## CSS/SCSS Customization

### Available CSS Parts

The label templates expose several CSS parts for styling:

```scss
// Main label styling
::part(label) {
  font-weight: 600;
  color: var(--label-color);
  margin-bottom: 8px;
}

// Required text indicator
::part(required-text) {
  color: var(--required-color, #d32f2f);
  font-weight: normal;
}

// Optional text indicator  
::part(optional-text) {
  color: var(--optional-color, #666);
  font-weight: normal;
  font-style: italic;
}

// Instructional text
::part(instructional-text) {
  color: var(--instructional-color, #666);
  font-size: 0.875rem;
  margin-top: 4px;
}
```

### Custom Label Styling
```scss
.custom-form {
  // Enhance label visibility
  ::part(label) {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    color: #2c3e50;
    margin-bottom: 6px;
    display: block;
  }

  // Style required indicators
  ::part(required-text) {
    color: #e74c3c;
    margin-left: 4px;
  }

  // Style optional text
  ::part(optional-text) {
    color: #7f8c8d;
    font-size: 0.875rem;
    margin-left: 8px;
  }

  // Style instructional text
  ::part(instructional-text) {
    color: #34495e;
    font-size: 0.8125rem;
    line-height: 1.4;
    margin-top: 4px;
    display: block;
  }
}
```

## Best Practices

- **Consistent labeling**: Use standardized patterns for required/optional indicators across your application.
- **Clear instructions**: Provide helpful instructional text for complex or ambiguous fields.
- **Accessibility first**: All label templates include proper accessibility attributes and associations.
- **Internationalization**: Design label configurations that work across multiple languages.
- **Progressive disclosure**: Consider showing additional guidance only when needed to avoid clutter.
- **Visual hierarchy**: Use consistent styling for different types of label information.
- **Required field strategy**: Choose either asterisks (*) or text ("Required") and use consistently.
- **Helpful guidance**: Include format examples or constraints in instructional text when helpful.

## Notes

- SafLabel templates are used internally by form components and handle proper label-input association.
- The templates automatically generate unique IDs and proper `for` attributes for accessibility.
- All label components support internationalization through configurable text properties.
- The template system ensures consistent styling and behavior across all form components.
- Required and optional indicators are properly marked with `aria-hidden="true"` to prevent redundant screen reader announcements.
- Instructional text is properly associated with form controls for screen reader users.
- The label templates support both simple and complex labeling scenarios.
