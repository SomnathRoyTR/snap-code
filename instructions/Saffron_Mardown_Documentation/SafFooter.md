# SafFooter

A comprehensive footer component designed for Thomson Reuters applications that provides consistent branding, copyright information, navigation links, and social media links. SafFooter automatically includes the Thomson Reuters logo and generates the current year for copyright information.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `productName` | `string` | - | The name of the product to display in the copyright notice |
| `a11yAriaLabelAnchorGroup` | `string` | - | ARIA label for the footer links navigation section |
| `a11yAriaLabelSocialIcons` | `string` | - | ARIA label for the social media links navigation section |
| `children` | `ReactNode` | - | Content to be slotted into the footer |

### Slots

| Slot | Description |
|------|-------------|
| `footer-links` | Navigation links section, typically containing legal and informational links |
| `footer-social` | Social media links section for external social platforms |

### Examples

#### Basic Company Footer
```jsx
import { SafFooter, SafList, SafListItem, SafAnchor } from '@saffron/core-components/react';

function CompanyFooter() {
  return (
    <SafFooter
      productName="My Application"
      a11yAriaLabelAnchorGroup="Footer navigation links"
      a11yAriaLabelSocialIcons="Social media links">
      
      {/* Footer links slot */}
      <SafList 
        slot="footer-links"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        <SafListItem>
          <SafAnchor href="https://www.thomsonreuters.com/en/terms-of-use.html">
            Terms of Use
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="https://www.thomsonreuters.com/en/privacy-statement.html">
            Privacy Policy
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="https://www.thomsonreuters.com/en/policies/copyright.html">
            Copyright
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="https://www.thomsonreuters.com/en/privacy-statement.html#CookieIBA">
            Cookie Settings
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="/contact">
            Contact Us
          </SafAnchor>
        </SafListItem>
      </SafList>
      
      {/* Social media links slot */}
      <SafList 
        slot="footer-social"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        <SafListItem>
          <SafAnchor 
            href="https://twitter.com/thomsonreuters"
            target="_blank"
            rel="noopener noreferrer"
            ariaLabel="Follow us on Twitter">
            <SafIcon name="twitter" />
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor 
            href="https://www.linkedin.com/company/thomson-reuters"
            target="_blank"
            rel="noopener noreferrer"
            ariaLabel="Connect with us on LinkedIn">
            <SafIcon name="linkedin" />
          </SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor 
            href="https://www.youtube.com/user/thomsonreuters"
            target="_blank"
            rel="noopener noreferrer"
            ariaLabel="Watch us on YouTube">
            <SafIcon name="youtube" />
          </SafAnchor>
        </SafListItem>
      </SafList>
    </SafFooter>
  );
}
```

#### Comprehensive Application Footer
```jsx
import { SafFooter, SafList, SafListItem, SafAnchor, SafIcon } from '@saffron/core-components/react';

function ApplicationFooter() {
  const currentProduct = "Thomson Reuters Legal Research";
  
  const legalLinks = [
    { href: "https://www.thomsonreuters.com/en/terms-of-use.html", text: "Terms of Use" },
    { href: "https://www.thomsonreuters.com/en/privacy-statement.html", text: "Privacy Statement" },
    { href: "https://www.thomsonreuters.com/en/policies/copyright.html", text: "Copyright" },
    { href: "https://www.thomsonreuters.com/en/privacy-statement.html#CookieIBA", text: "Cookie Settings" },
    { href: "/accessibility", text: "Accessibility" },
    { href: "/support", text: "Support" }
  ];

  const socialLinks = [
    { 
      href: "https://twitter.com/thomsonreuters",
      icon: "twitter",
      label: "Follow Thomson Reuters on Twitter"
    },
    { 
      href: "https://www.linkedin.com/company/thomson-reuters",
      icon: "linkedin",
      label: "Connect with Thomson Reuters on LinkedIn"
    },
    { 
      href: "https://www.facebook.com/ThomsonReuters",
      icon: "facebook",
      label: "Like Thomson Reuters on Facebook"
    },
    { 
      href: "https://www.youtube.com/user/thomsonreuters",
      icon: "youtube",
      label: "Subscribe to Thomson Reuters on YouTube"
    }
  ];

  return (
    <SafFooter
      productName={currentProduct}
      a11yAriaLabelAnchorGroup="Legal and support links"
      a11yAriaLabelSocialIcons="Thomson Reuters social media">
      
      <SafList 
        slot="footer-links"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        {legalLinks.map((link, index) => (
          <SafListItem key={index}>
            <SafAnchor 
              href={link.href}
              target={link.href.startsWith('http') ? '_blank' : '_self'}
              rel={link.href.startsWith('http') ? 'noopener noreferrer' : undefined}>
              {link.text}
            </SafAnchor>
          </SafListItem>
        ))}
      </SafList>
      
      <SafList 
        slot="footer-social"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        {socialLinks.map((social, index) => (
          <SafListItem key={index}>
            <SafAnchor 
              href={social.href}
              target="_blank"
              rel="noopener noreferrer"
              ariaLabel={social.label}>
              <SafIcon name={social.icon} />
            </SafAnchor>
          </SafListItem>
        ))}
      </SafList>
    </SafFooter>
  );
}
```

#### Minimal Footer
```jsx
import { SafFooter, SafList, SafListItem, SafAnchor } from '@saffron/core-components/react';

function MinimalFooter() {
  return (
    <SafFooter
      productName="Internal Tool"
      a11yAriaLabelAnchorGroup="Essential links">
      
      <SafList 
        slot="footer-links"
        size="small"
        listStyle="none"
        order="unordered"
        inline={true}>
        <SafListItem>
          <SafAnchor href="/terms">Terms</SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="/privacy">Privacy</SafAnchor>
        </SafListItem>
        <SafListItem>
          <SafAnchor href="/help">Help</SafAnchor>
        </SafListItem>
      </SafList>
      
      {/* No social links for internal tools */}
    </SafFooter>
  );
}
```

#### Dynamic Footer with Context
```jsx
import { SafFooter, SafList, SafListItem, SafAnchor, SafIcon } from '@saffron/core-components/react';

function DynamicFooter({ appConfig, userPreferences }) {
  const getFooterLinks = () => {
    const baseLinks = [
      { href: "/terms", text: "Terms" },
      { href: "/privacy", text: "Privacy" }
    ];

    // Add context-specific links
    if (appConfig.showSupport) {
      baseLinks.push({ href: "/support", text: "Support" });
    }

    if (appConfig.showAccessibility) {
      baseLinks.push({ href: "/accessibility", text: "Accessibility" });
    }

    if (userPreferences.showAdvancedOptions) {
      baseLinks.push({ href: "/settings", text: "Settings" });
    }

    return baseLinks;
  };

  const getSocialLinks = () => {
    if (!appConfig.showSocialLinks) return [];
    
    return [
      { 
        href: "https://twitter.com/thomsonreuters",
        icon: "twitter",
        label: "Twitter"
      },
      { 
        href: "https://www.linkedin.com/company/thomson-reuters",
        icon: "linkedin",
        label: "LinkedIn"
      }
    ];
  };

  const footerLinks = getFooterLinks();
  const socialLinks = getSocialLinks();

  return (
    <SafFooter
      productName={appConfig.productName || "Thomson Reuters Application"}
      a11yAriaLabelAnchorGroup="Application links"
      a11yAriaLabelSocialIcons={socialLinks.length > 0 ? "Social media links" : undefined}>
      
      <SafList 
        slot="footer-links"
        size="medium"
        listStyle="none"
        order="unordered"
        inline={true}>
        {footerLinks.map((link, index) => (
          <SafListItem key={index}>
            <SafAnchor href={link.href}>
              {link.text}
            </SafAnchor>
          </SafListItem>
        ))}
      </SafList>
      
      {socialLinks.length > 0 && (
        <SafList 
          slot="footer-social"
          size="medium"
          listStyle="none"
          order="unordered"
          inline={true}>
          {socialLinks.map((social, index) => (
            <SafListItem key={index}>
              <SafAnchor 
                href={social.href}
                target="_blank"
                rel="noopener noreferrer"
                ariaLabel={`Visit our ${social.label} page`}>
                <SafIcon name={social.icon} />
              </SafAnchor>
            </SafListItem>
          ))}
        </SafList>
      )}
    </SafFooter>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `productName` | `string` | - | The name of the product to display in the copyright notice |
| `a11yAriaLabelAnchorGroup` | `string` | - | ARIA label for the footer links navigation section |
| `a11yAriaLabelSocialIcons` | `string` | - | ARIA label for the social media links navigation section |

### Examples

#### Basic Company Footer
```html
<saf-footer
  productName="My Application"
  a11yAriaLabelAnchorGroup="Footer navigation links"
  a11yAriaLabelSocialIcons="Social media links">
  
  <!-- Footer links slot -->
  <saf-list 
    slot="footer-links"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item>
      <saf-anchor href="https://www.thomsonreuters.com/en/terms-of-use.html">
        Terms of Use
      </saf-anchor>
    </saf-list-item>
    <saf-list-item>
      <saf-anchor href="https://www.thomsonreuters.com/en/privacy-statement.html">
        Privacy Policy
      </saf-anchor>
    </saf-list-item>
    <saf-list-item>
      <saf-anchor href="https://www.thomsonreuters.com/en/policies/copyright.html">
        Copyright
      </saf-anchor>
    </saf-list-item>
    <saf-list-item>
      <saf-anchor href="/contact">
        Contact Us
      </saf-anchor>
    </saf-list-item>
  </saf-list>
  
  <!-- Social media links slot -->
  <saf-list 
    slot="footer-social"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item>
      <saf-anchor 
        href="https://twitter.com/thomsonreuters"
        target="_blank"
        rel="noopener noreferrer"
        ariaLabel="Follow us on Twitter">
        <saf-icon name="twitter"></saf-icon>
      </saf-anchor>
    </saf-list-item>
    <saf-list-item>
      <saf-anchor 
        href="https://www.linkedin.com/company/thomson-reuters"
        target="_blank"
        rel="noopener noreferrer"
        ariaLabel="Connect with us on LinkedIn">
        <saf-icon name="linkedin"></saf-icon>
      </saf-anchor>
    </saf-list-item>
  </saf-list>
</saf-footer>
```

#### Comprehensive Application Footer
```html
<saf-footer
  [productName]="currentProduct"
  a11yAriaLabelAnchorGroup="Legal and support links"
  a11yAriaLabelSocialIcons="Thomson Reuters social media">
  
  <saf-list 
    slot="footer-links"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item *ngFor="let link of legalLinks">
      <saf-anchor 
        [href]="link.href"
        [target]="link.href.startsWith('http') ? '_blank' : '_self'"
        [rel]="link.href.startsWith('http') ? 'noopener noreferrer' : null">
        {{ link.text }}
      </saf-anchor>
    </saf-list-item>
  </saf-list>
  
  <saf-list 
    slot="footer-social"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item *ngFor="let social of socialLinks">
      <saf-anchor 
        [href]="social.href"
        target="_blank"
        rel="noopener noreferrer"
        [ariaLabel]="social.label">
        <saf-icon [name]="social.icon"></saf-icon>
      </saf-anchor>
    </saf-list-item>
  </saf-list>
</saf-footer>
```

```typescript
import { Component } from '@angular/core';

interface FooterLink {
  href: string;
  text: string;
}

interface SocialLink {
  href: string;
  icon: string;
  label: string;
}

@Component({
  selector: 'app-application-footer',
  templateUrl: './application-footer.component.html'
})
export class ApplicationFooterComponent {
  currentProduct = "Thomson Reuters Legal Research";
  
  legalLinks: FooterLink[] = [
    { href: "https://www.thomsonreuters.com/en/terms-of-use.html", text: "Terms of Use" },
    { href: "https://www.thomsonreuters.com/en/privacy-statement.html", text: "Privacy Statement" },
    { href: "https://www.thomsonreuters.com/en/policies/copyright.html", text: "Copyright" },
    { href: "https://www.thomsonreuters.com/en/privacy-statement.html#CookieIBA", text: "Cookie Settings" },
    { href: "/accessibility", text: "Accessibility" },
    { href: "/support", text: "Support" }
  ];

  socialLinks: SocialLink[] = [
    { 
      href: "https://twitter.com/thomsonreuters",
      icon: "twitter",
      label: "Follow Thomson Reuters on Twitter"
    },
    { 
      href: "https://www.linkedin.com/company/thomson-reuters",
      icon: "linkedin",
      label: "Connect with Thomson Reuters on LinkedIn"
    },
    { 
      href: "https://www.facebook.com/ThomsonReuters",
      icon: "facebook",
      label: "Like Thomson Reuters on Facebook"
    },
    { 
      href: "https://www.youtube.com/user/thomsonreuters",
      icon: "youtube",
      label: "Subscribe to Thomson Reuters on YouTube"
    }
  ];
}
```

#### Dynamic Footer with Service
```html
<saf-footer
  [productName]="footerService.getProductName()"
  [a11yAriaLabelAnchorGroup]="footerService.getLinksAriaLabel()"
  [a11yAriaLabelSocialIcons]="footerService.getSocialAriaLabel()">
  
  <saf-list 
    slot="footer-links"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item *ngFor="let link of footerService.getFooterLinks()">
      <saf-anchor [href]="link.href">
        {{ link.text }}
      </saf-anchor>
    </saf-list-item>
  </saf-list>
  
  <saf-list 
    *ngIf="footerService.shouldShowSocialLinks()"
    slot="footer-social"
    size="medium"
    listStyle="none"
    order="unordered"
    [inline]="true">
    <saf-list-item *ngFor="let social of footerService.getSocialLinks()">
      <saf-anchor 
        [href]="social.href"
        target="_blank"
        rel="noopener noreferrer"
        [ariaLabel]="social.label">
        <saf-icon [name]="social.icon"></saf-icon>
      </saf-anchor>
    </saf-list-item>
  </saf-list>
</saf-footer>
```

```typescript
import { Component } from '@angular/core';
import { FooterService } from './footer.service';

@Component({
  selector: 'app-dynamic-footer',
  templateUrl: './dynamic-footer.component.html'
})
export class DynamicFooterComponent {
  constructor(public footerService: FooterService) {}
}

// footer.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class FooterService {
  private appConfig = {
    productName: 'Thomson Reuters Application',
    showSocialLinks: true,
    showSupport: true
  };

  getProductName(): string {
    return this.appConfig.productName;
  }

  getLinksAriaLabel(): string {
    return 'Application navigation links';
  }

  getSocialAriaLabel(): string {
    return this.shouldShowSocialLinks() ? 'Social media links' : '';
  }

  getFooterLinks(): FooterLink[] {
    const baseLinks = [
      { href: '/terms', text: 'Terms' },
      { href: '/privacy', text: 'Privacy' }
    ];

    if (this.appConfig.showSupport) {
      baseLinks.push({ href: '/support', text: 'Support' });
    }

    return baseLinks;
  }

  getSocialLinks(): SocialLink[] {
    return [
      { 
        href: 'https://twitter.com/thomsonreuters',
        icon: 'twitter',
        label: 'Twitter'
      },
      { 
        href: 'https://www.linkedin.com/company/thomson-reuters',
        icon: 'linkedin',
        label: 'LinkedIn'
      }
    ];
  }

  shouldShowSocialLinks(): boolean {
    return this.appConfig.showSocialLinks;
  }
}
```

## Best Practices

- **Consistent product naming**: Use a clear, descriptive `productName` that matches your application's branding.
- **Accessibility first**: Always provide meaningful ARIA labels for the navigation sections to help screen readers.
- **Link organization**: Group related links logically - legal/policy links in the main section, social media in the social section.
- **External link safety**: Use `target="_blank"` and `rel="noopener noreferrer"` for external links to ensure security.
- **Responsive considerations**: The footer layout adapts to different screen sizes automatically.
- **Legal compliance**: Include required legal links like Terms, Privacy, and Cookie policies.
- **Social media guidelines**: Only include social media links that are actively maintained and relevant to your users.
- **Icon accessibility**: Provide descriptive ARIA labels for social media icons.

## Notes

- SafFooter automatically includes the Thomson Reuters logo and generates the current year in the copyright notice.
- The component uses slots to provide flexible content placement while maintaining consistent structure and styling.
- The footer includes proper semantic HTML with `<footer>` and `<nav>` elements for better accessibility.
- The copyright notice format is: "© [Current Year] Thomson Reuters. [Product Name]"
- The component is designed to be placed at the bottom of page layouts and will expand to full width.
- All navigation elements are properly labeled for screen readers and keyboard navigation.
- The footer maintains Thomson Reuters branding guidelines while allowing product-specific customization.
