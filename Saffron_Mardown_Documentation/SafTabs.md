# SafTabs

## Overview

SafTabs is a navigation component that organizes content into multiple panels, allowing users to switch between different views using clickable tab headers. It supports horizontal and vertical orientations, closable tabs, lazy loading, keyboard navigation, and accessibility features for screen readers.

## React API

### SafTabs Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `children` | `ReactNode` | - | SafTab components |
| `activeTab` | `string` | - | Currently active tab ID |
| `defaultActiveTab` | `string` | - | Default active tab ID |
| `onTabChange` | `(tabId: string) => void` | - | Tab change callback |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Tab orientation |
| `variant` | `'default' \| 'pills' \| 'underline' \| 'cards'` | `'default'` | Tab visual style |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Tab size |
| `disabled` | `boolean` | `false` | Disable all tabs |
| `scrollable` | `boolean` | `false` | Enable horizontal scrolling for overflow |
| `centered` | `boolean` | `false` | Center tab headers |
| `fullWidth` | `boolean` | `false` | Make tabs fill container width |
| `lazy` | `boolean` | `false` | Enable lazy loading of tab content |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### SafTab Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string` | - | Unique tab identifier |
| `label` | `string \| ReactNode` | - | Tab header label |
| `children` | `ReactNode` | - | Tab content |
| `disabled` | `boolean` | `false` | Disable this tab |
| `closable` | `boolean` | `false` | Enable close button |
| `icon` | `ReactNode` | - | Tab header icon |
| `badge` | `string \| number` | - | Badge content |
| `tooltip` | `string` | - | Tab tooltip |
| `onClose` | `() => void` | - | Close callback |
| `className` | `string` | - | Additional CSS classes |

## Angular API

### SafTabs Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `activeTab` | `string` | - | Currently active tab ID |
| `defaultActiveTab` | `string` | - | Default active tab ID |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Tab orientation |
| `variant` | `'default' \| 'pills' \| 'underline' \| 'cards'` | `'default'` | Tab visual style |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Tab size |
| `disabled` | `boolean` | `false` | Disable all tabs |
| `scrollable` | `boolean` | `false` | Enable horizontal scrolling |
| `centered` | `boolean` | `false` | Center tab headers |
| `fullWidth` | `boolean` | `false` | Make tabs fill container width |
| `lazy` | `boolean` | `false` | Enable lazy loading |

### SafTabs Events

| Event | Type | Description |
|-------|------|-------------|
| `tabChange` | `EventEmitter<string>` | Fired when active tab changes |
| `tabClose` | `EventEmitter<string>` | Fired when tab is closed |

### SafTab Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string` | - | Unique tab identifier |
| `label` | `string` | - | Tab header label |
| `disabled` | `boolean` | `false` | Disable this tab |
| `closable` | `boolean` | `false` | Enable close button |
| `icon` | `string` | - | Tab header icon name |
| `badge` | `string \| number` | - | Badge content |
| `tooltip` | `string` | - | Tab tooltip |

### SafTab Events

| Event | Type | Description |
|-------|------|-------------|
| `close` | `EventEmitter<void>` | Fired when tab is closed |

## Usage Examples

### Basic Horizontal Tabs

```typescript
// React
const BasicHorizontalTabs = () => {
  const [activeTab, setActiveTab] = useState('overview');

  const handleTabChange = (tabId) => {
    setActiveTab(tabId);
    console.log('Active tab changed to:', tabId);
  };

  return (
    <div className="basic-horizontal-tabs">
      <h3>Project Dashboard</h3>
      
      <SafTabs
        activeTab={activeTab}
        onTabChange={handleTabChange}
        variant="underline"
        className="dashboard-tabs"
      >
        <SafTab
          id="overview"
          label="Overview"
          icon={<SafIcon name="home" />}
        >
          <div className="tab-content">
            <div className="overview-stats">
              <SafCard>
                <div className="stat-item">
                  <SafIcon name="users" size="large" color="primary" />
                  <div className="stat-info">
                    <h4>24,583</h4>
                    <p>Total Users</p>
                  </div>
                  <SafBadge label="+12%" color="success" />
                </div>
              </SafCard>
              
              <SafCard>
                <div className="stat-item">
                  <SafIcon name="activity" size="large" color="secondary" />
                  <div className="stat-info">
                    <h4>1,247</h4>
                    <p>Active Sessions</p>
                  </div>
                  <SafBadge label="+8%" color="success" />
                </div>
              </SafCard>
              
              <SafCard>
                <div className="stat-item">
                  <SafIcon name="dollar-sign" size="large" color="warning" />
                  <div className="stat-info">
                    <h4>$45,291</h4>
                    <p>Revenue</p>
                  </div>
                  <SafBadge label="+23%" color="success" />
                </div>
              </SafCard>
            </div>
            
            <SafCard>
              <h5>Recent Activity</h5>
              <SafList>
                <SafListItem>
                  <SafIcon name="user-plus" />
                  <span>New user registered: john.doe@example.com</span>
                  <span className="timestamp">2 minutes ago</span>
                </SafListItem>
                <SafListItem>
                  <SafIcon name="shopping-cart" />
                  <span>Order completed: #12345</span>
                  <span className="timestamp">5 minutes ago</span>
                </SafListItem>
                <SafListItem>
                  <SafIcon name="alert-triangle" />
                  <span>System maintenance scheduled</span>
                  <span className="timestamp">1 hour ago</span>
                </SafListItem>
              </SafList>
            </SafCard>
          </div>
        </SafTab>
        
        <SafTab
          id="analytics"
          label="Analytics"
          icon={<SafIcon name="bar-chart" />}
          badge={3}
        >
          <div className="tab-content">
            <div className="analytics-header">
              <h4>Analytics Dashboard</h4>
              <div className="analytics-controls">
                <SafDropdown
                  label="Time Period"
                  value="7d"
                  options={[
                    { value: '24h', label: 'Last 24 hours' },
                    { value: '7d', label: 'Last 7 days' },
                    { value: '30d', label: 'Last 30 days' },
                    { value: '90d', label: 'Last 90 days' }
                  ]}
                />
                <SafButton variant="outline" icon={<SafIcon name="download" />}>
                  Export
                </SafButton>
              </div>
            </div>
            
            <div className="charts-grid">
              <SafCard>
                <h5>Page Views</h5>
                <div className="chart-placeholder">
                  <SafIcon name="trending-up" size="large" />
                  <p>Page views chart would be displayed here</p>
                  <SafProgressBar value={75} label="75% increase" />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>User Engagement</h5>
                <div className="chart-placeholder">
                  <SafIcon name="activity" size="large" />
                  <p>Engagement metrics chart</p>
                  <SafProgressBar value={62} label="62% engagement rate" />
                </div>
              </SafCard>
            </div>
          </div>
        </SafTab>
        
        <SafTab
          id="reports"
          label="Reports"
          icon={<SafIcon name="file-text" />}
        >
          <div className="tab-content">
            <div className="reports-header">
              <h4>Generated Reports</h4>
              <SafButton variant="primary" icon={<SafIcon name="plus" />}>
                New Report
              </SafButton>
            </div>
            
            <SafDataTable
              columns={[
                { key: 'name', title: 'Report Name', sortable: true },
                { key: 'type', title: 'Type', sortable: true },
                { key: 'created', title: 'Created', sortable: true },
                { key: 'status', title: 'Status', sortable: false },
                { key: 'actions', title: 'Actions', sortable: false }
              ]}
              data={[
                {
                  name: 'Monthly Sales Report',
                  type: 'Sales',
                  created: '2023-09-25',
                  status: 'Ready',
                  actions: 'download'
                },
                {
                  name: 'User Activity Analysis',
                  type: 'Analytics',
                  created: '2023-09-24',
                  status: 'Processing',
                  actions: 'view'
                },
                {
                  name: 'Performance Metrics',
                  type: 'Performance',
                  created: '2023-09-23',
                  status: 'Ready',
                  actions: 'download'
                }
              ]}
              pagination
            />
          </div>
        </SafTab>
        
        <SafTab
          id="settings"
          label="Settings"
          icon={<SafIcon name="settings" />}
        >
          <div className="tab-content">
            <div className="settings-sections">
              <SafCard>
                <h5>General Settings</h5>
                <div className="setting-item">
                  <SafLabel>Project Name</SafLabel>
                  <SafTextInput 
                    value="My Dashboard Project"
                    placeholder="Enter project name"
                  />
                </div>
                <div className="setting-item">
                  <SafLabel>Description</SafLabel>
                  <SafTextarea 
                    value="A comprehensive dashboard for project management"
                    placeholder="Enter project description"
                    rows={3}
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Notification Settings</h5>
                <div className="setting-item">
                  <SafCheckbox 
                    label="Email notifications"
                    defaultChecked
                  />
                </div>
                <div className="setting-item">
                  <SafCheckbox 
                    label="Push notifications"
                    defaultChecked
                  />
                </div>
                <div className="setting-item">
                  <SafCheckbox 
                    label="Weekly reports"
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Privacy Settings</h5>
                <div className="setting-item">
                  <SafCheckbox 
                    label="Make project public"
                  />
                </div>
                <div className="setting-item">
                  <SafCheckbox 
                    label="Allow team collaboration"
                    defaultChecked
                  />
                </div>
              </SafCard>
            </div>
            
            <div className="settings-actions">
              <SafButton variant="primary">Save Changes</SafButton>
              <SafButton variant="outline">Cancel</SafButton>
            </div>
          </div>
        </SafTab>
      </SafTabs>
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-horizontal-tabs">
  <h3>Project Dashboard</h3>
  
  <saf-tabs
    [activeTab]="activeTab"
    (tabChange)="handleTabChange($event)"
    variant="underline"
    class="dashboard-tabs">
    
    <saf-tab
      id="overview"
      label="Overview"
      icon="home">
      
      <div class="tab-content">
        <div class="overview-stats">
          <saf-card>
            <div class="stat-item">
              <saf-icon name="users" size="large" color="primary"></saf-icon>
              <div class="stat-info">
                <h4>24,583</h4>
                <p>Total Users</p>
              </div>
              <saf-badge label="+12%" color="success"></saf-badge>
            </div>
          </saf-card>
          
          <!-- More stat cards... -->
        </div>
        
        <saf-card>
          <h5>Recent Activity</h5>
          <saf-list>
            <saf-list-item>
              <saf-icon name="user-plus"></saf-icon>
              <span>New user registered: john.doe@example.com</span>
              <span class="timestamp">2 minutes ago</span>
            </saf-list-item>
            <!-- More list items... -->
          </saf-list>
        </saf-card>
      </div>
    </saf-tab>
    
    <saf-tab
      id="analytics"
      label="Analytics"
      icon="bar-chart"
      [badge]="3">
      
      <div class="tab-content">
        <!-- Analytics content... -->
      </div>
    </saf-tab>
    
    <saf-tab
      id="reports"
      label="Reports"
      icon="file-text">
      
      <div class="tab-content">
        <!-- Reports content... -->
      </div>
    </saf-tab>
    
    <saf-tab
      id="settings"
      label="Settings"
      icon="settings">
      
      <div class="tab-content">
        <!-- Settings content... -->
      </div>
    </saf-tab>
  </saf-tabs>
</div>
```

### Vertical Tabs Layout

```typescript
// React
const VerticalTabsLayout = () => {
  const [activeTab, setActiveTab] = useState('profile');

  return (
    <div className="vertical-tabs-layout">
      <h3>User Account Settings</h3>
      
      <SafTabs
        activeTab={activeTab}
        onTabChange={setActiveTab}
        orientation="vertical"
        variant="pills"
        size="large"
        className="settings-vertical-tabs"
      >
        <SafTab
          id="profile"
          label="Profile"
          icon={<SafIcon name="user" />}
        >
          <div className="settings-content">
            <div className="content-header">
              <h4>Profile Information</h4>
              <p>Update your personal information and profile settings</p>
            </div>
            
            <div className="profile-form">
              <div className="form-section">
                <h5>Basic Information</h5>
                <div className="form-grid">
                  <div className="form-item">
                    <SafLabel required>First Name</SafLabel>
                    <SafTextInput 
                      value="John"
                      placeholder="Enter first name"
                    />
                  </div>
                  <div className="form-item">
                    <SafLabel required>Last Name</SafLabel>
                    <SafTextInput 
                      value="Doe"
                      placeholder="Enter last name"
                    />
                  </div>
                  <div className="form-item">
                    <SafLabel required>Email</SafLabel>
                    <SafTextInput 
                      type="email"
                      value="john.doe@example.com"
                      placeholder="Enter email address"
                    />
                  </div>
                  <div className="form-item">
                    <SafLabel>Phone</SafLabel>
                    <SafTextInput 
                      type="tel"
                      value="+1 (555) 123-4567"
                      placeholder="Enter phone number"
                    />
                  </div>
                </div>
              </div>
              
              <div className="form-section">
                <h5>Profile Picture</h5>
                <div className="profile-picture-section">
                  <SafAvatar 
                    name="John Doe"
                    size="large"
                    src="/path/to/profile-picture.jpg"
                  />
                  <div className="picture-actions">
                    <SafButton variant="outline" icon={<SafIcon name="upload" />}>
                      Upload New Picture
                    </SafButton>
                    <SafButton variant="ghost" icon={<SafIcon name="trash" />}>
                      Remove
                    </SafButton>
                  </div>
                </div>
              </div>
              
              <div className="form-section">
                <h5>Bio</h5>
                <SafTextarea 
                  value="Software developer with 5+ years of experience in web technologies."
                  placeholder="Tell us about yourself"
                  rows={4}
                />
              </div>
            </div>
          </div>
        </SafTab>
        
        <SafTab
          id="account"
          label="Account"
          icon={<SafIcon name="key" />}
        >
          <div className="settings-content">
            <div className="content-header">
              <h4>Account Security</h4>
              <p>Manage your account security and login preferences</p>
            </div>
            
            <div className="account-sections">
              <SafCard>
                <h5>Change Password</h5>
                <div className="password-form">
                  <div className="form-item">
                    <SafLabel required>Current Password</SafLabel>
                    <SafTextInput 
                      type="password"
                      placeholder="Enter current password"
                    />
                  </div>
                  <div className="form-item">
                    <SafLabel required>New Password</SafLabel>
                    <SafTextInput 
                      type="password"
                      placeholder="Enter new password"
                    />
                  </div>
                  <div className="form-item">
                    <SafLabel required>Confirm Password</SafLabel>
                    <SafTextInput 
                      type="password"
                      placeholder="Confirm new password"
                    />
                  </div>
                  <SafButton variant="primary">Update Password</SafButton>
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Two-Factor Authentication</h5>
                <div className="tfa-section">
                  <div className="tfa-status">
                    <SafIcon name="shield-check" color="success" />
                    <span>Two-factor authentication is enabled</span>
                    <SafBadge label="Active" color="success" />
                  </div>
                  <div className="tfa-actions">
                    <SafButton variant="outline">View Recovery Codes</SafButton>
                    <SafButton variant="ghost">Disable 2FA</SafButton>
                  </div>
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Active Sessions</h5>
                <div className="sessions-list">
                  <div className="session-item">
                    <div className="session-info">
                      <SafIcon name="monitor" />
                      <div className="session-details">
                        <h6>Windows - Chrome</h6>
                        <p>Current session • New York, NY</p>
                      </div>
                    </div>
                    <SafBadge label="Current" color="success" />
                  </div>
                  <div className="session-item">
                    <div className="session-info">
                      <SafIcon name="smartphone" />
                      <div className="session-details">
                        <h6>iPhone - Safari</h6>
                        <p>Last used 2 hours ago • New York, NY</p>
                      </div>
                    </div>
                    <SafButton variant="ghost" size="small">End Session</SafButton>
                  </div>
                </div>
              </SafCard>
            </div>
          </div>
        </SafTab>
        
        <SafTab
          id="notifications"
          label="Notifications"
          icon={<SafIcon name="bell" />}
          badge={2}
        >
          <div className="settings-content">
            <div className="content-header">
              <h4>Notification Preferences</h4>
              <p>Choose what notifications you want to receive</p>
            </div>
            
            <div className="notification-sections">
              <SafCard>
                <h5>Email Notifications</h5>
                <div className="notification-options">
                  <SafCheckbox 
                    label="Account updates"
                    defaultChecked
                    helpText="Receive emails about account changes and security updates"
                  />
                  <SafCheckbox 
                    label="Product updates"
                    defaultChecked
                    helpText="Get notified about new features and improvements"
                  />
                  <SafCheckbox 
                    label="Marketing emails"
                    helpText="Receive promotional emails and special offers"
                  />
                  <SafCheckbox 
                    label="Weekly digest"
                    defaultChecked
                    helpText="A summary of your weekly activity"
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Push Notifications</h5>
                <div className="notification-options">
                  <SafCheckbox 
                    label="Real-time alerts"
                    defaultChecked
                    helpText="Immediate notifications for important events"
                  />
                  <SafCheckbox 
                    label="Daily summary"
                    helpText="A daily overview of your activity"
                  />
                  <SafCheckbox 
                    label="Reminders"
                    defaultChecked
                    helpText="Helpful reminders and due dates"
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Notification Schedule</h5>
                <div className="schedule-settings">
                  <div className="form-item">
                    <SafLabel>Quiet Hours</SafLabel>
                    <div className="time-range">
                      <SafTextInput 
                        type="time"
                        value="22:00"
                        size="small"
                      />
                      <span>to</span>
                      <SafTextInput 
                        type="time"
                        value="08:00"
                        size="small"
                      />
                    </div>
                  </div>
                  <SafCheckbox 
                    label="Pause notifications on weekends"
                  />
                </div>
              </SafCard>
            </div>
          </div>
        </SafTab>
        
        <SafTab
          id="privacy"
          label="Privacy"
          icon={<SafIcon name="lock" />}
        >
          <div className="settings-content">
            <div className="content-header">
              <h4>Privacy Settings</h4>
              <p>Control your privacy and data sharing preferences</p>
            </div>
            
            <div className="privacy-sections">
              <SafCard>
                <h5>Profile Visibility</h5>
                <div className="privacy-options">
                  <SafRadioButton
                    name="profileVisibility"
                    value="public"
                    label="Public"
                    helpText="Anyone can view your profile"
                  />
                  <SafRadioButton
                    name="profileVisibility"
                    value="friends"
                    label="Friends only"
                    helpText="Only your connections can view your profile"
                    defaultChecked
                  />
                  <SafRadioButton
                    name="profileVisibility"
                    value="private"
                    label="Private"
                    helpText="Only you can view your profile"
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Data Collection</h5>
                <div className="privacy-options">
                  <SafCheckbox 
                    label="Analytics and performance"
                    defaultChecked
                    helpText="Help improve our service by sharing usage data"
                  />
                  <SafCheckbox 
                    label="Personalized recommendations"
                    defaultChecked
                    helpText="Use your activity to suggest relevant content"
                  />
                  <SafCheckbox 
                    label="Third-party integrations"
                    helpText="Allow third-party services to access your data"
                  />
                </div>
              </SafCard>
              
              <SafCard>
                <h5>Data Export & Deletion</h5>
                <div className="data-actions">
                  <div className="action-item">
                    <div className="action-info">
                      <h6>Export Your Data</h6>
                      <p>Download a copy of all your data</p>
                    </div>
                    <SafButton variant="outline">Export Data</SafButton>
                  </div>
                  <div className="action-item">
                    <div className="action-info">
                      <h6>Delete Account</h6>
                      <p>Permanently delete your account and all data</p>
                    </div>
                    <SafButton variant="outline" color="error">Delete Account</SafButton>
                  </div>
                </div>
              </SafCard>
            </div>
          </div>
        </SafTab>
      </SafTabs>
    </div>
  );
};
```

### Closable Tabs with Dynamic Content

```typescript
// React
const ClosableTabsWithDynamicContent = () => {
  const [tabs, setTabs] = useState([
    { id: 'welcome', label: 'Welcome', content: 'Welcome to the application!', closable: false },
    { id: 'document1', label: 'Document 1', content: 'Content of document 1', closable: true },
    { id: 'document2', label: 'Document 2', content: 'Content of document 2', closable: true }
  ]);
  const [activeTab, setActiveTab] = useState('welcome');
  const [tabCounter, setTabCounter] = useState(3);

  const handleTabClose = (tabId) => {
    const newTabs = tabs.filter(tab => tab.id !== tabId);
    setTabs(newTabs);
    
    // If closed tab was active, switch to first available tab
    if (activeTab === tabId && newTabs.length > 0) {
      setActiveTab(newTabs[0].id);
    }
  };

  const addNewTab = () => {
    const newTabId = `document${tabCounter}`;
    const newTab = {
      id: newTabId,
      label: `Document ${tabCounter}`,
      content: `Content of document ${tabCounter}`,
      closable: true
    };
    
    setTabs([...tabs, newTab]);
    setActiveTab(newTabId);
    setTabCounter(tabCounter + 1);
  };

  const saveDocument = (tabId) => {
    console.log(`Saving document: ${tabId}`);
    // Simulate save operation
  };

  return (
    <div className="closable-tabs-dynamic">
      <div className="editor-toolbar">
        <h3>Document Editor</h3>
        <div className="toolbar-actions">
          <SafButton 
            variant="primary" 
            onClick={addNewTab}
            icon={<SafIcon name="plus" />}
          >
            New Document
          </SafButton>
          <SafButton 
            variant="outline"
            onClick={() => saveDocument(activeTab)}
            icon={<SafIcon name="save" />}
          >
            Save
          </SafButton>
          <SafButton 
            variant="outline"
            icon={<SafIcon name="folder-open" />}
          >
            Open
          </SafButton>
        </div>
      </div>
      
      <SafTabs
        activeTab={activeTab}
        onTabChange={setActiveTab}
        variant="cards"
        scrollable
        className="editor-tabs"
      >
        {tabs.map(tab => (
          <SafTab
            key={tab.id}
            id={tab.id}
            label={tab.label}
            closable={tab.closable}
            onClose={() => handleTabClose(tab.id)}
            icon={tab.id === 'welcome' ? <SafIcon name="home" /> : <SafIcon name="file-text" />}
          >
            <div className="editor-content">
              {tab.id === 'welcome' ? (
                <div className="welcome-content">
                  <div className="welcome-header">
                    <SafIcon name="file-text" size="large" color="primary" />
                    <h4>Welcome to Document Editor</h4>
                    <p>Create and edit documents with our powerful editor</p>
                  </div>
                  
                  <div className="welcome-actions">
                    <SafButton 
                      variant="primary" 
                      onClick={addNewTab}
                      icon={<SafIcon name="plus" />}
                    >
                      Create New Document
                    </SafButton>
                    <SafButton 
                      variant="outline"
                      icon={<SafIcon name="folder-open" />}
                    >
                      Open Existing Document
                    </SafButton>
                  </div>
                  
                  <div className="recent-documents">
                    <h5>Recent Documents</h5>
                    <SafList>
                      <SafListItem>
                        <SafIcon name="file-text" />
                        <span>Project Proposal.docx</span>
                        <span className="document-date">Modified 2 hours ago</span>
                      </SafListItem>
                      <SafListItem>
                        <SafIcon name="file-text" />
                        <span>Meeting Notes.docx</span>
                        <span className="document-date">Modified yesterday</span>
                      </SafListItem>
                      <SafListItem>
                        <SafIcon name="file-text" />
                        <span>Requirements.docx</span>
                        <span className="document-date">Modified 3 days ago</span>
                      </SafListItem>
                    </SafList>
                  </div>
                </div>
              ) : (
                <div className="document-editor">
                  <div className="editor-toolbar">
                    <div className="formatting-tools">
                      <SafButtonGroup>
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="bold" />} />
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="italic" />} />
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="underline" />} />
                      </SafButtonGroup>
                      
                      <SafButtonGroup>
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="align-left" />} />
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="align-center" />} />
                        <SafButton variant="ghost" size="small" icon={<SafIcon name="align-right" />} />
                      </SafButtonGroup>
                      
                      <SafDropdown
                        label="Font Size"
                        value="14"
                        options={[
                          { value: '12', label: '12px' },
                          { value: '14', label: '14px' },
                          { value: '16', label: '16px' },
                          { value: '18', label: '18px' }
                        ]}
                        size="small"
                      />
                    </div>
                    
                    <div className="document-status">
                      <SafBadge label="Saved" color="success" size="small" />
                      <span className="word-count">245 words</span>
                    </div>
                  </div>
                  
                  <div className="editor-area">
                    <SafTextarea
                      value={tab.content}
                      placeholder="Start typing your document..."
                      rows={20}
                      className="document-textarea"
                      onChange={(value) => {
                        const updatedTabs = tabs.map(t => 
                          t.id === tab.id ? { ...t, content: value } : t
                        );
                        setTabs(updatedTabs);
                      }}
                    />
                  </div>
                  
                  <div className="editor-footer">
                    <div className="document-info">
                      <span>Line 1, Column 1</span>
                      <span>Characters: {tab.content.length}</span>
                    </div>
                  </div>
                </div>
              )}
            </div>
          </SafTab>
        ))}
      </SafTabs>
    </div>
  );
};
```

### Scrollable Tabs with Badges

```typescript
// React
const ScrollableTabsWithBadges = () => {
  const [activeTab, setActiveTab] = useState('inbox');
  
  const emailFolders = [
    { id: 'inbox', label: 'Inbox', count: 23, icon: 'inbox' },
    { id: 'starred', label: 'Starred', count: 5, icon: 'star' },
    { id: 'sent', label: 'Sent', count: 0, icon: 'send' },
    { id: 'drafts', label: 'Drafts', count: 3, icon: 'edit' },
    { id: 'spam', label: 'Spam', count: 12, icon: 'shield' },
    { id: 'trash', label: 'Trash', count: 8, icon: 'trash' },
    { id: 'archive', label: 'Archive', count: 156, icon: 'archive' },
    { id: 'promotions', label: 'Promotions', count: 45, icon: 'tag' },
    { id: 'social', label: 'Social', count: 89, icon: 'users' },
    { id: 'updates', label: 'Updates', count: 34, icon: 'refresh-cw' }
  ];

  const getEmailsForFolder = (folderId) => {
    const sampleEmails = {
      inbox: [
        { id: 1, from: 'Alice Johnson', subject: 'Project Update', time: '2:30 PM', unread: true },
        { id: 2, from: 'Bob Smith', subject: 'Meeting Tomorrow', time: '1:15 PM', unread: true },
        { id: 3, from: 'Carol Wilson', subject: 'Design Review', time: '11:45 AM', unread: false }
      ],
      starred: [
        { id: 4, from: 'Important Client', subject: 'Contract Review', time: 'Yesterday', unread: false }
      ],
      drafts: [
        { id: 5, from: 'Draft', subject: 'Quarterly Report', time: 'Draft', unread: false }
      ]
    };
    
    return sampleEmails[folderId] || [];
  };

  return (
    <div className="scrollable-tabs-badges">
      <div className="email-header">
        <h3>Email Client</h3>
        <div className="email-actions">
          <SafButton variant="primary" icon={<SafIcon name="edit" />}>
            Compose
          </SafButton>
          <SafButton variant="outline" icon={<SafIcon name="refresh-cw" />} />
        </div>
      </div>
      
      <SafTabs
        activeTab={activeTab}
        onTabChange={setActiveTab}
        variant="pills"
        scrollable
        size="small"
        className="email-folder-tabs"
      >
        {emailFolders.map(folder => (
          <SafTab
            key={folder.id}
            id={folder.id}
            label={folder.label}
            icon={<SafIcon name={folder.icon} />}
            badge={folder.count > 0 ? folder.count : undefined}
            tooltip={`${folder.label} - ${folder.count} emails`}
          >
            <div className="folder-content">
              <div className="folder-header">
                <h4>{folder.label}</h4>
                <div className="folder-actions">
                  {folder.count > 0 && (
                    <SafBadge 
                      label={`${folder.count} emails`}
                      color={folder.id === 'spam' ? 'error' : 'primary'}
                    />
                  )}
                  <SafIconButton icon={<SafIcon name="more-vertical" />} size="small" />
                </div>
              </div>
              
              <div className="emails-list">
                {getEmailsForFolder(folder.id).length > 0 ? (
                  getEmailsForFolder(folder.id).map(email => (
                    <div key={email.id} className={`email-item ${email.unread ? 'unread' : ''}`}>
                      <div className="email-sender">
                        <SafAvatar name={email.from} size="small" />
                        <span className="sender-name">{email.from}</span>
                      </div>
                      <div className="email-content">
                        <h5 className="email-subject">{email.subject}</h5>
                        <span className="email-time">{email.time}</span>
                      </div>
                      {email.unread && <div className="unread-indicator" />}
                    </div>
                  ))
                ) : (
                  <div className="empty-folder">
                    <SafIcon name={folder.icon} size="large" color="secondary" />
                    <h5>No emails in {folder.label}</h5>
                    <p>This folder is empty</p>
                  </div>
                )}
              </div>
            </div>
          </SafTab>
        ))}
      </SafTabs>
    </div>
  );
};
```

### Lazy Loading Tabs

```typescript
// React
const LazyLoadingTabs = () => {
  const [activeTab, setActiveTab] = useState('overview');
  const [loadedTabs, setLoadedTabs] = useState(new Set(['overview']));

  const handleTabChange = (tabId) => {
    setActiveTab(tabId);
    if (!loadedTabs.has(tabId)) {
      setLoadedTabs(new Set([...loadedTabs, tabId]));
    }
  };

  const LoadingContent = () => (
    <div className="tab-loading">
      <SafLoadingSpinner size="large" />
      <p>Loading content...</p>
    </div>
  );

  const LazyTabContent = ({ tabId, children }) => {
    if (!loadedTabs.has(tabId)) {
      return <LoadingContent />;
    }
    return children;
  };

  return (
    <div className="lazy-loading-tabs">
      <h3>Data Analytics Dashboard</h3>
      
      <SafTabs
        activeTab={activeTab}
        onTabChange={handleTabChange}
        lazy
        variant="underline"
        className="analytics-tabs"
      >
        <SafTab
          id="overview"
          label="Overview"
          icon={<SafIcon name="home" />}
        >
          <div className="tab-content">
            <h4>Dashboard Overview</h4>
            <p>This content loads immediately as it's the default tab.</p>
            
            <div className="overview-metrics">
              <SafCard>
                <h5>Quick Stats</h5>
                <div className="stats-grid">
                  <div className="stat-item">
                    <SafIcon name="users" color="primary" />
                    <span>1,234 Users</span>
                  </div>
                  <div className="stat-item">
                    <SafIcon name="activity" color="success" />
                    <span>5,678 Sessions</span>
                  </div>
                  <div className="stat-item">
                    <SafIcon name="dollar-sign" color="warning" />
                    <span>$12,345 Revenue</span>
                  </div>
                </div>
              </SafCard>
            </div>
          </div>
        </SafTab>
        
        <SafTab
          id="users"
          label="Users"
          icon={<SafIcon name="users" />}
          badge="1.2k"
        >
          <LazyTabContent tabId="users">
            <div className="tab-content">
              <h4>User Analytics</h4>
              <p>This content loads when the tab is first accessed.</p>
              
              <SafCard>
                <h5>User Demographics</h5>
                <div className="user-demographics">
                  <div className="demographic-item">
                    <span className="label">Age 18-24</span>
                    <SafProgressBar value={25} label="25%" />
                  </div>
                  <div className="demographic-item">
                    <span className="label">Age 25-34</span>
                    <SafProgressBar value={40} label="40%" />
                  </div>
                  <div className="demographic-item">
                    <span className="label">Age 35-44</span>
                    <SafProgressBar value={20} label="20%" />
                  </div>
                  <div className="demographic-item">
                    <span className="label">Age 45+</span>
                    <SafProgressBar value={15} label="15%" />
                  </div>
                </div>
              </SafCard>
            </div>
          </LazyTabContent>
        </SafTab>
        
        <SafTab
          id="performance"
          label="Performance"
          icon={<SafIcon name="activity" />}
        >
          <LazyTabContent tabId="performance">
            <div className="tab-content">
              <h4>Performance Metrics</h4>
              <p>Performance data loads on demand to optimize initial page load.</p>
              
              <div className="performance-cards">
                <SafCard>
                  <h5>Page Load Time</h5>
                  <div className="metric-value">
                    <span className="value">2.3s</span>
                    <SafBadge label="Good" color="success" />
                  </div>
                  <SafProgressBar value={77} label="77% faster than average" />
                </SafCard>
                
                <SafCard>
                  <h5>Core Web Vitals</h5>
                  <div className="vitals-list">
                    <div className="vital-item">
                      <span>LCP</span>
                      <SafBadge label="1.8s" color="success" />
                    </div>
                    <div className="vital-item">
                      <span>FID</span>
                      <SafBadge label="45ms" color="success" />
                    </div>
                    <div className="vital-item">
                      <span>CLS</span>
                      <SafBadge label="0.12" color="warning" />
                    </div>
                  </div>
                </SafCard>
              </div>
            </div>
          </LazyTabContent>
        </SafTab>
        
        <SafTab
          id="reports"
          label="Reports"
          icon={<SafIcon name="file-text" />}
        >
          <LazyTabContent tabId="reports">
            <div className="tab-content">
              <h4>Generated Reports</h4>
              <p>Report data is loaded when needed to improve performance.</p>
              
              <div className="reports-section">
                <div className="reports-header">
                  <SafButton variant="primary" icon={<SafIcon name="plus" />}>
                    Generate Report
                  </SafButton>
                  <SafButton variant="outline" icon={<SafIcon name="download" />}>
                    Export All
                  </SafButton>
                </div>
                
                <SafDataTable
                  columns={[
                    { key: 'name', title: 'Report Name' },
                    { key: 'type', title: 'Type' },
                    { key: 'created', title: 'Created' },
                    { key: 'status', title: 'Status' }
                  ]}
                  data={[
                    { name: 'Monthly Analytics', type: 'Analytics', created: '2023-09-25', status: 'Ready' },
                    { name: 'User Report', type: 'Users', created: '2023-09-24', status: 'Processing' },
                    { name: 'Performance Audit', type: 'Performance', created: '2023-09-23', status: 'Ready' }
                  ]}
                />
              </div>
            </div>
          </LazyTabContent>
        </SafTab>
      </SafTabs>
      
      <div className="loading-status">
        <h5>Tab Loading Status</h5>
        <div className="status-list">
          {['overview', 'users', 'performance', 'reports'].map(tabId => (
            <div key={tabId} className="status-item">
              <span className="tab-name">{tabId}</span>
              <SafBadge 
                label={loadedTabs.has(tabId) ? 'Loaded' : 'Not loaded'}
                color={loadedTabs.has(tabId) ? 'success' : 'secondary'}
                size="small"
              />
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};
```

## Best Practices

### Content Organization
- **Logical Grouping**: Group related content within appropriate tabs
- **Tab Labels**: Use clear, concise labels that describe the content
- **Icon Usage**: Use consistent icons that support the tab labels
- **Content Loading**: Implement lazy loading for tabs with heavy content

### User Experience
- **Active State**: Clearly indicate which tab is currently active
- **Navigation**: Enable keyboard navigation with arrow keys and Enter
- **Responsive Design**: Handle tab overflow appropriately with scrolling
- **State Persistence**: Remember active tab state when appropriate

### Performance
- **Lazy Loading**: Load tab content only when needed
- **Memory Management**: Clean up resources when tabs are closed
- **Efficient Rendering**: Minimize re-renders during tab switches
- **Content Caching**: Cache loaded content appropriately

### Accessibility
- **ARIA Labels**: Use proper ARIA attributes for screen readers
- **Keyboard Support**: Implement full keyboard navigation
- **Focus Management**: Handle focus appropriately during tab changes
- **Screen Reader Announcements**: Announce tab changes and content

## Accessibility Considerations

- Uses proper ARIA roles including `tablist`, `tab`, and `tabpanel`
- Supports complete keyboard navigation with arrow keys, Home, and End
- Provides screen reader announcements for tab changes and content
- Maintains proper focus management during tab switching
- Uses semantic HTML structure with appropriate heading hierarchy
- Supports high contrast mode with clear visual indicators
- Respects reduced motion preferences for smooth transitions

## Related Components

- **SafNavigation**: Primary navigation component
- **SafBreadcrumb**: Hierarchical navigation breadcrumbs
- **SafAccordion**: Collapsible content organization
- **SafStepper**: Step-by-step process navigation

## Notes

- SafTabs automatically handles keyboard navigation and accessibility
- The component supports both controlled and uncontrolled tab management
- Lazy loading helps optimize performance for content-heavy applications
- Closable tabs enable dynamic tab management for editor-like interfaces
- Badge support provides visual indicators for tab content status
- Scrollable tabs handle overflow gracefully on smaller screens
- Vertical orientation works well for sidebar navigation patterns
- The component maintains state consistency across tab operations
