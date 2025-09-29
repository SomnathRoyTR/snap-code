# SafSkipLink

The SafSkipLink component provides an accessibility feature that allows users to skip to main content or other important sections of a page. It's particularly useful for screen reader users and keyboard navigation, typically hidden until focused.

## React

### API

| Prop         | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `href`       | `string`                | `"#main"`   | The target element ID to skip to              |
| `text`       | `string`                | `"Skip to main content"` | The text displayed in the skip link |
| `visible`    | `boolean`               | `false`     | Whether the link is always visible            |
| `position`   | `"top-left" \| "top-right" \| "center"` | `"top-left"` | Position of the skip link |
| `className`  | `string`                | `undefined` | Additional CSS class names                     |
| `onFocus`    | `(event: FocusEvent) => void` | `undefined` | Handler called when the link receives focus |
| `onBlur`     | `(event: FocusEvent) => void` | `undefined` | Handler called when the link loses focus |
| `onClick`    | `(event: MouseEvent) => void` | `undefined` | Handler called when the link is clicked |

### Examples

#### Basic Usage

```jsx
import { SafSkipLink } from '@saffron/core-components';

function BasicSkipLink() {
  return (
    <SafSkipLink 
      href="#main-content"
      text="Skip to main content"
    />
  );
}
```

#### Multiple Skip Links

```jsx
import { SafSkipLink } from '@saffron/core-components';

function MultipleSkipLinks() {
  return (
    <div>
      <SafSkipLink 
        href="#main-content"
        text="Skip to main content"
      />
      <SafSkipLink 
        href="#navigation"
        text="Skip to navigation"
      />
      <SafSkipLink 
        href="#footer"
        text="Skip to footer"
      />
    </div>
  );
}
```

#### Always Visible Skip Link

```jsx
import { SafSkipLink } from '@saffron/core-components';

function VisibleSkipLink() {
  return (
    <SafSkipLink 
      href="#main-content"
      text="Skip to main content"
      visible={true}
      position="center"
    />
  );
}
```

#### Advanced Usage with Event Handlers

```jsx
import { SafSkipLink } from '@saffron/core-components';
import { useState } from 'react';

function AdvancedSkipLink() {
  const [skipCount, setSkipCount] = useState(0);
  const [isFocused, setIsFocused] = useState(false);

  const handleSkipClick = (event) => {
    setSkipCount(prev => prev + 1);
    console.log('Skip link activated:', event.target.href);
    
    // Ensure target element receives focus
    const targetId = event.target.getAttribute('href').substring(1);
    const targetElement = document.getElementById(targetId);
    if (targetElement) {
      targetElement.setAttribute('tabindex', '-1');
      targetElement.focus();
    }
  };

  const handleFocus = () => {
    setIsFocused(true);
  };

  const handleBlur = () => {
    setIsFocused(false);
  };

  return (
    <div>
      <SafSkipLink 
        href="#main-content"
        text={`Skip to main content (used ${skipCount} times)`}
        position="top-right"
        onClick={handleSkipClick}
        onFocus={handleFocus}
        onBlur={handleBlur}
        className={isFocused ? 'focused' : ''}
      />
      
      <main id="main-content" tabIndex="-1">
        <h1>Main Content</h1>
        <p>This is the main content area.</p>
      </main>
    </div>
  );
}
```

#### Custom Styled Skip Link

```jsx
import { SafSkipLink } from '@saffron/core-components';

function CustomSkipLink() {
  return (
    <SafSkipLink 
      href="#main-content"
      text="Jump to main content"
      className="custom-skip-link"
      position="center"
      visible={false}
    />
  );
}

// CSS for custom styling
/*
.custom-skip-link {
  background-color: #000;
  color: #fff;
  padding: 8px 16px;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
}

.custom-skip-link:focus {
  outline: 3px solid #ff0;
  outline-offset: 2px;
}
*/
```

## Angular

### API

| Input        | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `href`       | `string`                | `"#main"`   | The target element ID to skip to              |
| `text`       | `string`                | `"Skip to main content"` | The text displayed in the skip link |
| `visible`    | `boolean`               | `false`     | Whether the link is always visible            |
| `position`   | `"top-left" \| "top-right" \| "center"` | `"top-left"` | Position of the skip link |

### Events

| Output       | Type                    | Description                                    |
| ------------ | ----------------------- | ---------------------------------------------- |
| `focus`      | `EventEmitter<FocusEvent>` | Emitted when the link receives focus       |
| `blur`       | `EventEmitter<FocusEvent>` | Emitted when the link loses focus          |
| `click`      | `EventEmitter<MouseEvent>` | Emitted when the link is clicked           |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-skip-link 
  href="#main-content"
  text="Skip to main content">
</saf-skip-link>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-skip-link',
  template: `
    <saf-skip-link 
      href="#main-content"
      text="Skip to main content">
    </saf-skip-link>
  `
})
export class BasicSkipLinkComponent {}
```

#### Multiple Skip Links

```html
<!-- Angular template -->
<div>
  <saf-skip-link 
    href="#main-content"
    text="Skip to main content">
  </saf-skip-link>
  <saf-skip-link 
    href="#navigation"
    text="Skip to navigation">
  </saf-skip-link>
  <saf-skip-link 
    href="#footer"
    text="Skip to footer">
  </saf-skip-link>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-multiple-skip-links',
  template: `
    <div>
      <saf-skip-link 
        href="#main-content"
        text="Skip to main content">
      </saf-skip-link>
      <saf-skip-link 
        href="#navigation"
        text="Skip to navigation">
      </saf-skip-link>
      <saf-skip-link 
        href="#footer"
        text="Skip to footer">
      </saf-skip-link>
    </div>
  `
})
export class MultipleSkipLinksComponent {}
```

#### Always Visible Skip Link

```html
<!-- Angular template -->
<saf-skip-link 
  href="#main-content"
  text="Skip to main content"
  [visible]="true"
  position="center">
</saf-skip-link>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-visible-skip-link',
  template: `
    <saf-skip-link 
      href="#main-content"
      text="Skip to main content"
      [visible]="true"
      position="center">
    </saf-skip-link>
  `
})
export class VisibleSkipLinkComponent {}
```

#### Advanced Usage with Event Handlers

```html
<!-- Angular template -->
<div>
  <saf-skip-link 
    href="#main-content"
    [text]="skipLinkText"
    position="top-right"
    (click)="handleSkipClick($event)"
    (focus)="handleFocus()"
    (blur)="handleBlur()"
    [class]="isFocused ? 'focused' : ''">
  </saf-skip-link>
  
  <main id="main-content" tabindex="-1">
    <h1>Main Content</h1>
    <p>This is the main content area.</p>
  </main>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-skip-link',
  template: `
    <div>
      <saf-skip-link 
        href="#main-content"
        [text]="skipLinkText"
        position="top-right"
        (click)="handleSkipClick($event)"
        (focus)="handleFocus()"
        (blur)="handleBlur()"
        [class]="isFocused ? 'focused' : ''">
      </saf-skip-link>
      
      <main id="main-content" tabindex="-1">
        <h1>Main Content</h1>
        <p>This is the main content area.</p>
      </main>
    </div>
  `
})
export class AdvancedSkipLinkComponent {
  skipCount = 0;
  isFocused = false;

  get skipLinkText(): string {
    return `Skip to main content (used ${this.skipCount} times)`;
  }

  handleSkipClick(event: MouseEvent): void {
    this.skipCount++;
    console.log('Skip link activated:', (event.target as HTMLAnchorElement).href);
    
    // Ensure target element receives focus
    const href = (event.target as HTMLAnchorElement).getAttribute('href');
    if (href) {
      const targetId = href.substring(1);
      const targetElement = document.getElementById(targetId);
      if (targetElement) {
        targetElement.setAttribute('tabindex', '-1');
        targetElement.focus();
      }
    }
  }

  handleFocus(): void {
    this.isFocused = true;
  }

  handleBlur(): void {
    this.isFocused = false;
  }
}
```

#### Dynamic Skip Links

```html
<!-- Angular template -->
<div>
  <saf-skip-link 
    *ngFor="let link of skipLinks; trackBy: trackByFn"
    [href]="link.href"
    [text]="link.text"
    [position]="link.position"
    [visible]="link.visible"
    (click)="onSkipLinkClick(link, $event)">
  </saf-skip-link>
  
  <nav id="navigation">Navigation content...</nav>
  <main id="main-content">Main content...</main>
  <aside id="sidebar">Sidebar content...</aside>
  <footer id="footer">Footer content...</footer>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface SkipLinkConfig {
  id: number;
  href: string;
  text: string;
  position: 'top-left' | 'top-right' | 'center';
  visible: boolean;
}

@Component({
  selector: 'app-dynamic-skip-links',
  template: `
    <div>
      <saf-skip-link 
        *ngFor="let link of skipLinks; trackBy: trackByFn"
        [href]="link.href"
        [text]="link.text"
        [position]="link.position"
        [visible]="link.visible"
        (click)="onSkipLinkClick(link, $event)">
      </saf-skip-link>
      
      <nav id="navigation">Navigation content...</nav>
      <main id="main-content">Main content...</main>
      <aside id="sidebar">Sidebar content...</aside>
      <footer id="footer">Footer content...</footer>
    </div>
  `
})
export class DynamicSkipLinksComponent {
  skipLinks: SkipLinkConfig[] = [
    {
      id: 1,
      href: '#navigation',
      text: 'Skip to navigation',
      position: 'top-left',
      visible: false
    },
    {
      id: 2,
      href: '#main-content',
      text: 'Skip to main content',
      position: 'top-left',
      visible: false
    },
    {
      id: 3,
      href: '#sidebar',
      text: 'Skip to sidebar',
      position: 'top-left',
      visible: false
    },
    {
      id: 4,
      href: '#footer',
      text: 'Skip to footer',
      position: 'top-left',
      visible: false
    }
  ];

  trackByFn(index: number, item: SkipLinkConfig): number {
    return item.id;
  }

  onSkipLinkClick(link: SkipLinkConfig, event: MouseEvent): void {
    console.log('Skip link clicked:', link.text);
    
    // Ensure the target element can receive focus
    const targetId = link.href.substring(1);
    const targetElement = document.getElementById(targetId);
    if (targetElement) {
      targetElement.setAttribute('tabindex', '-1');
      targetElement.focus();
    }
  }
}
```

### Best Practices

- **Position early**: Place skip links at the very beginning of the page before any other content
- **Clear text**: Use descriptive text that clearly indicates what section the link will skip to
- **Focus management**: Ensure the target element receives focus after the skip link is activated
- **Keyboard accessibility**: Skip links should be the first focusable element on the page
- **Visual design**: When focused, skip links should be clearly visible with sufficient contrast
- **Target elements**: Ensure target elements exist and have appropriate IDs
- **Multiple links**: Provide skip links for all major page sections (navigation, main content, sidebar, footer)
- **Screen reader testing**: Test with actual screen readers to ensure proper functionality

### Notes

- Skip links are typically hidden until focused for visual users but always available to screen readers
- The target element should have `tabindex="-1"` to ensure it can receive programmatic focus
- Skip links improve accessibility compliance and user experience for keyboard and screen reader users
- Consider the logical tab order when implementing multiple skip links
- The component automatically handles ARIA attributes and keyboard navigation
- Skip links should be among the first elements in the DOM structure for proper accessibility
