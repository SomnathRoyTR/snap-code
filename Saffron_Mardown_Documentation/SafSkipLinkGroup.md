# SafSkipLinkGroup

The SafSkipLinkGroup component provides a container for organizing multiple SafSkipLink components. It manages the layout, positioning, and accessibility features for a group of skip navigation links, ensuring proper keyboard navigation and screen reader compatibility.

## React

### API

| Prop         | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `position`   | `"top-left" \| "top-right" \| "center" \| "fixed"` | `"top-left"` | Position of the skip link group |
| `visible`    | `boolean`               | `false`     | Whether the group is always visible           |
| `orientation`| `"horizontal" \| "vertical"` | `"vertical"` | Layout orientation of skip links         |
| `spacing`    | `"tight" \| "normal" \| "loose"` | `"normal"` | Spacing between skip links            |
| `className`  | `string`                | `undefined` | Additional CSS class names                     |
| `ariaLabel`  | `string`                | `"Skip navigation"` | ARIA label for the group           |
| `onFocus`    | `(event: FocusEvent) => void` | `undefined` | Handler called when group receives focus |
| `onBlur`     | `(event: FocusEvent) => void` | `undefined` | Handler called when group loses focus |
| `children`   | `ReactNode`             | `undefined` | SafSkipLink components                         |

### Examples

#### Basic Usage

```jsx
import { SafSkipLinkGroup, SafSkipLink } from '@saffron/core-components';

function BasicSkipLinkGroup() {
  return (
    <SafSkipLinkGroup>
      <SafSkipLink href="#main-content" text="Skip to main content" />
      <SafSkipLink href="#navigation" text="Skip to navigation" />
      <SafSkipLink href="#footer" text="Skip to footer" />
    </SafSkipLinkGroup>
  );
}
```

#### Horizontal Layout with Custom Position

```jsx
import { SafSkipLinkGroup, SafSkipLink } from '@saffron/core-components';

function HorizontalSkipLinkGroup() {
  return (
    <SafSkipLinkGroup 
      orientation="horizontal" 
      position="center"
      spacing="loose"
    >
      <SafSkipLink href="#main-content" text="Main Content" />
      <SafSkipLink href="#navigation" text="Navigation" />
      <SafSkipLink href="#sidebar" text="Sidebar" />
      <SafSkipLink href="#footer" text="Footer" />
    </SafSkipLinkGroup>
  );
}
```

#### Always Visible Skip Link Group

```jsx
import { SafSkipLinkGroup, SafSkipLink } from '@saffron/core-components';

function VisibleSkipLinkGroup() {
  return (
    <SafSkipLinkGroup 
      visible={true}
      position="top-right"
      orientation="vertical"
      spacing="tight"
      ariaLabel="Page navigation shortcuts"
    >
      <SafSkipLink href="#search" text="Skip to search" />
      <SafSkipLink href="#main-content" text="Skip to main content" />
      <SafSkipLink href="#related-links" text="Skip to related links" />
    </SafSkipLinkGroup>
  );
}
```

#### Advanced Usage with Event Handlers

```jsx
import { SafSkipLinkGroup, SafSkipLink } from '@saffron/core-components';
import { useState, useRef } from 'react';

function AdvancedSkipLinkGroup() {
  const [focusedIndex, setFocusedIndex] = useState(-1);
  const [isGroupFocused, setIsGroupFocused] = useState(false);
  const groupRef = useRef(null);

  const skipLinks = [
    { href: '#header', text: 'Skip to header' },
    { href: '#main-content', text: 'Skip to main content' },
    { href: '#sidebar', text: 'Skip to sidebar' },
    { href: '#footer', text: 'Skip to footer' }
  ];

  const handleGroupFocus = (event) => {
    setIsGroupFocused(true);
    console.log('Skip link group focused');
  };

  const handleGroupBlur = (event) => {
    // Check if focus is moving outside the group
    if (!groupRef.current?.contains(event.relatedTarget)) {
      setIsGroupFocused(false);
      setFocusedIndex(-1);
      console.log('Skip link group lost focus');
    }
  };

  const handleSkipLinkFocus = (index) => {
    setFocusedIndex(index);
  };

  const handleSkipLinkClick = (link, event) => {
    console.log(`Skip link activated: ${link.text}`);
    
    // Ensure target receives focus
    const targetId = link.href.substring(1);
    const targetElement = document.getElementById(targetId);
    if (targetElement) {
      targetElement.setAttribute('tabindex', '-1');
      targetElement.focus();
    }
  };

  return (
    <div>
      <SafSkipLinkGroup 
        ref={groupRef}
        position="top-left"
        orientation="vertical"
        spacing="normal"
        onFocus={handleGroupFocus}
        onBlur={handleGroupBlur}
        className={isGroupFocused ? 'group-focused' : ''}
        ariaLabel="Page navigation shortcuts"
      >
        {skipLinks.map((link, index) => (
          <SafSkipLink
            key={index}
            href={link.href}
            text={link.text}
            onFocus={() => handleSkipLinkFocus(index)}
            onClick={(event) => handleSkipLinkClick(link, event)}
            className={focusedIndex === index ? 'focused' : ''}
          />
        ))}
      </SafSkipLinkGroup>

      <header id="header">Header content...</header>
      <main id="main-content">Main content...</main>
      <aside id="sidebar">Sidebar content...</aside>
      <footer id="footer">Footer content...</footer>
    </div>
  );
}
```

#### Responsive Skip Link Group

```jsx
import { SafSkipLinkGroup, SafSkipLink } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function ResponsiveSkipLinkGroup() {
  const [isMobile, setIsMobile] = useState(false);
  const [skipLinks, setSkipLinks] = useState([]);

  useEffect(() => {
    const checkScreenSize = () => {
      const mobile = window.innerWidth < 768;
      setIsMobile(mobile);
      
      // Adjust skip links based on screen size
      if (mobile) {
        setSkipLinks([
          { href: '#main-content', text: 'Main' },
          { href: '#navigation', text: 'Menu' }
        ]);
      } else {
        setSkipLinks([
          { href: '#header', text: 'Skip to header' },
          { href: '#navigation', text: 'Skip to navigation' },
          { href: '#main-content', text: 'Skip to main content' },
          { href: '#sidebar', text: 'Skip to sidebar' },
          { href: '#footer', text: 'Skip to footer' }
        ]);
      }
    };
    
    checkScreenSize();
    window.addEventListener('resize', checkScreenSize);
    
    return () => window.removeEventListener('resize', checkScreenSize);
  }, []);

  return (
    <SafSkipLinkGroup 
      orientation={isMobile ? 'horizontal' : 'vertical'}
      position={isMobile ? 'center' : 'top-left'}
      spacing={isMobile ? 'tight' : 'normal'}
    >
      {skipLinks.map((link, index) => (
        <SafSkipLink
          key={index}
          href={link.href}
          text={link.text}
        />
      ))}
    </SafSkipLinkGroup>
  );
}
```

## Angular

### API

| Input        | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `position`   | `"top-left" \| "top-right" \| "center" \| "fixed"` | `"top-left"` | Position of the skip link group |
| `visible`    | `boolean`               | `false`     | Whether the group is always visible           |
| `orientation`| `"horizontal" \| "vertical"` | `"vertical"` | Layout orientation of skip links         |
| `spacing`    | `"tight" \| "normal" \| "loose"` | `"normal"` | Spacing between skip links            |
| `ariaLabel`  | `string`                | `"Skip navigation"` | ARIA label for the group           |

### Events

| Output       | Type                    | Description                                    |
| ------------ | ----------------------- | ---------------------------------------------- |
| `focus`      | `EventEmitter<FocusEvent>` | Emitted when group receives focus          |
| `blur`       | `EventEmitter<FocusEvent>` | Emitted when group loses focus             |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-skip-link-group>
  <saf-skip-link href="#main-content" text="Skip to main content"></saf-skip-link>
  <saf-skip-link href="#navigation" text="Skip to navigation"></saf-skip-link>
  <saf-skip-link href="#footer" text="Skip to footer"></saf-skip-link>
</saf-skip-link-group>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-skip-link-group',
  template: `
    <saf-skip-link-group>
      <saf-skip-link href="#main-content" text="Skip to main content"></saf-skip-link>
      <saf-skip-link href="#navigation" text="Skip to navigation"></saf-skip-link>
      <saf-skip-link href="#footer" text="Skip to footer"></saf-skip-link>
    </saf-skip-link-group>
  `
})
export class BasicSkipLinkGroupComponent {}
```

#### Horizontal Layout with Custom Position

```html
<!-- Angular template -->
<saf-skip-link-group 
  orientation="horizontal" 
  position="center"
  spacing="loose">
  <saf-skip-link href="#main-content" text="Main Content"></saf-skip-link>
  <saf-skip-link href="#navigation" text="Navigation"></saf-skip-link>
  <saf-skip-link href="#sidebar" text="Sidebar"></saf-skip-link>
  <saf-skip-link href="#footer" text="Footer"></saf-skip-link>
</saf-skip-link-group>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-horizontal-skip-link-group',
  template: `
    <saf-skip-link-group 
      orientation="horizontal" 
      position="center"
      spacing="loose">
      <saf-skip-link href="#main-content" text="Main Content"></saf-skip-link>
      <saf-skip-link href="#navigation" text="Navigation"></saf-skip-link>
      <saf-skip-link href="#sidebar" text="Sidebar"></saf-skip-link>
      <saf-skip-link href="#footer" text="Footer"></saf-skip-link>
    </saf-skip-link-group>
  `
})
export class HorizontalSkipLinkGroupComponent {}
```

#### Always Visible Skip Link Group

```html
<!-- Angular template -->
<saf-skip-link-group 
  [visible]="true"
  position="top-right"
  orientation="vertical"
  spacing="tight"
  ariaLabel="Page navigation shortcuts">
  <saf-skip-link href="#search" text="Skip to search"></saf-skip-link>
  <saf-skip-link href="#main-content" text="Skip to main content"></saf-skip-link>
  <saf-skip-link href="#related-links" text="Skip to related links"></saf-skip-link>
</saf-skip-link-group>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-visible-skip-link-group',
  template: `
    <saf-skip-link-group 
      [visible]="true"
      position="top-right"
      orientation="vertical"
      spacing="tight"
      ariaLabel="Page navigation shortcuts">
      <saf-skip-link href="#search" text="Skip to search"></saf-skip-link>
      <saf-skip-link href="#main-content" text="Skip to main content"></saf-skip-link>
      <saf-skip-link href="#related-links" text="Skip to related links"></saf-skip-link>
    </saf-skip-link-group>
  `
})
export class VisibleSkipLinkGroupComponent {}
```

#### Advanced Usage with Event Handlers

```html
<!-- Angular template -->
<div>
  <saf-skip-link-group 
    #skipLinkGroup
    position="top-left"
    orientation="vertical"
    spacing="normal"
    (focus)="handleGroupFocus()"
    (blur)="handleGroupBlur($event)"
    [class]="isGroupFocused ? 'group-focused' : ''"
    ariaLabel="Page navigation shortcuts">
    <saf-skip-link 
      *ngFor="let link of skipLinks; let i = index"
      [href]="link.href"
      [text]="link.text"
      (focus)="handleSkipLinkFocus(i)"
      (click)="handleSkipLinkClick(link, $event)"
      [class]="focusedIndex === i ? 'focused' : ''">
    </saf-skip-link>
  </saf-skip-link-group>

  <header id="header">Header content...</header>
  <main id="main-content">Main content...</main>
  <aside id="sidebar">Sidebar content...</aside>
  <footer id="footer">Footer content...</footer>
</div>
```

```typescript
// Angular component
import { Component, ElementRef, ViewChild } from '@angular/core';

interface SkipLinkConfig {
  href: string;
  text: string;
}

@Component({
  selector: 'app-advanced-skip-link-group',
  template: `
    <div>
      <saf-skip-link-group 
        #skipLinkGroup
        position="top-left"
        orientation="vertical"
        spacing="normal"
        (focus)="handleGroupFocus()"
        (blur)="handleGroupBlur($event)"
        [class]="isGroupFocused ? 'group-focused' : ''"
        ariaLabel="Page navigation shortcuts">
        <saf-skip-link 
          *ngFor="let link of skipLinks; let i = index"
          [href]="link.href"
          [text]="link.text"
          (focus)="handleSkipLinkFocus(i)"
          (click)="handleSkipLinkClick(link, $event)"
          [class]="focusedIndex === i ? 'focused' : ''">
        </saf-skip-link>
      </saf-skip-link-group>

      <header id="header">Header content...</header>
      <main id="main-content">Main content...</main>
      <aside id="sidebar">Sidebar content...</aside>
      <footer id="footer">Footer content...</footer>
    </div>
  `
})
export class AdvancedSkipLinkGroupComponent {
  @ViewChild('skipLinkGroup', { read: ElementRef }) groupRef!: ElementRef;

  focusedIndex = -1;
  isGroupFocused = false;

  skipLinks: SkipLinkConfig[] = [
    { href: '#header', text: 'Skip to header' },
    { href: '#main-content', text: 'Skip to main content' },
    { href: '#sidebar', text: 'Skip to sidebar' },
    { href: '#footer', text: 'Skip to footer' }
  ];

  handleGroupFocus(): void {
    this.isGroupFocused = true;
    console.log('Skip link group focused');
  }

  handleGroupBlur(event: FocusEvent): void {
    // Check if focus is moving outside the group
    const relatedTarget = event.relatedTarget as Element;
    if (!this.groupRef.nativeElement.contains(relatedTarget)) {
      this.isGroupFocused = false;
      this.focusedIndex = -1;
      console.log('Skip link group lost focus');
    }
  }

  handleSkipLinkFocus(index: number): void {
    this.focusedIndex = index;
  }

  handleSkipLinkClick(link: SkipLinkConfig, event: MouseEvent): void {
    console.log(`Skip link activated: ${link.text}`);
    
    // Ensure target receives focus
    const targetId = link.href.substring(1);
    const targetElement = document.getElementById(targetId);
    if (targetElement) {
      targetElement.setAttribute('tabindex', '-1');
      targetElement.focus();
    }
  }
}
```

#### Dynamic Skip Link Groups

```html
<!-- Angular template -->
<saf-skip-link-group 
  [orientation]="groupOrientation"
  [position]="groupPosition"
  [spacing]="groupSpacing">
  <saf-skip-link 
    *ngFor="let link of dynamicSkipLinks; trackBy: trackByFn"
    [href]="link.href"
    [text]="link.text"
    [visible]="link.visible"
    (click)="onSkipLinkClick(link, $event)">
  </saf-skip-link>
</saf-skip-link-group>
```

```typescript
// Angular component
import { Component, OnInit, OnDestroy, HostListener } from '@angular/core';

interface DynamicSkipLink {
  id: number;
  href: string;
  text: string;
  visible: boolean;
  priority: number;
}

@Component({
  selector: 'app-dynamic-skip-link-group',
  template: `
    <saf-skip-link-group 
      [orientation]="groupOrientation"
      [position]="groupPosition"
      [spacing]="groupSpacing">
      <saf-skip-link 
        *ngFor="let link of dynamicSkipLinks; trackBy: trackByFn"
        [href]="link.href"
        [text]="link.text"
        [visible]="link.visible"
        (click)="onSkipLinkClick(link, $event)">
      </saf-skip-link>
    </saf-skip-link-group>
  `
})
export class DynamicSkipLinkGroupComponent implements OnInit {
  groupOrientation: 'horizontal' | 'vertical' = 'vertical';
  groupPosition: 'top-left' | 'top-right' | 'center' = 'top-left';
  groupSpacing: 'tight' | 'normal' | 'loose' = 'normal';

  allSkipLinks: DynamicSkipLink[] = [
    { id: 1, href: '#search', text: 'Skip to search', visible: true, priority: 1 },
    { id: 2, href: '#navigation', text: 'Skip to navigation', visible: true, priority: 2 },
    { id: 3, href: '#main-content', text: 'Skip to main content', visible: true, priority: 3 },
    { id: 4, href: '#sidebar', text: 'Skip to sidebar', visible: true, priority: 4 },
    { id: 5, href: '#related-content', text: 'Skip to related content', visible: true, priority: 5 },
    { id: 6, href: '#footer', text: 'Skip to footer', visible: true, priority: 6 }
  ];

  get dynamicSkipLinks(): DynamicSkipLink[] {
    return this.allSkipLinks
      .filter(link => link.visible)
      .sort((a, b) => a.priority - b.priority);
  }

  ngOnInit(): void {
    this.updateSkipLinksForScreenSize();
  }

  @HostListener('window:resize', ['$event'])
  onResize(): void {
    this.updateSkipLinksForScreenSize();
  }

  private updateSkipLinksForScreenSize(): void {
    const isMobile = window.innerWidth < 768;
    
    if (isMobile) {
      this.groupOrientation = 'horizontal';
      this.groupPosition = 'center';
      this.groupSpacing = 'tight';
      
      // Show only essential skip links on mobile
      this.allSkipLinks.forEach(link => {
        link.visible = ['#main-content', '#navigation'].includes(link.href);
      });
    } else {
      this.groupOrientation = 'vertical';
      this.groupPosition = 'top-left';
      this.groupSpacing = 'normal';
      
      // Show all skip links on desktop
      this.allSkipLinks.forEach(link => {
        link.visible = true;
      });
    }
  }

  trackByFn(index: number, item: DynamicSkipLink): number {
    return item.id;
  }

  onSkipLinkClick(link: DynamicSkipLink, event: MouseEvent): void {
    console.log('Skip link clicked:', link.text);
    
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

- **Logical grouping**: Group related skip links together for better organization and user experience
- **Consistent positioning**: Use consistent positioning across pages for predictable user experience
- **Appropriate spacing**: Choose spacing that provides clear separation without excessive gaps
- **Focus management**: Ensure proper focus management within the group and to target elements
- **Screen reader compatibility**: Use meaningful ARIA labels and maintain logical tab order
- **Responsive design**: Adjust orientation and visible links based on screen size and context
- **Performance**: Use trackBy functions in Angular for efficient rendering of dynamic groups
- **Target validation**: Ensure all target elements referenced by skip links actually exist on the page

### Notes

- SafSkipLinkGroup should contain only SafSkipLink components as direct children
- The group automatically manages focus behavior and keyboard navigation between skip links
- When `visible` is false, the group appears only when focused (accessibility-first approach)
- The component provides built-in ARIA attributes for proper screen reader support
- Use the `position="fixed"` option for groups that should remain in view while scrolling
- Consider the cognitive load when including too many skip links in a single group
- Test with actual assistive technologies to ensure optimal user experience
