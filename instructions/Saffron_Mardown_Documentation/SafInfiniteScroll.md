# SafInfiniteScroll

## Overview

SafInfiniteScroll is a component that automatically loads and displays additional content as the user scrolls near the end of the current content. It provides seamless pagination for large datasets, supports various loading strategies, handles loading states, and includes accessibility features for assistive technologies.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `children` | `ReactNode` | - | Current list of items to display |
| `hasNextPage` | `boolean` | `false` | Whether more items can be loaded |
| `loading` | `boolean` | `false` | Current loading state |
| `loadMore` | `() => void \| Promise<void>` | - | Function to load more items |
| `threshold` | `number` | `200` | Pixels from bottom to trigger load |
| `loader` | `ReactNode` | - | Custom loading indicator |
| `endMessage` | `ReactNode` | - | Message when all items loaded |
| `scrollableTarget` | `string \| HTMLElement` | `window` | Scrollable container |
| `inverse` | `boolean` | `false` | Load items at top (chat style) |
| `pullToRefresh` | `boolean` | `false` | Enable pull-to-refresh |
| `refreshFunction` | `() => void \| Promise<void>` | - | Refresh function |
| `pullDownToRefreshThreshold` | `number` | `100` | Pull threshold for refresh |
| `onScroll` | `(event: Event) => void` | - | Scroll event handler |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `hasNextPage` | `boolean` | `false` | Whether more items can be loaded |
| `loading` | `boolean` | `false` | Current loading state |
| `threshold` | `number` | `200` | Pixels from bottom to trigger load |
| `inverse` | `boolean` | `false` | Load items at top (chat style) |
| `pullToRefresh` | `boolean` | `false` | Enable pull-to-refresh |
| `pullDownToRefreshThreshold` | `number` | `100` | Pull threshold for refresh |
| `scrollableTarget` | `string \| HTMLElement` | `window` | Scrollable container |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `loadMore` | `EventEmitter<void>` | Fired when more items should be loaded |
| `refresh` | `EventEmitter<void>` | Fired when pull-to-refresh triggered |
| `scroll` | `EventEmitter<Event>` | Fired on scroll events |

## Usage Examples

### Basic Infinite Scroll

```typescript
// React
const BasicInfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);

  const loadMoreItems = async () => {
    if (loading) return;

    setLoading(true);
    try {
      const newItems = await fetchItems(page, 20);
      
      if (newItems.length === 0) {
        setHasMore(false);
      } else {
        setItems(prev => [...prev, ...newItems]);
        setPage(prev => prev + 1);
      }
    } catch (error) {
      console.error('Failed to load items:', error);
    } finally {
      setLoading(false);
    }
  };

  // Load initial items
  useEffect(() => {
    loadMoreItems();
  }, []);

  const renderItem = (item, index) => (
    <div key={item.id || index} className="infinite-scroll-item">
      <div className="item-header">
        <SafAvatar 
          src={item.avatar}
          name={item.author}
          size="medium"
        />
        <div className="item-info">
          <h4>{item.title}</h4>
          <p className="item-author">{item.author}</p>
          <span className="item-date">
            {new Date(item.createdAt).toLocaleDateString()}
          </span>
        </div>
      </div>
      
      <div className="item-content">
        <p>{item.description}</p>
        {item.tags && (
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
        )}
      </div>
      
      <div className="item-actions">
        <SafButton
          variant="ghost"
          size="small"
          icon={<SafIcon name="heart" />}
          onClick={() => console.log('Like:', item.id)}
        >
          {item.likes}
        </SafButton>
        <SafButton
          variant="ghost"
          size="small"
          icon={<SafIcon name="message-circle" />}
          onClick={() => console.log('Comment:', item.id)}
        >
          {item.comments}
        </SafButton>
        <SafButton
          variant="ghost"
          size="small"
          icon={<SafIcon name="share" />}
          onClick={() => console.log('Share:', item.id)}
        />
      </div>
    </div>
  );

  return (
    <div className="basic-infinite-scroll">
      <div className="infinite-scroll-header">
        <h3>Infinite Scroll Feed</h3>
        <SafBadge 
          label={`${items.length} items loaded`}
          color="primary"
        />
      </div>
      
      <SafInfiniteScroll
        hasNextPage={hasMore}
        loading={loading}
        loadMore={loadMoreItems}
        loader={
          <div className="infinite-loader">
            <SafLoadingSpinner size="medium" />
            <span>Loading more items...</span>
          </div>
        }
        endMessage={
          <div className="infinite-end-message">
            <SafIcon name="check-circle" color="success" />
            <span>All items loaded</span>
          </div>
        }
      >
        <div className="infinite-scroll-items">
          {items.map((item, index) => renderItem(item, index))}
        </div>
      </SafInfiniteScroll>
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-infinite-scroll">
  <div class="infinite-scroll-header">
    <h3>Infinite Scroll Feed</h3>
    <saf-badge 
      [label]="items.length + ' items loaded'"
      color="primary">
    </saf-badge>
  </div>
  
  <saf-infinite-scroll
    [hasNextPage]="hasMore"
    [loading]="loading"
    (loadMore)="loadMoreItems()">
    
    <div class="infinite-scroll-items">
      <div 
        *ngFor="let item of items; index as i" 
        class="infinite-scroll-item">
        
        <div class="item-header">
          <saf-avatar 
            [src]="item.avatar"
            [name]="item.author"
            size="medium">
          </saf-avatar>
          <div class="item-info">
            <h4>{{item.title}}</h4>
            <p class="item-author">{{item.author}}</p>
            <span class="item-date">
              {{item.createdAt | date}}
            </span>
          </div>
        </div>
        
        <div class="item-content">
          <p>{{item.description}}</p>
          <div class="item-tags" *ngIf="item.tags">
            <saf-badge
              *ngFor="let tag of item.tags"
              [label]="tag"
              size="small"
              variant="outline">
            </saf-badge>
          </div>
        </div>
        
        <div class="item-actions">
          <saf-button
            variant="ghost"
            size="small"
            (click)="likeItem(item.id)">
            <saf-icon name="heart"></saf-icon>
            {{item.likes}}
          </saf-button>
          <saf-button
            variant="ghost"
            size="small"
            (click)="commentItem(item.id)">
            <saf-icon name="message-circle"></saf-icon>
            {{item.comments}}
          </saf-button>
          <saf-button
            variant="ghost"
            size="small"
            (click)="shareItem(item.id)">
            <saf-icon name="share"></saf-icon>
          </saf-button>
        </div>
      </div>
    </div>
    
    <!-- Loading template -->
    <ng-container infiniteScrollLoader>
      <div class="infinite-loader">
        <saf-loading-spinner size="medium"></saf-loading-spinner>
        <span>Loading more items...</span>
      </div>
    </ng-container>
    
    <!-- End message template -->
    <ng-container infiniteScrollEndMessage>
      <div class="infinite-end-message">
        <saf-icon name="check-circle" color="success"></saf-icon>
        <span>All items loaded</span>
      </div>
    </ng-container>
  </saf-infinite-scroll>
</div>
```

### Infinite Scroll with Search and Filters

```typescript
// React
const SearchableInfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedCategory, setSelectedCategory] = useState('all');
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);

  // Reset pagination when search/filter changes
  useEffect(() => {
    setItems([]);
    setPage(1);
    setHasMore(true);
    loadMoreItems(true);
  }, [searchQuery, selectedCategory]);

  const loadMoreItems = async (reset = false) => {
    if (loading) return;

    setLoading(true);
    try {
      const currentPage = reset ? 1 : page;
      const newItems = await fetchFilteredItems({
        page: currentPage,
        pageSize: 20,
        search: searchQuery,
        category: selectedCategory
      });
      
      if (newItems.length === 0) {
        setHasMore(false);
      } else {
        setItems(prev => reset ? newItems : [...prev, ...newItems]);
        setPage(currentPage + 1);
      }
    } catch (error) {
      console.error('Failed to load items:', error);
    } finally {
      setLoading(false);
    }
  };

  const handleSearchChange = (query) => {
    setSearchQuery(query);
  };

  const handleCategoryChange = (category) => {
    setSelectedCategory(category);
  };

  const renderProduct = (product) => (
    <div key={product.id} className="product-card">
      <div className="product-image">
        <SafImage 
          src={product.image}
          alt={product.name}
          width="100%"
          height={200}
          placeholder="product"
        />
        {product.discount && (
          <SafBadge 
            label={`${product.discount}% OFF`}
            color="error"
            className="discount-badge"
          />
        )}
      </div>
      
      <div className="product-info">
        <div className="product-category">
          <SafBadge 
            label={product.category}
            size="small"
            variant="outline"
          />
        </div>
        
        <h4 className="product-name">{product.name}</h4>
        <p className="product-description">{product.description}</p>
        
        <div className="product-rating">
          <div className="rating-stars">
            {[...Array(5)].map((_, i) => (
              <SafIcon
                key={i}
                name="star"
                size="small"
                className={i < product.rating ? 'filled' : 'empty'}
              />
            ))}
          </div>
          <span className="rating-count">({product.reviewCount})</span>
        </div>
        
        <div className="product-price">
          {product.originalPrice && product.originalPrice !== product.price && (
            <span className="original-price">${product.originalPrice}</span>
          )}
          <span className="current-price">${product.price}</span>
        </div>
        
        <div className="product-actions">
          <SafButton
            variant="primary"
            onClick={() => console.log('Add to cart:', product.id)}
          >
            Add to Cart
          </SafButton>
          <SafButton
            variant="outline"
            onClick={() => console.log('View details:', product.id)}
          >
            View Details
          </SafButton>
        </div>
      </div>
    </div>
  );

  const categories = [
    { value: 'all', label: 'All Categories' },
    { value: 'electronics', label: 'Electronics' },
    { value: 'clothing', label: 'Clothing' },
    { value: 'books', label: 'Books' },
    { value: 'home', label: 'Home & Garden' },
    { value: 'sports', label: 'Sports' }
  ];

  return (
    <div className="searchable-infinite-scroll">
      <div className="scroll-header">
        <h3>Product Catalog</h3>
        
        <div className="scroll-controls">
          <SafSearchField
            placeholder="Search products..."
            value={searchQuery}
            onSearch={handleSearchChange}
            clearable
          />
          
          <SafDropdown
            label="Category"
            value={selectedCategory}
            onChange={handleCategoryChange}
            options={categories}
          />
        </div>
        
        <div className="scroll-stats">
          <span>{items.length} products loaded</span>
          {searchQuery && (
            <SafBadge 
              label={`Searching: "${searchQuery}"`}
              color="primary"
            />
          )}
          {selectedCategory !== 'all' && (
            <SafBadge 
              label={`Category: ${selectedCategory}`}
              color="secondary"
            />
          )}
        </div>
      </div>
      
      <SafInfiniteScroll
        hasNextPage={hasMore}
        loading={loading}
        loadMore={() => loadMoreItems(false)}
        threshold={300}
        loader={
          <div className="products-loader">
            <SafLoadingSpinner size="large" />
            <span>Loading more products...</span>
          </div>
        }
        endMessage={
          <div className="products-end-message">
            {items.length > 0 ? (
              <>
                <SafIcon name="package" size="large" color="success" />
                <h4>All products loaded</h4>
                <p>Found {items.length} products matching your criteria</p>
              </>
            ) : (
              <>
                <SafIcon name="search-x" size="large" color="warning" />
                <h4>No products found</h4>
                <p>Try adjusting your search or filters</p>
              </>
            )}
          </div>
        }
      >
        <div className="products-grid">
          {items.map(product => renderProduct(product))}
        </div>
      </SafInfiniteScroll>
    </div>
  );
};
```

### Chat-Style Infinite Scroll (Inverse)

```typescript
// React
const ChatInfiniteScroll = ({ chatId }) => {
  const [messages, setMessages] = useState([]);
  const [hasOlderMessages, setHasOlderMessages] = useState(true);
  const [loading, setLoading] = useState(false);
  const [oldestMessageId, setOldestMessageId] = useState(null);

  const loadOlderMessages = async () => {
    if (loading) return;

    setLoading(true);
    try {
      const olderMessages = await fetchOlderMessages({
        chatId,
        beforeId: oldestMessageId,
        limit: 30
      });
      
      if (olderMessages.length === 0) {
        setHasOlderMessages(false);
      } else {
        setMessages(prev => [...olderMessages, ...prev]);
        setOldestMessageId(olderMessages[0].id);
      }
    } catch (error) {
      console.error('Failed to load older messages:', error);
    } finally {
      setLoading(false);
    }
  };

  // Load initial messages
  useEffect(() => {
    const loadInitialMessages = async () => {
      const initialMessages = await fetchRecentMessages(chatId, 30);
      setMessages(initialMessages);
      
      if (initialMessages.length > 0) {
        setOldestMessageId(initialMessages[0].id);
      }
    };
    
    loadInitialMessages();
  }, [chatId]);

  const renderMessage = (message) => {
    const isCurrentUser = message.senderId === currentUserId;
    
    return (
      <div 
        key={message.id} 
        className={`chat-message ${isCurrentUser ? 'current-user' : 'other-user'}`}
      >
        {!isCurrentUser && (
          <SafAvatar 
            src={message.sender.avatar}
            name={message.sender.name}
            size="small"
            className="message-avatar"
          />
        )}
        
        <div className="message-content">
          <div className="message-bubble">
            {message.type === 'text' && (
              <p>{message.text}</p>
            )}
            
            {message.type === 'image' && (
              <div className="message-image">
                <SafImage 
                  src={message.imageUrl}
                  alt="Shared image"
                  maxWidth={300}
                  onClick={() => console.log('View full image')}
                />
              </div>
            )}
            
            {message.type === 'file' && (
              <div className="message-file">
                <SafIcon name="paperclip" />
                <span>{message.fileName}</span>
                <SafButton
                  variant="ghost"
                  size="small"
                  onClick={() => console.log('Download file:', message.fileId)}
                >
                  Download
                </SafButton>
              </div>
            )}
          </div>
          
          <div className="message-meta">
            {!isCurrentUser && (
              <span className="sender-name">{message.sender.name}</span>
            )}
            <span className="message-time">
              {new Date(message.timestamp).toLocaleTimeString()}
            </span>
            {message.edited && (
              <SafBadge 
                label="edited"
                size="small"
                variant="outline"
              />
            )}
            {isCurrentUser && message.status && (
              <SafIcon 
                name={message.status === 'delivered' ? 'check' : 'check-check'}
                size="small"
                className="message-status"
              />
            )}
          </div>
        </div>
      </div>
    );
  };

  return (
    <div className="chat-infinite-scroll">
      <div className="chat-header">
        <SafAvatar 
          src={chat.avatar}
          name={chat.name}
          size="medium"
        />
        <div className="chat-info">
          <h4>{chat.name}</h4>
          <span className="chat-status">{chat.isOnline ? 'Online' : 'Last seen recently'}</span>
        </div>
        <div className="chat-actions">
          <SafIconButton icon={<SafIcon name="phone" />} />
          <SafIconButton icon={<SafIcon name="video" />} />
          <SafIconButton icon={<SafIcon name="more-vertical" />} />
        </div>
      </div>
      
      <SafInfiniteScroll
        hasNextPage={hasOlderMessages}
        loading={loading}
        loadMore={loadOlderMessages}
        inverse={true}
        threshold={100}
        loader={
          <div className="chat-loader">
            <SafLoadingSpinner size="small" />
            <span>Loading older messages...</span>
          </div>
        }
        endMessage={
          <div className="chat-beginning">
            <SafIcon name="message-circle" size="large" color="secondary" />
            <span>This is the beginning of your conversation</span>
          </div>
        }
        className="chat-messages-container"
      >
        <div className="chat-messages">
          {messages.map(message => renderMessage(message))}
        </div>
      </SafInfiniteScroll>
      
      <div className="chat-input">
        <SafTextInput
          placeholder="Type a message..."
          multiline
          maxRows={4}
        />
        <SafButton
          variant="primary"
          icon={<SafIcon name="send" />}
        />
      </div>
    </div>
  );
};
```

### Pull-to-Refresh Infinite Scroll

```typescript
// React
const PullToRefreshInfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);
  const [refreshing, setRefreshing] = useState(false);
  const [lastRefresh, setLastRefresh] = useState(new Date());

  const loadMoreItems = async (resetPagination = false) => {
    if (loading) return;

    setLoading(true);
    try {
      const currentPage = resetPagination ? 1 : page;
      const newItems = await fetchItems(currentPage, 15);
      
      if (newItems.length === 0) {
        setHasMore(false);
      } else {
        setItems(prev => resetPagination ? newItems : [...prev, ...newItems]);
        setPage(resetPagination ? 2 : currentPage + 1);
        
        if (resetPagination) {
          setHasMore(true);
        }
      }
    } catch (error) {
      console.error('Failed to load items:', error);
    } finally {
      setLoading(false);
    }
  };

  const handleRefresh = async () => {
    if (refreshing) return;

    setRefreshing(true);
    try {
      await loadMoreItems(true);
      setLastRefresh(new Date());
    } finally {
      setRefreshing(false);
    }
  };

  // Load initial items
  useEffect(() => {
    loadMoreItems();
  }, []);

  const renderNewsItem = (item) => (
    <div key={item.id} className="news-item">
      <div className="news-image">
        <SafImage 
          src={item.imageUrl}
          alt={item.title}
          width="100%"
          height={200}
          placeholder="news"
        />
        {item.isBreaking && (
          <SafBadge 
            label="BREAKING"
            color="error"
            className="breaking-badge"
          />
        )}
      </div>
      
      <div className="news-content">
        <div className="news-category">
          <SafBadge 
            label={item.category}
            size="small"
            color="primary"
          />
          <span className="news-time">
            {formatTimeAgo(item.publishedAt)}
          </span>
        </div>
        
        <h3 className="news-title">{item.title}</h3>
        <p className="news-summary">{item.summary}</p>
        
        <div className="news-author">
          <SafAvatar 
            src={item.author.avatar}
            name={item.author.name}
            size="small"
          />
          <span className="author-name">{item.author.name}</span>
        </div>
        
        <div className="news-actions">
          <SafButton
            variant="ghost"
            size="small"
            icon={<SafIcon name="bookmark" />}
            onClick={() => console.log('Bookmark:', item.id)}
          />
          <SafButton
            variant="ghost"
            size="small"
            icon={<SafIcon name="share" />}
            onClick={() => console.log('Share:', item.id)}
          />
          <SafButton
            variant="outline"
            size="small"
            onClick={() => console.log('Read more:', item.id)}
          >
            Read More
          </SafButton>
        </div>
      </div>
    </div>
  );

  return (
    <div className="pull-to-refresh-infinite-scroll">
      <div className="news-header">
        <div className="header-title">
          <h2>Latest News</h2>
          <SafBadge 
            label="LIVE"
            color="error"
            className="live-badge"
          />
        </div>
        
        <div className="header-info">
          <span className="last-update">
            Last updated: {lastRefresh.toLocaleTimeString()}
          </span>
          <SafButton
            variant="ghost"
            size="small"
            icon={<SafIcon name="refresh-cw" />}
            onClick={handleRefresh}
            disabled={refreshing}
          >
            {refreshing ? 'Refreshing...' : 'Refresh'}
          </SafButton>
        </div>
      </div>
      
      <SafInfiniteScroll
        hasNextPage={hasMore}
        loading={loading}
        loadMore={() => loadMoreItems(false)}
        pullToRefresh={true}
        refreshFunction={handleRefresh}
        pullDownToRefreshThreshold={80}
        threshold={250}
        loader={
          <div className="news-loader">
            <SafLoadingSpinner size="medium" />
            <span>Loading more news...</span>
          </div>
        }
        endMessage={
          <div className="news-end-message">
            <SafIcon name="newspaper" size="large" color="secondary" />
            <h4>You're all caught up!</h4>
            <p>Check back later for more news updates</p>
            <SafButton
              variant="outline"
              onClick={handleRefresh}
              icon={<SafIcon name="refresh-cw" />}
            >
              Refresh for Latest
            </SafButton>
          </div>
        }
        className="news-infinite-scroll"
      >
        {refreshing && (
          <div className="refresh-indicator">
            <SafLoadingSpinner size="small" />
            <span>Refreshing news...</span>
          </div>
        )}
        
        <div className="news-items">
          {items.map(item => renderNewsItem(item))}
        </div>
      </SafInfiniteScroll>
    </div>
  );
};
```

### Custom Scrollable Container

```typescript
// React
const CustomScrollableInfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [selectedCategory, setSelectedCategory] = useState('documents');
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);
  const scrollContainerRef = useRef(null);

  const loadMoreItems = async () => {
    if (loading) return;

    setLoading(true);
    try {
      const newItems = await fetchCategoryItems(selectedCategory, page, 25);
      
      if (newItems.length === 0) {
        setHasMore(false);
      } else {
        setItems(prev => [...prev, ...newItems]);
        setPage(prev => prev + 1);
      }
    } catch (error) {
      console.error('Failed to load items:', error);
    } finally {
      setLoading(false);
    }
  };

  // Reset when category changes
  useEffect(() => {
    setItems([]);
    setPage(1);
    setHasMore(true);
    loadMoreItems();
  }, [selectedCategory]);

  const renderFileItem = (file) => (
    <div key={file.id} className="file-item">
      <div className="file-icon">
        <SafIcon 
          name={getFileIcon(file.type)}
          size="large"
          color={getFileIconColor(file.type)}
        />
      </div>
      
      <div className="file-info">
        <h4 className="file-name">{file.name}</h4>
        <p className="file-path">{file.path}</p>
        
        <div className="file-meta">
          <span className="file-size">{formatFileSize(file.size)}</span>
          <span className="file-modified">
            Modified {formatDate(file.lastModified)}
          </span>
        </div>
        
        {file.tags && (
          <div className="file-tags">
            {file.tags.map(tag => (
              <SafBadge
                key={tag}
                label={tag}
                size="small"
                variant="outline"
              />
            ))}
          </div>
        )}
      </div>
      
      <div className="file-actions">
        <SafIconButton
          icon={<SafIcon name="eye" />}
          onClick={() => console.log('Preview:', file.id)}
          tooltip="Preview"
        />
        <SafIconButton
          icon={<SafIcon name="download" />}
          onClick={() => console.log('Download:', file.id)}
          tooltip="Download"
        />
        <SafIconButton
          icon={<SafIcon name="share" />}
          onClick={() => console.log('Share:', file.id)}
          tooltip="Share"
        />
        <SafIconButton
          icon={<SafIcon name="more-horizontal" />}
          onClick={() => console.log('More actions:', file.id)}
          tooltip="More"
        />
      </div>
    </div>
  );

  const categories = [
    { value: 'documents', label: 'Documents', icon: 'file-text' },
    { value: 'images', label: 'Images', icon: 'image' },
    { value: 'videos', label: 'Videos', icon: 'video' },
    { value: 'audio', label: 'Audio', icon: 'music' },
    { value: 'archives', label: 'Archives', icon: 'archive' },
    { value: 'other', label: 'Other', icon: 'file' }
  ];

  return (
    <div className="custom-scrollable-infinite-scroll">
      <div className="file-manager-header">
        <h3>File Manager</h3>
        
        <div className="category-tabs">
          {categories.map(category => (
            <SafButton
              key={category.value}
              variant={selectedCategory === category.value ? 'primary' : 'ghost'}
              size="small"
              icon={<SafIcon name={category.icon} />}
              onClick={() => setSelectedCategory(category.value)}
            >
              {category.label}
            </SafButton>
          ))}
        </div>
        
        <div className="file-stats">
          <SafBadge 
            label={`${items.length} files`}
            color="secondary"
          />
        </div>
      </div>
      
      <div className="file-manager-container">
        <div className="file-manager-sidebar">
          <SafNavigation>
            <SafNavigationItem icon={<SafIcon name="home" />} label="Home" />
            <SafNavigationItem icon={<SafIcon name="star" />} label="Favorites" />
            <SafNavigationItem icon={<SafIcon name="clock" />} label="Recent" />
            <SafNavigationItem icon={<SafIcon name="trash-2" />} label="Trash" />
          </SafNavigation>
          
          <div className="storage-info">
            <h4>Storage</h4>
            <SafProgressBar 
              value={72}
              max={100}
              label="72% used"
            />
            <p>28 GB free of 100 GB</p>
          </div>
        </div>
        
        <div 
          className="file-manager-content"
          ref={scrollContainerRef}
        >
          <SafInfiniteScroll
            hasNextPage={hasMore}
            loading={loading}
            loadMore={loadMoreItems}
            scrollableTarget={scrollContainerRef.current}
            threshold={200}
            loader={
              <div className="file-loader">
                <SafLoadingSpinner size="medium" />
                <span>Loading more files...</span>
              </div>
            }
            endMessage={
              <div className="files-end-message">
                <SafIcon name="folder" size="large" color="secondary" />
                <h4>All files loaded</h4>
                <p>{items.length} files in {selectedCategory}</p>
              </div>
            }
          >
            <div className="file-list">
              {items.map(file => renderFileItem(file))}
            </div>
          </SafInfiniteScroll>
        </div>
      </div>
    </div>
  );
};
```

### Performance Optimized Infinite Scroll

```typescript
// React
const PerformanceOptimizedInfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  const [retryCount, setRetryCount] = useState(0);
  const loadingRef = useRef(false);
  const abortControllerRef = useRef(null);

  // Debounce load more to prevent rapid firing
  const debouncedLoadMore = useMemo(
    () => debounce(async () => {
      if (loadingRef.current || !hasMore) return;

      loadingRef.current = true;
      setLoading(true);
      setError(null);

      // Cancel previous request if still pending
      if (abortControllerRef.current) {
        abortControllerRef.current.abort();
      }

      abortControllerRef.current = new AbortController();

      try {
        const newItems = await fetchItemsWithRetry({
          page,
          pageSize: 50,
          signal: abortControllerRef.current.signal,
          retryCount: 3
        });

        if (newItems.length === 0) {
          setHasMore(false);
        } else {
          // Use functional update for better performance
          setItems(prevItems => {
            const existingIds = new Set(prevItems.map(item => item.id));
            const uniqueNewItems = newItems.filter(item => !existingIds.has(item.id));
            return [...prevItems, ...uniqueNewItems];
          });
          setPage(prev => prev + 1);
        }
        
        setRetryCount(0);
      } catch (error) {
        if (error.name !== 'AbortError') {
          console.error('Failed to load items:', error);
          setError(error);
          setRetryCount(prev => prev + 1);
        }
      } finally {
        loadingRef.current = false;
        setLoading(false);
      }
    }, 300),
    [page, hasMore]
  );

  // Memoize item renderer for performance
  const MemoizedItem = memo(({ item, index }) => (
    <div className="performance-item">
      <div className="item-header">
        <SafAvatar 
          src={item.avatar}
          name={item.name}
          size="medium"
        />
        <div className="item-info">
          <h4>{item.title}</h4>
          <p className="item-subtitle">{item.subtitle}</p>
        </div>
        <SafBadge 
          label={`#${index + 1}`}
          size="small"
          color="secondary"
        />
      </div>
      
      <div className="item-content">
        <p>{item.description}</p>
        
        {item.metrics && (
          <div className="item-metrics">
            {Object.entries(item.metrics).map(([key, value]) => (
              <div key={key} className="metric">
                <span className="metric-label">{key}:</span>
                <span className="metric-value">{value}</span>
              </div>
            ))}
          </div>
        )}
        
        <div className="item-chart">
          <div className="mini-chart">
            {item.chartData?.map((value, i) => (
              <div
                key={i}
                className="chart-bar"
                style={{ height: `${(value / 100) * 30}px` }}
              />
            ))}
          </div>
        </div>
      </div>
      
      <div className="item-actions">
        <SafButton
          variant="outline"
          size="small"
          onClick={() => console.log('View:', item.id)}
        >
          View Details
        </SafButton>
      </div>
    </div>
  ));

  const retryLoad = () => {
    setError(null);
    debouncedLoadMore();
  };

  // Load initial items
  useEffect(() => {
    debouncedLoadMore();
    
    return () => {
      if (abortControllerRef.current) {
        abortControllerRef.current.abort();
      }
    };
  }, []);

  // Custom error boundary for graceful error handling
  const ErrorBoundary = ({ children }) => (
    <div className="infinite-scroll-error">
      {error && (
        <div className="error-message">
          <SafIcon name="alert-circle" color="error" />
          <h4>Failed to load more items</h4>
          <p>{error.message}</p>
          <div className="error-actions">
            <SafButton
              variant="outline"
              onClick={retryLoad}
              icon={<SafIcon name="refresh-cw" />}
            >
              Retry ({retryCount}/3)
            </SafButton>
          </div>
        </div>
      )}
      {children}
    </div>
  );

  return (
    <div className="performance-optimized-infinite-scroll">
      <div className="performance-header">
        <h3>Performance Optimized Feed</h3>
        <div className="performance-stats">
          <SafBadge 
            label={`${items.length} items`}
            color="primary"
          />
          <SafBadge 
            label={loading ? 'Loading...' : 'Ready'}
            color={loading ? 'warning' : 'success'}
          />
        </div>
      </div>
      
      <ErrorBoundary>
        <SafInfiniteScroll
          hasNextPage={hasMore && !error}
          loading={loading}
          loadMore={debouncedLoadMore}
          threshold={500}
          loader={
            <div className="optimized-loader">
              <SafLoadingSpinner size="medium" />
              <span>Optimizing load performance...</span>
              <div className="loader-progress">
                <SafProgressBar 
                  value={((page - 1) * 50)}
                  max={1000}
                  size="small"
                />
              </div>
            </div>
          }
          endMessage={
            <div className="optimized-end-message">
              <SafIcon name="zap" size="large" color="success" />
              <h4>All items loaded efficiently!</h4>
              <p>Loaded {items.length} items with optimal performance</p>
            </div>
          }
        >
          <div className="optimized-items">
            {items.map((item, index) => (
              <MemoizedItem key={item.id} item={item} index={index} />
            ))}
          </div>
        </SafInfiniteScroll>
      </ErrorBoundary>
    </div>
  );
};
```

## Best Practices

### Performance Optimization
- **Debounce Loading**: Prevent rapid consecutive load requests
- **Request Cancellation**: Cancel previous requests when new ones are initiated
- **Memoization**: Use React.memo or similar for expensive item components
- **Efficient Updates**: Use functional state updates for better performance

### Data Management
- **Deduplication**: Prevent duplicate items when loading more data
- **Stable Keys**: Use stable, unique keys for list items
- **Pagination**: Implement proper cursor or offset-based pagination
- **Error Recovery**: Handle network errors gracefully with retry mechanisms

### User Experience
- **Loading States**: Show clear loading indicators during data fetching
- **Empty States**: Provide meaningful messages when no data is available
- **End Messages**: Indicate when all data has been loaded
- **Pull to Refresh**: Enable refresh functionality on mobile devices

### Accessibility
- **Screen Reader Announcements**: Announce when new content is loaded
- **Loading Indicators**: Use proper ARIA labels for loading states
- **Keyboard Navigation**: Ensure keyboard accessibility for loaded content
- **Focus Management**: Maintain focus appropriately during loading

## Accessibility Considerations

- Uses proper ARIA live regions to announce new content loading
- Supports screen reader navigation with semantic HTML structure
- Provides keyboard-accessible loading and retry mechanisms
- Maintains proper focus management during content updates
- Uses meaningful loading and status announcements
- Supports high contrast mode and respects reduced motion preferences

## Related Components

- **SafVirtualScroller**: Virtual scrolling for performance optimization
- **SafPagination**: Traditional page-based navigation
- **SafLoadingSpinner**: Loading indicators for async operations
- **SafEmptyState**: Empty state displays for zero results

## Notes

- SafInfiniteScroll automatically handles scroll event detection and threshold calculations
- The component supports both window and custom container scrolling
- Pull-to-refresh functionality is available for mobile-friendly experiences
- Inverse scrolling enables chat-style message loading from the top
- Error handling and retry mechanisms ensure robust data loading
- Performance optimizations prevent excessive API calls and memory usage
- The component maintains scroll position stability during data updates
- Accessibility features provide comprehensive screen reader support
