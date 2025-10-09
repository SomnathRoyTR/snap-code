# SafResizablePanel

## Overview

SafResizablePanel is a flexible layout component that allows users to interactively resize panel sections within a container. It supports horizontal and vertical resizing, minimum and maximum size constraints, persistence of panel sizes, and accessibility features for keyboard-based resizing.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `children` | `ReactNode \| ReactNode[]` | - | Panel content (multiple children create multiple panels) |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | Resize direction |
| `defaultSizes` | `number[]` | `[]` | Default panel sizes (percentages) |
| `sizes` | `number[]` | - | Controlled panel sizes |
| `onResize` | `(sizes: number[]) => void` | - | Resize event handler |
| `onResizeStart` | `(panelIndex: number) => void` | - | Resize start handler |
| `onResizeEnd` | `(panelIndex: number, sizes: number[]) => void` | - | Resize end handler |
| `minSizes` | `number[]` | `[10]` | Minimum panel sizes (percentages) |
| `maxSizes` | `number[]` | `[90]` | Maximum panel sizes (percentages) |
| `disabled` | `boolean \| boolean[]` | `false` | Disable resizing for all or specific panels |
| `resizerStyle` | `object` | - | Custom resizer handle styles |
| `split` | `boolean` | `true` | Enable split functionality |
| `allowResize` | `boolean` | `true` | Allow resizing |
| `storage` | `'localStorage' \| 'sessionStorage' \| null` | `null` | Persist panel sizes |
| `storageKey` | `string` | `'resizable-panel-sizes'` | Storage key for persistence |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | Resize direction |
| `defaultSizes` | `number[]` | `[]` | Default panel sizes (percentages) |
| `sizes` | `number[]` | - | Controlled panel sizes |
| `minSizes` | `number[]` | `[10]` | Minimum panel sizes (percentages) |
| `maxSizes` | `number[]` | `[90]` | Maximum panel sizes (percentages) |
| `disabled` | `boolean \| boolean[]` | `false` | Disable resizing for all or specific panels |
| `split` | `boolean` | `true` | Enable split functionality |
| `allowResize` | `boolean` | `true` | Allow resizing |
| `storage` | `'localStorage' \| 'sessionStorage' \| null` | `null` | Persist panel sizes |
| `storageKey` | `string` | `'resizable-panel-sizes'` | Storage key for persistence |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `resize` | `EventEmitter<number[]>` | Fired when panels are resized |
| `resizeStart` | `EventEmitter<number>` | Fired when resize starts |
| `resizeEnd` | `EventEmitter<{panelIndex: number, sizes: number[]}>` | Fired when resize ends |

## Usage Examples

### Basic Horizontal Resizable Panels

```typescript
// React
const BasicHorizontalResizablePanels = () => {
  const [panelSizes, setPanelSizes] = useState([30, 70]);

  const handleResize = (sizes) => {
    setPanelSizes(sizes);
    console.log('Panel sizes changed:', sizes);
  };

  return (
    <div className="basic-horizontal-resizable">
      <h3>Horizontal Resizable Panels</h3>
      
      <SafResizablePanel
        direction="horizontal"
        defaultSizes={panelSizes}
        onResize={handleResize}
        minSizes={[20, 20]}
        maxSizes={[80, 80]}
        className="horizontal-panels"
      >
        <div className="panel left-panel">
          <div className="panel-header">
            <h4>Navigation Panel</h4>
            <span className="panel-size">{panelSizes[0].toFixed(1)}%</span>
          </div>
          
          <SafNavigation>
            <SafNavigationItem icon={<SafIcon name="home" />} label="Dashboard" active />
            <SafNavigationItem icon={<SafIcon name="users" />} label="Users" />
            <SafNavigationItem icon={<SafIcon name="settings" />} label="Settings" />
            <SafNavigationItem icon={<SafIcon name="help-circle" />} label="Help" />
          </SafNavigation>
          
          <div className="panel-footer">
            <SafButton 
              variant="outline" 
              size="small"
              icon={<SafIcon name="menu" />}
            >
              Toggle Menu
            </SafButton>
          </div>
        </div>
        
        <div className="panel right-panel">
          <div className="panel-header">
            <h4>Main Content</h4>
            <span className="panel-size">{panelSizes[1].toFixed(1)}%</span>
          </div>
          
          <div className="panel-content">
            <p>This is the main content area that can be resized by dragging the panel divider.</p>
            
            <div className="content-cards">
              <SafCard>
                <h5>Recent Activity</h5>
                <SafList>
                  <SafListItem>User John logged in</SafListItem>
                  <SafListItem>Report generated</SafListItem>
                  <SafListItem>Settings updated</SafListItem>
                </SafList>
              </SafCard>
              
              <SafCard>
                <h5>System Status</h5>
                <div className="status-indicators">
                  <SafBadge label="API Server" color="success" />
                  <SafBadge label="Database" color="success" />
                  <SafBadge label="Cache" color="warning" />
                </div>
              </SafCard>
            </div>
          </div>
        </div>
      </SafResizablePanel>
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-horizontal-resizable">
  <h3>Horizontal Resizable Panels</h3>
  
  <saf-resizable-panel
    direction="horizontal"
    [defaultSizes]="[30, 70]"
    [minSizes]="[20, 20]"
    [maxSizes]="[80, 80]"
    (resize)="handleResize($event)"
    class="horizontal-panels">
    
    <div class="panel left-panel">
      <div class="panel-header">
        <h4>Navigation Panel</h4>
        <span class="panel-size">{{panelSizes[0] | number:'1.1-1'}}%</span>
      </div>
      
      <saf-navigation>
        <saf-navigation-item 
          icon="home" 
          label="Dashboard" 
          [active]="true">
        </saf-navigation-item>
        <saf-navigation-item icon="users" label="Users"></saf-navigation-item>
        <saf-navigation-item icon="settings" label="Settings"></saf-navigation-item>
        <saf-navigation-item icon="help-circle" label="Help"></saf-navigation-item>
      </saf-navigation>
      
      <div class="panel-footer">
        <saf-button 
          variant="outline" 
          size="small">
          <saf-icon name="menu"></saf-icon>
          Toggle Menu
        </saf-button>
      </div>
    </div>
    
    <div class="panel right-panel">
      <div class="panel-header">
        <h4>Main Content</h4>
        <span class="panel-size">{{panelSizes[1] | number:'1.1-1'}}%</span>
      </div>
      
      <div class="panel-content">
        <p>This is the main content area that can be resized by dragging the panel divider.</p>
        
        <div class="content-cards">
          <saf-card>
            <h5>Recent Activity</h5>
            <saf-list>
              <saf-list-item>User John logged in</saf-list-item>
              <saf-list-item>Report generated</saf-list-item>
              <saf-list-item>Settings updated</saf-list-item>
            </saf-list>
          </saf-card>
          
          <saf-card>
            <h5>System Status</h5>
            <div class="status-indicators">
              <saf-badge label="API Server" color="success"></saf-badge>
              <saf-badge label="Database" color="success"></saf-badge>
              <saf-badge label="Cache" color="warning"></saf-badge>
            </div>
          </saf-card>
        </div>
      </div>
    </div>
  </saf-resizable-panel>
</div>
```

### Vertical Resizable Panels

```typescript
// React
const VerticalResizablePanels = () => {
  const [panelSizes, setPanelSizes] = useState([40, 35, 25]);

  const handleResizeStart = (panelIndex) => {
    console.log('Started resizing panel:', panelIndex);
  };

  const handleResizeEnd = (panelIndex, sizes) => {
    console.log('Finished resizing panel:', panelIndex, 'New sizes:', sizes);
    setPanelSizes(sizes);
  };

  return (
    <div className="vertical-resizable-panels">
      <h3>Vertical Layout Dashboard</h3>
      
      <SafResizablePanel
        direction="vertical"
        defaultSizes={panelSizes}
        onResizeStart={handleResizeStart}
        onResizeEnd={handleResizeEnd}
        minSizes={[25, 20, 15]}
        maxSizes={[60, 55, 40]}
        className="vertical-panels"
      >
        <div className="panel header-panel">
          <div className="panel-header">
            <h4>Header Section</h4>
            <span className="panel-size">{panelSizes[0].toFixed(1)}%</span>
          </div>
          
          <div className="dashboard-header">
            <div className="header-stats">
              <div className="stat-card">
                <SafIcon name="users" size="large" color="primary" />
                <div className="stat-info">
                  <span className="stat-value">1,234</span>
                  <span className="stat-label">Active Users</span>
                </div>
              </div>
              
              <div className="stat-card">
                <SafIcon name="activity" size="large" color="success" />
                <div className="stat-info">
                  <span className="stat-value">5,678</span>
                  <span className="stat-label">Sessions</span>
                </div>
              </div>
              
              <div className="stat-card">
                <SafIcon name="trending-up" size="large" color="warning" />
                <div className="stat-info">
                  <span className="stat-value">23%</span>
                  <span className="stat-label">Growth</span>
                </div>
              </div>
            </div>
            
            <div className="header-actions">
              <SafButton variant="primary" icon={<SafIcon name="plus" />}>
                Add New
              </SafButton>
              <SafButton variant="outline" icon={<SafIcon name="download" />}>
                Export
              </SafButton>
            </div>
          </div>
        </div>
        
        <div className="panel content-panel">
          <div className="panel-header">
            <h4>Main Content</h4>
            <span className="panel-size">{panelSizes[1].toFixed(1)}%</span>
          </div>
          
          <div className="content-area">
            <SafTabs defaultActiveTab="overview">
              <SafTab id="overview" label="Overview">
                <div className="overview-content">
                  <div className="chart-placeholder">
                    <SafIcon name="bar-chart-2" size="large" />
                    <p>Analytics Chart Would Go Here</p>
                  </div>
                </div>
              </SafTab>
              
              <SafTab id="data" label="Data">
                <SafDataTable
                  columns={[
                    { key: 'name', title: 'Name' },
                    { key: 'value', title: 'Value' },
                    { key: 'status', title: 'Status' }
                  ]}
                  data={[
                    { name: 'Item 1', value: 100, status: 'Active' },
                    { name: 'Item 2', value: 200, status: 'Pending' },
                    { name: 'Item 3', value: 150, status: 'Active' }
                  ]}
                />
              </SafTab>
              
              <SafTab id="settings" label="Settings">
                <div className="settings-content">
                  <p>Configuration options would be displayed here.</p>
                </div>
              </SafTab>
            </SafTabs>
          </div>
        </div>
        
        <div className="panel footer-panel">
          <div className="panel-header">
            <h4>Activity Log</h4>
            <span className="panel-size">{panelSizes[2].toFixed(1)}%</span>
          </div>
          
          <div className="activity-log">
            <div className="log-entry">
              <SafIcon name="info" size="small" color="primary" />
              <span className="log-time">10:30 AM</span>
              <span className="log-message">System started successfully</span>
            </div>
            
            <div className="log-entry">
              <SafIcon name="alert-triangle" size="small" color="warning" />
              <span className="log-time">10:25 AM</span>
              <span className="log-message">High memory usage detected</span>
            </div>
            
            <div className="log-entry">
              <SafIcon name="check-circle" size="small" color="success" />
              <span className="log-time">10:20 AM</span>
              <span className="log-message">Backup completed</span>
            </div>
          </div>
        </div>
      </SafResizablePanel>
    </div>
  );
};
```

### Multi-Panel IDE Layout

```typescript
// React
const IDELayoutResizablePanels = () => {
  const [panelSizes, setPanelSizes] = useState([25, 50, 25]);
  const [verticalSizes, setVerticalSizes] = useState([70, 30]);
  const [selectedFile, setSelectedFile] = useState('App.tsx');

  const fileTree = [
    {
      name: 'src',
      type: 'folder',
      children: [
        { name: 'App.tsx', type: 'file', size: '2.1 KB' },
        { name: 'index.tsx', type: 'file', size: '0.5 KB' },
        { name: 'styles.css', type: 'file', size: '1.8 KB' }
      ]
    },
    {
      name: 'public',
      type: 'folder',
      children: [
        { name: 'index.html', type: 'file', size: '1.2 KB' },
        { name: 'favicon.ico', type: 'file', size: '15.1 KB' }
      ]
    }
  ];

  const renderFileTree = (files) => (
    <SafTreeView>
      {files.map(file => (
        <SafTreeNode
          key={file.name}
          label={file.name}
          icon={<SafIcon name={file.type === 'folder' ? 'folder' : 'file'} />}
          expandable={file.type === 'folder'}
        >
          {file.children && renderFileTree(file.children)}
        </SafTreeNode>
      ))}
    </SafTreeView>
  );

  return (
    <div className="ide-layout-resizable">
      <div className="ide-header">
        <h3>Code Editor IDE</h3>
        <div className="ide-controls">
          <SafButton variant="ghost" size="small" icon={<SafIcon name="play" />} />
          <SafButton variant="ghost" size="small" icon={<SafIcon name="stop" />} />
          <SafButton variant="ghost" size="small" icon={<SafIcon name="save" />} />
        </div>
      </div>
      
      <SafResizablePanel
        direction="horizontal"
        defaultSizes={panelSizes}
        onResize={setPanelSizes}
        minSizes={[15, 30, 15]}
        maxSizes={[40, 80, 40]}
        storage="localStorage"
        storageKey="ide-horizontal-panels"
        className="ide-main-panels"
      >
        {/* File Explorer Panel */}
        <div className="panel file-explorer-panel">
          <div className="panel-header">
            <h4>Explorer</h4>
            <SafIconButton
              icon={<SafIcon name="refresh-cw" />}
              size="small"
              tooltip="Refresh"
            />
          </div>
          
          <div className="file-explorer">
            <div className="explorer-section">
              <h5>Files</h5>
              {renderFileTree(fileTree)}
            </div>
            
            <div className="explorer-section">
              <h5>Search</h5>
              <SafSearchField
                placeholder="Search files..."
                size="small"
              />
            </div>
          </div>
        </div>
        
        {/* Editor Panel */}
        <div className="panel editor-panel">
          <SafResizablePanel
            direction="vertical"
            defaultSizes={verticalSizes}
            onResize={setVerticalSizes}
            minSizes={[50, 20]}
            maxSizes={[85, 50]}
            className="editor-vertical-panels"
          >
            <div className="panel code-editor-panel">
              <div className="editor-tabs">
                <SafTabs activeTab={selectedFile} onTabChange={setSelectedFile}>
                  <SafTab
                    id="App.tsx"
                    label="App.tsx"
                    closable
                    icon={<SafIcon name="file" size="small" />}
                  />
                  <SafTab
                    id="index.tsx"
                    label="index.tsx"
                    closable
                    icon={<SafIcon name="file" size="small" />}
                  />
                </SafTabs>
              </div>
              
              <div className="code-editor">
                <div className="code-content">
                  <div className="line-numbers">
                    {[...Array(20)].map((_, i) => (
                      <div key={i} className="line-number">{i + 1}</div>
                    ))}
                  </div>
                  <div className="code-text">
                    <pre>
{`import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1>Hello World</h1>
        <p>Welcome to the IDE!</p>
      </header>
    </div>
  );
}

export default App;`}
                    </pre>
                  </div>
                </div>
              </div>
            </div>
            
            <div className="panel console-panel">
              <div className="panel-header">
                <h4>Console</h4>
                <div className="console-controls">
                  <SafButton variant="ghost" size="small" icon={<SafIcon name="trash-2" />}>
                    Clear
                  </SafButton>
                </div>
              </div>
              
              <div className="console-output">
                <div className="console-line">
                  <span className="console-prompt">$</span>
                  <span className="console-text">npm start</span>
                </div>
                <div className="console-line info">
                  <SafIcon name="info" size="small" />
                  <span>Starting development server...</span>
                </div>
                <div className="console-line success">
                  <SafIcon name="check-circle" size="small" />
                  <span>Server started on http://localhost:3000</span>
                </div>
              </div>
            </div>
          </SafResizablePanel>
        </div>
        
        {/* Properties Panel */}
        <div className="panel properties-panel">
          <div className="panel-header">
            <h4>Properties</h4>
          </div>
          
          <div className="properties-content">
            <div className="property-section">
              <h5>File Info</h5>
              <div className="property-item">
                <label>Name:</label>
                <span>{selectedFile}</span>
              </div>
              <div className="property-item">
                <label>Size:</label>
                <span>2.1 KB</span>
              </div>
              <div className="property-item">
                <label>Type:</label>
                <span>TypeScript</span>
              </div>
            </div>
            
            <div className="property-section">
              <h5>Editor Settings</h5>
              <SafCheckbox label="Word wrap" defaultChecked />
              <SafCheckbox label="Line numbers" defaultChecked />
              <SafCheckbox label="Syntax highlighting" defaultChecked />
            </div>
            
            <div className="property-section">
              <h5>Quick Actions</h5>
              <SafButton variant="outline" size="small" fullWidth>
                Format Document
              </SafButton>
              <SafButton variant="outline" size="small" fullWidth>
                Find & Replace
              </SafButton>
            </div>
          </div>
        </div>
      </SafResizablePanel>
    </div>
  );
};
```

### Email Client Layout

```typescript
// React
const EmailClientResizablePanels = () => {
  const [folderPanelSize, setFolderPanelSize] = useState(25);
  const [contentSizes, setContentSizes] = useState([40, 60]);
  const [selectedEmail, setSelectedEmail] = useState(null);

  const folders = [
    { name: 'Inbox', count: 12, icon: 'inbox' },
    { name: 'Sent', count: 45, icon: 'send' },
    { name: 'Drafts', count: 3, icon: 'edit' },
    { name: 'Spam', count: 8, icon: 'shield' },
    { name: 'Trash', count: 2, icon: 'trash' }
  ];

  const emails = [
    {
      id: 1,
      from: 'John Smith',
      subject: 'Project Update Meeting',
      preview: 'Hi team, I wanted to schedule a meeting to discuss...',
      time: '2:30 PM',
      unread: true,
      important: true
    },
    {
      id: 2,
      from: 'Sarah Wilson',
      subject: 'Design Review Feedback',
      preview: 'The latest design looks great! I have a few suggestions...',
      time: '1:15 PM',
      unread: true,
      important: false
    },
    {
      id: 3,
      from: 'Mike Johnson',
      subject: 'Weekly Report',
      preview: 'Please find attached the weekly performance report...',
      time: '11:45 AM',
      unread: false,
      important: false
    }
  ];

  return (
    <div className="email-client-resizable">
      <div className="email-header">
        <div className="email-title">
          <h3>Mail Client</h3>
          <SafBadge label="12 unread" color="primary" />
        </div>
        
        <div className="email-actions">
          <SafButton variant="primary" icon={<SafIcon name="edit" />}>
            Compose
          </SafButton>
          <SafButton variant="outline" icon={<SafIcon name="refresh-cw" />} />
          <SafButton variant="outline" icon={<SafIcon name="settings" />} />
        </div>
      </div>
      
      <SafResizablePanel
        direction="horizontal"
        defaultSizes={[folderPanelSize, 100 - folderPanelSize]}
        onResize={([folderSize, contentSize]) => {
          setFolderPanelSize(folderSize);
        }}
        minSizes={[20, 60]}
        maxSizes={[35, 80]}
        className="email-main-panels"
      >
        {/* Folders Panel */}
        <div className="panel folders-panel">
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
                    size="small"
                    color={folder.name === 'Inbox' ? 'primary' : 'secondary'}
                  />
                )}
              </div>
            ))}
          </div>
          
          <div className="folders-footer">
            <SafButton variant="outline" size="small" fullWidth>
              <SafIcon name="plus" size="small" />
              New Folder
            </SafButton>
          </div>
        </div>
        
        {/* Content Panel */}
        <div className="panel content-panel">
          <SafResizablePanel
            direction="horizontal"
            defaultSizes={contentSizes}
            onResize={setContentSizes}
            minSizes={[30, 35]}
            maxSizes={[65, 70]}
            className="content-sub-panels"
          >
            {/* Email List Panel */}
            <div className="panel email-list-panel">
              <div className="panel-header">
                <h4>Inbox</h4>
                <div className="email-list-controls">
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
              
              <div className="email-list">
                {emails.map(email => (
                  <div
                    key={email.id}
                    className={`email-item ${email.unread ? 'unread' : ''} ${selectedEmail?.id === email.id ? 'selected' : ''}`}
                    onClick={() => setSelectedEmail(email)}
                  >
                    <div className="email-sender">
                      <SafAvatar name={email.from} size="small" />
                      <div className="sender-info">
                        <span className="sender-name">{email.from}</span>
                        <span className="email-time">{email.time}</span>
                      </div>
                      {email.important && (
                        <SafIcon name="star" size="small" color="warning" />
                      )}
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
            
            {/* Email Details Panel */}
            <div className="panel email-details-panel">
              {selectedEmail ? (
                <div className="email-details">
                  <div className="email-details-header">
                    <div className="email-subject-line">
                      <h4>{selectedEmail.subject}</h4>
                      {selectedEmail.important && (
                        <SafIcon name="star" color="warning" />
                      )}
                    </div>
                    
                    <div className="email-actions">
                      <SafIconButton
                        icon={<SafIcon name="reply" />}
                        tooltip="Reply"
                      />
                      <SafIconButton
                        icon={<SafIcon name="reply-all" />}
                        tooltip="Reply All"
                      />
                      <SafIconButton
                        icon={<SafIcon name="forward" />}
                        tooltip="Forward"
                      />
                      <SafIconButton
                        icon={<SafIcon name="archive" />}
                        tooltip="Archive"
                      />
                      <SafIconButton
                        icon={<SafIcon name="trash" />}
                        tooltip="Delete"
                      />
                    </div>
                  </div>
                  
                  <div className="email-meta">
                    <div className="sender-details">
                      <SafAvatar name={selectedEmail.from} size="medium" />
                      <div className="sender-text">
                        <span className="sender-name">{selectedEmail.from}</span>
                        <span className="sender-email">to: me</span>
                        <span className="email-timestamp">{selectedEmail.time}, Today</span>
                      </div>
                    </div>
                  </div>
                  
                  <div className="email-body">
                    <p>Hi there,</p>
                    <p>{selectedEmail.preview} This is the full content of the email that would be displayed here with proper formatting and styling.</p>
                    <p>Let me know if you have any questions or need clarification on any points discussed.</p>
                    <p>Best regards,<br/>{selectedEmail.from}</p>
                  </div>
                  
                  <div className="email-attachments">
                    <h5>Attachments</h5>
                    <div className="attachment-item">
                      <SafIcon name="paperclip" />
                      <span>project-update.pdf</span>
                      <SafButton variant="ghost" size="small">Download</SafButton>
                    </div>
                  </div>
                </div>
              ) : (
                <div className="no-email-selected">
                  <SafIcon name="mail" size="large" color="secondary" />
                  <h4>No email selected</h4>
                  <p>Select an email from the list to view its contents</p>
                </div>
              )}
            </div>
          </SafResizablePanel>
        </div>
      </SafResizablePanel>
    </div>
  );
};
```

### Persistent Resizable Panels with Settings

```typescript
// React
const PersistentResizablePanels = () => {
  const [panelSizes, setPanelSizes] = useState([25, 50, 25]);
  const [resizeEnabled, setResizeEnabled] = useState(true);
  const [showPanelSizes, setShowPanelSizes] = useState(true);
  const [minConstraints, setMinConstraints] = useState([15, 20, 15]);
  const [maxConstraints, setMaxConstraints] = useState([40, 60, 40]);

  const resetPanelSizes = () => {
    const defaultSizes = [25, 50, 25];
    setPanelSizes(defaultSizes);
    // Clear from storage
    localStorage.removeItem('persistent-panel-sizes');
  };

  const handlePanelResize = (sizes) => {
    setPanelSizes(sizes);
    if (showPanelSizes) {
      console.log('Panel sizes updated:', sizes.map(s => `${s.toFixed(1)}%`).join(', '));
    }
  };

  return (
    <div className="persistent-resizable-panels">
      <div className="persistent-header">
        <h3>Persistent Resizable Panels</h3>
        
        <div className="panel-controls">
          <SafCheckbox
            label="Enable Resize"
            checked={resizeEnabled}
            onChange={(checked) => setResizeEnabled(checked)}
          />
          
          <SafCheckbox
            label="Show Panel Sizes"
            checked={showPanelSizes}
            onChange={(checked) => setShowPanelSizes(checked)}
          />
          
          <SafButton
            variant="outline"
            size="small"
            onClick={resetPanelSizes}
            icon={<SafIcon name="refresh-ccw" />}
          >
            Reset Layout
          </SafButton>
        </div>
      </div>
      
      {showPanelSizes && (
        <div className="panel-size-display">
          <SafBadge 
            label={`Left: ${panelSizes[0].toFixed(1)}%`}
            color="primary"
          />
          <SafBadge 
            label={`Center: ${panelSizes[1].toFixed(1)}%`}
            color="secondary"
          />
          <SafBadge 
            label={`Right: ${panelSizes[2].toFixed(1)}%`}
            color="success"
          />
        </div>
      )}
      
      <SafResizablePanel
        direction="horizontal"
        sizes={panelSizes}
        onResize={handlePanelResize}
        minSizes={minConstraints}
        maxSizes={maxConstraints}
        allowResize={resizeEnabled}
        storage="localStorage"
        storageKey="persistent-panel-sizes"
        className="persistent-panels"
      >
        <div className="panel settings-panel">
          <div className="panel-header">
            <h4>Panel Settings</h4>
          </div>
          
          <div className="settings-content">
            <div className="setting-group">
              <h5>Resize Constraints</h5>
              
              <div className="constraint-controls">
                <label>Minimum Sizes (%):</label>
                <div className="constraint-inputs">
                  <SafTextInput
                    type="number"
                    value={minConstraints[0]}
                    onChange={(value) => setMinConstraints([+value, minConstraints[1], minConstraints[2]])}
                    min={5}
                    max={30}
                    size="small"
                  />
                  <SafTextInput
                    type="number"
                    value={minConstraints[1]}
                    onChange={(value) => setMinConstraints([minConstraints[0], +value, minConstraints[2]])}
                    min={10}
                    max={40}
                    size="small"
                  />
                  <SafTextInput
                    type="number"
                    value={minConstraints[2]}
                    onChange={(value) => setMinConstraints([minConstraints[0], minConstraints[1], +value])}
                    min={5}
                    max={30}
                    size="small"
                  />
                </div>
              </div>
              
              <div className="constraint-controls">
                <label>Maximum Sizes (%):</label>
                <div className="constraint-inputs">
                  <SafTextInput
                    type="number"
                    value={maxConstraints[0]}
                    onChange={(value) => setMaxConstraints([+value, maxConstraints[1], maxConstraints[2]])}
                    min={30}
                    max={70}
                    size="small"
                  />
                  <SafTextInput
                    type="number"
                    value={maxConstraints[1]}
                    onChange={(value) => setMaxConstraints([maxConstraints[0], +value, maxConstraints[2]])}
                    min={40}
                    max={80}
                    size="small"
                  />
                  <SafTextInput
                    type="number"
                    value={maxConstraints[2]}
                    onChange={(value) => setMaxConstraints([maxConstraints[0], maxConstraints[1], +value])}
                    min={30}
                    max={70}
                    size="small"
                  />
                </div>
              </div>
            </div>
            
            <div className="setting-group">
              <h5>Panel Actions</h5>
              <SafButton
                variant="outline"
                size="small"
                fullWidth
                onClick={() => setPanelSizes([33.33, 33.33, 33.33])}
              >
                Equal Panels
              </SafButton>
              <SafButton
                variant="outline"
                size="small"
                fullWidth
                onClick={() => setPanelSizes([20, 60, 20])}
              >
                Focus Center
              </SafButton>
            </div>
          </div>
        </div>
        
        <div className="panel main-content-panel">
          <div className="panel-header">
            <h4>Main Content Area</h4>
          </div>
          
          <div className="main-content">
            <div className="content-section">
              <h5>Resizable Panel Demo</h5>
              <p>This is the main content area that can be resized by dragging the panel dividers on either side.</p>
              
              <div className="demo-features">
                <div className="feature-item">
                  <SafIcon name="save" color="success" />
                  <span>Panel sizes are automatically saved to localStorage</span>
                </div>
                
                <div className="feature-item">
                  <SafIcon name="move" color="primary" />
                  <span>Drag the panel dividers to resize</span>
                </div>
                
                <div className="feature-item">
                  <SafIcon name="settings" color="secondary" />
                  <span>Configurable minimum and maximum constraints</span>
                </div>
                
                <div className="feature-item">
                  <SafIcon name="eye" color="warning" />
                  <span>Real-time size feedback and controls</span>
                </div>
              </div>
            </div>
            
            <div className="content-section">
              <h5>Layout Information</h5>
              <SafCard>
                <div className="layout-info">
                  <div className="info-row">
                    <label>Current Layout:</label>
                    <span>Horizontal Triple Panel</span>
                  </div>
                  <div className="info-row">
                    <label>Resize Enabled:</label>
                    <span>{resizeEnabled ? 'Yes' : 'No'}</span>
                  </div>
                  <div className="info-row">
                    <label>Persistence:</label>
                    <span>localStorage</span>
                  </div>
                  <div className="info-row">
                    <label>Total Panels:</label>
                    <span>3</span>
                  </div>
                </div>
              </SafCard>
            </div>
          </div>
        </div>
        
        <div className="panel sidebar-panel">
          <div className="panel-header">
            <h4>Sidebar Panel</h4>
          </div>
          
          <div className="sidebar-content">
            <div className="sidebar-section">
              <h5>Quick Stats</h5>
              <div className="stat-list">
                <div className="stat-item">
                  <SafIcon name="monitor" size="small" />
                  <span>Screen Size: 1920x1080</span>
                </div>
                <div className="stat-item">
                  <SafIcon name="layout" size="small" />
                  <span>Layout: Horizontal</span>
                </div>
                <div className="stat-item">
                  <SafIcon name="grid" size="small" />
                  <span>Panels: 3</span>
                </div>
              </div>
            </div>
            
            <div className="sidebar-section">
              <h5>Recent Actions</h5>
              <SafList size="small">
                <SafListItem>Panel resized</SafListItem>
                <SafListItem>Settings updated</SafListItem>
                <SafListItem>Layout saved</SafListItem>
              </SafList>
            </div>
            
            <div className="sidebar-section">
              <h5>Quick Actions</h5>
              <SafButton variant="outline" size="small" fullWidth>
                Export Layout
              </SafButton>
              <SafButton variant="outline" size="small" fullWidth>
                Import Layout
              </SafButton>
            </div>
          </div>
        </div>
      </SafResizablePanel>
    </div>
  );
};
```

## Best Practices

### Layout Design
- **Logical Grouping**: Group related content within panels for better UX
- **Minimum Sizes**: Set appropriate minimum sizes to prevent unusable panels
- **Visual Hierarchy**: Use panel headers and visual cues for content organization
- **Responsive Behavior**: Consider how panels behave on different screen sizes

### Performance Optimization
- **Efficient Rendering**: Minimize re-renders during resize operations
- **Storage Strategy**: Use appropriate storage (localStorage vs sessionStorage)
- **Debounced Updates**: Debounce resize events for better performance
- **Memory Management**: Clean up event listeners and stored data when needed

### User Experience
- **Visual Feedback**: Provide clear visual feedback during resize operations
- **Constraint Validation**: Enforce sensible minimum and maximum constraints
- **Persistence**: Remember user preferences across sessions
- **Keyboard Support**: Enable keyboard-based resizing for accessibility

### Development
- **Controlled vs Uncontrolled**: Choose appropriate state management patterns
- **Event Handling**: Handle resize events appropriately for your use case
- **Error Boundaries**: Implement error handling for storage operations
- **Testing**: Test resize behavior across different screen sizes and browsers

## Accessibility Considerations

- Uses proper ARIA roles and labels for resizable elements
- Supports keyboard navigation for resize handles using arrow keys
- Provides screen reader announcements for panel size changes
- Maintains proper focus management during resize operations
- Uses semantic HTML structure for panel content
- Supports high contrast mode with appropriate visual indicators
- Respects reduced motion preferences for smooth transitions

## Related Components

- **SafSplitter**: Specialized two-panel splitter component
- **SafTabs**: Tab-based content organization
- **SafDrawer**: Slide-out panel component
- **SafModal**: Overlay-based content panels

## Notes

- SafResizablePanel automatically handles browser compatibility for resize events
- The component supports both controlled and uncontrolled resize modes
- Panel sizes are calculated as percentages for responsive behavior
- Storage persistence works with both localStorage and sessionStorage
- Resize constraints are enforced during all resize operations
- The component maintains accessibility standards for keyboard and screen reader users
- Custom resizer styling allows for brand-specific appearance customization
- Multi-panel layouts support complex application interfaces like IDEs and dashboards
