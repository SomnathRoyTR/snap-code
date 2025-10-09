# SafMessageBox

## Overview

SafMessageBox is a versatile messaging component for displaying alerts, notifications, and informational content to users. It provides consistent styling and behavior for various message types with support for actions, dismissal, and rich content including icons, images, and interactive elements.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'info' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'info'` | Message type determining color and default icon |
| `title` | `string` | - | Message title/heading |
| `message` | `string` | - | Primary message content |
| `severity` | `'low' \| 'medium' \| 'high' \| 'critical'` | `'medium'` | Message severity level |
| `dismissible` | `boolean` | `false` | Shows dismiss button and allows closing |
| `persistent` | `boolean` | `false` | Prevents automatic dismissal |
| `icon` | `string \| ReactElement \| boolean` | - | Custom icon or false to hide default |
| `actions` | `Array<{ label: string; onClick: () => void; variant?: string; disabled?: boolean }>` | `[]` | Action buttons |
| `image` | `string \| ReactElement` | - | Optional image or illustration |
| `compact` | `boolean` | `false` | Reduces padding and spacing |
| `fullWidth` | `boolean` | `false` | Expands to full container width |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Custom content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onDismiss` | `() => void` | Fired when message box is dismissed |
| `onShow` | `() => void` | Fired when message box is displayed |
| `onActionClick` | `(actionIndex: number) => void` | Fired when action button is clicked |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'info' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'info'` | Message type determining color and default icon |
| `title` | `string` | - | Message title/heading |
| `message` | `string` | - | Primary message content |
| `severity` | `'low' \| 'medium' \| 'high' \| 'critical'` | `'medium'` | Message severity level |
| `dismissible` | `boolean` | `false` | Shows dismiss button and allows closing |
| `persistent` | `boolean` | `false` | Prevents automatic dismissal |
| `icon` | `string \| boolean` | - | Custom icon name or false to hide default |
| `actions` | `Array<{ label: string; variant?: string; disabled?: boolean }>` | `[]` | Action buttons configuration |
| `image` | `string` | - | Optional image URL |
| `compact` | `boolean` | `false` | Reduces padding and spacing |
| `fullWidth` | `boolean` | `false` | Expands to full container width |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `dismiss` | `EventEmitter<void>` | Fired when message box is dismissed |
| `show` | `EventEmitter<void>` | Fired when message box is displayed |
| `actionClick` | `EventEmitter<number>` | Fired when action button is clicked |

## Usage Examples

### Basic Message Boxes

```typescript
// React
<SafMessageBox 
  variant="info" 
  title="Information" 
  message="This is an informational message." 
/>

<SafMessageBox 
  variant="success" 
  title="Success!" 
  message="Your changes have been saved successfully." 
/>

<SafMessageBox 
  variant="warning" 
  title="Warning" 
  message="Please review your input before continuing." 
/>

<SafMessageBox 
  variant="error" 
  title="Error" 
  message="Unable to complete the requested operation." 
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="info" 
  title="Information" 
  message="This is an informational message.">
</saf-message-box>

<saf-message-box 
  variant="success" 
  title="Success!" 
  message="Your changes have been saved successfully.">
</saf-message-box>

<saf-message-box 
  variant="warning" 
  title="Warning" 
  message="Please review your input before continuing.">
</saf-message-box>

<saf-message-box 
  variant="error" 
  title="Error" 
  message="Unable to complete the requested operation.">
</saf-message-box>
```

### Dismissible Messages

```typescript
// React
<SafMessageBox 
  variant="info" 
  title="System Update" 
  message="A system update is available. Would you like to install it now?"
  dismissible
  onDismiss={() => console.log('Message dismissed')}
/>

<SafMessageBox 
  variant="warning" 
  title="Session Expiring" 
  message="Your session will expire in 5 minutes."
  dismissible
  persistent
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="info" 
  title="System Update" 
  message="A system update is available. Would you like to install it now?"
  [dismissible]="true"
  (dismiss)="onMessageDismiss()">
</saf-message-box>

<saf-message-box 
  variant="warning" 
  title="Session Expiring" 
  message="Your session will expire in 5 minutes."
  [dismissible]="true"
  [persistent]="true">
</saf-message-box>
```

### Messages with Actions

```typescript
// React
<SafMessageBox 
  variant="success" 
  title="File Uploaded" 
  message="Your file has been uploaded successfully."
  actions={[
    { label: 'View File', onClick: () => viewFile() },
    { label: 'Share', onClick: () => shareFile(), variant: 'outline' }
  ]}
  dismissible
/>

<SafMessageBox 
  variant="error" 
  title="Connection Failed" 
  message="Unable to connect to the server. Please try again."
  actions={[
    { label: 'Retry', onClick: () => retryConnection() },
    { label: 'Offline Mode', onClick: () => enableOfflineMode(), variant: 'text' }
  ]}
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="success" 
  title="File Uploaded" 
  message="Your file has been uploaded successfully."
  [actions]="uploadActions"
  [dismissible]="true"
  (actionClick)="handleActionClick($event)">
</saf-message-box>

<saf-message-box 
  variant="error" 
  title="Connection Failed" 
  message="Unable to connect to the server. Please try again."
  [actions]="connectionActions"
  (actionClick)="handleConnectionAction($event)">
</saf-message-box>
```

### Custom Icons and Images

```typescript
// React
<SafMessageBox 
  variant="info" 
  title="Welcome!" 
  message="Welcome to our application. Let's get you started."
  icon="user-plus"
  image="/images/welcome-illustration.svg"
/>

<SafMessageBox 
  variant="success" 
  title="Achievement Unlocked!" 
  message="You've completed your first project."
  icon={<SafIcon name="trophy" size="large" />}
/>

<SafMessageBox 
  variant="neutral" 
  title="System Maintenance" 
  message="Scheduled maintenance will occur tonight from 12 AM to 2 AM."
  icon={false}
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="info" 
  title="Welcome!" 
  message="Welcome to our application. Let's get you started."
  icon="user-plus"
  image="/images/welcome-illustration.svg">
</saf-message-box>

<saf-message-box 
  variant="success" 
  title="Achievement Unlocked!" 
  message="You've completed your first project."
  icon="trophy">
</saf-message-box>

<saf-message-box 
  variant="neutral" 
  title="System Maintenance" 
  message="Scheduled maintenance will occur tonight from 12 AM to 2 AM."
  [icon]="false">
</saf-message-box>
```

### Severity Levels

```typescript
// React
<SafMessageBox 
  variant="warning" 
  severity="low"
  title="Minor Issue" 
  message="A minor issue was detected but won't affect functionality."
/>

<SafMessageBox 
  variant="warning" 
  severity="high"
  title="Important Warning" 
  message="This action cannot be undone. Please confirm before proceeding."
  actions={[
    { label: 'Confirm', onClick: () => confirmAction() },
    { label: 'Cancel', onClick: () => cancelAction(), variant: 'outline' }
  ]}
/>

<SafMessageBox 
  variant="error" 
  severity="critical"
  title="Critical Error" 
  message="System failure detected. Contact support immediately."
  persistent
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="warning" 
  severity="low"
  title="Minor Issue" 
  message="A minor issue was detected but won't affect functionality.">
</saf-message-box>

<saf-message-box 
  variant="warning" 
  severity="high"
  title="Important Warning" 
  message="This action cannot be undone. Please confirm before proceeding."
  [actions]="confirmActions">
</saf-message-box>

<saf-message-box 
  variant="error" 
  severity="critical"
  title="Critical Error" 
  message="System failure detected. Contact support immediately."
  [persistent]="true">
</saf-message-box>
```

### Custom Content with Children

```typescript
// React
<SafMessageBox 
  variant="info" 
  title="Software Update Available"
  dismissible
>
  <div>
    <p>Version 2.1.0 is now available with the following improvements:</p>
    <ul>
      <li>Enhanced performance</li>
      <li>New collaboration features</li>
      <li>Bug fixes and security updates</li>
    </ul>
    <SafProgressBar value={75} size="small" />
    <p><small>Download: 75% complete</small></p>
  </div>
</SafMessageBox>

<SafMessageBox 
  variant="success" 
  title="Team Invitation"
>
  <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
    <SafAvatar name="John Doe" size="medium" />
    <div>
      <p><strong>John Doe</strong> invited you to join the <strong>Project Alpha</strong> team.</p>
      <div style={{ marginTop: '8px' }}>
        <SafButton size="small" onClick={() => acceptInvite()}>Accept</SafButton>
        <SafButton variant="outline" size="small" onClick={() => declineInvite()}>
          Decline
        </SafButton>
      </div>
    </div>
  </div>
</SafMessageBox>
```

### Compact Layout

```typescript
// React
<SafMessageBox 
  variant="warning" 
  message="Your trial expires in 3 days."
  compact
  actions={[
    { label: 'Upgrade', onClick: () => upgrade() }
  ]}
  dismissible
/>

<SafMessageBox 
  variant="info" 
  message="2 new messages"
  compact
  icon="mail"
  actions={[
    { label: 'View', onClick: () => viewMessages() }
  ]}
/>
```

```html
<!-- Angular -->
<saf-message-box 
  variant="warning" 
  message="Your trial expires in 3 days."
  [compact]="true"
  [actions]="trialActions"
  [dismissible]="true">
</saf-message-box>

<saf-message-box 
  variant="info" 
  message="2 new messages"
  [compact]="true"
  icon="mail"
  [actions]="messageActions">
</saf-message-box>
```

### Form Validation Messages

```typescript
// React
<SafMessageBox 
  variant="error" 
  title="Form Validation Failed"
  message="Please correct the following errors before submitting:"
>
  <ul>
    <li>Email address is required</li>
    <li>Password must be at least 8 characters</li>
    <li>Terms and conditions must be accepted</li>
  </ul>
</SafMessageBox>

<SafMessageBox 
  variant="success" 
  title="Form Submitted Successfully"
  message="Your information has been saved and you will receive a confirmation email shortly."
  dismissible
  actions={[
    { label: 'Continue', onClick: () => navigate('/dashboard') }
  ]}
/>
```

### Data Processing Messages

```typescript
// React
<SafMessageBox 
  variant="info" 
  title="Processing Data"
  message="Please wait while we process your request..."
  persistent
>
  <SafProgressBar value={45} />
  <p><small>Processing 450 of 1000 records...</small></p>
</SafMessageBox>

<SafMessageBox 
  variant="warning" 
  title="Data Import Issues"
  message="Some issues were found during import:"
>
  <div>
    <p>• 15 duplicate entries were skipped</p>
    <p>• 3 records had missing required fields</p>
    <p>• 987 records were imported successfully</p>
    <SafButton 
      variant="text" 
      size="small" 
      onClick={() => downloadErrorReport()}
    >
      Download Error Report
    </SafButton>
  </div>
</SafMessageBox>
```

### System Status Messages

```typescript
// React
<SafMessageBox 
  variant="error" 
  title="Service Unavailable"
  severity="critical"
  message="Our servers are currently experiencing issues."
>
  <div>
    <p>We're working to resolve this as quickly as possible.</p>
    <SafStatus variant="error">Last updated: 2 minutes ago</SafStatus>
    <div style={{ marginTop: '12px' }}>
      <SafButton 
        variant="outline" 
        size="small" 
        onClick={() => checkStatus()}
      >
        Check Status
      </SafButton>
      <SafButton 
        variant="text" 
        size="small" 
        onClick={() => subscribe()}
      >
        Get Updates
      </SafButton>
    </div>
  </div>
</SafMessageBox>
```

### Multi-Action Complex Messages

```typescript
// React
const ComplexMessage = () => {
  const [selectedOption, setSelectedOption] = useState('');
  
  return (
    <SafMessageBox 
      variant="info" 
      title="Data Export Ready"
      dismissible
    >
      <div>
        <p>Your data export has been prepared. Choose how you'd like to receive it:</p>
        <SafRadioGroup 
          value={selectedOption} 
          onChange={setSelectedOption}
          style={{ margin: '12px 0' }}
        >
          <SafRadio value="download">Download immediately</SafRadio>
          <SafRadio value="email">Send to email</SafRadio>
          <SafRadio value="cloud">Save to cloud storage</SafRadio>
        </SafRadioGroup>
        <div style={{ display: 'flex', gap: '8px', marginTop: '12px' }}>
          <SafButton 
            disabled={!selectedOption}
            onClick={() => processExport(selectedOption)}
          >
            Proceed
          </SafButton>
          <SafButton 
            variant="outline" 
            onClick={() => cancelExport()}
          >
            Cancel
          </SafButton>
        </div>
      </div>
    </SafMessageBox>
  );
};
```

## Best Practices

### Message Clarity
- **Clear Titles**: Use descriptive, action-oriented titles
- **Concise Content**: Keep messages brief but informative
- **User Language**: Use terminology familiar to your users
- **Actionable Information**: Include clear next steps when appropriate

### Visual Hierarchy
- **Appropriate Variants**: Choose variants that match the message importance
- **Severity Levels**: Use severity to indicate urgency appropriately
- **Icon Usage**: Use icons to reinforce message meaning
- **Action Priority**: Order actions by importance and expected use

### User Experience
- **Dismissible Logic**: Make messages dismissible unless critical
- **Persistent Use**: Use persistent only for truly critical messages
- **Action Clarity**: Make action buttons clearly labeled
- **Feedback**: Provide feedback when actions are taken

### Content Strategy
- **Progressive Disclosure**: Use custom content for complex information
- **Error Guidance**: Provide specific guidance for error messages
- **Success Celebration**: Acknowledge successful actions appropriately
- **System Communication**: Keep users informed of system status

## Accessibility Considerations

- Uses appropriate ARIA roles and attributes for message regions
- Provides screen reader announcements for important messages
- Ensures sufficient color contrast for all variants and severity levels
- Supports keyboard navigation for actions and dismissal
- Maintains focus management when messages appear and disappear
- Respects user preferences for reduced motion

## Related Components

- **SafAlert**: Simpler alert component for basic notifications
- **SafToast**: Temporary notification component
- **SafModal**: Modal dialog for complex messages requiring user attention
- **SafBanner**: Page-level messaging component
- **SafStatus**: Status indicator component
- **SafNotification**: Push notification component

## Notes

- SafMessageBox automatically provides appropriate default icons for each variant
- Action buttons inherit the message box styling context
- Custom content through children overrides the message prop
- Severity levels affect visual emphasis but maintain variant color scheme
- Dismissible messages can be controlled programmatically
- The component supports rich content including forms, progress indicators, and other components
- Persistent messages prevent automatic dismissal but still allow manual dismissal if dismissible is true
