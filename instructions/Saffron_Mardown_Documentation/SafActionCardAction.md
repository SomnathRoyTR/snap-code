# SafActionCardAction Component

## Overview

SafActionCardAction is a specialized sub-component designed to represent individual actions within action cards or interactive interfaces. It provides a consistent interface for buttons, links, and other actionable elements that can be grouped together in action collections. This component is typically used as a child component of SafActionCard or in action toolbars where multiple related actions need to be displayed together.

## React API

### SafActionCardAction

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `label` | `string \| ReactNode` | Yes | - | Action button text or content |
| `variant` | `'primary' \| 'secondary' \| 'outline' \| 'ghost' \| 'danger'` | No | `'secondary'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the action |
| `icon` | `string \| ReactNode` | No | - | Icon to display with the action |
| `iconPosition` | `'start' \| 'end'` | No | `'start'` | Position of the icon relative to text |
| `disabled` | `boolean` | No | `false` | Whether the action is disabled |
| `loading` | `boolean` | No | `false` | Whether to show loading state |
| `href` | `string` | No | - | URL for link actions |
| `target` | `string` | No | - | Target for link actions |
| `type` | `'button' \| 'submit' \| 'reset' \| 'link'` | No | `'button'` | Type of action element |
| `fullWidth` | `boolean` | No | `false` | Whether action takes full container width |
| `tooltip` | `string \| ReactNode` | No | - | Tooltip text for the action |
| `badge` | `string \| ReactNode` | No | - | Badge or notification indicator |
| `shortcut` | `string` | No | - | Keyboard shortcut for the action |
| `destructive` | `boolean` | No | `false` | Whether action is destructive/dangerous |
| `confirmation` | `ConfirmationConfig` | No | - | Confirmation dialog configuration |
| `onClick` | `(event: MouseEvent) => void \| Promise<void>` | No | - | Callback when action is clicked |
| `onDoubleClick` | `(event: MouseEvent) => void` | No | - | Callback for double-click events |
| `onKeyDown` | `(event: KeyboardEvent) => void` | No | - | Callback for key down events |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### ConfirmationConfig Interface

```typescript
interface ConfirmationConfig {
  title: string;
  message: string;
  confirmLabel?: string;
  cancelLabel?: string;
  variant?: 'default' | 'danger';
  onConfirm?: () => void | Promise<void>;
  onCancel?: () => void;
}
```

## Angular API

### saf-action-card-action

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[label]` | `string \| TemplateRef` | Yes | - | Action button text or content |
| `[variant]` | `'primary' \| 'secondary' \| 'outline' \| 'ghost' \| 'danger'` | No | `'secondary'` | Visual style variant |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the action |
| `[icon]` | `string \| TemplateRef` | No | - | Icon to display with the action |
| `[iconPosition]` | `'start' \| 'end'` | No | `'start'` | Position of the icon relative to text |
| `[disabled]` | `boolean` | No | `false` | Whether the action is disabled |
| `[loading]` | `boolean` | No | `false` | Whether to show loading state |
| `[href]` | `string` | No | - | URL for link actions |
| `[target]` | `string` | No | - | Target for link actions |
| `[type]` | `'button' \| 'submit' \| 'reset' \| 'link'` | No | `'button'` | Type of action element |
| `[fullWidth]` | `boolean` | No | `false` | Whether action takes full container width |
| `[tooltip]` | `string \| TemplateRef` | No | - | Tooltip text for the action |
| `[badge]` | `string \| TemplateRef` | No | - | Badge or notification indicator |
| `[shortcut]` | `string` | No | - | Keyboard shortcut for the action |
| `[destructive]` | `boolean` | No | `false` | Whether action is destructive/dangerous |
| `[confirmation]` | `ConfirmationConfig` | No | - | Confirmation dialog configuration |
| `(click)` | `EventEmitter<MouseEvent>` | No | - | Event when action is clicked |
| `(doubleClick)` | `EventEmitter<MouseEvent>` | No | - | Event for double-click events |
| `(keydown)` | `EventEmitter<KeyboardEvent>` | No | - | Event for key down events |

## Usage Examples

### Basic Action Groups

#### React
```jsx
import { SafActionCardAction, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const BasicActionGroupExample = () => {
  const [loading, setLoading] = useState({});
  const [notifications, setNotifications] = useState({ messages: 3, alerts: 1 });

  const handleAction = async (actionId) => {
    setLoading(prev => ({ ...prev, [actionId]: true }));
    
    // Simulate async operation
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    setLoading(prev => ({ ...prev, [actionId]: false }));
    console.log(`Action ${actionId} completed`);
  };

  const handleDestructiveAction = async () => {
    // This would show confirmation dialog
    console.log('Destructive action confirmed');
    await handleAction('delete');
  };

  return (
    <div className="action-group-demo">
      <h2>Document Actions</h2>
      
      <div className="primary-actions">
        <SafActionCardAction
          label="Save Document"
          variant="primary"
          icon={<SafIcon name="save" />}
          loading={loading.save}
          onClick={() => handleAction('save')}
          shortcut="Ctrl+S"
        />
        
        <SafActionCardAction
          label="Share"
          variant="secondary"
          icon={<SafIcon name="share" />}
          loading={loading.share}
          onClick={() => handleAction('share')}
          tooltip="Share with team members"
        />
        
        <SafActionCardAction
          label="Export"
          variant="outline"
          icon={<SafIcon name="download" />}
          loading={loading.export}
          onClick={() => handleAction('export')}
        />
      </div>

      <div className="secondary-actions">
        <SafActionCardAction
          label="Messages"
          variant="ghost"
          icon={<SafIcon name="mail" />}
          badge={notifications.messages > 0 ? notifications.messages : null}
          onClick={() => handleAction('messages')}
        />
        
        <SafActionCardAction
          label="Alerts"
          variant="ghost"
          icon={<SafIcon name="bell" />}
          badge={notifications.alerts > 0 ? 
            <SafBadge variant="danger" size="small">{notifications.alerts}</SafBadge> : null
          }
          onClick={() => handleAction('alerts')}
        />
        
        <SafActionCardAction
          label="Settings"
          variant="ghost"
          icon={<SafIcon name="settings" />}
          onClick={() => handleAction('settings')}
          shortcut="Ctrl+,"
        />
      </div>

      <div className="danger-actions">
        <SafActionCardAction
          label="Delete Document"
          variant="danger"
          icon={<SafIcon name="trash" />}
          destructive={true}
          loading={loading.delete}
          confirmation={{
            title: 'Delete Document',
            message: 'Are you sure you want to delete this document? This action cannot be undone.',
            confirmLabel: 'Delete',
            cancelLabel: 'Cancel',
            variant: 'danger',
            onConfirm: handleDestructiveAction
          }}
          onClick={() => handleAction('delete')}
        />
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// basic-action-group.component.ts
import { Component } from '@angular/core';

interface ConfirmationConfig {
  title: string;
  message: string;
  confirmLabel?: string;
  cancelLabel?: string;
  variant?: 'default' | 'danger';
  onConfirm?: () => void | Promise<void>;
  onCancel?: () => void;
}

@Component({
  selector: 'app-basic-action-group',
  template: `
    <div class="action-group-demo">
      <h2>Document Actions</h2>
      
      <div class="primary-actions">
        <saf-action-card-action
          label="Save Document"
          variant="primary"
          [loading]="loading.save"
          shortcut="Ctrl+S"
          (click)="handleAction('save')">
          <saf-icon name="save" slot="icon"></saf-icon>
        </saf-action-card-action>
        
        <saf-action-card-action
          label="Share"
          variant="secondary"
          [loading]="loading.share"
          tooltip="Share with team members"
          (click)="handleAction('share')">
          <saf-icon name="share" slot="icon"></saf-icon>
        </saf-action-card-action>
        
        <saf-action-card-action
          label="Export"
          variant="outline"
          [loading]="loading.export"
          (click)="handleAction('export')">
          <saf-icon name="download" slot="icon"></saf-icon>
        </saf-action-card-action>
      </div>

      <div class="secondary-actions">
        <saf-action-card-action
          label="Messages"
          variant="ghost"
          [badge]="notifications.messages > 0 ? notifications.messages : null"
          (click)="handleAction('messages')">
          <saf-icon name="mail" slot="icon"></saf-icon>
        </saf-action-card-action>
        
        <saf-action-card-action
          label="Alerts"
          variant="ghost"
          (click)="handleAction('alerts')">
          <saf-icon name="bell" slot="icon"></saf-icon>
          <saf-badge 
            *ngIf="notifications.alerts > 0" 
            variant="danger" 
            size="small"
            slot="badge">
            {{ notifications.alerts }}
          </saf-badge>
        </saf-action-card-action>
        
        <saf-action-card-action
          label="Settings"
          variant="ghost"
          shortcut="Ctrl+,"
          (click)="handleAction('settings')">
          <saf-icon name="settings" slot="icon"></saf-icon>
        </saf-action-card-action>
      </div>

      <div class="danger-actions">
        <saf-action-card-action
          label="Delete Document"
          variant="danger"
          [destructive]="true"
          [loading]="loading.delete"
          [confirmation]="deleteConfirmation"
          (click)="handleAction('delete')">
          <saf-icon name="trash" slot="icon"></saf-icon>
        </saf-action-card-action>
      </div>
    </div>
  `
})
export class BasicActionGroupComponent {
  loading: { [key: string]: boolean } = {};
  notifications = { messages: 3, alerts: 1 };

  deleteConfirmation: ConfirmationConfig = {
    title: 'Delete Document',
    message: 'Are you sure you want to delete this document? This action cannot be undone.',
    confirmLabel: 'Delete',
    cancelLabel: 'Cancel',
    variant: 'danger',
    onConfirm: () => this.handleDestructiveAction()
  };

  async handleAction(actionId: string) {
    this.loading = { ...this.loading, [actionId]: true };
    
    // Simulate async operation
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    this.loading = { ...this.loading, [actionId]: false };
    console.log(`Action ${actionId} completed`);
  }

  async handleDestructiveAction() {
    console.log('Destructive action confirmed');
    await this.handleAction('delete');
  }
}
```

### Action Toolbar with Contextual Actions

#### React
```jsx
import { SafActionCardAction, SafIcon } from '@saffron/react';
import { useState } from 'react';

const ActionToolbarExample = () => {
  const [selectedItems, setSelectedItems] = useState([]);
  const [viewMode, setViewMode] = useState('grid');
  const [sortBy, setSortBy] = useState('name');

  const hasSelection = selectedItems.length > 0;
  const isMultiSelection = selectedItems.length > 1;

  const handleBulkAction = async (action) => {
    console.log(`Performing ${action} on ${selectedItems.length} items`);
    // Simulate bulk operation
    await new Promise(resolve => setTimeout(resolve, 1000));
    setSelectedItems([]);
  };

  const toggleViewMode = () => {
    setViewMode(prev => prev === 'grid' ? 'list' : 'grid');
  };

  const handleSort = (newSortBy) => {
    setSortBy(newSortBy);
    console.log('Sorting by:', newSortBy);
  };

  return (
    <div className="action-toolbar-demo">
      <div className="toolbar-section">
        <h3>File Manager Toolbar</h3>
        
        {/* Main Actions */}
        <div className="main-actions">
          <SafActionCardAction
            label="New Folder"
            variant="primary"
            icon={<SafIcon name="folder-plus" />}
            onClick={() => console.log('Create new folder')}
          />
          
          <SafActionCardAction
            label="Upload"
            variant="secondary"
            icon={<SafIcon name="upload" />}
            onClick={() => console.log('Upload files')}
          />
          
          <SafActionCardAction
            label="Import"
            variant="outline"
            icon={<SafIcon name="file-import" />}
            onClick={() => console.log('Import files')}
          />
        </div>

        {/* Selection-based Actions */}
        {hasSelection && (
          <div className="selection-actions">
            <span className="selection-count">
              {selectedItems.length} item{selectedItems.length !== 1 ? 's' : ''} selected
            </span>
            
            <SafActionCardAction
              label="Download"
              variant="outline"
              icon={<SafIcon name="download" />}
              onClick={() => handleBulkAction('download')}
            />
            
            <SafActionCardAction
              label="Move"
              variant="outline"
              icon={<SafIcon name="move" />}
              onClick={() => handleBulkAction('move')}
            />
            
            <SafActionCardAction
              label="Copy"
              variant="outline"
              icon={<SafIcon name="copy" />}
              onClick={() => handleBulkAction('copy')}
            />
            
            {isMultiSelection && (
              <SafActionCardAction
                label="Archive"
                variant="outline"
                icon={<SafIcon name="archive" />}
                onClick={() => handleBulkAction('archive')}
              />
            )}
            
            <SafActionCardAction
              label="Delete"
              variant="danger"
              icon={<SafIcon name="trash" />}
              destructive={true}
              confirmation={{
                title: 'Delete Files',
                message: `Are you sure you want to delete ${selectedItems.length} item${selectedItems.length !== 1 ? 's' : ''}?`,
                confirmLabel: 'Delete',
                variant: 'danger'
              }}
              onClick={() => handleBulkAction('delete')}
            />
          </div>
        )}

        {/* View Controls */}
        <div className="view-controls">
          <SafActionCardAction
            label={viewMode === 'grid' ? 'List View' : 'Grid View'}
            variant="ghost"
            icon={<SafIcon name={viewMode === 'grid' ? 'list' : 'grid'} />}
            onClick={toggleViewMode}
            tooltip={`Switch to ${viewMode === 'grid' ? 'list' : 'grid'} view`}
          />
          
          <SafActionCardAction
            label="Sort by Name"
            variant={sortBy === 'name' ? 'secondary' : 'ghost'}
            icon={<SafIcon name="sort-alpha" />}
            onClick={() => handleSort('name')}
          />
          
          <SafActionCardAction
            label="Sort by Date"
            variant={sortBy === 'date' ? 'secondary' : 'ghost'}
            icon={<SafIcon name="sort-numeric" />}
            onClick={() => handleSort('date')}
          />
          
          <SafActionCardAction
            label="Sort by Size"
            variant={sortBy === 'size' ? 'secondary' : 'ghost'}
            icon={<SafIcon name="sort-amount" />}
            onClick={() => handleSort('size')}
          />
        </div>

        {/* Settings and More */}
        <div className="utility-actions">
          <SafActionCardAction
            label="Refresh"
            variant="ghost"
            icon={<SafIcon name="refresh" />}
            onClick={() => console.log('Refresh view')}
            shortcut="F5"
            tooltip="Refresh the file list"
          />
          
          <SafActionCardAction
            label="Filter"
            variant="ghost"
            icon={<SafIcon name="filter" />}
            onClick={() => console.log('Show filters')}
            tooltip="Show filter options"
          />
          
          <SafActionCardAction
            label="More Actions"
            variant="ghost"
            icon={<SafIcon name="more-horizontal" />}
            onClick={() => console.log('Show more actions')}
          />
        </div>
      </div>

      {/* Demo Selection Controls */}
      <div className="demo-controls">
        <h4>Demo Controls (Select items to see contextual actions)</h4>
        <button onClick={() => setSelectedItems(['file1'])}>
          Select 1 item
        </button>
        <button onClick={() => setSelectedItems(['file1', 'file2', 'file3'])}>
          Select 3 items
        </button>
        <button onClick={() => setSelectedItems([])}>
          Clear selection
        </button>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// action-toolbar.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-action-toolbar',
  template: `
    <div class="action-toolbar-demo">
      <div class="toolbar-section">
        <h3>File Manager Toolbar</h3>
        
        <!-- Main Actions -->
        <div class="main-actions">
          <saf-action-card-action
            label="New Folder"
            variant="primary"
            (click)="createNewFolder()">
            <saf-icon name="folder-plus" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Upload"
            variant="secondary"
            (click)="uploadFiles()">
            <saf-icon name="upload" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Import"
            variant="outline"
            (click)="importFiles()">
            <saf-icon name="file-import" slot="icon"></saf-icon>
          </saf-action-card-action>
        </div>

        <!-- Selection-based Actions -->
        <div *ngIf="hasSelection" class="selection-actions">
          <span class="selection-count">
            {{ selectedItems.length }} item{{ selectedItems.length !== 1 ? 's' : '' }} selected
          </span>
          
          <saf-action-card-action
            label="Download"
            variant="outline"
            (click)="handleBulkAction('download')">
            <saf-icon name="download" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Move"
            variant="outline"
            (click)="handleBulkAction('move')">
            <saf-icon name="move" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Copy"
            variant="outline"
            (click)="handleBulkAction('copy')">
            <saf-icon name="copy" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            *ngIf="isMultiSelection"
            label="Archive"
            variant="outline"
            (click)="handleBulkAction('archive')">
            <saf-icon name="archive" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Delete"
            variant="danger"
            [destructive]="true"
            [confirmation]="deleteConfirmation"
            (click)="handleBulkAction('delete')">
            <saf-icon name="trash" slot="icon"></saf-icon>
          </saf-action-card-action>
        </div>

        <!-- View Controls -->
        <div class="view-controls">
          <saf-action-card-action
            [label]="viewMode === 'grid' ? 'List View' : 'Grid View'"
            variant="ghost"
            [tooltip]="'Switch to ' + (viewMode === 'grid' ? 'list' : 'grid') + ' view'"
            (click)="toggleViewMode()">
            <saf-icon [name]="viewMode === 'grid' ? 'list' : 'grid'" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Sort by Name"
            [variant]="sortBy === 'name' ? 'secondary' : 'ghost'"
            (click)="handleSort('name')">
            <saf-icon name="sort-alpha" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Sort by Date"
            [variant]="sortBy === 'date' ? 'secondary' : 'ghost'"
            (click)="handleSort('date')">
            <saf-icon name="sort-numeric" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Sort by Size"
            [variant]="sortBy === 'size' ? 'secondary' : 'ghost'"
            (click)="handleSort('size')">
            <saf-icon name="sort-amount" slot="icon"></saf-icon>
          </saf-action-card-action>
        </div>

        <!-- Settings and More -->
        <div class="utility-actions">
          <saf-action-card-action
            label="Refresh"
            variant="ghost"
            shortcut="F5"
            tooltip="Refresh the file list"
            (click)="refreshView()">
            <saf-icon name="refresh" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="Filter"
            variant="ghost"
            tooltip="Show filter options"
            (click)="showFilters()">
            <saf-icon name="filter" slot="icon"></saf-icon>
          </saf-action-card-action>
          
          <saf-action-card-action
            label="More Actions"
            variant="ghost"
            (click)="showMoreActions()">
            <saf-icon name="more-horizontal" slot="icon"></saf-icon>
          </saf-action-card-action>
        </div>
      </div>

      <!-- Demo Selection Controls -->
      <div class="demo-controls">
        <h4>Demo Controls (Select items to see contextual actions)</h4>
        <button (click)="selectItems(['file1'])">Select 1 item</button>
        <button (click)="selectItems(['file1', 'file2', 'file3'])">Select 3 items</button>
        <button (click)="selectItems([])">Clear selection</button>
      </div>
    </div>
  `
})
export class ActionToolbarComponent {
  selectedItems: string[] = [];
  viewMode: 'grid' | 'list' = 'grid';
  sortBy: 'name' | 'date' | 'size' = 'name';

  get hasSelection(): boolean {
    return this.selectedItems.length > 0;
  }

  get isMultiSelection(): boolean {
    return this.selectedItems.length > 1;
  }

  get deleteConfirmation(): ConfirmationConfig {
    return {
      title: 'Delete Files',
      message: `Are you sure you want to delete ${this.selectedItems.length} item${this.selectedItems.length !== 1 ? 's' : ''}?`,
      confirmLabel: 'Delete',
      variant: 'danger'
    };
  }

  selectItems(items: string[]) {
    this.selectedItems = items;
  }

  async handleBulkAction(action: string) {
    console.log(`Performing ${action} on ${this.selectedItems.length} items`);
    // Simulate bulk operation
    await new Promise(resolve => setTimeout(resolve, 1000));
    this.selectedItems = [];
  }

  toggleViewMode() {
    this.viewMode = this.viewMode === 'grid' ? 'list' : 'grid';
  }

  handleSort(newSortBy: 'name' | 'date' | 'size') {
    this.sortBy = newSortBy;
    console.log('Sorting by:', newSortBy);
  }

  createNewFolder() {
    console.log('Create new folder');
  }

  uploadFiles() {
    console.log('Upload files');
  }

  importFiles() {
    console.log('Import files');
  }

  refreshView() {
    console.log('Refresh view');
  }

  showFilters() {
    console.log('Show filters');
  }

  showMoreActions() {
    console.log('Show more actions');
  }
}
```

## Best Practices

1. **Action Grouping**
   - Group related actions together logically
   - Use visual separators between action groups
   - Prioritize primary actions visually

2. **Contextual Behavior**
   - Show/hide actions based on current state
   - Adapt action availability to user permissions
   - Provide appropriate feedback for state changes

3. **Visual Hierarchy**
   - Use variants to establish action importance
   - Implement consistent icon usage
   - Apply proper spacing and alignment

4. **Interaction Design**
   - Provide immediate feedback for user actions
   - Use loading states for async operations
   - Implement confirmation for destructive actions

5. **Keyboard Support**
   - Define logical keyboard shortcuts
   - Support standard navigation patterns
   - Provide alternative access methods

## Accessibility Considerations

1. **ARIA Support**
   - Use proper button roles and states
   - Implement aria-describedby for tooltips
   - Provide meaningful action descriptions

2. **Keyboard Navigation**
   - Support Tab navigation through actions
   - Implement Enter/Space activation
   - Handle keyboard shortcuts appropriately

3. **Screen Reader Compatibility**
   - Announce action state changes
   - Provide context for action outcomes
   - Use semantic markup for action groups

4. **Visual Accessibility**
   - Ensure sufficient color contrast
   - Provide clear focus indicators
   - Support high contrast mode

## Related Components

- **SafActionCard**: Parent container for action cards
- **SafButton**: Basic button component
- **SafIcon**: Icons for visual action identification
- **SafBadge**: Notification and status indicators
- **SafTooltip**: Additional context for actions

## Notes

- Action card actions automatically handle async operations and loading states
- Custom CSS variables available for consistent theming
- Built-in support for confirmation dialogs and destructive actions
- Optimized for both desktop and mobile interaction patterns
- Compatible with keyboard navigation and screen readers
- Supports both controlled and uncontrolled usage patterns
