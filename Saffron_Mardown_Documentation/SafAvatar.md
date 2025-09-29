# SafAvatar Component

The **SafAvatar** component represents a user or entity with various display options including initials, images, icons, and colored backgrounds. It supports multiple sizes and provides proper accessibility features.

## Basic Usage

```html
<!-- Avatar with initials -->
<saf-avatar label="John Doe">JD</saf-avatar>

<!-- Avatar with image -->
<saf-avatar 
  appearance="image" 
  img-src="/path/to/profile.jpg" 
  label="John Doe">
</saf-avatar>

<!-- Avatar with icon -->
<saf-avatar appearance="icon" label="Guest User">
  <saf-icon slot="media" icon-name="user"></saf-icon>
</saf-avatar>
```

## API Reference

### Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `size` | `'xlarge' \| 'large' \| 'medium' \| 'small'` | `'large'` | Size of the avatar |
| `appearance` | `AvatarAppearance` | `'neutral'` | Visual style and color of the avatar |
| `img-src` | `string` | - | Image source URL (when appearance is 'image' or 'image-light') |
| `label` | `string` | - | Accessible label describing the avatar |
| `presentation` | `boolean` | `false` | Whether avatar is decorative only |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `size` | `AvatarSize` | `'large'` | Current size setting |
| `appearance` | `AvatarAppearance` | `'neutral'` | Current appearance setting |
| `imgSrc` | `string` | - | Current image source |
| `label` | `string` | - | Current accessible label |
| `presentation` | `boolean` | `false` | Current presentation mode |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Avatar content (typically initials or name) |
| `media` | Media content such as images or icons |
| `badge` | Status badge or indicator overlay |

### CSS Parts

| Part | Description |
|------|-------------|
| `backplate` | Main avatar container |
| `content` | Default slot content area |

## Size Options

| Size | Description | Typical Use Case |
|------|-------------|------------------|
| `'xlarge'` | Extra large avatar | Profile pages, hero sections |
| `'large'` | Large avatar | Card headers, detailed views |
| `'medium'` | Medium avatar | Lists, moderate detail contexts |
| `'small'` | Small avatar | Compact lists, comments, mentions |

## Appearance Options

### Color Appearances

| Appearance | Description | Light Variant |
|------------|-------------|---------------|
| `'neutral'` | Default neutral color | `'neutral-light'` |
| `'blue'` | Blue background | `'blue-light'` |
| `'gray'` | Gray background | `'gray-light'` |
| `'green'` | Green background | `'green-light'` |
| `'red'` | Red background | `'red-light'` |
| `'hue-2'` | Alternative hue | `'hue-2-light'` |

### Special Appearances

| Appearance | Description | Light Variant |
|------------|-------------|---------------|
| `'icon'` | For icon-based avatars | `'icon-light'` |
| `'image'` | For photo avatars | `'image-light'` |

### Deprecated

| Appearance | Status | Replacement |
|------------|--------|-------------|
| `'purple'` | Deprecated | Use `'hue-2'` |
| `'purple-light'` | Deprecated | Use `'hue-2-light'` |

## Comprehensive Examples

### Different Sizes

```html
<div class="avatar-sizes">
  <h3>Avatar Sizes</h3>
  <div class="size-examples">
    <div class="size-item">
      <saf-avatar size="small" label="Small Avatar">SM</saf-avatar>
      <span>Small</span>
    </div>
    <div class="size-item">
      <saf-avatar size="medium" label="Medium Avatar">MD</saf-avatar>
      <span>Medium</span>
    </div>
    <div class="size-item">
      <saf-avatar size="large" label="Large Avatar">LG</saf-avatar>
      <span>Large</span>
    </div>
    <div class="size-item">
      <saf-avatar size="xlarge" label="Extra Large Avatar">XL</saf-avatar>
      <span>Extra Large</span>
    </div>
  </div>
</div>

<style>
.avatar-sizes {
  padding: 2rem;
}

.size-examples {
  display: flex;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.size-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.size-item span {
  font-size: 12px;
  color: #666;
}
</style>
```

### Color Appearances

```html
<div class="avatar-colors">
  <h3>Color Appearances</h3>
  <div class="color-grid">
    <div class="color-section">
      <h4>Standard Colors</h4>
      <div class="color-examples">
        <div class="color-item">
          <saf-avatar appearance="neutral" label="Neutral User">NU</saf-avatar>
          <span>Neutral</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="blue" label="Blue User">BU</saf-avatar>
          <span>Blue</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="gray" label="Gray User">GU</saf-avatar>
          <span>Gray</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="green" label="Green User">GU</saf-avatar>
          <span>Green</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="red" label="Red User">RU</saf-avatar>
          <span>Red</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="hue-2" label="Hue 2 User">H2</saf-avatar>
          <span>Hue 2</span>
        </div>
      </div>
    </div>

    <div class="color-section">
      <h4>Light Variants</h4>
      <div class="color-examples">
        <div class="color-item">
          <saf-avatar appearance="neutral-light" label="Neutral Light User">NL</saf-avatar>
          <span>Neutral Light</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="blue-light" label="Blue Light User">BL</saf-avatar>
          <span>Blue Light</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="gray-light" label="Gray Light User">GL</saf-avatar>
          <span>Gray Light</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="green-light" label="Green Light User">GL</saf-avatar>
          <span>Green Light</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="red-light" label="Red Light User">RL</saf-avatar>
          <span>Red Light</span>
        </div>
        <div class="color-item">
          <saf-avatar appearance="hue-2-light" label="Hue 2 Light User">H2L</saf-avatar>
          <span>Hue 2 Light</span>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
.avatar-colors {
  padding: 2rem;
}

.color-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.color-section h4 {
  margin-bottom: 1rem;
}

.color-examples {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
  gap: 1rem;
}

.color-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.color-item span {
  font-size: 11px;
  color: #666;
  text-align: center;
}
</style>
```

### Avatar with Images

```html
<div class="avatar-images">
  <h3>Image Avatars</h3>
  <div class="image-examples">
    <div class="image-item">
      <saf-avatar 
        appearance="image" 
        img-src="https://via.placeholder.com/64/4285f4/ffffff?text=JS" 
        label="Jane Smith"
        size="large">
      </saf-avatar>
      <span>Standard Image</span>
    </div>
    
    <div class="image-item">
      <saf-avatar 
        appearance="image-light" 
        img-src="https://via.placeholder.com/64/34a853/ffffff?text=MJ" 
        label="Mike Johnson"
        size="large">
      </saf-avatar>
      <span>Light Image</span>
    </div>
    
    <!-- Fallback when image fails to load -->
    <div class="image-item">
      <saf-avatar 
        appearance="image" 
        img-src="https://invalid-url.jpg" 
        label="Sarah Wilson"
        size="large">
        SW
      </saf-avatar>
      <span>Fallback to Initials</span>
    </div>
  </div>
</div>

<style>
.avatar-images {
  padding: 2rem;
}

.image-examples {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.image-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.image-item span {
  font-size: 12px;
  color: #666;
  text-align: center;
}
</style>
```

### Avatar with Icons

```html
<div class="avatar-icons">
  <h3>Icon Avatars</h3>
  <div class="icon-examples">
    <div class="icon-item">
      <saf-avatar appearance="icon" label="Guest User" size="large">
        <saf-icon slot="media" icon-name="user" appearance="solid"></saf-icon>
      </saf-avatar>
      <span>User Icon</span>
    </div>
    
    <div class="icon-item">
      <saf-avatar appearance="icon-light" label="Admin User" size="large">
        <saf-icon slot="media" icon-name="user-crown" appearance="solid"></saf-icon>
      </saf-avatar>
      <span>Admin Icon</span>
    </div>
    
    <div class="icon-item">
      <saf-avatar appearance="icon" label="Support Bot" size="large">
        <saf-icon slot="media" icon-name="robot" appearance="solid"></saf-icon>
      </saf-avatar>
      <span>Bot Icon</span>
    </div>
    
    <div class="icon-item">
      <saf-avatar appearance="icon-light" label="Guest" size="large">
        <saf-icon slot="media" icon-name="user-secret" appearance="solid"></saf-icon>
      </saf-avatar>
      <span>Anonymous</span>
    </div>
  </div>
</div>

<style>
.avatar-icons {
  padding: 2rem;
}

.icon-examples {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.icon-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.icon-item span {
  font-size: 12px;
  color: #666;
  text-align: center;
}
</style>
```

### Avatars with Status Badges

```html
<div class="avatar-badges">
  <h3>Avatars with Status Badges</h3>
  <div class="badge-examples">
    <div class="badge-item">
      <saf-avatar appearance="blue" label="Online User" size="large">
        JD
        <saf-badge slot="badge" appearance="success" class="status-badge"></saf-badge>
      </saf-avatar>
      <span>Online</span>
    </div>
    
    <div class="badge-item">
      <saf-avatar appearance="green" label="Away User" size="large">
        SM
        <saf-badge slot="badge" appearance="warning" class="status-badge"></saf-badge>
      </saf-avatar>
      <span>Away</span>
    </div>
    
    <div class="badge-item">
      <saf-avatar appearance="neutral" label="Busy User" size="large">
        TW
        <saf-badge slot="badge" appearance="error" class="status-badge"></saf-badge>
      </saf-avatar>
      <span>Busy</span>
    </div>
    
    <div class="badge-item">
      <saf-avatar appearance="gray" label="Offline User" size="large">
        RB
        <saf-badge slot="badge" appearance="neutral" class="status-badge"></saf-badge>
      </saf-avatar>
      <span>Offline</span>
    </div>
    
    <div class="badge-item">
      <saf-avatar 
        appearance="image" 
        img-src="https://via.placeholder.com/64/ff6b6b/ffffff?text=AL" 
        label="User with Notification" 
        size="large">
        <saf-badge slot="badge" appearance="error" class="notification-badge">5</saf-badge>
      </saf-avatar>
      <span>Notifications</span>
    </div>
  </div>
</div>

<style>
.avatar-badges {
  padding: 2rem;
}

.badge-examples {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.badge-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  position: relative;
}

.badge-item span {
  font-size: 12px;
  color: #666;
  text-align: center;
}

.status-badge {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid white;
}

.notification-badge {
  min-width: 20px;
  height: 20px;
  border-radius: 10px;
  border: 2px solid white;
  font-size: 10px;
  font-weight: bold;
}
</style>
```

### Avatar Groups and Lists

```html
<div class="avatar-groups">
  <h3>Avatar in Lists</h3>
  
  <!-- User list -->
  <div class="user-list">
    <div class="user-item">
      <saf-avatar appearance="blue" label="John Doe" size="medium">JD</saf-avatar>
      <div class="user-info">
        <h4>John Doe</h4>
        <p>Software Engineer</p>
        <span class="status online">Online</span>
      </div>
      <div class="user-actions">
        <button class="action-btn">Message</button>
        <button class="action-btn secondary">View Profile</button>
      </div>
    </div>
    
    <div class="user-item">
      <saf-avatar 
        appearance="image" 
        img-src="https://via.placeholder.com/48/28a745/ffffff?text=SM" 
        label="Sarah Miller" 
        size="medium">
      </saf-avatar>
      <div class="user-info">
        <h4>Sarah Miller</h4>
        <p>Product Designer</p>
        <span class="status away">Away</span>
      </div>
      <div class="user-actions">
        <button class="action-btn">Message</button>
        <button class="action-btn secondary">View Profile</button>
      </div>
    </div>
    
    <div class="user-item">
      <saf-avatar appearance="green" label="Mike Johnson" size="medium">
        MJ
        <saf-badge slot="badge" appearance="error" class="notification-count">3</saf-badge>
      </saf-avatar>
      <div class="user-info">
        <h4>Mike Johnson</h4>
        <p>Project Manager</p>
        <span class="status busy">Busy</span>
      </div>
      <div class="user-actions">
        <button class="action-btn">Message</button>
        <button class="action-btn secondary">View Profile</button>
      </div>
    </div>
  </div>
  
  <!-- Avatar stack -->
  <div class="avatar-stack-section">
    <h4>Avatar Stack</h4>
    <div class="avatar-stack">
      <saf-avatar appearance="blue" label="User 1" size="small">U1</saf-avatar>
      <saf-avatar appearance="green" label="User 2" size="small">U2</saf-avatar>
      <saf-avatar appearance="red" label="User 3" size="small">U3</saf-avatar>
      <saf-avatar appearance="neutral" label="User 4" size="small">U4</saf-avatar>
      <div class="more-count">+5</div>
    </div>
  </div>
</div>

<style>
.avatar-groups {
  padding: 2rem;
}

.user-list {
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 2rem;
}

.user-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border-bottom: 1px solid #f0f0f0;
}

.user-item:last-child {
  border-bottom: none;
}

.user-info {
  flex: 1;
}

.user-info h4 {
  margin: 0 0 0.25rem 0;
  font-size: 16px;
}

.user-info p {
  margin: 0 0 0.25rem 0;
  color: #666;
  font-size: 14px;
}

.status {
  font-size: 12px;
  padding: 2px 8px;
  border-radius: 12px;
  text-transform: uppercase;
  font-weight: 500;
}

.status.online {
  background: #d4edda;
  color: #155724;
}

.status.away {
  background: #fff3cd;
  color: #856404;
}

.status.busy {
  background: #f8d7da;
  color: #721c24;
}

.user-actions {
  display: flex;
  gap: 0.5rem;
}

.action-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #007acc;
  background: #007acc;
  color: white;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
}

.action-btn.secondary {
  background: transparent;
  color: #007acc;
}

.action-btn:hover {
  background: #005a9e;
}

.action-btn.secondary:hover {
  background: #f0f8ff;
}

.avatar-stack-section {
  margin-top: 2rem;
}

.avatar-stack {
  display: flex;
  align-items: center;
}

.avatar-stack saf-avatar {
  margin-right: -8px;
  border: 2px solid white;
  z-index: 1;
}

.avatar-stack saf-avatar:last-of-type {
  margin-right: 8px;
}

.more-count {
  width: 32px;
  height: 32px;
  background: #f0f0f0;
  border: 2px solid white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 500;
  color: #666;
}

.notification-count {
  min-width: 16px;
  height: 16px;
  border-radius: 8px;
  border: 2px solid white;
  font-size: 10px;
  font-weight: bold;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React, { useState } from 'react';

interface AvatarProps {
  size?: 'small' | 'medium' | 'large' | 'xlarge';
  appearance?: string;
  imgSrc?: string;
  label: string;
  presentation?: boolean;
  children?: React.ReactNode;
  badge?: React.ReactNode;
  onClick?: () => void;
}

const SafAvatarComponent: React.FC<AvatarProps> = ({
  size = 'large',
  appearance = 'neutral',
  imgSrc,
  label,
  presentation = false,
  children,
  badge,
  onClick
}) => {
  return (
    <saf-avatar
      size={size}
      appearance={appearance}
      img-src={imgSrc}
      label={label}
      presentation={presentation}
      onClick={onClick}
    >
      {children}
      {badge && <div slot="badge">{badge}</div>}
    </saf-avatar>
  );
};

// User Card Component
interface UserCardProps {
  user: {
    id: string;
    name: string;
    email: string;
    avatar?: string;
    status: 'online' | 'away' | 'busy' | 'offline';
    role: string;
  };
}

const UserCard: React.FC<UserCardProps> = ({ user }) => {
  const [showDetails, setShowDetails] = useState(false);
  
  const getInitials = (name: string) => {
    return name
      .split(' ')
      .map(n => n[0])
      .join('')
      .toUpperCase();
  };
  
  const getAppearanceFromStatus = (status: string) => {
    switch (status) {
      case 'online': return 'green';
      case 'away': return 'neutral';
      case 'busy': return 'red';
      default: return 'gray';
    }
  };
  
  const statusBadge = (
    <div 
      className={`status-indicator ${user.status}`}
      aria-label={`Status: ${user.status}`}
    />
  );

  return (
    <div className="user-card">
      <SafAvatarComponent
        size="large"
        appearance={user.avatar ? 'image' : getAppearanceFromStatus(user.status)}
        imgSrc={user.avatar}
        label={user.name}
        badge={statusBadge}
        onClick={() => setShowDetails(!showDetails)}
      >
        {!user.avatar && getInitials(user.name)}
      </SafAvatarComponent>
      
      <div className="user-details">
        <h3>{user.name}</h3>
        <p>{user.email}</p>
        <span className="role">{user.role}</span>
        
        {showDetails && (
          <div className="additional-info">
            <p>Status: {user.status}</p>
            <button onClick={() => console.log('Message user')}>
              Send Message
            </button>
          </div>
        )}
      </div>
    </div>
  );
};

// Avatar Group Component
interface AvatarGroupProps {
  users: Array<{
    id: string;
    name: string;
    avatar?: string;
  }>;
  maxVisible?: number;
  size?: 'small' | 'medium' | 'large';
}

const AvatarGroup: React.FC<AvatarGroupProps> = ({
  users,
  maxVisible = 4,
  size = 'medium'
}) => {
  const visibleUsers = users.slice(0, maxVisible);
  const hiddenCount = users.length - maxVisible;
  
  return (
    <div className="avatar-group">
      {visibleUsers.map((user, index) => (
        <SafAvatarComponent
          key={user.id}
          size={size}
          appearance={user.avatar ? 'image' : 'neutral'}
          imgSrc={user.avatar}
          label={user.name}
          style={{ zIndex: visibleUsers.length - index }}
        >
          {!user.avatar && user.name.split(' ').map(n => n[0]).join('')}
        </SafAvatarComponent>
      ))}
      
      {hiddenCount > 0 && (
        <div className={`more-indicator size-${size}`}>
          +{hiddenCount}
        </div>
      )}
    </div>
  );
};
```

### Angular Example

```typescript
// avatar.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-saf-avatar',
  template: `
    <saf-avatar
      [attr.size]="size"
      [attr.appearance]="appearance"
      [attr.img-src]="imgSrc"
      [attr.label]="label"
      [attr.presentation]="presentation"
      [class]="className"
      (click)="handleClick()"
    >
      <ng-content></ng-content>
      <ng-content select="[slot=badge]" slot="badge"></ng-content>
      <ng-content select="[slot=media]" slot="media"></ng-content>
    </saf-avatar>
  `
})
export class SafAvatarComponent {
  @Input() size: 'small' | 'medium' | 'large' | 'xlarge' = 'large';
  @Input() appearance: string = 'neutral';
  @Input() imgSrc?: string;
  @Input() label: string = '';
  @Input() presentation: boolean = false;
  @Input() className?: string;
  @Input() clickable: boolean = false;

  handleClick() {
    if (this.clickable) {
      // Emit click event or handle click logic
    }
  }
}

// Usage in component template
/*
<app-saf-avatar
  size="large"
  appearance="blue"
  label="John Doe"
  [clickable]="true">
  JD
  <div slot="badge" class="status-badge online"></div>
</app-saf-avatar>

<app-saf-avatar
  size="medium"
  appearance="image"
  imgSrc="/path/to/avatar.jpg"
  label="Jane Smith">
</app-saf-avatar>
*/
```

### Vue Example

```vue
<template>
  <saf-avatar
    :size="size"
    :appearance="appearance"
    :img-src="imgSrc"
    :label="label"
    :presentation="presentation"
    :class="className"
    @click="handleClick"
  >
    <slot></slot>
    <template #badge>
      <slot name="badge"></slot>
    </template>
    <template #media>
      <slot name="media"></slot>
    </template>
  </saf-avatar>
</template>

<script>
export default {
  name: 'SafAvatarComponent',
  props: {
    size: {
      type: String,
      default: 'large',
      validator: value => ['small', 'medium', 'large', 'xlarge'].includes(value)
    },
    appearance: {
      type: String,
      default: 'neutral'
    },
    imgSrc: String,
    label: {
      type: String,
      required: true
    },
    presentation: {
      type: Boolean,
      default: false
    },
    className: String,
    clickable: {
      type: Boolean,
      default: false
    }
  },
  emits: ['click'],
  methods: {
    handleClick() {
      if (this.clickable) {
        this.$emit('click');
      }
    }
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <div class="avatar-examples">
    <SafAvatarComponent
      size="large"
      appearance="blue"
      label="John Doe"
      :clickable="true"
      @click="handleAvatarClick"
    >
      JD
      <div slot="badge" class="status-online"></div>
    </SafAvatarComponent>
    
    <SafAvatarComponent
      size="medium"
      appearance="image"
      :img-src="user.avatar"
      :label="user.name"
    />
  </div>
</template>
-->
```

## Accessibility Features

### ARIA Support

- **Labels**: Always provide meaningful `label` attribute for screen reader users
- **Presentation Mode**: Use `presentation="true"` for purely decorative avatars
- **Role Semantics**: Automatically applies appropriate ARIA roles based on presentation mode
- **Keyboard Navigation**: Supports focus when used in interactive contexts

### Screen Reader Support

- When `presentation="false"` (default), avatar content is announced to screen readers
- Label attribute provides full context (e.g., "John Doe's profile picture")
- Badge content is included in accessibility tree when relevant
- Proper semantic structure for avatar groups and lists

### Keyboard Navigation

- Avatar can receive focus when used in interactive components
- Tab navigation works naturally in avatar groups
- Badge indicators are accessible via keyboard navigation

## Best Practices

### Content Guidelines
- Always provide meaningful labels that describe the person or entity
- Use initials when images are unavailable (2-3 characters maximum)
- Keep badge content minimal and meaningful
- Consider cultural differences in name formatting

### Visual Design
- Choose appropriate sizes for the context (small for lists, large for profiles)
- Use consistent color schemes throughout your application
- Ensure sufficient contrast for text within avatars
- Test across different screen sizes and densities

### Performance
- Optimize avatar images for appropriate sizes
- Implement lazy loading for large avatar lists
- Use appropriate image formats (WebP, AVIF when supported)
- Consider caching strategies for frequently displayed avatars

### User Experience
- Provide fallbacks for failed image loads
- Use loading states for avatar images
- Consider hover states for interactive avatars
- Implement consistent interaction patterns

### Implementation
- Use semantic markup when avatars represent interactive elements
- Group related avatars logically
- Implement proper error handling for image loading
- Test with various content lengths and character sets

## Related Components

- **SafBadge**: For status indicators and notification counts
- **SafIcon**: For icon-based avatars
- **SafButton**: When avatars are interactive elements
- **SafTooltip**: For additional user information on hover

---

*This documentation covers SafAvatar v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
