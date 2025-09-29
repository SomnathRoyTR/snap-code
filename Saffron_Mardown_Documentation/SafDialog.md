# SafDialog

A modal or non-modal dialog component that overlays content on the page, commonly used for confirmations, forms, detailed information, or other focused interactions.

## Usage

```html
<saf-dialog dialog-title="Confirm Action">
  Are you sure you want to delete this item?
  <div slot="footer">
    <saf-button appearance="neutral">Cancel</saf-button>
    <saf-button appearance="accent">Delete</saf-button>
  </div>
</saf-dialog>
```

## API

### SafDialog

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `dialog-title` | `string` | - | The main title displayed in the dialog header |
| `dialog-subtitle` | `string` | - | Optional subtitle displayed below the title |
| `modal` | `boolean` | `true` | Whether the dialog should be modal (blocks interaction with page) |
| `hidden` | `boolean` | `true` | Whether the dialog is currently hidden |
| `is-alert` | `boolean` | `false` | Whether dialog should use `alertdialog` role for urgent messages |
| `is-header` | `boolean` | `true` | Whether to show the dialog header |
| `is-footer` | `boolean` | `false` | Whether to show the dialog footer |
| `no-focus-trap` | `boolean` | `false` | Whether to disable focus trapping within the dialog |

#### Accessibility Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `a11y-aria-label` | `string` | - | ARIA label for the dialog (use when no title) |
| `close-aria-label` | `string` | `'Close'` | ARIA label for the close button |
| `aria-title-level` | `1-6` | `2` | Heading level for the dialog title |
| `aria-subtitle-level` | `1-6` | `3` | Heading level for the dialog subtitle |
| `aria-describedby` | `string` | - | ID of element describing the dialog |
| `aria-labelledby` | `string` | - | ID of element labeling the dialog |

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `triggerElement` | `HTMLElement \| null` | Element that triggered the dialog (for focus return) |

#### Methods

| Name | Parameters | Description |
|------|------------|-------------|
| `show()` | - | Show the dialog |
| `hide()` | - | Hide the dialog |
| `dismiss()` | - | Dismiss the dialog (emits cancel event) |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `show` | `CustomEvent` | Fires when the dialog is shown |
| `hide` | `CustomEvent` | Fires when the dialog is hidden |
| `cancel` | `CustomEvent` | Fires when the dialog is dismissed (overlay click, ESC) |

#### Slots

| Name | Description |
|------|-------------|
| default | Main dialog content |
| `subheader` | Content below the title/subtitle in the header |
| `footer` | Footer content (buttons, actions) |

#### Parts

| Name | Description |
|------|-------------|
| `overlay` | The modal overlay background |
| `control` | The main dialog container |
| `dialog-header-wrapper` | Container for the entire header area |
| `dialog-headings` | Container for title and subtitle |
| `dialog-title` | The dialog title element |
| `dialog-subtitle` | The dialog subtitle element |
| `close` | The close button |
| `subheader` | The subheader content area |
| `content` | The main content area |
| `footer` | The footer content area |

## Examples

### Basic Confirmation Dialog

```html
<saf-dialog id="confirm-dialog" dialog-title="Confirm Delete" is-footer>
  <p>Are you sure you want to delete this item? This action cannot be undone.</p>
  
  <div slot="footer">
    <saf-button appearance="neutral" onclick="document.getElementById('confirm-dialog').hide()">
      Cancel
    </saf-button>
    <saf-button appearance="accent" onclick="deleteItem()">
      Delete
    </saf-button>
  </div>
</saf-dialog>

<saf-button onclick="document.getElementById('confirm-dialog').show()">
  Delete Item
</saf-button>
```

### Form Dialog

```html
<saf-dialog id="form-dialog" dialog-title="Add New User" dialog-subtitle="Enter user details" is-footer>
  <form id="user-form">
    <saf-text-field label="First Name" name="firstName" required></saf-text-field>
    <saf-text-field label="Last Name" name="lastName" required></saf-text-field>
    <saf-text-field label="Email" name="email" type="email" required></saf-text-field>
    <saf-select label="Role" name="role" required>
      <saf-option value="user">User</saf-option>
      <saf-option value="admin">Admin</saf-option>
      <saf-option value="moderator">Moderator</saf-option>
    </saf-select>
  </form>
  
  <div slot="footer">
    <saf-button appearance="neutral" onclick="cancelForm()">Cancel</saf-button>
    <saf-button appearance="accent" onclick="submitForm()">Create User</saf-button>
  </div>
</saf-dialog>
```

### Alert Dialog

```html
<saf-dialog id="error-dialog" dialog-title="Error" is-alert is-footer>
  <div style="display: flex; align-items: flex-start; gap: 12px;">
    <saf-icon icon-name="hexagon-exclamation" appearance="solid" color="var(--saf-color-status-error-strong)"></saf-icon>
    <div>
      <p><strong>Failed to save changes</strong></p>
      <p>The server is currently unavailable. Please try again later or contact support if the problem persists.</p>
    </div>
  </div>
  
  <div slot="footer">
    <saf-button appearance="accent" onclick="document.getElementById('error-dialog').hide()">
      OK
    </saf-button>
  </div>
</saf-dialog>
```

### Non-Modal Dialog

```html
<saf-dialog id="info-panel" dialog-title="Additional Information" modal="false">
  <div style="max-height: 300px; overflow-y: auto;">
    <h3>Product Specifications</h3>
    <ul>
      <li>Weight: 2.5 lbs</li>
      <li>Dimensions: 12" x 8" x 3"</li>
      <li>Color: Available in black, white, or silver</li>
      <li>Warranty: 2 year limited warranty</li>
    </ul>
    
    <h3>Features</h3>
    <ul>
      <li>Advanced processing capabilities</li>
      <li>Energy efficient design</li>
      <li>Wireless connectivity</li>
      <li>User-friendly interface</li>
    </ul>
  </div>
</saf-dialog>
```

### Dialog with Subheader

```html
<saf-dialog id="settings-dialog" dialog-title="Account Settings" dialog-subtitle="Manage your preferences" is-footer>
  <div slot="subheader" style="padding: 8px 0; border-bottom: 1px solid #e1e5e9;">
    <saf-badge appearance="informational">Premium Account</saf-badge>
  </div>
  
  <div style="display: grid; gap: 16px; margin-top: 16px;">
    <div>
      <label style="display: flex; align-items: center; gap: 8px;">
        <input type="checkbox" checked>
        <span>Email notifications</span>
      </label>
    </div>
    <div>
      <label style="display: flex; align-items: center; gap: 8px;">
        <input type="checkbox">
        <span>SMS notifications</span>
      </label>
    </div>
    <div>
      <label style="display: flex; align-items: center; gap: 8px;">
        <input type="checkbox" checked>
        <span>Weekly digest</span>
      </label>
    </div>
  </div>
  
  <div slot="footer">
    <saf-button appearance="neutral" onclick="document.getElementById('settings-dialog').hide()">
      Cancel
    </saf-button>
    <saf-button appearance="accent" onclick="saveSettings()">
      Save Settings
    </saf-button>
  </div>
</saf-dialog>
```

### Dialog without Header

```html
<saf-dialog id="minimal-dialog" is-header="false" a11y-aria-label="Image viewer">
  <div style="text-align: center;">
    <img src="/api/placeholder/400/300" alt="Sample image" style="max-width: 100%; height: auto;">
    <p style="margin-top: 16px;">Sample Image Description</p>
  </div>
</saf-dialog>
```

### Loading Dialog

```html
<saf-dialog id="loading-dialog" dialog-title="Processing..." hide-close-button no-focus-trap>
  <div style="display: flex; align-items: center; gap: 16px; padding: 20px;">
    <saf-spinner></saf-spinner>
    <div>
      <p>Please wait while we process your request...</p>
      <p style="color: #666; font-size: 0.875rem;">This may take a few moments.</p>
    </div>
  </div>
</saf-dialog>
```

### Multi-step Dialog

```html
<saf-dialog id="wizard-dialog" dialog-title="Setup Wizard" dialog-subtitle="Step 1 of 3" is-footer>
  <div id="step-content">
    <h3>Welcome</h3>
    <p>This wizard will help you set up your account. Let's get started!</p>
    <saf-text-field label="Organization Name" required></saf-text-field>
  </div>
  
  <div slot="footer">
    <saf-button id="prev-btn" appearance="neutral" disabled>Previous</saf-button>
    <saf-button id="next-btn" appearance="accent">Next</saf-button>
  </div>
</saf-dialog>
```

### Event Handling Examples

```html
<saf-dialog id="event-dialog" dialog-title="Event Example">
  <p>This dialog demonstrates various event handling.</p>
</saf-dialog>

<div>
  <saf-button onclick="showDialog()">Show Dialog</saf-button>
  <saf-button onclick="hideDialog()">Hide Dialog</saf-button>
</div>

<script>
  const dialog = document.getElementById('event-dialog');

  // Listen for show event
  dialog.addEventListener('show', () => {
    console.log('Dialog shown');
  });

  // Listen for hide event
  dialog.addEventListener('hide', () => {
    console.log('Dialog hidden');
  });

  // Listen for cancel event (ESC key or overlay click)
  dialog.addEventListener('cancel', () => {
    console.log('Dialog cancelled');
  });

  function showDialog() {
    dialog.show();
  }

  function hideDialog() {
    dialog.hide();
  }

  function submitForm() {
    const form = document.getElementById('user-form');
    const formData = new FormData(form);
    
    // Simulate form submission
    console.log('Submitting form:', Object.fromEntries(formData));
    
    // Hide dialog after successful submission
    document.getElementById('form-dialog').hide();
  }

  function cancelForm() {
    // Reset form and hide dialog
    document.getElementById('user-form').reset();
    document.getElementById('form-dialog').hide();
  }
</script>
```

### Focus Management Example

```html
<saf-dialog id="focus-dialog" dialog-title="Focus Management">
  <p>Tab through these elements to see focus trapping in action:</p>
  
  <saf-text-field label="First Field"></saf-text-field>
  <saf-text-field label="Second Field"></saf-text-field>
  
  <div style="margin: 16px 0;">
    <saf-button appearance="neutral">Button 1</saf-button>
    <saf-button appearance="neutral">Button 2</saf-button>
  </div>
  
  <saf-text-field label="Last Field"></saf-text-field>
</saf-dialog>

<!-- Dialog with focus trapping disabled -->
<saf-dialog id="no-trap-dialog" dialog-title="No Focus Trap" no-focus-trap>
  <p>This dialog does not trap focus, allowing you to tab to elements outside the dialog.</p>
  <saf-text-field label="Test Field"></saf-text-field>
</saf-dialog>
```

## Framework Integration

### React

```jsx
import { SafDialog, SafButton, SafTextField } from '@saffron/core-components-react';
import { useState, useRef } from 'react';

function DialogExample() {
  const [isOpen, setIsOpen] = useState(false);
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });
  const dialogRef = useRef();

  const handleShow = () => {
    if (dialogRef.current) {
      dialogRef.current.show();
      setIsOpen(true);
    }
  };

  const handleHide = () => {
    if (dialogRef.current) {
      dialogRef.current.hide();
      setIsOpen(false);
    }
  };

  const handleSubmit = () => {
    console.log('Form submitted:', formData);
    handleHide();
    // Reset form
    setFormData({ name: '', email: '', message: '' });
  };

  const handleCancel = () => {
    // Ask for confirmation if form has data
    const hasData = Object.values(formData).some(value => value.trim());
    if (hasData && !confirm('Are you sure you want to cancel? Your changes will be lost.')) {
      return;
    }
    handleHide();
  };

  return (
    <div>
      <SafButton appearance="accent" onClick={handleShow}>
        Open Contact Form
      </SafButton>

      <SafDialog
        ref={dialogRef}
        dialogTitle="Contact Us"
        dialogSubtitle="We'd love to hear from you"
        isFooter={true}
        onHide={() => setIsOpen(false)}
        onCancel={handleCancel}
      >
        <div style={{ display: 'grid', gap: '16px' }}>
          <SafTextField
            label="Name"
            value={formData.name}
            onChange={(e) => setFormData(prev => ({ ...prev, name: e.target.value }))}
            required
          />
          <SafTextField
            label="Email"
            type="email"
            value={formData.email}
            onChange={(e) => setFormData(prev => ({ ...prev, email: e.target.value }))}
            required
          />
          <saf-textarea
            label="Message"
            value={formData.message}
            onChange={(e) => setFormData(prev => ({ ...prev, message: e.target.value }))}
            rows={4}
          />
        </div>

        <div slot="footer">
          <SafButton appearance="neutral" onClick={handleCancel}>
            Cancel
          </SafButton>
          <SafButton 
            appearance="accent" 
            onClick={handleSubmit}
            disabled={!formData.name || !formData.email}
          >
            Send Message
          </SafButton>
        </div>
      </SafDialog>
    </div>
  );
}
```

### Angular

```typescript
// component.ts
import { Component, ViewChild, ElementRef } from '@angular/core';

interface DialogData {
  title: string;
  content: string;
  confirmText: string;
  cancelText: string;
}

@Component({
  selector: 'app-dialog-demo',
  template: `
    <div class="dialog-triggers">
      <button (click)="showConfirmation()">Show Confirmation</button>
      <button (click)="showForm()">Show Form</button>
      <button (click)="showAlert()">Show Alert</button>
    </div>

    <!-- Confirmation Dialog -->
    <saf-dialog
      #confirmDialog
      [dialog-title]="confirmData.title"
      is-footer="true"
      (hide)="onDialogHide()"
      (cancel)="onDialogCancel()"
    >
      <p [innerHTML]="confirmData.content"></p>
      
      <div slot="footer">
        <saf-button appearance="neutral" (click)="hideConfirmDialog()">
          {{ confirmData.cancelText }}
        </saf-button>
        <saf-button appearance="accent" (click)="confirmAction()">
          {{ confirmData.confirmText }}
        </saf-button>
      </div>
    </saf-dialog>

    <!-- Form Dialog -->
    <saf-dialog
      #formDialog
      dialog-title="User Information"
      dialog-subtitle="Please fill out the form"
      is-footer="true"
    >
      <form #userForm="ngForm" (ngSubmit)="submitForm()">
        <div class="form-fields">
          <saf-text-field
            label="First Name"
            name="firstName"
            [(ngModel)]="userData.firstName"
            required
          ></saf-text-field>
          
          <saf-text-field
            label="Last Name"
            name="lastName"
            [(ngModel)]="userData.lastName"
            required
          ></saf-text-field>
          
          <saf-text-field
            label="Email"
            name="email"
            type="email"
            [(ngModel)]="userData.email"
            required
            email
          ></saf-text-field>
        </div>
      </form>

      <div slot="footer">
        <saf-button appearance="neutral" (click)="cancelForm()">
          Cancel
        </saf-button>
        <saf-button 
          appearance="accent" 
          [disabled]="!userForm.valid"
          (click)="submitForm()"
        >
          Save
        </saf-button>
      </div>
    </saf-dialog>

    <!-- Alert Dialog -->
    <saf-dialog
      #alertDialog
      dialog-title="Important Notice"
      is-alert="true"
      is-footer="true"
    >
      <div class="alert-content">
        <saf-icon icon-name="triangle-exclamation" appearance="solid"></saf-icon>
        <div>
          <p><strong>System Maintenance</strong></p>
          <p>The system will be down for maintenance from 2:00 AM to 4:00 AM EST.</p>
        </div>
      </div>

      <div slot="footer">
        <saf-button appearance="accent" (click)="hideAlertDialog()">
          I Understand
        </saf-button>
      </div>
    </saf-dialog>
  `,
  styles: [`
    .dialog-triggers {
      display: flex;
      gap: 12px;
      margin-bottom: 20px;
    }
    .form-fields {
      display: grid;
      gap: 16px;
    }
    .alert-content {
      display: flex;
      align-items: flex-start;
      gap: 12px;
    }
  `]
})
export class DialogDemoComponent {
  @ViewChild('confirmDialog') confirmDialog!: ElementRef;
  @ViewChild('formDialog') formDialog!: ElementRef;
  @ViewChild('alertDialog') alertDialog!: ElementRef;

  confirmData: DialogData = {
    title: 'Confirm Delete',
    content: 'Are you sure you want to delete this item? This action cannot be undone.',
    confirmText: 'Delete',
    cancelText: 'Cancel'
  };

  userData = {
    firstName: '',
    lastName: '',
    email: ''
  };

  showConfirmation() {
    this.confirmDialog.nativeElement.show();
  }

  showForm() {
    this.formDialog.nativeElement.show();
  }

  showAlert() {
    this.alertDialog.nativeElement.show();
  }

  hideConfirmDialog() {
    this.confirmDialog.nativeElement.hide();
  }

  hideFormDialog() {
    this.formDialog.nativeElement.hide();
  }

  hideAlertDialog() {
    this.alertDialog.nativeElement.hide();
  }

  confirmAction() {
    console.log('Action confirmed');
    this.hideConfirmDialog();
    // Perform the confirmed action here
  }

  submitForm() {
    if (this.userData.firstName && this.userData.lastName && this.userData.email) {
      console.log('Form submitted:', this.userData);
      this.hideFormDialog();
      // Reset form
      this.userData = { firstName: '', lastName: '', email: '' };
    }
  }

  cancelForm() {
    this.hideFormDialog();
    // Reset form
    this.userData = { firstName: '', lastName: '', email: '' };
  }

  onDialogHide() {
    console.log('Dialog hidden');
  }

  onDialogCancel() {
    console.log('Dialog cancelled');
  }
}
```

## Accessibility Features

- **ARIA Dialog Pattern**: Implements the complete WAI-ARIA dialog pattern
- **Focus Management**: Automatically traps focus within the dialog and returns to trigger element
- **Keyboard Navigation**: 
  - `Escape`: Closes the dialog
  - `Tab`: Cycles through focusable elements within dialog
- **Screen Reader Support**: Proper labeling with `aria-labelledby`, `aria-describedby`
- **Alert Dialogs**: Special `alertdialog` role for urgent messages
- **Heading Levels**: Configurable heading levels for proper document structure

## Best Practices

1. **Use Appropriate Roles**: Use `is-alert` for urgent messages that need immediate attention
2. **Meaningful Titles**: Provide clear, descriptive titles that explain the dialog's purpose
3. **Focus Management**: Always ensure proper focus handling for keyboard users
4. **Modal vs Non-Modal**: Use modal dialogs for critical decisions, non-modal for supplementary info
5. **Action Buttons**: Place primary action on the right, secondary on the left
6. **Content Scrolling**: Keep content concise or handle long content with scrolling
7. **Responsive Design**: Ensure dialogs work well on different screen sizes
8. **Loading States**: Show appropriate loading indicators for async operations

## Related Components

- `saf-popover`: For lightweight contextual overlays
- `saf-tooltip`: For brief explanatory overlays
- `saf-alert`: For inline status messages
- `saf-drawer`: For slide-out panels
- `saf-modal`: For simpler modal overlays (if available)
