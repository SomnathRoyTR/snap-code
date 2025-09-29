# SafAlert

A flexible alert component for displaying important messages to users with various appearance types and automatic dismissal options. Supports both inline and toast display modes.

## Usage

```html
<saf-alert appearance="informational">
  This is an informational alert message.
</saf-alert>
```

## API

### SafAlert

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `appearance` | `'informational' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'informational'` | The visual style and semantic meaning of the alert |
| `alert-type` | `'inline' \| 'toast'` | `'inline'` | Display mode - inline appears in content flow, toast appears at top of page |
| `duration` | `number` | - | Auto-dismiss time in seconds (minimum 10 seconds, 0 = no auto-dismiss) |
| `is-hidden` | `boolean` | `false` | Whether the alert is currently hidden |
| `hide-close-button` | `boolean` | `false` | Whether to hide the close button |
| `announce` | `boolean` | `true` | Whether the alert should be immediately announced to screen readers |
| `density` | `'compact' \| 'normal' \| 'spacious'` | `'inherit'` | Controls the spacing in and around the component |

#### Accessibility Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `icon-aria-label` | `string` | auto | ARIA label for the status icon |
| `icon-presentation` | `boolean` | `false` | Whether to hide the icon from screen readers |
| `close-aria-label` | `string` | `'Close alert'` | ARIA label for the close button |

#### Methods

| Name | Parameters | Description |
|------|------------|-------------|
| `close(timer)` | `timer: number` | Programmatically close the alert with optional delay |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `close` | `CustomEvent` | Fires when the alert is closed (user action or auto-dismiss) |

#### Slots

| Name | Description |
|------|-------------|
| default | Main alert message content |
| `link` | Additional link or action content (announced differently to screen readers) |

#### Parts

| Name | Description |
|------|-------------|
| `control` | The main alert container |
| `alert-icon` | The status icon element |
| `content` | The content area containing message and links |
| `alert-btn` | The close button element |

## Examples

### Basic Alert Types

```html
<!-- Informational alert -->
<saf-alert appearance="informational">
  This is general information that might be helpful to know.
</saf-alert>

<!-- Success alert -->
<saf-alert appearance="success">
  Your changes have been saved successfully!
</saf-alert>

<!-- Warning alert -->
<saf-alert appearance="warning">
  Please review your information before submitting.
</saf-alert>

<!-- Error alert -->
<saf-alert appearance="error">
  An error occurred while processing your request.
</saf-alert>

<!-- Neutral alert -->
<saf-alert appearance="neutral">
  This is a neutral status message.
</saf-alert>
```

### Auto-Dismissing Alerts

```html
<!-- Auto-dismiss after 15 seconds -->
<saf-alert appearance="success" duration="15">
  File uploaded successfully! This message will disappear automatically.
</saf-alert>

<!-- Auto-dismiss after 30 seconds -->
<saf-alert appearance="informational" duration="30">
  New features are available. This notification will auto-dismiss.
</saf-alert>
```

### Alert with Action Links

```html
<saf-alert appearance="warning">
  Your session will expire soon.
  <a href="/extend-session" slot="link">Extend Session</a>
</saf-alert>

<saf-alert appearance="error">
  Failed to save your work.
  <button slot="link" onclick="retryAction()">Try Again</button>
  <a href="/help" slot="link">Get Help</a>
</saf-alert>
```

### Non-Dismissible Alerts

```html
<saf-alert appearance="error" hide-close-button>
  System maintenance is currently in progress. This alert cannot be dismissed.
</saf-alert>
```

### Toast Alerts

```html
<saf-alert alert-type="toast" appearance="success" duration="10">
  Operation completed successfully!
</saf-alert>

<saf-alert alert-type="toast" appearance="error">
  Network connection lost. Please check your connection.
</saf-alert>
```

### Custom Icon Labels

```html
<saf-alert appearance="warning" icon-aria-label="Security warning">
  Two-factor authentication is recommended for your account.
</saf-alert>

<saf-alert appearance="informational" icon-presentation>
  <!-- Icon is hidden from screen readers, meaning is in text -->
  Important: Your password expires in 5 days.
</saf-alert>
```

### Different Density Settings

```html
<saf-alert appearance="informational" density="compact">
  Compact alert with reduced spacing.
</saf-alert>

<saf-alert appearance="informational" density="spacious">
  Spacious alert with increased spacing for better readability.
</saf-alert>
```

### Form Validation Alerts

```html
<form>
  <saf-text-field label="Email" type="email" required></saf-text-field>
  
  <saf-alert appearance="error" style="margin-top: 8px; display: none;" id="email-error">
    Please enter a valid email address.
  </saf-alert>
  
  <saf-text-field label="Password" type="password" required></saf-text-field>
  
  <saf-alert appearance="error" style="margin-top: 8px; display: none;" id="password-error">
    Password must be at least 8 characters long.
    <a href="/password-help" slot="link">Password Requirements</a>
  </saf-alert>
  
  <saf-button type="submit">Submit</saf-button>
</form>
```

### Status Updates

```html
<div id="status-area">
  <!-- Different statuses shown based on operation state -->
  <saf-alert appearance="informational" id="loading-alert" style="display: none;">
    Processing your request...
  </saf-alert>
  
  <saf-alert appearance="success" id="success-alert" style="display: none;" duration="10">
    Request processed successfully!
  </saf-alert>
  
  <saf-alert appearance="error" id="error-alert" style="display: none;">
    Request failed. Please try again.
    <button slot="link" onclick="retryRequest()">Retry</button>
  </saf-alert>
</div>
```

### System Announcements

```html
<saf-alert appearance="informational" hide-close-button>
  <strong>Scheduled Maintenance:</strong> System will be unavailable from 2:00 AM to 4:00 AM EST.
  <a href="/maintenance-details" slot="link">Learn More</a>
</saf-alert>

<saf-alert appearance="success">
  <strong>New Feature:</strong> Dark mode is now available in user settings.
  <a href="/settings/appearance" slot="link">Enable Now</a>
</saf-alert>
```

### Event Handling

```html
<saf-alert id="dismissible-alert" appearance="warning">
  This alert can be programmatically dismissed.
  <button slot="link" onclick="dismissAlert()">Dismiss</button>
</saf-alert>

<script>
  const alert = document.getElementById('dismissible-alert');

  // Listen for close event
  alert.addEventListener('close', () => {
    console.log('Alert was closed');
    // Perform cleanup or additional actions
  });

  function dismissAlert() {
    // Close the alert programmatically
    alert.close(0); // Close immediately
  }

  // Example: Close alert after user interaction elsewhere
  function delayedDismiss() {
    // Close alert after 3 seconds
    alert.close(3);
  }
</script>
```

### Progress Notifications

```html
<div id="progress-notifications">
  <!-- Step 1 -->
  <saf-alert appearance="informational" id="step1">
    Step 1: Validating information...
  </saf-alert>

  <!-- Step 2 (initially hidden) -->
  <saf-alert appearance="informational" id="step2" style="display: none;">
    Step 2: Processing payment...
  </saf-alert>

  <!-- Step 3 (initially hidden) -->
  <saf-alert appearance="success" id="step3" style="display: none;">
    Step 3: Order confirmed! Confirmation email sent.
    <a href="/order-details" slot="link">View Order</a>
  </saf-alert>
</div>
```

### Bulk Operations Feedback

```html
<saf-alert appearance="success" id="bulk-success">
  Successfully processed 45 of 50 items.
  <button slot="link" onclick="showFailedItems()">View Failed Items</button>
</saf-alert>

<saf-alert appearance="warning" id="partial-failure" style="display: none;">
  5 items failed to process due to validation errors.
  <a href="/bulk-errors" slot="link">Download Error Report</a>
  <button slot="link" onclick="retryFailedItems()">Retry Failed</button>
</saf-alert>
```

## Framework Integration

### React

```jsx
import { SafAlert } from '@saffron/core-components-react';
import { useState, useEffect } from 'react';

function AlertExample() {
  const [alerts, setAlerts] = useState([]);
  const [nextId, setNextId] = useState(1);

  const addAlert = (appearance, message, duration = 0) => {
    const newAlert = {
      id: nextId,
      appearance,
      message,
      duration,
      visible: true
    };
    
    setAlerts(prev => [...prev, newAlert]);
    setNextId(prev => prev + 1);
  };

  const removeAlert = (id) => {
    setAlerts(prev => prev.filter(alert => alert.id !== id));
  };

  const handleAlertClose = (id) => {
    removeAlert(id);
  };

  return (
    <div>
      <div style={{ marginBottom: '16px' }}>
        <button onClick={() => addAlert('success', 'Operation successful!', 10)}>
          Show Success Alert
        </button>
        <button onClick={() => addAlert('error', 'Something went wrong!')}>
          Show Error Alert
        </button>
        <button onClick={() => addAlert('warning', 'Please be careful', 15)}>
          Show Warning Alert
        </button>
      </div>

      <div className="alert-container">
        {alerts.map(alert => (
          <SafAlert
            key={alert.id}
            appearance={alert.appearance}
            duration={alert.duration}
            onClose={() => handleAlertClose(alert.id)}
            style={{ marginBottom: '8px' }}
          >
            {alert.message}
          </SafAlert>
        ))}
      </div>
    </div>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

interface AlertItem {
  id: number;
  appearance: 'informational' | 'success' | 'warning' | 'error' | 'neutral';
  message: string;
  duration?: number;
  hideCloseButton?: boolean;
  linkText?: string;
  linkAction?: () => void;
}

@Component({
  selector: 'app-alert-demo',
  template: `
    <div class="alert-controls">
      <button (click)="showSuccess()">Success Alert</button>
      <button (click)="showWarning()">Warning Alert</button>
      <button (click)="showError()">Error Alert</button>
      <button (click)="clearAll()">Clear All</button>
    </div>

    <div class="alerts-container">
      <saf-alert
        *ngFor="let alert of alerts; trackBy: trackAlert"
        [appearance]="alert.appearance"
        [duration]="alert.duration"
        [hide-close-button]="alert.hideCloseButton"
        (close)="removeAlert(alert.id)"
        class="alert-item"
      >
        {{ alert.message }}
        
        <button 
          *ngIf="alert.linkAction"
          slot="link"
          (click)="alert.linkAction()"
        >
          {{ alert.linkText }}
        </button>
      </saf-alert>
    </div>

    <div class="system-alerts">
      <saf-alert 
        appearance="informational"
        hide-close-button="true"
        *ngIf="systemStatus === 'maintenance'"
      >
        <strong>Maintenance Mode:</strong> Some features may be limited.
        <a href="/status" slot="link">System Status</a>
      </saf-alert>
    </div>
  `,
  styles: [`
    .alert-controls {
      margin-bottom: 20px;
    }
    .alert-controls button {
      margin-right: 8px;
    }
    .alert-item {
      margin-bottom: 8px;
    }
    .system-alerts {
      margin-top: 20px;
      border-top: 1px solid #e1e5e9;
      padding-top: 20px;
    }
  `]
})
export class AlertDemoComponent {
  alerts: AlertItem[] = [];
  systemStatus = 'normal';
  private nextId = 1;

  showSuccess() {
    this.addAlert({
      appearance: 'success',
      message: 'Operation completed successfully!',
      duration: 10
    });
  }

  showWarning() {
    this.addAlert({
      appearance: 'warning',
      message: 'Please review your changes before saving.',
      linkText: 'Review Changes',
      linkAction: () => console.log('Reviewing changes...')
    });
  }

  showError() {
    this.addAlert({
      appearance: 'error',
      message: 'Failed to save changes. Please try again.',
      linkText: 'Retry',
      linkAction: () => this.retryAction()
    });
  }

  addAlert(alert: Omit<AlertItem, 'id'>) {
    this.alerts.push({
      ...alert,
      id: this.nextId++
    });
  }

  removeAlert(id: number) {
    this.alerts = this.alerts.filter(alert => alert.id !== id);
  }

  clearAll() {
    this.alerts = [];
  }

  retryAction() {
    console.log('Retrying action...');
    // Simulate retry logic
    setTimeout(() => {
      this.removeAlert(this.alerts.find(a => a.appearance === 'error')?.id);
      this.showSuccess();
    }, 1000);
  }

  trackAlert(index: number, alert: AlertItem): number {
    return alert.id;
  }
}
```

## Accessibility Features

- **ARIA Live Regions**: Alerts are automatically announced to screen readers when they appear
- **Screen Reader Support**: Proper labeling and status communication through ARIA attributes
- **Keyboard Navigation**: Close button is keyboard accessible with appropriate focus management
- **Semantic Meaning**: Different appearances convey semantic meaning through icons and styling
- **Customizable Announcements**: Control over what gets announced via `announce` and `icon-presentation` attributes
- **Focus Management**: Proper focus handling when alerts appear and disappear

## Best Practices

1. **Use Appropriate Appearance**: Choose appearance based on semantic meaning, not just visual preference
2. **Provide Clear Messages**: Write concise, actionable messages that explain what happened and what users can do
3. **Auto-Dismiss Timing**: Use minimum 10 seconds for auto-dismiss to give users time to read and act
4. **Action Links**: Include helpful links or actions when users can take next steps
5. **Toast vs Inline**: Use toast for system-wide notifications, inline for contextual messages
6. **Error Recovery**: Always provide ways for users to recover from errors or retry failed actions
7. **Consistent Language**: Use consistent terminology across different alert types
8. **Avoid Alert Fatigue**: Don't overwhelm users with too many alerts at once

## Related Components

- `saf-toast`: For standalone toast notifications
- `saf-notification-banner`: For persistent system-wide announcements  
- `saf-badge`: For subtle status indicators
- `saf-progress`: For progress-related status updates
