# SafVirtualScroller

## Overview

SafVirtualScroller is a performance optimization component that renders only visible items from large datasets by implementing virtual scrolling. It provides smooth scrolling experiences for thousands of items while maintaining minimal DOM nodes and memory usage, with support for dynamic heights, horizontal scrolling, and accessibility features.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `T[]` | `[]` | Array of data items to virtualize |
| `itemHeight` | `number \| (index: number, item: T) => number` | `50` | Height of each item (fixed or dynamic) |
| `height` | `number \| string` | `400` | Container height |
| `width` | `number \| string` | `'100%'` | Container width |
| `overscan` | `number` | `5` | Number of items to render outside visible area |
| `direction` | `'vertical' \| 'horizontal'` | `'vertical'` | Scroll direction |
| `scrollToIndex` | `number` | - | Index to scroll to |
| `scrollToAlignment` | `'auto' \| 'start' \| 'center' \| 'end'` | `'auto'` | Scroll alignment |
| `estimatedItemSize` | `number` | - | Estimated size for dynamic heights |
| `renderItem` | `(props: ItemProps<T>) => ReactNode` | - | Item render function |
| `renderEmpty` | `() => ReactNode` | - | Empty state render function |
| `onScroll` | `(scrollTop: number, scrollLeft: number) => void` | - | Scroll event handler |
| `onItemsRendered` | `(range: VisibleRange) => void` | - | Rendered items change handler |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### ItemProps Interface

```typescript
interface ItemProps<T> {
  index: number;
  item: T;
  style: React.CSSProperties;
  isVisible: boolean;
}

interface VisibleRange {
  startIndex: number;
  endIndex: number;
  visibleStartIndex: number;
  visibleEndIndex: number;
}
```

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `T[]` | `[]` | Array of data items to virtualize |
| `itemHeight` | `number \| (index: number, item: T) => number` | `50` | Height of each item (fixed or dynamic) |
| `height` | `number \| string` | `400` | Container height |
| `width` | `number \| string` | `'100%'` | Container width |
| `overscan` | `number` | `5` | Number of items to render outside visible area |
| `direction` | `'vertical' \| 'horizontal'` | `'vertical'` | Scroll direction |
| `scrollToIndex` | `number` | - | Index to scroll to |
| `scrollToAlignment` | `'auto' \| 'start' \| 'center' \| 'end'` | `'auto'` | Scroll alignment |
| `estimatedItemSize` | `number` | - | Estimated size for dynamic heights |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `scroll` | `EventEmitter<{scrollTop: number, scrollLeft: number}>` | Fired on scroll |
| `itemsRendered` | `EventEmitter<VisibleRange>` | Fired when rendered items change |

## Usage Examples

### Basic Virtual List

```typescript
// React
const BasicVirtualList = ({ data }) => {
  const renderItem = ({ index, item, style }) => (
    <div style={style} className="virtual-list-item">
      <div className="item-content">
        <h4>{item.title}</h4>
        <p>{item.description}</p>
        <span className="item-index">#{index}</span>
      </div>
    </div>
  );

  return (
    <div className="basic-virtual-list">
      <h3>Virtual List ({data.length} items)</h3>
      
      <SafVirtualScroller
        items={data}
        height={400}
        itemHeight={80}
        renderItem={renderItem}
        className="virtual-scroller"
      />
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-virtual-list">
  <h3>Virtual List ({{data.length}} items)</h3>
  
  <saf-virtual-scroller
    [items]="data"
    [height]="400"
    [itemHeight]="80"
    class="virtual-scroller">
    
    <ng-template let-item let-index="index" let-style="style">
      <div [ngStyle]="style" class="virtual-list-item">
        <div class="item-content">
          <h4>{{item.title}}</h4>
          <p>{{item.description}}</p>
          <span class="item-index">#{{index}}</span>
        </div>
      </div>
    </ng-template>
  </saf-virtual-scroller>
</div>
```

### Dynamic Height Virtual List

```typescript
// React
const DynamicHeightVirtualList = ({ messages }) => {
  const [heights, setHeights] = useState(new Map());
  const measureRef = useRef(null);

  const getItemHeight = (index, item) => {
    return heights.get(index) || estimateHeight(item);
  };

  const estimateHeight = (item) => {
    // Basic estimation based on content length
    const baseHeight = 60; // Header + padding
    const textHeight = Math.ceil(item.content.length / 50) * 20; // ~50 chars per line
    const attachmentsHeight = item.attachments ? item.attachments.length * 30 : 0;
    
    return baseHeight + textHeight + attachmentsHeight;
  };

  const measureItem = (index, element) => {
    if (element) {
      const height = element.getBoundingClientRect().height;
      setHeights(prev => new Map(prev).set(index, height));
    }
  };

  const renderMessage = ({ index, item, style, isVisible }) => (
    <div
      style={style}
      className="message-item"
      ref={isVisible ? (el) => measureItem(index, el) : null}
    >
      <div className="message-header">
        <SafAvatar 
          src={item.author.avatar}
          name={item.author.name}
          size="small"
        />
        <div className="message-info">
          <span className="author-name">{item.author.name}</span>
          <span className="message-time">
            {new Date(item.timestamp).toLocaleTimeString()}
          </span>
        </div>
        {item.edited && (
          <SafBadge 
            label="edited"
            size="small"
            variant="outline"
          />
        )}
      </div>
      
      <div className="message-content">
        {item.content}
      </div>
      
      {item.attachments && (
        <div className="message-attachments">
          {item.attachments.map(attachment => (
            <div key={attachment.id} className="attachment">
              <SafIcon name="paperclip" size="small" />
              <span>{attachment.name}</span>
            </div>
          ))}
        </div>
      )}
      
      <div className="message-actions">
        <SafButton variant="ghost" size="small" icon={<SafIcon name="heart" />} />
        <SafButton variant="ghost" size="small" icon={<SafIcon name="message-square" />} />
        <SafButton variant="ghost" size="small" icon={<SafIcon name="share" />} />
      </div>
    </div>
  );

  return (
    <div className="dynamic-height-virtual-list">
      <div className="chat-header">
        <h3>Chat Messages</h3>
        <SafBadge 
          label={`${messages.length} messages`}
          color="primary"
        />
      </div>
      
      <SafVirtualScroller
        items={messages}
        height={500}
        itemHeight={getItemHeight}
        estimatedItemSize={120}
        overscan={3}
        renderItem={renderMessage}
        className="chat-virtual-scroller"
      />
    </div>
  );
};
```

### Horizontal Virtual Scroller

```typescript
// React
const HorizontalVirtualScroller = ({ products }) => {
  const [selectedProduct, setSelectedProduct] = useState(null);

  const renderProduct = ({ index, item, style }) => (
    <div
      style={style}
      className={`product-card ${selectedProduct === item.id ? 'selected' : ''}`}
      onClick={() => setSelectedProduct(item.id)}
    >
      <div className="product-image">
        <SafImage 
          src={item.image}
          alt={item.name}
          width="100%"
          height={180}
          placeholder="product"
        />
        {item.onSale && (
          <SafBadge 
            label={`${item.discount}% OFF`}
            color="error"
            className="sale-badge"
          />
        )}
      </div>
      
      <div className="product-info">
        <h4 className="product-name">{item.name}</h4>
        <p className="product-description">{item.description}</p>
        
        <div className="product-rating">
          {[...Array(5)].map((_, i) => (
            <SafIcon
              key={i}
              name="star"
              size="small"
              className={i < item.rating ? 'filled' : 'empty'}
            />
          ))}
          <span className="rating-count">({item.reviewCount})</span>
        </div>
        
        <div className="product-price">
          {item.onSale && (
            <span className="original-price">${item.originalPrice}</span>
          )}
          <span className="current-price">${item.price}</span>
        </div>
        
        <SafButton
          variant="primary"
          size="small"
          onClick={(e) => {
            e.stopPropagation();
            console.log('Add to cart:', item.id);
          }}
        >
          Add to Cart
        </SafButton>
      </div>
    </div>
  );

  return (
    <div className="horizontal-virtual-scroller">
      <div className="products-header">
        <h3>Featured Products</h3>
        <div className="products-controls">
          <SafButton
            variant="outline"
            size="small"
            icon={<SafIcon name="filter" />}
          >
            Filter
          </SafButton>
          <SafButton
            variant="outline"
            size="small"
            icon={<SafIcon name="sort-desc" />}
          >
            Sort
          </SafButton>
        </div>
      </div>
      
      <SafVirtualScroller
        items={products}
        height={400}
        width="100%"
        direction="horizontal"
        itemHeight={280} // itemWidth in horizontal mode
        overscan={2}
        renderItem={renderProduct}
        className="products-virtual-scroller"
      />
    </div>
  );
};
```

### Virtual Table with Fixed Headers

```typescript
// React
const VirtualTable = ({ 
  data, 
  columns,
  sortColumn,
  sortDirection,
  onSort 
}) => {
  const [scrollLeft, setScrollLeft] = useState(0);

  const renderRow = ({ index, item, style }) => (
    <div style={style} className="virtual-table-row">
      {columns.map(column => (
        <div
          key={column.key}
          className="virtual-table-cell"
          style={{ width: column.width }}
        >
          {column.render ? column.render(item[column.key], item, index) : item[column.key]}
        </div>
      ))}
    </div>
  );

  const handleScroll = (scrollTop, scrollLeft) => {
    setScrollLeft(scrollLeft);
  };

  const handleSort = (column) => {
    const newDirection = 
      sortColumn === column.key && sortDirection === 'asc' ? 'desc' : 'asc';
    onSort(column.key, newDirection);
  };

  return (
    <div className="virtual-table">
      <div 
        className="virtual-table-header"
        style={{ transform: `translateX(-${scrollLeft}px)` }}
      >
        {columns.map(column => (
          <div
            key={column.key}
            className={`virtual-table-header-cell ${column.sortable ? 'sortable' : ''}`}
            style={{ width: column.width }}
            onClick={() => column.sortable && handleSort(column)}
          >
            <span>{column.title}</span>
            {column.sortable && sortColumn === column.key && (
              <SafIcon 
                name={sortDirection === 'asc' ? 'chevron-up' : 'chevron-down'}
                size="small"
              />
            )}
          </div>
        ))}
      </div>
      
      <SafVirtualScroller
        items={data}
        height={400}
        itemHeight={50}
        renderItem={renderRow}
        onScroll={handleScroll}
        className="virtual-table-scroller"
      />
      
      <div className="virtual-table-footer">
        <span>Total: {data.length} rows</span>
      </div>
    </div>
  );
};
```

### Infinite Loading Virtual Scroller

```typescript
// React
const InfiniteLoadingVirtualScroller = ({ 
  initialData,
  loadMoreItems,
  hasNextPage 
}) => {
  const [items, setItems] = useState(initialData);
  const [loading, setLoading] = useState(false);
  const [loadedPages, setLoadedPages] = useState(1);

  const loadMore = useCallback(async () => {
    if (loading || !hasNextPage) return;

    setLoading(true);
    try {
      const newItems = await loadMoreItems(loadedPages);
      setItems(prev => [...prev, ...newItems]);
      setLoadedPages(prev => prev + 1);
    } catch (error) {
      console.error('Failed to load more items:', error);
    } finally {
      setLoading(false);
    }
  }, [loading, hasNextPage, loadedPages, loadMoreItems]);

  const handleItemsRendered = ({ visibleEndIndex, endIndex }) => {
    // Load more when approaching the end
    if (!loading && hasNextPage && visibleEndIndex >= endIndex - 5) {
      loadMore();
    }
  };

  const renderItem = ({ index, item, style }) => {
    if (!item) {
      return (
        <div style={style} className="virtual-list-item loading">
          <SafLoadingSpinner size="small" />
          <span>Loading...</span>
        </div>
      );
    }

    return (
      <div style={style} className="virtual-list-item">
        <div className="item-avatar">
          <SafAvatar 
            src={item.avatar}
            name={item.name}
            size="medium"
          />
        </div>
        <div className="item-content">
          <h4>{item.name}</h4>
          <p>{item.email}</p>
          <div className="item-tags">
            {item.tags.map(tag => (
              <SafBadge 
                key={tag}
                label={tag}
                size="small"
                variant="outline"
              />
            ))}
          </div>
        </div>
        <div className="item-actions">
          <SafButton
            variant="ghost"
            size="small"
            icon={<SafIcon name="mail" />}
            onClick={() => console.log('Email:', item.email)}
          />
          <SafButton
            variant="ghost"
            size="small"
            icon={<SafIcon name="more-horizontal" />}
          />
        </div>
      </div>
    );
  };

  // Add placeholder items for loading
  const displayItems = [...items];
  if (loading && hasNextPage) {
    displayItems.push(...Array(5).fill(null));
  }

  return (
    <div className="infinite-loading-virtual-scroller">
      <div className="scroller-header">
        <h3>Team Members</h3>
        <div className="loading-status">
          {loading && (
            <>
              <SafLoadingSpinner size="small" />
              <span>Loading more...</span>
            </>
          )}
          {!hasNextPage && items.length > 0 && (
            <span className="end-message">All items loaded</span>
          )}
        </div>
      </div>
      
      <SafVirtualScroller
        items={displayItems}
        height={600}
        itemHeight={80}
        overscan={10}
        renderItem={renderItem}
        onItemsRendered={handleItemsRendered}
        className="infinite-virtual-scroller"
      />
    </div>
  );
};
```

### Search-Enabled Virtual List

```typescript
// React
const SearchEnabledVirtualList = ({ 
  allItems,
  onItemSelect 
}) => {
  const [searchQuery, setSearchQuery] = useState('');
  const [filteredItems, setFilteredItems] = useState(allItems);
  const [selectedIndex, setSelectedIndex] = useState(-1);

  // Filter items based on search query
  useEffect(() => {
    if (!searchQuery) {
      setFilteredItems(allItems);
      return;
    }

    const filtered = allItems.filter(item =>
      item.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
      item.description.toLowerCase().includes(searchQuery.toLowerCase()) ||
      item.tags.some(tag => tag.toLowerCase().includes(searchQuery.toLowerCase()))
    );

    setFilteredItems(filtered);
    setSelectedIndex(-1);
  }, [searchQuery, allItems]);

  const highlightMatch = (text, query) => {
    if (!query) return text;

    const regex = new RegExp(`(${query})`, 'gi');
    const parts = text.split(regex);

    return parts.map((part, index) =>
      regex.test(part) ? (
        <mark key={index} className="search-highlight">{part}</mark>
      ) : part
    );
  };

  const renderSearchItem = ({ index, item, style, isVisible }) => (
    <div
      style={style}
      className={`search-virtual-item ${selectedIndex === index ? 'selected' : ''}`}
      onClick={() => {
        setSelectedIndex(index);
        onItemSelect(item);
      }}
    >
      <div className="item-icon">
        <SafIcon name={item.type === 'file' ? 'file' : 'folder'} />
      </div>
      
      <div className="item-content">
        <h4 className="item-name">
          {highlightMatch(item.name, searchQuery)}
        </h4>
        <p className="item-description">
          {highlightMatch(item.description, searchQuery)}
        </p>
        
        {item.tags.length > 0 && (
          <div className="item-tags">
            {item.tags.map(tag => (
              <SafBadge
                key={tag}
                label={highlightMatch(tag, searchQuery)}
                size="small"
                variant="outline"
              />
            ))}
          </div>
        )}
      </div>
      
      <div className="item-meta">
        <span className="item-date">
          {new Date(item.lastModified).toLocaleDateString()}
        </span>
        <span className="item-size">{item.size}</span>
      </div>
    </div>
  );

  const renderEmpty = () => (
    <div className="search-empty-state">
      <SafEmptyState
        title={searchQuery ? "No results found" : "Start typing to search"}
        description={
          searchQuery 
            ? `No items match "${searchQuery}"`
            : "Search through thousands of items instantly"
        }
        icon={<SafIcon name="search" />}
      />
    </div>
  );

  return (
    <div className="search-enabled-virtual-list">
      <div className="search-header">
        <SafSearchField
          placeholder="Search items..."
          value={searchQuery}
          onSearch={setSearchQuery}
          clearable
        />
        
        <div className="search-results-count">
          {searchQuery && (
            <span>
              {filteredItems.length} of {allItems.length} items
            </span>
          )}
        </div>
      </div>
      
      <SafVirtualScroller
        items={filteredItems}
        height={500}
        itemHeight={100}
        renderItem={renderSearchItem}
        renderEmpty={renderEmpty}
        className="search-virtual-scroller"
      />
    </div>
  );
};
```

### Performance Monitoring Virtual Scroller

```typescript
// React
const PerformanceMonitoringVirtualScroller = ({ data }) => {
  const [performanceStats, setPerformanceStats] = useState({
    renderedItems: 0,
    renderTime: 0,
    scrollFPS: 0
  });
  
  const lastFrameTime = useRef(performance.now());
  const frameCount = useRef(0);
  const fpsInterval = useRef(null);

  useEffect(() => {
    // Monitor FPS during scrolling
    fpsInterval.current = setInterval(() => {
      const fps = frameCount.current;
      frameCount.current = 0;
      setPerformanceStats(prev => ({ ...prev, scrollFPS: fps }));
    }, 1000);

    return () => {
      if (fpsInterval.current) {
        clearInterval(fpsInterval.current);
      }
    };
  }, []);

  const handleItemsRendered = (range) => {
    const renderedCount = range.endIndex - range.startIndex + 1;
    setPerformanceStats(prev => ({
      ...prev,
      renderedItems: renderedCount
    }));
  };

  const handleScroll = () => {
    frameCount.current++;
  };

  const renderItem = ({ index, item, style }) => {
    const renderStart = performance.now();
    
    const element = (
      <div style={style} className="performance-virtual-item">
        <div className="item-header">
          <SafAvatar 
            src={item.avatar}
            name={item.name}
            size="small"
          />
          <div className="item-info">
            <h4>{item.name}</h4>
            <span className="item-id">ID: {item.id}</span>
          </div>
          <SafBadge 
            label={`#${index}`}
            size="small"
            color="secondary"
          />
        </div>
        
        <div className="item-content">
          <p>{item.description}</p>
          <div className="item-stats">
            <span>Views: {item.views.toLocaleString()}</span>
            <span>Likes: {item.likes.toLocaleString()}</span>
            <span>Comments: {item.comments.toLocaleString()}</span>
          </div>
        </div>
        
        <div className="item-chart">
          {/* Simulated mini chart */}
          <div className="mini-chart">
            {item.chartData.map((value, i) => (
              <div
                key={i}
                className="chart-bar"
                style={{ height: `${(value / 100) * 20}px` }}
              />
            ))}
          </div>
        </div>
      </div>
    );
    
    const renderTime = performance.now() - renderStart;
    setPerformanceStats(prev => ({
      ...prev,
      renderTime: renderTime
    }));
    
    return element;
  };

  return (
    <div className="performance-monitoring-virtual-scroller">
      <div className="performance-header">
        <h3>Performance Virtual Scroller</h3>
        <div className="performance-stats">
          <SafBadge 
            label={`${performanceStats.renderedItems} items rendered`}
            color="primary"
          />
          <SafBadge 
            label={`${performanceStats.renderTime.toFixed(2)}ms render time`}
            color="secondary"
          />
          <SafBadge 
            label={`${performanceStats.scrollFPS} FPS`}
            color={performanceStats.scrollFPS >= 50 ? "success" : performanceStats.scrollFPS >= 30 ? "warning" : "error"}
          />
        </div>
      </div>
      
      <SafVirtualScroller
        items={data}
        height={600}
        itemHeight={120}
        overscan={5}
        renderItem={renderItem}
        onItemsRendered={handleItemsRendered}
        onScroll={handleScroll}
        className="performance-virtual-scroller"
      />
      
      <div className="performance-footer">
        <p>Total items: {data.length.toLocaleString()}</p>
        <p>Memory usage: Only visible items + overscan are in DOM</p>
      </div>
    </div>
  );
};
```

### Accessible Virtual Scroller

```typescript
// React
const AccessibleVirtualScroller = ({ 
  items,
  onSelectionChange,
  ariaLabel = "Virtual list" 
}) => {
  const [selectedIndex, setSelectedIndex] = useState(-1);
  const [focusedIndex, setFocusedIndex] = useState(-1);
  const [announcements, setAnnouncements] = useState('');
  const scrollerRef = useRef(null);

  const handleKeyDown = (event) => {
    switch (event.key) {
      case 'ArrowDown':
        event.preventDefault();
        moveFocus(1);
        break;
        
      case 'ArrowUp':
        event.preventDefault();
        moveFocus(-1);
        break;
        
      case 'PageDown':
        event.preventDefault();
        moveFocus(10);
        break;
        
      case 'PageUp':
        event.preventDefault();
        moveFocus(-10);
        break;
        
      case 'Home':
        event.preventDefault();
        setFocusedIndex(0);
        scrollToIndex(0);
        break;
        
      case 'End':
        event.preventDefault();
        const lastIndex = items.length - 1;
        setFocusedIndex(lastIndex);
        scrollToIndex(lastIndex);
        break;
        
      case 'Enter':
      case ' ':
        event.preventDefault();
        if (focusedIndex >= 0) {
          selectItem(focusedIndex);
        }
        break;
    }
  };

  const moveFocus = (delta) => {
    const newIndex = Math.max(0, Math.min(items.length - 1, focusedIndex + delta));
    setFocusedIndex(newIndex);
    scrollToIndex(newIndex);
    
    const item = items[newIndex];
    setAnnouncements(`${item.name}, ${newIndex + 1} of ${items.length}`);
  };

  const selectItem = (index) => {
    setSelectedIndex(index);
    const item = items[index];
    setAnnouncements(`Selected ${item.name}`);
    onSelectionChange(item, index);
  };

  const scrollToIndex = (index) => {
    if (scrollerRef.current) {
      scrollerRef.current.scrollToIndex(index, 'center');
    }
  };

  const renderAccessibleItem = ({ index, item, style }) => (
    <div
      style={style}
      className={`accessible-virtual-item ${selectedIndex === index ? 'selected' : ''} ${focusedIndex === index ? 'focused' : ''}`}
      role="option"
      aria-selected={selectedIndex === index}
      aria-posinset={index + 1}
      aria-setsize={items.length}
      id={`virtual-item-${index}`}
      onClick={() => selectItem(index)}
      onMouseEnter={() => setFocusedIndex(index)}
    >
      <div className="item-content">
        <div className="item-icon">
          <SafIcon name={item.type} />
        </div>
        <div className="item-text">
          <h4>{item.name}</h4>
          <p>{item.description}</p>
        </div>
        <div className="item-status">
          {item.status && (
            <SafBadge 
              label={item.status}
              color={item.status === 'active' ? 'success' : 'secondary'}
            />
          )}
        </div>
      </div>
    </div>
  );

  return (
    <div 
      className="accessible-virtual-scroller"
      role="listbox"
      aria-label={ariaLabel}
      aria-activedescendant={focusedIndex >= 0 ? `virtual-item-${focusedIndex}` : undefined}
      tabIndex={0}
      onKeyDown={handleKeyDown}
    >
      <div className="scroller-instructions">
        <span className="sr-only">
          Use arrow keys to navigate, Enter or Space to select, Home/End to jump to beginning/end
        </span>
      </div>
      
      <SafVirtualScroller
        ref={scrollerRef}
        items={items}
        height={400}
        itemHeight={60}
        renderItem={renderAccessibleItem}
        scrollToIndex={focusedIndex >= 0 ? focusedIndex : undefined}
        className="accessible-scroller-inner"
      />
      
      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>
      
      <div className="scroller-summary" aria-live="polite">
        {items.length} total items
        {selectedIndex >= 0 && `, ${items[selectedIndex].name} selected`}
      </div>
    </div>
  );
};
```

## Best Practices

### Performance Optimization
- **Fixed Heights**: Use fixed item heights when possible for best performance
- **Overscan Management**: Balance overscan count between smooth scrolling and memory usage
- **Efficient Rendering**: Minimize complex calculations in render functions
- **Memoization**: Use React.memo or similar for expensive item components

### Data Management
- **Stable Keys**: Use stable, unique keys for items to prevent unnecessary re-renders
- **Immutable Updates**: Use immutable patterns for data updates
- **Batch Updates**: Batch data changes to minimize re-renders
- **Memory Cleanup**: Clean up resources when component unmounts

### User Experience
- **Smooth Scrolling**: Maintain consistent scroll performance
- **Loading States**: Show loading indicators for dynamic content
- **Empty States**: Provide meaningful empty state messages
- **Accessibility**: Support keyboard navigation and screen readers

### Dynamic Content
- **Height Estimation**: Provide good estimates for dynamic heights
- **Measurement**: Measure actual heights when possible
- **Scroll Position**: Maintain scroll position during data updates
- **Responsive Design**: Adapt to container size changes

## Accessibility Considerations

- Uses proper ARIA roles including `listbox`, `option`, and `grid` patterns
- Supports complete keyboard navigation with arrow keys and page up/down
- Provides screen reader announcements for navigation and selection
- Maintains proper focus management during virtual scrolling
- Includes aria-posinset and aria-setsize for position information
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafInfiniteScroll**: Infinite scrolling without virtualization
- **SafLoadingSpinner**: Loading indicators for async operations
- **SafEmptyState**: Empty state displays for zero items
- **SafList**: Non-virtualized list component for smaller datasets

## Notes

- SafVirtualScroller only renders visible items plus overscan buffer
- The component automatically handles scroll position calculations
- Dynamic height support requires height estimation and measurement
- Horizontal scrolling uses the same API with direction="horizontal"
- Performance monitoring helps optimize for specific use cases
- Memory usage remains constant regardless of total item count
- Scroll-to-index functionality enables programmatic navigation
- Accessibility features provide comprehensive keyboard and screen reader support
