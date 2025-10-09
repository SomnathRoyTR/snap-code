# SafOverlay

## Overview

SafOverlay is a layout component that provides modal overlays and backdrop functionality for dialogs, popups, and other content that needs to appear above the main page content. It manages focus trapping, scroll locking, and proper z-index layering with accessibility support and customizable styling options.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `boolean` | `false` | Show/hide the overlay |
| `backdrop` | `boolean \| 'static'` | `true` | Show backdrop and click behavior |
| `closeOnBackdropClick` | `boolean` | `true` | Close when clicking backdrop |
| `closeOnEscapeKey` | `boolean` | `true` | Close when pressing Escape key |
| `trapFocus` | `boolean` | `true` | Trap focus within overlay |
| `restoreFocus` | `boolean` | `true` | Restore focus when closing |
| `lockScroll` | `boolean` | `true` | Lock body scroll when open |
| `zIndex` | `number` | `1000` | Z-index for overlay positioning |
| `backdropOpacity` | `number` | `0.5` | Backdrop opacity (0-1) |
| `backdropColor` | `string` | `'rgba(0,0,0,0.5)'` | Backdrop color |
| `backdropBlur` | `boolean` | `false` | Apply backdrop blur effect |
| `position` | `'center' \| 'top' \| 'bottom' \| 'left' \| 'right'` | `'center'` | Content positioning |
| `size` | `'auto' \| 'small' \| 'medium' \| 'large' \| 'fullscreen'` | `'auto'` | Content size preset |
| `maxWidth` | `string \| number` | - | Maximum width override |
| `maxHeight` | `string \| number` | - | Maximum height override |
| `padding` | `string \| number` | `24` | Content padding |
| `animation` | `'fade' \| 'slide' \| 'scale' \| 'none'` | `'fade'` | Entry/exit animation |
| `animationDuration` | `number` | `200` | Animation duration in ms |
| `preventClose` | `boolean` | `false` | Prevent all close interactions |
| `className` | `string` | - | Additional CSS classes |
| `backdropClassName` | `string` | - | Backdrop CSS classes |
| `contentClassName` | `string` | - | Content CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onShow` | `() => void` | Fired when overlay becomes visible |
| `onHide` | `() => void` | Fired when overlay becomes hidden |
| `onBackdropClick` | `(event: MouseEvent) => void` | Fired when backdrop is clicked |
| `onEscapeKey` | `(event: KeyboardEvent) => void` | Fired when Escape key is pressed |
| `onFocusTrap` | `(event: FocusEvent) => void` | Fired when focus is trapped |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `boolean` | `false` | Show/hide the overlay |
| `backdrop` | `boolean \| 'static'` | `true` | Show backdrop and click behavior |
| `closeOnBackdropClick` | `boolean` | `true` | Close when clicking backdrop |
| `closeOnEscapeKey` | `boolean` | `true` | Close when pressing Escape key |
| `trapFocus` | `boolean` | `true` | Trap focus within overlay |
| `restoreFocus` | `boolean` | `true` | Restore focus when closing |
| `lockScroll` | `boolean` | `true` | Lock body scroll when open |
| `zIndex` | `number` | `1000` | Z-index for overlay positioning |
| `backdropOpacity` | `number` | `0.5` | Backdrop opacity (0-1) |
| `backdropColor` | `string` | `'rgba(0,0,0,0.5)'` | Backdrop color |
| `backdropBlur` | `boolean` | `false` | Apply backdrop blur effect |
| `position` | `'center' \| 'top' \| 'bottom' \| 'left' \| 'right'` | `'center'` | Content positioning |
| `size` | `'auto' \| 'small' \| 'medium' \| 'large' \| 'fullscreen'` | `'auto'` | Content size preset |
| `maxWidth` | `string \| number` | - | Maximum width override |
| `maxHeight` | `string \| number` | - | Maximum height override |
| `padding` | `string \| number` | `24` | Content padding |
| `animation` | `'fade' \| 'slide' \| 'scale' \| 'none'` | `'fade'` | Entry/exit animation |
| `animationDuration` | `number` | `200` | Animation duration in ms |
| `preventClose` | `boolean` | `false` | Prevent all close interactions |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `show` | `EventEmitter<void>` | Fired when overlay becomes visible |
| `hide` | `EventEmitter<void>` | Fired when overlay becomes hidden |
| `backdropClick` | `EventEmitter<MouseEvent>` | Fired when backdrop is clicked |
| `escapeKey` | `EventEmitter<KeyboardEvent>` | Fired when Escape key is pressed |

## Usage Examples

### Basic Modal Overlay

```typescript
// React
const BasicModalOverlay = ({ isOpen, onClose }) => {
  return (
    <SafOverlay 
      visible={isOpen}
      onHide={onClose}
      onBackdropClick={onClose}
      closeOnEscapeKey
      trapFocus
      lockScroll
    >
      <div className="modal-content">
        <h2>Confirm Action</h2>
        <p>Are you sure you want to proceed with this action?</p>
        <div className="modal-actions">
          <SafButton variant="primary" onClick={onClose}>
            Confirm
          </SafButton>
          <SafButton variant="secondary" onClick={onClose}>
            Cancel
          </SafButton>
        </div>
      </div>
    </SafOverlay>
  );
};
```

```html
<!-- Angular -->
<saf-overlay 
  [visible]="isOpen"
  [closeOnBackdropClick]="true"
  [closeOnEscapeKey]="true"
  [trapFocus]="true"
  [lockScroll]="true"
  (hide)="onClose()">
  
  <div class="modal-content">
    <h2>Confirm Action</h2>
    <p>Are you sure you want to proceed with this action?</p>
    <div class="modal-actions">
      <saf-button variant="primary" (click)="onClose()">Confirm</saf-button>
      <saf-button variant="secondary" (click)="onClose()">Cancel</saf-button>
    </div>
  </div>
</saf-overlay>
```

### Full-Screen Overlay

```typescript
// React
const FullScreenOverlay = ({ isOpen, onClose, content }) => {
  return (
    <SafOverlay 
      visible={isOpen}
      size="fullscreen"
      animation="slide"
      backdropColor="rgba(0,0,0,0.8)"
      closeOnBackdropClick={false}
      onHide={onClose}
    >
      <div className="fullscreen-content">
        <header className="fullscreen-header">
          <h1>Full Screen View</h1>
          <SafButton 
            variant="ghost"
            icon={<SafIcon name="x" />}
            onClick={onClose}
            aria-label="Close"
          />
        </header>
        
        <main className="fullscreen-body">
          {content}
        </main>
      </div>
    </SafOverlay>
  );
};
```

### Side Panel Overlay

```typescript
// React
const SidePanelOverlay = ({ isOpen, onClose, position = 'right' }) => {
  return (
    <SafOverlay 
      visible={isOpen}
      position={position}
      size="medium"
      animation="slide"
      backdropOpacity={0.3}
      onHide={onClose}
      contentClassName={`side-panel side-panel--${position}`}
    >
      <div className="panel-header">
        <h3>Settings</h3>
        <SafButton 
          variant="ghost"
          size="small"
          icon={<SafIcon name="x" />}
          onClick={onClose}
        />
      </div>
      
      <div className="panel-content">
        <SafFieldset legend="Appearance">
          <SafRadioGroup name="theme">
            <SafRadio value="light">Light Theme</SafRadio>
            <SafRadio value="dark">Dark Theme</SafRadio>
          </SafRadioGroup>
        </SafFieldset>
        
        <SafFieldset legend="Notifications">
          <SafCheckbox>Email notifications</SafCheckbox>
          <SafCheckbox>Push notifications</SafCheckbox>
        </SafFieldset>
      </div>
      
      <div className="panel-footer">
        <SafButton variant="primary" onClick={onClose}>
          Save Changes
        </SafButton>
      </div>
    </SafOverlay>
  );
};
```

### Loading Overlay

```typescript
// React
const LoadingOverlay = ({ isLoading, message = 'Loading...' }) => {
  return (
    <SafOverlay 
      visible={isLoading}
      backdrop="static"
      closeOnBackdropClick={false}
      closeOnEscapeKey={false}
      trapFocus={false}
      backdropColor="rgba(255,255,255,0.8)"
      contentClassName="loading-overlay"
    >
      <div className="loading-content">
        <SafProgressRing size="large" />
        <p className="loading-message">{message}</p>
      </div>
    </SafOverlay>
  );
};
```

### Image Gallery Overlay

```typescript
// React
const ImageGalleryOverlay = ({ 
  isOpen, 
  images, 
  currentIndex, 
  onClose, 
  onPrevious, 
  onNext 
}) => {
  const handleKeyDown = (event) => {
    switch (event.key) {
      case 'ArrowLeft':
        onPrevious();
        break;
      case 'ArrowRight':
        onNext();
        break;
      case 'Escape':
        onClose();
        break;
    }
  };

  return (
    <SafOverlay 
      visible={isOpen}
      size="fullscreen"
      backdropColor="rgba(0,0,0,0.9)"
      animation="fade"
      onHide={onClose}
      onEscapeKey={onClose}
      contentClassName="gallery-overlay"
      onKeyDown={handleKeyDown}
    >
      <div className="gallery-container">
        <button 
          className="gallery-close"
          onClick={onClose}
          aria-label="Close gallery"
        >
          <SafIcon name="x" />
        </button>
        
        <button 
          className="gallery-nav gallery-prev"
          onClick={onPrevious}
          disabled={currentIndex === 0}
          aria-label="Previous image"
        >
          <SafIcon name="chevron-left" />
        </button>
        
        <div className="gallery-content">
          <img 
            src={images[currentIndex]?.src}
            alt={images[currentIndex]?.alt}
            className="gallery-image"
          />
          <div className="gallery-info">
            <p>{images[currentIndex]?.caption}</p>
            <span className="gallery-counter">
              {currentIndex + 1} of {images.length}
            </span>
          </div>
        </div>
        
        <button 
          className="gallery-nav gallery-next"
          onClick={onNext}
          disabled={currentIndex === images.length - 1}
          aria-label="Next image"
        >
          <SafIcon name="chevron-right" />
        </button>
      </div>
    </SafOverlay>
  );
};
```

### Animated Overlay

```typescript
// React
const AnimatedOverlay = ({ isOpen, onClose, animationType = 'scale' }) => {
  const [isAnimating, setIsAnimating] = useState(false);

  const handleShow = () => {
    setIsAnimating(true);
  };

  const handleHide = () => {
    setIsAnimating(false);
    setTimeout(() => onClose(), 200);
  };

  return (
    <SafOverlay 
      visible={isOpen}
      animation={animationType}
      animationDuration={300}
      backdropBlur
      onShow={handleShow}
      onHide={handleHide}
      contentClassName={`animated-overlay ${isAnimating ? 'animating' : ''}`}
    >
      <div className="animated-content">
        <div className="animation-demo">
          <SafIcon name="zap" size="large" />
          <h3>Animation Demo</h3>
          <p>This overlay demonstrates different animation types.</p>
        </div>
        
        <div className="animation-controls">
          <SafButton 
            variant="outline"
            onClick={() => setAnimationType('fade')}
          >
            Fade
          </SafButton>
          <SafButton 
            variant="outline"
            onClick={() => setAnimationType('scale')}
          >
            Scale
          </SafButton>
          <SafButton 
            variant="outline"
            onClick={() => setAnimationType('slide')}
          >
            Slide
          </SafButton>
        </div>
        
        <SafButton 
          variant="primary"
          onClick={handleHide}
        >
          Close
        </SafButton>
      </div>
    </SafOverlay>
  );
};
```

### Form Overlay

```typescript
// React
const FormOverlay = ({ isOpen, onClose, onSubmit, initialData }) => {
  const [formData, setFormData] = useState(initialData || {});
  const [errors, setErrors] = useState({});
  const [isSubmitting, setIsSubmitting] = useState(false);

  const validateForm = () => {
    const newErrors = {};
    
    if (!formData.name?.trim()) {
      newErrors.name = 'Name is required';
    }
    
    if (!formData.email?.trim()) {
      newErrors.email = 'Email is required';
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)) {
      newErrors.email = 'Invalid email format';
    }
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleSubmit = async (event) => {
    event.preventDefault();
    
    if (!validateForm()) return;
    
    setIsSubmitting(true);
    try {
      await onSubmit(formData);
      onClose();
    } catch (error) {
      setErrors({ submit: 'Failed to submit form' });
    } finally {
      setIsSubmitting(false);
    }
  };

  const handleFieldChange = (field, value) => {
    setFormData(prev => ({ ...prev, [field]: value }));
    if (errors[field]) {
      setErrors(prev => ({ ...prev, [field]: null }));
    }
  };

  return (
    <SafOverlay 
      visible={isOpen}
      size="medium"
      onHide={onClose}
      preventClose={isSubmitting}
    >
      <form onSubmit={handleSubmit} className="form-overlay">
        <header className="form-header">
          <h2>Edit Profile</h2>
          <SafButton 
            type="button"
            variant="ghost"
            icon={<SafIcon name="x" />}
            onClick={onClose}
            disabled={isSubmitting}
          />
        </header>
        
        <div className="form-body">
          <SafField>
            <SafLabel htmlFor="name" required>Name</SafLabel>
            <SafTextInput 
              id="name"
              value={formData.name || ''}
              onChange={(value) => handleFieldChange('name', value)}
              invalid={!!errors.name}
              disabled={isSubmitting}
            />
            {errors.name && (
              <SafFieldMessage type="error" message={errors.name} />
            )}
          </SafField>
          
          <SafField>
            <SafLabel htmlFor="email" required>Email</SafLabel>
            <SafTextInput 
              id="email"
              type="email"
              value={formData.email || ''}
              onChange={(value) => handleFieldChange('email', value)}
              invalid={!!errors.email}
              disabled={isSubmitting}
            />
            {errors.email && (
              <SafFieldMessage type="error" message={errors.email} />
            )}
          </SafField>
          
          <SafField>
            <SafLabel htmlFor="bio">Bio</SafLabel>
            <SafTextarea 
              id="bio"
              value={formData.bio || ''}
              onChange={(value) => handleFieldChange('bio', value)}
              rows={4}
              disabled={isSubmitting}
            />
          </SafField>
        </div>
        
        <footer className="form-footer">
          <SafButton 
            type="button"
            variant="secondary"
            onClick={onClose}
            disabled={isSubmitting}
          >
            Cancel
          </SafButton>
          <SafButton 
            type="submit"
            variant="primary"
            loading={isSubmitting}
          >
            Save Changes
          </SafButton>
        </footer>
        
        {errors.submit && (
          <SafAlert type="error" message={errors.submit} />
        )}
      </form>
    </SafOverlay>
  );
};
```

### Multi-Level Overlay

```typescript
// React
const MultiLevelOverlay = ({ level1Open, level2Open, onCloseLevel1, onCloseLevel2 }) => {
  return (
    <>
      {/* Level 1 Overlay */}
      <SafOverlay 
        visible={level1Open}
        zIndex={1000}
        onHide={onCloseLevel1}
        contentClassName="level-1-overlay"
      >
        <div className="overlay-content">
          <h2>Level 1 Overlay</h2>
          <p>This is the first overlay level.</p>
          
          <SafButton 
            variant="primary"
            onClick={() => setLevel2Open(true)}
          >
            Open Level 2
          </SafButton>
          
          <SafButton 
            variant="secondary"
            onClick={onCloseLevel1}
          >
            Close
          </SafButton>
        </div>
      </SafOverlay>
      
      {/* Level 2 Overlay */}
      <SafOverlay 
        visible={level2Open}
        zIndex={1100}
        size="small"
        onHide={onCloseLevel2}
        contentClassName="level-2-overlay"
      >
        <div className="overlay-content">
          <h3>Level 2 Overlay</h3>
          <p>This overlay appears on top of the first one.</p>
          
          <div className="overlay-actions">
            <SafButton 
              variant="primary"
              onClick={onCloseLevel2}
            >
              Done
            </SafButton>
          </div>
        </div>
      </SafOverlay>
    </>
  );
};
```

### Confirmation Overlay

```typescript
// React
const ConfirmationOverlay = ({ 
  isOpen, 
  onClose, 
  onConfirm,
  title,
  message,
  confirmText = 'Confirm',
  cancelText = 'Cancel',
  type = 'default'
}) => {
  const [isProcessing, setIsProcessing] = useState(false);

  const handleConfirm = async () => {
    setIsProcessing(true);
    try {
      await onConfirm();
      onClose();
    } catch (error) {
      console.error('Confirmation failed:', error);
    } finally {
      setIsProcessing(false);
    }
  };

  const getIcon = () => {
    const icons = {
      warning: 'alert-triangle',
      error: 'alert-circle',
      info: 'info',
      success: 'check-circle'
    };
    return icons[type] || 'help-circle';
  };

  const getColor = () => {
    const colors = {
      warning: 'orange',
      error: 'red',
      info: 'blue',
      success: 'green'
    };
    return colors[type] || 'gray';
  };

  return (
    <SafOverlay 
      visible={isOpen}
      size="small"
      onHide={onClose}
      preventClose={isProcessing}
      contentClassName={`confirmation-overlay confirmation-overlay--${type}`}
    >
      <div className="confirmation-content">
        <div className="confirmation-icon">
          <SafIcon 
            name={getIcon()} 
            size="large" 
            color={getColor()}
          />
        </div>
        
        <div className="confirmation-text">
          <h3>{title}</h3>
          <p>{message}</p>
        </div>
        
        <div className="confirmation-actions">
          <SafButton 
            variant="secondary"
            onClick={onClose}
            disabled={isProcessing}
          >
            {cancelText}
          </SafButton>
          <SafButton 
            variant={type === 'error' ? 'danger' : 'primary'}
            onClick={handleConfirm}
            loading={isProcessing}
          >
            {confirmText}
          </SafButton>
        </div>
      </div>
    </SafOverlay>
  );
};
```

### Mobile-Optimized Overlay

```typescript
// React
const MobileOptimizedOverlay = ({ isOpen, onClose, children }) => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return (
    <SafOverlay 
      visible={isOpen}
      size={isMobile ? 'fullscreen' : 'medium'}
      position={isMobile ? 'bottom' : 'center'}
      animation={isMobile ? 'slide' : 'scale'}
      backdropOpacity={isMobile ? 0.3 : 0.5}
      padding={isMobile ? 0 : 24}
      onHide={onClose}
      contentClassName={`responsive-overlay ${isMobile ? 'mobile' : 'desktop'}`}
    >
      {isMobile && (
        <div className="mobile-handle">
          <div className="handle-bar" />
        </div>
      )}
      
      <div className="overlay-header">
        <h2>Responsive Overlay</h2>
        <SafButton 
          variant="ghost"
          icon={<SafIcon name="x" />}
          onClick={onClose}
        />
      </div>
      
      <div className="overlay-content">
        {children}
      </div>
      
      {isMobile && (
        <div className="mobile-footer">
          <SafButton 
            variant="primary"
            size="large"
            fullWidth
            onClick={onClose}
          >
            Done
          </SafButton>
        </div>
      )}
    </SafOverlay>
  );
};
```

## Best Practices

### User Experience
- **Clear Purpose**: Use overlays for focused tasks or important messages
- **Easy Dismissal**: Provide multiple ways to close overlays
- **Appropriate Size**: Choose overlay size based on content and context
- **Visual Hierarchy**: Ensure overlay content has clear visual structure

### Accessibility
- **Focus Management**: Trap focus within overlay and restore on close
- **Keyboard Support**: Support Escape key and proper tab navigation
- **Screen Reader Support**: Provide proper ARIA attributes and announcements
- **Color Contrast**: Ensure sufficient contrast for backdrop and content

### Performance
- **Lazy Loading**: Load overlay content only when needed
- **Animation Performance**: Use CSS animations and avoid complex JavaScript
- **Memory Management**: Clean up event listeners and resources
- **Z-Index Management**: Properly layer multiple overlays

### Mobile Experience
- **Touch Gestures**: Support swipe-to-close gestures where appropriate
- **Safe Areas**: Respect device safe areas and notches
- **Viewport Handling**: Handle virtual keyboard and orientation changes
- **Performance**: Optimize for mobile rendering performance

## Accessibility Considerations

- Uses proper ARIA roles and attributes including `dialog` and `presentation`
- Traps focus within overlay content and restores focus on close
- Supports comprehensive keyboard navigation including Escape key
- Provides proper screen reader announcements for state changes
- Maintains accessible color contrast for backdrop and content
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafModal**: High-level modal dialog component
- **SafDrawer**: Side panel overlay component
- **SafPopover**: Lightweight overlay for contextual content
- **SafTooltip**: Small overlay for help text
- **SafDialog**: Accessible dialog wrapper

## Notes

- SafOverlay automatically manages focus trapping and restoration
- The component handles scroll locking to prevent background scrolling
- Z-index management allows for multiple overlay layers
- Animation support provides smooth enter/exit transitions
- Backdrop behavior is configurable for different interaction patterns
- The component works seamlessly with form validation and submission
- Mobile optimizations ensure good touch device experience
- Proper cleanup prevents memory leaks and event listener issues
