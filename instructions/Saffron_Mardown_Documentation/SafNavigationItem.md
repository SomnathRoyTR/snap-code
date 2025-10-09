# SafNavigationItem

## Overview

SafNavigationItem is an individual navigation element that can be used within navigation systems. It supports various states, interactions, hierarchical structures, and provides consistent styling and behavior for navigation interfaces across applications.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string` | - | Navigation item text label |
| `href` | `string` | - | URL for navigation link |
| `active` | `boolean` | `false` | Whether item is currently active |
| `disabled` | `boolean` | `false` | Disables item interaction |
| `icon` | `string \| ReactElement` | - | Icon displayed before label |
| `iconPosition` | `'start' \| 'end'` | `'start'` | Icon position relative to label |
| `badge` | `string \| number \| ReactElement` | - | Badge content (count, status, etc.) |
| `badgeVariant` | `'default' \| 'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | `'default'` | Badge color variant |
| `children` | `NavigationItem[]` | - | Nested navigation items |
| `expanded` | `boolean` | `false` | Whether submenu is expanded |
| `expandable` | `boolean` | - | Whether item can be expanded (auto-detected from children) |
| `level` | `number` | `0` | Nesting level for indentation |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Item size variant |
| `variant` | `'default' \| 'primary' \| 'secondary' \| 'sidebar' \| 'breadcrumb'` | `'default'` | Visual style variant |
| `target` | `'_self' \| '_blank' \| '_parent' \| '_top'` | `'_self'` | Link target attribute |
| `external` | `boolean` | `false` | Indicates external link (shows icon) |
| `loading` | `boolean` | `false` | Shows loading state |
| `tooltip` | `string` | - | Tooltip text on hover |
| `ariaLabel` | `string` | - | Accessibility label override |
| `testId` | `string` | - | Test identifier |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(event: MouseEvent) => void` | Fired when item is clicked |
| `onExpand` | `(expanded: boolean) => void` | Fired when expansion state changes |
| `onFocus` | `(event: FocusEvent) => void` | Fired when item receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when item loses focus |
| `onKeyDown` | `(event: KeyboardEvent) => void` | Fired on key press |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string` | - | Navigation item text label |
| `href` | `string` | - | URL for navigation link |
| `active` | `boolean` | `false` | Whether item is currently active |
| `disabled` | `boolean` | `false` | Disables item interaction |
| `icon` | `string` | - | Icon name displayed before label |
| `iconPosition` | `'start' \| 'end'` | `'start'` | Icon position relative to label |
| `badge` | `string \| number` | - | Badge content (count, status, etc.) |
| `badgeVariant` | `'default' \| 'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | `'default'` | Badge color variant |
| `expanded` | `boolean` | `false` | Whether submenu is expanded |
| `expandable` | `boolean` | - | Whether item can be expanded |
| `level` | `number` | `0` | Nesting level for indentation |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Item size variant |
| `variant` | `'default' \| 'primary' \| 'secondary' \| 'sidebar' \| 'breadcrumb'` | `'default'` | Visual style variant |
| `target` | `string` | `'_self'` | Link target attribute |
| `external` | `boolean` | `false` | Indicates external link |
| `loading` | `boolean` | `false` | Shows loading state |
| `tooltip` | `string` | - | Tooltip text on hover |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `itemClick` | `EventEmitter<MouseEvent>` | Fired when item is clicked |
| `expand` | `EventEmitter<boolean>` | Fired when expansion state changes |
| `focus` | `EventEmitter<FocusEvent>` | Fired when item receives focus |
| `blur` | `EventEmitter<FocusEvent>` | Fired when item loses focus |

## Usage Examples

### Basic Navigation Item

```typescript
// React
<SafNavigationItem 
  label="Dashboard"
  href="/dashboard"
  icon="dashboard"
  onClick={(event) => console.log('Clicked:', event)}
/>
```

```html
<!-- Angular -->
<saf-navigation-item 
  label="Dashboard"
  href="/dashboard"
  icon="dashboard"
  (itemClick)="onItemClick($event)">
</saf-navigation-item>
```

### Active Navigation Item

```typescript
// React
<SafNavigationItem 
  label="Current Page"
  href="/current"
  active
  icon="home"
/>
```

### Navigation Item with Badge

```typescript
// React
<SafNavigationItem 
  label="Messages"
  href="/messages"
  icon="mail"
  badge={12}
  badgeVariant="primary"
/>
```

### Expandable Navigation Item

```typescript
// React
const [expanded, setExpanded] = useState(false);

<SafNavigationItem 
  label="Products"
  icon="inventory"
  expandable
  expanded={expanded}
  onExpand={setExpanded}
  children={[
    { key: 'all', label: 'All Products', href: '/products' },
    { key: 'categories', label: 'Categories', href: '/products/categories' },
    { key: 'inventory', label: 'Inventory', href: '/products/inventory' }
  ]}
/>
```

### External Link Item

```typescript
// React
<SafNavigationItem 
  label="Documentation"
  href="https://docs.example.com"
  external
  target="_blank"
  icon="external-link"
/>
```

### Sidebar Navigation Items

```typescript
// React
const SidebarNavigation = ({ items, activeItem }) => (
  <nav className="sidebar">
    {items.map(item => (
      <SafNavigationItem 
        key={item.key}
        label={item.label}
        href={item.href}
        icon={item.icon}
        badge={item.badge}
        active={activeItem === item.key}
        variant="sidebar"
        size="medium"
      />
    ))}
  </nav>
);
```

### Breadcrumb Navigation

```typescript
// React
const BreadcrumbNavigation = ({ breadcrumbs }) => (
  <nav className="breadcrumb">
    {breadcrumbs.map((crumb, index) => (
      <SafNavigationItem 
        key={crumb.key}
        label={crumb.label}
        href={index < breadcrumbs.length - 1 ? crumb.href : undefined}
        variant="breadcrumb"
        active={index === breadcrumbs.length - 1}
        size="small"
      />
    ))}
  </nav>
);
```

### Multi-Level Navigation

```typescript
// React
const MultiLevelNavigation = ({ navigationTree }) => {
  const [expandedItems, setExpandedItems] = useState(new Set());

  const handleExpand = (itemKey, expanded) => {
    const newExpanded = new Set(expandedItems);
    if (expanded) {
      newExpanded.add(itemKey);
    } else {
      newExpanded.delete(itemKey);
    }
    setExpandedItems(newExpanded);
  };

  const renderNavItem = (item, level = 0) => (
    <SafNavigationItem 
      key={item.key}
      label={item.label}
      href={item.href}
      icon={item.icon}
      badge={item.badge}
      level={level}
      expandable={!!item.children}
      expanded={expandedItems.has(item.key)}
      onExpand={(expanded) => handleExpand(item.key, expanded)}
      disabled={item.disabled}
    >
      {item.children && expandedItems.has(item.key) && 
        item.children.map(child => renderNavItem(child, level + 1))
      }
    </SafNavigationItem>
  );

  return (
    <nav className="multi-level-nav">
      {navigationTree.map(item => renderNavItem(item))}
    </nav>
  );
};
```

### Tab Navigation Items

```typescript
// React
const TabNavigation = ({ tabs, activeTab, onTabChange }) => (
  <div className="tab-navigation">
    {tabs.map(tab => (
      <SafNavigationItem 
        key={tab.key}
        label={tab.label}
        active={activeTab === tab.key}
        variant="primary"
        badge={tab.count}
        disabled={tab.disabled}
        onClick={() => onTabChange(tab.key)}
      />
    ))}
  </div>
);
```

### Mobile Navigation Items

```typescript
// React
const MobileNavigation = ({ items, onItemClick }) => (
  <div className="mobile-nav">
    {items.map(item => (
      <SafNavigationItem 
        key={item.key}
        label={item.label}
        icon={item.icon}
        badge={item.badge}
        size="large"
        onClick={() => onItemClick(item)}
        style={{ 
          justifyContent: 'center',
          flexDirection: 'column',
          textAlign: 'center'
        }}
      />
    ))}
  </div>
);
```

### Admin Panel Navigation

```typescript
// React
const AdminPanelNav = ({ sections, userPermissions }) => {
  const hasPermission = (section) => {
    return section.permissions.some(p => userPermissions.includes(p));
  };

  return (
    <div className="admin-nav">
      {sections.map(section => (
        <SafNavigationItem 
          key={section.key}
          label={section.label}
          href={section.href}
          icon={section.icon}
          badge={section.alertCount}
          badgeVariant="error"
          disabled={!hasPermission(section)}
          variant="sidebar"
          tooltip={!hasPermission(section) ? 'Access restricted' : undefined}
        />
      ))}
    </div>
  );
};
```

### Navigation with Loading States

```typescript
// React
const NavigationWithLoading = ({ items, loadingItems }) => (
  <nav className="nav-with-loading">
    {items.map(item => (
      <SafNavigationItem 
        key={item.key}
        label={item.label}
        href={item.href}
        icon={item.icon}
        loading={loadingItems.includes(item.key)}
        disabled={loadingItems.includes(item.key)}
      />
    ))}
  </nav>
);
```

### Context Menu Navigation

```typescript
// React
const ContextMenuNav = ({ actions, onActionSelect }) => (
  <div className="context-menu">
    {actions.map(action => (
      <SafNavigationItem 
        key={action.key}
        label={action.label}
        icon={action.icon}
        disabled={action.disabled}
        variant="secondary"
        size="small"
        onClick={() => onActionSelect(action)}
      />
    ))}
  </div>
);
```

### E-commerce Category Navigation

```typescript
// React
const CategoryNavigation = ({ categories, selectedCategory }) => {
  const [expandedCategories, setExpandedCategories] = useState(new Set());

  const handleCategoryExpand = (categoryId, expanded) => {
    const newExpanded = new Set(expandedCategories);
    if (expanded) {
      newExpanded.add(categoryId);
    } else {
      newExpanded.delete(categoryId);
    }
    setExpandedCategories(newExpanded);
  };

  return (
    <nav className="category-nav">
      {categories.map(category => (
        <SafNavigationItem 
          key={category.id}
          label={category.name}
          href={`/category/${category.slug}`}
          active={selectedCategory === category.id}
          expandable={category.subcategories?.length > 0}
          expanded={expandedCategories.has(category.id)}
          onExpand={(expanded) => handleCategoryExpand(category.id, expanded)}
          badge={category.productCount}
          variant="sidebar"
        >
          {category.subcategories && expandedCategories.has(category.id) && 
            category.subcategories.map(sub => (
              <SafNavigationItem 
                key={sub.id}
                label={sub.name}
                href={`/category/${category.slug}/${sub.slug}`}
                level={1}
                badge={sub.productCount}
                size="small"
              />
            ))
          }
        </SafNavigationItem>
      ))}
    </nav>
  );
};
```

### Settings Navigation

```typescript
// React
const SettingsNavigation = ({ settingsSections, currentSection }) => (
  <nav className="settings-nav">
    <div className="nav-header">
      <h3>Settings</h3>
    </div>
    {settingsSections.map(section => (
      <SafNavigationItem 
        key={section.key}
        label={section.title}
        href={`/settings/${section.key}`}
        icon={section.icon}
        active={currentSection === section.key}
        variant="sidebar"
        badge={section.hasChanges ? '•' : undefined}
        badgeVariant="warning"
      />
    ))}
  </nav>
);
```

### Dashboard Widget Navigation

```typescript
// React
const DashboardNav = ({ widgets, activeWidget, onWidgetSelect }) => (
  <div className="dashboard-nav">
    {widgets.map(widget => (
      <SafNavigationItem 
        key={widget.id}
        label={widget.name}
        icon={widget.icon}
        active={activeWidget === widget.id}
        badge={widget.alertCount}
        badgeVariant={widget.status === 'error' ? 'error' : 'primary'}
        disabled={!widget.enabled}
        onClick={() => onWidgetSelect(widget.id)}
        tooltip={`${widget.description} ${widget.enabled ? '' : '(Disabled)'}`}
      />
    ))}
  </div>
);
```

### User Profile Navigation

```typescript
// React
const UserProfileNav = ({ user, profileSections }) => (
  <div className="profile-nav">
    <div className="profile-header">
      <SafAvatar src={user.avatar} name={user.name} />
      <div className="user-info">
        <div className="user-name">{user.name}</div>
        <div className="user-role">{user.role}</div>
      </div>
    </div>
    
    {profileSections.map(section => (
      <SafNavigationItem 
        key={section.key}
        label={section.label}
        href={`/profile/${section.key}`}
        icon={section.icon}
        badge={section.requiresAttention ? '!' : undefined}
        badgeVariant="warning"
        variant="sidebar"
      />
    ))}
  </div>
);
```

## Best Practices

### Content and Labeling
- **Clear Labels**: Use descriptive and action-oriented labels
- **Consistent Terminology**: Use consistent language across navigation
- **Icon Alignment**: Choose icons that clearly represent the content
- **Badge Usage**: Use badges for counts and status indicators appropriately

### Visual Hierarchy
- **Active States**: Clearly indicate current location/selection
- **Nesting Levels**: Use consistent indentation for nested items
- **Size Consistency**: Maintain consistent sizing within navigation groups
- **Color Usage**: Use color meaningfully for states and categories

### Interaction Design
- **Touch Targets**: Ensure adequate touch target size (44px minimum)
- **Hover States**: Provide clear hover feedback
- **Loading States**: Show loading indicators for async operations
- **Disabled States**: Clearly indicate and explain disabled items

### Accessibility
- **Keyboard Navigation**: Support arrow keys and Enter/Space
- **Screen Readers**: Provide proper ARIA labels and descriptions
- **Focus Management**: Maintain logical focus order
- **Color Contrast**: Ensure sufficient contrast for all states

## Accessibility Considerations

- Uses semantic HTML elements (`<a>`, `<button>`) based on functionality
- Implements proper ARIA attributes including `aria-current` for active items
- Supports keyboard navigation with Tab, Enter, Space, and arrow keys
- Provides screen reader announcements for state changes
- Maintains proper focus order and visible focus indicators
- Supports high contrast mode and respects reduced motion preferences

## Related Components

- **SafNavigation**: Container component for navigation systems
- **SafBreadcrumb**: Breadcrumb navigation component
- **SafTabs**: Tab-based navigation system
- **SafDrawer**: Slide-out navigation drawer
- **SafSidebar**: Fixed sidebar navigation container
- **SafButton**: Basic button component for actions

## Notes

- SafNavigationItem automatically handles active state styling based on current URL
- The component supports both link (`href`) and button (`onClick`) behaviors
- Badge positioning and styling adapt automatically to the item size and variant
- Icon positioning can be customized and supports both string names and React elements
- Loading states disable interaction and show appropriate visual feedback
- External links automatically receive appropriate security attributes (`rel="noopener"`)
- The component integrates seamlessly with routing libraries and navigation systems
- Tooltip behavior respects user preferences for reduced motion
