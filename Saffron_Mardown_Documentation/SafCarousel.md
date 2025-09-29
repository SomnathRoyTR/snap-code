# SafCarousel

## Overview

SafCarousel is a flexible content carousel component that enables users to navigate through multiple items or slides horizontally. It provides smooth transitions, touch/swipe support, keyboard navigation, and various display options including thumbnails, indicators, and automatic playback functionality.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `Array<ReactNode>` | `[]` | Carousel items/slides |
| `activeIndex` | `number` | `0` | Currently active slide index (controlled) |
| `defaultActiveIndex` | `number` | `0` | Initial active slide index (uncontrolled) |
| `autoPlay` | `boolean` | `false` | Enables automatic slide progression |
| `autoPlayInterval` | `number` | `5000` | Auto-play interval in milliseconds |
| `loop` | `boolean` | `true` | Enables continuous looping |
| `showControls` | `boolean` | `true` | Shows navigation arrow buttons |
| `showIndicators` | `boolean` | `true` | Shows dot indicators |
| `showThumbnails` | `boolean` | `false` | Shows thumbnail navigation |
| `thumbnails` | `Array<string \| ReactNode>` | - | Thumbnail images or elements |
| `itemsPerView` | `number \| 'auto'` | `1` | Number of items visible at once |
| `itemSpacing` | `number` | `16` | Space between items in pixels |
| `transitionDuration` | `number` | `300` | Transition animation duration |
| `pauseOnHover` | `boolean` | `true` | Pauses auto-play on hover |
| `swipeable` | `boolean` | `true` | Enables touch/swipe navigation |
| `keyboardNavigation` | `boolean` | `true` | Enables keyboard arrow navigation |
| `aspectRatio` | `string` | - | CSS aspect-ratio for items (e.g., "16/9") |
| `height` | `string \| number` | - | Fixed height for carousel |
| `className` | `string` | - | Additional CSS classes |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onSlideChange` | `(index: number) => void` | Fired when active slide changes |
| `onBeforeSlideChange` | `(currentIndex: number, nextIndex: number) => void` | Fired before slide change |
| `onAutoPlayStart` | `() => void` | Fired when auto-play starts |
| `onAutoPlayStop` | `() => void` | Fired when auto-play stops |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `Array<any>` | `[]` | Carousel items data |
| `activeIndex` | `number` | `0` | Currently active slide index |
| `autoPlay` | `boolean` | `false` | Enables automatic slide progression |
| `autoPlayInterval` | `number` | `5000` | Auto-play interval in milliseconds |
| `loop` | `boolean` | `true` | Enables continuous looping |
| `showControls` | `boolean` | `true` | Shows navigation arrow buttons |
| `showIndicators` | `boolean` | `true` | Shows dot indicators |
| `showThumbnails` | `boolean` | `false` | Shows thumbnail navigation |
| `thumbnails` | `Array<string>` | - | Thumbnail image URLs |
| `itemsPerView` | `number` | `1` | Number of items visible at once |
| `itemSpacing` | `number` | `16` | Space between items in pixels |
| `transitionDuration` | `number` | `300` | Transition animation duration |
| `pauseOnHover` | `boolean` | `true` | Pauses auto-play on hover |
| `swipeable` | `boolean` | `true` | Enables touch/swipe navigation |
| `keyboardNavigation` | `boolean` | `true` | Enables keyboard arrow navigation |
| `aspectRatio` | `string` | - | CSS aspect-ratio for items |
| `height` | `string \| number` | - | Fixed height for carousel |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `slideChange` | `EventEmitter<number>` | Fired when active slide changes |
| `beforeSlideChange` | `EventEmitter<{current: number, next: number}>` | Fired before slide change |
| `autoPlayStart` | `EventEmitter<void>` | Fired when auto-play starts |
| `autoPlayStop` | `EventEmitter<void>` | Fired when auto-play stops |

## Usage Examples

### Basic Image Carousel

```typescript
// React
const images = [
  '/images/slide1.jpg',
  '/images/slide2.jpg',
  '/images/slide3.jpg',
  '/images/slide4.jpg'
];

<SafCarousel 
  items={images.map(src => (
    <img key={src} src={src} alt="Carousel slide" style={{ width: '100%' }} />
  ))}
  autoPlay
  autoPlayInterval={4000}
  aspectRatio="16/9"
/>
```

```html
<!-- Angular -->
<saf-carousel 
  [items]="carouselImages"
  [autoPlay]="true"
  [autoPlayInterval]="4000"
  aspectRatio="16/9"
>
  <ng-template let-item>
    <img [src]="item" alt="Carousel slide" style="width: 100%;" />
  </ng-template>
</saf-carousel>
```

### Product Carousel with Thumbnails

```typescript
// React
const products = [
  { id: 1, title: 'Product A', image: '/images/product-a.jpg', thumbnail: '/images/thumb-a.jpg' },
  { id: 2, title: 'Product B', image: '/images/product-b.jpg', thumbnail: '/images/thumb-b.jpg' },
  { id: 3, title: 'Product C', image: '/images/product-c.jpg', thumbnail: '/images/thumb-c.jpg' }
];

<SafCarousel 
  items={products.map(product => (
    <div key={product.id} className="product-slide">
      <img src={product.image} alt={product.title} />
      <h3>{product.title}</h3>
    </div>
  ))}
  thumbnails={products.map(product => (
    <img src={product.thumbnail} alt={`${product.title} thumbnail`} />
  ))}
  showThumbnails
  aspectRatio="4/3"
/>
```

```html
<!-- Angular -->
<saf-carousel 
  [items]="products"
  [thumbnails]="productThumbnails"
  [showThumbnails]="true"
  aspectRatio="4/3"
>
  <ng-template let-product>
    <div class="product-slide">
      <img [src]="product.image" [alt]="product.title" />
      <h3>{{product.title}}</h3>
    </div>
  </ng-template>
</saf-carousel>
```

### Multi-Item Carousel

```typescript
// React
const testimonials = [
  { name: 'John Doe', comment: 'Great service!', rating: 5 },
  { name: 'Jane Smith', comment: 'Highly recommended.', rating: 5 },
  { name: 'Bob Johnson', comment: 'Excellent quality.', rating: 4 },
  { name: 'Alice Brown', comment: 'Fast delivery.', rating: 5 }
];

<SafCarousel 
  items={testimonials.map(testimonial => (
    <SafCard key={testimonial.name} className="testimonial-card">
      <SafCardContent>
        <SafRating value={testimonial.rating} readOnly size="small" />
        <p>"{testimonial.comment}"</p>
        <footer>— {testimonial.name}</footer>
      </SafCardContent>
    </SafCard>
  ))}
  itemsPerView={2}
  itemSpacing={24}
  autoPlay
  pauseOnHover
/>
```

### Controlled Carousel

```typescript
// React
const [activeSlide, setActiveSlide] = useState(0);
const [isAutoPlaying, setIsAutoPlaying] = useState(true);

<div>
  <SafCarousel 
    items={slides}
    activeIndex={activeSlide}
    onSlideChange={setActiveSlide}
    autoPlay={isAutoPlaying}
    onAutoPlayStart={() => setIsAutoPlaying(true)}
    onAutoPlayStop={() => setIsAutoPlaying(false)}
  />
  
  <div className="carousel-controls">
    <SafButton 
      variant="outline" 
      onClick={() => setIsAutoPlaying(!isAutoPlaying)}
    >
      {isAutoPlaying ? 'Pause' : 'Play'}
    </SafButton>
    <span>Slide {activeSlide + 1} of {slides.length}</span>
  </div>
</div>
```

```html
<!-- Angular -->
<div>
  <saf-carousel 
    [items]="slides"
    [activeIndex]="activeSlide"
    [autoPlay]="isAutoPlaying"
    (slideChange)="setActiveSlide($event)"
    (autoPlayStart)="setIsAutoPlaying(true)"
    (autoPlayStop)="setIsAutoPlaying(false)"
  >
  </saf-carousel>
  
  <div class="carousel-controls">
    <saf-button 
      variant="outline" 
      (click)="toggleAutoPlay()"
    >
      {{isAutoPlaying ? 'Pause' : 'Play'}}
    </saf-button>
    <span>Slide {{activeSlide + 1}} of {{slides.length}}</span>
  </div>
</div>
```

### Content Card Carousel

```typescript
// React
const features = [
  {
    icon: 'shield',
    title: 'Secure',
    description: 'Bank-level security for all your data'
  },
  {
    icon: 'zap',
    title: 'Fast',
    description: 'Lightning-fast performance and response times'
  },
  {
    icon: 'users',
    title: 'Collaborative',
    description: 'Built for teams and seamless collaboration'
  },
  {
    icon: 'smartphone',
    title: 'Mobile-First',
    description: 'Optimized for mobile and tablet devices'
  }
];

<SafCarousel 
  items={features.map(feature => (
    <SafCard key={feature.title} className="feature-card">
      <SafCardContent style={{ textAlign: 'center' }}>
        <SafIcon name={feature.icon} size="large" />
        <h3>{feature.title}</h3>
        <p>{feature.description}</p>
      </SafCardContent>
    </SafCard>
  ))}
  itemsPerView="auto"
  itemSpacing={20}
  showControls={false}
  showIndicators
  swipeable
/>
```

### Video Carousel

```typescript
// React
const videos = [
  { id: 1, src: '/videos/intro.mp4', poster: '/images/intro-poster.jpg', title: 'Introduction' },
  { id: 2, src: '/videos/demo.mp4', poster: '/images/demo-poster.jpg', title: 'Demo' },
  { id: 3, src: '/videos/tutorial.mp4', poster: '/images/tutorial-poster.jpg', title: 'Tutorial' }
];

<SafCarousel 
  items={videos.map(video => (
    <div key={video.id} className="video-slide">
      <video 
        src={video.src} 
        poster={video.poster}
        controls
        style={{ width: '100%' }}
      />
      <h3>{video.title}</h3>
    </div>
  ))}
  autoPlay={false}
  aspectRatio="16/9"
  onSlideChange={(index) => {
    // Pause all videos when switching slides
    document.querySelectorAll('video').forEach(video => video.pause());
  }}
/>
```

### News Article Carousel

```typescript
// React
const articles = [
  {
    id: 1,
    headline: 'Breaking: New Technology Advances',
    summary: 'Scientists make breakthrough in quantum computing.',
    image: '/images/tech-news.jpg',
    category: 'Technology',
    publishDate: '2024-09-26'
  },
  {
    id: 2,
    headline: 'Market Update: Stocks Rise',
    summary: 'Global markets show positive trends this quarter.',
    image: '/images/market-news.jpg',
    category: 'Finance',
    publishDate: '2024-09-25'
  }
];

<SafCarousel 
  items={articles.map(article => (
    <SafCard key={article.id} className="news-card">
      <img src={article.image} alt={article.headline} />
      <SafCardContent>
        <SafBadge variant="primary">{article.category}</SafBadge>
        <h3>{article.headline}</h3>
        <p>{article.summary}</p>
        <time>{new Date(article.publishDate).toLocaleDateString()}</time>
      </SafCardContent>
    </SafCard>
  ))}
  autoPlay
  autoPlayInterval={8000}
  height={400}
/>
```

### Image Gallery with Lightbox

```typescript
// React
const [selectedImage, setSelectedImage] = useState(null);

<div>
  <SafCarousel 
    items={galleryImages.map((image, index) => (
      <div 
        key={image.id} 
        className="gallery-thumbnail"
        onClick={() => setSelectedImage(index)}
      >
        <img src={image.thumbnail} alt={image.caption} />
        <div className="overlay">
          <SafIcon name="expand" />
        </div>
      </div>
    ))}
    itemsPerView={4}
    itemSpacing={12}
    showControls
    showIndicators={false}
  />
  
  {selectedImage !== null && (
    <SafModal 
      open 
      onClose={() => setSelectedImage(null)}
      size="large"
    >
      <SafCarousel 
        items={galleryImages.map(image => (
          <img key={image.id} src={image.fullSize} alt={image.caption} />
        ))}
        activeIndex={selectedImage}
        onSlideChange={setSelectedImage}
        aspectRatio="16/9"
      />
    </SafModal>
  )}
</div>
```

### Responsive Carousel

```typescript
// React
const useResponsiveCarousel = () => {
  const [itemsPerView, setItemsPerView] = useState(1);
  
  useEffect(() => {
    const updateItemsPerView = () => {
      if (window.innerWidth >= 1200) {
        setItemsPerView(4);
      } else if (window.innerWidth >= 768) {
        setItemsPerView(2);
      } else {
        setItemsPerView(1);
      }
    };
    
    updateItemsPerView();
    window.addEventListener('resize', updateItemsPerView);
    return () => window.removeEventListener('resize', updateItemsPerView);
  }, []);
  
  return itemsPerView;
};

const ResponsiveCarousel = ({ items }) => {
  const itemsPerView = useResponsiveCarousel();
  
  return (
    <SafCarousel 
      items={items}
      itemsPerView={itemsPerView}
      itemSpacing={16}
      autoPlay
      swipeable
    />
  );
};
```

### Carousel with Custom Controls

```typescript
// React
const CustomCarousel = ({ items }) => {
  const [currentIndex, setCurrentIndex] = useState(0);
  const [isPlaying, setIsPlaying] = useState(true);
  
  return (
    <div className="custom-carousel-container">
      <SafCarousel 
        items={items}
        activeIndex={currentIndex}
        onSlideChange={setCurrentIndex}
        showControls={false}
        showIndicators={false}
        autoPlay={isPlaying}
      />
      
      <div className="custom-controls">
        <SafButton 
          variant="ghost" 
          icon="chevron-left"
          onClick={() => setCurrentIndex(Math.max(0, currentIndex - 1))}
          disabled={currentIndex === 0}
        />
        
        <div className="slide-info">
          <span>{currentIndex + 1} / {items.length}</span>
          <SafButton 
            variant="text" 
            icon={isPlaying ? 'pause' : 'play'}
            onClick={() => setIsPlaying(!isPlaying)}
          />
        </div>
        
        <SafButton 
          variant="ghost" 
          icon="chevron-right"
          onClick={() => setCurrentIndex(Math.min(items.length - 1, currentIndex + 1))}
          disabled={currentIndex === items.length - 1}
        />
      </div>
      
      <div className="custom-indicators">
        {items.map((_, index) => (
          <button
            key={index}
            className={`indicator ${index === currentIndex ? 'active' : ''}`}
            onClick={() => setCurrentIndex(index)}
          />
        ))}
      </div>
    </div>
  );
};
```

## Best Practices

### Performance
- **Lazy Loading**: Implement lazy loading for images and heavy content
- **Virtual Scrolling**: Use virtual scrolling for large datasets
- **Optimize Images**: Use appropriate image formats and sizes
- **Preload Strategy**: Preload adjacent slides for smooth transitions

### User Experience
- **Touch Support**: Ensure swipe gestures work smoothly on mobile
- **Keyboard Navigation**: Support arrow keys and other standard navigation
- **Auto-Play Control**: Allow users to pause auto-play easily
- **Progress Indication**: Show current position clearly

### Content Strategy
- **Consistent Sizing**: Maintain consistent dimensions across slides
- **Meaningful Thumbnails**: Use representative thumbnail images
- **Content Priority**: Place most important content first
- **Loading States**: Show loading indicators for async content

### Accessibility
- **Screen Reader Support**: Provide proper ARIA labels and descriptions
- **Keyboard Navigation**: Ensure all functions work with keyboard only
- **Motion Preferences**: Respect reduced motion preferences
- **Focus Management**: Handle focus appropriately during navigation

## Accessibility Considerations

- Uses appropriate ARIA attributes including `role="region"` and `aria-live`
- Provides keyboard navigation with arrow keys, Home, and End
- Announces slide changes to screen readers
- Supports reduced motion preferences for animations
- Maintains proper focus management during slide transitions
- Includes accessible labels for all interactive elements

## Related Components

- **SafFlipper**: Simple two-item switcher component
- **SafTabs**: Tab-based content switching
- **SafAccordion**: Vertical content expansion
- **SafModal**: Overlay content display
- **SafCard**: Content card container
- **SafImage**: Image display component

## Notes

- SafCarousel automatically handles touch events for swipe navigation
- Auto-play pauses when the carousel is not visible (intersection observer)
- Thumbnail navigation provides an alternative way to access slides
- The component supports both controlled and uncontrolled usage patterns
- Transitions use CSS transforms for optimal performance
- Loop mode creates seamless infinite scrolling experience
- Custom aspect ratios ensure consistent slide dimensions
- The component is fully responsive and works across all device sizes
