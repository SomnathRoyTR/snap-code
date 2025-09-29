# SafBreadcrumbItem

The SafBreadcrumbItem component represents an individual item within a breadcrumb navigation. It displays a clickable or non-clickable element that shows the user's current location within the navigation hierarchy.

## React

### API

| Prop        | Type                    | Default     | Description                                    |
| ----------- | ----------------------- | ----------- | ---------------------------------------------- |
| `href`      | `string`                | `undefined` | The URL to navigate to when clicked            |
| `current`   | `boolean`               | `false`     | Indicates if this is the current page          |
| `separator` | `string`                | `undefined` | Custom separator character or symbol           |
| `disabled`  | `boolean`               | `false`     | Whether the breadcrumb item is disabled        |
| `onClick`   | `(event: Event) => void`| `undefined` | Handler called when the item is clicked        |
| `className` | `string`                | `undefined` | Additional CSS class names                     |
| `children`  | `ReactNode`             | `undefined` | The content to display within the item         |

### Examples

#### Basic Usage

```jsx
import { SafBreadcrumbItem } from '@saffron/core-components';

function BasicBreadcrumbItem() {
  return (
    <SafBreadcrumbItem href="/home">
      Home
    </SafBreadcrumbItem>
  );
}
```

#### Current Page Item

```jsx
import { SafBreadcrumbItem } from '@saffron/core-components';

function CurrentBreadcrumbItem() {
  return (
    <SafBreadcrumbItem current={true}>
      Current Page
    </SafBreadcrumbItem>
  );
}
```

#### Advanced Usage with Event Handler

```jsx
import { SafBreadcrumbItem } from '@saffron/core-components';
import { useState } from 'react';

function AdvancedBreadcrumbItem() {
  const [clickCount, setClickCount] = useState(0);

  const handleClick = (event) => {
    setClickCount(prev => prev + 1);
    console.log('Breadcrumb item clicked:', event.target.textContent);
  };

  return (
    <SafBreadcrumbItem 
      href="/products" 
      onClick={handleClick}
      className="custom-breadcrumb-item"
    >
      Products ({clickCount})
    </SafBreadcrumbItem>
  );
}
```

#### Disabled Breadcrumb Item

```jsx
import { SafBreadcrumbItem } from '@saffron/core-components';

function DisabledBreadcrumbItem() {
  return (
    <SafBreadcrumbItem disabled={true}>
      Unavailable Section
    </SafBreadcrumbItem>
  );
}
```

## Angular

### API

| Input       | Type                    | Default     | Description                                    |
| ----------- | ----------------------- | ----------- | ---------------------------------------------- |
| `href`      | `string`                | `undefined` | The URL to navigate to when clicked            |
| `current`   | `boolean`               | `false`     | Indicates if this is the current page          |
| `separator` | `string`                | `undefined` | Custom separator character or symbol           |
| `disabled`  | `boolean`               | `false`     | Whether the breadcrumb item is disabled        |

### Events

| Output      | Type                    | Description                                    |
| ----------- | ----------------------- | ---------------------------------------------- |
| `click`     | `EventEmitter<Event>`   | Emitted when the breadcrumb item is clicked   |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-breadcrumb-item href="/home">
  Home
</saf-breadcrumb-item>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-breadcrumb',
  template: `
    <saf-breadcrumb-item href="/home">
      Home
    </saf-breadcrumb-item>
  `
})
export class BasicBreadcrumbComponent {}
```

#### Current Page Item

```html
<!-- Angular template -->
<saf-breadcrumb-item [current]="true">
  Current Page
</saf-breadcrumb-item>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-current-breadcrumb',
  template: `
    <saf-breadcrumb-item [current]="true">
      Current Page
    </saf-breadcrumb-item>
  `
})
export class CurrentBreadcrumbComponent {}
```

#### Advanced Usage with Event Handler

```html
<!-- Angular template -->
<saf-breadcrumb-item 
  href="/products" 
  (click)="handleClick($event)"
  class="custom-breadcrumb-item">
  Products ({{ clickCount }})
</saf-breadcrumb-item>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-breadcrumb',
  template: `
    <saf-breadcrumb-item 
      href="/products" 
      (click)="handleClick($event)"
      class="custom-breadcrumb-item">
      Products ({{ clickCount }})
    </saf-breadcrumb-item>
  `
})
export class AdvancedBreadcrumbComponent {
  clickCount = 0;

  handleClick(event: Event): void {
    this.clickCount++;
    console.log('Breadcrumb item clicked:', (event.target as HTMLElement).textContent);
  }
}
```

#### Disabled Breadcrumb Item

```html
<!-- Angular template -->
<saf-breadcrumb-item [disabled]="true">
  Unavailable Section
</saf-breadcrumb-item>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-disabled-breadcrumb',
  template: `
    <saf-breadcrumb-item [disabled]="true">
      Unavailable Section
    </saf-breadcrumb-item>
  `
})
export class DisabledBreadcrumbComponent {}
```

#### Dynamic Breadcrumb Items

```html
<!-- Angular template -->
<ng-container *ngFor="let item of breadcrumbItems; let last = last">
  <saf-breadcrumb-item 
    [href]="item.url"
    [current]="last"
    [disabled]="item.disabled"
    (click)="onItemClick(item, $event)">
    {{ item.label }}
  </saf-breadcrumb-item>
</ng-container>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface BreadcrumbItem {
  label: string;
  url: string;
  disabled?: boolean;
}

@Component({
  selector: 'app-dynamic-breadcrumb',
  template: `
    <ng-container *ngFor="let item of breadcrumbItems; let last = last">
      <saf-breadcrumb-item 
        [href]="item.url"
        [current]="last"
        [disabled]="item.disabled"
        (click)="onItemClick(item, $event)">
        {{ item.label }}
      </saf-breadcrumb-item>
    </ng-container>
  `
})
export class DynamicBreadcrumbComponent {
  breadcrumbItems: BreadcrumbItem[] = [
    { label: 'Home', url: '/home' },
    { label: 'Products', url: '/products' },
    { label: 'Electronics', url: '/products/electronics' },
    { label: 'Smartphones', url: '/products/electronics/smartphones' }
  ];

  onItemClick(item: BreadcrumbItem, event: Event): void {
    console.log('Clicked breadcrumb item:', item.label);
  }
}
```

### Best Practices

- **Use meaningful labels**: Ensure breadcrumb item text clearly describes the page or section it represents
- **Maintain hierarchy**: Structure breadcrumb items to reflect the actual site navigation hierarchy
- **Current page indication**: Always mark the current page item with the `current` attribute and avoid making it clickable
- **Consistent navigation**: Use the `href` attribute consistently for navigation-enabled items
- **Accessibility**: Ensure proper contrast and keyboard navigation support
- **Mobile considerations**: Consider truncating long breadcrumb labels on smaller screens
- **Performance**: For dynamic breadcrumbs, implement proper change detection strategies

### Notes

- The SafBreadcrumbItem component should typically be used within a SafBreadcrumb container
- When `current` is true, the item should not be clickable even if an `href` is provided
- The component automatically handles ARIA attributes for accessibility
- Custom separators can be defined at the item level or inherited from the parent breadcrumb component
- Disabled items will not respond to click events and will have appropriate visual styling
