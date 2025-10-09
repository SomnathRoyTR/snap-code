# SafForm Component

## Overview

SafForm is a comprehensive form management component designed for complex data entry, validation, and submission workflows. It provides advanced features including field validation, conditional logic, multi-step forms, auto-save, file uploads, and integration with legal data systems. The component is ideal for client intake forms, case documentation, contract generation, compliance reporting, legal research forms, and any application requiring robust form handling with real-time validation and user guidance.

## React API

### SafForm

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `onSubmit` | `(data: FormData, event: FormEvent) => void \| Promise<void>` | Yes | - | Form submission handler |
| `initialValues` | `Record<string, any>` | No | `{}` | Initial form field values |
| `validationSchema` | `ValidationSchema` | No | - | Form validation schema |
| `mode` | `'onChange' \| 'onBlur' \| 'onSubmit' \| 'all'` | No | `'onBlur'` | Validation trigger mode |
| `revalidateMode` | `'onChange' \| 'onBlur' \| 'onSubmit'` | No | `'onChange'` | Revalidation trigger mode |
| `disabled` | `boolean` | No | `false` | Disable entire form |
| `readOnly` | `boolean` | No | `false` | Make form read-only |
| `loading` | `boolean` | No | `false` | Show form loading state |
| `autoSave` | `boolean \| AutoSaveConfig` | No | `false` | Enable auto-save functionality |
| `resetOnSubmit` | `boolean` | No | `false` | Reset form after successful submission |
| `validateOnMount` | `boolean` | No | `false` | Validate form when mounted |
| `focusFirstError` | `boolean` | No | `true` | Focus first field with error |
| `scrollToError` | `boolean` | No | `true` | Scroll to first error field |
| `preserveValues` | `boolean` | No | `false` | Preserve values on unmount |
| `layout` | `'vertical' \| 'horizontal' \| 'inline' \| 'grid'` | No | `'vertical'` | Form layout style |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Form field sizes |
| `variant` | `'default' \| 'outlined' \| 'filled' \| 'minimal'` | No | `'default'` | Form style variant |
| `spacing` | `'compact' \| 'normal' \| 'comfortable'` | No | `'normal'` | Field spacing |
| `labelPosition` | `'top' \| 'left' \| 'right' \| 'floating'` | No | `'top'` | Label positioning |
| `requiredIndicator` | `'asterisk' \| 'text' \| 'none'` | No | `'asterisk'` | Required field indicator |
| `errorDisplay` | `'tooltip' \| 'inline' \| 'summary' \| 'none'` | No | `'inline'` | Error display mode |
| `successMessage` | `string \| ReactNode` | No | - | Success message after submission |
| `errorMessage` | `string \| ReactNode` | No | - | Global error message |
| `submitButton` | `ButtonConfig \| boolean` | No | `true` | Submit button configuration |
| `resetButton` | `ButtonConfig \| boolean` | No | `false` | Reset button configuration |
| `actions` | `FormAction[]` | No | - | Custom action buttons |
| `progress` | `ProgressConfig \| boolean` | No | `false` | Form progress indicator |
| `steps` | `FormStep[]` | No | - | Multi-step form configuration |
| `currentStep` | `number` | No | `0` | Current step in multi-step form |
| `onStepChange` | `(step: number) => void` | No | - | Step change handler |
| `conditionalFields` | `ConditionalFieldConfig[]` | No | - | Conditional field logic |
| `onChange` | `(values: FormData, changedField?: string) => void` | No | - | Form values change handler |
| `onValidation` | `(errors: FormErrors, isValid: boolean) => void` | No | - | Validation state handler |
| `onReset` | `() => void` | No | - | Form reset handler |
| `onAutoSave` | `(data: FormData) => void` | No | - | Auto-save handler |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |
| `children` | `ReactNode` | No | - | Form content |

### Form Interfaces

```typescript
interface ValidationSchema {
  [fieldName: string]: FieldValidation;
}

interface FieldValidation {
  required?: boolean | string;
  minLength?: number | { value: number; message: string };
  maxLength?: number | { value: number; message: string };
  min?: number | { value: number; message: string };
  max?: number | { value: number; message: string };
  pattern?: RegExp | { value: RegExp; message: string };
  custom?: (value: any, formData: FormData) => boolean | string;
  dependencies?: string[];
}

interface AutoSaveConfig {
  interval?: number; // milliseconds
  debounce?: number; // milliseconds
  exclude?: string[]; // field names to exclude
  onSave?: (data: FormData) => void;
  onError?: (error: Error) => void;
}

interface FormStep {
  id: string;
  title: string;
  description?: string;
  fields: string[];
  optional?: boolean;
  validation?: ValidationSchema;
  onEnter?: (formData: FormData) => void;
  onExit?: (formData: FormData) => boolean | Promise<boolean>;
}

interface ConditionalFieldConfig {
  field: string;
  condition: (formData: FormData) => boolean;
  action: 'show' | 'hide' | 'enable' | 'disable' | 'require';
}

interface FormAction {
  id: string;
  label: string;
  variant?: 'primary' | 'secondary' | 'tertiary' | 'danger';
  icon?: string;
  position?: 'left' | 'right';
  disabled?: boolean | ((formData: FormData) => boolean);
  loading?: boolean;
  onClick: (formData: FormData, event: React.MouseEvent) => void;
}

interface ProgressConfig {
  show?: boolean;
  showSteps?: boolean;
  showPercentage?: boolean;
  calculate?: (formData: FormData, steps: FormStep[]) => number;
}
```

### Form Hooks

```typescript
// Main form hook
const useForm = (config?: FormConfig) => ({
  formState: FormState;
  register: (name: string, validation?: FieldValidation) => FieldRegistration;
  unregister: (name: string) => void;
  setValue: (name: string, value: any, options?: SetValueOptions) => void;
  getValue: (name: string) => any;
  getValues: () => FormData;
  watch: (name?: string | string[]) => any;
  reset: (values?: FormData) => void;
  trigger: (name?: string | string[]) => Promise<boolean>;
  clearErrors: (name?: string | string[]) => void;
  setError: (name: string, error: FieldError) => void;
  handleSubmit: (onSubmit: SubmitHandler) => (event: FormEvent) => void;
});

// Field-specific hooks
const useFormField = (name: string) => FieldState;
const useFormValidation = () => ValidationState;
const useFormProgress = () => ProgressState;
```

## Angular API

### saf-form

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[initialValues]` | `Record<string, any>` | No | `{}` | Initial form field values |
| `[validationSchema]` | `ValidationSchema` | No | - | Form validation schema |
| `[mode]` | `'onChange' \| 'onBlur' \| 'onSubmit' \| 'all'` | No | `'onBlur'` | Validation trigger mode |
| `[revalidateMode]` | `'onChange' \| 'onBlur' \| 'onSubmit'` | No | `'onChange'` | Revalidation trigger mode |
| `[disabled]` | `boolean` | No | `false` | Disable entire form |
| `[readOnly]` | `boolean` | No | `false` | Make form read-only |
| `[loading]` | `boolean` | No | `false` | Show form loading state |
| `[autoSave]` | `boolean \| AutoSaveConfig` | No | `false` | Enable auto-save functionality |
| `[resetOnSubmit]` | `boolean` | No | `false` | Reset form after successful submission |
| `[validateOnMount]` | `boolean` | No | `false` | Validate form when mounted |
| `[focusFirstError]` | `boolean` | No | `true` | Focus first field with error |
| `[scrollToError]` | `boolean` | No | `true` | Scroll to first error field |
| `[layout]` | `'vertical' \| 'horizontal' \| 'inline' \| 'grid'` | No | `'vertical'` | Form layout style |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Form field sizes |
| `[variant]` | `'default' \| 'outlined' \| 'filled' \| 'minimal'` | No | `'default'` | Form style variant |
| `[spacing]` | `'compact' \| 'normal' \| 'comfortable'` | No | `'normal'` | Field spacing |
| `[labelPosition]` | `'top' \| 'left' \| 'right' \| 'floating'` | No | `'top'` | Label positioning |
| `[requiredIndicator]` | `'asterisk' \| 'text' \| 'none'` | No | `'asterisk'` | Required field indicator |
| `[errorDisplay]` | `'tooltip' \| 'inline' \| 'summary' \| 'none'` | No | `'inline'` | Error display mode |
| `[successMessage]` | `string \| TemplateRef` | No | - | Success message after submission |
| `[errorMessage]` | `string \| TemplateRef` | No | - | Global error message |
| `[submitButton]` | `ButtonConfig \| boolean` | No | `true` | Submit button configuration |
| `[resetButton]` | `ButtonConfig \| boolean` | No | `false` | Reset button configuration |
| `[actions]` | `FormAction[]` | No | - | Custom action buttons |
| `[progress]` | `ProgressConfig \| boolean` | No | `false` | Form progress indicator |
| `[steps]` | `FormStep[]` | No | - | Multi-step form configuration |
| `[currentStep]` | `number` | No | `0` | Current step in multi-step form |
| `[conditionalFields]` | `ConditionalFieldConfig[]` | No | - | Conditional field logic |
| `(submit)` | `EventEmitter<FormData>` | No | - | Form submission event |
| `(change)` | `EventEmitter<{values: FormData, changedField?: string}>` | No | - | Form values change event |
| `(validation)` | `EventEmitter<{errors: FormErrors, isValid: boolean}>` | No | - | Validation state event |
| `(reset)` | `EventEmitter<void>` | No | - | Form reset event |
| `(stepChange)` | `EventEmitter<number>` | No | - | Step change event |
| `(autoSave)` | `EventEmitter<FormData>` | No | - | Auto-save event |

### Services

```typescript
@Injectable()
export class SafFormService {
  createForm(config: FormConfig): FormGroup;
  validateForm(form: FormGroup, schema: ValidationSchema): ValidationResult;
  autoSave(form: FormGroup, config: AutoSaveConfig): Observable<void>;
  generateFormFromSchema(schema: JsonSchema): FormGroup;
  exportFormData(form: FormGroup, format: 'json' | 'pdf' | 'xml'): Observable<Blob>;
}
```

## Usage Examples

### Client Intake Form

#### React
```jsx
import { SafForm, SafFormField, SafInput, SafSelect, SafTextarea, SafDatePicker, SafFileUpload, SafCheckbox, SafRadio, SafButton } from '@saffron/react';
import { useState } from 'react';

const ClientIntakeForm = () => {
  const [formData, setFormData] = useState({});
  const [loading, setLoading] = useState(false);
  const [submitted, setSubmitted] = useState(false);

  const initialValues = {
    clientType: 'individual',
    urgency: 'normal',
    communicationPreference: 'email',
    referralSource: '',
    hasConflictCheck: false,
    agreedToTerms: false,
    marketingConsent: false
  };

  const validationSchema = {
    firstName: {
      required: 'First name is required',
      minLength: { value: 2, message: 'First name must be at least 2 characters' },
      maxLength: { value: 50, message: 'First name cannot exceed 50 characters' }
    },
    lastName: {
      required: 'Last name is required',
      minLength: { value: 2, message: 'Last name must be at least 2 characters' },
      maxLength: { value: 50, message: 'Last name cannot exceed 50 characters' }
    },
    email: {
      required: 'Email address is required',
      pattern: {
        value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
        message: 'Please enter a valid email address'
      }
    },
    phone: {
      required: 'Phone number is required',
      pattern: {
        value: /^[\+]?[1-9][\d]{0,15}$/,
        message: 'Please enter a valid phone number'
      }
    },
    clientType: {
      required: 'Please select client type'
    },
    legalMatter: {
      required: 'Please describe your legal matter',
      minLength: { value: 20, message: 'Please provide more details (minimum 20 characters)' },
      maxLength: { value: 2000, message: 'Description cannot exceed 2000 characters' }
    },
    preferredAttorney: {
      dependencies: ['practiceArea']
    },
    hasConflictCheck: {
      custom: (value, formData) => {
        if (formData.clientType === 'corporate' && !value) {
          return 'Conflict check is required for corporate clients';
        }
        return true;
      }
    },
    agreedToTerms: {
      required: 'You must agree to the terms and conditions'
    }
  };

  const conditionalFields = [
    {
      field: 'companyName',
      condition: (data) => data.clientType === 'corporate',
      action: 'require'
    },
    {
      field: 'jobTitle',
      condition: (data) => data.clientType === 'corporate',
      action: 'show'
    },
    {
      field: 'taxId',
      condition: (data) => data.clientType === 'corporate',
      action: 'show'
    },
    {
      field: 'preferredAttorney',
      condition: (data) => data.practiceArea !== '',
      action: 'enable'
    }
  ];

  const autoSaveConfig = {
    interval: 30000, // 30 seconds
    debounce: 1000,  // 1 second
    exclude: ['agreedToTerms', 'marketingConsent'],
    onSave: (data) => {
      console.log('Auto-saved form data:', data);
      localStorage.setItem('clientIntakeForm', JSON.stringify(data));
    },
    onError: (error) => {
      console.error('Auto-save failed:', error);
    }
  };

  const handleSubmit = async (data, event) => {
    setLoading(true);
    try {
      // Simulate API submission
      await new Promise(resolve => setTimeout(resolve, 2000));
      
      console.log('Form submitted successfully:', data);
      
      // Clear auto-saved data
      localStorage.removeItem('clientIntakeForm');
      
      setSubmitted(true);
      setFormData(data);
    } catch (error) {
      console.error('Form submission failed:', error);
    } finally {
      setLoading(false);
    }
  };

  const handleChange = (values, changedField) => {
    console.log('Form changed:', { values, changedField });
    setFormData(values);
  };

  const handleValidation = (errors, isValid) => {
    console.log('Validation state:', { errors, isValid });
  };

  if (submitted) {
    return (
      <div className="submission-success">
        <div className="success-content">
          <SafIcon name="check-circle" size="large" color="success" />
          <h2>Client Intake Form Submitted Successfully</h2>
          <p>
            Thank you, {formData.firstName} {formData.lastName}. 
            Your request has been received and will be reviewed by our legal team.
          </p>
          <div className="next-steps">
            <h3>What happens next?</h3>
            <ul>
              <li>Our team will review your case within 24-48 hours</li>
              <li>We'll conduct a conflict check if required</li>
              <li>A lawyer will contact you to discuss your matter</li>
              <li>We'll provide an initial assessment and fee estimate</li>
            </ul>
          </div>
          <SafButton
            variant="primary"
            onClick={() => setSubmitted(false)}
          >
            Submit Another Form
          </SafButton>
        </div>
      </div>
    );
  }

  return (
    <div className="client-intake-form-demo">
      <div className="form-header">
        <h1>Client Intake Form</h1>
        <p>Please provide your information so we can assist you with your legal matter.</p>
      </div>

      <SafForm
        initialValues={initialValues}
        validationSchema={validationSchema}
        conditionalFields={conditionalFields}
        autoSave={autoSaveConfig}
        onSubmit={handleSubmit}
        onChange={handleChange}
        onValidation={handleValidation}
        loading={loading}
        layout="vertical"
        size="medium"
        variant="outlined"
        spacing="comfortable"
        focusFirstError={true}
        scrollToError={true}
        submitButton={{
          label: 'Submit Intake Form',
          icon: 'send',
          variant: 'primary',
          size: 'large'
        }}
        resetButton={{
          label: 'Clear Form',
          variant: 'secondary'
        }}
        progress={{
          show: true,
          showPercentage: true,
          calculate: (data) => {
            const requiredFields = ['firstName', 'lastName', 'email', 'phone', 'legalMatter'];
            const completed = requiredFields.filter(field => data[field] && data[field].trim()).length;
            return (completed / requiredFields.length) * 100;
          }
        }}
        successMessage="Your client intake form has been submitted successfully!"
      >
        <div className="form-sections">
          {/* Personal Information Section */}
          <div className="form-section">
            <h2>Personal Information</h2>
            
            <div className="form-row">
              <SafFormField
                name="firstName"
                label="First Name"
                required
                help="Enter your legal first name"
              >
                <SafInput
                  placeholder="Enter first name"
                  autoComplete="given-name"
                />
              </SafFormField>

              <SafFormField
                name="lastName"
                label="Last Name"
                required
                help="Enter your legal last name"
              >
                <SafInput
                  placeholder="Enter last name"
                  autoComplete="family-name"
                />
              </SafFormField>
            </div>

            <div className="form-row">
              <SafFormField
                name="email"
                label="Email Address"
                required
                help="We'll use this for all communications"
              >
                <SafInput
                  type="email"
                  placeholder="Enter email address"
                  autoComplete="email"
                />
              </SafFormField>

              <SafFormField
                name="phone"
                label="Phone Number"
                required
                help="Primary contact number"
              >
                <SafInput
                  type="tel"
                  placeholder="Enter phone number"
                  autoComplete="tel"
                />
              </SafFormField>
            </div>

            <SafFormField
              name="clientType"
              label="Client Type"
              required
            >
              <SafRadio
                options={[
                  { label: 'Individual', value: 'individual', description: 'Personal legal matter' },
                  { label: 'Corporate', value: 'corporate', description: 'Business legal matter' },
                  { label: 'Non-Profit', value: 'nonprofit', description: 'Non-profit organization' }
                ]}
                layout="horizontal"
              />
            </SafFormField>

            {/* Conditional Corporate Fields */}
            <ConditionalFields show={formData.clientType === 'corporate'}>
              <div className="corporate-fields">
                <SafFormField
                  name="companyName"
                  label="Company Name"
                  required={formData.clientType === 'corporate'}
                >
                  <SafInput
                    placeholder="Enter company name"
                    autoComplete="organization"
                  />
                </SafFormField>

                <div className="form-row">
                  <SafFormField
                    name="jobTitle"
                    label="Job Title"
                  >
                    <SafInput
                      placeholder="Enter job title"
                      autoComplete="organization-title"
                    />
                  </SafFormField>

                  <SafFormField
                    name="taxId"
                    label="Tax ID / EIN"
                  >
                    <SafInput
                      placeholder="Enter tax ID"
                    />
                  </SafFormField>
                </div>
              </div>
            </ConditionalFields>
          </div>

          {/* Contact Information Section */}
          <div className="form-section">
            <h2>Contact Information</h2>
            
            <div className="form-row">
              <SafFormField
                name="address"
                label="Street Address"
              >
                <SafInput
                  placeholder="Enter street address"
                  autoComplete="street-address"
                />
              </SafFormField>
            </div>

            <div className="form-row">
              <SafFormField
                name="city"
                label="City"
              >
                <SafInput
                  placeholder="Enter city"
                  autoComplete="address-level2"
                />
              </SafFormField>

              <SafFormField
                name="state"
                label="State/Province"
              >
                <SafSelect
                  placeholder="Select state"
                  options={[
                    { label: 'New York', value: 'NY' },
                    { label: 'California', value: 'CA' },
                    { label: 'Texas', value: 'TX' },
                    { label: 'Florida', value: 'FL' },
                    // ... more states
                  ]}
                  searchable
                />
              </SafFormField>

              <SafFormField
                name="zipCode"
                label="ZIP/Postal Code"
              >
                <SafInput
                  placeholder="Enter ZIP code"
                  autoComplete="postal-code"
                />
              </SafFormField>
            </div>

            <SafFormField
              name="communicationPreference"
              label="Preferred Communication Method"
            >
              <SafSelect
                options={[
                  { label: 'Email', value: 'email' },
                  { label: 'Phone', value: 'phone' },
                  { label: 'Text Message', value: 'sms' },
                  { label: 'Mail', value: 'mail' }
                ]}
              />
            </SafFormField>
          </div>

          {/* Legal Matter Section */}
          <div className="form-section">
            <h2>Legal Matter Information</h2>
            
            <SafFormField
              name="practiceArea"
              label="Practice Area"
              required
              help="Select the area of law that best describes your matter"
            >
              <SafSelect
                placeholder="Select practice area"
                options={[
                  { label: 'Corporate Law', value: 'corporate' },
                  { label: 'Employment Law', value: 'employment' },
                  { label: 'Intellectual Property', value: 'ip' },
                  { label: 'Real Estate', value: 'realestate' },
                  { label: 'Litigation', value: 'litigation' },
                  { label: 'Tax Law', value: 'tax' },
                  { label: 'Family Law', value: 'family' },
                  { label: 'Immigration', value: 'immigration' },
                  { label: 'Other', value: 'other' }
                ]}
                searchable
              />
            </SafFormField>

            <SafFormField
              name="preferredAttorney"
              label="Preferred Attorney"
              help="Select from available attorneys in your practice area"
              disabled={!formData.practiceArea}
            >
              <SafSelect
                placeholder="Select attorney (optional)"
                options={[
                  { label: 'Sarah Johnson - Senior Partner', value: 'sarah.johnson' },
                  { label: 'Michael Chen - Partner', value: 'michael.chen' },
                  { label: 'Emily Rodriguez - Associate', value: 'emily.rodriguez' },
                  { label: 'No preference', value: 'no-preference' }
                ]}
              />
            </SafFormField>

            <SafFormField
              name="legalMatter"
              label="Description of Legal Matter"
              required
              help="Please provide a detailed description of your legal matter (minimum 20 characters)"
            >
              <SafTextarea
                placeholder="Describe your legal matter in detail..."
                rows={6}
                maxLength={2000}
                showCharacterCount
              />
            </SafFormField>

            <SafFormField
              name="urgency"
              label="Urgency Level"
            >
              <SafRadio
                options={[
                  { label: 'Low - No immediate deadline', value: 'low' },
                  { label: 'Normal - Within 30 days', value: 'normal' },
                  { label: 'High - Within 1 week', value: 'high' },
                  { label: 'Urgent - Immediate attention needed', value: 'urgent' }
                ]}
              />
            </SafFormField>

            <SafFormField
              name="referralSource"
              label="How did you hear about us?"
            >
              <SafSelect
                placeholder="Select referral source"
                options={[
                  { label: 'Google Search', value: 'google' },
                  { label: 'Referral from Friend/Family', value: 'referral-personal' },
                  { label: 'Referral from Another Attorney', value: 'referral-attorney' },
                  { label: 'Thomson Reuters Directory', value: 'tr-directory' },
                  { label: 'Social Media', value: 'social-media' },
                  { label: 'Professional Network', value: 'professional' },
                  { label: 'Advertisement', value: 'advertisement' },
                  { label: 'Other', value: 'other' }
                ]}
              />
            </SafFormField>
          </div>

          {/* Document Upload Section */}
          <div className="form-section">
            <h2>Supporting Documents</h2>
            
            <SafFormField
              name="documents"
              label="Upload Documents"
              help="Upload any relevant documents (contracts, correspondence, etc.)"
            >
              <SafFileUpload
                accept=".pdf,.doc,.docx,.txt,.jpg,.png"
                multiple
                maxFiles={10}
                maxSize="10MB"
                placeholder="Drop files here or click to upload"
                showFileList
              />
            </SafFormField>
          </div>

          {/* Agreements Section */}
          <div className="form-section">
            <h2>Agreements and Consents</h2>
            
            <SafFormField
              name="hasConflictCheck"
              variant="checkbox"
            >
              <SafCheckbox
                label="I understand that a conflict check will be performed"
                description="We must check for potential conflicts of interest before representation"
              />
            </SafFormField>

            <SafFormField
              name="agreedToTerms"
              variant="checkbox"
              required
            >
              <SafCheckbox
                label="I agree to the Terms and Conditions"
                description={
                  <span>
                    I have read and agree to the{' '}
                    <a href="/terms" target="_blank">Terms and Conditions</a>
                    {' '}and{' '}
                    <a href="/privacy" target="_blank">Privacy Policy</a>
                  </span>
                }
              />
            </SafFormField>

            <SafFormField
              name="marketingConsent"
              variant="checkbox"
            >
              <SafCheckbox
                label="I consent to receive marketing communications"
                description="Receive updates about legal services and industry insights (optional)"
              />
            </SafFormField>
          </div>

          {/* Form Actions */}
          <div className="form-actions">
            <SafButton
              type="button"
              variant="secondary"
              onClick={() => {
                const saved = localStorage.getItem('clientIntakeForm');
                if (saved) {
                  setFormData(JSON.parse(saved));
                }
              }}
            >
              Load Saved Data
            </SafButton>
            
            <div className="primary-actions">
              <SafButton
                type="reset"
                variant="tertiary"
              >
                Clear Form
              </SafButton>
              
              <SafButton
                type="submit"
                variant="primary"
                loading={loading}
                icon="send"
              >
                Submit Intake Form
              </SafButton>
            </div>
          </div>
        </div>
      </SafForm>
    </div>
  );
};

// Conditional fields wrapper component
const ConditionalFields = ({ show, children }) => {
  return show ? <div className="conditional-fields">{children}</div> : null;
};
```

#### Angular
```typescript
// client-intake-form.component.ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-client-intake-form',
  template: `
    <div class="client-intake-form-demo">
      <div class="form-header">
        <h1>Client Intake Form</h1>
        <p>Please provide your information so we can assist you with your legal matter.</p>
      </div>

      <saf-form
        [initialValues]="initialValues"
        [validationSchema]="validationSchema"
        [conditionalFields]="conditionalFields"
        [autoSave]="autoSaveConfig"
        [loading]="loading"
        layout="vertical"
        size="medium"
        variant="outlined"
        spacing="comfortable"
        [focusFirstError]="true"
        [scrollToError]="true"
        [submitButton]="submitButtonConfig"
        [resetButton]="resetButtonConfig"
        [progress]="progressConfig"
        (submit)="handleSubmit($event)"
        (change)="handleChange($event)"
        (validation)="handleValidation($event)">

        <div class="form-sections">
          <!-- Personal Information Section -->
          <div class="form-section">
            <h2>Personal Information</h2>
            
            <div class="form-row">
              <saf-form-field
                name="firstName"
                label="First Name"
                [required]="true"
                help="Enter your legal first name">
                <saf-input
                  placeholder="Enter first name"
                  autoComplete="given-name">
                </saf-input>
              </saf-form-field>

              <saf-form-field
                name="lastName"
                label="Last Name"
                [required]="true"
                help="Enter your legal last name">
                <saf-input
                  placeholder="Enter last name"
                  autoComplete="family-name">
                </saf-input>
              </saf-form-field>
            </div>

            <div class="form-row">
              <saf-form-field
                name="email"
                label="Email Address"
                [required]="true"
                help="We'll use this for all communications">
                <saf-input
                  type="email"
                  placeholder="Enter email address"
                  autoComplete="email">
                </saf-input>
              </saf-form-field>

              <saf-form-field
                name="phone"
                label="Phone Number"
                [required]="true"
                help="Primary contact number">
                <saf-input
                  type="tel"
                  placeholder="Enter phone number"
                  autoComplete="tel">
                </saf-input>
              </saf-form-field>
            </div>

            <saf-form-field
              name="clientType"
              label="Client Type"
              [required]="true">
              <saf-radio
                [options]="clientTypeOptions"
                layout="horizontal">
              </saf-radio>
            </saf-form-field>

            <!-- Conditional Corporate Fields -->
            <div class="corporate-fields" *ngIf="formData.clientType === 'corporate'">
              <saf-form-field
                name="companyName"
                label="Company Name"
                [required]="formData.clientType === 'corporate'">
                <saf-input
                  placeholder="Enter company name"
                  autoComplete="organization">
                </saf-input>
              </saf-form-field>

              <div class="form-row">
                <saf-form-field
                  name="jobTitle"
                  label="Job Title">
                  <saf-input
                    placeholder="Enter job title"
                    autoComplete="organization-title">
                  </saf-input>
                </saf-form-field>

                <saf-form-field
                  name="taxId"
                  label="Tax ID / EIN">
                  <saf-input placeholder="Enter tax ID"></saf-input>
                </saf-form-field>
              </div>
            </div>
          </div>

          <!-- Legal Matter Section -->
          <div class="form-section">
            <h2>Legal Matter Information</h2>
            
            <saf-form-field
              name="practiceArea"
              label="Practice Area"
              [required]="true"
              help="Select the area of law that best describes your matter">
              <saf-select
                placeholder="Select practice area"
                [options]="practiceAreaOptions"
                [searchable]="true">
              </saf-select>
            </saf-form-field>

            <saf-form-field
              name="legalMatter"
              label="Description of Legal Matter"
              [required]="true"
              help="Please provide a detailed description of your legal matter">
              <saf-textarea
                placeholder="Describe your legal matter in detail..."
                [rows]="6"
                [maxLength]="2000"
                [showCharacterCount]="true">
              </saf-textarea>
            </saf-form-field>

            <saf-form-field
              name="urgency"
              label="Urgency Level">
              <saf-radio [options]="urgencyOptions"></saf-radio>
            </saf-form-field>
          </div>

          <!-- Document Upload Section -->
          <div class="form-section">
            <h2>Supporting Documents</h2>
            
            <saf-form-field
              name="documents"
              label="Upload Documents"
              help="Upload any relevant documents (contracts, correspondence, etc.)">
              <saf-file-upload
                accept=".pdf,.doc,.docx,.txt,.jpg,.png"
                [multiple]="true"
                [maxFiles]="10"
                maxSize="10MB"
                placeholder="Drop files here or click to upload"
                [showFileList]="true">
              </saf-file-upload>
            </saf-form-field>
          </div>

          <!-- Agreements Section -->
          <div class="form-section">
            <h2>Agreements and Consents</h2>
            
            <saf-form-field
              name="agreedToTerms"
              variant="checkbox"
              [required]="true">
              <saf-checkbox
                label="I agree to the Terms and Conditions"
                [description]="termsDescription">
              </saf-checkbox>
            </saf-form-field>
          </div>
        </div>
      </saf-form>
    </div>
  `
})
export class ClientIntakeFormComponent implements OnInit {
  loading = false;
  formData: any = {};

  initialValues = {
    clientType: 'individual',
    urgency: 'normal',
    communicationPreference: 'email',
    referralSource: '',
    hasConflictCheck: false,
    agreedToTerms: false,
    marketingConsent: false
  };

  validationSchema = {
    firstName: {
      required: 'First name is required',
      minLength: { value: 2, message: 'First name must be at least 2 characters' }
    },
    lastName: {
      required: 'Last name is required',
      minLength: { value: 2, message: 'Last name must be at least 2 characters' }
    },
    email: {
      required: 'Email address is required',
      pattern: {
        value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
        message: 'Please enter a valid email address'
      }
    },
    legalMatter: {
      required: 'Please describe your legal matter',
      minLength: { value: 20, message: 'Please provide more details (minimum 20 characters)' }
    },
    agreedToTerms: {
      required: 'You must agree to the terms and conditions'
    }
  };

  conditionalFields = [
    {
      field: 'companyName',
      condition: (data: any) => data.clientType === 'corporate',
      action: 'require'
    }
  ];

  autoSaveConfig = {
    interval: 30000,
    debounce: 1000,
    exclude: ['agreedToTerms', 'marketingConsent']
  };

  submitButtonConfig = {
    label: 'Submit Intake Form',
    icon: 'send',
    variant: 'primary',
    size: 'large'
  };

  resetButtonConfig = {
    label: 'Clear Form',
    variant: 'secondary'
  };

  progressConfig = {
    show: true,
    showPercentage: true
  };

  clientTypeOptions = [
    { label: 'Individual', value: 'individual', description: 'Personal legal matter' },
    { label: 'Corporate', value: 'corporate', description: 'Business legal matter' },
    { label: 'Non-Profit', value: 'nonprofit', description: 'Non-profit organization' }
  ];

  practiceAreaOptions = [
    { label: 'Corporate Law', value: 'corporate' },
    { label: 'Employment Law', value: 'employment' },
    { label: 'Intellectual Property', value: 'ip' },
    { label: 'Real Estate', value: 'realestate' },
    { label: 'Litigation', value: 'litigation' }
  ];

  urgencyOptions = [
    { label: 'Low - No immediate deadline', value: 'low' },
    { label: 'Normal - Within 30 days', value: 'normal' },
    { label: 'High - Within 1 week', value: 'high' },
    { label: 'Urgent - Immediate attention needed', value: 'urgent' }
  ];

  termsDescription = 'I have read and agree to the Terms and Conditions and Privacy Policy';

  ngOnInit() {
    // Initialize form
  }

  async handleSubmit(data: any) {
    this.loading = true;
    try {
      await new Promise(resolve => setTimeout(resolve, 2000));
      console.log('Form submitted successfully:', data);
    } catch (error) {
      console.error('Form submission failed:', error);
    } finally {
      this.loading = false;
    }
  }

  handleChange(event: any) {
    this.formData = event.values;
    console.log('Form changed:', event);
  }

  handleValidation(event: any) {
    console.log('Validation state:', event);
  }
}
```

## Best Practices

1. **Form Design**
   - Group related fields logically
   - Use clear, descriptive labels
   - Provide helpful validation messages
   - Implement progressive disclosure for complex forms

2. **Validation**
   - Validate on appropriate events (blur, change, submit)
   - Provide immediate feedback for errors
   - Use client-side validation with server-side backup
   - Show validation status clearly

3. **User Experience**
   - Auto-save form data to prevent loss
   - Show form completion progress
   - Focus management for accessibility
   - Responsive design for all devices

4. **Performance**
   - Lazy load form sections when needed
   - Debounce validation and auto-save
   - Optimize re-renders with proper memoization
   - Handle large file uploads efficiently

5. **Security**
   - Sanitize all form inputs
   - Validate file uploads server-side
   - Implement CSRF protection
   - Use secure data transmission

## Accessibility Considerations

1. **Screen Reader Support**
   - Proper form labels and descriptions
   - Error announcements
   - Progress indicators
   - Field state changes

2. **Keyboard Navigation**
   - Tab order management
   - Enter key submission
   - Arrow key navigation in radio groups
   - Escape key to cancel actions

3. **Visual Accessibility**
   - High contrast mode support
   - Error color coding with icons
   - Clear focus indicators
   - Scalable text and interface elements

4. **Motor Accessibility**
   - Large touch targets
   - Click area expansion
   - Drag and drop alternatives
   - Voice input support

## Related Components

- **SafFormField**: Individual form field wrapper
- **SafInput**: Text input fields
- **SafSelect**: Dropdown selection fields
- **SafTextarea**: Multi-line text inputs
- **SafFileUpload**: File upload functionality

## Notes

- Form supports complex validation with dependencies and conditional logic
- Auto-save functionality prevents data loss
- Multi-step form support with progress tracking
- Integration with legal industry validation patterns
- Comprehensive accessibility support with ARIA attributes
- Mobile-responsive design with touch-friendly interactions
- Real-time validation feedback with debounced updates
- File upload integration with legal document handling
- Data export capabilities in multiple formats
