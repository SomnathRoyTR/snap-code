# SafBadge - Status Indicator Component

## Overview
`SafBadge` is a compact component for displaying status indicators, labels, counters, and notifications. It supports various appearances, sizes, and can be positioned as attached overlays or standalone elements.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `appearance` | `'error' \| 'error-light' \| 'info' \| 'info-light' \| 'success' \| 'success-light' \| 'warning' \| 'warning-light' \| 'neutral' \| 'neutral-light'` | `'neutral'` | Visual style variant |
| `attached` | `boolean` | `false` | Whether badge is positioned as overlay |
| `counter` | `boolean` | `false` | Whether to render as compact counter |
| `density` | `'compact' \| 'standard'` | `'inherit'` | Size density |

### Slots
| Slot | Description |
|------|-------------|
| (default) | Main badge content |
| `start` | Content before main content |
| `end` | Content after main content |

### CSS Parts
| Part | Description |
|------|-------------|
| `control` | The main badge element |

## Usage Examples

### Basic Status Badges
```typescript
// React
import { SafBadge } from '@saffron/react';

export const StatusBadges = () => {
  return (
    <div style={{ display: 'flex', gap: '8px', flexWrap: 'wrap' }}>
      <SafBadge appearance="success">Active</SafBadge>
      <SafBadge appearance="warning">Pending</SafBadge>
      <SafBadge appearance="error">Error</SafBadge>
      <SafBadge appearance="info">Info</SafBadge>
      <SafBadge appearance="neutral">Draft</SafBadge>
    </div>
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <div style="display: flex; gap: 8px; flex-wrap: wrap;">
      <saf-badge appearance="success">Active</saf-badge>
      <saf-badge appearance="warning">Pending</saf-badge>
      <saf-badge appearance="error">Error</saf-badge>
      <saf-badge appearance="info">Info</saf-badge>
      <saf-badge appearance="neutral">Draft</saf-badge>
    </div>
  `
})
export class StatusBadgesComponent {}
```

### Counter Badges
```typescript
// React
export const CounterBadges = () => {
  const [notifications, setNotifications] = useState(12);
  const [messages, setMessages] = useState(3);
  
  return (
    <div style={{ display: 'flex', gap: '16px', alignItems: 'center' }}>
      <div style={{ position: 'relative', display: 'inline-block' }}>
        <SafButton appearance="ghost">
          <saf-icon icon-name="bell" />
          Notifications
        </SafButton>
        {notifications > 0 && (
          <SafBadge 
            counter 
            attached 
            appearance="error"
            style={{ 
              position: 'absolute', 
              top: '-8px', 
              right: '-8px' 
            }}
          >
            {notifications > 99 ? '99+' : notifications}
          </SafBadge>
        )}
      </div>
      
      <div style={{ position: 'relative', display: 'inline-block' }}>
        <SafButton appearance="ghost">
          <saf-icon icon-name="message" />
          Messages
        </SafButton>
        {messages > 0 && (
          <SafBadge 
            counter 
            attached 
            appearance="info"
            style={{ 
              position: 'absolute', 
              top: '-8px', 
              right: '-8px' 
            }}
          >
            {messages}
          </SafBadge>
        )}
      </div>
    </div>
  );
};
```

### Feature Status Indicators
```typescript
// React
export const FeatureStatus = () => {
  const features = [
    { name: 'User Authentication', status: 'success', label: 'Complete' },
    { name: 'Payment Processing', status: 'warning', label: 'In Progress' },
    { name: 'Email Integration', status: 'error', label: 'Blocked' },
    { name: 'Mobile App', status: 'info', label: 'Planning' },
    { name: 'Analytics', status: 'neutral', label: 'Not Started' }
  ];
  
  return (
    <div>
      <h3>Project Status</h3>
      <div style={{ display: 'flex', flexDirection: 'column', gap: '12px' }}>
        {features.map(feature => (
          <div 
            key={feature.name}
            style={{ 
              display: 'flex', 
              justifyContent: 'space-between', 
              alignItems: 'center',
              padding: '12px',
              border: '1px solid #e0e0e0',
              borderRadius: '8px'
            }}
          >
            <span>{feature.name}</span>
            <SafBadge appearance={feature.status}>
              {feature.label}
            </SafBadge>
          </div>
        ))}
      </div>
    </div>
  );
};
```

### Light Variant Badges
```typescript
// React
export const LightBadges = () => {
  return (
    <div style={{ display: 'flex', gap: '8px', flexWrap: 'wrap' }}>
      <SafBadge appearance="success-light">Published</SafBadge>
      <SafBadge appearance="warning-light">Review</SafBadge>
      <SafBadge appearance="error-light">Failed</SafBadge>
      <SafBadge appearance="info-light">Updated</SafBadge>
      <SafBadge appearance="neutral-light">Archived</SafBadge>
    </div>
  );
};
```

### Badges with Icons
```typescript
// React
export const IconBadges = () => {
  return (
    <div style={{ display: 'flex', gap: '8px', flexWrap: 'wrap' }}>
      <SafBadge appearance="success">
        <saf-icon icon-name="check-circle" slot="start" />
        Verified
      </SafBadge>
      
      <SafBadge appearance="warning">
        <saf-icon icon-name="alert-triangle" slot="start" />
        Warning
      </SafBadge>
      
      <SafBadge appearance="error">
        <saf-icon icon-name="x-circle" slot="start" />
        Error
      </SafBadge>
      
      <SafBadge appearance="info">
        <saf-icon icon-name="info-circle" slot="start" />
        Beta
        <saf-icon icon-name="external-link" slot="end" />
      </SafBadge>
    </div>
  );
};
```

### User Profile Badges
```typescript
// React
export const UserProfileBadges = () => {
  const user = {
    name: 'John Doe',
    role: 'Admin',
    verified: true,
    premium: true,
    lastActive: '2 hours ago'
  };
  
  return (
    <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
      <div style={{ position: 'relative' }}>
        <SafAvatar name={user.name} />
        {user.verified && (
          <SafBadge 
            attached 
            appearance="success" 
            counter
            style={{ 
              position: 'absolute', 
              bottom: '-2px', 
              right: '-2px' 
            }}
          >
            ✓
          </SafBadge>
        )}
      </div>
      
      <div>
        <h4>{user.name}</h4>
        <div style={{ display: 'flex', gap: '8px', alignItems: 'center' }}>
          <SafBadge appearance="info">{user.role}</SafBadge>
          {user.premium && (
            <SafBadge appearance="warning">Premium</SafBadge>
          )}
          <SafBadge appearance="neutral-light">{user.lastActive}</SafBadge>
        </div>
      </div>
    </div>
  );
};
```

### E-commerce Badges
```typescript
// React
export const EcommerceBadges = () => {
  const products = [
    { 
      name: 'Wireless Headphones', 
      price: '$99',
      badges: [
        { text: 'Best Seller', appearance: 'success' },
        { text: '20% Off', appearance: 'error' }
      ]
    },
    { 
      name: 'Smart Watch', 
      price: '$299',
      badges: [
        { text: 'New', appearance: 'info' },
        { text: 'Limited', appearance: 'warning' }
      ]
    }
  ];
  
  return (
    <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fit, minmax(200px, 1fr))', gap: '16px' }}>
      {products.map(product => (
        <div 
          key={product.name}
          style={{ 
            position: 'relative',
            border: '1px solid #e0e0e0',
            borderRadius: '8px',
            padding: '16px'
          }}
        >
          <div style={{ position: 'absolute', top: '8px', right: '8px', display: 'flex', flexDirection: 'column', gap: '4px' }}>
            {product.badges.map((badge, index) => (
              <SafBadge key={index} appearance={badge.appearance} counter>
                {badge.text}
              </SafBadge>
            ))}
          </div>
          
          <h4 style={{ marginBottom: '8px' }}>{product.name}</h4>
          <p style={{ fontSize: '1.2rem', fontWeight: 'bold', color: '#007acc' }}>
            {product.price}
          </p>
        </div>
      ))}
    </div>
  );
};
```

### Task Management Badges
```typescript
// React
export const TaskBadges = () => {
  const tasks = [
    { 
      id: 1, 
      title: 'Update user interface',
      priority: 'high',
      status: 'in-progress',
      assignee: 'John'
    },
    { 
      id: 2, 
      title: 'Fix login bug',
      priority: 'critical',
      status: 'todo',
      assignee: 'Sarah'
    },
    { 
      id: 3, 
      title: 'Write documentation',
      priority: 'low',
      status: 'done',
      assignee: 'Mike'
    }
  ];
  
  const getPriorityAppearance = (priority: string) => {
    switch (priority) {
      case 'critical': return 'error';
      case 'high': return 'warning';
      case 'low': return 'neutral';
      default: return 'info';
    }
  };
  
  const getStatusAppearance = (status: string) => {
    switch (status) {
      case 'done': return 'success';
      case 'in-progress': return 'info';
      default: return 'neutral-light';
    }
  };
  
  return (
    <div>
      <h3>Task Board</h3>
      <div style={{ display: 'flex', flexDirection: 'column', gap: '12px' }}>
        {tasks.map(task => (
          <div 
            key={task.id}
            style={{ 
              display: 'flex',
              justifyContent: 'space-between',
              alignItems: 'center',
              padding: '12px',
              border: '1px solid #e0e0e0',
              borderRadius: '8px'
            }}
          >
            <div style={{ flex: 1 }}>
              <h4 style={{ margin: '0 0 8px 0' }}>{task.title}</h4>
              <div style={{ display: 'flex', gap: '8px' }}>
                <SafBadge appearance={getPriorityAppearance(task.priority)}>
                  {task.priority}
                </SafBadge>
                <SafBadge appearance={getStatusAppearance(task.status)}>
                  {task.status.replace('-', ' ')}
                </SafBadge>
                <SafBadge appearance="neutral-light">
                  {task.assignee}
                </SafBadge>
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};
```

### Interactive Notification Badge
```typescript
// React
export const NotificationBadge = () => {
  const [notifications, setNotifications] = useState([
    { id: 1, text: 'New message received', type: 'info' },
    { id: 2, text: 'Payment successful', type: 'success' },
    { id: 3, text: 'Server error detected', type: 'error' }
  ]);
  
  const clearNotifications = () => setNotifications([]);
  const removeNotification = (id: number) => {
    setNotifications(prev => prev.filter(n => n.id !== id));
  };
  
  return (
    <div style={{ position: 'relative', display: 'inline-block' }}>
      <SafButton appearance="ghost">
        <saf-icon icon-name="bell" />
        Notifications
      </SafButton>
      
      {notifications.length > 0 && (
        <SafBadge 
          counter 
          attached 
          appearance="error"
          style={{ 
            position: 'absolute', 
            top: '-8px', 
            right: '-8px',
            cursor: 'pointer'
          }}
          onClick={clearNotifications}
          title="Click to clear all notifications"
        >
          {notifications.length}
        </SafBadge>
      )}
      
      {notifications.length > 0 && (
        <div style={{ 
          position: 'absolute',
          top: '100%',
          right: '0',
          marginTop: '8px',
          width: '300px',
          background: 'white',
          border: '1px solid #e0e0e0',
          borderRadius: '8px',
          boxShadow: '0 4px 12px rgba(0,0,0,0.1)',
          zIndex: 1000
        }}>
          <div style={{ padding: '12px', borderBottom: '1px solid #e0e0e0' }}>
            <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
              <h4>Notifications</h4>
              <SafButton appearance="ghost" onClick={clearNotifications}>
                Clear All
              </SafButton>
            </div>
          </div>
          
          {notifications.map(notification => (
            <div 
              key={notification.id}
              style={{ 
                display: 'flex',
                justifyContent: 'space-between',
                alignItems: 'center',
                padding: '12px',
                borderBottom: '1px solid #f0f0f0'
              }}
            >
              <span>{notification.text}</span>
              <div style={{ display: 'flex', gap: '8px', alignItems: 'center' }}>
                <SafBadge appearance={notification.type} counter>
                  {notification.type}
                </SafBadge>
                <SafButton 
                  appearance="ghost" 
                  onClick={() => removeNotification(notification.id)}
                >
                  ×
                </SafButton>
              </div>
            </div>
          ))}
        </div>
      )}
    </div>
  );
};
```

## Accessibility Features

- **Semantic Meaning**: Conveys status and context clearly
- **High Contrast**: Excellent visibility in high contrast mode
- **Screen Reader Support**: Proper text content for assistive technology
- **Color Independence**: Status communicated through text, not just color
- **Focus Management**: Keyboard accessible when interactive

## Best Practices

1. **Clear Text**: Use concise, meaningful labels
2. **Consistent Colors**: Use appearance variants consistently across app
3. **Icon Support**: Combine with icons for better comprehension
4. **Counter Limits**: Show "99+" for counts over 99
5. **Positioning**: Use attached badges carefully to avoid overlap
6. **Accessibility**: Don't rely solely on color for meaning
7. **Size Limits**: Keep text short for optimal appearance

## Advanced Usage

### Custom Badge Appearances
```css
/* Custom badge styling */
saf-badge[appearance="custom"] {
  --badge-background: linear-gradient(45deg, #ff6b6b, #ffa500);
  --badge-color: white;
  --badge-border: none;
}

saf-badge[counter] {
  --badge-min-width: 18px;
  --badge-height: 18px;
  --badge-font-size: 0.75rem;
}
```

### Dynamic Badge Updates
```typescript
// React
export const DynamicBadge = () => {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    const interval = setInterval(() => {
      setCount(prev => (prev + 1) % 100);
    }, 2000);
    
    return () => clearInterval(interval);
  }, []);
  
  return (
    <SafBadge 
      counter 
      appearance={count > 50 ? 'error' : 'info'}
      style={{
        transition: 'all 0.3s ease'
      }}
    >
      {count}
    </SafBadge>
  );
};
```

## Notes

- Supports both standalone and attached (overlay) positioning
- Provides multiple appearance variants for different contexts
- Counter variant optimized for numeric displays
- Integrates well with buttons, avatars, and other components
- Supports start/end slots for icons and additional content
- Maintains accessibility and high contrast support
