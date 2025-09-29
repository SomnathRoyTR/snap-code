# SafDrawer

## Overview

SafDrawer is a slide-out panel component that provides an overlay or push-style container for navigation menus, settings panels, or additional content. It supports multiple positions, responsive behavior, gesture controls, and accessibility features for creating mobile-friendly and desktop navigation experiences.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `open` | `boolean` | `false` | Controls drawer visibility (controlled) |
| `defaultOpen` | `boolean` | `false` | Initial open state (uncontrolled) |
| `position` | `'left' \| 'right' \| 'top' \| 'bottom'` | `'left'` | Drawer slide direction |
| `variant` | `'overlay' \| 'push' \| 'persistent'` | `'overlay'` | Drawer behavior type |
| `size` | `'small' \| 'medium' \| 'large' \| number \| string` | `'medium'` | Drawer size (width/height) |
| `backdrop` | `boolean \| 'static'` | `true` | Show backdrop and click-to-close |
| `escapeKeyDown` | `boolean` | `true` | Close on Escape key press |
| `swipeGesture` | `boolean` | `true` | Enable swipe-to-close gesture |
| `swipeThreshold` | `number` | `50` | Swipe distance threshold in pixels |
| `modal` | `boolean` | `true` | Modal behavior (focus trap) |
| `keepMounted` | `boolean` | `false` | Keep drawer content mounted when closed |
| `transitionDuration` | `number \| object` | `300` | Animation duration in milliseconds |
| `elevation` | `number` | `16` | Shadow elevation level |
| `anchor` | `'left' \| 'right' \| 'top' \| 'bottom'` | - | Deprecated: use `position` |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |
| `PaperProps` | `object` | - | Props for the paper container |
| `ModalProps` | `object` | - | Props for the modal wrapper |
| `SlideProps` | `object` | - | Props for the slide transition |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onOpen` | `() => void` | Fired when drawer opens |
| `onClose` | `(event: Event, reason: string) => void` | Fired when drawer closes |
| `onBackdropClick` | `(event: MouseEvent) => void` | Fired when backdrop is clicked |
| `onEscapeKeyDown` | `(event: KeyboardEvent) => void` | Fired when Escape key is pressed |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `open` | `boolean` | `false` | Controls drawer visibility |
| `position` | `'left' \| 'right' \| 'top' \| 'bottom'` | `'left'` | Drawer slide direction |
| `variant` | `'overlay' \| 'push' \| 'persistent'` | `'overlay'` | Drawer behavior type |
| `size` | `'small' \| 'medium' \| 'large' \| string` | `'medium'` | Drawer size (width/height) |
| `backdrop` | `boolean \| 'static'` | `true` | Show backdrop and click-to-close |
| `escapeKeyDown` | `boolean` | `true` | Close on Escape key press |
| `swipeGesture` | `boolean` | `true` | Enable swipe-to-close gesture |
| `swipeThreshold` | `number` | `50` | Swipe distance threshold in pixels |
| `modal` | `boolean` | `true` | Modal behavior (focus trap) |
| `keepMounted` | `boolean` | `false` | Keep drawer content mounted when closed |
| `transitionDuration` | `number` | `300` | Animation duration in milliseconds |
| `elevation` | `number` | `16` | Shadow elevation level |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `openChange` | `EventEmitter<boolean>` | Fired when open state changes |
| `backdropClick` | `EventEmitter<MouseEvent>` | Fired when backdrop is clicked |
| `escapeKeyDown` | `EventEmitter<KeyboardEvent>` | Fired when Escape key is pressed |

## Usage Examples

### Basic Drawer

```typescript
// React
const [drawerOpen, setDrawerOpen] = useState(false);

<>
  <SafButton onClick={() => setDrawerOpen(true)}>
    Open Drawer
  </SafButton>
  
  <SafDrawer 
    open={drawerOpen}
    onClose={() => setDrawerOpen(false)}
    position="left"
  >
    <div style={{ padding: '16px', width: '300px' }}>
      <h3>Drawer Content</h3>
      <p>This is the drawer content.</p>
      <SafButton onClick={() => setDrawerOpen(false)}>
        Close
      </SafButton>
    </div>
  </SafDrawer>
</>
```

```html
<!-- Angular -->
<saf-button (click)="drawerOpen = true">Open Drawer</saf-button>

<saf-drawer 
  [open]="drawerOpen"
  (openChange)="drawerOpen = $event"
  position="left">
  <div style="padding: 16px; width: 300px;">
    <h3>Drawer Content</h3>
    <p>This is the drawer content.</p>
    <saf-button (click)="drawerOpen = false">Close</saf-button>
  </div>
</saf-drawer>
```

### Navigation Drawer

```typescript
// React
const NavigationDrawer = ({ open, onClose, navigationItems }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="left"
    variant="persistent"
    size="medium"
  >
    <div className="nav-drawer">
      <div className="drawer-header">
        <h2>Navigation</h2>
        <SafIconButton 
          icon="close" 
          onClick={onClose}
          aria-label="Close navigation"
        />
      </div>
      
      <SafNavigation 
        items={navigationItems}
        orientation="vertical"
        variant="sidebar"
      />
    </div>
  </SafDrawer>
);
```

### Mobile Menu Drawer

```typescript
// React
const MobileMenuDrawer = ({ open, onClose, menuItems }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="left"
    variant="overlay"
    size="280px"
    swipeGesture
    className="mobile-menu-drawer"
  >
    <div className="mobile-menu">
      <div className="menu-header">
        <SafLogo size="small" />
        <SafIconButton 
          icon="close" 
          onClick={onClose}
          size="small"
        />
      </div>
      
      <div className="menu-items">
        {menuItems.map(item => (
          <SafNavigationItem 
            key={item.key}
            label={item.label}
            href={item.href}
            icon={item.icon}
            onClick={() => {
              // Navigate to item
              onClose();
            }}
          />
        ))}
      </div>
      
      <div className="menu-footer">
        <SafButton variant="outline" fullWidth>
          Sign In
        </SafButton>
      </div>
    </div>
  </SafDrawer>
);
```

### Settings Drawer

```typescript
// React
const SettingsDrawer = ({ open, onClose, settings, onSettingsChange }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="right"
    size="400px"
    variant="overlay"
  >
    <div className="settings-drawer">
      <div className="drawer-header">
        <h3>Settings</h3>
        <SafIconButton icon="close" onClick={onClose} />
      </div>
      
      <div className="settings-content">
        <SafFormField label="Theme">
          <SafRadioGroup 
            value={settings.theme}
            onChange={(theme) => onSettingsChange({ ...settings, theme })}
          >
            <SafRadio value="light" label="Light" />
            <SafRadio value="dark" label="Dark" />
            <SafRadio value="auto" label="System" />
          </SafRadioGroup>
        </SafFormField>
        
        <SafFormField label="Notifications">
          <SafCheckbox 
            checked={settings.notifications}
            onChange={(notifications) => onSettingsChange({ ...settings, notifications })}
            label="Enable notifications"
          />
        </SafFormField>
        
        <SafFormField label="Language">
          <SafSelect 
            value={settings.language}
            onChange={(language) => onSettingsChange({ ...settings, language })}
          >
            <SafOption value="en">English</SafOption>
            <SafOption value="es">Spanish</SafOption>
            <SafOption value="fr">French</SafOption>
          </SafSelect>
        </SafFormField>
      </div>
      
      <div className="drawer-actions">
        <SafButton onClick={onClose} variant="outline">
          Cancel
        </SafButton>
        <SafButton onClick={() => saveSettings(settings)}>
          Save Changes
        </SafButton>
      </div>
    </div>
  </SafDrawer>
);
```

### Shopping Cart Drawer

```typescript
// React
const ShoppingCartDrawer = ({ open, onClose, cartItems, onUpdateQuantity, onRemoveItem }) => {
  const total = cartItems.reduce((sum, item) => sum + (item.price * item.quantity), 0);

  return (
    <SafDrawer 
      open={open}
      onClose={onClose}
      position="right"
      size="420px"
      variant="overlay"
    >
      <div className="cart-drawer">
        <div className="drawer-header">
          <h3>Shopping Cart ({cartItems.length})</h3>
          <SafIconButton icon="close" onClick={onClose} />
        </div>
        
        <div className="cart-items">
          {cartItems.length === 0 ? (
            <SafEmptyState 
              icon="shopping-cart"
              title="Your cart is empty"
              description="Add items to get started"
            />
          ) : (
            cartItems.map(item => (
              <div key={item.id} className="cart-item">
                <img src={item.image} alt={item.name} className="item-image" />
                <div className="item-details">
                  <h4>{item.name}</h4>
                  <p className="item-price">${item.price}</p>
                  <div className="quantity-controls">
                    <SafButton 
                      size="small" 
                      variant="outline"
                      onClick={() => onUpdateQuantity(item.id, item.quantity - 1)}
                    >
                      -
                    </SafButton>
                    <span className="quantity">{item.quantity}</span>
                    <SafButton 
                      size="small" 
                      variant="outline"
                      onClick={() => onUpdateQuantity(item.id, item.quantity + 1)}
                    >
                      +
                    </SafButton>
                  </div>
                </div>
                <SafIconButton 
                  icon="delete"
                  onClick={() => onRemoveItem(item.id)}
                  size="small"
                />
              </div>
            ))
          )}
        </div>
        
        {cartItems.length > 0 && (
          <div className="cart-footer">
            <div className="cart-total">
              <strong>Total: ${total.toFixed(2)}</strong>
            </div>
            <SafButton fullWidth size="large">
              Checkout
            </SafButton>
          </div>
        )}
      </div>
    </SafDrawer>
  );
};
```

### Filters Drawer

```typescript
// React
const FiltersDrawer = ({ open, onClose, filters, onFiltersChange }) => {
  const [tempFilters, setTempFilters] = useState(filters);

  const handleApplyFilters = () => {
    onFiltersChange(tempFilters);
    onClose();
  };

  const handleResetFilters = () => {
    const resetFilters = {
      category: 'all',
      priceRange: [0, 1000],
      rating: 0,
      inStock: false
    };
    setTempFilters(resetFilters);
  };

  return (
    <SafDrawer 
      open={open}
      onClose={onClose}
      position="left"
      size="320px"
      variant="overlay"
    >
      <div className="filters-drawer">
        <div className="drawer-header">
          <h3>Filters</h3>
          <div className="header-actions">
            <SafButton 
              variant="text" 
              size="small"
              onClick={handleResetFilters}
            >
              Reset
            </SafButton>
            <SafIconButton icon="close" onClick={onClose} />
          </div>
        </div>
        
        <div className="filters-content">
          <SafFormField label="Category">
            <SafSelect 
              value={tempFilters.category}
              onChange={(category) => setTempFilters({...tempFilters, category})}
            >
              <SafOption value="all">All Categories</SafOption>
              <SafOption value="electronics">Electronics</SafOption>
              <SafOption value="clothing">Clothing</SafOption>
              <SafOption value="books">Books</SafOption>
            </SafSelect>
          </SafFormField>
          
          <SafFormField label="Price Range">
            <SafSlider 
              value={tempFilters.priceRange}
              onChange={(priceRange) => setTempFilters({...tempFilters, priceRange})}
              min={0}
              max={1000}
              range
              formatLabel={(value) => `$${value}`}
            />
          </SafFormField>
          
          <SafFormField label="Minimum Rating">
            <SafSlider 
              value={tempFilters.rating}
              onChange={(rating) => setTempFilters({...tempFilters, rating})}
              min={0}
              max={5}
              step={0.5}
              marks
            />
          </SafFormField>
          
          <SafFormField>
            <SafCheckbox 
              checked={tempFilters.inStock}
              onChange={(inStock) => setTempFilters({...tempFilters, inStock})}
              label="In stock only"
            />
          </SafFormField>
        </div>
        
        <div className="drawer-actions">
          <SafButton onClick={onClose} variant="outline" fullWidth>
            Cancel
          </SafButton>
          <SafButton onClick={handleApplyFilters} fullWidth>
            Apply Filters
          </SafButton>
        </div>
      </div>
    </SafDrawer>
  );
};
```

### Help Drawer

```typescript
// React
const HelpDrawer = ({ open, onClose, helpSections }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="right"
    size="480px"
    variant="overlay"
    keepMounted
  >
    <div className="help-drawer">
      <div className="drawer-header">
        <h3>Help & Support</h3>
        <SafIconButton icon="close" onClick={onClose} />
      </div>
      
      <div className="help-content">
        <SafSearchBox 
          placeholder="Search help articles..."
          size="small"
        />
        
        <SafAccordion>
          {helpSections.map(section => (
            <SafAccordionItem 
              key={section.id}
              title={section.title}
              icon={section.icon}
            >
              <div className="help-section">
                {section.articles.map(article => (
                  <SafNavigationItem 
                    key={article.id}
                    label={article.title}
                    href={article.url}
                    variant="secondary"
                    size="small"
                  />
                ))}
              </div>
            </SafAccordionItem>
          ))}
        </SafAccordion>
        
        <div className="help-actions">
          <SafButton variant="outline" fullWidth>
            Contact Support
          </SafButton>
        </div>
      </div>
    </div>
  </SafDrawer>
);
```

### Profile Drawer

```typescript
// React
const ProfileDrawer = ({ open, onClose, user, onSignOut }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="right"
    size="360px"
    variant="overlay"
  >
    <div className="profile-drawer">
      <div className="drawer-header">
        <div className="profile-info">
          <SafAvatar 
            src={user.avatar} 
            name={user.name} 
            size="large" 
          />
          <div className="user-details">
            <h3>{user.name}</h3>
            <p>{user.email}</p>
            <SafBadge variant={user.plan}>{user.plan}</SafBadge>
          </div>
        </div>
        <SafIconButton icon="close" onClick={onClose} />
      </div>
      
      <div className="profile-menu">
        <SafNavigationItem 
          label="Account Settings"
          href="/account/settings"
          icon="settings"
        />
        <SafNavigationItem 
          label="Billing & Plans"
          href="/account/billing"
          icon="credit-card"
        />
        <SafNavigationItem 
          label="Privacy & Security"
          href="/account/privacy"
          icon="shield"
        />
        <SafNavigationItem 
          label="Notifications"
          href="/account/notifications"
          icon="bell"
        />
        
        <SafDivider />
        
        <SafNavigationItem 
          label="Help & Support"
          href="/help"
          icon="help"
        />
        <SafNavigationItem 
          label="Feedback"
          href="/feedback"
          icon="message"
        />
        
        <SafDivider />
        
        <SafNavigationItem 
          label="Sign Out"
          icon="logout"
          onClick={onSignOut}
        />
      </div>
    </div>
  </SafDrawer>
);
```

### Persistent Sidebar Drawer

```typescript
// React
const PersistentSidebarDrawer = ({ open, onToggle, navigationItems }) => (
  <SafDrawer 
    open={open}
    variant="persistent"
    position="left"
    size="280px"
    backdrop={false}
    modal={false}
  >
    <div className="sidebar-drawer">
      <div className="sidebar-header">
        <SafLogo />
        <SafIconButton 
          icon={open ? "chevron-left" : "chevron-right"}
          onClick={onToggle}
        />
      </div>
      
      <nav className="sidebar-nav">
        <SafNavigation 
          items={navigationItems}
          orientation="vertical"
          variant="sidebar"
          showIcons
          collapsible
        />
      </nav>
    </div>
  </SafDrawer>
);
```

### Bottom Sheet Drawer

```typescript
// React
const BottomSheetDrawer = ({ open, onClose, children }) => (
  <SafDrawer 
    open={open}
    onClose={onClose}
    position="bottom"
    size="50vh"
    variant="overlay"
    swipeGesture
    className="bottom-sheet"
  >
    <div className="bottom-sheet-content">
      <div className="sheet-handle" />
      <div className="sheet-header">
        <h3>Options</h3>
        <SafIconButton icon="close" onClick={onClose} size="small" />
      </div>
      <div className="sheet-body">
        {children}
      </div>
    </div>
  </SafDrawer>
);
```

### Responsive Drawer

```typescript
// React
const ResponsiveDrawer = ({ items, activeItem }) => {
  const [mobileOpen, setMobileOpen] = useState(false);
  const isMobile = useMediaQuery('(max-width: 768px)');

  return (
    <>
      {isMobile && (
        <SafIconButton 
          icon="menu"
          onClick={() => setMobileOpen(true)}
          className="mobile-menu-button"
        />
      )}
      
      <SafDrawer 
        open={isMobile ? mobileOpen : true}
        onClose={() => setMobileOpen(false)}
        variant={isMobile ? 'overlay' : 'persistent'}
        position="left"
        size="280px"
        backdrop={isMobile}
        modal={isMobile}
      >
        <SafNavigation 
          items={items}
          activeItem={activeItem}
          orientation="vertical"
          variant="sidebar"
        />
      </SafDrawer>
    </>
  );
};
```

## Best Practices

### Layout and Positioning
- **Appropriate Position**: Choose drawer position based on content and user flow
- **Size Considerations**: Use appropriate sizes that don't overwhelm the screen
- **Responsive Design**: Adapt drawer behavior for different screen sizes
- **Content Organization**: Structure drawer content logically with clear sections

### User Experience
- **Clear Entry/Exit**: Provide obvious ways to open and close the drawer
- **Backdrop Interaction**: Use backdrop clicks appropriately for different variants
- **Gesture Support**: Enable swipe gestures on touch devices when appropriate
- **Focus Management**: Handle focus properly for accessibility

### Performance
- **Conditional Mounting**: Use `keepMounted` judiciously to balance performance and UX
- **Smooth Animations**: Ensure smooth transitions across devices
- **Content Loading**: Load drawer content efficiently, especially for large datasets
- **Memory Management**: Clean up resources when drawers are closed

### Content Strategy
- **Prioritized Content**: Place most important items at the top
- **Search and Filter**: Provide search/filter for long lists of items
- **Action Grouping**: Group related actions together
- **Progressive Disclosure**: Use nested navigation for complex hierarchies

## Accessibility Considerations

- Implements proper modal behavior with focus trapping when `modal={true}`
- Supports keyboard navigation including Escape to close
- Provides appropriate ARIA attributes and roles
- Maintains focus management when opening/closing
- Supports screen reader announcements for state changes
- Ensures adequate color contrast and touch targets

## Related Components

- **SafNavigation**: Navigation component often used within drawers
- **SafNavigationItem**: Individual navigation items
- **SafModal**: Modal dialog component
- **SafSidebar**: Fixed sidebar component
- **SafOverlay**: Backdrop overlay component
- **SafIconButton**: Button for drawer triggers

## Notes

- SafDrawer automatically handles z-index and stacking context
- The component supports both controlled and uncontrolled usage patterns
- Swipe gestures work on both mouse and touch devices
- Backdrop behavior can be customized or disabled entirely
- The component integrates with routing for navigation use cases
- Animation performance is optimized using CSS transforms
- The drawer content can be kept mounted for faster subsequent opens
- Different variants (overlay, push, persistent) affect page layout differently
