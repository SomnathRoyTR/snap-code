# SafResponsiveElement Mixin

The `SafResponsiveElement` is a base class mixin that provides responsive behavior capabilities to components in the Saffron Design System. Built on FAST Element, it uses ResizeObserver to detect viewport changes and automatically adjusts component behavior between desktop and mobile modes.

## Table of Contents

- [Overview](#overview)
- [Mixin Properties](#mixin-properties)
- [Events](#events)
- [Methods](#methods)
- [Configuration](#configuration)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Components Using This Mixin](#components-using-this-mixin)
- [Best Practices](#best-practices)

## Overview

The SafResponsiveElement mixin is designed to be applied to components that need to adapt their behavior based on viewport width. It provides automatic mode detection (desktop vs mobile) and emits events when the mode changes, allowing components to implement responsive behaviors.

Key Features:
- **Automatic Mode Detection**: Observes parent element width to determine desktop/mobile mode
- **ResizeObserver Integration**: Efficient viewport change detection
- **Configurable Breakpoints**: Customizable breakpoint and threshold values
- **Event Emission**: Notifies when mode changes occur
- **Performance Optimized**: Throttled observations to prevent excessive firing
- **Easy Integration**: Simple mixin pattern for existing components

## Mixin Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `mode` | `'desktop' \| 'mobile'` | `'mobile'` | Current responsive mode (read-only) |
| `resizeObserver` | `ResizeObserver \| undefined` | `undefined` | ResizeObserver instance |

### Private Properties

| Property | Type | Description |
|----------|------|-------------|
| `_mode` | `'desktop' \| 'mobile'` | Internal mode state |
| `_modeChanged` | `function` | Mode change handler function |

## Events

| Event | Bubbles | Cancelable | Detail | Description |
|-------|---------|------------|--------|-------------|
| `mode-change` | `true` | `false` | `string` | Fired when responsive mode changes |

## Methods

### Configuration Methods

```typescript
// Initialize responsiveness with optional configuration
initializeResponsiveness(config?: CreateResizeObserverConfig): void

// Create a ResizeObserver with configuration
createResizeObserver(config?: CreateResizeObserverConfig): ResizeObserver

// Disconnect the ResizeObserver
disconnectResizeObserver(): void
```

### Property Accessors

```typescript
// Get current mode (read-only)
get mode(): 'desktop' | 'mobile'

// Throws error if attempt to set mode directly
set mode(_: 'desktop' | 'mobile'): never
```

## Configuration

The `CreateResizeObserverConfig` interface allows customization of responsive behavior:

```typescript
interface CreateResizeObserverConfig {
  threshold?: number;    // Default: 5px
  breakpoint?: number;   // Default: 480px
}
```

### Configuration Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `threshold` | `number` | `5` | Minimum width change (px) before firing mode change |
| `breakpoint` | `number` | `480` | Width (px) below which component enters mobile mode |

## React Integration

### Basic Mixin Usage

```tsx
// Note: SafResponsiveElement is a mixin, not a standalone component
// It's used internally by components like SafWizard and SafStepper

import SafWizard from '@saffron/react/wizard';
import { useState, useEffect } from 'react';

function ResponsiveWizardExample() {
  const [wizardMode, setWizardMode] = useState<'desktop' | 'mobile'>('desktop');
  
  const handleModeChange = (event: CustomEvent) => {
    setWizardMode(event.detail);
  };
  
  return (
    <SafWizard 
      onModeChange={handleModeChange}
      className={`wizard-${wizardMode}`}
    >
      {/* Wizard steps */}
    </SafWizard>
  );
}
```

### Creating Custom Responsive Component

```tsx
// Example of creating a custom component using ResponsiveElement pattern
import { FASTElement, observable } from '@microsoft/fast-element';
import { ResponsiveElement } from '@saffron/core/responsive-element';

class CustomResponsiveComponent extends FASTElement {
  @observable
  public content: string = '';
  
  connectedCallback() {
    super.connectedCallback();
    // Initialize responsiveness with custom breakpoint
    this.initializeResponsiveness({ 
      breakpoint: 768,  // Custom breakpoint
      threshold: 10     // Custom threshold
    });
  }
  
  disconnectedCallback() {
    super.disconnectedCallback();
    this.disconnectResizeObserver();
  }
  
  private handleModeChange = (mode: 'desktop' | 'mobile') => {
    // Custom responsive behavior
    if (mode === 'mobile') {
      this.classList.add('mobile-layout');
    } else {
      this.classList.remove('mobile-layout');
    }
  };
}

// Apply the mixin
Object.assign(CustomResponsiveComponent.prototype, ResponsiveElement.prototype);
```

### Listening to Mode Changes

```tsx
import SafStepper from '@saffron/react/stepper';
import { useEffect, useState } from 'react';

function ResponsiveStepperExample() {
  const [stepperRef, setStepperRef] = useState<HTMLElement | null>(null);
  const [currentMode, setCurrentMode] = useState<'desktop' | 'mobile'>('desktop');
  
  useEffect(() => {
    if (!stepperRef) return;
    
    const handleModeChange = (event: CustomEvent) => {
      setCurrentMode(event.detail);
      console.log('Stepper mode changed to:', event.detail);
    };
    
    stepperRef.addEventListener('mode-change', handleModeChange);
    
    return () => {
      stepperRef.removeEventListener('mode-change', handleModeChange);
    };
  }, [stepperRef]);
  
  return (
    <div>
      <p>Current mode: {currentMode}</p>
      <SafStepper ref={setStepperRef}>
        {/* Stepper content */}
      </SafStepper>
    </div>
  );
}
```

## Angular Integration

### Basic Mixin Usage

```typescript
// Note: ResponsiveElement is used internally by components
// like saf-wizard and saf-stepper

import { Component } from '@angular/core';

@Component({
  selector: 'app-responsive-wizard',
  template: `
    <saf-wizard 
      (mode-change)="onModeChange($event)"
      [class]="'wizard-' + currentMode">
      <!-- Wizard steps -->
    </saf-wizard>
  `
})
export class ResponsiveWizardComponent {
  currentMode: 'desktop' | 'mobile' = 'desktop';
  
  onModeChange(event: CustomEvent) {
    this.currentMode = event.detail;
    console.log('Wizard mode changed to:', this.currentMode);
  }
}
```

### Custom Responsive Service

```typescript
import { Injectable, ElementRef } from '@angular/core';
import { BehaviorSubject, Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ResponsiveService {
  private modeSubject = new BehaviorSubject<'desktop' | 'mobile'>('desktop');
  public mode$: Observable<'desktop' | 'mobile'> = this.modeSubject.asObservable();
  
  private resizeObserver?: ResizeObserver;
  
  initializeResponsiveness(
    element: ElementRef,
    config: { threshold?: number; breakpoint?: number } = {}
  ) {
    const { threshold = 5, breakpoint = 480 } = config;
    let previousWidth = 0;
    
    this.resizeObserver = new ResizeObserver((entries) => {
      const parent = entries[0];
      
      if (Math.abs(parent.contentRect.width - previousWidth) > threshold) {
        const isNarrow = parent.contentRect.width < breakpoint;
        const newMode = isNarrow ? 'mobile' : 'desktop';
        this.modeSubject.next(newMode);
        previousWidth = parent.contentRect.width;
      }
    });
    
    this.resizeObserver.observe(element.nativeElement.parentElement!);
    
    // Initialize mode
    const initialWidth = element.nativeElement.parentElement!.getBoundingClientRect().width;
    const initialMode = initialWidth < breakpoint ? 'mobile' : 'desktop';
    this.modeSubject.next(initialMode);
  }
  
  disconnect() {
    this.resizeObserver?.disconnect();
  }
}
```

### Component with Responsive Service

```typescript
import { Component, ElementRef, OnInit, OnDestroy } from '@angular/core';
import { ResponsiveService } from './responsive.service';

@Component({
  selector: 'app-custom-responsive',
  template: `
    <div class="responsive-container" [class.mobile]="isMobile">
      <saf-stepper (mode-change)="onModeChange($event)">
        <!-- Stepper content adapts based on mode -->
      </saf-stepper>
      
      <div class="content">
        <p>Current mode: {{ currentMode }}</p>
        <p>Mobile layout: {{ isMobile ? 'Yes' : 'No' }}</p>
      </div>
    </div>
  `
})
export class CustomResponsiveComponent implements OnInit, OnDestroy {
  currentMode: 'desktop' | 'mobile' = 'desktop';
  
  get isMobile() {
    return this.currentMode === 'mobile';
  }
  
  constructor(
    private elementRef: ElementRef,
    private responsiveService: ResponsiveService
  ) {}
  
  ngOnInit() {
    // Initialize custom responsiveness
    this.responsiveService.initializeResponsiveness(this.elementRef, {
      breakpoint: 768,
      threshold: 10
    });
    
    // Subscribe to mode changes
    this.responsiveService.mode$.subscribe(mode => {
      this.currentMode = mode;
    });
  }
  
  ngOnDestroy() {
    this.responsiveService.disconnect();
  }
  
  onModeChange(event: CustomEvent) {
    this.currentMode = event.detail;
  }
}
```

### Responsive Layout Directive

```typescript
import { 
  Directive, 
  ElementRef, 
  OnInit, 
  OnDestroy, 
  Output, 
  EventEmitter,
  Input 
} from '@angular/core';

@Directive({
  selector: '[responsiveElement]'
})
export class ResponsiveElementDirective implements OnInit, OnDestroy {
  @Input() breakpoint: number = 480;
  @Input() threshold: number = 5;
  @Output() modeChange = new EventEmitter<'desktop' | 'mobile'>();
  
  private resizeObserver?: ResizeObserver;
  private currentMode: 'desktop' | 'mobile' = 'mobile';
  
  constructor(private elementRef: ElementRef) {}
  
  ngOnInit() {
    this.initializeResponsiveness();
  }
  
  ngOnDestroy() {
    this.resizeObserver?.disconnect();
  }
  
  private initializeResponsiveness() {
    let previousWidth = 0;
    
    this.resizeObserver = new ResizeObserver((entries) => {
      const parent = entries[0];
      
      if (Math.abs(parent.contentRect.width - previousWidth) > this.threshold) {
        const isNarrow = parent.contentRect.width < this.breakpoint;
        const newMode = isNarrow ? 'mobile' : 'desktop';
        
        if (newMode !== this.currentMode) {
          this.currentMode = newMode;
          this.modeChange.emit(newMode);
        }
        
        previousWidth = parent.contentRect.width;
      }
    });
    
    // Observe parent element
    const parentElement = this.elementRef.nativeElement.parentElement;
    if (parentElement) {
      this.resizeObserver.observe(parentElement);
      
      // Initialize mode
      const initialWidth = parentElement.getBoundingClientRect().width;
      this.currentMode = initialWidth < this.breakpoint ? 'mobile' : 'desktop';
      this.modeChange.emit(this.currentMode);
    }
  }
}
```

## Usage Examples

### Components Using ResponsiveElement

```html
<!-- SafWizard with responsive behavior -->
<saf-wizard id="responsive-wizard">
  <saf-wizard-step-content step="1">
    Step 1 content
  </saf-wizard-step-content>
  <saf-wizard-step-content step="2">
    Step 2 content
  </saf-wizard-step-content>
</saf-wizard>

<!-- SafStepper with responsive behavior -->
<saf-stepper id="responsive-stepper">
  <saf-step>Step 1</saf-step>
  <saf-step>Step 2</saf-step>
  <saf-step>Step 3</saf-step>
</saf-stepper>
```

### JavaScript Integration

```javascript
// Listen for mode changes
const wizard = document.getElementById('responsive-wizard');

wizard.addEventListener('mode-change', (event) => {
  const mode = event.detail;
  console.log('Wizard mode changed to:', mode);
  
  // Apply responsive styling or behavior
  if (mode === 'mobile') {
    wizard.classList.add('mobile-layout');
  } else {
    wizard.classList.remove('mobile-layout');
  }
});

// Check current mode
console.log('Current wizard mode:', wizard.mode);
```

### Custom Responsive Behavior

```javascript
// Create a custom component with ResponsiveElement behavior
class CustomResponsiveComponent extends HTMLElement {
  constructor() {
    super();
    this.resizeObserver = null;
    this._mode = 'mobile';
  }
  
  connectedCallback() {
    this.initializeResponsiveness({
      breakpoint: 600,
      threshold: 8
    });
  }
  
  disconnectedCallback() {
    this.disconnectResizeObserver();
  }
  
  initializeResponsiveness(config = {}) {
    const { threshold = 5, breakpoint = 480 } = config;
    let previousWidth = 0;
    
    setTimeout(() => {
      this.resizeObserver = new ResizeObserver((entries) => {
        const parent = entries[0];
        
        if (Math.abs(parent.contentRect.width - previousWidth) > threshold) {
          const isNarrow = parent.contentRect.width < breakpoint;
          this._mode = isNarrow ? 'mobile' : 'desktop';
          previousWidth = parent.contentRect.width;
          
          // Emit mode change event
          this.dispatchEvent(new CustomEvent('mode-change', {
            detail: this._mode,
            bubbles: true
          }));
        }
      });
      
      this.resizeObserver.observe(this.parentElement);
      
      // Initialize mode
      const initialWidth = this.parentElement.getBoundingClientRect().width;
      this._mode = initialWidth < breakpoint ? 'mobile' : 'desktop';
    });
  }
  
  disconnectResizeObserver() {
    setTimeout(() => {
      this.resizeObserver?.disconnect();
    });
  }
  
  get mode() {
    return this._mode;
  }
}

customElements.define('custom-responsive', CustomResponsiveComponent);
```

## Components Using This Mixin

The SafResponsiveElement mixin is currently used by:

### SafWizard
- Automatically adjusts layout between horizontal and vertical orientations
- Optimizes step navigation for mobile devices
- Adapts content presentation based on available space

### SafStepper  
- Changes orientation from horizontal to vertical on narrow screens
- Adjusts step indicator sizing and spacing
- Modifies navigation behavior for touch interfaces

### Usage in Components

```typescript
// Example of how components integrate the mixin
export class Wizard extends FASTElement {
  // Component-specific properties and methods
}

// Apply the ResponsiveElement mixin
export interface Wizard extends ResponsiveElement {}
applyMixins(Wizard, ResponsiveElement);
```

## Best Practices

### Initialization
- Always call `initializeResponsiveness()` in `connectedCallback()`
- Always call `disconnectResizeObserver()` in `disconnectedCallback()`
- Use appropriate timeout values to ensure proper render order

### Configuration
- Choose breakpoints that match your component's design requirements
- Set threshold values to prevent excessive mode change events
- Consider using standard design system breakpoints for consistency

### Performance
- Use throttling mechanisms (threshold) to limit ResizeObserver firing
- Disconnect observers when components are removed from DOM
- Avoid complex operations in mode change handlers

### Event Handling
- Listen for `mode-change` events to implement responsive behaviors
- Use the read-only `mode` property to check current state
- Emit meaningful events when implementing custom responsive components

### Testing
- Test responsive behavior at various screen sizes
- Verify mode changes occur at expected breakpoints
- Ensure observers are properly cleaned up to prevent memory leaks

### Accessibility
- Ensure responsive changes don't break keyboard navigation
- Maintain focus management during mode transitions
- Provide appropriate ARIA updates when layout changes

### Integration
- Coordinate with CSS media queries when appropriate
- Consider server-side rendering implications
- Use consistent breakpoint values across your application

The SafResponsiveElement mixin provides a robust foundation for creating components that adapt seamlessly to different viewport sizes while maintaining performance and accessibility standards.
