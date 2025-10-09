# SafTab Component

## Overview
The `SafTab` component represents an individual tab within a tab container. It provides an interactive tab button that users can click to switch between different content panels. This component is designed to work within `SafTabs` containers and supports various states, icons, and accessibility features for creating tabbed interfaces.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the tab is currently selected |
| `disabled` | `boolean` | `false` | Whether the tab is disabled |
| `id` | `string` | `undefined` | Unique identifier for the tab |
| `tabIndex` | `number` | `undefined` | Tab index for keyboard navigation |
| `closable` | `boolean` | `false` | Whether the tab can be closed |
| `icon` | `string` | `undefined` | Icon name to display in the tab |
| `badge` | `string \| number` | `undefined` | Badge content to display |
| `href` | `string` | `undefined` | If provided, renders the tab as a link |
| `target` | `string` | `undefined` | Link target when href is provided |
| `onClick` | `(event: MouseEvent) => void` | `undefined` | Click event handler |
| `onClose` | `(event: MouseEvent) => void` | `undefined` | Close button click handler |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Focus event handler |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Blur event handler |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Tab label content |

### Events
- `onClick`: Fired when the tab is clicked
- `onClose`: Fired when the close button is clicked
- `onFocus`: Fired when the tab receives focus
- `onBlur`: Fired when the tab loses focus
- `onSelect`: Fired when the tab becomes selected

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the tab is currently selected |
| `disabled` | `boolean` | `false` | Whether the tab is disabled |
| `id` | `string` | `undefined` | Unique identifier for the tab |
| `tabIndex` | `number` | `undefined` | Tab index for keyboard navigation |
| `closable` | `boolean` | `false` | Whether the tab can be closed |
| `icon` | `string` | `undefined` | Icon name to display in the tab |
| `badge` | `string \| number` | `undefined` | Badge content to display |
| `href` | `string` | `undefined` | If provided, renders the tab as a link |
| `target` | `string` | `undefined` | Link target when href is provided |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(click)` | `EventEmitter<MouseEvent>` | Emitted when the tab is clicked |
| `(close)` | `EventEmitter<MouseEvent>` | Emitted when the close button is clicked |
| `(focus)` | `EventEmitter<FocusEvent>` | Emitted when the tab receives focus |
| `(blur)` | `EventEmitter<FocusEvent>` | Emitted when the tab loses focus |
| `(tabSelect)` | `EventEmitter<string>` | Emitted when the tab becomes selected |

### Content Projection
- **Default slot**: Tab label content
- **`start` slot**: Content at the start of the tab (e.g., icons)
- **`end` slot**: Content at the end of the tab (e.g., badges, close button)

## Usage Examples

### Basic Tabs

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel } from '@saffron/core-components';

function BasicTabExample() {
  const [selectedTab, setSelectedTab] = useState('tab1');

  return (
    <div>
      <SafTabs>
        <SafTab 
          id="tab1"
          selected={selectedTab === 'tab1'}
          onClick={() => setSelectedTab('tab1')}
        >
          Overview
        </SafTab>
        <SafTab 
          id="tab2"
          selected={selectedTab === 'tab2'}
          onClick={() => setSelectedTab('tab2')}
        >
          Details
        </SafTab>
        <SafTab 
          id="tab3"
          selected={selectedTab === 'tab3'}
          onClick={() => setSelectedTab('tab3')}
        >
          Settings
        </SafTab>
        <SafTab disabled>
          Coming Soon
        </SafTab>
      </SafTabs>
      
      <SafTabPanel id="tab1" selected={selectedTab === 'tab1'}>
        <h3>Overview Content</h3>
        <p>This is the overview panel content.</p>
      </SafTabPanel>
      
      <SafTabPanel id="tab2" selected={selectedTab === 'tab2'}>
        <h3>Details Content</h3>
        <p>This is the details panel content.</p>
      </SafTabPanel>
      
      <SafTabPanel id="tab3" selected={selectedTab === 'tab3'}>
        <h3>Settings Content</h3>
        <p>This is the settings panel content.</p>
      </SafTabPanel>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-tabs',
  template: `
    <div>
      <saf-tabs>
        <saf-tab 
          id="tab1"
          [selected]="selectedTab === 'tab1'"
          (click)="setSelectedTab('tab1')"
        >
          Overview
        </saf-tab>
        <saf-tab 
          id="tab2"
          [selected]="selectedTab === 'tab2'"
          (click)="setSelectedTab('tab2')"
        >
          Details
        </saf-tab>
        <saf-tab 
          id="tab3"
          [selected]="selectedTab === 'tab3'"
          (click)="setSelectedTab('tab3')"
        >
          Settings
        </saf-tab>
        <saf-tab disabled>
          Coming Soon
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel id="tab1" [selected]="selectedTab === 'tab1'">
        <h3>Overview Content</h3>
        <p>This is the overview panel content.</p>
      </saf-tab-panel>
      
      <saf-tab-panel id="tab2" [selected]="selectedTab === 'tab2'">
        <h3>Details Content</h3>
        <p>This is the details panel content.</p>
      </saf-tab-panel>
      
      <saf-tab-panel id="tab3" [selected]="selectedTab === 'tab3'">
        <h3>Settings Content</h3>
        <p>This is the settings panel content.</p>
      </saf-tab-panel>
    </div>
  `
})
export class BasicTabsComponent {
  selectedTab = 'tab1';

  setSelectedTab(tabId: string) {
    this.selectedTab = tabId;
  }
}
```

### Tabs with Icons and Badges

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel, SafIcon, SafBadge } from '@saffron/core-components';
import { useState } from 'react';

function IconTabExample() {
  const [selectedTab, setSelectedTab] = useState('dashboard');

  return (
    <div>
      <SafTabs>
        <SafTab 
          id="dashboard"
          icon="dashboard"
          selected={selectedTab === 'dashboard'}
          onClick={() => setSelectedTab('dashboard')}
        >
          Dashboard
        </SafTab>
        
        <SafTab 
          id="messages"
          icon="mail"
          badge="3"
          selected={selectedTab === 'messages'}
          onClick={() => setSelectedTab('messages')}
        >
          Messages
        </SafTab>
        
        <SafTab 
          id="notifications"
          icon="bell"
          badge="12"
          selected={selectedTab === 'notifications'}
          onClick={() => setSelectedTab('notifications')}
        >
          <SafIcon slot="start" name="bell" />
          Notifications
          <SafBadge slot="end" variant="error" size="small">12</SafBadge>
        </SafTab>
        
        <SafTab 
          id="profile"
          icon="user"
          selected={selectedTab === 'profile'}
          onClick={() => setSelectedTab('profile')}
        >
          Profile
        </SafTab>
      </SafTabs>
      
      <SafTabPanel id="dashboard" selected={selectedTab === 'dashboard'}>
        <h3>Dashboard</h3>
        <p>Welcome to your dashboard overview.</p>
      </SafTabPanel>
      
      <SafTabPanel id="messages" selected={selectedTab === 'messages'}>
        <h3>Messages</h3>
        <p>You have 3 unread messages.</p>
      </SafTabPanel>
      
      <SafTabPanel id="notifications" selected={selectedTab === 'notifications'}>
        <h3>Notifications</h3>
        <p>You have 12 new notifications.</p>
      </SafTabPanel>
      
      <SafTabPanel id="profile" selected={selectedTab === 'profile'}>
        <h3>Profile</h3>
        <p>Manage your profile settings.</p>
      </SafTabPanel>
    </div>
  );
}
```

#### Angular
```html
<div>
  <saf-tabs>
    <saf-tab 
      id="dashboard"
      icon="dashboard"
      [selected]="selectedTab === 'dashboard'"
      (click)="setSelectedTab('dashboard')"
    >
      Dashboard
    </saf-tab>
    
    <saf-tab 
      id="messages"
      icon="mail"
      badge="3"
      [selected]="selectedTab === 'messages'"
      (click)="setSelectedTab('messages')"
    >
      Messages
    </saf-tab>
    
    <saf-tab 
      id="notifications"
      icon="bell"
      [selected]="selectedTab === 'notifications'"
      (click)="setSelectedTab('notifications')"
    >
      <saf-icon slot="start" name="bell"></saf-icon>
      Notifications
      <saf-badge slot="end" variant="error" size="small">12</saf-badge>
    </saf-tab>
    
    <saf-tab 
      id="profile"
      icon="user"
      [selected]="selectedTab === 'profile'"
      (click)="setSelectedTab('profile')"
    >
      Profile
    </saf-tab>
  </saf-tabs>
  
  <saf-tab-panel id="dashboard" [selected]="selectedTab === 'dashboard'">
    <h3>Dashboard</h3>
    <p>Welcome to your dashboard overview.</p>
  </saf-tab-panel>
  
  <saf-tab-panel id="messages" [selected]="selectedTab === 'messages'">
    <h3>Messages</h3>
    <p>You have 3 unread messages.</p>
  </saf-tab-panel>
  
  <saf-tab-panel id="notifications" [selected]="selectedTab === 'notifications'">
    <h3>Notifications</h3>
    <p>You have 12 new notifications.</p>
  </saf-tab-panel>
  
  <saf-tab-panel id="profile" [selected]="selectedTab === 'profile'">
    <h3>Profile</h3>
    <p>Manage your profile settings.</p>
  </saf-tab-panel>
</div>
```

### Closable Tabs

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel } from '@saffron/core-components';
import { useState } from 'react';

function ClosableTabExample() {
  const [tabs, setTabs] = useState([
    { id: 'tab1', title: 'Document 1', content: 'Content of document 1' },
    { id: 'tab2', title: 'Document 2', content: 'Content of document 2' },
    { id: 'tab3', title: 'Document 3', content: 'Content of document 3' }
  ]);
  const [selectedTab, setSelectedTab] = useState('tab1');

  const closeTab = (tabId) => {
    const newTabs = tabs.filter(tab => tab.id !== tabId);
    setTabs(newTabs);
    
    if (selectedTab === tabId && newTabs.length > 0) {
      setSelectedTab(newTabs[0].id);
    }
  };

  const addTab = () => {
    const newId = `tab${Date.now()}`;
    const newTab = {
      id: newId,
      title: `New Document`,
      content: `Content of new document`
    };
    setTabs([...tabs, newTab]);
    setSelectedTab(newId);
  };

  return (
    <div>
      <SafTabs>
        {tabs.map((tab) => (
          <SafTab
            key={tab.id}
            id={tab.id}
            closable
            selected={selectedTab === tab.id}
            onClick={() => setSelectedTab(tab.id)}
            onClose={() => closeTab(tab.id)}
          >
            {tab.title}
          </SafTab>
        ))}
        <button onClick={addTab}>+ Add Tab</button>
      </SafTabs>
      
      {tabs.map((tab) => (
        <SafTabPanel 
          key={tab.id}
          id={tab.id}
          selected={selectedTab === tab.id}
        >
          <h3>{tab.title}</h3>
          <p>{tab.content}</p>
        </SafTabPanel>
      ))}
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface TabData {
  id: string;
  title: string;
  content: string;
}

@Component({
  selector: 'app-closable-tabs',
  template: `
    <div>
      <saf-tabs>
        <saf-tab
          *ngFor="let tab of tabs"
          [id]="tab.id"
          [closable]="true"
          [selected]="selectedTab === tab.id"
          (click)="setSelectedTab(tab.id)"
          (close)="closeTab(tab.id)"
        >
          {{tab.title}}
        </saf-tab>
        <button (click)="addTab()">+ Add Tab</button>
      </saf-tabs>
      
      <saf-tab-panel 
        *ngFor="let tab of tabs"
        [id]="tab.id"
        [selected]="selectedTab === tab.id"
      >
        <h3>{{tab.title}}</h3>
        <p>{{tab.content}}</p>
      </saf-tab-panel>
    </div>
  `
})
export class ClosableTabsComponent {
  tabs: TabData[] = [
    { id: 'tab1', title: 'Document 1', content: 'Content of document 1' },
    { id: 'tab2', title: 'Document 2', content: 'Content of document 2' },
    { id: 'tab3', title: 'Document 3', content: 'Content of document 3' }
  ];
  selectedTab = 'tab1';

  setSelectedTab(tabId: string) {
    this.selectedTab = tabId;
  }

  closeTab(tabId: string) {
    this.tabs = this.tabs.filter(tab => tab.id !== tabId);
    
    if (this.selectedTab === tabId && this.tabs.length > 0) {
      this.selectedTab = this.tabs[0].id;
    }
  }

  addTab() {
    const newId = `tab${Date.now()}`;
    const newTab: TabData = {
      id: newId,
      title: 'New Document',
      content: 'Content of new document'
    };
    this.tabs.push(newTab);
    this.selectedTab = newId;
  }
}
```

### Link Tabs (Navigation)

#### React
```jsx
import { SafTabs, SafTab } from '@saffron/core-components';

function NavigationTabExample() {
  const currentPath = window.location.pathname;

  return (
    <SafTabs role="tablist" aria-label="Main navigation">
      <SafTab 
        href="/dashboard"
        selected={currentPath === '/dashboard'}
        icon="dashboard"
      >
        Dashboard
      </SafTab>
      
      <SafTab 
        href="/reports"
        selected={currentPath === '/reports'}
        icon="chart"
      >
        Reports
      </SafTab>
      
      <SafTab 
        href="/settings"
        selected={currentPath === '/settings'}
        icon="settings"
      >
        Settings
      </SafTab>
      
      <SafTab 
        href="/help"
        target="_blank"
        icon="help"
      >
        Help
      </SafTab>
    </SafTabs>
  );
}
```

#### Angular
```html
<saf-tabs role="tablist" aria-label="Main navigation">
  <saf-tab 
    href="/dashboard"
    [selected]="currentPath === '/dashboard'"
    icon="dashboard"
  >
    Dashboard
  </saf-tab>
  
  <saf-tab 
    href="/reports"
    [selected]="currentPath === '/reports'"
    icon="chart"
  >
    Reports
  </saf-tab>
  
  <saf-tab 
    href="/settings"
    [selected]="currentPath === '/settings'"
    icon="settings"
  >
    Settings
  </saf-tab>
  
  <saf-tab 
    href="/help"
    target="_blank"
    icon="help"
  >
    Help
  </saf-tab>
</saf-tabs>
```

### Dynamic Tabs with Data

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel, SafSpinner } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicTabExample() {
  const [tabs, setTabs] = useState([]);
  const [selectedTab, setSelectedTab] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      const tabData = [
        { 
          id: 'summary', 
          title: 'Summary', 
          icon: 'chart', 
          badge: null,
          content: 'Summary information and key metrics.'
        },
        { 
          id: 'details', 
          title: 'Details', 
          icon: 'list', 
          badge: null,
          content: 'Detailed information and data tables.'
        },
        { 
          id: 'activity', 
          title: 'Activity', 
          icon: 'clock', 
          badge: '5',
          content: 'Recent activity and audit logs.'
        },
        { 
          id: 'comments', 
          title: 'Comments', 
          icon: 'comment', 
          badge: '2',
          content: 'User comments and discussions.'
        }
      ];
      setTabs(tabData);
      setSelectedTab('summary');
      setLoading(false);
    }, 1000);
  }, []);

  if (loading) {
    return <SafSpinner size="medium" />;
  }

  return (
    <div>
      <SafTabs>
        {tabs.map((tab) => (
          <SafTab
            key={tab.id}
            id={tab.id}
            icon={tab.icon}
            badge={tab.badge}
            selected={selectedTab === tab.id}
            onClick={() => setSelectedTab(tab.id)}
          >
            {tab.title}
          </SafTab>
        ))}
      </SafTabs>
      
      {tabs.map((tab) => (
        <SafTabPanel 
          key={tab.id}
          id={tab.id}
          selected={selectedTab === tab.id}
        >
          <h3>{tab.title}</h3>
          <p>{tab.content}</p>
        </SafTabPanel>
      ))}
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component, OnInit } from '@angular/core';

interface TabData {
  id: string;
  title: string;
  icon: string;
  badge: string | null;
  content: string;
}

@Component({
  selector: 'app-dynamic-tabs',
  template: `
    <saf-spinner *ngIf="loading" size="medium"></saf-spinner>
    
    <div *ngIf="!loading">
      <saf-tabs>
        <saf-tab
          *ngFor="let tab of tabs"
          [id]="tab.id"
          [icon]="tab.icon"
          [badge]="tab.badge"
          [selected]="selectedTab === tab.id"
          (click)="setSelectedTab(tab.id)"
        >
          {{tab.title}}
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel 
        *ngFor="let tab of tabs"
        [id]="tab.id"
        [selected]="selectedTab === tab.id"
      >
        <h3>{{tab.title}}</h3>
        <p>{{tab.content}}</p>
      </saf-tab-panel>
    </div>
  `
})
export class DynamicTabsComponent implements OnInit {
  tabs: TabData[] = [];
  selectedTab: string | null = null;
  loading = true;

  ngOnInit() {
    // Simulate API call
    setTimeout(() => {
      this.tabs = [
        { 
          id: 'summary', 
          title: 'Summary', 
          icon: 'chart', 
          badge: null,
          content: 'Summary information and key metrics.'
        },
        { 
          id: 'details', 
          title: 'Details', 
          icon: 'list', 
          badge: null,
          content: 'Detailed information and data tables.'
        },
        { 
          id: 'activity', 
          title: 'Activity', 
          icon: 'clock', 
          badge: '5',
          content: 'Recent activity and audit logs.'
        },
        { 
          id: 'comments', 
          title: 'Comments', 
          icon: 'comment', 
          badge: '2',
          content: 'User comments and discussions.'
        }
      ];
      this.selectedTab = 'summary';
      this.loading = false;
    }, 1000);
  }

  setSelectedTab(tabId: string) {
    this.selectedTab = tabId;
  }
}
```

## Best Practices

1. **Tab Labels**: Use clear, concise labels that describe the content
2. **Icon Usage**: Use meaningful icons that enhance comprehension
3. **Badge Guidelines**: Use badges sparingly for important notifications
4. **Keyboard Navigation**: Implement arrow key navigation between tabs
5. **Close Behavior**: Provide clear visual feedback for closable tabs
6. **Loading States**: Show loading indicators when tab content is being fetched
7. **Responsive Design**: Consider how tabs behave on smaller screens
8. **Selection State**: Ensure the selected tab is clearly indicated

## Accessibility Considerations

- Use proper ARIA attributes (role="tab", aria-selected, aria-controls)
- Support keyboard navigation with arrow keys and Enter/Space
- Provide clear focus indicators
- Ensure sufficient color contrast for all states
- Use semantic markup for tab content
- Announce tab changes to screen readers
- Support high contrast mode

## Related Components

- `SafTabs`: Container component for tab groups
- `SafTabPanel`: Content panels associated with tabs
- `SafIcon`: For tab icons
- `SafBadge`: For notification badges
- `SafButton`: For close buttons in closable tabs
- `SafSpinner`: For loading states

## Notes

- Tabs must be used within `SafTabs` containers
- Each tab should have a corresponding `SafTabPanel`
- The `id` prop is required for proper tab-panel associations
- Use controlled mode for complex tab state management
- Consider performance implications with many tabs
- Closable tabs should handle edge cases (e.g., closing the last tab)
