# SafFormField Component

## Overview

SafFormField is a comprehensive form field wrapper component designed to provide consistent labeling, validation, help text, and accessibility features for form inputs. It integrates seamlessly with the SafForm ecosystem to deliver professional form experiences with legal industry-specific patterns. The component supports various field types, validation states, conditional visibility, and advanced features like field dependencies, custom validation messages, and responsive layouts ideal for legal data entry workflows.

## React API

### SafFormField

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `name` | `string` | Yes | - | Field name for form registration |
| `label` | `string \| ReactNode` | No | - | Field label content |
| `description` | `string \| ReactNode` | No | - | Field description or help text |
| `required` | `boolean` | No | `false` | Mark field as required |
| `disabled` | `boolean` | No | `false` | Disable field interaction |
| `readOnly` | `boolean` | No | `false` | Make field read-only |
| `hidden` | `boolean` | No | `false` | Hide field from display |
| `error` | `string \| ReactNode` | No | - | Custom error message |
| `warning` | `string \| ReactNode` | No | - | Warning message |
| `success` | `string \| ReactNode` | No | - | Success message |
| `info` | `string \| ReactNode` | No | - | Informational message |
| `help` | `string \| ReactNode` | No | - | Help text or tooltip content |
| `helpPosition` | `'top' \| 'bottom' \| 'right' \| 'tooltip'` | No | `'bottom'` | Help text positioning |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Field size variant |
| `variant` | `'default' \| 'outlined' \| 'filled' \| 'minimal' \| 'inline' \| 'floating'` | No | `'default'` | Field style variant |
| `layout` | `'vertical' \| 'horizontal' \| 'inline'` | No | `'vertical'` | Field layout direction |
| `labelWidth` | `string \| number` | No | - | Label width in horizontal layout |
| `labelPosition` | `'top' \| 'left' \| 'right' \| 'floating' \| 'inside'` | No | `'top'` | Label positioning |
| `requiredIndicator` | `'asterisk' \| 'text' \| 'icon' \| 'none'` | No | `'asterisk'` | Required field indicator style |
| `optionalIndicator` | `boolean \| string` | No | `false` | Show optional field indicator |
| `validationTrigger` | `'onChange' \| 'onBlur' \| 'onSubmit' \| 'manual'` | No | `'onBlur'` | When to trigger validation |
| `showValidationIcon` | `boolean` | No | `true` | Show validation state icons |
| `validationDelay` | `number` | No | `300` | Validation debounce delay (ms) |
| `errorDisplay` | `'inline' \| 'tooltip' \| 'modal' \| 'none'` | No | `'inline'` | Error message display style |
| `maxErrorLength` | `number` | No | `200` | Maximum error message length |
| `multipleErrors` | `boolean` | No | `false` | Show multiple error messages |
| `fieldType` | `'text' \| 'email' \| 'password' \| 'number' \| 'tel' \| 'url' \| 'date' \| 'time' \| 'datetime' \| 'file' \| 'checkbox' \| 'radio' \| 'select' \| 'textarea' \| 'custom'` | No | `'text'` | Field input type |
| `autoComplete` | `string` | No | - | HTML autocomplete attribute |
| `spellCheck` | `boolean` | No | - | Enable spell checking |
| `tabIndex` | `number` | No | - | Tab order index |
| `accessibilityLabel` | `string` | No | - | ARIA label override |
| `accessibilityDescription` | `string` | No | - | ARIA description |
| `accessibilityInvalid` | `boolean` | No | - | ARIA invalid state |
| `tooltip` | `string \| TooltipConfig` | No | - | Field tooltip configuration |
| `conditionalLogic` | `ConditionalLogic` | No | - | Conditional field behavior |
| `dependencies` | `string[]` | No | - | Field dependencies for validation |
| `width` | `string \| number` | No | - | Field width override |
| `maxWidth` | `string \| number` | No | - | Maximum field width |
| `minWidth` | `string \| number` | No | - | Minimum field width |
| `className` | `string` | No | - | Additional CSS classes |
| `labelClassName` | `string` | No | - | Label CSS classes |
| `inputClassName` | `string` | No | - | Input CSS classes |
| `errorClassName` | `string` | No | - | Error message CSS classes |
| `testId` | `string` | No | - | Test identifier |
| `children` | `ReactNode` | No | - | Form input component |

### Field State Interfaces

```typescript
interface FieldState {
  value: any;
  error: string | null;
  touched: boolean;
  dirty: boolean;
  valid: boolean;
  validating: boolean;
  disabled: boolean;
  readOnly: boolean;
  required: boolean;
}

interface ConditionalLogic {
  condition: (formData: FormData, fieldValue: any) => boolean;
  action: 'show' | 'hide' | 'enable' | 'disable' | 'require' | 'optional';
  trigger?: string[]; // Fields that trigger condition check
}

interface TooltipConfig {
  content: string | ReactNode;
  position?: 'top' | 'bottom' | 'left' | 'right';
  trigger?: 'hover' | 'click' | 'focus';
  delay?: number;
  maxWidth?: string;
}

interface ValidationConfig {
  required?: boolean | string;
  minLength?: number | { value: number; message: string };
  maxLength?: number | { value: number; message: string };
  min?: number | { value: number; message: string };
  max?: number | { value: number; message: string };
  pattern?: RegExp | { value: RegExp; message: string };
  custom?: (value: any, formData: FormData) => boolean | string | Promise<boolean | string>;
  asyncValidation?: (value: any) => Promise<boolean | string>;
  dependencies?: string[];
}
```

### Field Hooks

```typescript
// Field-specific hooks
const useFormField = (name: string) => ({
  field: FieldState;
  fieldProps: FieldProps;
  meta: FieldMeta;
  helpers: FieldHelpers;
});

const useFieldValidation = (name: string, validation: ValidationConfig) => ({
  validate: () => Promise<boolean>;
  clearErrors: () => void;
  setError: (error: string) => void;
  isValidating: boolean;
});

const useConditionalField = (name: string, logic: ConditionalLogic) => ({
  isVisible: boolean;
  isEnabled: boolean;
  isRequired: boolean;
});
```

## Angular API

### saf-form-field

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[name]` | `string` | Yes | - | Field name for form registration |
| `[label]` | `string \| TemplateRef` | No | - | Field label content |
| `[description]` | `string \| TemplateRef` | No | - | Field description or help text |
| `[required]` | `boolean` | No | `false` | Mark field as required |
| `[disabled]` | `boolean` | No | `false` | Disable field interaction |
| `[readOnly]` | `boolean` | No | `false` | Make field read-only |
| `[hidden]` | `boolean` | No | `false` | Hide field from display |
| `[error]` | `string \| TemplateRef` | No | - | Custom error message |
| `[warning]` | `string \| TemplateRef` | No | - | Warning message |
| `[success]` | `string \| TemplateRef` | No | - | Success message |
| `[info]` | `string \| TemplateRef` | No | - | Informational message |
| `[help]` | `string \| TemplateRef` | No | - | Help text or tooltip content |
| `[helpPosition]` | `'top' \| 'bottom' \| 'right' \| 'tooltip'` | No | `'bottom'` | Help text positioning |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Field size variant |
| `[variant]` | `'default' \| 'outlined' \| 'filled' \| 'minimal' \| 'inline' \| 'floating'` | No | `'default'` | Field style variant |
| `[layout]` | `'vertical' \| 'horizontal' \| 'inline'` | No | `'vertical'` | Field layout direction |
| `[labelWidth]` | `string \| number` | No | - | Label width in horizontal layout |
| `[labelPosition]` | `'top' \| 'left' \| 'right' \| 'floating' \| 'inside'` | No | `'top'` | Label positioning |
| `[requiredIndicator]` | `'asterisk' \| 'text' \| 'icon' \| 'none'` | No | `'asterisk'` | Required field indicator style |
| `[optionalIndicator]` | `boolean \| string` | No | `false` | Show optional field indicator |
| `[validationTrigger]` | `'onChange' \| 'onBlur' \| 'onSubmit' \| 'manual'` | No | `'onBlur'` | When to trigger validation |
| `[showValidationIcon]` | `boolean` | No | `true` | Show validation state icons |
| `[validationDelay]` | `number` | No | `300` | Validation debounce delay (ms) |
| `[errorDisplay]` | `'inline' \| 'tooltip' \| 'modal' \| 'none'` | No | `'inline'` | Error message display style |
| `[fieldType]` | `'text' \| 'email' \| 'password' \| 'number' \| 'tel' \| 'url' \| 'date' \| 'time' \| 'datetime' \| 'file' \| 'checkbox' \| 'radio' \| 'select' \| 'textarea' \| 'custom'` | No | `'text'` | Field input type |
| `[tooltip]` | `string \| TooltipConfig` | No | - | Field tooltip configuration |
| `[conditionalLogic]` | `ConditionalLogic` | No | - | Conditional field behavior |
| `[dependencies]` | `string[]` | No | - | Field dependencies for validation |
| `[width]` | `string \| number` | No | - | Field width override |
| `(valueChange)` | `EventEmitter<any>` | No | - | Field value change event |
| `(validationChange)` | `EventEmitter<ValidationState>` | No | - | Validation state change event |
| `(focus)` | `EventEmitter<FocusEvent>` | No | - | Field focus event |
| `(blur)` | `EventEmitter<FocusEvent>` | No | - | Field blur event |

### Directives

```typescript
// Form field directive for custom components
@Directive({
  selector: '[safFormField]'
})
export class SafFormFieldDirective {
  @Input() name: string;
  @Input() validation: ValidationConfig;
  @Input() conditionalLogic: ConditionalLogic;
}

// Field validation directive
@Directive({
  selector: '[safFieldValidation]'
})
export class SafFieldValidationDirective {
  @Input() validationRules: ValidationConfig;
  @Input() validateOn: 'change' | 'blur' | 'submit';
}
```

## Usage Examples

### Legal Contract Form Fields

#### React
```jsx
import { SafFormField, SafInput, SafSelect, SafTextarea, SafDatePicker, SafCheckbox, SafRadio, SafFileUpload, SafButton } from '@saffron/react';
import { useState } from 'react';

const LegalContractFormFields = () => {
  const [formData, setFormData] = useState({
    contractType: '',
    jurisdiction: '',
    governingLaw: '',
    clientType: 'individual',
    hasExistingAgreement: false,
    confidentialityLevel: 'standard'
  });

  const [fieldStates, setFieldStates] = useState({});

  const handleFieldChange = (fieldName, value) => {
    setFormData(prev => ({
      ...prev,
      [fieldName]: value
    }));
  };

  const handleValidationChange = (fieldName, validationState) => {
    setFieldStates(prev => ({
      ...prev,
      [fieldName]: validationState
    }));
  };

  // Contract type-specific conditional logic
  const corporateConditionalLogic = {
    condition: (formData) => formData.clientType === 'corporate',
    action: 'show',
    trigger: ['clientType']
  };

  const existingAgreementLogic = {
    condition: (formData) => formData.hasExistingAgreement === true,
    action: 'require',
    trigger: ['hasExistingAgreement']
  };

  return (
    <div className="legal-contract-form-demo">
      <h1>Legal Contract Information Form</h1>
      <p>Complete the following fields to generate your legal contract documentation.</p>

      <div className="form-sections">
        {/* Contract Basics Section */}
        <div className="form-section">
          <h2>Contract Basics</h2>
          
          <div className="form-row">
            <SafFormField
              name="contractType"
              label="Contract Type"
              description="Select the type of legal contract you need"
              required={true}
              size="large"
              variant="outlined"
              help="Choose the contract category that best fits your legal needs"
              helpPosition="tooltip"
              tooltip={{
                content: "Contract types determine the specific legal framework and clauses that will be included in your agreement.",
                position: "right",
                maxWidth: "300px"
              }}
              fieldType="select"
              validationTrigger="onChange"
              showValidationIcon={true}
              onChange={(value) => handleFieldChange('contractType', value)}
              onValidation={(state) => handleValidationChange('contractType', state)}
            >
              <SafSelect
                placeholder="Select contract type"
                options={[
                  { 
                    label: 'Service Agreement', 
                    value: 'service',
                    description: 'Professional services contract'
                  },
                  { 
                    label: 'Employment Contract', 
                    value: 'employment',
                    description: 'Employee hiring agreement'
                  },
                  { 
                    label: 'Non-Disclosure Agreement (NDA)', 
                    value: 'nda',
                    description: 'Confidentiality protection'
                  },
                  { 
                    label: 'Partnership Agreement', 
                    value: 'partnership',
                    description: 'Business partnership terms'
                  },
                  { 
                    label: 'Licensing Agreement', 
                    value: 'licensing',
                    description: 'Intellectual property licensing'
                  },
                  { 
                    label: 'Purchase Agreement', 
                    value: 'purchase',
                    description: 'Asset or goods purchase'
                  },
                  { 
                    label: 'Lease Agreement', 
                    value: 'lease',
                    description: 'Property or equipment lease'
                  },
                  { 
                    label: 'Consulting Agreement', 
                    value: 'consulting',
                    description: 'Consulting services contract'
                  }
                ]}
                searchable={true}
                groupBy="category"
              />
            </SafFormField>

            <SafFormField
              name="urgency"
              label="Project Urgency"
              description="Timeline for contract completion"
              size="large"
              variant="outlined"
              fieldType="radio"
            >
              <SafRadio
                options={[
                  { 
                    label: 'Standard (2-3 weeks)', 
                    value: 'standard',
                    description: 'Normal processing timeline'
                  },
                  { 
                    label: 'Expedited (1 week)', 
                    value: 'expedited',
                    description: 'Faster turnaround time'
                  },
                  { 
                    label: 'Rush (2-3 days)', 
                    value: 'rush',
                    description: 'Priority processing'
                  },
                  { 
                    label: 'Emergency (24 hours)', 
                    value: 'emergency',
                    description: 'Immediate attention required'
                  }
                ]}
                layout="horizontal"
              />
            </SafFormField>
          </div>

          <SafFormField
            name="contractTitle"
            label="Contract Title"
            description="Descriptive title for your contract"
            required={true}
            size="large"
            variant="outlined"
            help="Provide a clear, descriptive title that identifies the purpose of this contract"
            maxLength={100}
            fieldType="text"
            autoComplete="off"
            spellCheck={true}
          >
            <SafInput
              placeholder="e.g., Software Development Services Agreement"
              maxLength={100}
              showCharacterCount={true}
            />
          </SafFormField>

          <div className="form-row">
            <SafFormField
              name="effectiveDate"
              label="Effective Date"
              description="When the contract becomes active"
              required={true}
              size="large"
              variant="outlined"
              fieldType="date"
              help="The date when contractual obligations begin"
            >
              <SafDatePicker
                placeholder="Select effective date"
                minDate={new Date()}
                showTodayButton={true}
                format="MMMM d, yyyy"
              />
            </SafFormField>

            <SafFormField
              name="expirationDate"
              label="Expiration Date"
              description="When the contract ends (optional)"
              size="large"
              variant="outlined"
              fieldType="date"
              help="Leave blank for indefinite duration contracts"
              optionalIndicator="Optional"
            >
              <SafDatePicker
                placeholder="Select expiration date (optional)"
                minDate={formData.effectiveDate}
                format="MMMM d, yyyy"
                clearable={true}
              />
            </SafFormField>
          </div>
        </div>

        {/* Parties Information Section */}
        <div className="form-section">
          <h2>Contracting Parties</h2>
          
          <SafFormField
            name="clientType"
            label="Client Type"
            description="Type of contracting entity"
            required={true}
            size="large"
            variant="outlined"
            fieldType="radio"
            help="This determines which additional information fields will be required"
          >
            <SafRadio
              options={[
                { 
                  label: 'Individual', 
                  value: 'individual',
                  description: 'Personal contract'
                },
                { 
                  label: 'Corporation', 
                  value: 'corporate',
                  description: 'Business entity'
                },
                { 
                  label: 'Partnership', 
                  value: 'partnership',
                  description: 'Partnership entity'
                },
                { 
                  label: 'Non-Profit', 
                  value: 'nonprofit',
                  description: 'Non-profit organization'
                },
                { 
                  label: 'Government', 
                  value: 'government',
                  description: 'Government entity'
                }
              ]}
              layout="horizontal"
              onChange={(value) => handleFieldChange('clientType', value)}
            />
          </SafFormField>

          <div className="form-row">
            <SafFormField
              name="firstName"
              label="First Name"
              required={formData.clientType === 'individual'}
              size="large"
              variant="outlined"
              hidden={formData.clientType !== 'individual'}
              fieldType="text"
              autoComplete="given-name"
              spellCheck={false}
            >
              <SafInput
                placeholder="Enter first name"
                autoComplete="given-name"
              />
            </SafFormField>

            <SafFormField
              name="lastName"
              label="Last Name"
              required={formData.clientType === 'individual'}
              size="large"
              variant="outlined"
              hidden={formData.clientType !== 'individual'}
              fieldType="text"
              autoComplete="family-name"
              spellCheck={false}
            >
              <SafInput
                placeholder="Enter last name"
                autoComplete="family-name"
              />
            </SafFormField>
          </div>

          {/* Corporate Fields - Conditional */}
          <SafFormField
            name="companyName"
            label="Company/Organization Name"
            required={formData.clientType !== 'individual'}
            size="large"
            variant="outlined"
            conditionalLogic={corporateConditionalLogic}
            fieldType="text"
            autoComplete="organization"
            spellCheck={true}
            help="Legal name of the organization as it appears in official documents"
          >
            <SafInput
              placeholder="Enter company or organization name"
              autoComplete="organization"
            />
          </SafFormField>

          <div className="form-row">
            <SafFormField
              name="contactEmail"
              label="Contact Email"
              description="Primary email for contract communications"
              required={true}
              size="large"
              variant="outlined"
              fieldType="email"
              autoComplete="email"
              help="This email will receive all contract-related communications"
              validationTrigger="onBlur"
              validationDelay={500}
            >
              <SafInput
                type="email"
                placeholder="Enter email address"
                autoComplete="email"
              />
            </SafFormField>

            <SafFormField
              name="contactPhone"
              label="Contact Phone"
              description="Primary phone number"
              required={true}
              size="large"
              variant="outlined"
              fieldType="tel"
              autoComplete="tel"
            >
              <SafInput
                type="tel"
                placeholder="Enter phone number"
                autoComplete="tel"
              />
            </SafFormField>
          </div>

          <SafFormField
            name="address"
            label="Business Address"
            description="Primary business or legal address"
            required={true}
            size="large"
            variant="outlined"
            fieldType="textarea"
            help="Include street address, city, state, and ZIP code"
            spellCheck={true}
          >
            <SafTextarea
              placeholder="Enter complete business address"
              rows={3}
              autoComplete="street-address"
            />
          </SafFormField>
        </div>

        {/* Legal Parameters Section */}
        <div className="form-section">
          <h2>Legal Parameters</h2>
          
          <div className="form-row">
            <SafFormField
              name="jurisdiction"
              label="Jurisdiction"
              description="Legal jurisdiction for contract disputes"
              required={true}
              size="large"
              variant="outlined"
              fieldType="select"
              help="The legal authority that will govern this contract"
              tooltip={{
                content: "Jurisdiction determines which courts have authority over disputes and which laws apply to contract interpretation.",
                position: "top"
              }}
            >
              <SafSelect
                placeholder="Select jurisdiction"
                options={[
                  { label: 'Federal Court', value: 'federal' },
                  { label: 'New York State', value: 'ny-state' },
                  { label: 'California State', value: 'ca-state' },
                  { label: 'Texas State', value: 'tx-state' },
                  { label: 'Florida State', value: 'fl-state' },
                  { label: 'Illinois State', value: 'il-state' },
                  { label: 'Other State Court', value: 'other-state' },
                  { label: 'International Arbitration', value: 'international' }
                ]}
                searchable={true}
              />
            </SafFormField>

            <SafFormField
              name="governingLaw"
              label="Governing Law"
              description="Legal framework that governs the contract"
              required={true}
              size="large"
              variant="outlined"
              fieldType="select"
              help="The specific laws that will be used to interpret the contract terms"
            >
              <SafSelect
                placeholder="Select governing law"
                options={[
                  { label: 'New York Law', value: 'ny-law' },
                  { label: 'Delaware Law', value: 'de-law' },
                  { label: 'California Law', value: 'ca-law' },
                  { label: 'Texas Law', value: 'tx-law' },
                  { label: 'Federal Law', value: 'federal-law' },
                  { label: 'International Law', value: 'international-law' }
                ]}
                searchable={true}
              />
            </SafFormField>
          </div>

          <SafFormField
            name="confidentialityLevel"
            label="Confidentiality Level"
            description="Level of confidentiality protection required"
            required={true}
            size="large"
            variant="outlined"
            fieldType="radio"
            help="Determines the scope of confidentiality obligations"
          >
            <SafRadio
              options={[
                { 
                  label: 'Standard', 
                  value: 'standard',
                  description: 'Normal confidentiality provisions'
                },
                { 
                  label: 'High', 
                  value: 'high',
                  description: 'Enhanced confidentiality protections'
                },
                { 
                  label: 'Maximum', 
                  value: 'maximum',
                  description: 'Strictest confidentiality requirements'
                },
                { 
                  label: 'Public', 
                  value: 'public',
                  description: 'No confidentiality restrictions'
                }
              ]}
              layout="vertical"
              onChange={(value) => handleFieldChange('confidentialityLevel', value)}
            />
          </SafFormField>
        </div>

        {/* Contract Specifics Section */}
        <div className="form-section">
          <h2>Contract Specifics</h2>
          
          <SafFormField
            name="contractScope"
            label="Scope of Work/Services"
            description="Detailed description of what will be provided"
            required={true}
            size="large"
            variant="outlined"
            fieldType="textarea"
            help="Be as specific as possible about deliverables, timelines, and expectations"
            spellCheck={true}
            maxLength={2000}
          >
            <SafTextarea
              placeholder="Describe the scope of work, services, or goods to be provided..."
              rows={6}
              maxLength={2000}
              showCharacterCount={true}
            />
          </SafFormField>

          <div className="form-row">
            <SafFormField
              name="contractValue"
              label="Contract Value"
              description="Total monetary value of the contract"
              size="large"
              variant="outlined"
              fieldType="number"
              help="Enter the total contract amount in USD"
              optionalIndicator="Optional"
            >
              <SafInput
                type="number"
                placeholder="0.00"
                min={0}
                step={0.01}
                prefix="$"
                suffix="USD"
              />
            </SafFormField>

            <SafFormField
              name="paymentTerms"
              label="Payment Terms"
              description="How and when payments will be made"
              size="large"
              variant="outlined"
              fieldType="select"
              help="Standard payment arrangement for this contract"
            >
              <SafSelect
                placeholder="Select payment terms"
                options={[
                  { label: 'Net 30 Days', value: 'net30' },
                  { label: 'Net 15 Days', value: 'net15' },
                  { label: 'Due on Receipt', value: 'due-receipt' },
                  { label: 'Advance Payment', value: 'advance' },
                  { label: 'Milestone-Based', value: 'milestone' },
                  { label: 'Monthly Recurring', value: 'monthly' },
                  { label: 'Quarterly', value: 'quarterly' },
                  { label: 'Upon Completion', value: 'completion' }
                ]}
              />
            </SafFormField>
          </div>

          {/* Existing Agreement Check */}
          <SafFormField
            name="hasExistingAgreement"
            label="Existing Agreement"
            description="Is this related to an existing contract?"
            size="large"
            variant="outlined"
            fieldType="checkbox"
            help="Check if this contract modifies or relates to an existing agreement"
          >
            <SafCheckbox
              label="This contract relates to or modifies an existing agreement"
              onChange={(checked) => handleFieldChange('hasExistingAgreement', checked)}
            />
          </SafFormField>

          {/* Conditional field for existing agreement details */}
          <SafFormField
            name="existingAgreementDetails"
            label="Existing Agreement Details"
            description="Provide details about the existing agreement"
            size="large"
            variant="outlined"
            conditionalLogic={existingAgreementLogic}
            fieldType="textarea"
            help="Include agreement title, date, and how this contract relates to it"
            spellCheck={true}
          >
            <SafTextarea
              placeholder="Describe the existing agreement and how this contract relates to it..."
              rows={4}
              maxLength={1000}
              showCharacterCount={true}
            />
          </SafFormField>
        </div>

        {/* Additional Requirements Section */}
        <div className="form-section">
          <h2>Additional Requirements</h2>
          
          <SafFormField
            name="specialClauses"
            label="Special Clauses or Requirements"
            description="Any additional legal provisions needed"
            size="large"
            variant="outlined"
            fieldType="textarea"
            help="Describe any specific clauses, terms, or legal requirements unique to this contract"
            optionalIndicator="Optional"
            spellCheck={true}
            maxLength={1500}
          >
            <SafTextarea
              placeholder="Describe any special clauses, requirements, or unique terms..."
              rows={5}
              maxLength={1500}
              showCharacterCount={true}
            />
          </SafFormField>

          <SafFormField
            name="supportingDocuments"
            label="Supporting Documents"
            description="Upload any relevant documents"
            size="large"
            variant="outlined"
            fieldType="file"
            help="Include any existing agreements, specifications, or reference materials"
            optionalIndicator="Optional"
          >
            <SafFileUpload
              accept=".pdf,.doc,.docx,.txt"
              multiple={true}
              maxFiles={10}
              maxSize="10MB"
              placeholder="Drop files here or click to upload"
              showFileList={true}
            />
          </SafFormField>

          <SafFormField
            name="reviewerNotifications"
            label="Legal Review Notifications"
            description="Who should be notified during the review process?"
            size="large"
            variant="outlined"
            fieldType="textarea"
            help="Provide email addresses of stakeholders who should receive updates"
            optionalIndicator="Optional"
            spellCheck={false}
          >
            <SafTextarea
              placeholder="Enter email addresses separated by commas..."
              rows={3}
            />
          </SafFormField>
        </div>

        {/* Agreement and Submission */}
        <div className="form-section">
          <h2>Review and Submit</h2>
          
          <SafFormField
            name="agreedToTerms"
            label="Legal Agreement"
            required={true}
            size="large"
            variant="outlined"
            fieldType="checkbox"
            help="Required to proceed with contract generation"
            error={fieldStates.agreedToTerms?.error}
          >
            <SafCheckbox
              label="I agree to the Terms of Service and Legal Representation Agreement"
              description={
                <span>
                  I understand that this contract generation service constitutes legal advice and agree to the{' '}
                  <a href="/terms" target="_blank" rel="noopener noreferrer">
                    Terms of Service
                  </a>{' '}
                  and{' '}
                  <a href="/legal-representation" target="_blank" rel="noopener noreferrer">
                    Legal Representation Agreement
                  </a>
                </span>
              }
            />
          </SafFormField>

          <SafFormField
            name="urgentReview"
            label="Request Urgent Review"
            size="large"
            variant="outlined"
            fieldType="checkbox"
            help="Additional fees may apply for expedited service"
            optionalIndicator="Optional"
          >
            <SafCheckbox
              label="Request urgent legal review (additional fees apply)"
              description="Expedited review within 24-48 hours instead of standard 5-7 business days"
            />
          </SafFormField>

          <div className="form-actions">
            <SafButton
              type="button"
              variant="secondary"
              size="large"
              icon="save"
            >
              Save as Draft
            </SafButton>
            
            <SafButton
              type="submit"
              variant="primary"
              size="large"
              icon="send"
            >
              Submit for Legal Review
            </SafButton>
          </div>
        </div>
      </div>

      {/* Form Progress Summary */}
      <div className="form-progress-summary">
        <h3>Form Completion Status</h3>
        <div className="field-summary">
          {Object.entries(fieldStates).map(([fieldName, state]) => (
            <div key={fieldName} className={`field-status ${state.valid ? 'valid' : state.error ? 'error' : 'pending'}`}>
              <span className="field-name">{fieldName}</span>
              <span className="field-state">
                {state.valid ? '✓' : state.error ? '✗' : '○'}
              </span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-contract-form-fields.component.ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-legal-contract-form-fields',
  template: `
    <div class="legal-contract-form-demo">
      <h1>Legal Contract Information Form</h1>
      <p>Complete the following fields to generate your legal contract documentation.</p>

      <div class="form-sections">
        <!-- Contract Basics Section -->
        <div class="form-section">
          <h2>Contract Basics</h2>
          
          <div class="form-row">
            <saf-form-field
              name="contractType"
              label="Contract Type"
              description="Select the type of legal contract you need"
              [required]="true"
              size="large"
              variant="outlined"
              help="Choose the contract category that best fits your legal needs"
              helpPosition="tooltip"
              [tooltip]="contractTypeTooltip"
              fieldType="select"
              validationTrigger="onChange"
              [showValidationIcon]="true"
              (valueChange)="handleFieldChange('contractType', $event)"
              (validationChange)="handleValidationChange('contractType', $event)">
              
              <saf-select
                placeholder="Select contract type"
                [options]="contractTypeOptions"
                [searchable]="true"
                groupBy="category">
              </saf-select>
            </saf-form-field>

            <saf-form-field
              name="urgency"
              label="Project Urgency"
              description="Timeline for contract completion"
              size="large"
              variant="outlined"
              fieldType="radio">
              
              <saf-radio
                [options]="urgencyOptions"
                layout="horizontal">
              </saf-radio>
            </saf-form-field>
          </div>

          <saf-form-field
            name="contractTitle"
            label="Contract Title"
            description="Descriptive title for your contract"
            [required]="true"
            size="large"
            variant="outlined"
            help="Provide a clear, descriptive title that identifies the purpose of this contract"
            [maxLength]="100"
            fieldType="text"
            autoComplete="off"
            [spellCheck]="true">
            
            <saf-input
              placeholder="e.g., Software Development Services Agreement"
              [maxLength]="100"
              [showCharacterCount]="true">
            </saf-input>
          </saf-form-field>

          <div class="form-row">
            <saf-form-field
              name="effectiveDate"
              label="Effective Date"
              description="When the contract becomes active"
              [required]="true"
              size="large"
              variant="outlined"
              fieldType="date"
              help="The date when contractual obligations begin">
              
              <saf-date-picker
                placeholder="Select effective date"
                [minDate]="today"
                [showTodayButton]="true"
                format="MMMM d, yyyy">
              </saf-date-picker>
            </saf-form-field>

            <saf-form-field
              name="expirationDate"
              label="Expiration Date"
              description="When the contract ends (optional)"
              size="large"
              variant="outlined"
              fieldType="date"
              help="Leave blank for indefinite duration contracts"
              optionalIndicator="Optional">
              
              <saf-date-picker
                placeholder="Select expiration date (optional)"
                [minDate]="formData.effectiveDate"
                format="MMMM d, yyyy"
                [clearable]="true">
              </saf-date-picker>
            </saf-form-field>
          </div>
        </div>

        <!-- Parties Information Section -->
        <div class="form-section">
          <h2>Contracting Parties</h2>
          
          <saf-form-field
            name="clientType"
            label="Client Type"
            description="Type of contracting entity"
            [required]="true"
            size="large"
            variant="outlined"
            fieldType="radio"
            help="This determines which additional information fields will be required">
            
            <saf-radio
              [options]="clientTypeOptions"
              layout="horizontal"
              (change)="handleFieldChange('clientType', $event)">
            </saf-radio>
          </saf-form-field>

          <div class="form-row">
            <saf-form-field
              name="firstName"
              label="First Name"
              [required]="formData.clientType === 'individual'"
              size="large"
              variant="outlined"
              [hidden]="formData.clientType !== 'individual'"
              fieldType="text"
              autoComplete="given-name"
              [spellCheck]="false">
              
              <saf-input
                placeholder="Enter first name"
                autoComplete="given-name">
              </saf-input>
            </saf-form-field>

            <saf-form-field
              name="lastName"
              label="Last Name"
              [required]="formData.clientType === 'individual'"
              size="large"
              variant="outlined"
              [hidden]="formData.clientType !== 'individual'"
              fieldType="text"
              autoComplete="family-name"
              [spellCheck]="false">
              
              <saf-input
                placeholder="Enter last name"
                autoComplete="family-name">
              </saf-input>
            </saf-form-field>
          </div>

          <!-- Corporate Fields - Conditional -->
          <saf-form-field
            name="companyName"
            label="Company/Organization Name"
            [required]="formData.clientType !== 'individual'"
            size="large"
            variant="outlined"
            [conditionalLogic]="corporateConditionalLogic"
            fieldType="text"
            autoComplete="organization"
            [spellCheck]="true"
            help="Legal name of the organization as it appears in official documents">
            
            <saf-input
              placeholder="Enter company or organization name"
              autoComplete="organization">
            </saf-input>
          </saf-form-field>

          <div class="form-row">
            <saf-form-field
              name="contactEmail"
              label="Contact Email"
              description="Primary email for contract communications"
              [required]="true"
              size="large"
              variant="outlined"
              fieldType="email"
              autoComplete="email"
              help="This email will receive all contract-related communications"
              validationTrigger="onBlur"
              [validationDelay]="500">
              
              <saf-input
                type="email"
                placeholder="Enter email address"
                autoComplete="email">
              </saf-input>
            </saf-form-field>

            <saf-form-field
              name="contactPhone"
              label="Contact Phone"
              description="Primary phone number"
              [required]="true"
              size="large"
              variant="outlined"
              fieldType="tel"
              autoComplete="tel">
              
              <saf-input
                type="tel"
                placeholder="Enter phone number"
                autoComplete="tel">
              </saf-input>
            </saf-form-field>
          </div>
        </div>

        <!-- Legal Parameters Section -->
        <div class="form-section">
          <h2>Legal Parameters</h2>
          
          <div class="form-row">
            <saf-form-field
              name="jurisdiction"
              label="Jurisdiction"
              description="Legal jurisdiction for contract disputes"
              [required]="true"
              size="large"
              variant="outlined"
              fieldType="select"
              help="The legal authority that will govern this contract"
              [tooltip]="jurisdictionTooltip">
              
              <saf-select
                placeholder="Select jurisdiction"
                [options]="jurisdictionOptions"
                [searchable]="true">
              </saf-select>
            </saf-form-field>

            <saf-form-field
              name="governingLaw"
              label="Governing Law"
              description="Legal framework that governs the contract"
              [required]="true"
              size="large"
              variant="outlined"
              fieldType="select"
              help="The specific laws that will be used to interpret the contract terms">
              
              <saf-select
                placeholder="Select governing law"
                [options]="governingLawOptions"
                [searchable]="true">
              </saf-select>
            </saf-form-field>
          </div>
        </div>

        <!-- Agreement and Submission -->
        <div class="form-section">
          <h2>Review and Submit</h2>
          
          <saf-form-field
            name="agreedToTerms"
            label="Legal Agreement"
            [required]="true"
            size="large"
            variant="outlined"
            fieldType="checkbox"
            help="Required to proceed with contract generation"
            [error]="fieldStates.agreedToTerms?.error">
            
            <saf-checkbox
              label="I agree to the Terms of Service and Legal Representation Agreement"
              [description]="termsDescription">
            </saf-checkbox>
          </saf-form-field>

          <div class="form-actions">
            <saf-button
              type="button"
              variant="secondary"
              size="large"
              icon="save">
              Save as Draft
            </saf-button>
            
            <saf-button
              type="submit"
              variant="primary"
              size="large"
              icon="send">
              Submit for Legal Review
            </saf-button>
          </div>
        </div>
      </div>
    </div>
  `
})
export class LegalContractFormFieldsComponent implements OnInit {
  formData: any = {
    clientType: 'individual',
    confidentialityLevel: 'standard'
  };
  
  fieldStates: any = {};
  today = new Date();

  contractTypeTooltip = {
    content: "Contract types determine the specific legal framework and clauses that will be included in your agreement.",
    position: "right",
    maxWidth: "300px"
  };

  jurisdictionTooltip = {
    content: "Jurisdiction determines which courts have authority over disputes and which laws apply to contract interpretation.",
    position: "top"
  };

  corporateConditionalLogic = {
    condition: (formData: any) => formData.clientType === 'corporate',
    action: 'show',
    trigger: ['clientType']
  };

  contractTypeOptions = [
    { 
      label: 'Service Agreement', 
      value: 'service',
      description: 'Professional services contract'
    },
    { 
      label: 'Employment Contract', 
      value: 'employment',
      description: 'Employee hiring agreement'
    },
    { 
      label: 'Non-Disclosure Agreement (NDA)', 
      value: 'nda',
      description: 'Confidentiality protection'
    }
  ];

  urgencyOptions = [
    { 
      label: 'Standard (2-3 weeks)', 
      value: 'standard',
      description: 'Normal processing timeline'
    },
    { 
      label: 'Expedited (1 week)', 
      value: 'expedited',
      description: 'Faster turnaround time'
    },
    { 
      label: 'Rush (2-3 days)', 
      value: 'rush',
      description: 'Priority processing'
    }
  ];

  clientTypeOptions = [
    { 
      label: 'Individual', 
      value: 'individual',
      description: 'Personal contract'
    },
    { 
      label: 'Corporation', 
      value: 'corporate',
      description: 'Business entity'
    },
    { 
      label: 'Partnership', 
      value: 'partnership',
      description: 'Partnership entity'
    }
  ];

  jurisdictionOptions = [
    { label: 'Federal Court', value: 'federal' },
    { label: 'New York State', value: 'ny-state' },
    { label: 'California State', value: 'ca-state' },
    { label: 'Texas State', value: 'tx-state' }
  ];

  governingLawOptions = [
    { label: 'New York Law', value: 'ny-law' },
    { label: 'Delaware Law', value: 'de-law' },
    { label: 'California Law', value: 'ca-law' },
    { label: 'Federal Law', value: 'federal-law' }
  ];

  termsDescription = 'I have read and agree to the Terms of Service and Legal Representation Agreement';

  ngOnInit() {
    // Initialize form
  }

  handleFieldChange(fieldName: string, value: any) {
    this.formData = {
      ...this.formData,
      [fieldName]: value
    };
  }

  handleValidationChange(fieldName: string, validationState: any) {
    this.fieldStates = {
      ...this.fieldStates,
      [fieldName]: validationState
    };
  }
}
```

## Best Practices

1. **Field Design**
   - Use clear, descriptive labels
   - Provide helpful descriptions and examples
   - Group related fields logically
   - Include appropriate input types and validation

2. **Validation**
   - Validate on appropriate triggers (blur, change, submit)
   - Provide immediate, clear feedback
   - Use field dependencies for complex validation
   - Show validation state visually

3. **User Experience**
   - Use conditional logic to show/hide relevant fields
   - Provide help text and tooltips for complex fields
   - Implement progressive disclosure for long forms
   - Show completion progress

4. **Accessibility**
   - Use proper ARIA labels and descriptions
   - Ensure keyboard navigation works correctly
   - Provide clear error messages
   - Support screen readers with proper markup

5. **Performance**
   - Debounce validation for better performance
   - Lazy load field options when needed
   - Optimize re-renders with proper memoization
   - Use virtual scrolling for large option lists

## Accessibility Considerations

1. **Screen Reader Support**
   - Proper field labels and descriptions
   - Error message announcements
   - Validation state changes
   - Help text association

2. **Keyboard Navigation**
   - Tab order management
   - Field focus handling
   - Keyboard shortcuts for actions
   - Arrow key navigation in radio groups

3. **Visual Accessibility**
   - High contrast mode support
   - Clear error indicators
   - Sufficient color contrast
   - Scalable text and interface elements

4. **Motor Accessibility**
   - Large click targets
   - Touch-friendly interactions
   - Voice input support
   - Reduced motion options

## Related Components

- **SafForm**: Parent form container
- **SafInput**: Text input component
- **SafSelect**: Dropdown selection component
- **SafTextarea**: Multi-line text input
- **SafCheckbox**: Checkbox input component

## Notes

- Form field supports complex conditional logic and dependencies
- Validation can be synchronous or asynchronous with proper debouncing
- Integration with form libraries like React Hook Form and Angular Reactive Forms
- Comprehensive accessibility support with ARIA attributes
- Mobile-responsive design with touch-friendly interactions
- Legal industry-specific validation patterns and field types
- Real-time validation feedback with visual indicators
- Support for custom validation rules and error messages
- Field state management with proper cleanup and optimization
