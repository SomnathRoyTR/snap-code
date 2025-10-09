# SafEmptyState

## Overview

SafEmptyState is a component for displaying empty or no-data states in a user-friendly way. It provides consistent messaging, illustrations, and actions to guide users when content is unavailable, helping maintain engagement and providing clear next steps for various empty state scenarios.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'default' \| 'search' \| 'error' \| 'loading' \| 'filtered' \| 'first-use'` | `'default'` | Type of empty state determining default content |
| `title` | `string` | - | Primary heading text |
| `description` | `string` | - | Supporting description text |
| `illustration` | `string \| ReactElement` | - | Image, icon, or custom illustration |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Overall size affecting spacing and typography |
| `actions` | `Array<{ label: string; onClick: () => void; variant?: string; icon?: string; disabled?: boolean }>` | `[]` | Action buttons |
| `secondaryActions` | `Array<{ label: string; onClick: () => void; icon?: string }>` | `[]` | Secondary/text action buttons |
| `showBackButton` | `boolean` | `false` | Shows back navigation button |
| `compact` | `boolean` | `false` | Reduces padding and spacing |
| `centered` | `boolean` | `true` | Centers content horizontally |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Custom content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onActionClick` | `(actionIndex: number) => void` | Fired when primary action is clicked |
| `onSecondaryActionClick` | `(actionIndex: number) => void` | Fired when secondary action is clicked |
| `onBack` | `() => void` | Fired when back button is clicked |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `'default' \| 'search' \| 'error' \| 'loading' \| 'filtered' \| 'first-use'` | `'default'` | Type of empty state determining default content |
| `title` | `string` | - | Primary heading text |
| `description` | `string` | - | Supporting description text |
| `illustration` | `string` | - | Image URL or icon name |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Overall size affecting spacing and typography |
| `actions` | `Array<{ label: string; variant?: string; icon?: string; disabled?: boolean }>` | `[]` | Action buttons configuration |
| `secondaryActions` | `Array<{ label: string; icon?: string }>` | `[]` | Secondary action buttons |
| `showBackButton` | `boolean` | `false` | Shows back navigation button |
| `compact` | `boolean` | `false` | Reduces padding and spacing |
| `centered` | `boolean` | `true` | Centers content horizontally |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `actionClick` | `EventEmitter<number>` | Fired when primary action is clicked |
| `secondaryActionClick` | `EventEmitter<number>` | Fired when secondary action is clicked |
| `back` | `EventEmitter<void>` | Fired when back button is clicked |

## Usage Examples

### Basic Empty States

```typescript
// React
<SafEmptyState 
  title="No items found"
  description="There are no items to display at the moment."
  illustration="inbox"
  actions={[
    { label: 'Add Item', onClick: () => addNewItem() }
  ]}
/>

<SafEmptyState 
  variant="search"
  title="No results found"
  description="We couldn't find anything matching your search."
  illustration="search-empty"
  actions={[
    { label: 'Clear Search', onClick: () => clearSearch() }
  ]}
  secondaryActions={[
    { label: 'Browse All Items', onClick: () => browseAll() }
  ]}
/>
```

```html
<!-- Angular -->
<saf-empty-state 
  title="No items found"
  description="There are no items to display at the moment."
  illustration="inbox"
  [actions]="addItemActions"
  (actionClick)="handleAction($event)">
</saf-empty-state>

<saf-empty-state 
  variant="search"
  title="No results found"
  description="We couldn't find anything matching your search."
  illustration="search-empty"
  [actions]="searchActions"
  [secondaryActions]="browseActions"
  (actionClick)="handleSearchAction($event)"
  (secondaryActionClick)="handleSecondaryAction($event)">
</saf-empty-state>
```

### Error State

```typescript
// React
<SafEmptyState 
  variant="error"
  title="Something went wrong"
  description="We're having trouble loading your data right now."
  illustration="error-cloud"
  actions={[
    { label: 'Try Again', onClick: () => retry(), icon: 'refresh' },
    { label: 'Contact Support', onClick: () => contactSupport(), variant: 'outline' }
  ]}
  showBackButton
  onBack={() => goBack()}
/>
```

```html
<!-- Angular -->
<saf-empty-state 
  variant="error"
  title="Something went wrong"
  description="We're having trouble loading your data right now."
  illustration="error-cloud"
  [actions]="errorActions"
  [showBackButton]="true"
  (actionClick)="handleErrorAction($event)"
  (back)="goBack()">
</saf-empty-state>
```

### First Use Experience

```typescript
// React
<SafEmptyState 
  variant="first-use"
  title="Welcome to Your Dashboard"
  description="Get started by creating your first project and inviting team members."
  illustration="/images/welcome-dashboard.svg"
  size="large"
  actions={[
    { label: 'Create Project', onClick: () => createProject(), icon: 'plus' },
    { label: 'Import Data', onClick: () => importData(), variant: 'outline', icon: 'upload' }
  ]}
  secondaryActions={[
    { label: 'Take Tour', onClick: () => startTour(), icon: 'play' },
    { label: 'View Documentation', onClick: () => viewDocs(), icon: 'book' }
  ]}
/>
```

```html
<!-- Angular -->
<saf-empty-state 
  variant="first-use"
  title="Welcome to Your Dashboard"
  description="Get started by creating your first project and inviting team members."
  illustration="/images/welcome-dashboard.svg"
  size="large"
  [actions]="firstUseActions"
  [secondaryActions]="firstUseSecondaryActions"
  (actionClick)="handleFirstUseAction($event)"
  (secondaryActionClick)="handleSecondaryAction($event)">
</saf-empty-state>
```

### Loading State

```typescript
// React
<SafEmptyState 
  variant="loading"
  title="Loading your content"
  description="Please wait while we fetch your data..."
  illustration={<SafSpinner size="large" />}
/>
```

```html
<!-- Angular -->
<saf-empty-state 
  variant="loading"
  title="Loading your content"
  description="Please wait while we fetch your data..."
  illustration="spinner">
</saf-empty-state>
```

### Filtered Results

```typescript
// React
<SafEmptyState 
  variant="filtered"
  title="No matches for current filters"
  description="Try adjusting your filters to see more results."
  illustration="filter-empty"
  actions={[
    { label: 'Clear Filters', onClick: () => clearFilters() },
    { label: 'Reset All', onClick: () => resetFilters(), variant: 'outline' }
  ]}
  compact
/>
```

```html
<!-- Angular -->
<saf-empty-state 
  variant="filtered"
  title="No matches for current filters"
  description="Try adjusting your filters to see more results."
  illustration="filter-empty"
  [actions]="filterActions"
  [compact]="true"
  (actionClick)="handleFilterAction($event)">
</saf-empty-state>
```

### Size Variants

```typescript
// React
<SafEmptyState 
  size="small"
  title="No notifications"
  description="You're all caught up!"
  illustration="check-circle"
  compact
/>

<SafEmptyState 
  size="medium"
  title="No files uploaded"
  description="Drag and drop files here to get started."
  illustration="upload-cloud"
  actions={[
    { label: 'Browse Files', onClick: () => browseFiles() }
  ]}
/>

<SafEmptyState 
  size="large"
  title="Welcome to Analytics"
  description="Connect your data sources to start seeing insights about your business."
  illustration="/images/analytics-hero.svg"
  actions={[
    { label: 'Connect Data Source', onClick: () => connectData() },
    { label: 'Upload CSV', onClick: () => uploadCSV(), variant: 'outline' }
  ]}
  secondaryActions={[
    { label: 'View Sample Dashboard', onClick: () => viewSample() }
  ]}
/>
```

### Custom Content

```typescript
// React
<SafEmptyState 
  title="Inbox Zero Achieved!"
  illustration="celebration"
  size="large"
>
  <div style={{ textAlign: 'center' }}>
    <p>🎉 Congratulations! You've processed all your messages.</p>
    <SafProgressRing value={100} variant="success" size="medium">
      <SafIcon name="check" />
    </SafProgressRing>
    <p>Take a moment to enjoy this achievement.</p>
    <div style={{ marginTop: '24px' }}>
      <SafButton onClick={() => celebrateSuccess()}>
        Share Achievement
      </SafButton>
      <SafButton variant="text" onClick={() => continueWorking()}>
        Continue Working
      </SafButton>
    </div>
  </div>
</SafEmptyState>
```

### Data Tables Empty State

```typescript
// React
const DataTableEmpty = ({ searchQuery, hasFilters }) => (
  <SafEmptyState 
    variant={searchQuery ? "search" : hasFilters ? "filtered" : "default"}
    title={
      searchQuery ? `No results for "${searchQuery}"` :
      hasFilters ? "No matches for current filters" :
      "No data available"
    }
    description={
      searchQuery ? "Try a different search term or browse all items." :
      hasFilters ? "Adjust your filters to see more results." :
      "Get started by adding your first entry."
    }
    illustration={searchQuery ? "search-empty" : hasFilters ? "filter-empty" : "table-empty"}
    actions={
      searchQuery ? [
        { label: 'Clear Search', onClick: () => clearSearch() }
      ] : hasFilters ? [
        { label: 'Clear Filters', onClick: () => clearFilters() }
      ] : [
        { label: 'Add Entry', onClick: () => addEntry() }
      ]
    }
    secondaryActions={
      searchQuery || hasFilters ? [
        { label: 'Show All', onClick: () => showAll() }
      ] : [
        { label: 'Import Data', onClick: () => importData() }
      ]
    }
    compact
  />
);
```

### E-commerce Empty States

```typescript
// React
// Empty Shopping Cart
<SafEmptyState 
  title="Your cart is empty"
  description="Looks like you haven't added any items to your cart yet."
  illustration="shopping-cart-empty"
  actions={[
    { label: 'Continue Shopping', onClick: () => continueShopping() }
  ]}
  secondaryActions={[
    { label: 'View Wishlist', onClick: () => viewWishlist() },
    { label: 'Browse Categories', onClick: () => browseCategories() }
  ]}
/>

// Empty Wishlist
<SafEmptyState 
  title="Your wishlist is empty"
  description="Save items you love to your wishlist for easy access later."
  illustration="heart-empty"
  actions={[
    { label: 'Explore Products', onClick: () => exploreProducts() }
  ]}
  secondaryActions={[
    { label: 'View Recommendations', onClick: () => viewRecommendations() }
  ]}
/>
```

### Content Management Empty States

```typescript
// React
// Empty Blog Posts
<SafEmptyState 
  variant="first-use"
  title="No blog posts yet"
  description="Create your first blog post to start sharing your thoughts with the world."
  illustration="pencil-paper"
  actions={[
    { label: 'Write First Post', onClick: () => createPost(), icon: 'pen' }
  ]}
  secondaryActions={[
    { label: 'Import from Draft', onClick: () => importDraft() },
    { label: 'Browse Templates', onClick: () => browseTemplates() }
  ]}
/>

// Empty Media Library
<SafEmptyState 
  title="No media files"
  description="Upload images, videos, and documents to your media library."
  illustration="folder-empty"
  actions={[
    { label: 'Upload Files', onClick: () => uploadFiles(), icon: 'upload' }
  ]}
  secondaryActions={[
    { label: 'Connect Cloud Storage', onClick: () => connectCloud() }
  ]}
/>
```

### Team Collaboration Empty States

```typescript
// React
// Empty Team
<SafEmptyState 
  variant="first-use"
  title="Build your team"
  description="Invite team members to start collaborating on projects together."
  illustration="team-collaboration"
  size="large"
  actions={[
    { label: 'Invite Team Members', onClick: () => inviteTeam(), icon: 'user-plus' }
  ]}
  secondaryActions={[
    { label: 'Create Team', onClick: () => createTeam() },
    { label: 'Join Existing Team', onClick: () => joinTeam() }
  ]}
/>

// Empty Projects
<SafEmptyState 
  title="No projects yet"
  description="Create your first project to start organizing your work."
  illustration="project-launch"
  actions={[
    { label: 'New Project', onClick: () => createProject(), icon: 'plus' },
    { label: 'Use Template', onClick: () => useTemplate(), variant: 'outline' }
  ]}
  secondaryActions={[
    { label: 'Import Project', onClick: () => importProject() }
  ]}
/>
```

### Responsive Empty States

```typescript
// React
const ResponsiveEmptyState = ({ isMobile }) => (
  <SafEmptyState 
    title="No messages"
    description={isMobile ? "No messages yet." : "You don't have any messages in your inbox yet."}
    illustration="envelope-empty"
    size={isMobile ? "small" : "medium"}
    compact={isMobile}
    actions={[
      { 
        label: isMobile ? "Compose" : "Compose Message", 
        onClick: () => composeMessage(),
        icon: "pen"
      }
    ]}
    secondaryActions={isMobile ? [] : [
      { label: 'Check Spam Folder', onClick: () => checkSpam() }
    ]}
  />
);
```

## Best Practices

### Content Strategy
- **Clear Messaging**: Use descriptive, encouraging titles and descriptions
- **Action-Oriented**: Provide clear next steps for users
- **Context Awareness**: Tailor content to the specific empty state scenario
- **Positive Tone**: Frame empty states as opportunities rather than failures

### Visual Design
- **Appropriate Illustrations**: Use relevant, engaging illustrations that reinforce the message
- **Size Selection**: Choose sizes that fit the container and content importance
- **Consistent Branding**: Ensure illustrations and colors align with brand guidelines
- **Accessibility**: Provide alt text for illustrations and ensure sufficient contrast

### User Experience
- **Primary Actions**: Make the most important action prominent and easy to find
- **Multiple Pathways**: Offer alternative actions when appropriate
- **Back Navigation**: Provide back buttons when users might be lost
- **Loading States**: Use loading variants for async operations

### Responsive Design
- **Mobile Optimization**: Adjust content length and button sizes for mobile
- **Flexible Layout**: Ensure empty states work well across different screen sizes
- **Touch Targets**: Make action buttons appropriately sized for touch interaction
- **Content Priority**: Show most important information first on smaller screens

## Accessibility Considerations

- Uses semantic HTML structure with appropriate headings
- Provides alternative text for illustrations and icons
- Ensures sufficient color contrast for all text content
- Supports keyboard navigation for all interactive elements
- Includes proper ARIA labels for screen readers
- Maintains focus management for action buttons

## Related Components

- **SafMessageBox**: Related component for inline messaging
- **SafLoader**: Component for full-page loading states
- **SafSpinner**: Simple loading indicator
- **SafCard**: Container component that may contain empty states
- **SafAlert**: Alert component for system messages
- **SafIllustration**: Dedicated component for empty state illustrations

## Notes

- SafEmptyState automatically provides appropriate default content for each variant
- Custom illustrations can be URLs, icon names, or React elements
- Action buttons are automatically styled to maintain visual hierarchy
- The component is designed to be flexible and work within various container sizes
- Secondary actions are displayed with less visual prominence
- Back buttons integrate with standard navigation patterns
- Variants provide sensible defaults but can be fully customized
- The component supports both static and dynamic content scenarios
