# SafActionCard Component

## Overview

SafActionCard is a specialized card component designed to display actionable content with prominent call-to-action buttons or interactive elements. It extends the basic card functionality to emphasize user actions and provides clear visual hierarchy for decision-making interfaces. SafActionCard is commonly used for feature highlights, pricing plans, product showcases, and workflow decision points.

## React API

### SafActionCard

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `title` | `string \| ReactNode` | No | - | Primary title or heading text |
| `subtitle` | `string \| ReactNode` | No | - | Secondary title or description |
| `description` | `string \| ReactNode` | No | - | Main content description |
| `image` | `string \| ReactNode` | No | - | Image URL or custom image element |
| `imageAlt` | `string` | No | - | Alternative text for the image |
| `variant` | `'outlined' \| 'filled' \| 'elevated'` | No | `'outlined'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the card |
| `orientation` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Layout orientation |
| `primaryAction` | `ActionConfig` | No | - | Primary action button configuration |
| `secondaryAction` | `ActionConfig` | No | - | Secondary action button configuration |
| `actions` | `ActionConfig[]` | No | - | Array of action configurations |
| `badge` | `string \| ReactNode` | No | - | Badge or label for the card |
| `status` | `'default' \| 'featured' \| 'disabled' \| 'selected'` | No | `'default'` | Visual status of the card |
| `clickable` | `boolean` | No | `false` | Whether the entire card is clickable |
| `loading` | `boolean` | No | `false` | Whether to show loading state |
| `disabled` | `boolean` | No | `false` | Whether the card is disabled |
| `fullWidth` | `boolean` | No | `false` | Whether card takes full container width |
| `showBorder` | `boolean` | No | `true` | Whether to show card border |
| `showShadow` | `boolean` | No | `true` | Whether to show card shadow |
| `onClick` | `(event: MouseEvent) => void` | No | - | Callback when card is clicked |
| `onPrimaryAction` | `(event: MouseEvent) => void` | No | - | Callback for primary action |
| `onSecondaryAction` | `(event: MouseEvent) => void` | No | - | Callback for secondary action |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### ActionConfig Interface

```typescript
interface ActionConfig {
  label: string;
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  size?: 'small' | 'medium' | 'large';
  icon?: string | ReactNode;
  disabled?: boolean;
  loading?: boolean;
  onClick?: (event: MouseEvent) => void;
}
```

## Angular API

### saf-action-card

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[title]` | `string \| TemplateRef` | No | - | Primary title or heading text |
| `[subtitle]` | `string \| TemplateRef` | No | - | Secondary title or description |
| `[description]` | `string \| TemplateRef` | No | - | Main content description |
| `[image]` | `string \| TemplateRef` | No | - | Image URL or custom image element |
| `[imageAlt]` | `string` | No | - | Alternative text for the image |
| `[variant]` | `'outlined' \| 'filled' \| 'elevated'` | No | `'outlined'` | Visual style variant |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the card |
| `[orientation]` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Layout orientation |
| `[primaryAction]` | `ActionConfig` | No | - | Primary action button configuration |
| `[secondaryAction]` | `ActionConfig` | No | - | Secondary action button configuration |
| `[actions]` | `ActionConfig[]` | No | - | Array of action configurations |
| `[badge]` | `string \| TemplateRef` | No | - | Badge or label for the card |
| `[status]` | `'default' \| 'featured' \| 'disabled' \| 'selected'` | No | `'default'` | Visual status of the card |
| `[clickable]` | `boolean` | No | `false` | Whether the entire card is clickable |
| `[loading]` | `boolean` | No | `false` | Whether to show loading state |
| `[disabled]` | `boolean` | No | `false` | Whether the card is disabled |
| `[fullWidth]` | `boolean` | No | `false` | Whether card takes full container width |
| `[showBorder]` | `boolean` | No | `true` | Whether to show card border |
| `[showShadow]` | `boolean` | No | `true` | Whether to show card shadow |
| `(click)` | `EventEmitter<MouseEvent>` | No | - | Event when card is clicked |
| `(primaryAction)` | `EventEmitter<MouseEvent>` | No | - | Event for primary action |
| `(secondaryAction)` | `EventEmitter<MouseEvent>` | No | - | Event for secondary action |

## Usage Examples

### Basic Action Cards

#### React
```jsx
import { SafActionCard, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const BasicActionCardExample = () => {
  const [selectedPlan, setSelectedPlan] = useState(null);

  const handlePlanSelect = (planId) => {
    setSelectedPlan(planId);
    console.log('Selected plan:', planId);
  };

  return (
    <div className="action-card-demo">
      <h2>Choose Your Plan</h2>
      
      <div className="plans-grid">
        <SafActionCard
          title="Basic Plan"
          subtitle="Perfect for individuals"
          description="Get started with essential features for personal use"
          badge="Most Popular"
          variant="outlined"
          status={selectedPlan === 'basic' ? 'selected' : 'default'}
          primaryAction={{
            label: 'Select Basic',
            variant: 'primary',
            onClick: () => handlePlanSelect('basic')
          }}
          secondaryAction={{
            label: 'Learn More',
            variant: 'outline',
            onClick: () => console.log('Learn more about basic plan')
          }}
          onClick={() => setSelectedPlan('basic')}
          clickable={true}
        >
          <div className="plan-features">
            <ul>
              <li>Up to 5 projects</li>
              <li>10GB storage</li>
              <li>Email support</li>
              <li>Basic analytics</li>
            </ul>
            <div className="price">
              <span className="currency">$</span>
              <span className="amount">9</span>
              <span className="period">/month</span>
            </div>
          </div>
        </SafActionCard>

        <SafActionCard
          title="Pro Plan"
          subtitle="For growing teams"
          description="Advanced features and collaboration tools for professional use"
          badge={<SafBadge variant="success">Recommended</SafBadge>}
          variant="filled"
          status={selectedPlan === 'pro' ? 'selected' : 'featured'}
          primaryAction={{
            label: 'Select Pro',
            variant: 'primary',
            onClick: () => handlePlanSelect('pro')
          }}
          secondaryAction={{
            label: 'Try Free',
            variant: 'outline',
            onClick: () => console.log('Try pro plan free')
          }}
          onClick={() => setSelectedPlan('pro')}
          clickable={true}
        >
          <div className="plan-features">
            <ul>
              <li>Unlimited projects</li>
              <li>100GB storage</li>
              <li>Priority support</li>
              <li>Advanced analytics</li>
              <li>Team collaboration</li>
              <li>API access</li>
            </ul>
            <div className="price">
              <span className="currency">$</span>
              <span className="amount">29</span>
              <span className="period">/month</span>
            </div>
          </div>
        </SafActionCard>

        <SafActionCard
          title="Enterprise"
          subtitle="For large organizations"
          description="Custom solutions with dedicated support and advanced security"
          variant="elevated"
          status={selectedPlan === 'enterprise' ? 'selected' : 'default'}
          primaryAction={{
            label: 'Contact Sales',
            variant: 'primary',
            icon: <SafIcon name="phone" />,
            onClick: () => handlePlanSelect('enterprise')
          }}
          secondaryAction={{
            label: 'Get Quote',
            variant: 'outline',
            onClick: () => console.log('Get enterprise quote')
          }}
          onClick={() => setSelectedPlan('enterprise')}
          clickable={true}
        >
          <div className="plan-features">
            <ul>
              <li>Custom projects limit</li>
              <li>Unlimited storage</li>
              <li>Dedicated support</li>
              <li>Custom analytics</li>
              <li>Advanced security</li>
              <li>SLA guarantee</li>
              <li>Custom integrations</li>
            </ul>
            <div className="price">
              <span className="currency">$</span>
              <span className="amount">99</span>
              <span className="period">/month</span>
            </div>
          </div>
        </SafActionCard>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// basic-action-card.component.ts
import { Component } from '@angular/core';

interface ActionConfig {
  label: string;
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  onClick?: () => void;
}

@Component({
  selector: 'app-basic-action-card',
  template: `
    <div class="action-card-demo">
      <h2>Choose Your Plan</h2>
      
      <div class="plans-grid">
        <saf-action-card
          title="Basic Plan"
          subtitle="Perfect for individuals"
          description="Get started with essential features for personal use"
          badge="Most Popular"
          variant="outlined"
          [status]="selectedPlan === 'basic' ? 'selected' : 'default'"
          [primaryAction]="basicPrimaryAction"
          [secondaryAction]="basicSecondaryAction"
          [clickable]="true"
          (click)="selectPlan('basic')">
          
          <div class="plan-features">
            <ul>
              <li>Up to 5 projects</li>
              <li>10GB storage</li>
              <li>Email support</li>
              <li>Basic analytics</li>
            </ul>
            <div class="price">
              <span class="currency">$</span>
              <span class="amount">9</span>
              <span class="period">/month</span>
            </div>
          </div>
        </saf-action-card>

        <saf-action-card
          title="Pro Plan"
          subtitle="For growing teams"
          description="Advanced features and collaboration tools for professional use"
          variant="filled"
          [status]="selectedPlan === 'pro' ? 'selected' : 'featured'"
          [primaryAction]="proPrimaryAction"
          [secondaryAction]="proSecondaryAction"
          [clickable]="true"
          (click)="selectPlan('pro')">
          
          <saf-badge slot="badge" variant="success">Recommended</saf-badge>
          
          <div class="plan-features">
            <ul>
              <li>Unlimited projects</li>
              <li>100GB storage</li>
              <li>Priority support</li>
              <li>Advanced analytics</li>
              <li>Team collaboration</li>
              <li>API access</li>
            </ul>
            <div class="price">
              <span class="currency">$</span>
              <span class="amount">29</span>
              <span class="period">/month</span>
            </div>
          </div>
        </saf-action-card>

        <saf-action-card
          title="Enterprise"
          subtitle="For large organizations"
          description="Custom solutions with dedicated support and advanced security"
          variant="elevated"
          [status]="selectedPlan === 'enterprise' ? 'selected' : 'default'"
          [primaryAction]="enterprisePrimaryAction"
          [secondaryAction]="enterpriseSecondaryAction"
          [clickable]="true"
          (click)="selectPlan('enterprise')">
          
          <div class="plan-features">
            <ul>
              <li>Custom projects limit</li>
              <li>Unlimited storage</li>
              <li>Dedicated support</li>
              <li>Custom analytics</li>
              <li>Advanced security</li>
              <li>SLA guarantee</li>
              <li>Custom integrations</li>
            </ul>
            <div class="price">
              <span class="currency">$</span>
              <span class="amount">99</span>
              <span class="period">/month</span>
            </div>
          </div>
        </saf-action-card>
      </div>
    </div>
  `
})
export class BasicActionCardComponent {
  selectedPlan: string | null = null;

  basicPrimaryAction: ActionConfig = {
    label: 'Select Basic',
    variant: 'primary',
    onClick: () => this.selectPlan('basic')
  };

  basicSecondaryAction: ActionConfig = {
    label: 'Learn More',
    variant: 'outline',
    onClick: () => console.log('Learn more about basic plan')
  };

  proPrimaryAction: ActionConfig = {
    label: 'Select Pro',
    variant: 'primary',
    onClick: () => this.selectPlan('pro')
  };

  proSecondaryAction: ActionConfig = {
    label: 'Try Free',
    variant: 'outline',
    onClick: () => console.log('Try pro plan free')
  };

  enterprisePrimaryAction: ActionConfig = {
    label: 'Contact Sales',
    variant: 'primary',
    onClick: () => this.selectPlan('enterprise')
  };

  enterpriseSecondaryAction: ActionConfig = {
    label: 'Get Quote',
    variant: 'outline',
    onClick: () => console.log('Get enterprise quote')
  };

  selectPlan(planId: string) {
    this.selectedPlan = planId;
    console.log('Selected plan:', planId);
  }
}
```

### Horizontal Action Cards with Images

#### React
```jsx
import { SafActionCard, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const HorizontalActionCardExample = () => {
  const [loading, setLoading] = useState({});

  const handleAction = async (actionType, itemId) => {
    setLoading(prev => ({ ...prev, [itemId]: true }));
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    setLoading(prev => ({ ...prev, [itemId]: false }));
    console.log(`${actionType} action for item ${itemId}`);
  };

  const products = [
    {
      id: 'product-1',
      title: 'Thomson Reuters Westlaw',
      subtitle: 'Legal Research Platform',
      description: 'Comprehensive legal research with AI-powered insights and extensive case law database.',
      image: '/images/westlaw-logo.png',
      badge: 'Best Seller',
      status: 'featured'
    },
    {
      id: 'product-2',
      title: 'Thomson Reuters CLEAR',
      subtitle: 'Investigation Software',
      description: 'Advanced investigation and risk management tools for compliance professionals.',
      image: '/images/clear-logo.png',
      badge: 'New',
      status: 'default'
    },
    {
      id: 'product-3',
      title: 'Thomson Reuters Practical Law',
      subtitle: 'Legal Guidance',
      description: 'Practical legal guidance, know-how, and precedents for everyday legal work.',
      image: '/images/practical-law-logo.png',
      badge: null,
      status: 'default'
    }
  ];

  return (
    <div className="horizontal-action-cards">
      <h2>Featured Products</h2>
      
      <div className="products-list">
        {products.map(product => (
          <SafActionCard
            key={product.id}
            title={product.title}
            subtitle={product.subtitle}
            description={product.description}
            image={product.image}
            imageAlt={`${product.title} logo`}
            badge={product.badge}
            orientation="horizontal"
            variant="outlined"
            status={product.status}
            size="large"
            loading={loading[product.id]}
            primaryAction={{
              label: 'Start Free Trial',
              variant: 'primary',
              loading: loading[product.id],
              onClick: () => handleAction('trial', product.id)
            }}
            secondaryAction={{
              label: 'Learn More',
              variant: 'outline',
              icon: <SafIcon name="arrow-right" />,
              onClick: () => handleAction('learn', product.id)
            }}
            actions={[
              {
                label: 'Watch Demo',
                variant: 'ghost',
                icon: <SafIcon name="play" />,
                onClick: () => handleAction('demo', product.id)
              },
              {
                label: 'Contact Sales',
                variant: 'ghost',
                icon: <SafIcon name="phone" />,
                onClick: () => handleAction('contact', product.id)
              }
            ]}
            fullWidth={true}
          />
        ))}
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// horizontal-action-card.component.ts
import { Component } from '@angular/core';

interface Product {
  id: string;
  title: string;
  subtitle: string;
  description: string;
  image: string;
  badge: string | null;
  status: 'default' | 'featured';
}

@Component({
  selector: 'app-horizontal-action-card',
  template: `
    <div class="horizontal-action-cards">
      <h2>Featured Products</h2>
      
      <div class="products-list">
        <saf-action-card
          *ngFor="let product of products"
          [title]="product.title"
          [subtitle]="product.subtitle"
          [description]="product.description"
          [image]="product.image"
          [imageAlt]="product.title + ' logo'"
          [badge]="product.badge"
          orientation="horizontal"
          variant="outlined"
          [status]="product.status"
          size="large"
          [loading]="loading[product.id]"
          [primaryAction]="getPrimaryAction(product.id)"
          [secondaryAction]="getSecondaryAction(product.id)"
          [actions]="getAdditionalActions(product.id)"
          [fullWidth]="true">
        </saf-action-card>
      </div>
    </div>
  `
})
export class HorizontalActionCardComponent {
  loading: { [key: string]: boolean } = {};

  products: Product[] = [
    {
      id: 'product-1',
      title: 'Thomson Reuters Westlaw',
      subtitle: 'Legal Research Platform',
      description: 'Comprehensive legal research with AI-powered insights and extensive case law database.',
      image: '/images/westlaw-logo.png',
      badge: 'Best Seller',
      status: 'featured'
    },
    {
      id: 'product-2',
      title: 'Thomson Reuters CLEAR',
      subtitle: 'Investigation Software',
      description: 'Advanced investigation and risk management tools for compliance professionals.',
      image: '/images/clear-logo.png',
      badge: 'New',
      status: 'default'
    },
    {
      id: 'product-3',
      title: 'Thomson Reuters Practical Law',
      subtitle: 'Legal Guidance',
      description: 'Practical legal guidance, know-how, and precedents for everyday legal work.',
      image: '/images/practical-law-logo.png',
      badge: null,
      status: 'default'
    }
  ];

  async handleAction(actionType: string, itemId: string) {
    this.loading = { ...this.loading, [itemId]: true };
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    this.loading = { ...this.loading, [itemId]: false };
    console.log(`${actionType} action for item ${itemId}`);
  }

  getPrimaryAction(productId: string): ActionConfig {
    return {
      label: 'Start Free Trial',
      variant: 'primary',
      loading: this.loading[productId],
      onClick: () => this.handleAction('trial', productId)
    };
  }

  getSecondaryAction(productId: string): ActionConfig {
    return {
      label: 'Learn More',
      variant: 'outline',
      onClick: () => this.handleAction('learn', productId)
    };
  }

  getAdditionalActions(productId: string): ActionConfig[] {
    return [
      {
        label: 'Watch Demo',
        variant: 'ghost',
        onClick: () => this.handleAction('demo', productId)
      },
      {
        label: 'Contact Sales',
        variant: 'ghost',
        onClick: () => this.handleAction('contact', productId)
      }
    ];
  }
}
```

## Best Practices

1. **Clear Call-to-Action**
   - Use primary actions for the most important user action
   - Limit the number of actions to avoid decision paralysis
   - Make action labels specific and action-oriented

2. **Visual Hierarchy**
   - Use status and variants to guide user attention
   - Featured cards should stand out for recommended options
   - Maintain consistent spacing and alignment

3. **Content Organization**
   - Keep titles concise and descriptive
   - Use subtitles for context or categorization
   - Provide clear, benefit-focused descriptions

4. **Responsive Design**
   - Consider horizontal layout for desktop, vertical for mobile
   - Use appropriate sizing for different screen sizes
   - Ensure touch targets are adequately sized

5. **Loading and States**
   - Show loading states during async operations
   - Provide clear feedback for user interactions
   - Handle disabled states appropriately

## Accessibility Considerations

1. **ARIA Support**
   - Use proper ARIA labels for card regions
   - Implement `aria-pressed` for selection states
   - Provide meaningful descriptions for screen readers

2. **Keyboard Navigation**
   - Support Tab navigation through interactive elements
   - Implement Enter/Space activation for clickable cards
   - Ensure focus indicators are clearly visible

3. **Screen Reader Compatibility**
   - Announce card status and state changes
   - Provide context for actions and interactions
   - Use semantic markup for content structure

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all text
   - Don't rely solely on color for status indication
   - Support high contrast and reduced motion preferences

## Related Components

- **SafCard**: Basic card container component
- **SafButton**: Individual action buttons
- **SafBadge**: Status and label indicators
- **SafIcon**: Icons for actions and status
- **SafActionCardAction**: Individual action sub-component

## Notes

- Action cards automatically handle layout and spacing for different orientations
- Custom CSS variables available for comprehensive theming
- Built-in support for loading states and async operations
- Optimized for both touch and mouse interactions
- Compatible with form validation and state management libraries
- Supports both controlled and uncontrolled usage patterns
