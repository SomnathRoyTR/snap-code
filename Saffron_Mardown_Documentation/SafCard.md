# SafCard Component Documentation

## Overview

The **SafCard** component is a versatile container that groups related information and actions in a cohesive, visually distinct element. It supports multiple layouts (vertical, horizontal), density options, image bleeding, and comprehensive content organization with slots for headers, content, actions, and media.

## React Implementation

### Basic Usage

```tsx
import { SafCard } from '@saffron/react-components';

function BasicCard() {
  return (
    <SafCard appearance="vertical" density="comfortable">
      <img slot="media" src="/api/placeholder/300/200" alt="Product preview" />
      <h3 slot="header">Product Title</h3>
      <p slot="content">
        This is a brief description of the product that provides key information 
        to help users understand what they're looking at.
      </p>
      <div slot="actions">
        <button className="btn-primary">Learn More</button>
        <button className="btn-secondary">Add to Cart</button>
      </div>
    </SafCard>
  );
}
```

### Advanced Product Gallery

```tsx
import { SafCard } from '@saffron/react-components';
import { useState } from 'react';

function ProductGallery() {
  const [products] = useState([
    {
      id: 1,
      title: 'Wireless Headphones',
      price: 199.99,
      originalPrice: 249.99,
      rating: 4.5,
      image: '/api/placeholder/300/200',
      badge: 'Sale',
      description: 'Premium wireless headphones with noise cancellation.',
      inStock: true,
      category: 'Electronics'
    },
    {
      id: 2,
      title: 'Smart Watch',
      price: 299.99,
      rating: 4.8,
      image: '/api/placeholder/300/200',
      badge: 'New',
      description: 'Advanced fitness tracking with heart rate monitoring.',
      inStock: true,
      category: 'Wearables'
    },
    {
      id: 3,
      title: 'Laptop Backpack',
      price: 79.99,
      rating: 4.2,
      image: '/api/placeholder/300/200',
      description: 'Durable backpack designed for modern professionals.',
      inStock: false,
      category: 'Accessories'
    }
  ]);

  const [selectedProduct, setSelectedProduct] = useState(null);

  const handleAddToCart = (product) => {
    console.log('Added to cart:', product);
    // Add to cart logic
  };

  const handleViewDetails = (product) => {
    setSelectedProduct(product);
  };

  const formatPrice = (price) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD'
    }).format(price);
  };

  const renderRating = (rating) => {
    return '⭐'.repeat(Math.floor(rating)) + (rating % 1 ? '⭐' : '');
  };

  return (
    <div className="product-gallery">
      <h2>Featured Products</h2>
      
      <div className="products-grid">
        {products.map(product => (
          <SafCard
            key={product.id}
            appearance="vertical"
            density="comfortable"
            imageBleed={true}
            headingLevel={3}
            className={`product-card ${!product.inStock ? 'out-of-stock' : ''}`}
          >
            <div slot="media" className="product-image-container">
              <img 
                src={product.image} 
                alt={product.title}
                className="product-image"
              />
              {product.badge && (
                <span className={`product-badge badge-${product.badge.toLowerCase()}`}>
                  {product.badge}
                </span>
              )}
              {!product.inStock && (
                <div className="out-of-stock-overlay">
                  Out of Stock
                </div>
              )}
            </div>

            <div slot="header" className="product-header">
              <h3 className="product-title">{product.title}</h3>
              <div className="product-meta">
                <span className="product-category">{product.category}</span>
                <div className="product-rating">
                  <span className="rating-stars">{renderRating(product.rating)}</span>
                  <span className="rating-value">({product.rating})</span>
                </div>
              </div>
            </div>

            <div slot="content" className="product-content">
              <p className="product-description">{product.description}</p>
              <div className="product-pricing">
                <span className="current-price">{formatPrice(product.price)}</span>
                {product.originalPrice && (
                  <span className="original-price">{formatPrice(product.originalPrice)}</span>
                )}
              </div>
            </div>

            <div slot="actions" className="product-actions">
              <button
                className="btn-primary"
                onClick={() => handleAddToCart(product)}
                disabled={!product.inStock}
              >
                {product.inStock ? 'Add to Cart' : 'Notify Me'}
              </button>
              <button
                className="btn-secondary"
                onClick={() => handleViewDetails(product)}
              >
                View Details
              </button>
            </div>
          </SafCard>
        ))}
      </div>

      {selectedProduct && (
        <div className="product-modal">
          <div className="modal-content">
            <h2>{selectedProduct.title}</h2>
            <p>Detailed product information would go here...</p>
            <button onClick={() => setSelectedProduct(null)}>Close</button>
          </div>
        </div>
      )}
    </div>
  );
}
```

### Dashboard Cards

```tsx
import { SafCard } from '@saffron/react-components';
import { useState, useEffect } from 'react';

function DashboardCards() {
  const [metrics, setMetrics] = useState({
    totalSales: { value: 0, target: 125000, change: 0 },
    newCustomers: { value: 0, target: 250, change: 0 },
    conversion: { value: 0, target: 3.5, change: 0 },
    avgOrder: { value: 0, target: 85, change: 0 }
  });

  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    // Simulate data loading
    setTimeout(() => {
      setMetrics({
        totalSales: { value: 132450, target: 125000, change: 12.5 },
        newCustomers: { value: 287, target: 250, change: 23.2 },
        conversion: { value: 3.8, target: 3.5, change: 8.6 },
        avgOrder: { value: 92.35, target: 85, change: 8.6 }
      });
      setIsLoading(false);
    }, 2000);
  }, []);

  const formatMetricValue = (key, value) => {
    switch (key) {
      case 'totalSales':
      case 'avgOrder':
        return new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD'
        }).format(value);
      case 'conversion':
        return `${value.toFixed(1)}%`;
      default:
        return Math.round(value).toLocaleString();
    }
  };

  const getChangeColor = (change) => {
    if (change > 0) return 'positive';
    if (change < 0) return 'negative';
    return 'neutral';
  };

  const getChangeIcon = (change) => {
    if (change > 0) return '📈';
    if (change < 0) return '📉';
    return '➖';
  };

  const metricConfigs = {
    totalSales: {
      title: 'Total Sales',
      subtitle: 'This month',
      icon: '💰',
      color: 'blue'
    },
    newCustomers: {
      title: 'New Customers',
      subtitle: 'This month',
      icon: '👥',
      color: 'green'
    },
    conversion: {
      title: 'Conversion Rate',
      subtitle: 'This month',
      icon: '🎯',
      color: 'purple'
    },
    avgOrder: {
      title: 'Avg Order Value',
      subtitle: 'This month',
      icon: '🛒',
      color: 'orange'
    }
  };

  return (
    <div className="dashboard">
      <h2>Performance Dashboard</h2>
      
      <div className="metrics-grid">
        {Object.entries(metrics).map(([key, metric]) => {
          const config = metricConfigs[key];
          const progressPercentage = Math.min((metric.value / metric.target) * 100, 100);
          
          return (
            <SafCard
              key={key}
              appearance="vertical"
              density="comfortable"
              className={`metric-card metric-${config.color}`}
            >
              <div slot="header" className="metric-header">
                <div className="metric-icon">{config.icon}</div>
                <div className="metric-title-group">
                  <h3 className="metric-title">{config.title}</h3>
                  <span className="metric-subtitle">{config.subtitle}</span>
                </div>
              </div>

              <div slot="content" className="metric-content">
                {isLoading ? (
                  <div className="metric-loading">
                    <div className="skeleton-text large"></div>
                    <div className="skeleton-text medium"></div>
                  </div>
                ) : (
                  <>
                    <div className="metric-value">
                      {formatMetricValue(key, metric.value)}
                    </div>
                    
                    <div className="metric-details">
                      <div className={`metric-change ${getChangeColor(metric.change)}`}>
                        <span className="change-icon">{getChangeIcon(metric.change)}</span>
                        <span className="change-value">
                          {Math.abs(metric.change).toFixed(1)}%
                        </span>
                        <span className="change-label">vs last month</span>
                      </div>
                      
                      <div className="metric-progress">
                        <div className="progress-bar">
                          <div 
                            className="progress-fill"
                            style={{ width: `${progressPercentage}%` }}
                          ></div>
                        </div>
                        <div className="progress-label">
                          {Math.round(progressPercentage)}% of target
                        </div>
                      </div>
                    </div>
                  </>
                )}
              </div>

              <div slot="actions" className="metric-actions">
                <button className="btn-secondary">View Details</button>
              </div>
            </SafCard>
          );
        })}
      </div>

      <div className="additional-cards">
        <SafCard appearance="horizontal" density="spacious" className="announcement-card">
          <div slot="media" className="announcement-icon">
            📢
          </div>
          <div slot="header">
            <h3>New Feature Release</h3>
          </div>
          <div slot="content">
            <p>Advanced analytics dashboard is now available with real-time insights and custom reporting capabilities.</p>
          </div>
          <div slot="actions">
            <button className="btn-primary">Learn More</button>
            <button className="btn-secondary">Dismiss</button>
          </div>
        </SafCard>

        <SafCard appearance="vertical" density="comfortable" className="quick-actions-card">
          <div slot="header">
            <h3>Quick Actions</h3>
          </div>
          <div slot="content" className="quick-actions-grid">
            <button className="quick-action">
              <span className="action-icon">📊</span>
              <span className="action-label">Generate Report</span>
            </button>
            <button className="quick-action">
              <span className="action-icon">👥</span>
              <span className="action-label">Invite Users</span>
            </button>
            <button className="quick-action">
              <span className="action-icon">⚙️</span>
              <span className="action-label">Settings</span>
            </button>
            <button className="quick-action">
              <span className="action-icon">💬</span>
              <span className="action-label">Support</span>
            </button>
          </div>
        </SafCard>
      </div>
    </div>
  );
}
```

### Interactive Content Cards

```tsx
import { SafCard } from '@saffron/react-components';
import { useState } from 'react';

function InteractiveCards() {
  const [selectedCard, setSelectedCard] = useState(null);
  const [favorites, setFavorites] = useState(new Set());

  const articles = [
    {
      id: 1,
      title: 'Getting Started with Design Systems',
      excerpt: 'Learn the fundamentals of building scalable design systems...',
      author: 'Sarah Johnson',
      date: '2024-01-15',
      readTime: '5 min read',
      category: 'Design',
      image: '/api/placeholder/400/250',
      tags: ['design systems', 'ui/ux', 'frontend']
    },
    {
      id: 2,
      title: 'Advanced React Patterns',
      excerpt: 'Explore advanced patterns and techniques for React development...',
      author: 'Mike Chen',
      date: '2024-01-12',
      readTime: '8 min read',
      category: 'Development',
      image: '/api/placeholder/400/250',
      tags: ['react', 'javascript', 'patterns']
    },
    {
      id: 3,
      title: 'Accessibility Best Practices',
      excerpt: 'Essential guidelines for creating inclusive web experiences...',
      author: 'Alex Rivera',
      date: '2024-01-10',
      readTime: '6 min read',
      category: 'Accessibility',
      image: '/api/placeholder/400/250',
      tags: ['a11y', 'wcag', 'inclusive design']
    }
  ];

  const toggleFavorite = (articleId) => {
    setFavorites(prev => {
      const newFavorites = new Set(prev);
      if (newFavorites.has(articleId)) {
        newFavorites.delete(articleId);
      } else {
        newFavorites.add(articleId);
      }
      return newFavorites;
    });
  };

  const handleCardClick = (article) => {
    setSelectedCard(selectedCard?.id === article.id ? null : article);
  };

  return (
    <div className="interactive-cards">
      <h2>Latest Articles</h2>
      
      <div className="articles-grid">
        {articles.map(article => (
          <SafCard
            key={article.id}
            appearance="vertical"
            density="comfortable"
            imageBleed={true}
            className={`article-card ${selectedCard?.id === article.id ? 'selected' : ''}`}
            onClick={() => handleCardClick(article)}
          >
            <div slot="media" className="article-image-container">
              <img 
                src={article.image} 
                alt={article.title}
                className="article-image"
              />
              <div className="article-overlay">
                <span className="category-badge">{article.category}</span>
                <button
                  className={`favorite-btn ${favorites.has(article.id) ? 'favorited' : ''}`}
                  onClick={(e) => {
                    e.stopPropagation();
                    toggleFavorite(article.id);
                  }}
                  aria-label={`${favorites.has(article.id) ? 'Remove from' : 'Add to'} favorites`}
                >
                  {favorites.has(article.id) ? '❤️' : '🤍'}
                </button>
              </div>
            </div>

            <div slot="header" className="article-header">
              <h3 className="article-title">{article.title}</h3>
              <div className="article-meta">
                <span className="author">By {article.author}</span>
                <span className="date">{new Date(article.date).toLocaleDateString()}</span>
                <span className="read-time">{article.readTime}</span>
              </div>
            </div>

            <div slot="content" className="article-content">
              <p className="article-excerpt">{article.excerpt}</p>
              
              {selectedCard?.id === article.id && (
                <div className="expanded-content">
                  <div className="article-tags">
                    {article.tags.map(tag => (
                      <span key={tag} className="tag">#{tag}</span>
                    ))}
                  </div>
                  <div className="article-stats">
                    <span>👁️ 1.2k views</span>
                    <span>👍 24 likes</span>
                    <span>💬 8 comments</span>
                  </div>
                </div>
              )}
            </div>

            <div slot="actions" className="article-actions">
              <button 
                className="btn-primary"
                onClick={(e) => {
                  e.stopPropagation();
                  console.log('Reading article:', article.id);
                }}
              >
                Read Article
              </button>
              <button 
                className="btn-secondary"
                onClick={(e) => {
                  e.stopPropagation();
                  console.log('Sharing article:', article.id);
                }}
              >
                Share
              </button>
            </div>
          </SafCard>
        ))}
      </div>
    </div>
  );
}
```

### API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `appearance` | `'vertical' \| 'horizontal'` | `'vertical'` | Layout orientation of the card |
| `density` | `'compact' \| 'comfortable' \| 'spacious' \| 'inherit'` | `'inherit'` | Visual density of the component |
| `headingLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `2` | Heading level for accessibility |
| `imageBleed` | `boolean` | `true` | Whether images bleed to card edges |
| `onClick` | `(event: MouseEvent) => void` | `undefined` | Handler for card click events |

### Slots

| Slot | Description |
|------|-------------|
| `media` | Image or media content |
| `header` | Card title and metadata |
| `content` | Main card content |
| `actions` | Action buttons |
| `(default)` | Additional content |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-card',
  template: `
    <saf-card 
      appearance="vertical" 
      density="comfortable">
      <img slot="media" src="/api/placeholder/300/200" alt="Product preview" />
      <h3 slot="header">Product Title</h3>
      <p slot="content">
        This is a brief description of the product that provides key information 
        to help users understand what they're looking at.
      </p>
      <div slot="actions">
        <button class="btn-primary">Learn More</button>
        <button class="btn-secondary">Add to Cart</button>
      </div>
    </saf-card>
  `
})
export class BasicCardComponent {}
```

### Advanced Product Cards

```typescript
// component.ts
import { Component } from '@angular/core';

interface Product {
  id: number;
  title: string;
  price: number;
  originalPrice?: number;
  rating: number;
  image: string;
  badge?: string;
  description: string;
  inStock: boolean;
  category: string;
}

@Component({
  selector: 'app-product-cards',
  template: `
    <div class="product-gallery">
      <h2>Featured Products</h2>
      
      <div class="products-grid">
        <saf-card
          *ngFor="let product of products; trackBy: trackByProductId"
          appearance="vertical"
          density="comfortable"
          [image-bleed]="true"
          [heading-level]="3"
          [class.out-of-stock]="!product.inStock"
          class="product-card">
          
          <div slot="media" class="product-image-container">
            <img 
              [src]="product.image" 
              [alt]="product.title"
              class="product-image">
            <span 
              *ngIf="product.badge" 
              [class]="'product-badge badge-' + product.badge.toLowerCase()">
              {{ product.badge }}
            </span>
            <div *ngIf="!product.inStock" class="out-of-stock-overlay">
              Out of Stock
            </div>
          </div>

          <div slot="header" class="product-header">
            <h3 class="product-title">{{ product.title }}</h3>
            <div class="product-meta">
              <span class="product-category">{{ product.category }}</span>
              <div class="product-rating">
                <span class="rating-stars">{{ renderRating(product.rating) }}</span>
                <span class="rating-value">({{ product.rating }})</span>
              </div>
            </div>
          </div>

          <div slot="content" class="product-content">
            <p class="product-description">{{ product.description }}</p>
            <div class="product-pricing">
              <span class="current-price">{{ product.price | currency }}</span>
              <span 
                *ngIf="product.originalPrice" 
                class="original-price">
                {{ product.originalPrice | currency }}
              </span>
            </div>
          </div>

          <div slot="actions" class="product-actions">
            <button
              class="btn-primary"
              (click)="addToCart(product)"
              [disabled]="!product.inStock">
              {{ product.inStock ? 'Add to Cart' : 'Notify Me' }}
            </button>
            <button
              class="btn-secondary"
              (click)="viewDetails(product)">
              View Details
            </button>
          </div>
        </saf-card>
      </div>
    </div>
  `
})
export class ProductCardsComponent {
  products: Product[] = [
    {
      id: 1,
      title: 'Wireless Headphones',
      price: 199.99,
      originalPrice: 249.99,
      rating: 4.5,
      image: '/api/placeholder/300/200',
      badge: 'Sale',
      description: 'Premium wireless headphones with noise cancellation.',
      inStock: true,
      category: 'Electronics'
    },
    // ... more products
  ];

  trackByProductId(index: number, product: Product): number {
    return product.id;
  }

  renderRating(rating: number): string {
    return '⭐'.repeat(Math.floor(rating)) + (rating % 1 ? '⭐' : '');
  }

  addToCart(product: Product): void {
    console.log('Added to cart:', product);
  }

  viewDetails(product: Product): void {
    console.log('Viewing details:', product);
  }
}
```

### API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `appearance` | `string` | `'vertical'` | Layout orientation |
| `density` | `string` | `'inherit'` | Visual density |
| `headingLevel` | `number` | `2` | Heading level |
| `imageBleed` | `boolean` | `true` | Image bleeding |

| Output | Type | Description |
|--------|------|-------------|
| `click` | `Event` | Emitted when card is clicked |

## Best Practices

### Content Organization
- **Clear hierarchy**: Use appropriate heading levels and visual hierarchy
- **Concise content**: Keep card content scannable and focused
- **Meaningful actions**: Provide relevant, actionable buttons
- **Consistent layout**: Maintain consistent card structure across similar content types

### Visual Design
- **Appropriate density**: Choose density based on content amount and screen space
- **Image optimization**: Optimize images for performance and responsive display
- **Color and contrast**: Ensure sufficient contrast for accessibility
- **Consistent spacing**: Maintain consistent spacing patterns

### Accessibility
- **Semantic structure**: Use proper heading levels and semantic HTML
- **Alternative text**: Provide meaningful alt text for images
- **Keyboard navigation**: Ensure cards and actions are keyboard accessible
- **Screen reader support**: Test with assistive technologies

### Performance
- **Image loading**: Implement lazy loading for card images
- **Virtual scrolling**: Consider virtualization for large card collections
- **Minimal re-renders**: Optimize state updates to prevent unnecessary re-renders

## Accessibility Notes

The SafCard component provides comprehensive accessibility support:

- **Semantic structure**: Proper heading hierarchy with configurable levels
- **ARIA support**: Appropriate ARIA labels and roles
- **Keyboard navigation**: Full keyboard support for interactive elements
- **Screen reader compatibility**: Optimized for assistive technologies
- **Focus management**: Clear focus indicators and logical tab order

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+
- **Responsive design**: CSS Grid and Flexbox support
- **Image formats**: WebP, AVIF support where available

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: Slot names may have changed, check slot documentation
- **v1.x to v2.x**: CSS custom properties updated for theming
- **Density prop**: New density values may be available in newer versions

---

*This documentation provides comprehensive guidance for implementing SafCard in both React and Angular applications with proper content organization, accessibility, and performance considerations.*
