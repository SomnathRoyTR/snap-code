# SafMetadata Component

## Overview
The `SafMetadata` component provides a container for displaying structured metadata information in a consistent format. It organizes key-value pairs, labels, and descriptive information in an accessible and visually appealing layout. This component is designed to work with `SafMetadataItem` components and supports various layouts, grouping, and styling options.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `layout` | `'horizontal' \| 'vertical' \| 'grid'` | `'vertical'` | Layout direction for metadata items |
| `spacing` | `'compact' \| 'normal' \| 'relaxed'` | `'normal'` | Spacing between metadata items |
| `columns` | `number` | `1` | Number of columns for grid layout |
| `dividers` | `boolean` | `false` | Whether to show dividers between items |
| `bordered` | `boolean` | `false` | Whether to show border around the container |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant for text and spacing |
| `alignment` | `'start' \| 'center' \| 'end'` | `'start'` | Alignment of content within items |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Metadata items and content |

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `layout` | `'horizontal' \| 'vertical' \| 'grid'` | `'vertical'` | Layout direction for metadata items |
| `spacing` | `'compact' \| 'normal' \| 'relaxed'` | `'normal'` | Spacing between metadata items |
| `columns` | `number` | `1` | Number of columns for grid layout |
| `dividers` | `boolean` | `false` | Whether to show dividers between items |
| `bordered` | `boolean` | `false` | Whether to show border around the container |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Size variant for text and spacing |
| `alignment` | `'start' \| 'center' \| 'end'` | `'start'` | Alignment of content within items |

### Content Projection
- **Default slot**: Metadata items and content

## Usage Examples

### Basic Metadata Display

#### React
```jsx
import { SafMetadata, SafMetadataItem } from '@saffron/core-components';

function BasicMetadataExample() {
  return (
    <SafMetadata>
      <SafMetadataItem label="Name" value="John Smith" />
      <SafMetadataItem label="Email" value="john.smith@example.com" />
      <SafMetadataItem label="Department" value="Engineering" />
      <SafMetadataItem label="Location" value="New York, NY" />
      <SafMetadataItem label="Start Date" value="January 15, 2023" />
    </SafMetadata>
  );
}
```

#### Angular
```html
<saf-metadata>
  <saf-metadata-item label="Name" value="John Smith"></saf-metadata-item>
  <saf-metadata-item label="Email" value="john.smith@example.com"></saf-metadata-item>
  <saf-metadata-item label="Department" value="Engineering"></saf-metadata-item>
  <saf-metadata-item label="Location" value="New York, NY"></saf-metadata-item>
  <saf-metadata-item label="Start Date" value="January 15, 2023"></saf-metadata-item>
</saf-metadata>
```

### Horizontal Layout with Dividers

#### React
```jsx
import { SafMetadata, SafMetadataItem } from '@saffron/core-components';

function HorizontalMetadataExample() {
  return (
    <SafMetadata layout="horizontal" dividers spacing="relaxed">
      <SafMetadataItem label="Status" value="Active" />
      <SafMetadataItem label="Priority" value="High" />
      <SafMetadataItem label="Assignee" value="Jane Doe" />
      <SafMetadataItem label="Due Date" value="Dec 31, 2024" />
    </SafMetadata>
  );
}
```

#### Angular
```html
<saf-metadata layout="horizontal" [dividers]="true" spacing="relaxed">
  <saf-metadata-item label="Status" value="Active"></saf-metadata-item>
  <saf-metadata-item label="Priority" value="High"></saf-metadata-item>
  <saf-metadata-item label="Assignee" value="Jane Doe"></saf-metadata-item>
  <saf-metadata-item label="Due Date" value="Dec 31, 2024"></saf-metadata-item>
</saf-metadata>
```

### Grid Layout

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge, SafIcon } from '@saffron/core-components';

function GridMetadataExample() {
  return (
    <SafMetadata 
      layout="grid" 
      columns={2} 
      bordered 
      spacing="normal"
      size="medium"
    >
      <SafMetadataItem label="Project Name" value="Saffron Design System" />
      
      <SafMetadataItem label="Status">
        <SafBadge variant="success">Active</SafBadge>
      </SafMetadataItem>
      
      <SafMetadataItem label="Team Size" value="8 members" />
      
      <SafMetadataItem label="Budget" value="$250,000" />
      
      <SafMetadataItem label="Start Date" value="March 1, 2024" />
      
      <SafMetadataItem label="Progress">
        <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
          <SafIcon name="chart" />
          <span>75% Complete</span>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Technologies">
        <div style={{ display: 'flex', gap: '0.25rem', flexWrap: 'wrap' }}>
          <SafBadge size="small">React</SafBadge>
          <SafBadge size="small">TypeScript</SafBadge>
          <SafBadge size="small">Angular</SafBadge>
        </div>
      </SafMetadataItem>
      
      <SafMetadataItem label="Last Updated" value="2 hours ago" />
    </SafMetadata>
  );
}
```

#### Angular
```html
<saf-metadata 
  layout="grid" 
  [columns]="2" 
  [bordered]="true" 
  spacing="normal"
  size="medium"
>
  <saf-metadata-item label="Project Name" value="Saffron Design System"></saf-metadata-item>
  
  <saf-metadata-item label="Status">
    <saf-badge variant="success">Active</saf-badge>
  </saf-metadata-item>
  
  <saf-metadata-item label="Team Size" value="8 members"></saf-metadata-item>
  
  <saf-metadata-item label="Budget" value="$250,000"></saf-metadata-item>
  
  <saf-metadata-item label="Start Date" value="March 1, 2024"></saf-metadata-item>
  
  <saf-metadata-item label="Progress">
    <div style="display: flex; align-items: center; gap: 0.5rem;">
      <saf-icon name="chart"></saf-icon>
      <span>75% Complete</span>
    </div>
  </saf-metadata-item>
  
  <saf-metadata-item label="Technologies">
    <div style="display: flex; gap: 0.25rem; flex-wrap: wrap;">
      <saf-badge size="small">React</saf-badge>
      <saf-badge size="small">TypeScript</saf-badge>
      <saf-badge size="small">Angular</saf-badge>
    </div>
  </saf-metadata-item>
  
  <saf-metadata-item label="Last Updated" value="2 hours ago"></saf-metadata-item>
</saf-metadata>
```

### Complex Metadata with Grouping

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge, SafIcon, SafButton } from '@saffron/core-components';

function ComplexMetadataExample() {
  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '2rem' }}>
      {/* Basic Information */}
      <div>
        <h3>Basic Information</h3>
        <SafMetadata layout="grid" columns={2} dividers>
          <SafMetadataItem label="User ID" value="USR-12345" />
          <SafMetadataItem label="Username" value="john.smith" />
          <SafMetadataItem label="Full Name" value="John Michael Smith" />
          <SafMetadataItem label="Email" value="john.smith@company.com" />
        </SafMetadata>
      </div>
      
      {/* Account Details */}
      <div>
        <h3>Account Details</h3>
        <SafMetadata spacing="relaxed">
          <SafMetadataItem label="Account Type">
            <SafBadge variant="info">Premium</SafBadge>
          </SafMetadataItem>
          
          <SafMetadataItem label="Status">
            <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
              <SafIcon name="check-circle" color="success" />
              <span>Active</span>
            </div>
          </SafMetadataItem>
          
          <SafMetadataItem label="Member Since" value="January 15, 2022" />
          
          <SafMetadataItem label="Last Login" value="2 hours ago" />
          
          <SafMetadataItem label="Two-Factor Auth">
            <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
              <SafIcon name="shield" color="success" />
              <span>Enabled</span>
              <SafButton variant="ghost" size="small">
                Manage
              </SafButton>
            </div>
          </SafMetadataItem>
        </SafMetadata>
      </div>
      
      {/* Preferences */}
      <div>
        <h3>Preferences</h3>
        <SafMetadata layout="horizontal" spacing="normal">
          <SafMetadataItem label="Language" value="English" />
          <SafMetadataItem label="Timezone" value="EST (UTC-5)" />
          <SafMetadataItem label="Theme" value="Light" />
          <SafMetadataItem label="Notifications" value="Enabled" />
        </SafMetadata>
      </div>
    </div>
  );
}
```

#### Angular
```html
<div style="display: flex; flex-direction: column; gap: 2rem;">
  <!-- Basic Information -->
  <div>
    <h3>Basic Information</h3>
    <saf-metadata layout="grid" [columns]="2" [dividers]="true">
      <saf-metadata-item label="User ID" value="USR-12345"></saf-metadata-item>
      <saf-metadata-item label="Username" value="john.smith"></saf-metadata-item>
      <saf-metadata-item label="Full Name" value="John Michael Smith"></saf-metadata-item>
      <saf-metadata-item label="Email" value="john.smith@company.com"></saf-metadata-item>
    </saf-metadata>
  </div>
  
  <!-- Account Details -->
  <div>
    <h3>Account Details</h3>
    <saf-metadata spacing="relaxed">
      <saf-metadata-item label="Account Type">
        <saf-badge variant="info">Premium</saf-badge>
      </saf-metadata-item>
      
      <saf-metadata-item label="Status">
        <div style="display: flex; align-items: center; gap: 0.5rem;">
          <saf-icon name="check-circle" color="success"></saf-icon>
          <span>Active</span>
        </div>
      </saf-metadata-item>
      
      <saf-metadata-item label="Member Since" value="January 15, 2022"></saf-metadata-item>
      
      <saf-metadata-item label="Last Login" value="2 hours ago"></saf-metadata-item>
      
      <saf-metadata-item label="Two-Factor Auth">
        <div style="display: flex; align-items: center; gap: 0.5rem;">
          <saf-icon name="shield" color="success"></saf-icon>
          <span>Enabled</span>
          <saf-button variant="ghost" size="small">
            Manage
          </saf-button>
        </div>
      </saf-metadata-item>
    </saf-metadata>
  </div>
  
  <!-- Preferences -->
  <div>
    <h3>Preferences</h3>
    <saf-metadata layout="horizontal" spacing="normal">
      <saf-metadata-item label="Language" value="English"></saf-metadata-item>
      <saf-metadata-item label="Timezone" value="EST (UTC-5)"></saf-metadata-item>
      <saf-metadata-item label="Theme" value="Light"></saf-metadata-item>
      <saf-metadata-item label="Notifications" value="Enabled"></saf-metadata-item>
    </saf-metadata>
  </div>
</div>
```

### Dynamic Metadata

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafSpinner, SafIcon } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicMetadataExample() {
  const [metadata, setMetadata] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      setMetadata({
        system: {
          version: '2.4.1',
          uptime: '15 days, 3 hours',
          status: 'healthy',
          environment: 'production'
        },
        performance: {
          cpuUsage: '45%',
          memoryUsage: '2.1 GB / 8 GB',
          diskSpace: '156 GB / 500 GB',
          requests: '1,234,567'
        },
        network: {
          bandwidth: '95.2 Mbps',
          latency: '12ms',
          connections: '2,847'
        }
      });
      setLoading(false);
    }, 2000);
  }, []);

  if (loading) {
    return (
      <div style={{ textAlign: 'center', padding: '2rem' }}>
        <SafSpinner size="large" />
        <p>Loading system information...</p>
      </div>
    );
  }

  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '2rem' }}>
      <div>
        <h3>System Information</h3>
        <SafMetadata layout="grid" columns={2} bordered>
          <SafMetadataItem label="Version" value={metadata.system.version} />
          <SafMetadataItem label="Uptime" value={metadata.system.uptime} />
          <SafMetadataItem label="Status">
            <div style={{ display: 'flex', alignItems: 'center', gap: '0.5rem' }}>
              <SafIcon name="check-circle" color="success" />
              <span style={{ textTransform: 'capitalize' }}>{metadata.system.status}</span>
            </div>
          </SafMetadataItem>
          <SafMetadataItem label="Environment" value={metadata.system.environment} />
        </SafMetadata>
      </div>
      
      <div>
        <h3>Performance Metrics</h3>
        <SafMetadata spacing="normal">
          <SafMetadataItem label="CPU Usage" value={metadata.performance.cpuUsage} />
          <SafMetadataItem label="Memory Usage" value={metadata.performance.memoryUsage} />
          <SafMetadataItem label="Disk Space" value={metadata.performance.diskSpace} />
          <SafMetadataItem label="Total Requests" value={metadata.performance.requests} />
        </SafMetadata>
      </div>
      
      <div>
        <h3>Network Statistics</h3>
        <SafMetadata layout="horizontal" dividers>
          <SafMetadataItem label="Bandwidth" value={metadata.network.bandwidth} />
          <SafMetadataItem label="Latency" value={metadata.network.latency} />
          <SafMetadataItem label="Active Connections" value={metadata.network.connections} />
        </SafMetadata>
      </div>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component, OnInit } from '@angular/core';

interface SystemMetadata {
  system: {
    version: string;
    uptime: string;
    status: string;
    environment: string;
  };
  performance: {
    cpuUsage: string;
    memoryUsage: string;
    diskSpace: string;
    requests: string;
  };
  network: {
    bandwidth: string;
    latency: string;
    connections: string;
  };
}

@Component({
  selector: 'app-dynamic-metadata',
  template: `
    <div *ngIf="loading" style="text-align: center; padding: 2rem;">
      <saf-spinner size="large"></saf-spinner>
      <p>Loading system information...</p>
    </div>

    <div *ngIf="!loading && metadata" style="display: flex; flex-direction: column; gap: 2rem;">
      <div>
        <h3>System Information</h3>
        <saf-metadata layout="grid" [columns]="2" [bordered]="true">
          <saf-metadata-item label="Version" [value]="metadata.system.version"></saf-metadata-item>
          <saf-metadata-item label="Uptime" [value]="metadata.system.uptime"></saf-metadata-item>
          <saf-metadata-item label="Status">
            <div style="display: flex; align-items: center; gap: 0.5rem;">
              <saf-icon name="check-circle" color="success"></saf-icon>
              <span style="text-transform: capitalize;">{{metadata.system.status}}</span>
            </div>
          </saf-metadata-item>
          <saf-metadata-item label="Environment" [value]="metadata.system.environment"></saf-metadata-item>
        </saf-metadata>
      </div>
      
      <div>
        <h3>Performance Metrics</h3>
        <saf-metadata spacing="normal">
          <saf-metadata-item label="CPU Usage" [value]="metadata.performance.cpuUsage"></saf-metadata-item>
          <saf-metadata-item label="Memory Usage" [value]="metadata.performance.memoryUsage"></saf-metadata-item>
          <saf-metadata-item label="Disk Space" [value]="metadata.performance.diskSpace"></saf-metadata-item>
          <saf-metadata-item label="Total Requests" [value]="metadata.performance.requests"></saf-metadata-item>
        </saf-metadata>
      </div>
      
      <div>
        <h3>Network Statistics</h3>
        <saf-metadata layout="horizontal" [dividers]="true">
          <saf-metadata-item label="Bandwidth" [value]="metadata.network.bandwidth"></saf-metadata-item>
          <saf-metadata-item label="Latency" [value]="metadata.network.latency"></saf-metadata-item>
          <saf-metadata-item label="Active Connections" [value]="metadata.network.connections"></saf-metadata-item>
        </saf-metadata>
      </div>
    </div>
  `
})
export class DynamicMetadataComponent implements OnInit {
  metadata: SystemMetadata | null = null;
  loading = true;

  ngOnInit() {
    // Simulate API call
    setTimeout(() => {
      this.metadata = {
        system: {
          version: '2.4.1',
          uptime: '15 days, 3 hours',
          status: 'healthy',
          environment: 'production'
        },
        performance: {
          cpuUsage: '45%',
          memoryUsage: '2.1 GB / 8 GB',
          diskSpace: '156 GB / 500 GB',
          requests: '1,234,567'
        },
        network: {
          bandwidth: '95.2 Mbps',
          latency: '12ms',
          connections: '2,847'
        }
      };
      this.loading = false;
    }, 2000);
  }
}
```

### Responsive Metadata

#### React
```jsx
import { SafMetadata, SafMetadataItem, SafBadge } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function ResponsiveMetadataExample() {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const checkScreenSize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    checkScreenSize();
    window.addEventListener('resize', checkScreenSize);
    
    return () => window.removeEventListener('resize', checkScreenSize);
  }, []);

  return (
    <SafMetadata 
      layout={isMobile ? 'vertical' : 'grid'}
      columns={isMobile ? 1 : 3}
      spacing={isMobile ? 'normal' : 'compact'}
      size={isMobile ? 'small' : 'medium'}
    >
      <SafMetadataItem label="Order ID" value="#ORD-2024-001234" />
      
      <SafMetadataItem label="Status">
        <SafBadge variant="warning">Processing</SafBadge>
      </SafMetadataItem>
      
      <SafMetadataItem label="Total" value="$249.99" />
      
      <SafMetadataItem label="Customer" value="Sarah Johnson" />
      
      <SafMetadataItem label="Date" value="Dec 15, 2024" />
      
      <SafMetadataItem label="Payment">
        <SafBadge variant="success" size="small">Paid</SafBadge>
      </SafMetadataItem>
      
      <SafMetadataItem label="Shipping" value="Express" />
      
      <SafMetadataItem label="Location" value="Chicago, IL" />
      
      <SafMetadataItem label="Items" value="3 products" />
    </SafMetadata>
  );
}
```

#### Angular
```typescript
// Component
import { Component, OnInit, OnDestroy, HostListener } from '@angular/core';

@Component({
  selector: 'app-responsive-metadata',
  template: `
    <saf-metadata 
      [layout]="isMobile ? 'vertical' : 'grid'"
      [columns]="isMobile ? 1 : 3"
      [spacing]="isMobile ? 'normal' : 'compact'"
      [size]="isMobile ? 'small' : 'medium'"
    >
      <saf-metadata-item label="Order ID" value="#ORD-2024-001234"></saf-metadata-item>
      
      <saf-metadata-item label="Status">
        <saf-badge variant="warning">Processing</saf-badge>
      </saf-metadata-item>
      
      <saf-metadata-item label="Total" value="$249.99"></saf-metadata-item>
      
      <saf-metadata-item label="Customer" value="Sarah Johnson"></saf-metadata-item>
      
      <saf-metadata-item label="Date" value="Dec 15, 2024"></saf-metadata-item>
      
      <saf-metadata-item label="Payment">
        <saf-badge variant="success" size="small">Paid</saf-badge>
      </saf-metadata-item>
      
      <saf-metadata-item label="Shipping" value="Express"></saf-metadata-item>
      
      <saf-metadata-item label="Location" value="Chicago, IL"></saf-metadata-item>
      
      <saf-metadata-item label="Items" value="3 products"></saf-metadata-item>
    </saf-metadata>
  `
})
export class ResponsiveMetadataComponent implements OnInit {
  isMobile = false;

  ngOnInit() {
    this.checkScreenSize();
  }

  @HostListener('window:resize', ['$event'])
  onResize() {
    this.checkScreenSize();
  }

  private checkScreenSize() {
    this.isMobile = window.innerWidth < 768;
  }
}
```

## Best Practices

1. **Information Hierarchy**: Organize metadata in logical groups and use appropriate headings
2. **Responsive Design**: Adapt layout and spacing based on screen size
3. **Content Formatting**: Use appropriate components (badges, icons) to enhance readability
4. **Loading States**: Show loading indicators when fetching dynamic metadata
5. **Consistent Labeling**: Use clear, consistent labels for metadata fields
6. **Visual Grouping**: Use spacing, dividers, and borders to group related information
7. **Accessibility**: Ensure proper semantic markup and screen reader support
8. **Performance**: Avoid unnecessary re-renders with large metadata sets

## Accessibility Considerations

- Use semantic HTML structure for metadata organization
- Provide clear labels and descriptions for screen readers
- Ensure sufficient color contrast for all text and components
- Support keyboard navigation through metadata items
- Use ARIA labels when content is not self-describing
- Maintain proper heading hierarchy for grouped content

## Related Components

- `SafMetadataItem`: Individual metadata key-value pairs
- `SafBadge`: For status and category indicators
- `SafIcon`: For visual enhancements and status indicators
- `SafButton`: For interactive elements within metadata
- `SafSpinner`: For loading states

## Notes

- The component automatically handles responsive behavior when layout changes
- Grid layout automatically adjusts column count based on available space
- Use appropriate spacing and sizing for different content densities
- Consider grouping related metadata for better user experience
- Loading states should be handled at the container level for better UX
