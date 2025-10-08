# SafClickAwayListener

A utility component that detects clicks outside of its contained elements and fires an event when such clicks occur. SafClickAwayListener is essential for implementing dropdowns, modals, popover menus, and other overlay components that need to close when users click elsewhere.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |
| `children` | `ReactNode` | - | The content to wrap with click-away detection |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClickAway` | `(event: CustomEvent<EventTarget[]>) => void` | Fires when a click occurs outside the component. Event detail contains the composed path of the click event |

### Examples

#### Basic Dropdown Menu
```jsx
import { SafClickAwayListener, SafButton, SafMenu, SafMenuItem } from '@saffron/core-components/react';

function DropdownWithClickAway() {
  const [isOpen, setIsOpen] = useState(false);

  const handleClickAway = (event) => {
    // Close dropdown when clicking outside
    setIsOpen(false);
    console.log('Clicked outside, path:', event.detail);
  };

  return (
    <div>
      <SafButton onClick={() => setIsOpen(!isOpen)}>
        {isOpen ? 'Close Menu' : 'Open Menu'}
      </SafButton>
      
      {isOpen && (
        <SafClickAwayListener onClickAway={handleClickAway}>
          <SafMenu 
            style={{ 
              position: 'absolute', 
              backgroundColor: 'white', 
              border: '1px solid #ccc',
              marginTop: '4px' 
            }}>
            <SafMenuItem>Option 1</SafMenuItem>
            <SafMenuItem>Option 2</SafMenuItem>
            <SafMenuItem>Option 3</SafMenuItem>
          </SafMenu>
        </SafClickAwayListener>
      )}
    </div>
  );
}
```

#### Modal Dialog with Click-Away
```jsx
import { SafClickAwayListener, SafButton, SafCard } from '@saffron/core-components/react';

function ModalWithClickAway() {
  const [showModal, setShowModal] = useState(false);

  const handleClickAway = () => {
    // Only close if clicking on the backdrop, not the modal content
    setShowModal(false);
  };

  if (!showModal) {
    return (
      <SafButton onClick={() => setShowModal(true)}>
        Open Modal
      </SafButton>
    );
  }

  return (
    <div 
      style={{
        position: 'fixed',
        top: 0,
        left: 0,
        right: 0,
        bottom: 0,
        backgroundColor: 'rgba(0, 0, 0, 0.5)',
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        zIndex: 1000
      }}>
      <SafClickAwayListener onClickAway={handleClickAway}>
        <SafCard style={{ maxWidth: '400px', padding: '24px' }}>
          <h2>Modal Title</h2>
          <p>Click outside this modal to close it.</p>
          <SafButton onClick={() => setShowModal(false)}>
            Close Modal
          </SafButton>
        </SafCard>
      </SafClickAwayListener>
    </div>
  );
}
```

#### Complex Nested Component
```jsx
import { SafClickAwayListener, SafButton, SafTextField } from '@saffron/core-components/react';

function NestedClickAwayExample() {
  const [showForm, setShowForm] = useState(false);
  const [formData, setFormData] = useState({ name: '', email: '' });

  const handleClickAway = (event) => {
    // Optional: Only close if form is empty or confirmed
    const shouldClose = !formData.name && !formData.email;
    
    if (shouldClose) {
      setShowForm(false);
    } else {
      // Ask for confirmation before closing
      const confirmed = window.confirm('Are you sure you want to close? Unsaved changes will be lost.');
      if (confirmed) {
        setShowForm(false);
        setFormData({ name: '', email: '' });
      }
    }
  };

  return (
    <div>
      <SafButton onClick={() => setShowForm(true)}>
        Show Form
      </SafButton>
      
      {showForm && (
        <div style={{ marginTop: '16px' }}>
          <SafClickAwayListener onClickAway={handleClickAway}>
            <div 
              style={{
                border: '1px solid #ccc',
                padding: '16px',
                borderRadius: '4px',
                backgroundColor: 'white'
              }}>
              <h3>User Information</h3>
              
              <SafTextField
                label="Name"
                value={formData.name}
                onChange={(e) => setFormData(prev => ({ ...prev, name: e.target.value }))}
              />
              
              <SafTextField
                label="Email"
                type="email"
                value={formData.email}
                onChange={(e) => setFormData(prev => ({ ...prev, email: e.target.value }))}
              />
              
              <div style={{ marginTop: '16px' }}>
                <SafButton 
                  appearance="primary" 
                  onClick={() => {
                    console.log('Saving:', formData);
                    setShowForm(false);
                    setFormData({ name: '', email: '' });
                  }}>
                  Save
                </SafButton>
                
                <SafButton 
                  appearance="secondary" 
                  onClick={() => setShowForm(false)}
                  style={{ marginLeft: '8px' }}>
                  Cancel
                </SafButton>
              </div>
            </div>
          </SafClickAwayListener>
        </div>
      )}
    </div>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |

### Events

| Output | Type | Description |
|--------|------|-------------|
| `clickAway` | `EventEmitter<CustomEvent<EventTarget[]>>` | Fires when a click occurs outside the component. Event detail contains the composed path of the click event |

### Examples

#### Basic Dropdown Menu
```html
<div>
  <saf-button (click)="toggleMenu()">
    {{ isOpen ? 'Close Menu' : 'Open Menu' }}
  </saf-button>
  
  <saf-click-away-listener 
    *ngIf="isOpen"
    (clickAway)="handleClickAway($event)">
    <saf-menu 
      [style]="{ 
        position: 'absolute', 
        backgroundColor: 'white', 
        border: '1px solid #ccc',
        marginTop: '4px' 
      }">
      <saf-menu-item>Option 1</saf-menu-item>
      <saf-menu-item>Option 2</saf-menu-item>
      <saf-menu-item>Option 3</saf-menu-item>
    </saf-menu>
  </saf-click-away-listener>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-dropdown-click-away',
  templateUrl: './dropdown-click-away.component.html'
})
export class DropdownClickAwayComponent {
  isOpen = false;

  toggleMenu() {
    this.isOpen = !this.isOpen;
  }

  handleClickAway(event: CustomEvent<EventTarget[]>) {
    // Close dropdown when clicking outside
    this.isOpen = false;
    console.log('Clicked outside, path:', event.detail);
  }
}
```

#### Modal Dialog with Click-Away
```html
<saf-button *ngIf="!showModal" (click)="openModal()">
  Open Modal
</saf-button>

<div 
  *ngIf="showModal"
  class="modal-backdrop">
  <saf-click-away-listener (clickAway)="closeModal()">
    <saf-card class="modal-content">
      <h2>Modal Title</h2>
      <p>Click outside this modal to close it.</p>
      <saf-button (click)="closeModal()">
        Close Modal
      </saf-button>
    </saf-card>
  </saf-click-away-listener>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-modal-click-away',
  templateUrl: './modal-click-away.component.html',
  styleUrls: ['./modal-click-away.component.scss']
})
export class ModalClickAwayComponent {
  showModal = false;

  openModal() {
    this.showModal = true;
  }

  closeModal() {
    this.showModal = false;
  }
}
```

```scss
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  max-width: 400px;
  padding: 24px;
}
```

#### Form with Conditional Close
```html
<div>
  <saf-button (click)="showForm = true">
    Show Form
  </saf-button>
  
  <div *ngIf="showForm" class="form-container">
    <saf-click-away-listener (clickAway)="handleFormClickAway()">
      <div class="form-wrapper">
        <h3>User Information</h3>
        
        <saf-text-field
          label="Name"
          [(ngModel)]="formData.name">
        </saf-text-field>
        
        <saf-text-field
          label="Email"
          type="email"
          [(ngModel)]="formData.email">
        </saf-text-field>
        
        <div class="form-actions">
          <saf-button 
            appearance="primary" 
            (click)="saveForm()">
            Save
          </saf-button>
          
          <saf-button 
            appearance="secondary" 
            (click)="cancelForm()">
            Cancel
          </saf-button>
        </div>
      </div>
    </saf-click-away-listener>
  </div>
</div>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-form-click-away',
  templateUrl: './form-click-away.component.html',
  styleUrls: ['./form-click-away.component.scss']
})
export class FormClickAwayComponent {
  showForm = false;
  formData = { name: '', email: '' };

  handleFormClickAway() {
    // Optional: Only close if form is empty or confirmed
    const shouldClose = !this.formData.name && !this.formData.email;
    
    if (shouldClose) {
      this.showForm = false;
    } else {
      // Ask for confirmation before closing
      const confirmed = window.confirm('Are you sure you want to close? Unsaved changes will be lost.');
      if (confirmed) {
        this.showForm = false;
        this.formData = { name: '', email: '' };
      }
    }
  }

  saveForm() {
    console.log('Saving:', this.formData);
    this.showForm = false;
    this.formData = { name: '', email: '' };
  }

  cancelForm() {
    this.showForm = false;
    this.formData = { name: '', email: '' };
  }
}
```

```scss
.form-container {
  margin-top: 16px;
}

.form-wrapper {
  border: 1px solid #ccc;
  padding: 16px;
  border-radius: 4px;
  background-color: white;
}

.form-actions {
  margin-top: 16px;
  
  saf-button + saf-button {
    margin-left: 8px;
  }
}
```

## Best Practices

- **Use for overlay components**: Ideal for dropdowns, tooltips, modals, and any floating content that should close when clicking outside.
- **Combine with escape key handling**: Consider adding keyboard event listeners for the Escape key alongside click-away behavior.
- **Handle edge cases**: Consider whether to close immediately or ask for confirmation when users have unsaved changes.
- **Test event propagation**: Ensure child elements don't interfere with click detection by testing event bubbling.
- **Performance considerations**: The component uses document-level event listeners, so use sparingly for better performance.
- **Accessibility**: Always provide alternative ways to close overlays (like a close button) for users who can't use mouse interactions.
- **Consider nested scenarios**: Be careful when nesting multiple click-away listeners to avoid unexpected behavior.

## Notes

- SafClickAwayListener uses `composedPath()` to detect clicks, which works correctly with Shadow DOM and event bubbling.
- The component automatically adds and removes event listeners when connected/disconnected from the DOM.
- Event listeners are attached to the document level, so they capture clicks anywhere on the page.
- The component is invisible and acts as a wrapper around its children without adding visual styling.
- Click events that originate from child elements will not trigger the click-away event.
- Use this component judiciously as each instance adds a document-level event listener.
