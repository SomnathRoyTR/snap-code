# SafTimeline Component

## Overview

SafTimeline is a chronological event display component that presents events, milestones, and activities in a sequential timeline format. It supports both vertical and horizontal orientations, customizable event markers, interactive events, and various timeline styles for different use cases including project timelines, activity feeds, process flows, and historical data visualization.

## React API

### SafTimeline

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `items` | `TimelineItem[]` | Yes | - | Array of timeline items to display |
| `orientation` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Timeline layout orientation |
| `variant` | `'default' \| 'alternating' \| 'compact' \| 'detailed'` | No | `'default'` | Timeline display variant |
| `showConnectors` | `boolean` | No | `true` | Whether to show connecting lines between items |
| `interactive` | `boolean` | No | `false` | Whether timeline items are clickable |
| `markerSize` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size of timeline markers |
| `groupBy` | `'date' \| 'category' \| 'none'` | No | `'none'` | How to group timeline items |
| `sortOrder` | `'asc' \| 'desc'` | No | `'asc'` | Sort order for timeline items |
| `maxHeight` | `string` | No | - | Maximum height with scrolling |
| `loading` | `boolean` | No | `false` | Whether timeline is in loading state |
| `onItemClick` | `(item: TimelineItem) => void` | No | - | Callback when item is clicked |
| `onItemHover` | `(item: TimelineItem \| null) => void` | No | - | Callback when item is hovered |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### TimelineItem Interface

```typescript
interface TimelineItem {
  id: string;
  title: string;
  description?: string;
  timestamp: Date | string;
  category?: string;
  status?: 'completed' | 'in-progress' | 'pending' | 'cancelled';
  icon?: string;
  color?: string;
  metadata?: Record<string, any>;
  actions?: TimelineAction[];
  attachments?: TimelineAttachment[];
}

interface TimelineAction {
  label: string;
  action: () => void;
  icon?: string;
  variant?: 'primary' | 'secondary' | 'danger';
}

interface TimelineAttachment {
  name: string;
  type: string;
  url: string;
  size?: string;
}
```

## Angular API

### saf-timeline

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[items]` | `TimelineItem[]` | Yes | - | Array of timeline items to display |
| `[orientation]` | `'vertical' \| 'horizontal'` | No | `'vertical'` | Timeline layout orientation |
| `[variant]` | `'default' \| 'alternating' \| 'compact' \| 'detailed'` | No | `'default'` | Timeline display variant |
| `[showConnectors]` | `boolean` | No | `true` | Whether to show connecting lines between items |
| `[interactive]` | `boolean` | No | `false` | Whether timeline items are clickable |
| `[markerSize]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size of timeline markers |
| `[groupBy]` | `'date' \| 'category' \| 'none'` | No | `'none'` | How to group timeline items |
| `[sortOrder]` | `'asc' \| 'desc'` | No | `'asc'` | Sort order for timeline items |
| `[maxHeight]` | `string` | No | - | Maximum height with scrolling |
| `[loading]` | `boolean` | No | `false` | Whether timeline is in loading state |
| `(itemClick)` | `EventEmitter<TimelineItem>` | No | - | Event when item is clicked |
| `(itemHover)` | `EventEmitter<TimelineItem \| null>` | No | - | Event when item is hovered |

## Usage Examples

### Basic Project Timeline

#### React
```jsx
import { SafTimeline } from '@saffron/react';

const ProjectTimelineExample = () => {
  const projectEvents = [
    {
      id: '1',
      title: 'Project Kickoff',
      description: 'Initial project planning and team onboarding meeting',
      timestamp: '2024-01-15T09:00:00Z',
      category: 'milestone',
      status: 'completed',
      icon: 'rocket',
      color: '#4CAF50'
    },
    {
      id: '2',
      title: 'Requirements Gathering',
      description: 'Stakeholder interviews and requirement documentation',
      timestamp: '2024-01-22T14:30:00Z',
      category: 'phase',
      status: 'completed',
      icon: 'document',
      color: '#2196F3'
    },
    {
      id: '3',
      title: 'Design Phase',
      description: 'UI/UX design and prototyping',
      timestamp: '2024-02-05T10:00:00Z',
      category: 'phase',
      status: 'in-progress',
      icon: 'design',
      color: '#FF9800'
    },
    {
      id: '4',
      title: 'Development Sprint 1',
      description: 'Core functionality implementation',
      timestamp: '2024-02-20T09:00:00Z',
      category: 'development',
      status: 'pending',
      icon: 'code',
      color: '#9C27B0'
    }
  ];

  const handleItemClick = (item) => {
    console.log('Timeline item clicked:', item);
  };

  return (
    <div className="project-timeline">
      <h2>Project Development Timeline</h2>
      <SafTimeline
        items={projectEvents}
        variant="detailed"
        interactive={true}
        markerSize="large"
        onItemClick={handleItemClick}
        className="project-timeline-container"
      />
    </div>
  );
};
```

#### Angular
```typescript
// project-timeline.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-project-timeline',
  template: `
    <div class="project-timeline">
      <h2>Project Development Timeline</h2>
      <saf-timeline
        [items]="projectEvents"
        variant="detailed"
        [interactive]="true"
        markerSize="large"
        (itemClick)="handleItemClick($event)"
        class="project-timeline-container">
      </saf-timeline>
    </div>
  `
})
export class ProjectTimelineComponent {
  projectEvents = [
    {
      id: '1',
      title: 'Project Kickoff',
      description: 'Initial project planning and team onboarding meeting',
      timestamp: '2024-01-15T09:00:00Z',
      category: 'milestone',
      status: 'completed',
      icon: 'rocket',
      color: '#4CAF50'
    },
    {
      id: '2',
      title: 'Requirements Gathering',
      description: 'Stakeholder interviews and requirement documentation',
      timestamp: '2024-01-22T14:30:00Z',
      category: 'phase',
      status: 'completed',
      icon: 'document',
      color: '#2196F3'
    },
    {
      id: '3',
      title: 'Design Phase',
      description: 'UI/UX design and prototyping',
      timestamp: '2024-02-05T10:00:00Z',
      category: 'phase',
      status: 'in-progress',
      icon: 'design',
      color: '#FF9800'
    },
    {
      id: '4',
      title: 'Development Sprint 1',
      description: 'Core functionality implementation',
      timestamp: '2024-02-20T09:00:00Z',
      category: 'development',
      status: 'pending',
      icon: 'code',
      color: '#9C27B0'
    }
  ];

  handleItemClick(item: any) {
    console.log('Timeline item clicked:', item);
  }
}
```

### Activity Feed Timeline

#### React
```jsx
import { SafTimeline, SafIcon, SafButton } from '@saffron/react';

const ActivityFeedExample = () => {
  const activities = [
    {
      id: '1',
      title: 'Sarah Johnson commented on Design Review',
      description: 'The new dashboard layout looks great! Just a few minor adjustments needed.',
      timestamp: '2024-02-10T15:30:00Z',
      category: 'comment',
      status: 'completed',
      icon: 'message',
      color: '#2196F3',
      metadata: {
        user: 'Sarah Johnson',
        avatar: '/images/users/sarah.jpg'
      }
    },
    {
      id: '2',
      title: 'File uploaded: wireframes_v2.pdf',
      description: 'Updated wireframes with stakeholder feedback incorporated',
      timestamp: '2024-02-10T14:15:00Z',
      category: 'upload',
      status: 'completed',
      icon: 'upload',
      color: '#4CAF50',
      attachments: [
        {
          name: 'wireframes_v2.pdf',
          type: 'PDF',
          url: '/files/wireframes_v2.pdf',
          size: '2.3 MB'
        }
      ]
    },
    {
      id: '3',
      title: 'Meeting scheduled: Sprint Planning',
      description: 'Weekly sprint planning session with development team',
      timestamp: '2024-02-10T13:00:00Z',
      category: 'meeting',
      status: 'completed',
      icon: 'calendar',
      color: '#FF9800',
      actions: [
        {
          label: 'Join Meeting',
          action: () => console.log('Joining meeting'),
          icon: 'video',
          variant: 'primary'
        },
        {
          label: 'View Agenda',
          action: () => console.log('Viewing agenda'),
          icon: 'document',
          variant: 'secondary'
        }
      ]
    }
  ];

  return (
    <div className="activity-feed">
      <h2>Recent Activity</h2>
      <SafTimeline
        items={activities}
        variant="compact"
        maxHeight="400px"
        interactive={true}
        groupBy="date"
        className="activity-timeline"
      />
    </div>
  );
};
```

#### Angular
```typescript
// activity-feed.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-activity-feed',
  template: `
    <div class="activity-feed">
      <h2>Recent Activity</h2>
      <saf-timeline
        [items]="activities"
        variant="compact"
        maxHeight="400px"
        [interactive]="true"
        groupBy="date"
        class="activity-timeline">
      </saf-timeline>
    </div>
  `
})
export class ActivityFeedComponent {
  activities = [
    {
      id: '1',
      title: 'Sarah Johnson commented on Design Review',
      description: 'The new dashboard layout looks great! Just a few minor adjustments needed.',
      timestamp: '2024-02-10T15:30:00Z',
      category: 'comment',
      status: 'completed',
      icon: 'message',
      color: '#2196F3',
      metadata: {
        user: 'Sarah Johnson',
        avatar: '/images/users/sarah.jpg'
      }
    },
    {
      id: '2',
      title: 'File uploaded: wireframes_v2.pdf',
      description: 'Updated wireframes with stakeholder feedback incorporated',
      timestamp: '2024-02-10T14:15:00Z',
      category: 'upload',
      status: 'completed',
      icon: 'upload',
      color: '#4CAF50',
      attachments: [
        {
          name: 'wireframes_v2.pdf',
          type: 'PDF',
          url: '/files/wireframes_v2.pdf',
          size: '2.3 MB'
        }
      ]
    },
    {
      id: '3',
      title: 'Meeting scheduled: Sprint Planning',
      description: 'Weekly sprint planning session with development team',
      timestamp: '2024-02-10T13:00:00Z',
      category: 'meeting',
      status: 'completed',
      icon: 'calendar',
      color: '#FF9800',
      actions: [
        {
          label: 'Join Meeting',
          action: () => console.log('Joining meeting'),
          icon: 'video',
          variant: 'primary'
        },
        {
          label: 'View Agenda',
          action: () => console.log('Viewing agenda'),
          icon: 'document',
          variant: 'secondary'
        }
      ]
    }
  ];
}
```

### Horizontal Process Timeline

#### React
```jsx
import { SafTimeline, SafCard } from '@saffron/react';

const ProcessTimelineExample = () => {
  const processSteps = [
    {
      id: '1',
      title: 'Order Placed',
      description: 'Customer submitted order #12345',
      timestamp: '2024-02-10T10:00:00Z',
      status: 'completed',
      icon: 'shopping-cart',
      color: '#4CAF50'
    },
    {
      id: '2',
      title: 'Payment Processed',
      description: 'Payment verified and processed',
      timestamp: '2024-02-10T10:15:00Z',
      status: 'completed',
      icon: 'credit-card',
      color: '#4CAF50'
    },
    {
      id: '3',
      title: 'Order Prepared',
      description: 'Items picked and packaged',
      timestamp: '2024-02-10T14:30:00Z',
      status: 'completed',
      icon: 'package',
      color: '#4CAF50'
    },
    {
      id: '4',
      title: 'Shipped',
      description: 'Order dispatched for delivery',
      timestamp: '2024-02-11T09:00:00Z',
      status: 'in-progress',
      icon: 'truck',
      color: '#FF9800'
    },
    {
      id: '5',
      title: 'Delivered',
      description: 'Package delivered to customer',
      timestamp: '2024-02-12T16:00:00Z',
      status: 'pending',
      icon: 'home',
      color: '#9E9E9E'
    }
  ];

  return (
    <SafCard className="process-timeline-card">
      <SafCard.Header>
        <h3>Order Tracking - #12345</h3>
      </SafCard.Header>
      <SafCard.Content>
        <SafTimeline
          items={processSteps}
          orientation="horizontal"
          variant="compact"
          markerSize="large"
          className="process-timeline"
        />
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// process-timeline.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-process-timeline',
  template: `
    <saf-card class="process-timeline-card">
      <saf-card-header>
        <h3>Order Tracking - #12345</h3>
      </saf-card-header>
      <saf-card-content>
        <saf-timeline
          [items]="processSteps"
          orientation="horizontal"
          variant="compact"
          markerSize="large"
          class="process-timeline">
        </saf-timeline>
      </saf-card-content>
    </saf-card>
  `
})
export class ProcessTimelineComponent {
  processSteps = [
    {
      id: '1',
      title: 'Order Placed',
      description: 'Customer submitted order #12345',
      timestamp: '2024-02-10T10:00:00Z',
      status: 'completed',
      icon: 'shopping-cart',
      color: '#4CAF50'
    },
    {
      id: '2',
      title: 'Payment Processed',
      description: 'Payment verified and processed',
      timestamp: '2024-02-10T10:15:00Z',
      status: 'completed',
      icon: 'credit-card',
      color: '#4CAF50'
    },
    {
      id: '3',
      title: 'Order Prepared',
      description: 'Items picked and packaged',
      timestamp: '2024-02-10T14:30:00Z',
      status: 'completed',
      icon: 'package',
      color: '#4CAF50'
    },
    {
      id: '4',
      title: 'Shipped',
      description: 'Order dispatched for delivery',
      timestamp: '2024-02-11T09:00:00Z',
      status: 'in-progress',
      icon: 'truck',
      color: '#FF9800'
    },
    {
      id: '5',
      title: 'Delivered',
      description: 'Package delivered to customer',
      timestamp: '2024-02-12T16:00:00Z',
      status: 'pending',
      icon: 'home',
      color: '#9E9E9E'
    }
  ];
}
```

### Alternating Timeline with Rich Content

#### React
```jsx
import { SafTimeline, SafBadge, SafButton } from '@saffron/react';

const HistoryTimelineExample = () => {
  const historyEvents = [
    {
      id: '1',
      title: 'Company Founded',
      description: 'Thomson Reuters was established through the merger of Thomson Corporation and Reuters Group.',
      timestamp: '2008-04-17T00:00:00Z',
      category: 'milestone',
      status: 'completed',
      icon: 'building',
      color: '#1976D2',
      metadata: {
        significance: 'high',
        employees: '50,000+',
        locations: '100+ countries'
      }
    },
    {
      id: '2',
      title: 'Digital Transformation Initiative',
      description: 'Launched comprehensive digital transformation to modernize technology infrastructure.',
      timestamp: '2015-01-01T00:00:00Z',
      category: 'technology',
      status: 'completed',
      icon: 'digital',
      color: '#388E3C',
      metadata: {
        investment: '$2B+',
        duration: '5 years'
      }
    },
    {
      id: '3',
      title: 'AI & Analytics Platform Launch',
      description: 'Introduced advanced AI and analytics capabilities across all product lines.',
      timestamp: '2020-06-15T00:00:00Z',
      category: 'innovation',
      status: 'completed',
      icon: 'brain',
      color: '#7B1FA2',
      metadata: {
        products: '25+ enhanced',
        customers: '1M+ impacted'
      }
    }
  ];

  return (
    <div className="history-timeline">
      <h2>Company Timeline</h2>
      <SafTimeline
        items={historyEvents}
        variant="alternating"
        markerSize="large"
        interactive={true}
        className="company-history"
      />
    </div>
  );
};
```

#### Angular
```typescript
// history-timeline.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-history-timeline',
  template: `
    <div class="history-timeline">
      <h2>Company Timeline</h2>
      <saf-timeline
        [items]="historyEvents"
        variant="alternating"
        markerSize="large"
        [interactive]="true"
        class="company-history">
      </saf-timeline>
    </div>
  `
})
export class HistoryTimelineComponent {
  historyEvents = [
    {
      id: '1',
      title: 'Company Founded',
      description: 'Thomson Reuters was established through the merger of Thomson Corporation and Reuters Group.',
      timestamp: '2008-04-17T00:00:00Z',
      category: 'milestone',
      status: 'completed',
      icon: 'building',
      color: '#1976D2',
      metadata: {
        significance: 'high',
        employees: '50,000+',
        locations: '100+ countries'
      }
    },
    {
      id: '2',
      title: 'Digital Transformation Initiative',
      description: 'Launched comprehensive digital transformation to modernize technology infrastructure.',
      timestamp: '2015-01-01T00:00:00Z',
      category: 'technology',
      status: 'completed',
      icon: 'digital',
      color: '#388E3C',
      metadata: {
        investment: '$2B+',
        duration: '5 years'
      }
    },
    {
      id: '3',
      title: 'AI & Analytics Platform Launch',
      description: 'Introduced advanced AI and analytics capabilities across all product lines.',
      timestamp: '2020-06-15T00:00:00Z',
      category: 'innovation',
      status: 'completed',
      icon: 'brain',
      color: '#7B1FA2',
      metadata: {
        products: '25+ enhanced',
        customers: '1M+ impacted'
      }
    }
  ];
}
```

### Loading Timeline with Skeleton States

#### React
```jsx
import { SafTimeline, SafLoadingSpinner } from '@saffron/react';
import { useState, useEffect } from 'react';

const LoadingTimelineExample = () => {
  const [loading, setLoading] = useState(true);
  const [timelineData, setTimelineData] = useState([]);

  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      setTimelineData([
        {
          id: '1',
          title: 'Data Loading Complete',
          description: 'Successfully loaded timeline data from API',
          timestamp: new Date().toISOString(),
          status: 'completed',
          icon: 'check',
          color: '#4CAF50'
        }
      ]);
      setLoading(false);
    }, 2000);
  }, []);

  return (
    <div className="loading-timeline">
      <h2>Dynamic Timeline</h2>
      {loading ? (
        <div className="timeline-loading">
          <SafLoadingSpinner size="large" />
          <p>Loading timeline data...</p>
        </div>
      ) : (
        <SafTimeline
          items={timelineData}
          variant="detailed"
          interactive={true}
        />
      )}
    </div>
  );
};
```

#### Angular
```typescript
// loading-timeline.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-loading-timeline',
  template: `
    <div class="loading-timeline">
      <h2>Dynamic Timeline</h2>
      <div *ngIf="loading" class="timeline-loading">
        <saf-loading-spinner size="large"></saf-loading-spinner>
        <p>Loading timeline data...</p>
      </div>
      <saf-timeline
        *ngIf="!loading"
        [items]="timelineData"
        variant="detailed"
        [interactive]="true">
      </saf-timeline>
    </div>
  `
})
export class LoadingTimelineComponent implements OnInit {
  loading = true;
  timelineData: any[] = [];

  ngOnInit() {
    // Simulate API call
    setTimeout(() => {
      this.timelineData = [
        {
          id: '1',
          title: 'Data Loading Complete',
          description: 'Successfully loaded timeline data from API',
          timestamp: new Date().toISOString(),
          status: 'completed',
          icon: 'check',
          color: '#4CAF50'
        }
      ];
      this.loading = false;
    }, 2000);
  }
}
```

## Best Practices

1. **Chronological Organization**
   - Sort timeline items by timestamp for logical flow
   - Use consistent date/time formatting
   - Group related events when appropriate

2. **Visual Hierarchy**
   - Use different marker sizes and colors for event importance
   - Implement consistent status indicators
   - Maintain proper spacing between timeline items

3. **Content Strategy**
   - Keep titles concise and descriptive
   - Provide meaningful descriptions for context
   - Use icons to enhance visual identification

4. **Performance Optimization**
   - Implement virtualization for large timeline datasets
   - Use lazy loading for timeline content
   - Optimize marker and connector rendering

5. **Responsive Design**
   - Switch between horizontal and vertical orientations based on screen size
   - Adjust marker sizes and spacing for mobile devices
   - Ensure touch-friendly interaction targets

## Accessibility Considerations

1. **ARIA Support**
   - Use `role="list"` and `role="listitem"` for timeline structure
   - Implement `aria-label` for timeline markers and status indicators
   - Provide `aria-describedby` for detailed timeline item information

2. **Keyboard Navigation**
   - Support Tab navigation through interactive timeline items
   - Implement Enter/Space activation for clickable items
   - Provide keyboard shortcuts for timeline navigation

3. **Screen Reader Compatibility**
   - Announce timeline orientation and total item count
   - Provide meaningful descriptions for timeline events and status
   - Use semantic markup for chronological relationships

4. **Visual Accessibility**
   - Ensure sufficient color contrast for markers and text
   - Provide alternative text for timeline icons
   - Support high contrast and reduced motion preferences

## Related Components

- **SafCard**: Container for timeline content and grouping
- **SafIcon**: Visual markers and status indicators
- **SafBadge**: Status indicators and category labels
- **SafButton**: Action buttons within timeline items
- **SafLoadingSpinner**: Loading states for dynamic timelines
- **SafTooltip**: Additional context on hover

## Notes

- Timeline automatically handles responsive layout adjustments
- Custom CSS variables available for theming timeline appearance
- Supports both real-time updates and static timeline data
- Built-in support for internationalization and localization
- Optimized for performance with large datasets through virtualization
- Compatible with drag-and-drop libraries for timeline item reordering
