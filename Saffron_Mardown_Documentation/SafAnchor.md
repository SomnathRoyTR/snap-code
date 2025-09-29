# SafAnchor

A hypertext link component that allows users to navigate from one place to another. SafAnchor provides multiple appearance variants including standard anchors and call-to-action (CTA) styles.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `href` | `string` | - | The URL that the hyperlink references |
| `target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `_blank` | Determines where the link will open in browsing context |
| `appearance` | `'anchor' \| 'cta-primary' \| 'cta-secondary' \| 'cta-tertiary'` | `anchor` | The visual appearance style variant of the anchor |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed'` | `standard` | The density/spacing of the anchor (applies to CTA variants only) |
| `iconOnly` | `boolean` | `false` | Indicates the anchor should be rendered as icon-only |
| `span` | `boolean` | `false` | If true, renders as span element instead of anchor (useful for SPA links) |
| `download` | `string` | - | Prompts the user to save the linked URL |
| `rel` | `string` | - | The relationship of the linked URL as space-separated link types |
| `type` | `string` | - | Hints at the linked URL's format with a MIME type |
| `hreflang` | `string` | - | Hints at the language of the referenced resource |
| `ping` | `string` | - | Space-separated list of URLs for POST requests when link is followed |
| `referrerpolicy` | `string` | - | Determines how much of the referrer to send when following the link |
| `a11yAriaDescription` | `string` | - | Description for screen readers only |
| `a11yAriaCurrent` | `'page' \| 'step' \| 'location' \| 'date' \| 'time' \| boolean \| string` | - | Indicates current item within a container or set |
| `ariaExpanded` | `'true' \| 'false' \| string` | - | Indicates if element is currently expanded or collapsed |

### Examples

#### Basic Usage
```jsx
import { SafAnchor } from '@saffron/core-components/react';

// Standard anchor link
function BasicAnchor() {
  return (
    <SafAnchor href="https://www.example.com">
      Visit Example.com
    </SafAnchor>
  );
}

// External link with target
function ExternalLink() {
  return (
    <SafAnchor href="https://www.external-site.com" target="_blank">
      External Link
    </SafAnchor>
  );
}
```

#### Advanced Usage
```jsx
import { SafAnchor, SafIcon } from '@saffron/core-components/react';

// CTA Primary Button Style
function CTALinks() {
  return (
    <div>
      <SafAnchor 
        appearance="cta-primary" 
        density="standard" 
        href="/dashboard"
      >
        Go to Dashboard
      </SafAnchor>
      
      <SafAnchor 
        appearance="cta-secondary" 
        density="compact" 
        href="/settings"
      >
        Settings
      </SafAnchor>
      
      <SafAnchor 
        appearance="cta-tertiary" 
        href="/help"
      >
        Need Help?
      </SafAnchor>
    </div>
  );
}

// Anchor with icons
function AnchorWithIcons() {
  return (
    <SafAnchor href="/profile">
      <SafIcon slot="start" iconName="user" />
      View Profile
      <SafIcon slot="end" iconName="arrow-right" />
    </SafAnchor>
  );
}

// SPA integration (renders as span for router compatibility)
function SPALink() {
  const handleClick = (e) => {
    e.preventDefault();
    // Handle SPA navigation
    navigate('/dashboard');
  };
  
  return (
    <SafAnchor 
      span={true}
      href="/dashboard"
      onClick={handleClick}
      appearance="cta-primary"
    >
      Go to Dashboard
    </SafAnchor>
  );
}

// Icon-only anchor with accessibility
function IconOnlyAnchor() {
  return (
    <SafAnchor 
      href="/settings" 
      iconOnly={true}
      ariaLabel="Settings"
      a11yAriaDescription="Navigate to user settings page"
    >
      <SafIcon iconName="settings" />
    </SafAnchor>
  );
}

// Download link
function DownloadLink() {
  return (
    <SafAnchor 
      href="/files/document.pdf" 
      download="document.pdf"
      appearance="cta-secondary"
    >
      <SafIcon slot="start" iconName="download" />
      Download PDF
    </SafAnchor>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `href` | `string` | - | The URL that the hyperlink references |
| `target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `_blank` | Determines where the link will open in browsing context |
| `appearance` | `'anchor' \| 'cta-primary' \| 'cta-secondary' \| 'cta-tertiary'` | `anchor` | The visual appearance style variant of the anchor |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed'` | `standard` | The density/spacing of the anchor (applies to CTA variants only) |
| `iconOnly` | `boolean` | `false` | Indicates the anchor should be rendered as icon-only |
| `span` | `boolean` | `false` | If true, renders as span element instead of anchor (useful for SPA links) |
| `download` | `string` | - | Prompts the user to save the linked URL |
| `rel` | `string` | - | The relationship of the linked URL as space-separated link types |
| `type` | `string` | - | Hints at the linked URL's format with a MIME type |
| `hreflang` | `string` | - | Hints at the language of the referenced resource |
| `ping` | `string` | - | Space-separated list of URLs for POST requests when link is followed |
| `referrerpolicy` | `string` | - | Determines how much of the referrer to send when following the link |
| `a11y-aria-description` | `string` | - | Description for screen readers only |
| `a11y-aria-current` | `'page' \| 'step' \| 'location' \| 'date' \| 'time' \| boolean \| string` | - | Indicates current item within a container or set |
| `aria-expanded` | `'true' \| 'false' \| string` | - | Indicates if element is currently expanded or collapsed |

### Examples

#### Basic Usage
```html
<!-- Standard anchor link -->
<saf-anchor href="https://www.example.com">
  Visit Example.com
</saf-anchor>

<!-- External link with target -->
<saf-anchor href="https://www.external-site.com" target="_blank">
  External Link
</saf-anchor>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-anchor',
  template: `
    <saf-anchor [href]="externalUrl" target="_blank">
      {{ linkText }}
    </saf-anchor>
  `
})
export class BasicAnchorComponent {
  externalUrl = 'https://www.example.com';
  linkText = 'Visit Example.com';
}
```

#### Advanced Usage
```html
<!-- CTA Button Styles -->
<div class="cta-links">
  <saf-anchor 
    appearance="cta-primary" 
    density="standard" 
    href="/dashboard">
    Go to Dashboard
  </saf-anchor>
  
  <saf-anchor 
    appearance="cta-secondary" 
    density="compact" 
    href="/settings">
    Settings
  </saf-anchor>
  
  <saf-anchor 
    appearance="cta-tertiary" 
    href="/help">
    Need Help?
  </saf-anchor>
</div>

<!-- Anchor with icons -->
<saf-anchor href="/profile">
  <saf-icon slot="start" icon-name="user"></saf-icon>
  View Profile
  <saf-icon slot="end" icon-name="arrow-right"></saf-icon>
</saf-anchor>

<!-- SPA integration -->
<saf-anchor 
  [span]="true"
  href="/dashboard"
  (click)="onNavigate($event)"
  appearance="cta-primary">
  Go to Dashboard
</saf-anchor>

<!-- Icon-only anchor with accessibility -->
<saf-anchor 
  href="/settings" 
  [icon-only]="true"
  aria-label="Settings"
  a11y-aria-description="Navigate to user settings page">
  <saf-icon icon-name="settings"></saf-icon>
</saf-anchor>

<!-- Download link -->
<saf-anchor 
  href="/files/document.pdf" 
  download="document.pdf"
  appearance="cta-secondary">
  <saf-icon slot="start" icon-name="download"></saf-icon>
  Download PDF
</saf-anchor>

<!-- Dynamic anchor with Angular Router -->
<saf-anchor 
  [span]="true"
  [href]="routerLink"
  (click)="navigateToRoute($event)"
  [appearance]="linkAppearance">
  {{ linkText }}
</saf-anchor>
```

```typescript
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-advanced-anchor',
  template: `
    <!-- Template content shown above -->
  `
})
export class AdvancedAnchorComponent {
  routerLink = '/dashboard';
  linkText = 'Go to Dashboard';
  linkAppearance = 'cta-primary';
  
  constructor(private router: Router) {}
  
  onNavigate(event: Event): void {
    event.preventDefault();
    this.router.navigate(['/dashboard']);
  }
  
  navigateToRoute(event: Event): void {
    event.preventDefault();
    this.router.navigate([this.routerLink]);
  }
}
```

### Best Practices

1. **Use appropriate appearance variants:**
   - Use `anchor` for standard text links within content
   - Use `cta-primary` for main call-to-action links
   - Use `cta-secondary` for secondary actions like "Cancel" or "Back"
   - Use `cta-tertiary` for subtle navigational elements

2. **Accessibility considerations:**
   - Always provide meaningful link text that describes the destination
   - Use `a11yAriaDescription` for additional context for screen readers
   - Use `ariaLabel` for icon-only anchors
   - Consider using `a11yAriaCurrent` to indicate current page in navigation

3. **External links:**
   - Always use `target="_blank"` for external links
   - Consider adding `rel="noopener noreferrer"` for security
   - Include visual indicators (like external link icons) for external links

4. **SPA integration:**
   - Use `span={true}` for React or `[span]="true"` for Angular when integrating with router libraries
   - Prevent default click behavior and handle navigation programmatically

5. **Icon usage:**
   - Use icons sparingly and ensure they add meaning
   - Always provide accessible labels for icon-only anchors
   - Use `slot="start"` and `slot="end"` to position icons appropriately

6. **Density considerations:**
   - Use appropriate density for the context (compact for toolbars, standard for main content)
   - Density only applies to CTA appearance variants

### Notes

- **Navigation vs Actions:** Use anchors for navigation to different pages/locations. Use buttons for actions that affect the current page.
- **Security:** When using `target="_blank"`, consider adding `rel="noopener noreferrer"` for security reasons.
- **Deprecated Features:** The `transferFocus` attribute is deprecated and will be removed in v4. Use click handlers instead.
- **Performance:** For SPA applications, use the `span` attribute and handle navigation through your router to avoid full page reloads.
- **SEO Considerations:** Proper `href` attributes help with SEO and allow search engines to crawl your links.
