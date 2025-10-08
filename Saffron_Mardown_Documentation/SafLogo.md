# SafLogo

A brand-compliant logo component that displays the Thomson Reuters logo in various visual appearances. SafLogo provides consistent branding across applications with support for different color schemes, themes, and optional product name display.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `appearance` | `'full-color' \| '2-color-reversed' \| '1-color-reversed' \| '1-color-black' \| '1-color-orange'` | `'full-color'` | Visual appearance variant of the logo |
| `productName` | `string` | - | Optional product name to display alongside the logo |

### Examples

#### Basic Logo Usage
```jsx
import { SafLogo } from '@saffron/core-components/react';

function BasicLogoExample() {
  return (
    <div>
      {/* Default full-color logo */}
      <SafLogo />
      
      {/* Logo with product name */}
      <SafLogo productName="Legal Research Platform" />
      
      {/* Black variant for light backgrounds */}
      <SafLogo appearance="1-color-black" />
      
      {/* Orange variant for special cases */}
      <SafLogo appearance="1-color-orange" />
    </div>
  );
}
```

#### Header with Logo and Navigation
```jsx
import { SafLogo, SafNavigation, SafNavigationItem, SafButton } from '@saffron/core-components/react';

function ApplicationHeader({ currentUser, onLogout }) {
  return (
    <header style={{
      display: 'flex',
      alignItems: 'center',
      justifyContent: 'space-between',
      padding: '16px 24px',
      backgroundColor: 'white',
      borderBottom: '1px solid #e0e0e0'
    }}>
      {/* Logo section */}
      <div style={{ display: 'flex', alignItems: 'center' }}>
        <SafLogo 
          appearance="full-color"
          productName="Thomson Reuters Westlaw"
        />
      </div>
      
      {/* Navigation */}
      <SafNavigation>
        <SafNavigationItem href="/dashboard">Dashboard</SafNavigationItem>
        <SafNavigationItem href="/research">Research</SafNavigationItem>
        <SafNavigationItem href="/cases">Cases</SafNavigationItem>
        <SafNavigationItem href="/documents">Documents</SafNavigationItem>
      </SafNavigation>
      
      {/* User actions */}
      <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
        <span>Welcome, {currentUser.name}</span>
        <SafButton appearance="secondary" onClick={onLogout}>
          Sign Out
        </SafButton>
      </div>
    </header>
  );
}
```

#### Dark Theme Logo
```jsx
import { SafLogo } from '@saffron/core-components/react';

function DarkThemeHeader() {
  return (
    <header style={{
      backgroundColor: '#1a1a1a',
      color: 'white',
      padding: '16px 24px',
      display: 'flex',
      alignItems: 'center'
    }}>
      {/* Logo optimized for dark backgrounds */}
      <SafLogo 
        appearance="2-color-reversed"
        productName="Thomson Reuters One"
      />
      
      <nav style={{ marginLeft: 'auto' }}>
        {/* Navigation items */}
      </nav>
    </header>
  );
}
```

#### Responsive Logo Layout
```jsx
import { SafLogo } from '@saffron/core-components/react';

function ResponsiveLogo() {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const checkMobile = () => {
      setIsMobile(window.innerWidth < 768);
    };
    
    checkMobile();
    window.addEventListener('resize', checkMobile);
    return () => window.removeEventListener('resize', checkMobile);
  }, []);

  return (
    <div style={{ padding: '16px' }}>
      <SafLogo 
        appearance="full-color"
        productName={isMobile ? undefined : "Thomson Reuters Professional"}
      />
      
      {/* Mobile-specific product name display */}
      {isMobile && (
        <div style={{ 
          fontSize: '0.875rem', 
          color: '#666', 
          marginTop: '4px' 
        }}>
          TR Professional
        </div>
      )}
    </div>
  );
}
```

#### Logo with Different Appearances
```jsx
import { SafLogo } from '@saffron/core-components/react';

function LogoShowcase() {
  const appearances = [
    { value: 'full-color', label: 'Full Color', background: '#ffffff' },
    { value: '1-color-black', label: 'Black', background: '#ffffff' },
    { value: '1-color-orange', label: 'Orange', background: '#ffffff' },
    { value: '2-color-reversed', label: '2-Color Reversed', background: '#1a1a1a' },
    { value: '1-color-reversed', label: '1-Color Reversed', background: '#1a1a1a' }
  ];

  return (
    <div style={{ padding: '24px' }}>
      <h2>Logo Appearance Variants</h2>
      
      <div style={{ 
        display: 'grid', 
        gridTemplateColumns: 'repeat(auto-fit, minmax(300px, 1fr))', 
        gap: '24px',
        marginTop: '24px'
      }}>
        {appearances.map(({ value, label, background }) => (
          <div 
            key={value}
            style={{
              padding: '24px',
              backgroundColor: background,
              border: '1px solid #e0e0e0',
              borderRadius: '8px',
              textAlign: 'center'
            }}>
            <SafLogo 
              appearance={value}
              productName="Sample Product"
            />
            <div style={{ 
              marginTop: '16px', 
              fontSize: '0.875rem',
              color: background === '#1a1a1a' ? 'white' : '#333'
            }}>
              {label}
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}
```

#### Logo in Footer
```jsx
import { SafLogo, SafFooter, SafList, SafListItem, SafAnchor } from '@saffron/core-components/react';

function ApplicationFooter() {
  return (
    <SafFooter 
      productName="Thomson Reuters Legal Research"
      a11yAriaLabelAnchorGroup="Footer links"
      a11yAriaLabelSocialIcons="Social media">
      
      <SafList 
        slot="footer-links"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        <SafListItem>
          <SafAnchor href="/terms">Terms of Use</SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="/privacy">Privacy Policy</SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="/support">Support</SafAnchor>
        </SafListItem>
      </SafList>
    </SafFooter>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `appearance` | `'full-color' \| '2-color-reversed' \| '1-color-reversed' \| '1-color-black' \| '1-color-orange'` | `'full-color'` | Visual appearance variant of the logo |
| `productName` | `string` | - | Optional product name to display alongside the logo |

### Examples

#### Basic Logo Usage
```html
<div>
  <!-- Default full-color logo -->
  <saf-logo></saf-logo>
  
  <!-- Logo with product name -->
  <saf-logo productName="Legal Research Platform"></saf-logo>
  
  <!-- Black variant for light backgrounds -->
  <saf-logo appearance="1-color-black"></saf-logo>
  
  <!-- Orange variant for special cases -->
  <saf-logo appearance="1-color-orange"></saf-logo>
</div>
```

#### Application Header
```html
<header class="app-header">
  <!-- Logo section -->
  <div class="logo-section">
    <saf-logo 
      appearance="full-color"
      [productName]="applicationName">
    </saf-logo>
  </div>
  
  <!-- Navigation -->
  <saf-navigation>
    <saf-navigation-item href="/dashboard">Dashboard</saf-navigation-item>
    <saf-navigation-item href="/research">Research</saf-navigation-item>
    <saf-navigation-item href="/cases">Cases</saf-navigation-item>
    <saf-navigation-item href="/documents">Documents</saf-navigation-item>
  </saf-navigation>
  
  <!-- User actions -->
  <div class="user-actions">
    <span>Welcome, {{ currentUser.name }}</span>
    <saf-button appearance="secondary" (click)="onLogout()">
      Sign Out
    </saf-button>
  </div>
</header>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-application-header',
  templateUrl: './application-header.component.html',
  styleUrls: ['./application-header.component.scss']
})
export class ApplicationHeaderComponent {
  applicationName = 'Thomson Reuters Westlaw';
  currentUser = { name: 'John Doe' };

  onLogout() {
    // Implement logout logic
    console.log('User logged out');
  }
}
```

```scss
.app-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 24px;
  background-color: white;
  border-bottom: 1px solid #e0e0e0;
}

.logo-section {
  display: flex;
  align-items: center;
}

.user-actions {
  display: flex;
  align-items: center;
  gap: 12px;
}
```

#### Theme-Aware Logo
```html
<header [class]="'header ' + currentTheme">
  <saf-logo 
    [appearance]="getLogoAppearance()"
    [productName]="productName">
  </saf-logo>
  
  <div class="theme-toggle">
    <saf-button (click)="toggleTheme()">
      {{ currentTheme === 'light' ? 'Dark' : 'Light' }} Theme
    </saf-button>
  </div>
</header>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-theme-aware-header',
  templateUrl: './theme-aware-header.component.html',
  styleUrls: ['./theme-aware-header.component.scss']
})
export class ThemeAwareHeaderComponent {
  currentTheme: 'light' | 'dark' = 'light';
  productName = 'Thomson Reuters One';

  getLogoAppearance(): string {
    return this.currentTheme === 'dark' ? '2-color-reversed' : 'full-color';
  }

  toggleTheme() {
    this.currentTheme = this.currentTheme === 'light' ? 'dark' : 'light';
  }
}
```

```scss
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 24px;
  transition: background-color 0.3s ease;

  &.light {
    background-color: #ffffff;
    color: #333333;
  }

  &.dark {
    background-color: #1a1a1a;
    color: #ffffff;
  }
}

.theme-toggle {
  margin-left: auto;
}
```

#### Responsive Logo Service
```html
<div class="responsive-container">
  <saf-logo 
    appearance="full-color"
    [productName]="getProductName()">
  </saf-logo>
  
  <div *ngIf="isMobile && fullProductName" class="mobile-product-name">
    {{ fullProductName }}
  </div>
</div>
```

```typescript
import { Component, OnInit, OnDestroy, HostListener } from '@angular/core';

@Component({
  selector: 'app-responsive-logo',
  templateUrl: './responsive-logo.component.html',
  styleUrls: ['./responsive-logo.component.scss']
})
export class ResponsiveLogoComponent implements OnInit {
  isMobile = false;
  fullProductName = 'Thomson Reuters Professional Platform';

  ngOnInit() {
    this.checkScreenSize();
  }

  @HostListener('window:resize', ['$event'])
  onResize() {
    this.checkScreenSize();
  }

  private checkScreenSize() {
    this.isMobile = window.innerWidth < 768;
  }

  getProductName(): string | undefined {
    return this.isMobile ? undefined : this.fullProductName;
  }
}
```

#### Logo Showcase Component
```html
<div class="logo-showcase">
  <h2>Logo Appearance Variants</h2>
  
  <div class="logo-grid">
    <div 
      *ngFor="let variant of logoVariants" 
      class="logo-card"
      [style.background-color]="variant.background">
      
      <saf-logo 
        [appearance]="variant.value"
        productName="Sample Product">
      </saf-logo>
      
      <div 
        class="variant-label"
        [style.color]="variant.textColor">
        {{ variant.label }}
      </div>
    </div>
  </div>
</div>
```

```typescript
import { Component } from '@angular/core';

interface LogoVariant {
  value: string;
  label: string;
  background: string;
  textColor: string;
}

@Component({
  selector: 'app-logo-showcase',
  templateUrl: './logo-showcase.component.html',
  styleUrls: ['./logo-showcase.component.scss']
})
export class LogoShowcaseComponent {
  logoVariants: LogoVariant[] = [
    { 
      value: 'full-color', 
      label: 'Full Color', 
      background: '#ffffff', 
      textColor: '#333333' 
    },
    { 
      value: '1-color-black', 
      label: 'Black', 
      background: '#ffffff', 
      textColor: '#333333' 
    },
    { 
      value: '1-color-orange', 
      label: 'Orange', 
      background: '#ffffff', 
      textColor: '#333333' 
    },
    { 
      value: '2-color-reversed', 
      label: '2-Color Reversed', 
      background: '#1a1a1a', 
      textColor: '#ffffff' 
    },
    { 
      value: '1-color-reversed', 
      label: '1-Color Reversed', 
      background: '#1a1a1a', 
      textColor: '#ffffff' 
    }
  ];
}
```

```scss
.logo-showcase {
  padding: 24px;
}

.logo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 24px;
  margin-top: 24px;
}

.logo-card {
  padding: 24px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  text-align: center;
}

.variant-label {
  margin-top: 16px;
  font-size: 0.875rem;
}
```

## Best Practices

- **Choose appropriate appearance**: Use `full-color` for most applications, `1-color-black` for light backgrounds, and reversed variants for dark themes.
- **Consistent product naming**: Use consistent product names across your application that align with Thomson Reuters branding guidelines.
- **Responsive considerations**: Consider hiding or shortening product names on mobile devices to maintain readability.
- **Accessibility**: The logo includes proper ARIA labeling and semantic markup for screen readers.
- **Brand compliance**: Follow Thomson Reuters brand guidelines when implementing logo usage.
- **Theme support**: Use appropriate logo variants for different themes (light/dark) automatically.
- **Loading states**: Consider showing a placeholder or skeleton while the logo loads.
- **Link behavior**: Wrap the logo in an anchor tag to link to the home page when appropriate.

## Notes

- SafLogo displays the official Thomson Reuters logo with proper brand compliance.
- The component includes multiple appearance variants optimized for different backgrounds and themes.
- The logo is implemented as SVG for crisp rendering at all sizes and resolutions.
- Product names are displayed alongside the logo when provided, following Thomson Reuters branding patterns.
- The component maintains proper aspect ratios and scaling across different screen sizes.
- All logo variants include proper accessibility attributes and semantic markup.
- The logo is designed to work seamlessly with other Saffron components like SafHeader and SafFooter.
