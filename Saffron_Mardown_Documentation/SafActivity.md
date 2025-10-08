# SafActivity Component

## Overview

SafActivity is a versatile component designed to display activity feeds, timelines, and event streams in applications. It provides a consistent interface for showing chronological events, user actions, system notifications, and workflow progress. The component supports various display formats including list views, timeline layouts, and condensed feeds, making it ideal for dashboards, audit logs, notification centers, and social activity streams.

## React API

### SafActivity

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `activities` | `Activity[]` | Yes | - | Array of activity items to display |
| `layout` | `'list' \| 'timeline' \| 'compact' \| 'card'` | No | `'list'` | Display layout variant |
| `orientation` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Timeline orientation (timeline layout only) |
| `showTimestamps` | `boolean` | No | `true` | Whether to display activity timestamps |
| `showAvatars` | `boolean` | No | `true` | Whether to display user avatars |
| `showIcons` | `boolean` | No | `true` | Whether to display activity type icons |
| `groupBy` | `'none' \| 'date' \| 'user' \| 'type'` | No | `'none'` | How to group activities |
| `sortOrder` | `'asc' \| 'desc'` | No | `'desc'` | Sort order for activities |
| `maxItems` | `number` | No | - | Maximum number of items to display |
| `enableFiltering` | `boolean` | No | `false` | Enable activity type filtering |
| `enableSearch` | `boolean` | No | `false` | Enable activity search |
| `autoRefresh` | `boolean` | No | `false` | Enable automatic refresh |
| `refreshInterval` | `number` | No | `30000` | Auto-refresh interval in milliseconds |
| `virtualized` | `boolean` | No | `false` | Enable virtualization for large datasets |
| `emptyMessage` | `string \| ReactNode` | No | `'No activities to display'` | Message when no activities |
| `loadingState` | `boolean` | No | `false` | Whether component is loading |
| `errorState` | `string \| ReactNode` | No | - | Error message to display |
| `realTimeUpdates` | `boolean` | No | `false` | Enable real-time activity updates |
| `onActivityClick` | `(activity: Activity) => void` | No | - | Callback when activity is clicked |
| `onLoadMore` | `() => void \| Promise<void>` | No | - | Callback for loading more activities |
| `onRefresh` | `() => void \| Promise<void>` | No | - | Callback for manual refresh |
| `onFilter` | `(filters: ActivityFilter) => void` | No | - | Callback when filters change |
| `onSearch` | `(query: string) => void` | No | - | Callback when search query changes |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### Activity Interface

```typescript
interface Activity {
  id: string;
  type: ActivityType;
  title: string;
  description?: string;
  timestamp: Date | string;
  user?: User;
  icon?: string | ReactNode;
  metadata?: { [key: string]: any };
  priority?: 'low' | 'medium' | 'high' | 'urgent';
  category?: string;
  relatedEntity?: {
    id: string;
    type: string;
    name: string;
  };
  actions?: ActivityAction[];
  read?: boolean;
  archived?: boolean;
}

interface User {
  id: string;
  name: string;
  avatar?: string;
  role?: string;
}

interface ActivityAction {
  id: string;
  label: string;
  icon?: string;
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  onClick: (activity: Activity) => void;
}

interface ActivityFilter {
  types?: ActivityType[];
  users?: string[];
  categories?: string[];
  dateRange?: {
    start: Date;
    end: Date;
  };
  priority?: string[];
}

type ActivityType = 
  | 'comment' 
  | 'edit' 
  | 'create' 
  | 'delete' 
  | 'share' 
  | 'approve' 
  | 'reject' 
  | 'assign' 
  | 'status_change' 
  | 'login' 
  | 'logout' 
  | 'upload' 
  | 'download' 
  | 'system' 
  | 'notification'
  | 'custom';
```

## Angular API

### saf-activity

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[activities]` | `Activity[]` | Yes | - | Array of activity items to display |
| `[layout]` | `'list' \| 'timeline' \| 'compact' \| 'card'` | No | `'list'` | Display layout variant |
| `[orientation]` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Timeline orientation (timeline layout only) |
| `[showTimestamps]` | `boolean` | No | `true` | Whether to display activity timestamps |
| `[showAvatars]` | `boolean` | No | `true` | Whether to display user avatars |
| `[showIcons]` | `boolean` | No | `true` | Whether to display activity type icons |
| `[groupBy]` | `'none' \| 'date' \| 'user' \| 'type'` | No | `'none'` | How to group activities |
| `[sortOrder]` | `'asc' \| 'desc'` | No | `'desc'` | Sort order for activities |
| `[maxItems]` | `number` | No | - | Maximum number of items to display |
| `[enableFiltering]` | `boolean` | No | `false` | Enable activity type filtering |
| `[enableSearch]` | `boolean` | No | `false` | Enable activity search |
| `[autoRefresh]` | `boolean` | No | `false` | Enable automatic refresh |
| `[refreshInterval]` | `number` | No | `30000` | Auto-refresh interval in milliseconds |
| `[virtualized]` | `boolean` | No | `false` | Enable virtualization for large datasets |
| `[emptyMessage]` | `string \| TemplateRef` | No | `'No activities to display'` | Message when no activities |
| `[loadingState]` | `boolean` | No | `false` | Whether component is loading |
| `[errorState]` | `string \| TemplateRef` | No | - | Error message to display |
| `[realTimeUpdates]` | `boolean` | No | `false` | Enable real-time activity updates |
| `(activityClick)` | `EventEmitter<Activity>` | No | - | Event when activity is clicked |
| `(loadMore)` | `EventEmitter<void>` | No | - | Event for loading more activities |
| `(refresh)` | `EventEmitter<void>` | No | - | Event for manual refresh |
| `(filter)` | `EventEmitter<ActivityFilter>` | No | - | Event when filters change |
| `(search)` | `EventEmitter<string>` | No | - | Event when search query changes |

## Usage Examples

### Document Activity Timeline

#### React
```jsx
import { SafActivity, SafIcon, SafAvatar } from '@saffron/react';
import { useState, useEffect } from 'react';

const DocumentActivityExample = () => {
  const [activities, setActivities] = useState([]);
  const [loading, setLoading] = useState(false);
  const [filters, setFilters] = useState({});

  // Sample activity data
  const sampleActivities = [
    {
      id: '1',
      type: 'create',
      title: 'Document created',
      description: 'Legal Contract Template v2.1 was created',
      timestamp: new Date('2024-01-15T09:00:00Z'),
      user: {
        id: 'user1',
        name: 'Sarah Johnson',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
        role: 'Legal Counsel'
      },
      priority: 'medium',
      category: 'document',
      relatedEntity: {
        id: 'doc123',
        type: 'document',
        name: 'Legal Contract Template v2.1'
      }
    },
    {
      id: '2',
      type: 'edit',
      title: 'Document updated',
      description: 'Modified clause 3.2 regarding termination conditions',
      timestamp: new Date('2024-01-15T10:30:00Z'),
      user: {
        id: 'user2',
        name: 'Michael Chen',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=michael',
        role: 'Senior Associate'
      },
      priority: 'high',
      category: 'document',
      relatedEntity: {
        id: 'doc123',
        type: 'document',
        name: 'Legal Contract Template v2.1'
      }
    },
    {
      id: '3',
      type: 'comment',
      title: 'Comment added',
      description: 'Please review the liability limitations in section 5.1',
      timestamp: new Date('2024-01-15T11:15:00Z'),
      user: {
        id: 'user3',
        name: 'Emily Rodriguez',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emily',
        role: 'Partner'
      },
      priority: 'urgent',
      category: 'review',
      actions: [
        {
          id: 'reply',
          label: 'Reply',
          icon: 'reply',
          variant: 'outline',
          onClick: (activity) => console.log('Reply to:', activity.id)
        },
        {
          id: 'resolve',
          label: 'Resolve',
          icon: 'check',
          variant: 'primary',
          onClick: (activity) => console.log('Resolve:', activity.id)
        }
      ]
    },
    {
      id: '4',
      type: 'approve',
      title: 'Document approved',
      description: 'Legal review completed and approved for client use',
      timestamp: new Date('2024-01-15T14:20:00Z'),
      user: {
        id: 'user3',
        name: 'Emily Rodriguez',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emily',
        role: 'Partner'
      },
      priority: 'high',
      category: 'approval'
    },
    {
      id: '5',
      type: 'share',
      title: 'Document shared',
      description: 'Shared with Thomson Reuters Legal Team',
      timestamp: new Date('2024-01-15T15:45:00Z'),
      user: {
        id: 'user1',
        name: 'Sarah Johnson',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
        role: 'Legal Counsel'
      },
      priority: 'medium',
      category: 'collaboration'
    }
  ];

  useEffect(() => {
    // Simulate initial data load
    setLoading(true);
    setTimeout(() => {
      setActivities(sampleActivities);
      setLoading(false);
    }, 1000);
  }, []);

  const handleActivityClick = (activity) => {
    console.log('Activity clicked:', activity);
    // Navigate to activity details or perform action
  };

  const handleLoadMore = async () => {
    setLoading(true);
    // Simulate loading more activities
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const newActivities = [
      {
        id: '6',
        type: 'system',
        title: 'Auto-backup completed',
        description: 'Document backed up to secure storage',
        timestamp: new Date('2024-01-14T23:30:00Z'),
        priority: 'low',
        category: 'system'
      }
    ];
    
    setActivities(prev => [...prev, ...newActivities]);
    setLoading(false);
  };

  const handleFilter = (newFilters) => {
    setFilters(newFilters);
    console.log('Filters applied:', newFilters);
    // Apply filtering logic
  };

  const handleSearch = (query) => {
    console.log('Search query:', query);
    // Apply search filtering
  };

  return (
    <div className="document-activity-demo">
      <h2>Document Activity Timeline</h2>
      
      <div className="activity-layouts">
        {/* Timeline Layout */}
        <div className="layout-section">
          <h3>Timeline View</h3>
          <SafActivity
            activities={activities}
            layout="timeline"
            orientation="vertical"
            showTimestamps={true}
            showAvatars={true}
            showIcons={true}
            groupBy="date"
            enableFiltering={true}
            enableSearch={true}
            loadingState={loading}
            onActivityClick={handleActivityClick}
            onLoadMore={handleLoadMore}
            onFilter={handleFilter}
            onSearch={handleSearch}
          />
        </div>

        {/* List Layout */}
        <div className="layout-section">
          <h3>List View</h3>
          <SafActivity
            activities={activities}
            layout="list"
            showTimestamps={true}
            showAvatars={true}
            groupBy="none"
            enableFiltering={true}
            maxItems={10}
            onActivityClick={handleActivityClick}
            onLoadMore={handleLoadMore}
          />
        </div>

        {/* Compact Layout */}
        <div className="layout-section">
          <h3>Compact View</h3>
          <SafActivity
            activities={activities}
            layout="compact"
            showTimestamps={false}
            showAvatars={false}
            showIcons={true}
            maxItems={5}
            onActivityClick={handleActivityClick}
          />
        </div>
      </div>

      {/* Real-time Updates Demo */}
      <div className="realtime-demo">
        <h3>Real-time Activity Feed</h3>
        <SafActivity
          activities={activities}
          layout="card"
          realTimeUpdates={true}
          autoRefresh={true}
          refreshInterval={10000}
          enableFiltering={true}
          enableSearch={true}
          onActivityClick={handleActivityClick}
          onRefresh={() => console.log('Manual refresh triggered')}
        />
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// document-activity.component.ts
import { Component, OnInit } from '@angular/core';

interface Activity {
  id: string;
  type: string;
  title: string;
  description?: string;
  timestamp: Date;
  user?: {
    id: string;
    name: string;
    avatar?: string;
    role?: string;
  };
  priority?: 'low' | 'medium' | 'high' | 'urgent';
  category?: string;
  actions?: {
    id: string;
    label: string;
    icon?: string;
    variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
    onClick: (activity: Activity) => void;
  }[];
}

@Component({
  selector: 'app-document-activity',
  template: `
    <div class="document-activity-demo">
      <h2>Document Activity Timeline</h2>
      
      <div class="activity-layouts">
        <!-- Timeline Layout -->
        <div class="layout-section">
          <h3>Timeline View</h3>
          <saf-activity
            [activities]="activities"
            layout="timeline"
            orientation="vertical"
            [showTimestamps]="true"
            [showAvatars]="true"
            [showIcons]="true"
            groupBy="date"
            [enableFiltering]="true"
            [enableSearch]="true"
            [loadingState]="loading"
            (activityClick)="handleActivityClick($event)"
            (loadMore)="handleLoadMore()"
            (filter)="handleFilter($event)"
            (search)="handleSearch($event)">
          </saf-activity>
        </div>

        <!-- List Layout -->
        <div class="layout-section">
          <h3>List View</h3>
          <saf-activity
            [activities]="activities"
            layout="list"
            [showTimestamps]="true"
            [showAvatars]="true"
            groupBy="none"
            [enableFiltering]="true"
            [maxItems]="10"
            (activityClick)="handleActivityClick($event)"
            (loadMore)="handleLoadMore()">
          </saf-activity>
        </div>

        <!-- Compact Layout -->
        <div class="layout-section">
          <h3>Compact View</h3>
          <saf-activity
            [activities]="activities"
            layout="compact"
            [showTimestamps]="false"
            [showAvatars]="false"
            [showIcons]="true"
            [maxItems]="5"
            (activityClick)="handleActivityClick($event)">
          </saf-activity>
        </div>
      </div>

      <!-- Real-time Updates Demo -->
      <div class="realtime-demo">
        <h3>Real-time Activity Feed</h3>
        <saf-activity
          [activities]="activities"
          layout="card"
          [realTimeUpdates]="true"
          [autoRefresh]="true"
          [refreshInterval]="10000"
          [enableFiltering]="true"
          [enableSearch]="true"
          (activityClick)="handleActivityClick($event)"
          (refresh)="handleRefresh()">
        </saf-activity>
      </div>
    </div>
  `
})
export class DocumentActivityComponent implements OnInit {
  activities: Activity[] = [];
  loading = false;
  filters = {};

  sampleActivities: Activity[] = [
    {
      id: '1',
      type: 'create',
      title: 'Document created',
      description: 'Legal Contract Template v2.1 was created',
      timestamp: new Date('2024-01-15T09:00:00Z'),
      user: {
        id: 'user1',
        name: 'Sarah Johnson',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
        role: 'Legal Counsel'
      },
      priority: 'medium',
      category: 'document'
    },
    {
      id: '2',
      type: 'edit',
      title: 'Document updated',
      description: 'Modified clause 3.2 regarding termination conditions',
      timestamp: new Date('2024-01-15T10:30:00Z'),
      user: {
        id: 'user2',
        name: 'Michael Chen',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=michael',
        role: 'Senior Associate'
      },
      priority: 'high',
      category: 'document'
    },
    {
      id: '3',
      type: 'comment',
      title: 'Comment added',
      description: 'Please review the liability limitations in section 5.1',
      timestamp: new Date('2024-01-15T11:15:00Z'),
      user: {
        id: 'user3',
        name: 'Emily Rodriguez',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emily',
        role: 'Partner'
      },
      priority: 'urgent',
      category: 'review',
      actions: [
        {
          id: 'reply',
          label: 'Reply',
          icon: 'reply',
          variant: 'outline',
          onClick: (activity) => console.log('Reply to:', activity.id)
        }
      ]
    }
  ];

  ngOnInit() {
    this.loadInitialData();
  }

  loadInitialData() {
    this.loading = true;
    setTimeout(() => {
      this.activities = this.sampleActivities;
      this.loading = false;
    }, 1000);
  }

  handleActivityClick(activity: Activity) {
    console.log('Activity clicked:', activity);
  }

  async handleLoadMore() {
    this.loading = true;
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const newActivities: Activity[] = [
      {
        id: '6',
        type: 'system',
        title: 'Auto-backup completed',
        description: 'Document backed up to secure storage',
        timestamp: new Date('2024-01-14T23:30:00Z'),
        priority: 'low',
        category: 'system'
      }
    ];
    
    this.activities = [...this.activities, ...newActivities];
    this.loading = false;
  }

  handleFilter(filters: any) {
    this.filters = filters;
    console.log('Filters applied:', filters);
  }

  handleSearch(query: string) {
    console.log('Search query:', query);
  }

  handleRefresh() {
    console.log('Manual refresh triggered');
  }
}
```

### System Activity Dashboard

#### React
```jsx
import { SafActivity, SafIcon, SafBadge } from '@saffron/react';
import { useState, useEffect } from 'react';

const SystemActivityDashboard = () => {
  const [systemActivities, setSystemActivities] = useState([]);
  const [userActivities, setUserActivities] = useState([]);
  const [securityActivities, setSecurityActivities] = useState([]);

  const systemEvents = [
    {
      id: 'sys1',
      type: 'system',
      title: 'Database backup completed',
      description: 'Scheduled backup of primary database completed successfully',
      timestamp: new Date('2024-01-15T02:00:00Z'),
      priority: 'low',
      category: 'maintenance',
      metadata: {
        duration: '45 minutes',
        size: '2.3 GB',
        location: 'aws-backup-vault'
      }
    },
    {
      id: 'sys2',
      type: 'system',
      title: 'High CPU usage detected',
      description: 'Server load exceeded 85% threshold for 10 minutes',
      timestamp: new Date('2024-01-15T08:30:00Z'),
      priority: 'urgent',
      category: 'alert',
      metadata: {
        server: 'prod-web-01',
        peak: '92%',
        duration: '10 minutes'
      },
      actions: [
        {
          id: 'investigate',
          label: 'Investigate',
          icon: 'search',
          variant: 'primary',
          onClick: (activity) => console.log('Investigating:', activity.id)
        },
        {
          id: 'scale',
          label: 'Auto Scale',
          icon: 'trending-up',
          variant: 'secondary',
          onClick: (activity) => console.log('Auto scaling:', activity.id)
        }
      ]
    },
    {
      id: 'sys3',
      type: 'system',
      title: 'Security patch applied',
      description: 'Applied CVE-2024-0001 security patch to all servers',
      timestamp: new Date('2024-01-15T04:15:00Z'),
      priority: 'high',
      category: 'security',
      metadata: {
        patch: 'CVE-2024-0001',
        servers: 12,
        rebootRequired: false
      }
    }
  ];

  const userEvents = [
    {
      id: 'user1',
      type: 'login',
      title: 'User login',
      description: 'Administrator logged in from new location',
      timestamp: new Date('2024-01-15T09:00:00Z'),
      user: {
        id: 'admin1',
        name: 'System Administrator',
        role: 'Administrator'
      },
      priority: 'medium',
      category: 'authentication',
      metadata: {
        ip: '192.168.1.100',
        location: 'New York, NY',
        userAgent: 'Mozilla/5.0...'
      }
    },
    {
      id: 'user2',
      type: 'logout',
      title: 'User logout',
      description: 'Session expired after 8 hours',
      timestamp: new Date('2024-01-15T17:00:00Z'),
      user: {
        id: 'admin1',
        name: 'System Administrator',
        role: 'Administrator'
      },
      priority: 'low',
      category: 'authentication'
    }
  ];

  const securityEvents = [
    {
      id: 'sec1',
      type: 'system',
      title: 'Failed login attempts',
      description: '5 consecutive failed login attempts detected',
      timestamp: new Date('2024-01-15T10:30:00Z'),
      priority: 'urgent',
      category: 'security',
      metadata: {
        attempts: 5,
        ip: '203.0.113.10',
        username: 'admin',
        blocked: true
      },
      actions: [
        {
          id: 'block',
          label: 'Block IP',
          icon: 'shield',
          variant: 'danger',
          onClick: (activity) => console.log('Blocking IP:', activity.id)
        },
        {
          id: 'investigate',
          label: 'Investigate',
          icon: 'search',
          variant: 'secondary',
          onClick: (activity) => console.log('Investigating:', activity.id)
        }
      ]
    }
  ];

  useEffect(() => {
    setSystemActivities(systemEvents);
    setUserActivities(userEvents);
    setSecurityActivities(securityEvents);
  }, []);

  return (
    <div className="system-activity-dashboard">
      <h2>System Activity Dashboard</h2>
      
      <div className="dashboard-grid">
        {/* System Events */}
        <div className="activity-panel">
          <div className="panel-header">
            <h3>System Events</h3>
            <SafBadge variant="info" size="small">
              {systemActivities.length} events
            </SafBadge>
          </div>
          
          <SafActivity
            activities={systemActivities}
            layout="list"
            showTimestamps={true}
            showAvatars={false}
            showIcons={true}
            groupBy="none"
            sortOrder="desc"
            enableFiltering={true}
            realTimeUpdates={true}
            autoRefresh={true}
            refreshInterval={30000}
            onActivityClick={(activity) => console.log('System event:', activity)}
          />
        </div>

        {/* User Activities */}
        <div className="activity-panel">
          <div className="panel-header">
            <h3>User Activities</h3>
            <SafBadge variant="success" size="small">
              {userActivities.length} activities
            </SafBadge>
          </div>
          
          <SafActivity
            activities={userActivities}
            layout="compact"
            showTimestamps={true}
            showAvatars={true}
            showIcons={true}
            groupBy="user"
            onActivityClick={(activity) => console.log('User activity:', activity)}
          />
        </div>

        {/* Security Alerts */}
        <div className="activity-panel security-panel">
          <div className="panel-header">
            <h3>Security Alerts</h3>
            <SafBadge variant="danger" size="small">
              {securityActivities.length} alerts
            </SafBadge>
          </div>
          
          <SafActivity
            activities={securityActivities}
            layout="card"
            showTimestamps={true}
            showAvatars={false}
            showIcons={true}
            groupBy="none"
            sortOrder="desc"
            onActivityClick={(activity) => console.log('Security alert:', activity)}
          />
        </div>

        {/* Combined Timeline */}
        <div className="activity-panel timeline-panel">
          <h3>Complete Activity Timeline</h3>
          
          <SafActivity
            activities={[...systemActivities, ...userActivities, ...securityActivities]}
            layout="timeline"
            orientation="vertical"
            showTimestamps={true}
            showAvatars={true}
            showIcons={true}
            groupBy="date"
            sortOrder="desc"
            enableFiltering={true}
            enableSearch={true}
            maxItems={20}
            virtualized={true}
            onActivityClick={(activity) => console.log('Timeline activity:', activity)}
            onLoadMore={() => console.log('Load more activities')}
          />
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// system-activity-dashboard.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-system-activity-dashboard',
  template: `
    <div class="system-activity-dashboard">
      <h2>System Activity Dashboard</h2>
      
      <div class="dashboard-grid">
        <!-- System Events -->
        <div class="activity-panel">
          <div class="panel-header">
            <h3>System Events</h3>
            <saf-badge variant="info" size="small">
              {{ systemActivities.length }} events
            </saf-badge>
          </div>
          
          <saf-activity
            [activities]="systemActivities"
            layout="list"
            [showTimestamps]="true"
            [showAvatars]="false"
            [showIcons]="true"
            groupBy="none"
            sortOrder="desc"
            [enableFiltering]="true"
            [realTimeUpdates]="true"
            [autoRefresh]="true"
            [refreshInterval]="30000"
            (activityClick)="handleSystemEvent($event)">
          </saf-activity>
        </div>

        <!-- User Activities -->
        <div class="activity-panel">
          <div class="panel-header">
            <h3>User Activities</h3>
            <saf-badge variant="success" size="small">
              {{ userActivities.length }} activities
            </saf-badge>
          </div>
          
          <saf-activity
            [activities]="userActivities"
            layout="compact"
            [showTimestamps]="true"
            [showAvatars]="true"
            [showIcons]="true"
            groupBy="user"
            (activityClick)="handleUserActivity($event)">
          </saf-activity>
        </div>

        <!-- Security Alerts -->
        <div class="activity-panel security-panel">
          <div class="panel-header">
            <h3>Security Alerts</h3>
            <saf-badge variant="danger" size="small">
              {{ securityActivities.length }} alerts
            </saf-badge>
          </div>
          
          <saf-activity
            [activities]="securityActivities"
            layout="card"
            [showTimestamps]="true"
            [showAvatars]="false"
            [showIcons]="true"
            groupBy="none"
            sortOrder="desc"
            (activityClick)="handleSecurityAlert($event)">
          </saf-activity>
        </div>

        <!-- Combined Timeline -->
        <div class="activity-panel timeline-panel">
          <h3>Complete Activity Timeline</h3>
          
          <saf-activity
            [activities]="allActivities"
            layout="timeline"
            orientation="vertical"
            [showTimestamps]="true"
            [showAvatars]="true"
            [showIcons]="true"
            groupBy="date"
            sortOrder="desc"
            [enableFiltering]="true"
            [enableSearch]="true"
            [maxItems]="20"
            [virtualized]="true"
            (activityClick)="handleTimelineActivity($event)"
            (loadMore)="loadMoreActivities()">
          </saf-activity>
        </div>
      </div>
    </div>
  `
})
export class SystemActivityDashboardComponent implements OnInit {
  systemActivities: Activity[] = [];
  userActivities: Activity[] = [];
  securityActivities: Activity[] = [];

  get allActivities(): Activity[] {
    return [...this.systemActivities, ...this.userActivities, ...this.securityActivities];
  }

  ngOnInit() {
    this.loadSystemActivities();
    this.loadUserActivities();
    this.loadSecurityActivities();
  }

  loadSystemActivities() {
    this.systemActivities = [
      {
        id: 'sys1',
        type: 'system',
        title: 'Database backup completed',
        description: 'Scheduled backup of primary database completed successfully',
        timestamp: new Date('2024-01-15T02:00:00Z'),
        priority: 'low',
        category: 'maintenance'
      }
      // ... more system activities
    ];
  }

  loadUserActivities() {
    this.userActivities = [
      {
        id: 'user1',
        type: 'login',
        title: 'User login',
        description: 'Administrator logged in from new location',
        timestamp: new Date('2024-01-15T09:00:00Z'),
        user: {
          id: 'admin1',
          name: 'System Administrator',
          role: 'Administrator'
        },
        priority: 'medium',
        category: 'authentication'
      }
      // ... more user activities
    ];
  }

  loadSecurityActivities() {
    this.securityActivities = [
      {
        id: 'sec1',
        type: 'system',
        title: 'Failed login attempts',
        description: '5 consecutive failed login attempts detected',
        timestamp: new Date('2024-01-15T10:30:00Z'),
        priority: 'urgent',
        category: 'security'
      }
      // ... more security activities
    ];
  }

  handleSystemEvent(activity: Activity) {
    console.log('System event:', activity);
  }

  handleUserActivity(activity: Activity) {
    console.log('User activity:', activity);
  }

  handleSecurityAlert(activity: Activity) {
    console.log('Security alert:', activity);
  }

  handleTimelineActivity(activity: Activity) {
    console.log('Timeline activity:', activity);
  }

  loadMoreActivities() {
    console.log('Load more activities');
  }
}
```

## Best Practices

1. **Performance Optimization**
   - Use virtualization for large activity lists
   - Implement pagination for extensive datasets
   - Consider lazy loading for activity details

2. **Real-time Updates**
   - Implement WebSocket connections for live updates
   - Use appropriate refresh intervals
   - Handle connection failures gracefully

3. **Activity Categorization**
   - Group related activities logically
   - Use consistent iconography for activity types
   - Implement effective filtering mechanisms

4. **User Experience**
   - Provide clear timestamps and relative time displays
   - Enable contextual actions on activities
   - Offer multiple view layouts for different use cases

5. **Data Management**
   - Implement efficient data structures for activity storage
   - Consider archiving old activities
   - Maintain activity metadata for analytics

## Accessibility Considerations

1. **Screen Reader Support**
   - Provide meaningful activity descriptions
   - Use proper heading hierarchy for grouping
   - Announce new activities when they arrive

2. **Keyboard Navigation**
   - Support Tab navigation through activities
   - Implement keyboard shortcuts for common actions
   - Provide focus indicators for interactive elements

3. **Visual Accessibility**
   - Ensure sufficient color contrast for priority indicators
   - Use multiple visual cues (color, icons, text) for activity types
   - Support high contrast and reduced motion preferences

4. **Content Accessibility**
   - Format timestamps in accessible ways
   - Provide alternative text for activity icons
   - Use semantic markup for activity structure

## Related Components

- **SafAvatar**: User avatars in activity displays
- **SafIcon**: Activity type and action icons
- **SafBadge**: Priority and status indicators
- **SafButton**: Action buttons within activities
- **SafTimeline**: Timeline layout component

## Notes

- Activity component supports real-time updates through WebSocket connections
- Built-in virtualization for handling large activity datasets efficiently
- Customizable activity types and icons for different application contexts
- Automatic grouping and sorting capabilities for better organization
- Mobile-responsive design with touch-friendly interactions
- Comprehensive filtering and search functionality for activity discovery
