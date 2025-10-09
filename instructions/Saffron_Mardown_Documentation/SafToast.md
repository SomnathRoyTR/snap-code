# SafToast Component

## Overview

SafToast is a notification component that displays brief, dismissible messages to users. It provides contextual feedback about actions, system status, or important information through temporary overlays that appear at designated positions on the screen. SafToast supports different severity levels, positioning options, auto-dismiss functionality, and action buttons for enhanced user interaction.

## React API

### SafToast

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `message` | `string \| ReactNode` | Yes | - | Toast message content |
| `variant` | `'success' \| 'error' \| 'warning' \| 'info'` | No | `'info'` | Toast severity/type |
| `position` | `'top-left' \| 'top-center' \| 'top-right' \| 'bottom-left' \| 'bottom-center' \| 'bottom-right'` | No | `'top-right'` | Toast positioning |
| `duration` | `number \| 'persistent'` | No | `5000` | Auto-dismiss duration in ms or persistent |
| `closable` | `boolean` | No | `true` | Whether toast can be manually dismissed |
| `showIcon` | `boolean` | No | `true` | Whether to show variant icon |
| `icon` | `string \| ReactNode` | No | - | Custom icon override |
| `actions` | `ToastAction[]` | No | - | Action buttons for toast |
| `progress` | `boolean` | No | `false` | Whether to show progress bar |
| `multiline` | `boolean` | No | `false` | Whether to allow multiline content |
| `maxWidth` | `string` | No | `'400px'` | Maximum width of toast |
| `animation` | `'slide' \| 'fade' \| 'bounce'` | No | `'slide'` | Toast animation type |
| `pauseOnHover` | `boolean` | No | `true` | Whether to pause auto-dismiss on hover |
| `stackLimit` | `number` | No | `3` | Maximum number of stacked toasts |
| `onDismiss` | `() => void` | No | - | Callback when toast is dismissed |
| `onAction` | `(actionId: string) => void` | No | - | Callback when action is clicked |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### ToastAction Interface

```typescript
interface ToastAction {
  id: string;
  label: string;
  variant?: 'primary' | 'secondary' | 'ghost';
  disabled?: boolean;
}
```

### Toast Provider

```typescript
// Toast context provider for global toast management
const ToastProvider = ({ children, config?: ToastConfig }) => JSX.Element;

interface ToastConfig {
  position?: ToastPosition;
  maxToasts?: number;
  defaultDuration?: number;
  animations?: boolean;
}

// Hook for toast management
const useToast = () => {
  const showToast: (config: ToastConfig) => string;
  const dismissToast: (id: string) => void;
  const dismissAll: () => void;
}
```

## Angular API

### saf-toast

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[message]` | `string \| TemplateRef` | Yes | - | Toast message content |
| `[variant]` | `'success' \| 'error' \| 'warning' \| 'info'` | No | `'info'` | Toast severity/type |
| `[position]` | `'top-left' \| 'top-center' \| 'top-right' \| 'bottom-left' \| 'bottom-center' \| 'bottom-right'` | No | `'top-right'` | Toast positioning |
| `[duration]` | `number \| 'persistent'` | No | `5000` | Auto-dismiss duration in ms or persistent |
| `[closable]` | `boolean` | No | `true` | Whether toast can be manually dismissed |
| `[showIcon]` | `boolean` | No | `true` | Whether to show variant icon |
| `[icon]` | `string \| TemplateRef` | No | - | Custom icon override |
| `[actions]` | `ToastAction[]` | No | - | Action buttons for toast |
| `[progress]` | `boolean` | No | `false` | Whether to show progress bar |
| `[multiline]` | `boolean` | No | `false` | Whether to allow multiline content |
| `[maxWidth]` | `string` | No | `'400px'` | Maximum width of toast |
| `[animation]` | `'slide' \| 'fade' \| 'bounce'` | No | `'slide'` | Toast animation type |
| `[pauseOnHover]` | `boolean` | No | `true` | Whether to pause auto-dismiss on hover |
| `[stackLimit]` | `number` | No | `3` | Maximum number of stacked toasts |
| `(dismiss)` | `EventEmitter<void>` | No | - | Event when toast is dismissed |
| `(actionClick)` | `EventEmitter<string>` | No | - | Event when action is clicked |

### Toast Service

```typescript
// Injectable service for global toast management
@Injectable({ providedIn: 'root' })
export class ToastService {
  showSuccess(message: string, config?: Partial<ToastConfig>): string;
  showError(message: string, config?: Partial<ToastConfig>): string;
  showWarning(message: string, config?: Partial<ToastConfig>): string;
  showInfo(message: string, config?: Partial<ToastConfig>): string;
  dismiss(id: string): void;
  dismissAll(): void;
}
```

## Usage Examples

### Basic Toast Notifications

#### React
```jsx
import { SafToast, SafButton, useToast } from '@saffron/react';

const BasicToastExample = () => {
  const { showToast } = useToast();

  const showSuccessToast = () => {
    showToast({
      message: 'Operation completed successfully!',
      variant: 'success',
      duration: 4000
    });
  };

  const showErrorToast = () => {
    showToast({
      message: 'An error occurred while processing your request.',
      variant: 'error',
      duration: 6000
    });
  };

  const showWarningToast = () => {
    showToast({
      message: 'Please review your input before proceeding.',
      variant: 'warning',
      duration: 5000
    });
  };

  const showInfoToast = () => {
    showToast({
      message: 'New feature available in settings.',
      variant: 'info',
      duration: 4000
    });
  };

  return (
    <div className="toast-demo">
      <h2>Toast Notifications</h2>
      <div className="button-group">
        <SafButton onClick={showSuccessToast} variant="success">
          Show Success
        </SafButton>
        <SafButton onClick={showErrorToast} variant="danger">
          Show Error
        </SafButton>
        <SafButton onClick={showWarningToast} variant="warning">
          Show Warning
        </SafButton>
        <SafButton onClick={showInfoToast} variant="primary">
          Show Info
        </SafButton>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// basic-toast.component.ts
import { Component } from '@angular/core';
import { ToastService } from '@saffron/angular';

@Component({
  selector: 'app-basic-toast',
  template: `
    <div class="toast-demo">
      <h2>Toast Notifications</h2>
      <div class="button-group">
        <saf-button (click)="showSuccessToast()" variant="success">
          Show Success
        </saf-button>
        <saf-button (click)="showErrorToast()" variant="danger">
          Show Error
        </saf-button>
        <saf-button (click)="showWarningToast()" variant="warning">
          Show Warning
        </saf-button>
        <saf-button (click)="showInfoToast()" variant="primary">
          Show Info
        </saf-button>
      </div>
    </div>
  `
})
export class BasicToastComponent {
  constructor(private toastService: ToastService) {}

  showSuccessToast() {
    this.toastService.showSuccess(
      'Operation completed successfully!',
      { duration: 4000 }
    );
  }

  showErrorToast() {
    this.toastService.showError(
      'An error occurred while processing your request.',
      { duration: 6000 }
    );
  }

  showWarningToast() {
    this.toastService.showWarning(
      'Please review your input before proceeding.',
      { duration: 5000 }
    );
  }

  showInfoToast() {
    this.toastService.showInfo(
      'New feature available in settings.',
      { duration: 4000 }
    );
  }
}
```

### Toast with Actions

#### React
```jsx
import { SafToast, SafButton, useToast } from '@saffron/react';

const ActionToastExample = () => {
  const { showToast } = useToast();

  const showUndoToast = () => {
    showToast({
      message: 'Item deleted from your library',
      variant: 'info',
      duration: 8000,
      actions: [
        {
          id: 'undo',
          label: 'Undo',
          variant: 'primary'
        },
        {
          id: 'view',
          label: 'View Trash',
          variant: 'secondary'
        }
      ],
      onAction: (actionId) => {
        if (actionId === 'undo') {
          console.log('Undo action triggered');
          showToast({
            message: 'Item restored successfully',
            variant: 'success',
            duration: 3000
          });
        } else if (actionId === 'view') {
          console.log('Navigate to trash');
        }
      }
    });
  };

  const showConfirmationToast = () => {
    showToast({
      message: 'Do you want to save your changes before leaving?',
      variant: 'warning',
      duration: 'persistent',
      actions: [
        {
          id: 'save',
          label: 'Save',
          variant: 'primary'
        },
        {
          id: 'discard',
          label: 'Discard',
          variant: 'secondary'
        }
      ],
      onAction: (actionId) => {
        if (actionId === 'save') {
          console.log('Saving changes');
        } else if (actionId === 'discard') {
          console.log('Discarding changes');
        }
      }
    });
  };

  return (
    <div className="action-toast-demo">
      <h2>Interactive Toast Notifications</h2>
      <div className="button-group">
        <SafButton onClick={showUndoToast}>
          Delete Item (with Undo)
        </SafButton>
        <SafButton onClick={showConfirmationToast}>
          Show Confirmation
        </SafButton>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// action-toast.component.ts
import { Component } from '@angular/core';
import { ToastService } from '@saffron/angular';

@Component({
  selector: 'app-action-toast',
  template: `
    <div class="action-toast-demo">
      <h2>Interactive Toast Notifications</h2>
      <div class="button-group">
        <saf-button (click)="showUndoToast()">
          Delete Item (with Undo)
        </saf-button>
        <saf-button (click)="showConfirmationToast()">
          Show Confirmation
        </saf-button>
      </div>
    </div>
  `
})
export class ActionToastComponent {
  constructor(private toastService: ToastService) {}

  showUndoToast() {
    const toastId = this.toastService.show({
      message: 'Item deleted from your library',
      variant: 'info',
      duration: 8000,
      actions: [
        {
          id: 'undo',
          label: 'Undo',
          variant: 'primary'
        },
        {
          id: 'view',
          label: 'View Trash',
          variant: 'secondary'
        }
      ]
    });

    // Handle action clicks
    this.toastService.onAction(toastId).subscribe(actionId => {
      if (actionId === 'undo') {
        console.log('Undo action triggered');
        this.toastService.showSuccess('Item restored successfully', { duration: 3000 });
      } else if (actionId === 'view') {
        console.log('Navigate to trash');
      }
    });
  }

  showConfirmationToast() {
    const toastId = this.toastService.show({
      message: 'Do you want to save your changes before leaving?',
      variant: 'warning',
      duration: 'persistent',
      actions: [
        {
          id: 'save',
          label: 'Save',
          variant: 'primary'
        },
        {
          id: 'discard',
          label: 'Discard',
          variant: 'secondary'
        }
      ]
    });

    this.toastService.onAction(toastId).subscribe(actionId => {
      if (actionId === 'save') {
        console.log('Saving changes');
      } else if (actionId === 'discard') {
        console.log('Discarding changes');
      }
    });
  }
}
```

### Positioned Toast Stack

#### React
```jsx
import { SafToast, SafButton, ToastProvider, useToast } from '@saffron/react';

const PositionedToastExample = () => {
  const { showToast } = useToast();

  const positions = [
    'top-left', 'top-center', 'top-right',
    'bottom-left', 'bottom-center', 'bottom-right'
  ];

  const showPositionedToast = (position) => {
    showToast({
      message: `Toast positioned at ${position}`,
      variant: 'info',
      position: position,
      duration: 4000
    });
  };

  const showStackedToasts = () => {
    const messages = [
      'First notification in stack',
      'Second notification in stack',
      'Third notification in stack',
      'Fourth notification in stack'
    ];

    messages.forEach((message, index) => {
      setTimeout(() => {
        showToast({
          message: message,
          variant: index % 2 === 0 ? 'info' : 'success',
          duration: 6000
        });
      }, index * 500);
    });
  };

  return (
    <div className="positioned-toast-demo">
      <h2>Toast Positioning</h2>
      <div className="position-grid">
        {positions.map(position => (
          <SafButton
            key={position}
            onClick={() => showPositionedToast(position)}
            variant="outline"
            size="small"
          >
            {position}
          </SafButton>
        ))}
      </div>
      <SafButton onClick={showStackedToasts} variant="primary">
        Show Stacked Toasts
      </SafButton>
    </div>
  );
};

// Wrap with ToastProvider
const App = () => (
  <ToastProvider config={{ maxToasts: 4, position: 'top-right' }}>
    <PositionedToastExample />
  </ToastProvider>
);
```

#### Angular
```typescript
// positioned-toast.component.ts
import { Component } from '@angular/core';
import { ToastService } from '@saffron/angular';

@Component({
  selector: 'app-positioned-toast',
  template: `
    <div class="positioned-toast-demo">
      <h2>Toast Positioning</h2>
      <div class="position-grid">
        <saf-button 
          *ngFor="let position of positions"
          (click)="showPositionedToast(position)"
          variant="outline"
          size="small">
          {{ position }}
        </saf-button>
      </div>
      <saf-button (click)="showStackedToasts()" variant="primary">
        Show Stacked Toasts
      </saf-button>
    </div>
  `
})
export class PositionedToastComponent {
  positions = [
    'top-left', 'top-center', 'top-right',
    'bottom-left', 'bottom-center', 'bottom-right'
  ];

  constructor(private toastService: ToastService) {}

  showPositionedToast(position: string) {
    this.toastService.show({
      message: `Toast positioned at ${position}`,
      variant: 'info',
      position: position as any,
      duration: 4000
    });
  }

  showStackedToasts() {
    const messages = [
      'First notification in stack',
      'Second notification in stack',
      'Third notification in stack',
      'Fourth notification in stack'
    ];

    messages.forEach((message, index) => {
      setTimeout(() => {
        this.toastService.show({
          message: message,
          variant: index % 2 === 0 ? 'info' : 'success',
          duration: 6000
        });
      }, index * 500);
    });
  }
}
```

### Progress and Rich Content Toast

#### React
```jsx
import { SafToast, SafButton, SafIcon, useToast } from '@saffron/react';
import { useState } from 'react';

const RichToastExample = () => {
  const { showToast } = useToast();
  const [uploadProgress, setUploadProgress] = useState(0);

  const showProgressToast = () => {
    const toastId = showToast({
      message: 'Uploading files...',
      variant: 'info',
      duration: 'persistent',
      progress: true,
      icon: <SafIcon name="upload" />
    });

    // Simulate upload progress
    let progress = 0;
    const interval = setInterval(() => {
      progress += 10;
      setUploadProgress(progress);
      
      if (progress >= 100) {
        clearInterval(interval);
        showToast({
          message: 'Upload completed successfully!',
          variant: 'success',
          duration: 3000,
          icon: <SafIcon name="check-circle" />
        });
      }
    }, 300);
  };

  const showRichContentToast = () => {
    showToast({
      message: (
        <div className="rich-toast-content">
          <div className="toast-header">
            <SafIcon name="bell" />
            <strong>New Message</strong>
          </div>
          <div className="toast-body">
            <p>You have received a new message from <strong>John Doe</strong></p>
            <p className="timestamp">2 minutes ago</p>
          </div>
        </div>
      ),
      variant: 'info',
      duration: 8000,
      multiline: true,
      maxWidth: '350px',
      actions: [
        {
          id: 'reply',
          label: 'Reply',
          variant: 'primary'
        },
        {
          id: 'mark-read',
          label: 'Mark as Read',
          variant: 'secondary'
        }
      ]
    });
  };

  const showPersistentToast = () => {
    showToast({
      message: 'System maintenance scheduled for tonight at 11 PM. Save your work before then.',
      variant: 'warning',
      duration: 'persistent',
      multiline: true,
      actions: [
        {
          id: 'remind',
          label: 'Remind Me',
          variant: 'primary'
        },
        {
          id: 'details',
          label: 'View Details',
          variant: 'secondary'
        }
      ]
    });
  };

  return (
    <div className="rich-toast-demo">
      <h2>Rich Content Toasts</h2>
      <div className="button-group">
        <SafButton onClick={showProgressToast}>
          Show Progress Toast
        </SafButton>
        <SafButton onClick={showRichContentToast}>
          Show Rich Content
        </SafButton>
        <SafButton onClick={showPersistentToast}>
          Show Persistent Toast
        </SafButton>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// rich-toast.component.ts
import { Component } from '@angular/core';
import { ToastService } from '@saffron/angular';

@Component({
  selector: 'app-rich-toast',
  template: `
    <div class="rich-toast-demo">
      <h2>Rich Content Toasts</h2>
      <div class="button-group">
        <saf-button (click)="showProgressToast()">
          Show Progress Toast
        </saf-button>
        <saf-button (click)="showRichContentToast()">
          Show Rich Content
        </saf-button>
        <saf-button (click)="showPersistentToast()">
          Show Persistent Toast
        </saf-button>
      </div>
    </div>

    <!-- Rich content template -->
    <ng-template #richContent>
      <div class="rich-toast-content">
        <div class="toast-header">
          <saf-icon name="bell"></saf-icon>
          <strong>New Message</strong>
        </div>
        <div class="toast-body">
          <p>You have received a new message from <strong>John Doe</strong></p>
          <p class="timestamp">2 minutes ago</p>
        </div>
      </div>
    </ng-template>
  `
})
export class RichToastComponent {
  uploadProgress = 0;

  constructor(private toastService: ToastService) {}

  showProgressToast() {
    const toastId = this.toastService.show({
      message: 'Uploading files...',
      variant: 'info',
      duration: 'persistent',
      progress: true,
      icon: 'upload'
    });

    // Simulate upload progress
    let progress = 0;
    const interval = setInterval(() => {
      progress += 10;
      this.uploadProgress = progress;
      
      if (progress >= 100) {
        clearInterval(interval);
        this.toastService.dismiss(toastId);
        this.toastService.showSuccess('Upload completed successfully!', {
          duration: 3000,
          icon: 'check-circle'
        });
      }
    }, 300);
  }

  showRichContentToast() {
    this.toastService.show({
      message: this.richContent,
      variant: 'info',
      duration: 8000,
      multiline: true,
      maxWidth: '350px',
      actions: [
        {
          id: 'reply',
          label: 'Reply',
          variant: 'primary'
        },
        {
          id: 'mark-read',
          label: 'Mark as Read',
          variant: 'secondary'
        }
      ]
    });
  }

  showPersistentToast() {
    this.toastService.show({
      message: 'System maintenance scheduled for tonight at 11 PM. Save your work before then.',
      variant: 'warning',
      duration: 'persistent',
      multiline: true,
      actions: [
        {
          id: 'remind',
          label: 'Remind Me',
          variant: 'primary'
        },
        {
          id: 'details',
          label: 'View Details',
          variant: 'secondary'
        }
      ]
    });
  }
}
```

### Custom Styled Toast

#### React
```jsx
import { SafToast, SafButton, useToast } from '@saffron/react';

const CustomStyledToastExample = () => {
  const { showToast } = useToast();

  const showCustomToast = () => {
    showToast({
      message: 'Custom styled toast with enhanced branding',
      variant: 'info',
      duration: 5000,
      animation: 'bounce',
      className: 'custom-branded-toast',
      icon: '🎉',
      actions: [
        {
          id: 'celebrate',
          label: 'Celebrate!',
          variant: 'primary'
        }
      ]
    });
  };

  const showMinimalToast = () => {
    showToast({
      message: 'Clean, minimal notification',
      variant: 'success',
      duration: 3000,
      showIcon: false,
      closable: false,
      animation: 'fade',
      className: 'minimal-toast'
    });
  };

  return (
    <div className="custom-toast-demo">
      <h2>Custom Styled Toasts</h2>
      <div className="button-group">
        <SafButton onClick={showCustomToast}>
          Show Custom Toast
        </SafButton>
        <SafButton onClick={showMinimalToast}>
          Show Minimal Toast
        </SafButton>
      </div>

      <style jsx>{`
        .custom-branded-toast {
          background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
          color: white;
          border: none;
          box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
        }
        
        .minimal-toast {
          background: #f8f9fa;
          border: 1px solid #e9ecef;
          color: #495057;
          box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }
      `}</style>
    </div>
  );
};
```

#### Angular
```typescript
// custom-styled-toast.component.ts
import { Component } from '@angular/core';
import { ToastService } from '@saffron/angular';

@Component({
  selector: 'app-custom-styled-toast',
  template: `
    <div class="custom-toast-demo">
      <h2>Custom Styled Toasts</h2>
      <div class="button-group">
        <saf-button (click)="showCustomToast()">
          Show Custom Toast
        </saf-button>
        <saf-button (click)="showMinimalToast()">
          Show Minimal Toast
        </saf-button>
      </div>
    </div>
  `,
  styles: [`
    :host ::ng-deep .custom-branded-toast {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border: none;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
    }
    
    :host ::ng-deep .minimal-toast {
      background: #f8f9fa;
      border: 1px solid #e9ecef;
      color: #495057;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }
  `]
})
export class CustomStyledToastComponent {
  constructor(private toastService: ToastService) {}

  showCustomToast() {
    this.toastService.show({
      message: 'Custom styled toast with enhanced branding',
      variant: 'info',
      duration: 5000,
      animation: 'bounce',
      className: 'custom-branded-toast',
      icon: '🎉',
      actions: [
        {
          id: 'celebrate',
          label: 'Celebrate!',
          variant: 'primary'
        }
      ]
    });
  }

  showMinimalToast() {
    this.toastService.show({
      message: 'Clean, minimal notification',
      variant: 'success',
      duration: 3000,
      showIcon: false,
      closable: false,
      animation: 'fade',
      className: 'minimal-toast'
    });
  }
}
```

## Best Practices

1. **Message Clarity**
   - Use clear, concise language for toast messages
   - Provide specific context about what happened
   - Include actionable next steps when appropriate

2. **Duration Management**
   - Use shorter durations (3-4s) for success messages
   - Use longer durations (6-8s) for error messages
   - Use persistent toasts for critical messages requiring action

3. **Visual Hierarchy**
   - Use appropriate variants based on message importance
   - Limit the number of concurrent toasts
   - Position toasts to avoid interfering with primary content

4. **Action Design**
   - Provide meaningful action buttons for actionable messages
   - Use primary actions for the most important response
   - Limit actions to 2-3 buttons maximum

5. **Accessibility**
   - Ensure toast messages are announced by screen readers
   - Provide sufficient time for users to read and act
   - Make dismiss and action buttons keyboard accessible

## Accessibility Considerations

1. **ARIA Support**
   - Use `role="alert"` for important notifications
   - Use `role="status"` for less critical updates
   - Implement `aria-live` regions for dynamic content

2. **Keyboard Navigation**
   - Support Tab navigation through action buttons
   - Enable Escape key to dismiss toasts
   - Provide keyboard shortcuts for common actions

3. **Screen Reader Compatibility**
   - Announce toast content when displayed
   - Provide context about toast type and actions
   - Use semantic markup for toast structure

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all variants
   - Provide icon alternatives for color-blind users
   - Support high contrast and reduced motion preferences

5. **Timing Considerations**
   - Allow users to extend auto-dismiss timing
   - Pause timers when screen reader is active
   - Provide manual dismiss options for all toasts

## Related Components

- **SafAlert**: Static alert messages for persistent information
- **SafDialog**: Modal dialogs for complex interactions
- **SafIcon**: Icons for toast visual indicators
- **SafButton**: Action buttons within toasts
- **SafProgressBar**: Progress indicators for long-running operations

## Notes

- Toast notifications automatically stack and manage positioning
- Custom CSS variables available for theming toast appearance
- Built-in debouncing prevents duplicate toast notifications
- Supports both imperative and declarative usage patterns
- Compatible with SSR frameworks and hydration
- Optimized for performance with minimal DOM manipulation
- Toast state persists across route changes when using global providers
