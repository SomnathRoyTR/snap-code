# SafBreadcrumb

A breadcrumb navigation component that displays the current page's location within a navigational hierarchy. Breadcrumbs help users understand their current location and provide a way to navigate back to parent pages.

## React

### API

#### SafBreadcrumb

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | `ReactNode` | - | SafBreadcrumbItem components |

#### SafBreadcrumbItem

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `href` | `string` | - | The URL that the breadcrumb item references |
| `target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `_blank` | Determines where the link will open in browsing context |
| `a11yAriaDescription` | `string` | - | Description for screen readers only |
| `separator` | `boolean` | `true` | Whether to show separator after this item (automatically managed) |
| `download` | `string` | - | Prompts the user to save the linked URL |
| `rel` | `string` | - | The relationship of the linked URL as space-separated link types |
| `type` | `string` | - | Hints at the linked URL's format with a MIME type |
| `hreflang` | `string` | - | Hints at the language of the referenced resource |
| `ping` | `string` | - | Space-separated list of URLs for POST requests when link is followed |
| `referrerpolicy` | `string` | - | Determines how much of the referrer to send when following the link |

### Examples

#### Basic Usage
```jsx
import { SafBreadcrumb, SafBreadcrumbItem } from '@saffron/core-components/react';

function BasicBreadcrumb() {
  return (
    <SafBreadcrumb>
      <SafBreadcrumbItem href="/">Home</SafBreadcrumbItem>
      <SafBreadcrumbItem href="/products">Products</SafBreadcrumbItem>
      <SafBreadcrumbItem href="/products/electronics">Electronics</SafBreadcrumbItem>
      <SafBreadcrumbItem>Current Page</SafBreadcrumbItem>
    </SafBreadcrumb>
  );
}
```

#### Advanced Usage
```jsx
import { SafBreadcrumb, SafBreadcrumbItem, SafIcon } from '@saffron/core-components/react';

// Dynamic breadcrumbs with icons
function AdvancedBreadcrumb() {
  const breadcrumbs = [
    { label: 'Home', href: '/', icon: 'home' },
    { label: 'Dashboard', href: '/dashboard', icon: 'dashboard' },
    { label: 'Projects', href: '/dashboard/projects', icon: 'folder' },
    { label: 'Project Alpha', href: '/dashboard/projects/alpha', icon: 'project' },
    { label: 'Settings', href: null, icon: 'settings' } // Current page
  ];

  return (
    <SafBreadcrumb>
      {breadcrumbs.map((crumb, index) => (
        <SafBreadcrumbItem 
          key={index}
          href={crumb.href}
          a11yAriaDescription={`Navigate to ${crumb.label}`}
        >
          <SafIcon slot="start" iconName={crumb.icon} />
          {crumb.label}
        </SafBreadcrumbItem>
      ))}
    </SafBreadcrumb>
  );
}

// Custom separator
function CustomSeparatorBreadcrumb() {
  return (
    <SafBreadcrumb>
      <SafBreadcrumbItem href="/">
        <SafIcon slot="start" iconName="home" />
        Home
        <SafIcon slot="separator" iconName="chevron-right" />
      </SafBreadcrumbItem>
      <SafBreadcrumbItem href="/products">
        Products
        <SafIcon slot="separator" iconName="chevron-right" />
      </SafBreadcrumbItem>
      <SafBreadcrumbItem>Current Page</SafBreadcrumbItem>
    </SafBreadcrumb>
  );
}

// Truncated breadcrumbs for long paths
function TruncatedBreadcrumb() {
  const allBreadcrumbs = [
    { label: 'Home', href: '/' },
    { label: 'Level 1', href: '/level1' },
    { label: 'Level 2', href: '/level1/level2' },
    { label: 'Level 3', href: '/level1/level2/level3' },
    { label: 'Level 4', href: '/level1/level2/level3/level4' },
    { label: 'Current Page', href: null }
  ];

  // Show first, last, and current with ellipsis for middle items
  const displayBreadcrumbs = [
    allBreadcrumbs[0], // First
    { label: '...', href: null }, // Ellipsis
    ...allBreadcrumbs.slice(-2) // Last two
  ];

  return (
    <SafBreadcrumb>
      {displayBreadcrumbs.map((crumb, index) => (
        <SafBreadcrumbItem 
          key={index}
          href={crumb.href}
          aria-label={crumb.href ? `Navigate to ${crumb.label}` : crumb.label}
        >
          {crumb.label}
        </SafBreadcrumbItem>
      ))}
    </SafBreadcrumb>
  );
}
```

## Angular

### API

#### saf-breadcrumb

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| - | - | - | Container for breadcrumb items |

#### saf-breadcrumb-item

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `href` | `string` | - | The URL that the breadcrumb item references |
| `target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `_blank` | Determines where the link will open in browsing context |
| `a11y-aria-description` | `string` | - | Description for screen readers only |
| `separator` | `boolean` | `true` | Whether to show separator after this item (automatically managed) |
| `download` | `string` | - | Prompts the user to save the linked URL |
| `rel` | `string` | - | The relationship of the linked URL as space-separated link types |
| `type` | `string` | - | Hints at the linked URL's format with a MIME type |
| `hreflang` | `string` | - | Hints at the language of the referenced resource |
| `ping` | `string` | - | Space-separated list of URLs for POST requests when link is followed |
| `referrerpolicy` | `string` | - | Determines how much of the referrer to send when following the link |

### Examples

#### Basic Usage
```html
<saf-breadcrumb>
  <saf-breadcrumb-item href="/">Home</saf-breadcrumb-item>
  <saf-breadcrumb-item href="/products">Products</saf-breadcrumb-item>
  <saf-breadcrumb-item href="/products/electronics">Electronics</saf-breadcrumb-item>
  <saf-breadcrumb-item>Current Page</saf-breadcrumb-item>
</saf-breadcrumb>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-breadcrumb',
  template: `
    <saf-breadcrumb>
      <saf-breadcrumb-item *ngFor="let crumb of breadcrumbs; let last = last" 
                          [href]="last ? null : crumb.href">
        {{ crumb.label }}
      </saf-breadcrumb-item>
    </saf-breadcrumb>
  `
})
export class BasicBreadcrumbComponent {
  breadcrumbs = [
    { label: 'Home', href: '/' },
    { label: 'Products', href: '/products' },
    { label: 'Electronics', href: '/products/electronics' },
    { label: 'Current Page', href: null }
  ];
}
```

#### Advanced Usage
```html
<!-- Dynamic breadcrumbs with icons -->
<saf-breadcrumb>
  <saf-breadcrumb-item 
    *ngFor="let crumb of breadcrumbs; let last = last" 
    [href]="last ? null : crumb.href"
    [a11y-aria-description]="'Navigate to ' + crumb.label">
    <saf-icon slot="start" [icon-name]="crumb.icon"></saf-icon>
    {{ crumb.label }}
  </saf-breadcrumb-item>
</saf-breadcrumb>

<!-- Custom separator -->
<saf-breadcrumb>
  <saf-breadcrumb-item href="/">
    <saf-icon slot="start" icon-name="home"></saf-icon>
    Home
    <saf-icon slot="separator" icon-name="chevron-right"></saf-icon>
  </saf-breadcrumb-item>
  <saf-breadcrumb-item href="/products">
    Products
    <saf-icon slot="separator" icon-name="chevron-right"></saf-icon>
  </saf-breadcrumb-item>
  <saf-breadcrumb-item>Current Page</saf-breadcrumb-item>
</saf-breadcrumb>

<!-- Router integration -->
<saf-breadcrumb>
  <saf-breadcrumb-item 
    *ngFor="let crumb of routeBreadcrumbs; let last = last"
    [href]="crumb.url"
    (click)="onBreadcrumbClick($event, crumb.route)"
    [attr.aria-current]="last ? 'page' : null">
    {{ crumb.label }}
  </saf-breadcrumb-item>
</saf-breadcrumb>
```

```typescript
import { Component, OnInit } from '@angular/core';
import { Router, ActivatedRoute, NavigationEnd } from '@angular/router';
import { filter, map } from 'rxjs/operators';

interface BreadcrumbItem {
  label: string;
  href: string;
  icon?: string;
}

interface RouteBreadcrumb {
  label: string;
  url: string;
  route: string[];
}

@Component({
  selector: 'app-advanced-breadcrumb',
  template: `
    <!-- Template content shown above -->
  `
})
export class AdvancedBreadcrumbComponent implements OnInit {
  breadcrumbs: BreadcrumbItem[] = [
    { label: 'Home', href: '/', icon: 'home' },
    { label: 'Dashboard', href: '/dashboard', icon: 'dashboard' },
    { label: 'Projects', href: '/dashboard/projects', icon: 'folder' },
    { label: 'Project Alpha', href: '/dashboard/projects/alpha', icon: 'project' },
    { label: 'Settings', href: null, icon: 'settings' }
  ];

  routeBreadcrumbs: RouteBreadcrumb[] = [];

  constructor(
    private router: Router,
    private activatedRoute: ActivatedRoute
  ) {}

  ngOnInit(): void {
    // Generate breadcrumbs from router
    this.router.events
      .pipe(
        filter(event => event instanceof NavigationEnd),
        map(() => this.buildBreadcrumbs(this.activatedRoute.root))
      )
      .subscribe(breadcrumbs => {
        this.routeBreadcrumbs = breadcrumbs;
      });
  }

  onBreadcrumbClick(event: Event, route: string[]): void {
    if (route) {
      event.preventDefault();
      this.router.navigate(route);
    }
  }

  private buildBreadcrumbs(route: ActivatedRoute, url: string = '', breadcrumbs: RouteBreadcrumb[] = []): RouteBreadcrumb[] {
    const children: ActivatedRoute[] = route.children;

    if (children.length === 0) {
      return breadcrumbs;
    }

    for (const child of children) {
      const routeURL: string = child.snapshot.url.map(segment => segment.path).join('/');
      if (routeURL !== '') {
        url += `/${routeURL}`;
      }

      const label = child.snapshot.data['breadcrumb'];
      if (label) {
        breadcrumbs.push({
          label,
          url,
          route: url.split('/').filter(segment => segment)
        });
      }

      return this.buildBreadcrumbs(child, url, breadcrumbs);
    }

    return breadcrumbs;
  }
}
```

### Best Practices

1. **Navigation hierarchy:**
   - Always start with the root/home page
   - Each item should represent a valid navigation step
   - The last item should represent the current page (no link)

2. **Accessibility:**
   - The last breadcrumb item automatically gets `aria-current="page"`
   - Use descriptive link text that makes sense out of context
   - Consider using `a11yAriaDescription` for additional context

3. **Performance:**
   - For SPA applications, prevent default navigation and use router programmatically
   - Consider lazy loading breadcrumb data for deep hierarchies

4. **Visual design:**
   - Keep breadcrumb labels concise but descriptive
   - Consider truncating very long paths with ellipsis
   - Use icons sparingly and consistently

5. **Mobile considerations:**
   - On small screens, consider showing only the parent and current page
   - Ensure touch targets are adequately sized

6. **SEO benefits:**
   - Proper breadcrumb structure helps search engines understand site hierarchy
   - Use semantic HTML structure with proper linking

### Notes

- **Automatic separator management:** The SafBreadcrumb component automatically manages separators between items. The last item will not have a separator.
- **Current page indication:** The last breadcrumb item automatically receives `data-aria-current="page"` for accessibility.
- **Custom separators:** You can provide custom separator content using the `separator` slot on individual breadcrumb items.
- **Router integration:** For SPA applications, handle click events to integrate with your routing system instead of using full page navigation.
- **Responsive behavior:** Consider implementing responsive breadcrumb patterns for mobile devices to avoid horizontal scrolling.
