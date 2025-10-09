# SafTabs

A tabbed interface component that allows users to switch between different content panels. Implements the WAI-ARIA tablist pattern for optimal accessibility.

## Usage

```html
<saf-tabs>
  <saf-tab slot="tab">Tab 1</saf-tab>
  <saf-tab slot="tab">Tab 2</saf-tab>
  <saf-tab slot="tab">Tab 3</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Content for Tab 1</h2>
    <p>This is the content for the first tab.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Content for Tab 2</h2>
    <p>This is the content for the second tab.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Content for Tab 3</h2>
    <p>This is the content for the third tab.</p>
  </saf-tab-panel>
</saf-tabs>
```

## API

### SafTabs

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Controls the visual orientation of the tabs |
| `activeid` | `string` | auto-set | The ID of the currently active tab |

#### Properties

| Name | Type | Description |
|------|------|-------------|
| `activetab` | `HTMLElement` | Reference to the currently active tab element |

#### Events

| Name | Type | Description |
|------|------|-------------|
| `change` | `CustomEvent<HTMLElement>` | Fires when the active tab changes, with the active tab element as detail |

#### Slots

| Name | Description |
|------|-------------|
| `tab` | Container for tab elements |
| `tabpanel` | Container for tab panel elements |
| `start` | Content positioned before the tab list |
| `end` | Content positioned after the tab list |

#### Parts

| Name | Description |
|------|-------------|
| `tablist-container` | The container wrapping the entire tab list area |
| `tablist` | The element wrapping the tabs with role="tablist" |
| `tabpanel` | The container for all tab panels |

### SafTab

#### Attributes

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `disabled` | `boolean` | `false` | When true, the tab cannot be activated by user interaction |

#### Slots

| Name | Description |
|------|-------------|
| default | The tab content/label |
| `start` | Content positioned before the tab content |
| `end` | Content positioned after the tab content |

### SafTabPanel

#### Slots

| Name | Description |
|------|-------------|
| default | The panel content that is shown when the corresponding tab is active |

## Examples

### Basic Tabs

```html
<saf-tabs>
  <saf-tab slot="tab">Overview</saf-tab>
  <saf-tab slot="tab">Details</saf-tab>
  <saf-tab slot="tab">Reviews</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Overview</h2>
    <p>General information about the product.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Details</h2>
    <p>Detailed specifications and features.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Reviews</h2>
    <p>Customer reviews and ratings.</p>
  </saf-tab-panel>
</saf-tabs>
```

### Vertical Tabs

```html
<saf-tabs orientation="vertical">
  <saf-tab slot="tab">Navigation</saf-tab>
  <saf-tab slot="tab">Content</saf-tab>
  <saf-tab slot="tab">Settings</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Navigation Options</h2>
    <p>Configure navigation settings.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Content Management</h2>
    <p>Manage your content preferences.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Application Settings</h2>
    <p>General application configuration.</p>
  </saf-tab-panel>
</saf-tabs>
```

### Tabs with Icons

```html
<saf-tabs>
  <saf-tab slot="tab">
    <saf-icon slot="start" icon-name="home" appearance="solid"></saf-icon>
    Home
  </saf-tab>
  <saf-tab slot="tab">
    <saf-icon slot="start" icon-name="user" appearance="solid"></saf-icon>
    Profile
  </saf-tab>
  <saf-tab slot="tab">
    <saf-icon slot="start" icon-name="settings" appearance="solid"></saf-icon>
    Settings
    <saf-badge slot="end" appearance="accent">New</saf-badge>
  </saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Home Dashboard</h2>
    <p>Welcome to your dashboard.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>User Profile</h2>
    <p>Manage your profile information.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Settings Panel</h2>
    <p>Application settings and preferences.</p>
  </saf-tab-panel>
</saf-tabs>
```

### Disabled Tab

```html
<saf-tabs>
  <saf-tab slot="tab">Available</saf-tab>
  <saf-tab slot="tab" disabled>Disabled</saf-tab>
  <saf-tab slot="tab">Another Tab</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Available Content</h2>
    <p>This tab is accessible.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Disabled Content</h2>
    <p>This content cannot be accessed.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Another Panel</h2>
    <p>This tab is also accessible.</p>
  </saf-tab-panel>
</saf-tabs>
```

### Tabs with Additional Content

```html
<saf-tabs>
  <div slot="start">
    <saf-icon icon-name="folder" appearance="solid"></saf-icon>
  </div>
  
  <saf-tab slot="tab">Documents</saf-tab>
  <saf-tab slot="tab">Images</saf-tab>
  <saf-tab slot="tab">Videos</saf-tab>
  
  <div slot="end">
    <saf-button appearance="subtle" icon-only>
      <saf-icon icon-name="more-horizontal" appearance="solid"></saf-icon>
    </saf-button>
  </div>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Documents</h2>
    <p>Your document files are listed here.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Images</h2>
    <p>Your image files are displayed here.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Videos</h2>
    <p>Your video files are available here.</p>
  </saf-tab-panel>
</saf-tabs>
```

### Programmatic Tab Control

```html
<saf-tabs id="my-tabs">
  <saf-tab slot="tab" id="tab-1">Tab 1</saf-tab>
  <saf-tab slot="tab" id="tab-2">Tab 2</saf-tab>
  <saf-tab slot="tab" id="tab-3">Tab 3</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Panel 1</h2>
    <p>Content for first tab.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Panel 2</h2>
    <p>Content for second tab.</p>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Panel 3</h2>
    <p>Content for third tab.</p>
  </saf-tab-panel>
</saf-tabs>

<div>
  <saf-button onclick="activateTab('tab-1')">Activate Tab 1</saf-button>
  <saf-button onclick="activateTab('tab-2')">Activate Tab 2</saf-button>
  <saf-button onclick="activateTab('tab-3')">Activate Tab 3</saf-button>
</div>

<script>
  function activateTab(tabId) {
    const tabs = document.getElementById('my-tabs');
    tabs.activeid = tabId;
  }
  
  // Listen for tab changes
  document.getElementById('my-tabs').addEventListener('change', (event) => {
    console.log('Active tab changed to:', event.detail);
  });
</script>
```

### Complex Tab Content

```html
<saf-tabs>
  <saf-tab slot="tab">Form</saf-tab>
  <saf-tab slot="tab">Data</saf-tab>
  <saf-tab slot="tab">Chart</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <form>
      <saf-text-field label="Name" required></saf-text-field>
      <saf-text-field label="Email" type="email"></saf-text-field>
      <saf-textarea label="Message"></saf-textarea>
      <saf-button appearance="accent">Submit</saf-button>
    </form>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
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
          <td>200</td>
          <td>Pending</td>
        </tr>
      </tbody>
    </table>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <div>
      <h3>Performance Chart</h3>
      <!-- Chart content would go here -->
      <p>Chart visualization would be rendered in this panel.</p>
    </div>
  </saf-tab-panel>
</saf-tabs>
```

### Nested Tabs

```html
<saf-tabs>
  <saf-tab slot="tab">Category A</saf-tab>
  <saf-tab slot="tab">Category B</saf-tab>
  
  <saf-tab-panel slot="tabpanel">
    <h2>Category A</h2>
    <saf-tabs>
      <saf-tab slot="tab">Subcategory 1</saf-tab>
      <saf-tab slot="tab">Subcategory 2</saf-tab>
      
      <saf-tab-panel slot="tabpanel">
        <h3>Subcategory 1 Content</h3>
        <p>Nested content for subcategory 1.</p>
      </saf-tab-panel>
      <saf-tab-panel slot="tabpanel">
        <h3>Subcategory 2 Content</h3>
        <p>Nested content for subcategory 2.</p>
      </saf-tab-panel>
    </saf-tabs>
  </saf-tab-panel>
  <saf-tab-panel slot="tabpanel">
    <h2>Category B</h2>
    <p>Content for category B.</p>
  </saf-tab-panel>
</saf-tabs>
```

## Framework Integration

### React

```jsx
import { SafTabs, SafTab, SafTabPanel } from '@saffron/core-components-react';

function TabsExample() {
  const [activeTab, setActiveTab] = useState('tab-1');

  const handleTabChange = (event) => {
    console.log('Tab changed to:', event.detail.id);
    setActiveTab(event.detail.id);
  };

  return (
    <SafTabs activeid={activeTab} onChange={handleTabChange}>
      <SafTab slot="tab" id="tab-1">
        Overview
      </SafTab>
      <SafTab slot="tab" id="tab-2">
        Details
      </SafTab>
      <SafTab slot="tab" id="tab-3" disabled>
        Coming Soon
      </SafTab>
      
      <SafTabPanel slot="tabpanel">
        <h2>Overview Content</h2>
        <p>General information panel.</p>
      </SafTabPanel>
      <SafTabPanel slot="tabpanel">
        <h2>Details Content</h2>
        <p>Detailed information panel.</p>
      </SafTabPanel>
      <SafTabPanel slot="tabpanel">
        <h2>Coming Soon</h2>
        <p>This content is not yet available.</p>
      </SafTabPanel>
    </SafTabs>
  );
}
```

### Angular

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-tabs-demo',
  template: `
    <saf-tabs orientation="horizontal" (change)="onTabChange($event)">
      <saf-tab slot="tab" id="overview">
        <span>Overview</span>
      </saf-tab>
      <saf-tab slot="tab" id="settings" [disabled]="isSettingsDisabled">
        <span>Settings</span>
      </saf-tab>
      
      <saf-tab-panel slot="tabpanel">
        <h2>Overview Panel</h2>
        <p>Content for overview tab</p>
      </saf-tab-panel>
      <saf-tab-panel slot="tabpanel">
        <h2>Settings Panel</h2>
        <p>Content for settings tab</p>
      </saf-tab-panel>
    </saf-tabs>
  `
})
export class TabsDemoComponent {
  isSettingsDisabled = false;

  onTabChange(event: CustomEvent) {
    console.log('Active tab:', event.detail);
  }
}
```

## Accessibility Features

- **ARIA Tablist Pattern**: Implements the complete WAI-ARIA tablist pattern
- **Keyboard Navigation**: 
  - `Arrow Left/Right` (horizontal) or `Up/Down` (vertical): Navigate between tabs
  - `Home`: Move to first tab
  - `End`: Move to last tab
  - `Enter/Space`: Activate focused tab
- **Screen Reader Support**: Proper labeling with `aria-selected`, `aria-controls`, and `aria-labelledby`
- **Focus Management**: Maintains focus within the tab list and manages tab panel visibility
- **Disabled State**: Properly handles disabled tabs with `aria-disabled`

## Best Practices

1. **Logical Tab Order**: Arrange tabs in a logical sequence for users
2. **Meaningful Labels**: Use clear, descriptive tab labels
3. **Consistent Content**: Keep tab panel content relevant to the tab label
4. **Avoid Too Many Tabs**: Consider alternative navigation for more than 5-7 tabs
5. **Responsive Design**: Consider using vertical orientation on smaller screens
6. **Loading States**: Show appropriate loading indicators in tab panels when content is being fetched
7. **URL Synchronization**: Consider updating the URL when tabs change for better UX
8. **Equal Tab Widths**: Design tabs to have similar widths when possible

## Related Components

- `saf-accordion`: For vertical collapsible content sections
- `saf-button-group`: For tab-like selection without panels
- `saf-card`: For organizing content within tab panels
- `saf-breadcrumb`: For showing navigation hierarchy within tabs
