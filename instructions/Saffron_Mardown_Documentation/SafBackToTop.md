# SafBackToTop

The SafBackToTop component provides a convenient way for users to quickly return to the top of a page. It typically appears as a floating button when the user scrolls down and smoothly scrolls back to the top when clicked.

## React

### API

| Prop           | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `threshold`    | `number`                | `300`       | Scroll distance before button appears (px)    |
| `position`     | `"bottom-right" \| "bottom-left" \| "bottom-center"` | `"bottom-right"` | Button position |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Button size                           |
| `variant`      | `"primary" \| "secondary" \| "minimal"` | `"primary"` | Button style variant           |
| `smooth`       | `boolean`               | `true`      | Whether to use smooth scrolling                |
| `duration`     | `number`                | `500`       | Scroll animation duration in milliseconds     |
| `offset`       | `number`                | `0`         | Offset from top when scrolling (px)           |
| `hideOnTop`    | `boolean`               | `true`      | Hide button when already at top               |
| `icon`         | `ReactNode`             | `undefined` | Custom icon (defaults to chevron up)          |
| `text`         | `string`                | `undefined` | Text to display with/instead of icon          |
| `ariaLabel`    | `string`                | `"Back to top"` | ARIA label for accessibility              |
| `className`    | `string`                | `undefined` | Additional CSS class names                     |
| `onClick`      | `(event: MouseEvent) => void` | `undefined` | Custom click handler                     |
| `onShow`       | `() => void`            | `undefined` | Called when button becomes visible            |
| `onHide`       | `() => void`            | `undefined` | Called when button becomes hidden             |

### Examples

#### Basic Usage

```jsx
import { SafBackToTop } from '@saffron/core-components';

function BasicBackToTop() {
  return (
    <SafBackToTop />
  );
}
```

#### Custom Threshold and Position

```jsx
import { SafBackToTop } from '@saffron/core-components';

function CustomBackToTop() {
  return (
    <SafBackToTop 
      threshold={500}
      position="bottom-left"
      size="large"
      variant="secondary"
    />
  );
}
```

#### With Custom Icon and Text

```jsx
import { SafBackToTop } from '@saffron/core-components';
import { ArrowUpIcon } from '@saffron/icons';

function CustomIconBackToTop() {
  return (
    <SafBackToTop 
      icon={<ArrowUpIcon />}
      text="Top"
      position="bottom-center"
      size="medium"
    />
  );
}
```

#### Advanced Usage with Event Handlers

```jsx
import { SafBackToTop } from '@saffron/core-components';
import { useState, useCallback } from 'react';

function AdvancedBackToTop() {
  const [clickCount, setClickCount] = useState(0);
  const [isVisible, setIsVisible] = useState(false);

  const handleClick = useCallback((event) => {
    setClickCount(prev => prev + 1);
    console.log('Back to top clicked', clickCount + 1);
    
    // Add analytics tracking
    if (window.gtag) {
      window.gtag('event', 'back_to_top_clicked', {
        event_category: 'Navigation',
        event_label: 'Back to Top Button'
      });
    }
  }, [clickCount]);

  const handleShow = useCallback(() => {
    setIsVisible(true);
    console.log('Back to top button is now visible');
  }, []);

  const handleHide = useCallback(() => {
    setIsVisible(false);
    console.log('Back to top button is now hidden');
  }, []);

  return (
    <div>
      <SafBackToTop 
        threshold={400}
        position="bottom-right"
        size="medium"
        variant="primary"
        smooth={true}
        duration={800}
        offset={50}
        onClick={handleClick}
        onShow={handleShow}
        onHide={handleHide}
        ariaLabel={`Back to top (clicked ${clickCount} times)`}
        className={isVisible ? 'visible-back-to-top' : ''}
      />
      
      {/* Long content to enable scrolling */}
      <div style={{ height: '200vh', padding: '20px' }}>
        <h1>Long Content</h1>
        <p>Scroll down to see the back to top button...</p>
        {/* More content */}
      </div>
    </div>
  );
}
```

#### Text-Only Back to Top

```jsx
import { SafBackToTop } from '@saffron/core-components';

function TextBackToTop() {
  return (
    <SafBackToTop 
      text="Back to Top"
      icon={null}
      position="bottom-center"
      size="small"
      variant="minimal"
      threshold={200}
    />
  );
}
```

#### Custom Scroll Behavior

```jsx
import { SafBackToTop } from '@saffron/core-components';
import { useEffect, useState } from 'react';

function CustomScrollBackToTop() {
  const [scrollProgress, setScrollProgress] = useState(0);

  useEffect(() => {
    const handleScroll = () => {
      const totalHeight = document.documentElement.scrollHeight - window.innerHeight;
      const progress = (window.scrollY / totalHeight) * 100;
      setScrollProgress(Math.min(progress, 100));
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const handleCustomClick = (event) => {
    // Prevent default scroll behavior
    event.preventDefault();
    
    // Custom scroll implementation
    const scrollStep = -window.scrollY / (1000 / 15);
    const scrollInterval = setInterval(() => {
      if (window.scrollY !== 0) {
        window.scrollBy(0, scrollStep);
      } else {
        clearInterval(scrollInterval);
      }
    }, 15);
  };

  return (
    <div>
      <SafBackToTop 
        onClick={handleCustomClick}
        smooth={false} // Disable default smooth scroll
        position="bottom-right"
        className="progress-back-to-top"
        style={{
          '--scroll-progress': `${scrollProgress}%`
        }}
      />
      
      <div style={{ height: '300vh', padding: '20px' }}>
        <h1>Scroll Progress: {Math.round(scrollProgress)}%</h1>
        <p>Custom scroll behavior with progress indicator...</p>
      </div>
    </div>
  );
}
```

## Angular

### API

| Input          | Type                    | Default     | Description                                    |
| -------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `threshold`    | `number`                | `300`       | Scroll distance before button appears (px)    |
| `position`     | `"bottom-right" \| "bottom-left" \| "bottom-center"` | `"bottom-right"` | Button position |
| `size`         | `"small" \| "medium" \| "large"` | `"medium"` | Button size                           |
| `variant`      | `"primary" \| "secondary" \| "minimal"` | `"primary"` | Button style variant           |
| `smooth`       | `boolean`               | `true`      | Whether to use smooth scrolling                |
| `duration`     | `number`                | `500`       | Scroll animation duration in milliseconds     |
| `offset`       | `number`                | `0`         | Offset from top when scrolling (px)           |
| `hideOnTop`    | `boolean`               | `true`      | Hide button when already at top               |
| `text`         | `string`                | `undefined` | Text to display with/instead of icon          |
| `ariaLabel`    | `string`                | `"Back to top"` | ARIA label for accessibility              |

### Events

| Output         | Type                    | Description                                    |
| -------------- | ----------------------- | ---------------------------------------------- |
| `click`        | `EventEmitter<MouseEvent>` | Emitted when button is clicked              |
| `show`         | `EventEmitter<void>`    | Emitted when button becomes visible           |
| `hide`         | `EventEmitter<void>`    | Emitted when button becomes hidden            |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-back-to-top></saf-back-to-top>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-back-to-top',
  template: `
    <saf-back-to-top></saf-back-to-top>
  `
})
export class BasicBackToTopComponent {}
```

#### Custom Threshold and Position

```html
<!-- Angular template -->
<saf-back-to-top 
  [threshold]="500"
  position="bottom-left"
  size="large"
  variant="secondary">
</saf-back-to-top>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-custom-back-to-top',
  template: `
    <saf-back-to-top 
      [threshold]="500"
      position="bottom-left"
      size="large"
      variant="secondary">
    </saf-back-to-top>
  `
})
export class CustomBackToTopComponent {}
```

#### With Custom Text

```html
<!-- Angular template -->
<saf-back-to-top 
  text="Top"
  position="bottom-center"
  size="medium">
</saf-back-to-top>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-text-back-to-top',
  template: `
    <saf-back-to-top 
      text="Top"
      position="bottom-center"
      size="medium">
    </saf-back-to-top>
  `
})
export class TextBackToTopComponent {}
```

#### Advanced Usage with Event Handlers

```html
<!-- Angular template -->
<div>
  <saf-back-to-top 
    [threshold]="400"
    position="bottom-right"
    size="medium"
    variant="primary"
    [smooth]="true"
    [duration]="800"
    [offset]="50"
    (click)="handleClick($event)"
    (show)="handleShow()"
    (hide)="handleHide()"
    [ariaLabel]="backToTopAriaLabel"
    [class]="isVisible ? 'visible-back-to-top' : ''">
  </saf-back-to-top>
  
  <!-- Long content to enable scrolling -->
  <div [style.height.vh]="200" [style.padding.px]="20">
    <h1>Long Content</h1>
    <p>Scroll down to see the back to top button...</p>
  </div>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-back-to-top',
  template: `
    <div>
      <saf-back-to-top 
        [threshold]="400"
        position="bottom-right"
        size="medium"
        variant="primary"
        [smooth]="true"
        [duration]="800"
        [offset]="50"
        (click)="handleClick($event)"
        (show)="handleShow()"
        (hide)="handleHide()"
        [ariaLabel]="backToTopAriaLabel"
        [class]="isVisible ? 'visible-back-to-top' : ''">
      </saf-back-to-top>
      
      <div [style.height.vh]="200" [style.padding.px]="20">
        <h1>Long Content</h1>
        <p>Scroll down to see the back to top button...</p>
      </div>
    </div>
  `
})
export class AdvancedBackToTopComponent {
  clickCount = 0;
  isVisible = false;

  get backToTopAriaLabel(): string {
    return `Back to top (clicked ${this.clickCount} times)`;
  }

  handleClick(event: MouseEvent): void {
    this.clickCount++;
    console.log('Back to top clicked', this.clickCount);
    
    // Add analytics tracking
    if ((window as any).gtag) {
      (window as any).gtag('event', 'back_to_top_clicked', {
        event_category: 'Navigation',
        event_label: 'Back to Top Button'
      });
    }
  }

  handleShow(): void {
    this.isVisible = true;
    console.log('Back to top button is now visible');
  }

  handleHide(): void {
    this.isVisible = false;
    console.log('Back to top button is now hidden');
  }
}
```

#### Custom Scroll Progress

```html
<!-- Angular template -->
<div>
  <saf-back-to-top 
    (click)="handleCustomClick($event)"
    [smooth]="false"
    position="bottom-right"
    class="progress-back-to-top"
    [style]="{ '--scroll-progress': scrollProgress + '%' }">
  </saf-back-to-top>
  
  <div [style.height.vh]="300" [style.padding.px]="20">
    <h1>Scroll Progress: {{ Math.round(scrollProgress) }}%</h1>
    <p>Custom scroll behavior with progress indicator...</p>
  </div>
</div>
```

```typescript
// Angular component
import { Component, OnInit, OnDestroy, HostListener } from '@angular/core';

@Component({
  selector: 'app-progress-back-to-top',
  template: `
    <div>
      <saf-back-to-top 
        (click)="handleCustomClick($event)"
        [smooth]="false"
        position="bottom-right"
        class="progress-back-to-top"
        [style]="{ '--scroll-progress': scrollProgress + '%' }">
      </saf-back-to-top>
      
      <div [style.height.vh]="300" [style.padding.px]="20">
        <h1>Scroll Progress: {{ Math.round(scrollProgress) }}%</h1>
        <p>Custom scroll behavior with progress indicator...</p>
      </div>
    </div>
  `
})
export class ProgressBackToTopComponent implements OnInit, OnDestroy {
  scrollProgress = 0;
  Math = Math;
  private scrollInterval: any;

  @HostListener('window:scroll', ['$event'])
  onScroll(): void {
    const totalHeight = document.documentElement.scrollHeight - window.innerHeight;
    const progress = (window.scrollY / totalHeight) * 100;
    this.scrollProgress = Math.min(progress, 100);
  }

  handleCustomClick(event: MouseEvent): void {
    // Prevent default scroll behavior
    event.preventDefault();
    
    // Custom scroll implementation
    const scrollStep = -window.scrollY / (1000 / 15);
    this.scrollInterval = setInterval(() => {
      if (window.scrollY !== 0) {
        window.scrollBy(0, scrollStep);
      } else {
        clearInterval(this.scrollInterval);
      }
    }, 15);
  }

  ngOnInit(): void {
    this.onScroll(); // Initialize scroll progress
  }

  ngOnDestroy(): void {
    if (this.scrollInterval) {
      clearInterval(this.scrollInterval);
    }
  }
}
```

#### Dynamic Configuration

```html
<!-- Angular template -->
<div>
  <div class="controls" style="position: fixed; top: 20px; left: 20px; z-index: 1000;">
    <label>
      Threshold:
      <input type="range" min="100" max="1000" [(ngModel)]="config.threshold">
      {{ config.threshold }}px
    </label>
    <label>
      Position:
      <select [(ngModel)]="config.position">
        <option value="bottom-left">Bottom Left</option>
        <option value="bottom-center">Bottom Center</option>
        <option value="bottom-right">Bottom Right</option>
      </select>
    </label>
    <label>
      Size:
      <select [(ngModel)]="config.size">
        <option value="small">Small</option>
        <option value="medium">Medium</option>
        <option value="large">Large</option>
      </select>
    </label>
  </div>

  <saf-back-to-top 
    [threshold]="config.threshold"
    [position]="config.position"
    [size]="config.size"
    [variant]="config.variant"
    [smooth]="config.smooth"
    [duration]="config.duration"
    (click)="onBackToTopClick($event)"
    (show)="onShow()"
    (hide)="onHide()">
  </saf-back-to-top>

  <div [style.height.vh]="400">
    <h1>Dynamic Configuration Demo</h1>
    <p>Use the controls above to modify the back to top button behavior.</p>
    <div *ngFor="let i of [].constructor(50); let idx = index">
      <p>Content block {{ idx + 1 }}</p>
    </div>
  </div>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface BackToTopConfig {
  threshold: number;
  position: 'bottom-left' | 'bottom-center' | 'bottom-right';
  size: 'small' | 'medium' | 'large';
  variant: 'primary' | 'secondary' | 'minimal';
  smooth: boolean;
  duration: number;
}

@Component({
  selector: 'app-dynamic-back-to-top',
  template: `
    <div>
      <div class="controls" style="position: fixed; top: 20px; left: 20px; z-index: 1000;">
        <label>
          Threshold:
          <input type="range" min="100" max="1000" [(ngModel)]="config.threshold">
          {{ config.threshold }}px
        </label>
        <label>
          Position:
          <select [(ngModel)]="config.position">
            <option value="bottom-left">Bottom Left</option>
            <option value="bottom-center">Bottom Center</option>
            <option value="bottom-right">Bottom Right</option>
          </select>
        </label>
        <label>
          Size:
          <select [(ngModel)]="config.size">
            <option value="small">Small</option>
            <option value="medium">Medium</option>
            <option value="large">Large</option>
          </select>
        </label>
      </div>

      <saf-back-to-top 
        [threshold]="config.threshold"
        [position]="config.position"
        [size]="config.size"
        [variant]="config.variant"
        [smooth]="config.smooth"
        [duration]="config.duration"
        (click)="onBackToTopClick($event)"
        (show)="onShow()"
        (hide)="onHide()">
      </saf-back-to-top>

      <div [style.height.vh]="400">
        <h1>Dynamic Configuration Demo</h1>
        <p>Use the controls above to modify the back to top button behavior.</p>
        <div *ngFor="let i of [].constructor(50); let idx = index">
          <p>Content block {{ idx + 1 }}</p>
        </div>
      </div>
    </div>
  `
})
export class DynamicBackToTopComponent {
  config: BackToTopConfig = {
    threshold: 300,
    position: 'bottom-right',
    size: 'medium',
    variant: 'primary',
    smooth: true,
    duration: 500
  };

  onBackToTopClick(event: MouseEvent): void {
    console.log('Back to top clicked with config:', this.config);
  }

  onShow(): void {
    console.log('Back to top button shown');
  }

  onHide(): void {
    console.log('Back to top button hidden');
  }
}
```

### Best Practices

- **Appropriate threshold**: Set a threshold that balances usability (not too early) with convenience (not too late)
- **Consistent positioning**: Use consistent positioning across your application for predictable user experience
- **Smooth scrolling**: Enable smooth scrolling for better user experience unless custom behavior is needed
- **Accessibility**: Always provide meaningful ARIA labels and ensure keyboard accessibility
- **Performance**: Consider debouncing scroll events for better performance on heavy pages
- **Mobile optimization**: Ensure the button is appropriately sized and positioned for touch devices
- **Visual feedback**: Provide clear visual feedback when the button is hovered or focused
- **Analytics tracking**: Consider tracking usage to understand user behavior patterns

### Notes

- The component automatically shows/hides based on scroll position and the specified threshold
- Smooth scrolling behavior may vary across browsers and can be customized
- The button is positioned using fixed positioning and has a high z-index by default
- Custom icons can be provided through content projection in Angular
- The component handles scroll event optimization internally to prevent performance issues
- Consider the page layout when choosing button position to avoid overlapping important content
- Test across different devices and screen sizes to ensure optimal placement and functionality
