# SafSplitter

## Overview

SafSplitter is a two-panel layout component that provides a resizable divider between two content areas. It offers precise control over panel sizing, orientation, visual customization of the splitter handle, and maintains accessibility features for keyboard and screen reader users.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `children` | `[ReactNode, ReactNode]` | - | Two child elements for left/right or top/bottom panels |
| `split` | `'vertical' \| 'horizontal'` | `'vertical'` | Split orientation (vertical = left/right, horizontal = top/bottom) |
| `size` | `number \| string` | `'50%'` | Size of first panel (pixels or percentage) |
| `defaultSize` | `number \| string` | `'50%'` | Default size of first panel |
| `minSize` | `number \| string` | `50` | Minimum size of first panel |
| `maxSize` | `number \| string` | - | Maximum size of first panel |
| `disabled` | `boolean` | `false` | Disable resizing |
| `allowResize` | `boolean` | `true` | Allow resizing |
| `resizerStyle` | `object` | - | Custom styles for resizer |
| `paneStyle` | `object` | - | Custom styles for panes |
| `pane1Style` | `object` | - | Custom styles for first pane |
| `pane2Style` | `object` | - | Custom styles for second pane |
| `onResizeStart` | `() => void` | - | Resize start callback |
| `onResize` | `(size: number) => void` | - | Resize callback |
| `onResizeEnd` | `(size: number) => void` | - | Resize end callback |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `split` | `'vertical' \| 'horizontal'` | `'vertical'` | Split orientation |
| `size` | `number \| string` | `'50%'` | Size of first panel |
| `defaultSize` | `number \| string` | `'50%'` | Default size of first panel |
| `minSize` | `number \| string` | `50` | Minimum size of first panel |
| `maxSize` | `number \| string` | - | Maximum size of first panel |
| `disabled` | `boolean` | `false` | Disable resizing |
| `allowResize` | `boolean` | `true` | Allow resizing |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `resizeStart` | `EventEmitter<void>` | Fired when resize starts |
| `resize` | `EventEmitter<number>` | Fired during resize |
| `resizeEnd` | `EventEmitter<number>` | Fired when resize ends |

## Usage Examples

### Basic Vertical Splitter

```typescript
// React
const BasicVerticalSplitter = () => {
  const [leftPanelSize, setLeftPanelSize] = useState(300);

  const handleResize = (size) => {
    setLeftPanelSize(size);
    console.log('Left panel size:', size);
  };

  return (
    <div className="basic-vertical-splitter">
      <h3>File Explorer with Content</h3>
      
      <SafSplitter
        split="vertical"
        size={leftPanelSize}
        minSize={200}
        maxSize={500}
        onResize={handleResize}
        className="main-splitter"
      >
        <div className="left-panel">
          <div className="panel-header">
            <h4>File Explorer</h4>
            <span className="panel-info">{leftPanelSize}px wide</span>
          </div>
          
          <div className="file-tree">
            <SafTreeView>
              <SafTreeNode
                label="src"
                icon={<SafIcon name="folder" />}
                expandable
                defaultExpanded
              >
                <SafTreeNode
                  label="components"
                  icon={<SafIcon name="folder" />}
                  expandable
                >
                  <SafTreeNode
                    label="Button.tsx"
                    icon={<SafIcon name="file" />}
                  />
                  <SafTreeNode
                    label="Input.tsx"
                    icon={<SafIcon name="file" />}
                  />
                  <SafTreeNode
                    label="Modal.tsx"
                    icon={<SafIcon name="file" />}
                  />
                </SafTreeNode>
                
                <SafTreeNode
                  label="utils"
                  icon={<SafIcon name="folder" />}
                  expandable
                >
                  <SafTreeNode
                    label="helpers.ts"
                    icon={<SafIcon name="file" />}
                  />
                  <SafTreeNode
                    label="constants.ts"
                    icon={<SafIcon name="file" />}
                  />
                </SafTreeNode>
                
                <SafTreeNode
                  label="App.tsx"
                  icon={<SafIcon name="file" />}
                />
                <SafTreeNode
                  label="index.tsx"
                  icon={<SafIcon name="file" />}
                />
              </SafTreeNode>
            </SafTreeView>
          </div>
          
          <div className="panel-footer">
            <SafButton variant="outline" size="small" fullWidth>
              <SafIcon name="folder-plus" size="small" />
              New Folder
            </SafButton>
          </div>
        </div>
        
        <div className="right-panel">
          <div className="panel-header">
            <h4>Code Editor</h4>
            <div className="editor-tabs">
              <div className="tab active">
                <SafIcon name="file" size="small" />
                <span>Button.tsx</span>
                <SafIconButton
                  icon={<SafIcon name="x" />}
                  size="small"
                  variant="ghost"
                />
              </div>
              <div className="tab">
                <SafIcon name="file" size="small" />
                <span>App.tsx</span>
                <SafIconButton
                  icon={<SafIcon name="x" />}
                  size="small"
                  variant="ghost"
                />
              </div>
            </div>
          </div>
          
          <div className="editor-content">
            <div className="code-editor">
              <div className="line-numbers">
                {[...Array(15)].map((_, i) => (
                  <div key={i} className="line-number">{i + 1}</div>
                ))}
              </div>
              
              <div className="code-content">
                <pre>
{`import React from 'react';
import './Button.css';

interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  size?: 'small' | 'medium' | 'large';
  onClick?: () => void;
  disabled?: boolean;
}

export const Button: React.FC<ButtonProps> = ({
  children,
  variant = 'primary',
  size = 'medium',
  onClick,
  disabled = false
}) => {
  return (
    <button
      className={\`btn btn--\${variant} btn--\${size}\`}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
};`}
                </pre>
              </div>
            </div>
          </div>
        </div>
      </SafSplitter>
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-vertical-splitter">
  <h3>File Explorer with Content</h3>
  
  <saf-splitter
    split="vertical"
    [size]="leftPanelSize"
    [minSize]="200"
    [maxSize]="500"
    (resize)="handleResize($event)"
    class="main-splitter">
    
    <div class="left-panel">
      <div class="panel-header">
        <h4>File Explorer</h4>
        <span class="panel-info">{{leftPanelSize}}px wide</span>
      </div>
      
      <div class="file-tree">
        <saf-tree-view>
          <saf-tree-node
            label="src"
            icon="folder"
            [expandable]="true"
            [defaultExpanded]="true">
            
            <saf-tree-node
              label="components"
              icon="folder"
              [expandable]="true">
              <saf-tree-node label="Button.tsx" icon="file"></saf-tree-node>
              <saf-tree-node label="Input.tsx" icon="file"></saf-tree-node>
              <saf-tree-node label="Modal.tsx" icon="file"></saf-tree-node>
            </saf-tree-node>
            
            <saf-tree-node
              label="utils"
              icon="folder"
              [expandable]="true">
              <saf-tree-node label="helpers.ts" icon="file"></saf-tree-node>
              <saf-tree-node label="constants.ts" icon="file"></saf-tree-node>
            </saf-tree-node>
            
            <saf-tree-node label="App.tsx" icon="file"></saf-tree-node>
            <saf-tree-node label="index.tsx" icon="file"></saf-tree-node>
          </saf-tree-node>
        </saf-tree-view>
      </div>
      
      <div class="panel-footer">
        <saf-button variant="outline" size="small" fullWidth>
          <saf-icon name="folder-plus" size="small"></saf-icon>
          New Folder
        </saf-button>
      </div>
    </div>
    
    <div class="right-panel">
      <div class="panel-header">
        <h4>Code Editor</h4>
        <div class="editor-tabs">
          <div class="tab active">
            <saf-icon name="file" size="small"></saf-icon>
            <span>Button.tsx</span>
            <saf-icon-button icon="x" size="small" variant="ghost"></saf-icon-button>
          </div>
          <div class="tab">
            <saf-icon name="file" size="small"></saf-icon>
            <span>App.tsx</span>
            <saf-icon-button icon="x" size="small" variant="ghost"></saf-icon-button>
          </div>
        </div>
      </div>
      
      <div class="editor-content">
        <div class="code-editor">
          <!-- Code content would go here -->
        </div>
      </div>
    </div>
  </saf-splitter>
</div>
```

### Horizontal Splitter with Content Areas

```typescript
// React
const HorizontalContentSplitter = () => {
  const [topPanelSize, setTopPanelSize] = useState('60%');
  const [isResizing, setIsResizing] = useState(false);

  const handleResizeStart = () => {
    setIsResizing(true);
  };

  const handleResizeEnd = (size) => {
    setIsResizing(false);
    setTopPanelSize(typeof size === 'number' ? `${size}px` : size);
  };

  return (
    <div className="horizontal-content-splitter">
      <h3>Dashboard with Activity Log</h3>
      
      <SafSplitter
        split="horizontal"
        size={topPanelSize}
        minSize="40%"
        maxSize="80%"
        onResizeStart={handleResizeStart}
        onResizeEnd={handleResizeEnd}
        resizerStyle={{
          backgroundColor: isResizing ? '#007acc' : '#e1e5e9',
          opacity: isResizing ? 1 : 0.7
        }}
        className="dashboard-splitter"
      >
        <div className="top-panel">
          <div className="panel-header">
            <h4>Dashboard Overview</h4>
            <div className="header-actions">
              <SafButton variant="outline" size="small">
                <SafIcon name="refresh-cw" size="small" />
                Refresh
              </SafButton>
              <SafButton variant="primary" size="small">
                <SafIcon name="settings" size="small" />
                Settings
              </SafButton>
            </div>
          </div>
          
          <div className="dashboard-content">
            <div className="metrics-grid">
              <SafCard className="metric-card">
                <div className="metric-header">
                  <SafIcon name="users" size="medium" color="primary" />
                  <h5>Active Users</h5>
                </div>
                <div className="metric-value">
                  <span className="value">2,847</span>
                  <span className="change positive">
                    <SafIcon name="trending-up" size="small" />
                    +12%
                  </span>
                </div>
                <SafProgressBar value={75} size="small" color="primary" />
              </SafCard>
              
              <SafCard className="metric-card">
                <div className="metric-header">
                  <SafIcon name="activity" size="medium" color="success" />
                  <h5>Sessions</h5>
                </div>
                <div className="metric-value">
                  <span className="value">15,293</span>
                  <span className="change positive">
                    <SafIcon name="trending-up" size="small" />
                    +8%
                  </span>
                </div>
                <SafProgressBar value={82} size="small" color="success" />
              </SafCard>
              
              <SafCard className="metric-card">
                <div className="metric-header">
                  <SafIcon name="dollar-sign" size="medium" color="warning" />
                  <h5>Revenue</h5>
                </div>
                <div className="metric-value">
                  <span className="value">$12,485</span>
                  <span className="change positive">
                    <SafIcon name="trending-up" size="small" />
                    +23%
                  </span>
                </div>
                <SafProgressBar value={68} size="small" color="warning" />
              </SafCard>
              
              <SafCard className="metric-card">
                <div className="metric-header">
                  <SafIcon name="target" size="medium" color="error" />
                  <h5>Conversion</h5>
                </div>
                <div className="metric-value">
                  <span className="value">3.2%</span>
                  <span className="change negative">
                    <SafIcon name="trending-down" size="small" />
                    -2%
                  </span>
                </div>
                <SafProgressBar value={32} size="small" color="error" />
              </SafCard>
            </div>
            
            <div className="charts-section">
              <SafCard>
                <div className="chart-header">
                  <h5>Traffic Overview</h5>
                  <SafDropdown
                    label="Period"
                    value="7d"
                    options={[
                      { value: '24h', label: 'Last 24 hours' },
                      { value: '7d', label: 'Last 7 days' },
                      { value: '30d', label: 'Last 30 days' },
                      { value: '90d', label: 'Last 90 days' }
                    ]}
                  />
                </div>
                <div className="chart-placeholder">
                  <SafIcon name="bar-chart" size="large" color="secondary" />
                  <p>Chart visualization would be rendered here</p>
                </div>
              </SafCard>
            </div>
          </div>
        </div>
        
        <div className="bottom-panel">
          <div className="panel-header">
            <h4>System Activity Log</h4>
            <div className="log-controls">
              <SafButton variant="ghost" size="small">
                <SafIcon name="filter" size="small" />
                Filter
              </SafButton>
              <SafButton variant="ghost" size="small">
                <SafIcon name="download" size="small" />
                Export
              </SafButton>
              <SafButton variant="ghost" size="small">
                <SafIcon name="trash-2" size="small" />
                Clear
              </SafButton>
            </div>
          </div>
          
          <div className="activity-log">
            <div className="log-filters">
              <SafFilterGroup>
                <SafFilterChip label="All" active />
                <SafFilterChip label="Errors" count={3} />
                <SafFilterChip label="Warnings" count={12} />
                <SafFilterChip label="Info" count={45} />
              </SafFilterGroup>
            </div>
            
            <div className="log-entries">
              <div className="log-entry error">
                <div className="log-time">14:32:15</div>
                <div className="log-level">
                  <SafBadge label="ERROR" color="error" size="small" />
                </div>
                <div className="log-message">
                  Failed to connect to database: Connection timeout after 30s
                </div>
                <div className="log-actions">
                  <SafIconButton
                    icon={<SafIcon name="external-link" />}
                    size="small"
                    tooltip="View Details"
                  />
                </div>
              </div>
              
              <div className="log-entry warning">
                <div className="log-time">14:31:42</div>
                <div className="log-level">
                  <SafBadge label="WARN" color="warning" size="small" />
                </div>
                <div className="log-message">
                  High memory usage detected: 89% of available memory in use
                </div>
                <div className="log-actions">
                  <SafIconButton
                    icon={<SafIcon name="external-link" />}
                    size="small"
                    tooltip="View Details"
                  />
                </div>
              </div>
              
              <div className="log-entry info">
                <div className="log-time">14:30:18</div>
                <div className="log-level">
                  <SafBadge label="INFO" color="primary" size="small" />
                </div>
                <div className="log-message">
                  User authentication successful for user: john.doe@company.com
                </div>
                <div className="log-actions">
                  <SafIconButton
                    icon={<SafIcon name="external-link" />}
                    size="small"
                    tooltip="View Details"
                  />
                </div>
              </div>
              
              <div className="log-entry info">
                <div className="log-time">14:29:55</div>
                <div className="log-level">
                  <SafBadge label="INFO" color="primary" size="small" />
                </div>
                <div className="log-message">
                  Scheduled backup completed successfully: 2.3GB backed up
                </div>
                <div className="log-actions">
                  <SafIconButton
                    icon={<SafIcon name="external-link" />}
                    size="small"
                    tooltip="View Details"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </SafSplitter>
    </div>
  );
};
```

### Email Client Splitter Layout

```typescript
// React
const EmailClientSplitter = () => {
  const [folderPanelSize, setFolderPanelSize] = useState(250);
  const [listPanelSize, setListPanelSize] = useState('40%');
  const [selectedEmail, setSelectedEmail] = useState(null);

  const folders = [
    { name: 'Inbox', count: 23, icon: 'inbox', color: 'primary' },
    { name: 'Sent', count: 0, icon: 'send', color: 'secondary' },
    { name: 'Drafts', count: 5, icon: 'edit', color: 'warning' },
    { name: 'Spam', count: 12, icon: 'shield', color: 'error' },
    { name: 'Trash', count: 8, icon: 'trash', color: 'secondary' }
  ];

  const emails = [
    {
      id: 1,
      from: 'Alice Johnson',
      subject: 'Quarterly Review Meeting',
      preview: 'Hi team, I wanted to schedule our quarterly review...',
      time: '3:45 PM',
      unread: true,
      important: true,
      hasAttachment: true
    },
    {
      id: 2,
      from: 'Bob Smith',
      subject: 'Project Timeline Update',
      preview: 'The project timeline has been updated with new milestones...',
      time: '2:30 PM',
      unread: true,
      important: false,
      hasAttachment: false
    },
    {
      id: 3,
      from: 'Carol Wilson',
      subject: 'Design System Guidelines',
      preview: 'Please review the updated design system guidelines...',
      time: '1:15 PM',
      unread: false,
      important: false,
      hasAttachment: true
    }
  ];

  return (
    <div className="email-client-splitter">
      <div className="email-toolbar">
        <div className="toolbar-section">
          <SafButton variant="primary" icon={<SafIcon name="edit" />}>
            Compose
          </SafButton>
          <SafButton variant="outline" icon={<SafIcon name="refresh-cw" />} />
          <SafButton variant="outline" icon={<SafIcon name="archive" />} />
          <SafButton variant="outline" icon={<SafIcon name="trash" />} />
        </div>
        
        <div className="toolbar-section">
          <SafSearchField
            placeholder="Search emails..."
            size="small"
          />
        </div>
        
        <div className="toolbar-section">
          <SafButton variant="ghost" icon={<SafIcon name="settings" />} />
        </div>
      </div>
      
      <SafSplitter
        split="vertical"
        size={folderPanelSize}
        minSize={200}
        maxSize={350}
        onResize={setFolderPanelSize}
        className="main-email-splitter"
      >
        <div className="folders-panel">
          <div className="panel-header">
            <h4>Folders</h4>
          </div>
          
          <div className="folders-list">
            {folders.map(folder => (
              <div key={folder.name} className="folder-item">
                <SafIcon name={folder.icon} size="small" />
                <span className="folder-name">{folder.name}</span>
                {folder.count > 0 && (
                  <SafBadge 
                    label={folder.count.toString()}
                    color={folder.color}
                    size="small"
                  />
                )}
              </div>
            ))}
          </div>
          
          <div className="folder-actions">
            <SafButton variant="outline" size="small" fullWidth>
              <SafIcon name="plus" size="small" />
              New Folder
            </SafButton>
          </div>
          
          <div className="storage-info">
            <h5>Storage</h5>
            <SafProgressBar 
              value={68}
              label="6.8 GB of 10 GB used"
              size="small"
            />
          </div>
        </div>
        
        <div className="content-area">
          <SafSplitter
            split="vertical"
            size={listPanelSize}
            minSize="30%"
            maxSize="70%"
            onResize={setListPanelSize}
            className="content-splitter"
          >
            <div className="email-list-panel">
              <div className="panel-header">
                <h4>Inbox</h4>
                <div className="list-controls">
                  <SafIconButton
                    icon={<SafIcon name="more-vertical" />}
                    size="small"
                  />
                </div>
              </div>
              
              <div className="email-list">
                {emails.map(email => (
                  <div
                    key={email.id}
                    className={`email-item ${email.unread ? 'unread' : ''} ${selectedEmail?.id === email.id ? 'selected' : ''}`}
                    onClick={() => setSelectedEmail(email)}
                  >
                    <div className="email-header">
                      <div className="sender-info">
                        <SafAvatar 
                          name={email.from}
                          size="small"
                        />
                        <span className="sender-name">{email.from}</span>
                      </div>
                      
                      <div className="email-meta">
                        <span className="email-time">{email.time}</span>
                        {email.important && (
                          <SafIcon name="star" size="small" color="warning" />
                        )}
                        {email.hasAttachment && (
                          <SafIcon name="paperclip" size="small" />
                        )}
                      </div>
                    </div>
                    
                    <div className="email-content">
                      <h5 className="email-subject">{email.subject}</h5>
                      <p className="email-preview">{email.preview}</p>
                    </div>
                    
                    {email.unread && (
                      <div className="unread-indicator" />
                    )}
                  </div>
                ))}
              </div>
            </div>
            
            <div className="email-detail-panel">
              {selectedEmail ? (
                <div className="email-detail">
                  <div className="detail-header">
                    <div className="email-subject-info">
                      <h3>{selectedEmail.subject}</h3>
                      {selectedEmail.important && (
                        <SafIcon name="star" color="warning" />
                      )}
                    </div>
                    
                    <div className="email-actions">
                      <SafButton variant="outline" size="small">
                        <SafIcon name="reply" size="small" />
                        Reply
                      </SafButton>
                      <SafButton variant="outline" size="small">
                        <SafIcon name="forward" size="small" />
                        Forward
                      </SafButton>
                      <SafIconButton
                        icon={<SafIcon name="archive" />}
                        size="small"
                        tooltip="Archive"
                      />
                      <SafIconButton
                        icon={<SafIcon name="trash" />}
                        size="small"
                        tooltip="Delete"
                      />
                    </div>
                  </div>
                  
                  <div className="sender-info-detailed">
                    <SafAvatar 
                      name={selectedEmail.from}
                      size="medium"
                    />
                    <div className="sender-details">
                      <h4>{selectedEmail.from}</h4>
                      <p>to: me</p>
                      <span className="email-timestamp">{selectedEmail.time}, Today</span>
                    </div>
                  </div>
                  
                  <div className="email-body">
                    <p>Dear Team,</p>
                    <p>{selectedEmail.preview} This is the full content of the email message that would be displayed with proper formatting and styling.</p>
                    <p>Please let me know your thoughts on this matter and if you have any questions or concerns.</p>
                    <p>Best regards,<br/>{selectedEmail.from}</p>
                  </div>
                  
                  {selectedEmail.hasAttachment && (
                    <div className="email-attachments">
                      <h5>Attachments</h5>
                      <div className="attachment-list">
                        <div className="attachment-item">
                          <SafIcon name="file" />
                          <span>quarterly-report.pdf</span>
                          <SafButton variant="ghost" size="small">
                            <SafIcon name="download" size="small" />
                          </SafButton>
                        </div>
                      </div>
                    </div>
                  )}
                </div>
              ) : (
                <div className="no-email-selected">
                  <SafIcon name="mail" size="large" color="secondary" />
                  <h4>Select an email</h4>
                  <p>Choose an email from the list to view its contents</p>
                </div>
              )}
            </div>
          </SafSplitter>
        </div>
      </SafSplitter>
    </div>
  );
};
```

### Database Query Builder Splitter

```typescript
// React
const DatabaseQueryBuilderSplitter = () => {
  const [schemaSize, setSchemaSize] = useState('25%');
  const [querySize, setQuerySize] = useState('60%');
  const [currentQuery, setCurrentQuery] = useState('');
  const [queryResults, setQueryResults] = useState([]);

  const databaseSchema = [
    {
      name: 'users',
      type: 'table',
      columns: [
        { name: 'id', type: 'INTEGER', primaryKey: true },
        { name: 'email', type: 'VARCHAR(255)', nullable: false },
        { name: 'name', type: 'VARCHAR(100)', nullable: false },
        { name: 'created_at', type: 'TIMESTAMP', nullable: false }
      ]
    },
    {
      name: 'orders',
      type: 'table',
      columns: [
        { name: 'id', type: 'INTEGER', primaryKey: true },
        { name: 'user_id', type: 'INTEGER', foreignKey: 'users.id' },
        { name: 'total', type: 'DECIMAL(10,2)', nullable: false },
        { name: 'status', type: 'VARCHAR(50)', nullable: false },
        { name: 'created_at', type: 'TIMESTAMP', nullable: false }
      ]
    }
  ];

  const executeQuery = () => {
    // Simulate query execution
    const mockResults = [
      { id: 1, email: 'john@example.com', name: 'John Doe', created_at: '2023-01-15' },
      { id: 2, email: 'jane@example.com', name: 'Jane Smith', created_at: '2023-01-16' },
      { id: 3, email: 'bob@example.com', name: 'Bob Johnson', created_at: '2023-01-17' }
    ];
    setQueryResults(mockResults);
  };

  return (
    <div className="db-query-builder-splitter">
      <div className="query-toolbar">
        <h3>Database Query Builder</h3>
        <div className="toolbar-actions">
          <SafButton 
            variant="primary" 
            onClick={executeQuery}
            icon={<SafIcon name="play" />}
          >
            Run Query
          </SafButton>
          <SafButton variant="outline" icon={<SafIcon name="save" />}>
            Save Query
          </SafButton>
          <SafButton variant="outline" icon={<SafIcon name="folder-open" />}>
            Load Query
          </SafButton>
        </div>
      </div>
      
      <SafSplitter
        split="vertical"
        size={schemaSize}
        minSize={200}
        maxSize={400}
        onResize={setSchemaSize}
        className="main-query-splitter"
      >
        <div className="schema-panel">
          <div className="panel-header">
            <h4>Database Schema</h4>
            <SafIconButton
              icon={<SafIcon name="refresh-cw" />}
              size="small"
              tooltip="Refresh Schema"
            />
          </div>
          
          <div className="schema-browser">
            <SafTreeView>
              {databaseSchema.map(table => (
                <SafTreeNode
                  key={table.name}
                  label={table.name}
                  icon={<SafIcon name="table" />}
                  expandable
                  defaultExpanded
                >
                  {table.columns.map(column => (
                    <SafTreeNode
                      key={`${table.name}.${column.name}`}
                      label={
                        <div className="column-info">
                          <span className="column-name">{column.name}</span>
                          <span className="column-type">{column.type}</span>
                          {column.primaryKey && (
                            <SafBadge label="PK" size="small" color="primary" />
                          )}
                          {column.foreignKey && (
                            <SafBadge label="FK" size="small" color="secondary" />
                          )}
                        </div>
                      }
                      icon={<SafIcon name="columns" size="small" />}
                    />
                  ))}
                </SafTreeNode>
              ))}
            </SafTreeView>
          </div>
        </div>
        
        <div className="query-and-results">
          <SafSplitter
            split="horizontal"
            size={querySize}
            minSize="40%"
            maxSize="80%"
            onResize={setQuerySize}
            className="query-results-splitter"
          >
            <div className="query-panel">
              <div className="panel-header">
                <h4>SQL Query</h4>
                <div className="query-controls">
                  <SafButton variant="ghost" size="small">
                    <SafIcon name="code" size="small" />
                    Format
                  </SafButton>
                  <SafButton variant="ghost" size="small">
                    <SafIcon name="check" size="small" />
                    Validate
                  </SafButton>
                </div>
              </div>
              
              <div className="query-editor">
                <SafTextarea
                  value={currentQuery}
                  onChange={setCurrentQuery}
                  placeholder="Enter your SQL query here..."
                  rows={15}
                  className="sql-textarea"
                  fontFamily="monospace"
                />
                
                <div className="query-info">
                  <SafBadge 
                    label={`${currentQuery.length} characters`}
                    size="small"
                    color="secondary"
                  />
                  <SafBadge 
                    label={currentQuery ? 'Modified' : 'Empty'}
                    size="small"
                    color={currentQuery ? 'warning' : 'secondary'}
                  />
                </div>
              </div>
            </div>
            
            <div className="results-panel">
              <div className="panel-header">
                <h4>Query Results</h4>
                <div className="results-controls">
                  {queryResults.length > 0 && (
                    <>
                      <SafBadge 
                        label={`${queryResults.length} rows`}
                        color="success"
                        size="small"
                      />
                      <SafButton variant="ghost" size="small">
                        <SafIcon name="download" size="small" />
                        Export
                      </SafButton>
                    </>
                  )}
                </div>
              </div>
              
              <div className="results-content">
                {queryResults.length > 0 ? (
                  <SafDataTable
                    columns={Object.keys(queryResults[0]).map(key => ({
                      key,
                      title: key.charAt(0).toUpperCase() + key.slice(1).replace('_', ' '),
                      sortable: true
                    }))}
                    data={queryResults}
                    pagination
                    pageSize={10}
                    className="query-results-table"
                  />
                ) : (
                  <div className="no-results">
                    <SafIcon name="database" size="large" color="secondary" />
                    <h5>No Results</h5>
                    <p>Run a query to see results here</p>
                    
                    <div className="sample-queries">
                      <h6>Sample Queries:</h6>
                      <SafButton
                        variant="outline"
                        size="small"
                        onClick={() => setCurrentQuery('SELECT * FROM users LIMIT 10;')}
                      >
                        Select All Users
                      </SafButton>
                      <SafButton
                        variant="outline"
                        size="small"
                        onClick={() => setCurrentQuery('SELECT u.name, COUNT(o.id) as order_count\nFROM users u\nLEFT JOIN orders o ON u.id = o.user_id\nGROUP BY u.id, u.name;')}
                      >
                        Users with Order Count
                      </SafButton>
                    </div>
                  </div>
                )}
              </div>
            </div>
          </SafSplitter>
        </div>
      </SafSplitter>
    </div>
  );
};
```

### Custom Styled Splitter

```typescript
// React
const CustomStyledSplitter = () => {
  const [leftSize, setLeftSize] = useState(400);
  const [isResizing, setIsResizing] = useState(false);

  const customResizerStyle = {
    background: isResizing 
      ? 'linear-gradient(90deg, #007acc, #0095ff)'
      : '#e1e5e9',
    border: isResizing ? '2px solid #007acc' : '1px solid #d1d5db',
    borderRadius: '4px',
    cursor: 'col-resize',
    position: 'relative',
    '::before': {
      content: '""',
      position: 'absolute',
      top: '50%',
      left: '50%',
      transform: 'translate(-50%, -50%)',
      width: '3px',
      height: '20px',
      background: isResizing ? '#fff' : '#6b7280',
      borderRadius: '1px'
    }
  };

  return (
    <div className="custom-styled-splitter">
      <h3>Custom Styled Splitter</h3>
      
      <SafSplitter
        split="vertical"
        size={leftSize}
        minSize={250}
        maxSize={600}
        onResize={setLeftSize}
        onResizeStart={() => setIsResizing(true)}
        onResizeEnd={() => setIsResizing(false)}
        resizerStyle={customResizerStyle}
        pane1Style={{
          background: '#f8f9fa',
          border: '1px solid #e9ecef',
          borderRadius: '8px 0 0 8px'
        }}
        pane2Style={{
          background: '#ffffff',
          border: '1px solid #e9ecef',
          borderRadius: '0 8px 8px 0'
        }}
        className="styled-splitter"
      >
        <div className="styled-left-panel">
          <div className="styled-panel-header">
            <h4>Styled Left Panel</h4>
            <SafBadge 
              label={`${leftSize}px`}
              color="primary"
              size="small"
            />
          </div>
          
          <div className="styled-panel-content">
            <SafCard>
              <h5>Custom Styling Features</h5>
              <ul>
                <li>Custom resizer appearance</li>
                <li>Rounded panel corners</li>
                <li>Different background colors</li>
                <li>Smooth transitions</li>
                <li>Interactive hover effects</li>
              </ul>
            </SafCard>
            
            <SafCard>
              <h5>Resize Status</h5>
              <div className="status-indicator">
                <SafBadge 
                  label={isResizing ? 'Resizing...' : 'Static'}
                  color={isResizing ? 'warning' : 'success'}
                />
                <SafProgressBar 
                  value={(leftSize - 250) / (600 - 250) * 100}
                  label={`${Math.round((leftSize - 250) / (600 - 250) * 100)}% of range`}
                />
              </div>
            </SafCard>
          </div>
        </div>
        
        <div className="styled-right-panel">
          <div className="styled-panel-header">
            <h4>Styled Right Panel</h4>
            <SafIconButton
              icon={<SafIcon name="settings" />}
              size="small"
            />
          </div>
          
          <div className="styled-panel-content">
            <div className="content-section">
              <h5>Dynamic Content Area</h5>
              <p>This panel adapts its width based on the splitter position. The custom styling includes:</p>
              
              <div className="feature-list">
                <div className="feature-item">
                  <SafIcon name="palette" color="primary" />
                  <span>Custom color scheme</span>
                </div>
                <div className="feature-item">
                  <SafIcon name="move" color="secondary" />
                  <span>Smooth resize animations</span>
                </div>
                <div className="feature-item">
                  <SafIcon name="eye" color="success" />
                  <span>Visual feedback states</span>
                </div>
                <div className="feature-item">
                  <SafIcon name="layers" color="warning" />
                  <span>Layered panel styling</span>
                </div>
              </div>
            </div>
            
            <div className="content-section">
              <h5>Panel Statistics</h5>
              <SafCard variant="outline">
                <div className="stat-grid">
                  <div className="stat-item">
                    <label>Left Panel Width:</label>
                    <span>{leftSize}px</span>
                  </div>
                  <div className="stat-item">
                    <label>Right Panel Width:</label>
                    <span>{window.innerWidth - leftSize - 10}px</span>
                  </div>
                  <div className="stat-item">
                    <label>Resize State:</label>
                    <span>{isResizing ? 'Active' : 'Inactive'}</span>
                  </div>
                  <div className="stat-item">
                    <label>Total Width:</label>
                    <span>{window.innerWidth}px</span>
                  </div>
                </div>
              </SafCard>
            </div>
          </div>
        </div>
      </SafSplitter>
    </div>
  );
};
```

## Best Practices

### Layout Planning
- **Content Organization**: Plan content hierarchy before implementing splitter layouts
- **Size Constraints**: Set appropriate minimum and maximum sizes for usability
- **Responsive Design**: Consider how splitters behave on different screen sizes
- **Visual Balance**: Maintain visual balance between panel contents

### Performance Optimization
- **Efficient Rendering**: Minimize re-renders during resize operations
- **Debounced Events**: Use debouncing for expensive resize event handlers
- **Memory Management**: Clean up event listeners properly
- **Layout Calculations**: Optimize layout calculations for smooth performance

### User Experience
- **Visual Feedback**: Provide clear visual feedback during resize operations
- **Intuitive Controls**: Make resize handles discoverable and easy to use
- **Consistent Behavior**: Maintain consistent resize behavior across the application
- **Accessibility**: Ensure keyboard and screen reader accessibility

### Implementation
- **Component Structure**: Keep panel content components independent and reusable
- **State Management**: Handle size state appropriately for your use case
- **Error Handling**: Implement error boundaries for robust operation
- **Testing**: Test resize behavior across different browsers and devices

## Accessibility Considerations

- Uses proper ARIA roles and labels for splitter functionality
- Supports keyboard navigation for resizing with arrow keys
- Provides screen reader announcements for size changes
- Maintains proper focus management during resize operations
- Uses semantic HTML structure within panels
- Supports high contrast mode with clear visual indicators
- Respects reduced motion preferences for smooth transitions

## Related Components

- **SafResizablePanel**: Multi-panel resizable layout component
- **SafTabs**: Tab-based content organization
- **SafDrawer**: Slide-out panel component
- **SafModal**: Overlay-based content display

## Notes

- SafSplitter automatically handles mouse and touch events for resizing
- The component supports both pixel and percentage-based sizing
- Custom styling can be applied to both panels and the resizer handle
- Resize constraints are enforced during all resize operations
- The component maintains responsive behavior across different screen sizes
- Accessibility features provide comprehensive keyboard and screen reader support
- Performance is optimized for smooth resize operations
- The component works well for two-panel layouts like file explorers, email clients, and code editors
