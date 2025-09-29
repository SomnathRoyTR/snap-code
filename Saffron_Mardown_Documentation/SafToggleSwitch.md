# SafToggleSwitch Component

## Overview

SafToggleSwitch is a binary control component that allows users to switch between two states (on/off, enabled/disabled, active/inactive). It provides an intuitive toggle interaction with smooth animations, customizable labels, validation support, and accessibility features. SafToggleSwitch is ideal for settings, preferences, feature toggles, and any scenario requiring binary state management.

## React API

### SafToggleSwitch

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `checked` | `boolean` | No | `false` | Whether the switch is checked/on |
| `defaultChecked` | `boolean` | No | `false` | Default checked state for uncontrolled usage |
| `disabled` | `boolean` | No | `false` | Whether the switch is disabled |
| `required` | `boolean` | No | `false` | Whether the switch is required |
| `readOnly` | `boolean` | No | `false` | Whether the switch is read-only |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the switch |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | No | `'primary'` | Color theme of the switch |
| `label` | `string \| ReactNode` | No | - | Label text for the switch |
| `labelPlacement` | `'start' \| 'end' \| 'top' \| 'bottom'` | No | `'end'` | Position of the label relative to switch |
| `description` | `string \| ReactNode` | No | - | Additional descriptive text |
| `error` | `string \| boolean` | No | `false` | Error state and message |
| `helperText` | `string \| ReactNode` | No | - | Helper text below the switch |
| `name` | `string` | No | - | Name attribute for form submission |
| `value` | `string` | No | - | Value attribute for form submission |
| `tabIndex` | `number` | No | `0` | Tab index for keyboard navigation |
| `autoFocus` | `boolean` | No | `false` | Whether to auto-focus the switch |
| `loading` | `boolean` | No | `false` | Whether to show loading state |
| `icon` | `ReactNode` | No | - | Custom icon for the switch thumb |
| `checkedIcon` | `ReactNode` | No | - | Icon when switch is checked |
| `uncheckedIcon` | `ReactNode` | No | - | Icon when switch is unchecked |
| `onChange` | `(checked: boolean, event: ChangeEvent) => void` | No | - | Callback when switch state changes |
| `onFocus` | `(event: FocusEvent) => void` | No | - | Callback when switch gains focus |
| `onBlur` | `(event: FocusEvent) => void` | No | - | Callback when switch loses focus |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

## Angular API

### saf-toggle-switch

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[checked]` | `boolean` | No | `false` | Whether the switch is checked/on |
| `[disabled]` | `boolean` | No | `false` | Whether the switch is disabled |
| `[required]` | `boolean` | No | `false` | Whether the switch is required |
| `[readonly]` | `boolean` | No | `false` | Whether the switch is read-only |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the switch |
| `[color]` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | No | `'primary'` | Color theme of the switch |
| `[label]` | `string \| TemplateRef` | No | - | Label text for the switch |
| `[labelPlacement]` | `'start' \| 'end' \| 'top' \| 'bottom'` | No | `'end'` | Position of the label relative to switch |
| `[description]` | `string \| TemplateRef` | No | - | Additional descriptive text |
| `[error]` | `string \| boolean` | No | `false` | Error state and message |
| `[helperText]` | `string \| TemplateRef` | No | - | Helper text below the switch |
| `[name]` | `string` | No | - | Name attribute for form submission |
| `[value]` | `string` | No | - | Value attribute for form submission |
| `[tabIndex]` | `number` | No | `0` | Tab index for keyboard navigation |
| `[loading]` | `boolean` | No | `false` | Whether to show loading state |
| `[checkedIcon]` | `string \| TemplateRef` | No | - | Icon when switch is checked |
| `[uncheckedIcon]` | `string \| TemplateRef` | No | - | Icon when switch is unchecked |
| `(checkedChange)` | `EventEmitter<boolean>` | No | - | Event when switch state changes |
| `(focus)` | `EventEmitter<FocusEvent>` | No | - | Event when switch gains focus |
| `(blur)` | `EventEmitter<FocusEvent>` | No | - | Event when switch loses focus |

## Usage Examples

### Basic Toggle Switches

#### React
```jsx
import { SafToggleSwitch, SafCard, SafIcon } from '@saffron/react';
import { useState } from 'react';

const BasicToggleSwitchExample = () => {
  const [notificationsEnabled, setNotificationsEnabled] = useState(true);
  const [darkModeEnabled, setDarkModeEnabled] = useState(false);
  const [autoSaveEnabled, setAutoSaveEnabled] = useState(true);
  const [bluetoothEnabled, setBluetoothEnabled] = useState(false);

  return (
    <SafCard className="toggle-switch-demo">
      <SafCard.Header>
        <h2>Settings</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="settings-group">
          <SafToggleSwitch
            checked={notificationsEnabled}
            onChange={setNotificationsEnabled}
            label="Enable Notifications"
            description="Receive alerts and updates"
            color="primary"
          />

          <SafToggleSwitch
            checked={darkModeEnabled}
            onChange={setDarkModeEnabled}
            label="Dark Mode"
            description="Switch to dark theme"
            color="secondary"
            checkedIcon={<SafIcon name="moon" />}
            uncheckedIcon={<SafIcon name="sun" />}
          />

          <SafToggleSwitch
            checked={autoSaveEnabled}
            onChange={setAutoSaveEnabled}
            label="Auto Save"
            description="Automatically save your work"
            color="success"
            size="large"
          />

          <SafToggleSwitch
            checked={bluetoothEnabled}
            onChange={setBluetoothEnabled}
            label="Bluetooth"
            description="Enable wireless connectivity"
            color="primary"
            size="small"
            disabled={false}
          />
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// basic-toggle-switch.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-toggle-switch',
  template: `
    <saf-card class="toggle-switch-demo">
      <saf-card-header>
        <h2>Settings</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="settings-group">
          <saf-toggle-switch
            [checked]="notificationsEnabled"
            (checkedChange)="notificationsEnabled = $event"
            label="Enable Notifications"
            description="Receive alerts and updates"
            color="primary">
          </saf-toggle-switch>

          <saf-toggle-switch
            [checked]="darkModeEnabled"
            (checkedChange)="darkModeEnabled = $event"
            label="Dark Mode"
            description="Switch to dark theme"
            color="secondary"
            checkedIcon="moon"
            uncheckedIcon="sun">
          </saf-toggle-switch>

          <saf-toggle-switch
            [checked]="autoSaveEnabled"
            (checkedChange)="autoSaveEnabled = $event"
            label="Auto Save"
            description="Automatically save your work"
            color="success"
            size="large">
          </saf-toggle-switch>

          <saf-toggle-switch
            [checked]="bluetoothEnabled"
            (checkedChange)="bluetoothEnabled = $event"
            label="Bluetooth"
            description="Enable wireless connectivity"
            color="primary"
            size="small"
            [disabled]="false">
          </saf-toggle-switch>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class BasicToggleSwitchComponent {
  notificationsEnabled = true;
  darkModeEnabled = false;
  autoSaveEnabled = true;
  bluetoothEnabled = false;
}
```

### Form Integration with Validation

#### React
```jsx
import { SafToggleSwitch, SafCard, SafButton, SafAlert } from '@saffron/react';
import { useState } from 'react';

const FormToggleSwitchExample = () => {
  const [formData, setFormData] = useState({
    termsAccepted: false,
    newsletterSubscription: true,
    dataProcessing: false,
    marketingEmails: false,
    twoFactorAuth: true
  });

  const [errors, setErrors] = useState({});
  const [submitted, setSubmitted] = useState(false);

  const handleToggleChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }));

    // Clear error when user interacts
    if (errors[field]) {
      setErrors(prev => ({
        ...prev,
        [field]: null
      }));
    }
  };

  const validateForm = () => {
    const newErrors = {};

    if (!formData.termsAccepted) {
      newErrors.termsAccepted = 'You must accept the terms and conditions';
    }

    if (!formData.dataProcessing) {
      newErrors.dataProcessing = 'Data processing consent is required';
    }

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleSubmit = () => {
    setSubmitted(true);
    if (validateForm()) {
      console.log('Form submitted:', formData);
      alert('Preferences saved successfully!');
    }
  };

  return (
    <SafCard className="form-toggle-demo">
      <SafCard.Header>
        <h2>Privacy & Communication Preferences</h2>
      </SafCard.Header>
      <SafCard.Content>
        <form className="preferences-form">
          <div className="form-section">
            <h3>Required Consents</h3>
            
            <SafToggleSwitch
              checked={formData.termsAccepted}
              onChange={(value) => handleToggleChange('termsAccepted', value)}
              label="Accept Terms and Conditions"
              description="I agree to the Terms of Service and Privacy Policy"
              required={true}
              color={errors.termsAccepted ? 'error' : 'primary'}
              error={errors.termsAccepted}
              size="large"
            />

            <SafToggleSwitch
              checked={formData.dataProcessing}
              onChange={(value) => handleToggleChange('dataProcessing', value)}
              label="Data Processing Consent"
              description="Allow processing of personal data for service provision"
              required={true}
              color={errors.dataProcessing ? 'error' : 'success'}
              error={errors.dataProcessing}
            />
          </div>

          <div className="form-section">
            <h3>Optional Preferences</h3>
            
            <SafToggleSwitch
              checked={formData.newsletterSubscription}
              onChange={(value) => handleToggleChange('newsletterSubscription', value)}
              label="Newsletter Subscription"
              description="Receive our monthly newsletter with updates and tips"
              color="primary"
              helperText="You can unsubscribe at any time"
            />

            <SafToggleSwitch
              checked={formData.marketingEmails}
              onChange={(value) => handleToggleChange('marketingEmails', value)}
              label="Marketing Communications"
              description="Receive promotional offers and product announcements"
              color="warning"
            />
          </div>

          <div className="form-section">
            <h3>Security Settings</h3>
            
            <SafToggleSwitch
              checked={formData.twoFactorAuth}
              onChange={(value) => handleToggleChange('twoFactorAuth', value)}
              label="Two-Factor Authentication"
              description="Add an extra layer of security to your account"
              color="success"
              helperText="Recommended for enhanced security"
              checkedIcon="shield-check"
              uncheckedIcon="shield"
            />
          </div>

          {submitted && Object.keys(errors).length > 0 && (
            <SafAlert variant="error" className="form-errors">
              Please correct the errors above before submitting.
            </SafAlert>
          )}

          <div className="form-actions">
            <SafButton 
              variant="primary" 
              onClick={handleSubmit}
              disabled={Object.keys(errors).length > 0}
            >
              Save Preferences
            </SafButton>
          </div>
        </form>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// form-toggle-switch.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-form-toggle-switch',
  template: `
    <saf-card class="form-toggle-demo">
      <saf-card-header>
        <h2>Privacy & Communication Preferences</h2>
      </saf-card-header>
      <saf-card-content>
        <form class="preferences-form" #form="ngForm">
          <div class="form-section">
            <h3>Required Consents</h3>
            
            <saf-toggle-switch
              [checked]="formData.termsAccepted"
              (checkedChange)="handleToggleChange('termsAccepted', $event)"
              label="Accept Terms and Conditions"
              description="I agree to the Terms of Service and Privacy Policy"
              [required]="true"
              [color]="getFieldColor('termsAccepted')"
              [error]="getFieldError('termsAccepted')"
              size="large">
            </saf-toggle-switch>

            <saf-toggle-switch
              [checked]="formData.dataProcessing"
              (checkedChange)="handleToggleChange('dataProcessing', $event)"
              label="Data Processing Consent"
              description="Allow processing of personal data for service provision"
              [required]="true"
              [color]="getFieldColor('dataProcessing')"
              [error]="getFieldError('dataProcessing')">
            </saf-toggle-switch>
          </div>

          <div class="form-section">
            <h3>Optional Preferences</h3>
            
            <saf-toggle-switch
              [checked]="formData.newsletterSubscription"
              (checkedChange)="handleToggleChange('newsletterSubscription', $event)"
              label="Newsletter Subscription"
              description="Receive our monthly newsletter with updates and tips"
              color="primary"
              helperText="You can unsubscribe at any time">
            </saf-toggle-switch>

            <saf-toggle-switch
              [checked]="formData.marketingEmails"
              (checkedChange)="handleToggleChange('marketingEmails', $event)"
              label="Marketing Communications"
              description="Receive promotional offers and product announcements"
              color="warning">
            </saf-toggle-switch>
          </div>

          <div class="form-section">
            <h3>Security Settings</h3>
            
            <saf-toggle-switch
              [checked]="formData.twoFactorAuth"
              (checkedChange)="handleToggleChange('twoFactorAuth', $event)"
              label="Two-Factor Authentication"
              description="Add an extra layer of security to your account"
              color="success"
              helperText="Recommended for enhanced security"
              checkedIcon="shield-check"
              uncheckedIcon="shield">
            </saf-toggle-switch>
          </div>

          <saf-alert 
            *ngIf="submitted && hasErrors()" 
            variant="error" 
            class="form-errors">
            Please correct the errors above before submitting.
          </saf-alert>

          <div class="form-actions">
            <saf-button 
              variant="primary" 
              (click)="handleSubmit()"
              [disabled]="hasErrors()">
              Save Preferences
            </saf-button>
          </div>
        </form>
      </saf-card-content>
    </saf-card>
  `
})
export class FormToggleSwitchComponent {
  formData = {
    termsAccepted: false,
    newsletterSubscription: true,
    dataProcessing: false,
    marketingEmails: false,
    twoFactorAuth: true
  };

  errors: { [key: string]: string } = {};
  submitted = false;

  handleToggleChange(field: string, value: boolean) {
    this.formData = {
      ...this.formData,
      [field]: value
    };

    // Clear error when user interacts
    if (this.errors[field]) {
      delete this.errors[field];
    }
  }

  validateForm(): boolean {
    this.errors = {};

    if (!this.formData.termsAccepted) {
      this.errors['termsAccepted'] = 'You must accept the terms and conditions';
    }

    if (!this.formData.dataProcessing) {
      this.errors['dataProcessing'] = 'Data processing consent is required';
    }

    return Object.keys(this.errors).length === 0;
  }

  handleSubmit() {
    this.submitted = true;
    if (this.validateForm()) {
      console.log('Form submitted:', this.formData);
      alert('Preferences saved successfully!');
    }
  }

  getFieldError(field: string): string {
    return this.errors[field] || '';
  }

  getFieldColor(field: string): string {
    return this.errors[field] ? 'error' : field === 'dataProcessing' ? 'success' : 'primary';
  }

  hasErrors(): boolean {
    return Object.keys(this.errors).length > 0;
  }
}
```

### Feature Toggles Dashboard

#### React
```jsx
import { SafToggleSwitch, SafCard, SafBadge, SafButton, SafIcon } from '@saffron/react';
import { useState } from 'react';

const FeatureTogglesDashboardExample = () => {
  const [features, setFeatures] = useState({
    newDashboard: { enabled: true, rollout: 85 },
    betaSearch: { enabled: false, rollout: 25 },
    advancedFilters: { enabled: true, rollout: 100 },
    realTimeSync: { enabled: false, rollout: 10 },
    mobileApp: { enabled: true, rollout: 75 },
    analyticsV2: { enabled: false, rollout: 0 }
  });

  const [loading, setLoading] = useState({});

  const handleFeatureToggle = async (featureKey, enabled) => {
    setLoading(prev => ({ ...prev, [featureKey]: true }));
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    setFeatures(prev => ({
      ...prev,
      [featureKey]: {
        ...prev[featureKey],
        enabled
      }
    }));
    
    setLoading(prev => ({ ...prev, [featureKey]: false }));
  };

  const getRolloutBadgeVariant = (rollout) => {
    if (rollout === 0) return 'secondary';
    if (rollout < 50) return 'warning';
    if (rollout < 100) return 'primary';
    return 'success';
  };

  const featureList = [
    {
      key: 'newDashboard',
      title: 'New Dashboard',
      description: 'Enhanced user interface with improved navigation',
      category: 'UI/UX',
      impact: 'High'
    },
    {
      key: 'betaSearch',
      title: 'Beta Search Engine',
      description: 'AI-powered search with natural language processing',
      category: 'Search',
      impact: 'High'
    },
    {
      key: 'advancedFilters',
      title: 'Advanced Filters',
      description: 'Complex filtering options for power users',
      category: 'Functionality',
      impact: 'Medium'
    },
    {
      key: 'realTimeSync',
      title: 'Real-time Sync',
      description: 'Live data synchronization across devices',
      category: 'Performance',
      impact: 'Medium'
    },
    {
      key: 'mobileApp',
      title: 'Mobile App Integration',
      description: 'Seamless mobile application experience',
      category: 'Mobile',
      impact: 'High'
    },
    {
      key: 'analyticsV2',
      title: 'Analytics v2',
      description: 'Advanced analytics and reporting dashboard',
      category: 'Analytics',
      impact: 'Low'
    }
  ];

  return (
    <SafCard className="feature-toggles-dashboard">
      <SafCard.Header>
        <h2>Feature Toggles Dashboard</h2>
        <div className="dashboard-actions">
          <SafButton variant="outline" size="small">
            <SafIcon name="download" />
            Export Config
          </SafButton>
          <SafButton variant="primary" size="small">
            <SafIcon name="save" />
            Save Changes
          </SafButton>
        </div>
      </SafCard.Header>
      <SafCard.Content>
        <div className="features-grid">
          {featureList.map((feature) => (
            <div key={feature.key} className="feature-item">
              <div className="feature-header">
                <div className="feature-info">
                  <h3>{feature.title}</h3>
                  <p className="feature-description">{feature.description}</p>
                </div>
                <SafToggleSwitch
                  checked={features[feature.key].enabled}
                  onChange={(enabled) => handleFeatureToggle(feature.key, enabled)}
                  loading={loading[feature.key]}
                  color="success"
                  size="large"
                />
              </div>
              
              <div className="feature-metadata">
                <div className="feature-tags">
                  <SafBadge variant="secondary" size="small">
                    {feature.category}
                  </SafBadge>
                  <SafBadge 
                    variant={feature.impact === 'High' ? 'error' : feature.impact === 'Medium' ? 'warning' : 'success'} 
                    size="small"
                  >
                    {feature.impact} Impact
                  </SafBadge>
                </div>
                
                <div className="rollout-info">
                  <span className="rollout-label">Rollout:</span>
                  <SafBadge variant={getRolloutBadgeVariant(features[feature.key].rollout)}>
                    {features[feature.key].rollout}%
                  </SafBadge>
                </div>
              </div>
              
              <div className="feature-status">
                <SafIcon 
                  name={features[feature.key].enabled ? 'check-circle' : 'x-circle'}
                  color={features[feature.key].enabled ? 'success' : 'error'}
                />
                <span className={`status-text ${features[feature.key].enabled ? 'enabled' : 'disabled'}`}>
                  {features[feature.key].enabled ? 'Enabled' : 'Disabled'}
                </span>
              </div>
            </div>
          ))}
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// feature-toggles-dashboard.component.ts
import { Component } from '@angular/core';

interface FeatureState {
  enabled: boolean;
  rollout: number;
}

interface Feature {
  key: string;
  title: string;
  description: string;
  category: string;
  impact: string;
}

@Component({
  selector: 'app-feature-toggles-dashboard',
  template: `
    <saf-card class="feature-toggles-dashboard">
      <saf-card-header>
        <h2>Feature Toggles Dashboard</h2>
        <div class="dashboard-actions">
          <saf-button variant="outline" size="small">
            <saf-icon name="download"></saf-icon>
            Export Config
          </saf-button>
          <saf-button variant="primary" size="small">
            <saf-icon name="save"></saf-icon>
            Save Changes
          </saf-button>
        </div>
      </saf-card-header>
      <saf-card-content>
        <div class="features-grid">
          <div *ngFor="let feature of featureList" class="feature-item">
            <div class="feature-header">
              <div class="feature-info">
                <h3>{{ feature.title }}</h3>
                <p class="feature-description">{{ feature.description }}</p>
              </div>
              <saf-toggle-switch
                [checked]="features[feature.key].enabled"
                (checkedChange)="handleFeatureToggle(feature.key, $event)"
                [loading]="loading[feature.key]"
                color="success"
                size="large">
              </saf-toggle-switch>
            </div>
            
            <div class="feature-metadata">
              <div class="feature-tags">
                <saf-badge variant="secondary" size="small">
                  {{ feature.category }}
                </saf-badge>
                <saf-badge [variant]="getImpactVariant(feature.impact)" size="small">
                  {{ feature.impact }} Impact
                </saf-badge>
              </div>
              
              <div class="rollout-info">
                <span class="rollout-label">Rollout:</span>
                <saf-badge [variant]="getRolloutBadgeVariant(features[feature.key].rollout)">
                  {{ features[feature.key].rollout }}%
                </saf-badge>
              </div>
            </div>
            
            <div class="feature-status">
              <saf-icon 
                [name]="features[feature.key].enabled ? 'check-circle' : 'x-circle'"
                [color]="features[feature.key].enabled ? 'success' : 'error'">
              </saf-icon>
              <span 
                class="status-text"
                [class.enabled]="features[feature.key].enabled"
                [class.disabled]="!features[feature.key].enabled">
                {{ features[feature.key].enabled ? 'Enabled' : 'Disabled' }}
              </span>
            </div>
          </div>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class FeatureTogglesDashboardComponent {
  features: { [key: string]: FeatureState } = {
    newDashboard: { enabled: true, rollout: 85 },
    betaSearch: { enabled: false, rollout: 25 },
    advancedFilters: { enabled: true, rollout: 100 },
    realTimeSync: { enabled: false, rollout: 10 },
    mobileApp: { enabled: true, rollout: 75 },
    analyticsV2: { enabled: false, rollout: 0 }
  };

  loading: { [key: string]: boolean } = {};

  featureList: Feature[] = [
    {
      key: 'newDashboard',
      title: 'New Dashboard',
      description: 'Enhanced user interface with improved navigation',
      category: 'UI/UX',
      impact: 'High'
    },
    {
      key: 'betaSearch',
      title: 'Beta Search Engine',
      description: 'AI-powered search with natural language processing',
      category: 'Search',
      impact: 'High'
    },
    {
      key: 'advancedFilters',
      title: 'Advanced Filters',
      description: 'Complex filtering options for power users',
      category: 'Functionality',
      impact: 'Medium'
    },
    {
      key: 'realTimeSync',
      title: 'Real-time Sync',
      description: 'Live data synchronization across devices',
      category: 'Performance',
      impact: 'Medium'
    },
    {
      key: 'mobileApp',
      title: 'Mobile App Integration',
      description: 'Seamless mobile application experience',
      category: 'Mobile',
      impact: 'High'
    },
    {
      key: 'analyticsV2',
      title: 'Analytics v2',
      description: 'Advanced analytics and reporting dashboard',
      category: 'Analytics',
      impact: 'Low'
    }
  ];

  async handleFeatureToggle(featureKey: string, enabled: boolean) {
    this.loading[featureKey] = true;
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    this.features[featureKey] = {
      ...this.features[featureKey],
      enabled
    };
    
    this.loading[featureKey] = false;
  }

  getRolloutBadgeVariant(rollout: number): string {
    if (rollout === 0) return 'secondary';
    if (rollout < 50) return 'warning';
    if (rollout < 100) return 'primary';
    return 'success';
  }

  getImpactVariant(impact: string): string {
    switch (impact) {
      case 'High': return 'error';
      case 'Medium': return 'warning';
      default: return 'success';
    }
  }
}
```

### Accessibility-Focused Toggle Switches

#### React
```jsx
import { SafToggleSwitch, SafCard, SafIcon, SafButton } from '@saffron/react';
import { useState } from 'react';

const AccessibilityToggleSwitchExample = () => {
  const [accessibilitySettings, setAccessibilitySettings] = useState({
    highContrast: false,
    reducedMotion: false,
    screenReader: true,
    largeText: false,
    keyboardNavigation: true,
    focusIndicators: true
  });

  const handleSettingChange = (setting, value) => {
    setAccessibilitySettings(prev => ({
      ...prev,
      [setting]: value
    }));
  };

  const resetToDefaults = () => {
    setAccessibilitySettings({
      highContrast: false,
      reducedMotion: false,
      screenReader: false,
      largeText: false,
      keyboardNavigation: true,
      focusIndicators: true
    });
  };

  return (
    <SafCard className="accessibility-settings">
      <SafCard.Header>
        <h2>Accessibility Settings</h2>
        <SafButton variant="outline" onClick={resetToDefaults}>
          Reset to Defaults
        </SafButton>
      </SafCard.Header>
      <SafCard.Content>
        <div className="accessibility-controls">
          <div className="control-section">
            <h3>Visual Accessibility</h3>
            
            <SafToggleSwitch
              checked={accessibilitySettings.highContrast}
              onChange={(value) => handleSettingChange('highContrast', value)}
              label="High Contrast Mode"
              description="Enhance color contrast for better visibility"
              color="primary"
              size="large"
              checkedIcon={<SafIcon name="contrast" />}
              uncheckedIcon={<SafIcon name="eye" />}
              aria-describedby="high-contrast-help"
            />
            <div id="high-contrast-help" className="sr-only">
              Increases contrast between text and background colors
            </div>

            <SafToggleSwitch
              checked={accessibilitySettings.largeText}
              onChange={(value) => handleSettingChange('largeText', value)}
              label="Large Text"
              description="Increase text size for easier reading"
              color="primary"
              checkedIcon={<SafIcon name="type" />}
              aria-describedby="large-text-help"
            />
            <div id="large-text-help" className="sr-only">
              Makes all text larger and easier to read
            </div>
          </div>

          <div className="control-section">
            <h3>Motion & Animation</h3>
            
            <SafToggleSwitch
              checked={accessibilitySettings.reducedMotion}
              onChange={(value) => handleSettingChange('reducedMotion', value)}
              label="Reduced Motion"
              description="Minimize animations and transitions"
              color="warning"
              checkedIcon={<SafIcon name="pause" />}
              uncheckedIcon={<SafIcon name="play" />}
              aria-describedby="reduced-motion-help"
            />
            <div id="reduced-motion-help" className="sr-only">
              Reduces or eliminates animations that may cause discomfort
            </div>
          </div>

          <div className="control-section">
            <h3>Navigation & Input</h3>
            
            <SafToggleSwitch
              checked={accessibilitySettings.keyboardNavigation}
              onChange={(value) => handleSettingChange('keyboardNavigation', value)}
              label="Enhanced Keyboard Navigation"
              description="Improve keyboard-only navigation experience"
              color="success"
              required={true}
              checkedIcon={<SafIcon name="keyboard" />}
              aria-describedby="keyboard-nav-help"
            />
            <div id="keyboard-nav-help" className="sr-only">
              Enables enhanced keyboard shortcuts and navigation aids
            </div>

            <SafToggleSwitch
              checked={accessibilitySettings.focusIndicators}
              onChange={(value) => handleSettingChange('focusIndicators', value)}
              label="Enhanced Focus Indicators"
              description="Make focus indicators more visible"
              color="success"
              checkedIcon={<SafIcon name="target" />}
              aria-describedby="focus-indicators-help"
            />
            <div id="focus-indicators-help" className="sr-only">
              Provides clearer visual indication of focused elements
            </div>
          </div>

          <div className="control-section">
            <h3>Assistive Technology</h3>
            
            <SafToggleSwitch
              checked={accessibilitySettings.screenReader}
              onChange={(value) => handleSettingChange('screenReader', value)}
              label="Screen Reader Optimizations"
              description="Enhance compatibility with screen reading software"
              color="primary"
              checkedIcon={<SafIcon name="headphones" />}
              uncheckedIcon={<SafIcon name="volume-x" />}
              aria-describedby="screen-reader-help"
            />
            <div id="screen-reader-help" className="sr-only">
              Optimizes content and interactions for screen reading software
            </div>
          </div>
        </div>

        <div className="settings-summary">
          <h3>Active Settings Summary</h3>
          <ul className="settings-list" role="list">
            {Object.entries(accessibilitySettings)
              .filter(([_, enabled]) => enabled)
              .map(([setting, _]) => (
                <li key={setting} role="listitem">
                  <SafIcon name="check" color="success" />
                  {setting.replace(/([A-Z])/g, ' $1').replace(/^./, str => str.toUpperCase())}
                </li>
              ))}
          </ul>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// accessibility-toggle-switch.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-accessibility-toggle-switch',
  template: `
    <saf-card class="accessibility-settings">
      <saf-card-header>
        <h2>Accessibility Settings</h2>
        <saf-button variant="outline" (click)="resetToDefaults()">
          Reset to Defaults
        </saf-button>
      </saf-card-header>
      <saf-card-content>
        <div class="accessibility-controls">
          <div class="control-section">
            <h3>Visual Accessibility</h3>
            
            <saf-toggle-switch
              [checked]="accessibilitySettings.highContrast"
              (checkedChange)="handleSettingChange('highContrast', $event)"
              label="High Contrast Mode"
              description="Enhance color contrast for better visibility"
              color="primary"
              size="large"
              checkedIcon="contrast"
              uncheckedIcon="eye"
              aria-describedby="high-contrast-help">
            </saf-toggle-switch>
            <div id="high-contrast-help" class="sr-only">
              Increases contrast between text and background colors
            </div>

            <saf-toggle-switch
              [checked]="accessibilitySettings.largeText"
              (checkedChange)="handleSettingChange('largeText', $event)"
              label="Large Text"
              description="Increase text size for easier reading"
              color="primary"
              checkedIcon="type"
              aria-describedby="large-text-help">
            </saf-toggle-switch>
            <div id="large-text-help" class="sr-only">
              Makes all text larger and easier to read
            </div>
          </div>

          <div class="control-section">
            <h3>Motion & Animation</h3>
            
            <saf-toggle-switch
              [checked]="accessibilitySettings.reducedMotion"
              (checkedChange)="handleSettingChange('reducedMotion', $event)"
              label="Reduced Motion"
              description="Minimize animations and transitions"
              color="warning"
              checkedIcon="pause"
              uncheckedIcon="play"
              aria-describedby="reduced-motion-help">
            </saf-toggle-switch>
            <div id="reduced-motion-help" class="sr-only">
              Reduces or eliminates animations that may cause discomfort
            </div>
          </div>

          <div class="control-section">
            <h3>Navigation & Input</h3>
            
            <saf-toggle-switch
              [checked]="accessibilitySettings.keyboardNavigation"
              (checkedChange)="handleSettingChange('keyboardNavigation', $event)"
              label="Enhanced Keyboard Navigation"
              description="Improve keyboard-only navigation experience"
              color="success"
              [required]="true"
              checkedIcon="keyboard"
              aria-describedby="keyboard-nav-help">
            </saf-toggle-switch>
            <div id="keyboard-nav-help" class="sr-only">
              Enables enhanced keyboard shortcuts and navigation aids
            </div>

            <saf-toggle-switch
              [checked]="accessibilitySettings.focusIndicators"
              (checkedChange)="handleSettingChange('focusIndicators', $event)"
              label="Enhanced Focus Indicators"
              description="Make focus indicators more visible"
              color="success"
              checkedIcon="target"
              aria-describedby="focus-indicators-help">
            </saf-toggle-switch>
            <div id="focus-indicators-help" class="sr-only">
              Provides clearer visual indication of focused elements
            </div>
          </div>

          <div class="control-section">
            <h3>Assistive Technology</h3>
            
            <saf-toggle-switch
              [checked]="accessibilitySettings.screenReader"
              (checkedChange)="handleSettingChange('screenReader', $event)"
              label="Screen Reader Optimizations"
              description="Enhance compatibility with screen reading software"
              color="primary"
              checkedIcon="headphones"
              uncheckedIcon="volume-x"
              aria-describedby="screen-reader-help">
            </saf-toggle-switch>
            <div id="screen-reader-help" class="sr-only">
              Optimizes content and interactions for screen reading software
            </div>
          </div>
        </div>

        <div class="settings-summary">
          <h3>Active Settings Summary</h3>
          <ul class="settings-list" role="list">
            <li 
              *ngFor="let setting of getActiveSettings()" 
              role="listitem">
              <saf-icon name="check" color="success"></saf-icon>
              {{ formatSettingName(setting) }}
            </li>
          </ul>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class AccessibilityToggleSwitchComponent {
  accessibilitySettings = {
    highContrast: false,
    reducedMotion: false,
    screenReader: true,
    largeText: false,
    keyboardNavigation: true,
    focusIndicators: true
  };

  handleSettingChange(setting: string, value: boolean) {
    this.accessibilitySettings = {
      ...this.accessibilitySettings,
      [setting]: value
    };
  }

  resetToDefaults() {
    this.accessibilitySettings = {
      highContrast: false,
      reducedMotion: false,
      screenReader: false,
      largeText: false,
      keyboardNavigation: true,
      focusIndicators: true
    };
  }

  getActiveSettings(): string[] {
    return Object.entries(this.accessibilitySettings)
      .filter(([_, enabled]) => enabled)
      .map(([setting, _]) => setting);
  }

  formatSettingName(setting: string): string {
    return setting.replace(/([A-Z])/g, ' $1').replace(/^./, str => str.toUpperCase());
  }
}
```

## Best Practices

1. **Label and Description**
   - Provide clear, descriptive labels for all toggle switches
   - Use descriptions to explain the effect of toggling
   - Consider the impact of state changes on user experience

2. **Visual Design**
   - Use appropriate colors to indicate state and importance
   - Ensure sufficient contrast for accessibility
   - Provide smooth animations for state transitions

3. **Form Integration**
   - Implement proper validation for required toggles
   - Show clear error states and messages
   - Group related toggles logically

4. **State Management**
   - Handle loading states for async operations
   - Provide immediate visual feedback for interactions
   - Consider the implications of state changes on other components

5. **Accessibility**
   - Use proper ARIA attributes and roles
   - Support keyboard navigation and interaction
   - Provide meaningful descriptions for screen readers

## Accessibility Considerations

1. **ARIA Support**
   - Use `role="switch"` for semantic meaning
   - Implement `aria-checked` to indicate state
   - Provide `aria-describedby` for additional context

2. **Keyboard Navigation**
   - Support Space bar for toggle activation
   - Enable Tab navigation to reach toggles
   - Provide clear focus indicators

3. **Screen Reader Compatibility**
   - Announce state changes when toggled
   - Provide descriptive labels and help text
   - Use semantic markup for grouping related toggles

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all states
   - Provide visual state indicators beyond color
   - Support high contrast and reduced motion preferences

## Related Components

- **SafCheckbox**: Alternative for binary selection in forms
- **SafRadioButton**: Exclusive selection within groups
- **SafButton**: Alternative action triggers
- **SafCard**: Container for grouped toggle switches
- **SafIcon**: Visual indicators for toggle states

## Notes

- Toggle switch automatically handles state transitions with smooth animations
- Custom CSS variables available for comprehensive theming
- Built-in support for form validation and integration
- Optimized for touch interactions on mobile devices
- Compatible with popular form libraries and state management solutions
- Supports both controlled and uncontrolled usage patterns
- Responsive design adapts to different screen sizes and orientations
