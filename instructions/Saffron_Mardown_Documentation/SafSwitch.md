# SafSwitch Component Documentation

## Overview

The **SafSwitch** component is a toggle control that allows users to switch between two states (on/off, enabled/disabled, etc.). It implements the ARIA switch specification and provides comprehensive accessibility features, making it ideal for settings, preferences, and feature toggles.

## React Implementation

### Basic Usage

```tsx
import { SafSwitch } from '@saffron/react-components';
import { useState } from 'react';

function BasicSwitch() {
  const [isEnabled, setIsEnabled] = useState(false);

  return (
    <SafSwitch
      checked={isEnabled}
      onChange={(event) => setIsEnabled(event.target.checked)}
    >
      Enable notifications
    </SafSwitch>
  );
}
```

### Advanced Usage with Settings Panel

```tsx
import { SafSwitch } from '@saffron/react-components';
import { useState, useEffect } from 'react';

function AdvancedSettingsPanel() {
  const [settings, setSettings] = useState({
    notifications: true,
    darkMode: false,
    autoSave: true,
    analytics: false,
    marketing: false,
    locationTracking: false
  });
  const [isLoading, setIsLoading] = useState(false);

  const settingsConfig = {
    notifications: {
      label: 'Push Notifications',
      description: 'Receive push notifications for important updates',
      category: 'Communication'
    },
    darkMode: {
      label: 'Dark Mode',
      description: 'Use dark theme throughout the application',
      category: 'Appearance'
    },
    autoSave: {
      label: 'Auto-save',
      description: 'Automatically save changes as you work',
      category: 'Productivity'
    },
    analytics: {
      label: 'Usage Analytics',
      description: 'Help improve the app by sharing anonymous usage data',
      category: 'Privacy'
    },
    marketing: {
      label: 'Marketing Communications',
      description: 'Receive emails about new features and promotions',
      category: 'Communication',
      dependsOn: 'notifications'
    },
    locationTracking: {
      label: 'Location Tracking',
      description: 'Allow location-based features and services',
      category: 'Privacy'
    }
  };

  const handleSettingChange = (setting: string) => (event: React.ChangeEvent<HTMLInputElement>) => {
    const checked = event.target.checked;
    
    setSettings(prev => {
      const newSettings = {
        ...prev,
        [setting]: checked
      };

      // Handle dependent settings
      if (setting === 'notifications' && !checked) {
        newSettings.marketing = false;
      }

      return newSettings;
    });

    // Simulate API call
    setIsLoading(true);
    setTimeout(() => {
      setIsLoading(false);
      console.log(`${setting} changed to:`, checked);
    }, 500);
  };

  const groupedSettings = Object.entries(settingsConfig).reduce((groups, [key, config]) => {
    if (!groups[config.category]) {
      groups[config.category] = [];
    }
    groups[config.category].push({ key, ...config });
    return groups;
  }, {});

  return (
    <div className="settings-panel">
      <h2>Application Settings</h2>
      
      {Object.entries(groupedSettings).map(([category, categorySettings]) => (
        <div key={category} className="settings-category">
          <h3>{category}</h3>
          
          {categorySettings.map(({ key, label, description, dependsOn }) => {
            const isDependent = dependsOn && !settings[dependsOn];
            
            return (
              <div key={key} className="setting-item">
                <SafSwitch
                  name={key}
                  checked={settings[key]}
                  onChange={handleSettingChange(key)}
                  disabled={isLoading || isDependent}
                  a11yAriaLabel={label}
                  a11yAriaDescription={description}
                >
                  <div className="setting-content">
                    <span className="setting-label">{label}</span>
                    <small className="setting-description">
                      {description}
                      {isDependent && ' (requires notifications to be enabled)'}
                    </small>
                  </div>
                </SafSwitch>
              </div>
            );
          })}
        </div>
      ))}

      <div className="settings-actions">
        <button 
          onClick={() => console.log('Settings saved:', settings)}
          disabled={isLoading}
        >
          {isLoading ? 'Saving...' : 'Save Settings'}
        </button>
        
        <button 
          onClick={() => setSettings({
            notifications: true,
            darkMode: false,
            autoSave: true,
            analytics: false,
            marketing: false,
            locationTracking: false
          })}
          disabled={isLoading}
        >
          Reset to Defaults
        </button>
      </div>
    </div>
  );
}
```

### Feature Toggle Dashboard

```tsx
import { SafSwitch } from '@saffron/react-components';
import { useState } from 'react';

function FeatureToggleDashboard() {
  const [features, setFeatures] = useState({
    betaFeatures: false,
    advancedAnalytics: true,
    experimentalUI: false,
    debugMode: false,
    apiV2: false
  });

  const [confirmDialog, setConfirmDialog] = useState(null);

  const featureConfigs = {
    betaFeatures: {
      label: 'Beta Features',
      description: 'Enable access to beta features and experimental functionality',
      status: 'stable',
      requiresConfirm: true
    },
    advancedAnalytics: {
      label: 'Advanced Analytics',
      description: 'Enable detailed analytics and reporting features',
      status: 'stable',
      requiresConfirm: false
    },
    experimentalUI: {
      label: 'Experimental UI',
      description: 'Try the new experimental user interface (may be unstable)',
      status: 'experimental',
      requiresConfirm: true
    },
    debugMode: {
      label: 'Debug Mode',
      description: 'Enable debug information and developer tools',
      status: 'development',
      requiresConfirm: true
    },
    apiV2: {
      label: 'API Version 2',
      description: 'Use the new API version (some features may not be available)',
      status: 'beta',
      requiresConfirm: true
    }
  };

  const handleFeatureToggle = (feature: string) => (event: React.ChangeEvent<HTMLInputElement>) => {
    const checked = event.target.checked;
    const config = featureConfigs[feature];

    if (config.requiresConfirm && checked) {
      setConfirmDialog({
        feature,
        label: config.label,
        description: config.description,
        status: config.status
      });
    } else {
      setFeatures(prev => ({
        ...prev,
        [feature]: checked
      }));
    }
  };

  const confirmFeatureToggle = () => {
    if (confirmDialog) {
      setFeatures(prev => ({
        ...prev,
        [confirmDialog.feature]: true
      }));
      setConfirmDialog(null);
    }
  };

  const getStatusBadge = (status: string) => {
    const badges = {
      stable: { className: 'badge-stable', text: 'Stable' },
      beta: { className: 'badge-beta', text: 'Beta' },
      experimental: { className: 'badge-experimental', text: 'Experimental' },
      development: { className: 'badge-dev', text: 'Dev Only' }
    };
    return badges[status] || badges.stable;
  };

  return (
    <div className="feature-toggle-dashboard">
      <h2>Feature Toggles</h2>
      <p>Enable or disable experimental features and functionality</p>

      <div className="feature-grid">
        {Object.entries(featureConfigs).map(([key, config]) => {
          const badge = getStatusBadge(config.status);
          
          return (
            <div key={key} className="feature-card">
              <div className="feature-header">
                <span className={`status-badge ${badge.className}`}>
                  {badge.text}
                </span>
              </div>
              
              <SafSwitch
                name={key}
                checked={features[key]}
                onChange={handleFeatureToggle(key)}
                a11yAriaLabel={config.label}
                a11yAriaDescription={config.description}
              >
                <div className="feature-content">
                  <h4>{config.label}</h4>
                  <p>{config.description}</p>
                </div>
              </SafSwitch>
            </div>
          );
        })}
      </div>

      {confirmDialog && (
        <div className="confirmation-dialog">
          <div className="dialog-content">
            <h3>Enable {confirmDialog.label}?</h3>
            <p>{confirmDialog.description}</p>
            <div className="dialog-warning">
              <strong>Warning:</strong> This feature is in {confirmDialog.status} status 
              and may not work as expected.
            </div>
            <div className="dialog-actions">
              <button onClick={confirmFeatureToggle}>
                Enable Feature
              </button>
              <button onClick={() => setConfirmDialog(null)}>
                Cancel
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
```

### Permission Management

```tsx
import { SafSwitch } from '@saffron/react-components';
import { useState } from 'react';

function PermissionManager() {
  const [userPermissions, setUserPermissions] = useState({
    canRead: true,
    canWrite: false,
    canDelete: false,
    canAdmin: false,
    canInvite: false,
    canExport: true
  });

  const permissionHierarchy = {
    canRead: { level: 1, label: 'Read Access', description: 'View content and data' },
    canWrite: { level: 2, label: 'Write Access', description: 'Create and edit content', requires: ['canRead'] },
    canDelete: { level: 3, label: 'Delete Access', description: 'Remove content and data', requires: ['canRead', 'canWrite'] },
    canExport: { level: 2, label: 'Export Access', description: 'Export data and reports', requires: ['canRead'] },
    canInvite: { level: 3, label: 'Invite Users', description: 'Send invitations to new users', requires: ['canRead', 'canWrite'] },
    canAdmin: { level: 4, label: 'Admin Access', description: 'Full administrative privileges', requires: ['canRead', 'canWrite', 'canDelete'] }
  };

  const checkPermissionDependencies = (permission: string, checked: boolean, currentPermissions: any) => {
    const config = permissionHierarchy[permission];
    const newPermissions = { ...currentPermissions, [permission]: checked };

    if (checked) {
      // Enable required permissions
      config.requires?.forEach(required => {
        newPermissions[required] = true;
      });
    } else {
      // Disable dependent permissions
      Object.entries(permissionHierarchy).forEach(([key, value]) => {
        if (value.requires?.includes(permission)) {
          newPermissions[key] = false;
        }
      });
    }

    return newPermissions;
  };

  const handlePermissionChange = (permission: string) => (event: React.ChangeEvent<HTMLInputElement>) => {
    const checked = event.target.checked;
    const newPermissions = checkPermissionDependencies(permission, checked, userPermissions);
    setUserPermissions(newPermissions);
  };

  const isPermissionDisabled = (permission: string) => {
    const config = permissionHierarchy[permission];
    return config.requires?.some(required => !userPermissions[required]) || false;
  };

  const getPermissionsByLevel = () => {
    const levels = {};
    Object.entries(permissionHierarchy).forEach(([key, config]) => {
      if (!levels[config.level]) {
        levels[config.level] = [];
      }
      levels[config.level].push({ key, ...config });
    });
    return levels;
  };

  const levelNames = {
    1: 'Basic Permissions',
    2: 'Content Permissions',
    3: 'Management Permissions',
    4: 'Administrative Permissions'
  };

  return (
    <div className="permission-manager">
      <h2>User Permissions</h2>
      
      {Object.entries(getPermissionsByLevel()).map(([level, permissions]) => (
        <div key={level} className="permission-level">
          <h3>{levelNames[level]}</h3>
          
          {permissions.map(({ key, label, description, requires }) => {
            const isDisabled = isPermissionDisabled(key);
            const hasRequirements = requires && requires.length > 0;
            
            return (
              <div key={key} className="permission-item">
                <SafSwitch
                  name={key}
                  checked={userPermissions[key]}
                  onChange={handlePermissionChange(key)}
                  disabled={isDisabled}
                  a11yAriaLabel={label}
                  a11yAriaDescription={description + (hasRequirements ? ` (requires: ${requires.map(r => permissionHierarchy[r].label).join(', ')})` : '')}
                >
                  <div className="permission-content">
                    <span className="permission-label">{label}</span>
                    <small className="permission-description">
                      {description}
                      {hasRequirements && (
                        <span className="permission-requirements">
                          Requires: {requires.map(r => permissionHierarchy[r].label).join(', ')}
                        </span>
                      )}
                    </small>
                  </div>
                </SafSwitch>
              </div>
            );
          })}
        </div>
      ))}

      <div className="permission-summary">
        <h4>Permission Summary</h4>
        <div className="active-permissions">
          {Object.entries(userPermissions)
            .filter(([, enabled]) => enabled)
            .map(([key]) => (
              <span key={key} className="permission-tag">
                {permissionHierarchy[key].label}
              </span>
            ))}
        </div>
      </div>
    </div>
  );
}
```

### API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `checked` | `boolean` | `false` | Controls the switch state |
| `disabled` | `boolean` | `false` | Disables the switch interaction |
| `readOnly` | `boolean` | `false` | Makes the switch read-only |
| `value` | `string` | `"on"` | The value sent with form data when checked |
| `name` | `string` | `undefined` | Name attribute for form submission |
| `id` | `string` | `auto-generated` | Unique identifier for the switch |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for screen readers |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for state changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-switch',
  template: `
    <saf-switch
      [checked]="isEnabled"
      (change)="onSwitchChange($event)">
      Enable notifications
    </saf-switch>
  `
})
export class BasicSwitchComponent {
  isEnabled = false;

  onSwitchChange(event: any) {
    this.isEnabled = event.target.checked;
  }
}
```

### Advanced Usage with Settings

```typescript
// component.ts
import { Component } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-settings-panel',
  template: `
    <div class="settings-panel">
      <h2>Application Settings</h2>
      
      <form [formGroup]="settingsForm">
        <div *ngFor="let setting of settingsConfig" class="setting-item">
          <saf-switch
            [formControlName]="setting.key"
            [disabled]="isSettingDisabled(setting.key)"
            [a11y-aria-label]="setting.label"
            [a11y-aria-description]="setting.description">
            <div class="setting-content">
              <span class="setting-label">{{ setting.label }}</span>
              <small class="setting-description">
                {{ setting.description }}
                <span *ngIf="isSettingDisabled(setting.key)">
                  (requires {{ setting.dependsOn }} to be enabled)
                </span>
              </small>
            </div>
          </saf-switch>
        </div>
      </form>

      <div class="settings-actions">
        <button (click)="saveSettings()" [disabled]="isLoading">
          {{ isLoading ? 'Saving...' : 'Save Settings' }}
        </button>
        <button (click)="resetSettings()" [disabled]="isLoading">
          Reset to Defaults
        </button>
      </div>
    </div>
  `
})
export class SettingsPanelComponent {
  settingsForm: FormGroup;
  isLoading = false;

  settingsConfig = [
    {
      key: 'notifications',
      label: 'Push Notifications',
      description: 'Receive push notifications for important updates',
      category: 'Communication'
    },
    {
      key: 'darkMode',
      label: 'Dark Mode',
      description: 'Use dark theme throughout the application',
      category: 'Appearance'
    },
    {
      key: 'autoSave',
      label: 'Auto-save',
      description: 'Automatically save changes as you work',
      category: 'Productivity'
    },
    {
      key: 'marketing',
      label: 'Marketing Communications',
      description: 'Receive emails about new features and promotions',
      category: 'Communication',
      dependsOn: 'notifications'
    }
  ];

  constructor(private fb: FormBuilder) {
    this.settingsForm = this.fb.group({
      notifications: [true],
      darkMode: [false],
      autoSave: [true],
      marketing: [false]
    });

    // Handle dependent settings
    this.settingsForm.get('notifications')?.valueChanges.subscribe(value => {
      if (!value) {
        this.settingsForm.get('marketing')?.setValue(false);
      }
    });
  }

  isSettingDisabled(settingKey: string): boolean {
    const setting = this.settingsConfig.find(s => s.key === settingKey);
    if (setting?.dependsOn) {
      return !this.settingsForm.get(setting.dependsOn)?.value;
    }
    return false;
  }

  saveSettings() {
    this.isLoading = true;
    // Simulate API call
    setTimeout(() => {
      console.log('Settings saved:', this.settingsForm.value);
      this.isLoading = false;
    }, 1000);
  }

  resetSettings() {
    this.settingsForm.reset({
      notifications: true,
      darkMode: false,
      autoSave: true,
      marketing: false
    });
  }
}
```

### API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `checked` | `boolean` | `false` | Switch state |
| `disabled` | `boolean` | `false` | Disabled state |
| `readOnly` | `boolean` | `false` | Read-only state |
| `value` | `string` | `"on"` | Form value when checked |
| `name` | `string` | `undefined` | Form field name |
| `id` | `string` | `auto-generated` | Element identifier |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when switch state changes |
| `focus` | `Event` | Emitted when switch receives focus |
| `blur` | `Event` | Emitted when switch loses focus |

## Best Practices

### Accessibility
- **Clear labels**: Use descriptive labels that clearly indicate what the switch controls
- **State announcements**: Ensure screen readers announce state changes properly
- **Keyboard interaction**: Support Space and Enter keys for activation
- **Focus indicators**: Provide clear visual focus indicators

### UX Guidelines
- **Immediate effect**: Switch changes should take effect immediately without requiring form submission
- **Clear labeling**: Use labels that clearly indicate what will happen when the switch is on/off
- **Consistent behavior**: Maintain consistent switch behavior throughout the application
- **Visual feedback**: Provide clear visual feedback for state changes

### Form Integration
- **State management**: Use controlled components with proper state management
- **Dependent settings**: Handle cascading settings changes appropriately
- **Validation**: Implement validation for required switches when necessary
- **Default states**: Set sensible default states for better user experience

### Design Considerations
- **Grouping**: Group related switches logically with clear section headings
- **Confirmation**: Consider confirmation dialogs for critical or irreversible changes
- **Loading states**: Show loading indicators for switches that trigger async operations
- **Error handling**: Provide clear error messages when switch operations fail

## Accessibility Notes

The SafSwitch component provides comprehensive accessibility support:

- **ARIA compliance**: Full implementation of ARIA switch role and states
- **Screen reader support**: Proper announcements for state changes and labels
- **Keyboard navigation**: Space and Enter key support for activation
- **Focus management**: Clear focus indicators and logical focus behavior
- **State communication**: Clear communication of on/off states to assistive technologies

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+ with touch optimization
- **Keyboard navigation**: Full keyboard support across all browsers
- **Accessibility**: NVDA, JAWS, VoiceOver support

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: The `checked` prop is now controlled by default, requires proper state management
- **v1.x to v2.x**: `onChange` event signature changed to match native input events
- **Deprecated props**: `defaultChecked` replaced with `checked` and proper state management

---

*This documentation provides comprehensive guidance for implementing SafSwitch in both React and Angular applications with proper accessibility, state management, and user experience considerations.*
