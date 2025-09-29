# SafTabPanel Component

## Overview
The `SafTabPanel` component represents the content panel associated with a tab in a tabbed interface. It displays the content that corresponds to a selected tab and manages the visibility and accessibility of that content. This component is designed to work with `SafTab` components and provides proper ARIA attributes for screen readers and keyboard navigation.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the tab panel is currently selected/visible |
| `id` | `string` | `undefined` | Unique identifier that matches the corresponding tab |
| `tabId` | `string` | `undefined` | ID of the associated tab (for ARIA attributes) |
| `hidden` | `boolean` | `false` | Whether the panel is hidden (alternative to selected) |
| `lazy` | `boolean` | `false` | Whether to lazy load content when first selected |
| `keepAlive` | `boolean` | `false` | Whether to keep content mounted when not selected |
| `role` | `string` | `'tabpanel'` | ARIA role for the panel |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Panel content |

### Events
- `onShow`: Fired when the panel becomes visible
- `onHide`: Fired when the panel becomes hidden
- `onMount`: Fired when the panel content is first mounted (lazy loading)

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `selected` | `boolean` | `false` | Whether the tab panel is currently selected/visible |
| `id` | `string` | `undefined` | Unique identifier that matches the corresponding tab |
| `tabId` | `string` | `undefined` | ID of the associated tab (for ARIA attributes) |
| `hidden` | `boolean` | `false` | Whether the panel is hidden (alternative to selected) |
| `lazy` | `boolean` | `false` | Whether to lazy load content when first selected |
| `keepAlive` | `boolean` | `false` | Whether to keep content mounted when not selected |
| `role` | `string` | `'tabpanel'` | ARIA role for the panel |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(show)` | `EventEmitter<void>` | Emitted when the panel becomes visible |
| `(hide)` | `EventEmitter<void>` | Emitted when the panel becomes hidden |
| `(mount)` | `EventEmitter<void>` | Emitted when content is first mounted |

### Content Projection
- **Default slot**: Panel content

## Usage Examples

### Basic Tab Panels

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel } from '@saffron/core-components';
import { useState } from 'react';

function BasicTabPanelExample() {
  const [selectedTab, setSelectedTab] = useState('overview');

  return (
    <div>
      <SafTabs>
        <SafTab 
          id="overview"
          selected={selectedTab === 'overview'}
          onClick={() => setSelectedTab('overview')}
        >
          Overview
        </SafTab>
        <SafTab 
          id="details"
          selected={selectedTab === 'details'}
          onClick={() => setSelectedTab('details')}
        >
          Details
        </SafTab>
        <SafTab 
          id="settings"
          selected={selectedTab === 'settings'}
          onClick={() => setSelectedTab('settings')}
        >
          Settings
        </SafTab>
      </SafTabs>
      
      <SafTabPanel 
        id="overview"
        tabId="overview"
        selected={selectedTab === 'overview'}
      >
        <h2>Overview</h2>
        <p>This is the overview content with key information and summaries.</p>
        <div>
          <h3>Key Metrics</h3>
          <ul>
            <li>Total Users: 1,234</li>
            <li>Active Sessions: 89</li>
            <li>Revenue: $45,678</li>
          </ul>
        </div>
      </SafTabPanel>
      
      <SafTabPanel 
        id="details"
        tabId="details"
        selected={selectedTab === 'details'}
      >
        <h2>Detailed Information</h2>
        <p>Comprehensive details and data tables.</p>
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Value</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Item 1</td>
              <td>100</td>
              <td>Active</td>
            </tr>
            <tr>
              <td>Item 2</td>
              <td>250</td>
              <td>Pending</td>
            </tr>
          </tbody>
        </table>
      </SafTabPanel>
      
      <SafTabPanel 
        id="settings"
        tabId="settings"
        selected={selectedTab === 'settings'}
      >
        <h2>Settings</h2>
        <p>Configuration options and preferences.</p>
        <form>
          <div>
            <label>
              <input type="checkbox" /> Enable notifications
            </label>
          </div>
          <div>
            <label>
              <input type="checkbox" /> Auto-save changes
            </label>
          </div>
          <button type="submit">Save Settings</button>
        </form>
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
  selector: 'app-basic-tab-panels',
  template: `
    <div>
      <saf-tabs>
        <saf-tab 
          id="overview"
          [selected]="selectedTab === 'overview'"
          (click)="setSelectedTab('overview')"
        >
          Overview
        </saf-tab>
        <saf-tab 
          id="details"
          [selected]="selectedTab === 'details'"
          (click)="setSelectedTab('details')"
        >
          Details
        </saf-tab>
        <saf-tab 
          id="settings"
          [selected]="selectedTab === 'settings'"
          (click)="setSelectedTab('settings')"
        >
          Settings
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel 
        id="overview"
        tabId="overview"
        [selected]="selectedTab === 'overview'"
      >
        <h2>Overview</h2>
        <p>This is the overview content with key information and summaries.</p>
        <div>
          <h3>Key Metrics</h3>
          <ul>
            <li>Total Users: 1,234</li>
            <li>Active Sessions: 89</li>
            <li>Revenue: $45,678</li>
          </ul>
        </div>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="details"
        tabId="details"
        [selected]="selectedTab === 'details'"
      >
        <h2>Detailed Information</h2>
        <p>Comprehensive details and data tables.</p>
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Value</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Item 1</td>
              <td>100</td>
              <td>Active</td>
            </tr>
            <tr>
              <td>Item 2</td>
              <td>250</td>
              <td>Pending</td>
            </tr>
          </tbody>
        </table>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="settings"
        tabId="settings"
        [selected]="selectedTab === 'settings'"
      >
        <h2>Settings</h2>
        <p>Configuration options and preferences.</p>
        <form>
          <div>
            <label>
              <input type="checkbox" /> Enable notifications
            </label>
          </div>
          <div>
            <label>
              <input type="checkbox" /> Auto-save changes
            </label>
          </div>
          <button type="submit">Save Settings</button>
        </form>
      </saf-tab-panel>
    </div>
  `
})
export class BasicTabPanelsComponent {
  selectedTab = 'overview';

  setSelectedTab(tabId: string) {
    this.selectedTab = tabId;
  }
}
```

### Lazy Loading Tab Panels

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel, SafSpinner } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function LazyTabPanelExample() {
  const [selectedTab, setSelectedTab] = useState('tab1');
  const [loadedTabs, setLoadedTabs] = useState(new Set(['tab1']));
  const [tabData, setTabData] = useState({});
  const [loading, setLoading] = useState({});

  const loadTabContent = async (tabId) => {
    if (loadedTabs.has(tabId)) return;
    
    setLoading(prev => ({ ...prev, [tabId]: true }));
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    const content = {
      tab1: { title: 'Dashboard', data: 'Real-time dashboard data...' },
      tab2: { title: 'Analytics', data: 'Complex analytics charts...' },
      tab3: { title: 'Reports', data: 'Generated report data...' }
    };
    
    setTabData(prev => ({ ...prev, [tabId]: content[tabId] }));
    setLoadedTabs(prev => new Set(prev).add(tabId));
    setLoading(prev => ({ ...prev, [tabId]: false }));
  };

  const handleTabClick = (tabId) => {
    setSelectedTab(tabId);
    if (!loadedTabs.has(tabId)) {
      loadTabContent(tabId);
    }
  };

  return (
    <div>
      <SafTabs>
        <SafTab 
          id="tab1"
          selected={selectedTab === 'tab1'}
          onClick={() => handleTabClick('tab1')}
        >
          Dashboard
        </SafTab>
        <SafTab 
          id="tab2"
          selected={selectedTab === 'tab2'}
          onClick={() => handleTabClick('tab2')}
        >
          Analytics
        </SafTab>
        <SafTab 
          id="tab3"
          selected={selectedTab === 'tab3'}
          onClick={() => handleTabClick('tab3')}
        >
          Reports
        </SafTab>
      </SafTabs>
      
      <SafTabPanel 
        id="tab1"
        selected={selectedTab === 'tab1'}
        lazy
        onShow={() => loadTabContent('tab1')}
      >
        {loading.tab1 ? (
          <SafSpinner size="large" />
        ) : (
          <div>
            <h2>{tabData.tab1?.title}</h2>
            <p>{tabData.tab1?.data}</p>
          </div>
        )}
      </SafTabPanel>
      
      <SafTabPanel 
        id="tab2"
        selected={selectedTab === 'tab2'}
        lazy
        onShow={() => loadTabContent('tab2')}
      >
        {loading.tab2 ? (
          <SafSpinner size="large" />
        ) : tabData.tab2 ? (
          <div>
            <h2>{tabData.tab2.title}</h2>
            <p>{tabData.tab2.data}</p>
          </div>
        ) : null}
      </SafTabPanel>
      
      <SafTabPanel 
        id="tab3"
        selected={selectedTab === 'tab3'}
        lazy
        onShow={() => loadTabContent('tab3')}
      >
        {loading.tab3 ? (
          <SafSpinner size="large" />
        ) : tabData.tab3 ? (
          <div>
            <h2>{tabData.tab3.title}</h2>
            <p>{tabData.tab3.data}</p>
          </div>
        ) : null}
      </SafTabPanel>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface TabData {
  title: string;
  data: string;
}

@Component({
  selector: 'app-lazy-tab-panels',
  template: `
    <div>
      <saf-tabs>
        <saf-tab 
          id="tab1"
          [selected]="selectedTab === 'tab1'"
          (click)="handleTabClick('tab1')"
        >
          Dashboard
        </saf-tab>
        <saf-tab 
          id="tab2"
          [selected]="selectedTab === 'tab2'"
          (click)="handleTabClick('tab2')"
        >
          Analytics
        </saf-tab>
        <saf-tab 
          id="tab3"
          [selected]="selectedTab === 'tab3'"
          (click)="handleTabClick('tab3')"
        >
          Reports
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel 
        id="tab1"
        [selected]="selectedTab === 'tab1'"
        [lazy]="true"
        (show)="loadTabContent('tab1')"
      >
        <saf-spinner *ngIf="loading['tab1']" size="large"></saf-spinner>
        <div *ngIf="!loading['tab1'] && tabData['tab1']">
          <h2>{{tabData['tab1'].title}}</h2>
          <p>{{tabData['tab1'].data}}</p>
        </div>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="tab2"
        [selected]="selectedTab === 'tab2'"
        [lazy]="true"
        (show)="loadTabContent('tab2')"
      >
        <saf-spinner *ngIf="loading['tab2']" size="large"></saf-spinner>
        <div *ngIf="!loading['tab2'] && tabData['tab2']">
          <h2>{{tabData['tab2'].title}}</h2>
          <p>{{tabData['tab2'].data}}</p>
        </div>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="tab3"
        [selected]="selectedTab === 'tab3'"
        [lazy]="true"
        (show)="loadTabContent('tab3')"
      >
        <saf-spinner *ngIf="loading['tab3']" size="large"></saf-spinner>
        <div *ngIf="!loading['tab3'] && tabData['tab3']">
          <h2>{{tabData['tab3'].title}}</h2>
          <p>{{tabData['tab3'].data}}</p>
        </div>
      </saf-tab-panel>
    </div>
  `
})
export class LazyTabPanelsComponent {
  selectedTab = 'tab1';
  loadedTabs = new Set(['tab1']);
  tabData: { [key: string]: TabData } = {};
  loading: { [key: string]: boolean } = {};

  handleTabClick(tabId: string) {
    this.selectedTab = tabId;
    if (!this.loadedTabs.has(tabId)) {
      this.loadTabContent(tabId);
    }
  }

  async loadTabContent(tabId: string) {
    if (this.loadedTabs.has(tabId)) return;
    
    this.loading[tabId] = true;
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    const content: { [key: string]: TabData } = {
      tab1: { title: 'Dashboard', data: 'Real-time dashboard data...' },
      tab2: { title: 'Analytics', data: 'Complex analytics charts...' },
      tab3: { title: 'Reports', data: 'Generated report data...' }
    };
    
    this.tabData[tabId] = content[tabId];
    this.loadedTabs.add(tabId);
    this.loading[tabId] = false;
  }
}
```

### Keep Alive Tab Panels

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel } from '@saffron/core-components';
import { useState } from 'react';

function KeepAliveTabPanelExample() {
  const [selectedTab, setSelectedTab] = useState('form');
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });

  const handleFormChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }));
  };

  return (
    <div>
      <SafTabs>
        <SafTab 
          id="form"
          selected={selectedTab === 'form'}
          onClick={() => setSelectedTab('form')}
        >
          Contact Form
        </SafTab>
        <SafTab 
          id="preview"
          selected={selectedTab === 'preview'}
          onClick={() => setSelectedTab('preview')}
        >
          Preview
        </SafTab>
        <SafTab 
          id="help"
          selected={selectedTab === 'help'}
          onClick={() => setSelectedTab('help')}
        >
          Help
        </SafTab>
      </SafTabs>
      
      <SafTabPanel 
        id="form"
        selected={selectedTab === 'form'}
        keepAlive
      >
        <h2>Contact Form</h2>
        <p>Fill out the form below. Your progress will be preserved when switching tabs.</p>
        <form>
          <div>
            <label>
              Name:
              <input 
                type="text" 
                value={formData.name}
                onChange={(e) => handleFormChange('name', e.target.value)}
              />
            </label>
          </div>
          <div>
            <label>
              Email:
              <input 
                type="email" 
                value={formData.email}
                onChange={(e) => handleFormChange('email', e.target.value)}
              />
            </label>
          </div>
          <div>
            <label>
              Message:
              <textarea 
                value={formData.message}
                onChange={(e) => handleFormChange('message', e.target.value)}
                rows="4"
              />
            </label>
          </div>
        </form>
      </SafTabPanel>
      
      <SafTabPanel 
        id="preview"
        selected={selectedTab === 'preview'}
      >
        <h2>Preview</h2>
        <p>Preview of your form submission:</p>
        <div>
          <strong>Name:</strong> {formData.name || '(not provided)'}
        </div>
        <div>
          <strong>Email:</strong> {formData.email || '(not provided)'}
        </div>
        <div>
          <strong>Message:</strong> {formData.message || '(not provided)'}
        </div>
      </SafTabPanel>
      
      <SafTabPanel 
        id="help"
        selected={selectedTab === 'help'}
      >
        <h2>Help</h2>
        <p>Need assistance? Here are some tips:</p>
        <ul>
          <li>All fields are required</li>
          <li>Use a valid email address</li>
          <li>Your form data is preserved while navigating</li>
        </ul>
      </SafTabPanel>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface FormData {
  name: string;
  email: string;
  message: string;
}

@Component({
  selector: 'app-keep-alive-tabs',
  template: `
    <div>
      <saf-tabs>
        <saf-tab 
          id="form"
          [selected]="selectedTab === 'form'"
          (click)="setSelectedTab('form')"
        >
          Contact Form
        </saf-tab>
        <saf-tab 
          id="preview"
          [selected]="selectedTab === 'preview'"
          (click)="setSelectedTab('preview')"
        >
          Preview
        </saf-tab>
        <saf-tab 
          id="help"
          [selected]="selectedTab === 'help'"
          (click)="setSelectedTab('help')"
        >
          Help
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel 
        id="form"
        [selected]="selectedTab === 'form'"
        [keepAlive]="true"
      >
        <h2>Contact Form</h2>
        <p>Fill out the form below. Your progress will be preserved when switching tabs.</p>
        <form>
          <div>
            <label>
              Name:
              <input 
                type="text" 
                [(ngModel)]="formData.name"
                name="name"
              />
            </label>
          </div>
          <div>
            <label>
              Email:
              <input 
                type="email" 
                [(ngModel)]="formData.email"
                name="email"
              />
            </label>
          </div>
          <div>
            <label>
              Message:
              <textarea 
                [(ngModel)]="formData.message"
                name="message"
                rows="4"
              ></textarea>
            </label>
          </div>
        </form>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="preview"
        [selected]="selectedTab === 'preview'"
      >
        <h2>Preview</h2>
        <p>Preview of your form submission:</p>
        <div>
          <strong>Name:</strong> {{formData.name || '(not provided)'}}
        </div>
        <div>
          <strong>Email:</strong> {{formData.email || '(not provided)'}}
        </div>
        <div>
          <strong>Message:</strong> {{formData.message || '(not provided)'}}
        </div>
      </saf-tab-panel>
      
      <saf-tab-panel 
        id="help"
        [selected]="selectedTab === 'help'"
      >
        <h2>Help</h2>
        <p>Need assistance? Here are some tips:</p>
        <ul>
          <li>All fields are required</li>
          <li>Use a valid email address</li>
          <li>Your form data is preserved while navigating</li>
        </ul>
      </saf-tab-panel>
    </div>
  `
})
export class KeepAliveTabsComponent {
  selectedTab = 'form';
  formData: FormData = {
    name: '',
    email: '',
    message: ''
  };

  setSelectedTab(tabId: string) {
    this.selectedTab = tabId;
  }
}
```

### Dynamic Tab Panels with Content Loading

#### React
```jsx
import { SafTabs, SafTab, SafTabPanel, SafSpinner } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function DynamicTabPanelExample() {
  const [tabs, setTabs] = useState([]);
  const [selectedTab, setSelectedTab] = useState(null);
  const [panelContent, setPanelContent] = useState({});
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Load initial tab structure
    setTimeout(() => {
      const tabStructure = [
        { id: 'summary', title: 'Summary', hasContent: true },
        { id: 'details', title: 'Details', hasContent: true },
        { id: 'history', title: 'History', hasContent: true }
      ];
      setTabs(tabStructure);
      setSelectedTab('summary');
      setLoading(false);
      
      // Load initial content
      loadPanelContent('summary');
    }, 1000);
  }, []);

  const loadPanelContent = async (panelId) => {
    if (panelContent[panelId]) return;
    
    setPanelContent(prev => ({ ...prev, [`${panelId}_loading`]: true }));
    
    // Simulate content loading
    await new Promise(resolve => setTimeout(resolve, 800));
    
    const content = {
      summary: {
        title: 'Project Summary',
        data: 'This project involves developing a new component library...'
      },
      details: {
        title: 'Technical Details',
        data: 'Built using React and TypeScript with comprehensive testing...'
      },
      history: {
        title: 'Project History',
        data: 'Started in Q1 2024, with major milestones achieved...'
      }
    };
    
    setPanelContent(prev => ({ 
      ...prev, 
      [panelId]: content[panelId],
      [`${panelId}_loading`]: false
    }));
  };

  const handleTabClick = (tabId) => {
    setSelectedTab(tabId);
    loadPanelContent(tabId);
  };

  if (loading) {
    return <SafSpinner size="large" />;
  }

  return (
    <div>
      <SafTabs>
        {tabs.map(tab => (
          <SafTab
            key={tab.id}
            id={tab.id}
            selected={selectedTab === tab.id}
            onClick={() => handleTabClick(tab.id)}
          >
            {tab.title}
          </SafTab>
        ))}
      </SafTabs>
      
      {tabs.map(tab => (
        <SafTabPanel
          key={tab.id}
          id={tab.id}
          selected={selectedTab === tab.id}
          onShow={() => loadPanelContent(tab.id)}
        >
          {panelContent[`${tab.id}_loading`] ? (
            <div style={{ textAlign: 'center', padding: '2rem' }}>
              <SafSpinner size="medium" />
              <p>Loading {tab.title.toLowerCase()}...</p>
            </div>
          ) : panelContent[tab.id] ? (
            <div>
              <h2>{panelContent[tab.id].title}</h2>
              <p>{panelContent[tab.id].data}</p>
            </div>
          ) : null}
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

interface TabStructure {
  id: string;
  title: string;
  hasContent: boolean;
}

interface PanelContent {
  title: string;
  data: string;
}

@Component({
  selector: 'app-dynamic-tab-panels',
  template: `
    <saf-spinner *ngIf="loading" size="large"></saf-spinner>
    
    <div *ngIf="!loading">
      <saf-tabs>
        <saf-tab
          *ngFor="let tab of tabs"
          [id]="tab.id"
          [selected]="selectedTab === tab.id"
          (click)="handleTabClick(tab.id)"
        >
          {{tab.title}}
        </saf-tab>
      </saf-tabs>
      
      <saf-tab-panel
        *ngFor="let tab of tabs"
        [id]="tab.id"
        [selected]="selectedTab === tab.id"
        (show)="loadPanelContent(tab.id)"
      >
        <div *ngIf="panelContent[tab.id + '_loading']" style="text-align: center; padding: 2rem;">
          <saf-spinner size="medium"></saf-spinner>
          <p>Loading {{tab.title.toLowerCase()}}...</p>
        </div>
        <div *ngIf="!panelContent[tab.id + '_loading'] && panelContent[tab.id]">
          <h2>{{panelContent[tab.id].title}}</h2>
          <p>{{panelContent[tab.id].data}}</p>
        </div>
      </saf-tab-panel>
    </div>
  `
})
export class DynamicTabPanelsComponent implements OnInit {
  tabs: TabStructure[] = [];
  selectedTab: string | null = null;
  panelContent: { [key: string]: PanelContent | boolean } = {};
  loading = true;

  ngOnInit() {
    // Load initial tab structure
    setTimeout(() => {
      this.tabs = [
        { id: 'summary', title: 'Summary', hasContent: true },
        { id: 'details', title: 'Details', hasContent: true },
        { id: 'history', title: 'History', hasContent: true }
      ];
      this.selectedTab = 'summary';
      this.loading = false;
      
      // Load initial content
      this.loadPanelContent('summary');
    }, 1000);
  }

  handleTabClick(tabId: string) {
    this.selectedTab = tabId;
    this.loadPanelContent(tabId);
  }

  async loadPanelContent(panelId: string) {
    if (this.panelContent[panelId]) return;
    
    this.panelContent[`${panelId}_loading`] = true;
    
    // Simulate content loading
    await new Promise(resolve => setTimeout(resolve, 800));
    
    const content: { [key: string]: PanelContent } = {
      summary: {
        title: 'Project Summary',
        data: 'This project involves developing a new component library...'
      },
      details: {
        title: 'Technical Details',
        data: 'Built using React and TypeScript with comprehensive testing...'
      },
      history: {
        title: 'Project History',
        data: 'Started in Q1 2024, with major milestones achieved...'
      }
    };
    
    this.panelContent[panelId] = content[panelId];
    this.panelContent[`${panelId}_loading`] = false;
  }
}
```

## Best Practices

1. **Content Organization**: Structure panel content logically and consistently
2. **Performance Optimization**: Use lazy loading for heavy content or data
3. **State Preservation**: Use keepAlive for forms or stateful content
4. **Loading States**: Show appropriate loading indicators during content fetch
5. **Accessibility**: Ensure proper ARIA attributes and keyboard navigation
6. **Error Handling**: Handle loading errors gracefully with fallback content
7. **Memory Management**: Clean up resources when panels are unmounted
8. **Content Height**: Consider consistent panel heights to prevent layout shifts

## Accessibility Considerations

- Use proper ARIA attributes (role="tabpanel", aria-labelledby)
- Ensure each panel has a unique ID matching its corresponding tab
- Support keyboard navigation and focus management
- Provide clear loading states for screen readers
- Use semantic HTML structure within panels
- Announce content changes when panels are loaded
- Ensure sufficient color contrast and readable text

## Related Components

- `SafTab`: Tab buttons that control panel visibility
- `SafTabs`: Container component for tab groups
- `SafSpinner`: For loading states in panels
- `SafButton`: For interactive elements within panels
- `SafForm`: For form content within panels

## Notes

- Tab panels must have corresponding `SafTab` components
- The `id` prop is required and must match the associated tab's ID
- Use `lazy` loading for performance with heavy content
- `keepAlive` prevents content from being unmounted when not visible
- Content is only rendered when the panel is selected (unless keepAlive is true)
- Proper ARIA attributes are automatically applied for accessibility
