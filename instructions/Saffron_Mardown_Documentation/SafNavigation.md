# SafNavigation

## Overview

SafNavigation is a flexible navigation component that provides hierarchical menu structures with support for multiple levels, various layouts, responsive behavior, and accessibility features. It serves as the primary navigation container for applications with complex navigation requirements.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `NavigationItem[]` | `[]` | Array of navigation items |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `variant` | `'primary' \| 'secondary' \| 'sidebar' \| 'tabs' \| 'breadcrumb'` | `'primary'` | Navigation style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size of navigation items |
| `activeItem` | `string` | - | Currently active item key |
| `defaultActiveItem` | `string` | - | Default active item (uncontrolled) |
| `expandedItems` | `string[]` | `[]` | Keys of expanded submenu items |
| `defaultExpandedItems` | `string[]` | `[]` | Default expanded items (uncontrolled) |
| `collapsible` | `boolean` | `true` | Allow collapsing submenus |
| `multiSelect` | `boolean` | `false` | Allow multiple expanded submenus |
| `showIcons` | `boolean` | `true` | Display item icons |
| `showBadges` | `boolean` | `true` | Display item badges/counters |
| `responsive` | `boolean` | `true` | Enable responsive behavior |
| `mobileBreakpoint` | `number` | `768` | Mobile breakpoint in pixels |
| `collapseMode` | `'hidden' \| 'overlay' \| 'drawer'` | `'overlay'` | Mobile collapse behavior |
| `sticky` | `boolean` | `false` | Enable sticky positioning |
| `bordered` | `boolean` | `false` | Add border styling |
| `separator` | `string \| ReactElement` | - | Custom separator between items |
| `loading` | `boolean` | `false` | Show loading state |
| `disabled` | `boolean` | `false` | Disable all interactions |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### NavigationItem Interface

```typescript
interface NavigationItem {
  key: string;
  label: string;
  href?: string;
  icon?: string | ReactElement;
  badge?: string | number;
  disabled?: boolean;
  children?: NavigationItem[];
  target?: string;
  onClick?: () => void;
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onItemClick` | `(item: NavigationItem, event: Event) => void` | Fired when item is clicked |
| `onActiveItemChange` | `(key: string) => void` | Fired when active item changes |
| `onExpandedItemsChange` | `(keys: string[]) => void` | Fired when submenu expansion changes |
| `onCollapseChange` | `(collapsed: boolean) => void` | Fired when navigation collapses/expands |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `NavigationItem[]` | `[]` | Array of navigation items |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout orientation |
| `variant` | `'primary' \| 'secondary' \| 'sidebar' \| 'tabs' \| 'breadcrumb'` | `'primary'` | Navigation style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size of navigation items |
| `activeItem` | `string` | - | Currently active item key |
| `expandedItems` | `string[]` | `[]` | Keys of expanded submenu items |
| `collapsible` | `boolean` | `true` | Allow collapsing submenus |
| `multiSelect` | `boolean` | `false` | Allow multiple expanded submenus |
| `showIcons` | `boolean` | `true` | Display item icons |
| `showBadges` | `boolean` | `true` | Display item badges/counters |
| `responsive` | `boolean` | `true` | Enable responsive behavior |
| `mobileBreakpoint` | `number` | `768` | Mobile breakpoint in pixels |
| `collapseMode` | `'hidden' \| 'overlay' \| 'drawer'` | `'overlay'` | Mobile collapse behavior |
| `sticky` | `boolean` | `false` | Enable sticky positioning |
| `bordered` | `boolean` | `false` | Add border styling |
| `loading` | `boolean` | `false` | Show loading state |
| `disabled` | `boolean` | `false` | Disable all interactions |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `itemClick` | `EventEmitter<{item: NavigationItem, event: Event}>` | Fired when item is clicked |
| `activeItemChange` | `EventEmitter<string>` | Fired when active item changes |
| `expandedItemsChange` | `EventEmitter<string[]>` | Fired when submenu expansion changes |
| `collapseChange` | `EventEmitter<boolean>` | Fired when navigation collapses/expands |

## Usage Examples

### Basic Navigation

```typescript
// React
const navigationItems = [
  { key: 'home', label: 'Home', icon: 'home', href: '/' },
  { key: 'about', label: 'About', icon: 'info', href: '/about' },
  { key: 'services', label: 'Services', icon: 'services', href: '/services' },
  { key: 'contact', label: 'Contact', icon: 'mail', href: '/contact' }
];

<SafNavigation 
  items={navigationItems}
  activeItem="home"
  onItemClick={(item) => console.log('Clicked:', item.label)}
/>
```

```html
<!-- Angular -->
<saf-navigation 
  [items]="navigationItems"
  [activeItem]="'home'"
  (itemClick)="onItemClick($event)">
</saf-navigation>
```

### Multi-Level Navigation

```typescript
// React
const multiLevelItems = [
  { 
    key: 'dashboard', 
    label: 'Dashboard', 
    icon: 'dashboard', 
    href: '/dashboard' 
  },
  {
    key: 'products',
    label: 'Products',
    icon: 'inventory',
    children: [
      { key: 'products-list', label: 'All Products', href: '/products' },
      { key: 'products-categories', label: 'Categories', href: '/products/categories' },
      { key: 'products-inventory', label: 'Inventory', href: '/products/inventory' },
      {
        key: 'products-reports',
        label: 'Reports',
        children: [
          { key: 'sales-report', label: 'Sales Report', href: '/products/reports/sales' },
          { key: 'inventory-report', label: 'Inventory Report', href: '/products/reports/inventory' }
        ]
      }
    ]
  },
  {
    key: 'customers',
    label: 'Customers',
    icon: 'people',
    badge: 12,
    children: [
      { key: 'customers-list', label: 'All Customers', href: '/customers' },
      { key: 'customers-groups', label: 'Customer Groups', href: '/customers/groups' }
    ]
  },
  {
    key: 'settings',
    label: 'Settings',
    icon: 'settings',
    children: [
      { key: 'account-settings', label: 'Account', href: '/settings/account' },
      { key: 'preferences', label: 'Preferences', href: '/settings/preferences' },
      { key: 'security', label: 'Security', href: '/settings/security' }
    ]
  }
];

<SafNavigation 
  items={multiLevelItems}
  orientation="vertical"
  variant="sidebar"
  activeItem="products-list"
  expandedItems={['products']}
  onActiveItemChange={setActiveItem}
  onExpandedItemsChange={setExpandedItems}
/>
```

### Responsive Navigation

```typescript
// React
const ResponsiveNavigation = ({ navigationItems }) => {
  const [activeItem, setActiveItem] = useState('home');
  const [collapsed, setCollapsed] = useState(false);

  return (
    <SafNavigation 
      items={navigationItems}
      activeItem={activeItem}
      onActiveItemChange={setActiveItem}
      responsive
      mobileBreakpoint={768}
      collapseMode="drawer"
      onCollapseChange={setCollapsed}
      sticky
    />
  );
};
```

### Tab Navigation

```typescript
// React
const TabNavigation = ({ tabs }) => (
  <SafNavigation 
    items={tabs}
    variant="tabs"
    orientation="horizontal"
    activeItem="overview"
    bordered
    onItemClick={(item) => {
      // Handle tab change
      setActiveTab(item.key);
    }}
  />
);

const tabs = [
  { key: 'overview', label: 'Overview', href: '#overview' },
  { key: 'details', label: 'Details', badge: '2', href: '#details' },
  { key: 'history', label: 'History', href: '#history' },
  { key: 'settings', label: 'Settings', disabled: true, href: '#settings' }
];
```

### Breadcrumb Navigation

```typescript
// React
const BreadcrumbNav = ({ breadcrumbs }) => (
  <SafNavigation 
    items={breadcrumbs}
    variant="breadcrumb"
    separator="/"
    showIcons={false}
  />
);

const breadcrumbs = [
  { key: 'home', label: 'Home', href: '/' },
  { key: 'products', label: 'Products', href: '/products' },
  { key: 'category', label: 'Electronics', href: '/products/electronics' },
  { key: 'product', label: 'Laptop', href: '/products/electronics/laptop' }
];
```

### Navigation with Search

```typescript
// React
const NavigationWithSearch = ({ items }) => {
  const [searchTerm, setSearchTerm] = useState('');
  
  const filteredItems = useMemo(() => {
    if (!searchTerm) return items;
    
    const filterItems = (items) => {
      return items.reduce((acc, item) => {
        if (item.label.toLowerCase().includes(searchTerm.toLowerCase())) {
          acc.push(item);
        } else if (item.children) {
          const filteredChildren = filterItems(item.children);
          if (filteredChildren.length > 0) {
            acc.push({ ...item, children: filteredChildren });
          }
        }
        return acc;
      }, []);
    };
    
    return filterItems(items);
  }, [items, searchTerm]);

  return (
    <div className="navigation-with-search">
      <div className="navigation-header">
        <SafSearchBox 
          value={searchTerm}
          onChange={setSearchTerm}
          placeholder="Search navigation..."
          size="small"
        />
      </div>
      <SafNavigation 
        items={filteredItems}
        variant="sidebar"
        orientation="vertical"
      />
    </div>
  );
};
```

### Admin Panel Navigation

```typescript
// React
const AdminNavigation = ({ user, notifications }) => {
  const navigationItems = [
    {
      key: 'dashboard',
      label: 'Dashboard',
      icon: 'dashboard',
      href: '/admin/dashboard'
    },
    {
      key: 'content',
      label: 'Content Management',
      icon: 'content',
      children: [
        { key: 'posts', label: 'Posts', badge: notifications.posts, href: '/admin/posts' },
        { key: 'pages', label: 'Pages', href: '/admin/pages' },
        { key: 'media', label: 'Media Library', href: '/admin/media' },
        { key: 'comments', label: 'Comments', badge: notifications.comments, href: '/admin/comments' }
      ]
    },
    {
      key: 'users',
      label: 'User Management',
      icon: 'people',
      children: [
        { key: 'all-users', label: 'All Users', href: '/admin/users' },
        { key: 'user-roles', label: 'Roles & Permissions', href: '/admin/users/roles' },
        { key: 'user-groups', label: 'User Groups', href: '/admin/users/groups' }
      ]
    },
    {
      key: 'analytics',
      label: 'Analytics',
      icon: 'analytics',
      children: [
        { key: 'overview', label: 'Overview', href: '/admin/analytics' },
        { key: 'traffic', label: 'Traffic', href: '/admin/analytics/traffic' },
        { key: 'conversions', label: 'Conversions', href: '/admin/analytics/conversions' }
      ]
    },
    {
      key: 'settings',
      label: 'System Settings',
      icon: 'settings',
      children: [
        { key: 'general', label: 'General', href: '/admin/settings/general' },
        { key: 'security', label: 'Security', href: '/admin/settings/security' },
        { key: 'integrations', label: 'Integrations', href: '/admin/settings/integrations' },
        { key: 'backup', label: 'Backup & Restore', href: '/admin/settings/backup' }
      ]
    }
  ];

  return (
    <div className="admin-sidebar">
      <div className="sidebar-header">
        <SafAvatar name={user.name} src={user.avatar} size="small" />
        <div className="user-info">
          <div className="user-name">{user.name}</div>
          <div className="user-role">{user.role}</div>
        </div>
      </div>
      
      <SafNavigation 
        items={navigationItems}
        orientation="vertical"
        variant="sidebar"
        showBadges
        collapsible
        multiSelect
      />
    </div>
  );
};
```

### E-commerce Navigation

```typescript
// React
const EcommerceNavigation = ({ categories, cartCount }) => {
  const navigationItems = [
    { key: 'home', label: 'Home', href: '/' },
    {
      key: 'shop',
      label: 'Shop',
      children: categories.map(category => ({
        key: category.slug,
        label: category.name,
        href: `/shop/${category.slug}`,
        children: category.subcategories?.map(sub => ({
          key: sub.slug,
          label: sub.name,
          href: `/shop/${category.slug}/${sub.slug}`
        }))
      }))
    },
    { key: 'deals', label: 'Deals', badge: 'New', href: '/deals' },
    { key: 'about', label: 'About Us', href: '/about' },
    { key: 'contact', label: 'Contact', href: '/contact' },
    { 
      key: 'cart', 
      label: 'Cart', 
      icon: 'shopping-cart',
      badge: cartCount,
      href: '/cart' 
    }
  ];

  return (
    <SafNavigation 
      items={navigationItems}
      orientation="horizontal"
      variant="primary"
      responsive
      collapseMode="overlay"
    />
  );
};
```

### Documentation Navigation

```typescript
// React
const DocNavigation = ({ docStructure, currentPath }) => {
  const [expandedSections, setExpandedSections] = useState([]);

  const buildNavigationItems = (sections) => {
    return sections.map(section => ({
      key: section.id,
      label: section.title,
      href: section.path,
      children: section.children ? buildNavigationItems(section.children) : undefined
    }));
  };

  const navigationItems = buildNavigationItems(docStructure);

  return (
    <div className="doc-sidebar">
      <div className="sidebar-header">
        <h3>Documentation</h3>
      </div>
      
      <SafNavigation 
        items={navigationItems}
        orientation="vertical"
        variant="sidebar"
        size="small"
        activeItem={currentPath}
        expandedItems={expandedSections}
        onExpandedItemsChange={setExpandedSections}
        showIcons={false}
        multiSelect={false}
      />
    </div>
  );
};
```

### Mobile App Navigation

```typescript
// React
const MobileAppNavigation = ({ user }) => {
  const bottomNavItems = [
    { key: 'home', label: 'Home', icon: 'home' },
    { key: 'explore', label: 'Explore', icon: 'search' },
    { key: 'favorites', label: 'Favorites', icon: 'heart', badge: 3 },
    { key: 'profile', label: 'Profile', icon: 'person' }
  ];

  return (
    <div className="mobile-navigation">
      <SafNavigation 
        items={bottomNavItems}
        orientation="horizontal"
        variant="primary"
        size="small"
        showBadges
        className="bottom-navigation"
      />
    </div>
  );
};
```

### Context-Aware Navigation

```typescript
// React
const ContextAwareNavigation = ({ currentModule, permissions }) => {
  const getNavigationForModule = (module) => {
    const baseItems = {
      dashboard: [
        { key: 'overview', label: 'Overview', icon: 'dashboard' },
        { key: 'analytics', label: 'Analytics', icon: 'chart' }
      ],
      projects: [
        { key: 'all-projects', label: 'All Projects', icon: 'folder' },
        { key: 'my-projects', label: 'My Projects', icon: 'person-folder' },
        { key: 'archived', label: 'Archived', icon: 'archive' }
      ],
      team: [
        { key: 'members', label: 'Team Members', icon: 'people' },
        { key: 'departments', label: 'Departments', icon: 'group' },
        { key: 'roles', label: 'Roles', icon: 'security' }
      ]
    };

    return baseItems[module]?.filter(item => 
      permissions.includes(item.key) || !item.permission
    ) || [];
  };

  const navigationItems = getNavigationForModule(currentModule);

  return (
    <SafNavigation 
      items={navigationItems}
      orientation="horizontal"
      variant="tabs"
      responsive
      onItemClick={(item) => {
        // Handle module navigation
        navigateToModuleSection(currentModule, item.key);
      }}
    />
  );
};
```

### Navigation with Loading States

```typescript
// React
const NavigationWithLoading = ({ isLoading }) => {
  const [navigationItems, setNavigationItems] = useState([]);

  useEffect(() => {
    if (!isLoading) {
      // Load navigation items from API
      loadNavigationItems().then(setNavigationItems);
    }
  }, [isLoading]);

  if (isLoading) {
    return (
      <SafNavigation 
        items={[
          { key: 'loading-1', label: 'Loading...', disabled: true },
          { key: 'loading-2', label: 'Loading...', disabled: true },
          { key: 'loading-3', label: 'Loading...', disabled: true }
        ]}
        loading
        disabled
      />
    );
  }

  return (
    <SafNavigation 
      items={navigationItems}
      onItemClick={(item) => {
        // Handle navigation
        navigate(item.href);
      }}
    />
  );
};
```

## Best Practices

### Structure and Organization
- **Logical Grouping**: Group related items together in submenus
- **Consistent Depth**: Avoid excessive nesting (max 3 levels recommended)
- **Clear Labels**: Use descriptive and actionable labels
- **Icon Usage**: Use icons consistently and meaningfully

### Navigation Hierarchy
- **Priority-Based Ordering**: Place most important items first
- **User Flow**: Organize items based on typical user workflows
- **Progressive Disclosure**: Show advanced options in submenus
- **Contextual Grouping**: Group items by functional area

### Responsive Design
- **Mobile-First**: Design navigation for mobile experiences first
- **Breakpoint Strategy**: Choose appropriate collapse points
- **Touch Targets**: Ensure adequate touch target sizes on mobile
- **Gesture Support**: Support swipe gestures where appropriate

### Performance
- **Lazy Loading**: Load submenu items on demand when possible
- **Virtual Scrolling**: Use virtual scrolling for very large navigation trees
- **Debounced Search**: Implement debounced search for filtering
- **Minimize Re-renders**: Optimize state management to reduce re-renders

## Accessibility Considerations

- Uses proper ARIA navigation landmarks and roles
- Supports keyboard navigation with arrow keys, Enter, Escape
- Provides screen reader announcements for state changes
- Maintains proper focus management during navigation
- Implements proper heading hierarchy for screen readers
- Supports high contrast mode and custom color schemes

## Related Components

- **SafNavigationItem**: Individual navigation item component
- **SafBreadcrumb**: Breadcrumb navigation component
- **SafDrawer**: Slide-out navigation drawer
- **SafTabs**: Tab-based navigation component
- **SafSidebar**: Fixed sidebar navigation
- **SafMenuButton**: Hamburger menu button for mobile

## Notes

- SafNavigation automatically handles responsive behavior and breakpoints
- The component supports both controlled and uncontrolled state management
- Nested navigation items are rendered recursively with proper indentation
- Badge counts and indicators are automatically formatted and positioned
- The component integrates with routing libraries through href and onClick props
- Mobile navigation can be customized with different collapse modes
- Keyboard navigation follows standard navigation patterns
- The component supports both horizontal and vertical layouts seamlessly
