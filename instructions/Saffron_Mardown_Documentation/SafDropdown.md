# SafDropdown Component

## Overview

SafDropdown is a versatile dropdown component designed for displaying contextual menus, action lists, selection options, and navigation elements. It provides flexible positioning, keyboard navigation, search functionality, and advanced features like grouping, multi-level menus, and custom content. The component is ideal for legal action menus, document operations, case management workflows, user preferences, navigation menus, and any application requiring dropdown interactions with comprehensive accessibility support.

## React API

### SafDropdown

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `trigger` | `ReactNode` | Yes | - | Element that triggers the dropdown |
| `children` | `ReactNode` | Yes | - | Dropdown content |
| `open` | `boolean` | No | `false` | Controls dropdown visibility |
| `defaultOpen` | `boolean` | No | `false` | Default open state (uncontrolled) |
| `onOpenChange` | `(open: boolean) => void` | No | - | Callback when open state changes |
| `placement` | `'top' \| 'bottom' \| 'left' \| 'right' \| 'top-start' \| 'top-end' \| 'bottom-start' \| 'bottom-end' \| 'left-start' \| 'left-end' \| 'right-start' \| 'right-end'` | No | `'bottom-start'` | Dropdown positioning |
| `offset` | `number \| [number, number]` | No | `4` | Distance from trigger element |
| `autoPlacement` | `boolean` | No | `true` | Automatically adjust placement if no space |
| `closeOnSelect` | `boolean` | No | `true` | Close dropdown when item is selected |
| `closeOnClickOutside` | `boolean` | No | `true` | Close dropdown when clicking outside |
| `closeOnEscape` | `boolean` | No | `true` | Close dropdown when Escape is pressed |
| `disabled` | `boolean` | No | `false` | Disable dropdown functionality |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Dropdown size |
| `variant` | `'default' \| 'menu' \| 'select' \| 'context' \| 'navigation'` | No | `'default'` | Dropdown style variant |
| `width` | `'auto' \| 'trigger' \| number \| string` | No | `'auto'` | Dropdown width |
| `maxHeight` | `string \| number` | No | `'300px'` | Maximum dropdown height |
| `searchable` | `boolean` | No | `false` | Enable search functionality |
| `searchPlaceholder` | `string` | No | `'Search...'` | Search input placeholder |
| `loading` | `boolean` | No | `false` | Show loading state |
| `empty` | `ReactNode` | No | `'No items found'` | Content when no items available |
| `portal` | `boolean` | No | `true` | Render dropdown in portal |
| `portalContainer` | `Element` | No | `document.body` | Portal container element |
| `zIndex` | `number` | No | `1000` | Dropdown z-index |
| `animation` | `boolean \| 'fade' \| 'slide' \| 'scale'` | No | `'fade'` | Animation type |
| `animationDuration` | `number` | No | `200` | Animation duration in milliseconds |
| `flip` | `boolean` | No | `true` | Flip placement when no space |
| `shift` | `boolean` | No | `true` | Shift position to stay in viewport |
| `arrow` | `boolean` | No | `false` | Show arrow pointer |
| `className` | `string` | No | - | Additional CSS classes |
| `dropdownClassName` | `string` | No | - | Dropdown content CSS classes |
| `testId` | `string` | No | - | Test identifier |

### SafDropdownItem

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `children` | `ReactNode` | Yes | - | Item content |
| `value` | `any` | No | - | Item value for selection |
| `disabled` | `boolean` | No | `false` | Disable item interaction |
| `selected` | `boolean` | No | `false` | Mark item as selected |
| `icon` | `string \| ReactNode` | No | - | Item icon |
| `description` | `string` | No | - | Item description text |
| `shortcut` | `string` | No | - | Keyboard shortcut display |
| `destructive` | `boolean` | No | `false` | Mark as destructive action |
| `loading` | `boolean` | No | `false` | Show loading state |
| `onClick` | `(event: React.MouseEvent) => void` | No | - | Click handler |
| `onSelect` | `(value: any) => void` | No | - | Selection handler |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### SafDropdownGroup

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `children` | `ReactNode` | Yes | - | Group content |
| `label` | `string` | No | - | Group label |
| `collapsible` | `boolean` | No | `false` | Allow group collapse |
| `defaultCollapsed` | `boolean` | No | `false` | Default collapsed state |
| `separator` | `boolean` | No | `true` | Show separator after group |
| `className` | `string` | No | - | Additional CSS classes |

### SafDropdownSeparator

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `className` | `string` | No | - | Additional CSS classes |

### Dropdown Context

```typescript
interface DropdownContextValue {
  open: boolean;
  close: () => void;
  toggle: () => void;
  selectedValue: any;
  setSelectedValue: (value: any) => void;
  searchQuery: string;
  setSearchQuery: (query: string) => void;
}

// Hook for accessing dropdown context
const useDropdown = (): DropdownContextValue;
```

## Angular API

### saf-dropdown

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[open]` | `boolean` | No | `false` | Controls dropdown visibility |
| `[defaultOpen]` | `boolean` | No | `false` | Default open state (uncontrolled) |
| `[placement]` | `'top' \| 'bottom' \| 'left' \| 'right' \| 'top-start' \| 'top-end' \| 'bottom-start' \| 'bottom-end' \| 'left-start' \| 'left-end' \| 'right-start' \| 'right-end'` | No | `'bottom-start'` | Dropdown positioning |
| `[offset]` | `number \| [number, number]` | No | `4` | Distance from trigger element |
| `[autoPlacement]` | `boolean` | No | `true` | Automatically adjust placement if no space |
| `[closeOnSelect]` | `boolean` | No | `true` | Close dropdown when item is selected |
| `[closeOnClickOutside]` | `boolean` | No | `true` | Close dropdown when clicking outside |
| `[closeOnEscape]` | `boolean` | No | `true` | Close dropdown when Escape is pressed |
| `[disabled]` | `boolean` | No | `false` | Disable dropdown functionality |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Dropdown size |
| `[variant]` | `'default' \| 'menu' \| 'select' \| 'context' \| 'navigation'` | No | `'default'` | Dropdown style variant |
| `[width]` | `'auto' \| 'trigger' \| number \| string` | No | `'auto'` | Dropdown width |
| `[maxHeight]` | `string \| number` | No | `'300px'` | Maximum dropdown height |
| `[searchable]` | `boolean` | No | `false` | Enable search functionality |
| `[searchPlaceholder]` | `string` | No | `'Search...'` | Search input placeholder |
| `[loading]` | `boolean` | No | `false` | Show loading state |
| `[empty]` | `string \| TemplateRef` | No | `'No items found'` | Content when no items available |
| `[portal]` | `boolean` | No | `true` | Render dropdown in portal |
| `[zIndex]` | `number` | No | `1000` | Dropdown z-index |
| `[animation]` | `boolean \| 'fade' \| 'slide' \| 'scale'` | No | `'fade'` | Animation type |
| `[animationDuration]` | `number` | No | `200` | Animation duration in milliseconds |
| `[flip]` | `boolean` | No | `true` | Flip placement when no space |
| `[shift]` | `boolean` | No | `true` | Shift position to stay in viewport |
| `[arrow]` | `boolean` | No | `false` | Show arrow pointer |
| `(openChange)` | `EventEmitter<boolean>` | No | - | Event when open state changes |

### saf-dropdown-item

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[value]` | `any` | No | - | Item value for selection |
| `[disabled]` | `boolean` | No | `false` | Disable item interaction |
| `[selected]` | `boolean` | No | `false` | Mark item as selected |
| `[icon]` | `string` | No | - | Item icon name |
| `[description]` | `string` | No | - | Item description text |
| `[shortcut]` | `string` | No | - | Keyboard shortcut display |
| `[destructive]` | `boolean` | No | `false` | Mark as destructive action |
| `[loading]` | `boolean` | No | `false` | Show loading state |
| `(click)` | `EventEmitter<MouseEvent>` | No | - | Click event |
| `(select)` | `EventEmitter<any>` | No | - | Selection event |

### saf-dropdown-group

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[label]` | `string` | No | - | Group label |
| `[collapsible]` | `boolean` | No | `false` | Allow group collapse |
| `[defaultCollapsed]` | `boolean` | No | `false` | Default collapsed state |
| `[separator]` | `boolean` | No | `true` | Show separator after group |

## Usage Examples

### Legal Document Actions Menu

#### React
```jsx
import { SafDropdown, SafDropdownItem, SafDropdownGroup, SafDropdownSeparator, SafButton, SafIcon, SafChip } from '@saffron/react';
import { useState } from 'react';

const LegalDocumentActionsMenu = () => {
  const [selectedDocument, setSelectedDocument] = useState(null);
  const [actionLoading, setActionLoading] = useState(null);

  const documentData = {
    id: 'DOC-2024-001',
    name: 'Contract Amendment - Global Corp Services Agreement.pdf',
    type: 'Contract',
    status: 'Under Review',
    size: '2.4 MB',
    lastModified: new Date('2024-01-28'),
    version: '2.1',
    confidentiality: 'Confidential',
    permissions: {
      canEdit: true,
      canDelete: true,
      canShare: true,
      canDownload: true,
      canComment: true,
      canVersion: true
    }
  };

  const handleAction = async (action, docId) => {
    setActionLoading(action);
    try {
      await new Promise(resolve => setTimeout(resolve, 1500));
      console.log(`Action ${action} performed on document ${docId}`);
      
      switch (action) {
        case 'download':
          // Simulate download
          console.log('Downloading document...');
          break;
        case 'edit':
          console.log('Opening document for editing...');
          break;
        case 'share':
          console.log('Opening share dialog...');
          break;
        case 'version':
          console.log('Creating new version...');
          break;
        case 'comment':
          console.log('Opening comment panel...');
          break;
        case 'duplicate':
          console.log('Duplicating document...');
          break;
        case 'move':
          console.log('Opening move dialog...');
          break;
        case 'archive':
          console.log('Archiving document...');
          break;
        case 'delete':
          console.log('Deleting document...');
          break;
        default:
          console.log('Unknown action:', action);
      }
    } catch (error) {
      console.error('Error performing action:', error);
    } finally {
      setActionLoading(null);
    }
  };

  const handleBulkAction = async (action) => {
    console.log('Bulk action:', action);
    // Handle bulk actions for multiple documents
  };

  return (
    <div className="legal-document-actions-demo">
      <h2>Legal Document Management</h2>

      {/* Document Card with Actions */}
      <div className="document-card">
        <div className="document-info">
          <div className="document-header">
            <SafIcon name="file-text" size="large" />
            <div className="document-details">
              <h3>{documentData.name}</h3>
              <div className="document-meta">
                <SafChip label={documentData.type} variant="soft" color="primary" size="small" />
                <SafChip label={documentData.status} variant="soft" color="warning" size="small" />
                <SafChip label={documentData.confidentiality} variant="soft" color="danger" size="small" />
                <span className="document-size">{documentData.size}</span>
                <span className="document-version">v{documentData.version}</span>
              </div>
            </div>
          </div>
        </div>

        <div className="document-actions">
          {/* Primary Actions */}
          <SafButton
            variant="primary"
            size="small"
            icon="eye"
            onClick={() => console.log('View document')}
          >
            View
          </SafButton>

          <SafButton
            variant="secondary"
            size="small"
            icon="download"
            onClick={() => handleAction('download', documentData.id)}
            loading={actionLoading === 'download'}
            disabled={!documentData.permissions.canDownload}
          >
            Download
          </SafButton>

          {/* More Actions Dropdown */}
          <SafDropdown
            trigger={
              <SafButton
                variant="tertiary"
                size="small"
                icon="more-horizontal"
                aria-label="More document actions"
              />
            }
            placement="bottom-end"
            closeOnSelect={true}
            searchable={true}
            searchPlaceholder="Search actions..."
          >
            <SafDropdownGroup label="Edit Actions">
              <SafDropdownItem
                icon="edit"
                shortcut="Ctrl+E"
                disabled={!documentData.permissions.canEdit}
                loading={actionLoading === 'edit'}
                onSelect={() => handleAction('edit', documentData.id)}
              >
                Edit Document
                <span className="item-description">Open in document editor</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="message-square"
                shortcut="Ctrl+M"
                disabled={!documentData.permissions.canComment}
                loading={actionLoading === 'comment'}
                onSelect={() => handleAction('comment', documentData.id)}
              >
                Add Comment
                <span className="item-description">Add review comments</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="git-branch"
                disabled={!documentData.permissions.canVersion}
                loading={actionLoading === 'version'}
                onSelect={() => handleAction('version', documentData.id)}
              >
                Create Version
                <span className="item-description">Create new document version</span>
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownSeparator />

            <SafDropdownGroup label="Share & Collaborate">
              <SafDropdownItem
                icon="share"
                shortcut="Ctrl+S"
                disabled={!documentData.permissions.canShare}
                loading={actionLoading === 'share'}
                onSelect={() => handleAction('share', documentData.id)}
              >
                Share Document
                <span className="item-description">Share with team members</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="link"
                onSelect={() => handleAction('copy-link', documentData.id)}
              >
                Copy Link
                <span className="item-description">Copy shareable link</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="mail"
                onSelect={() => handleAction('email', documentData.id)}
              >
                Email Document
                <span className="item-description">Send via email</span>
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownSeparator />

            <SafDropdownGroup label="Organization">
              <SafDropdownItem
                icon="copy"
                loading={actionLoading === 'duplicate'}
                onSelect={() => handleAction('duplicate', documentData.id)}
              >
                Duplicate
                <span className="item-description">Create a copy</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="folder"
                loading={actionLoading === 'move'}
                onSelect={() => handleAction('move', documentData.id)}
              >
                Move to Folder
                <span className="item-description">Organize in folder structure</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="tag"
                onSelect={() => handleAction('tags', documentData.id)}
              >
                Manage Tags
                <span className="item-description">Add or edit document tags</span>
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownSeparator />

            <SafDropdownGroup label="Document Actions">
              <SafDropdownItem
                icon="archive"
                loading={actionLoading === 'archive'}
                onSelect={() => handleAction('archive', documentData.id)}
              >
                Archive Document
                <span className="item-description">Move to archive</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="trash"
                destructive={true}
                disabled={!documentData.permissions.canDelete}
                loading={actionLoading === 'delete'}
                onSelect={() => handleAction('delete', documentData.id)}
              >
                Delete Document
                <span className="item-description">Permanently delete</span>
              </SafDropdownItem>
            </SafDropdownGroup>
          </SafDropdown>
        </div>
      </div>

      {/* Bulk Actions for Multiple Documents */}
      <div className="bulk-actions-section">
        <h3>Bulk Document Actions</h3>
        <div className="bulk-actions-bar">
          <span className="selection-info">3 documents selected</span>
          
          <SafDropdown
            trigger={
              <SafButton variant="secondary" icon="layers">
                Bulk Actions
              </SafButton>
            }
            placement="bottom-start"
            width="300px"
          >
            <SafDropdownGroup label="Bulk Edit">
              <SafDropdownItem
                icon="download"
                onSelect={() => handleBulkAction('download-all')}
              >
                Download All
                <span className="item-description">Download as ZIP archive</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="share"
                onSelect={() => handleBulkAction('share-all')}
              >
                Share Selected
                <span className="item-description">Share multiple documents</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="tag"
                onSelect={() => handleBulkAction('tag-all')}
              >
                Apply Tags
                <span className="item-description">Add tags to all selected</span>
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownSeparator />

            <SafDropdownGroup label="Organization">
              <SafDropdownItem
                icon="folder"
                onSelect={() => handleBulkAction('move-all')}
              >
                Move to Folder
                <span className="item-description">Move all to same folder</span>
              </SafDropdownItem>

              <SafDropdownItem
                icon="archive"
                onSelect={() => handleBulkAction('archive-all')}
              >
                Archive All
                <span className="item-description">Archive selected documents</span>
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownSeparator />

            <SafDropdownItem
              icon="trash"
              destructive={true}
              onSelect={() => handleBulkAction('delete-all')}
            >
              Delete Selected
              <span className="item-description">Permanently delete all</span>
            </SafDropdownItem>
          </SafDropdown>
        </div>
      </div>

      {/* Context Menu Example */}
      <div className="context-menu-section">
        <h3>Document Context Menu</h3>
        <p>Right-click on the document below to see context menu:</p>
        
        <SafDropdown
          trigger={
            <div 
              className="document-item"
              onContextMenu={(e) => {
                e.preventDefault();
                // Context menu would be triggered here
              }}
            >
              <SafIcon name="file-text" />
              <span>Legal Brief - Case Analysis.docx</span>
              <SafChip label="Draft" variant="soft" color="warning" size="small" />
            </div>
          }
          variant="context"
          placement="bottom-start"
        >
          <SafDropdownItem icon="eye" shortcut="Enter">
            Open Document
          </SafDropdownItem>
          <SafDropdownItem icon="edit" shortcut="Ctrl+E">
            Edit
          </SafDropdownItem>
          <SafDropdownItem icon="download" shortcut="Ctrl+D">
            Download
          </SafDropdownItem>
          
          <SafDropdownSeparator />
          
          <SafDropdownItem icon="copy" shortcut="Ctrl+C">
            Copy
          </SafDropdownItem>
          <SafDropdownItem icon="cut" shortcut="Ctrl+X">
            Cut
          </SafDropdownItem>
          
          <SafDropdownSeparator />
          
          <SafDropdownItem icon="info">
            Properties
          </SafDropdownItem>
        </SafDropdown>
      </div>

      {/* Filter Dropdown */}
      <div className="filter-section">
        <h3>Document Filters</h3>
        <div className="filter-controls">
          <SafDropdown
            trigger={
              <SafButton variant="outline" icon="filter">
                Document Type
              </SafButton>
            }
            width="250px"
            searchable={true}
            searchPlaceholder="Search document types..."
          >
            <SafDropdownItem value="all" selected={true}>
              All Document Types
            </SafDropdownItem>
            
            <SafDropdownSeparator />
            
            <SafDropdownGroup label="Legal Documents">
              <SafDropdownItem value="contract" icon="file-text">
                Contracts (245)
              </SafDropdownItem>
              <SafDropdownItem value="brief" icon="file-text">
                Legal Briefs (89)
              </SafDropdownItem>
              <SafDropdownItem value="motion" icon="file-text">
                Motions (156)
              </SafDropdownItem>
              <SafDropdownItem value="pleading" icon="file-text">
                Pleadings (67)
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownGroup label="Administrative">
              <SafDropdownItem value="invoice" icon="file-text">
                Invoices (324)
              </SafDropdownItem>
              <SafDropdownItem value="correspondence" icon="mail">
                Correspondence (445)
              </SafDropdownItem>
              <SafDropdownItem value="notes" icon="edit">
                Notes (678)
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownGroup label="Evidence">
              <SafDropdownItem value="exhibits" icon="image">
                Exhibits (123)
              </SafDropdownItem>
              <SafDropdownItem value="depositions" icon="mic">
                Depositions (45)
              </SafDropdownItem>
              <SafDropdownItem value="discovery" icon="search">
                Discovery (234)
              </SafDropdownItem>
            </SafDropdownGroup>
          </SafDropdown>

          <SafDropdown
            trigger={
              <SafButton variant="outline" icon="calendar">
                Date Range
              </SafButton>
            }
            width="200px"
          >
            <SafDropdownItem value="today" icon="calendar">
              Today
            </SafDropdownItem>
            <SafDropdownItem value="week" icon="calendar">
              This Week
            </SafDropdownItem>
            <SafDropdownItem value="month" icon="calendar">
              This Month
            </SafDropdownItem>
            <SafDropdownItem value="quarter" icon="calendar">
              This Quarter
            </SafDropdownItem>
            <SafDropdownItem value="year" icon="calendar">
              This Year
            </SafDropdownItem>
            
            <SafDropdownSeparator />
            
            <SafDropdownItem value="custom" icon="settings">
              Custom Range...
            </SafDropdownItem>
          </SafDropdown>

          <SafDropdown
            trigger={
              <SafButton variant="outline" icon="user">
                Assigned To
              </SafButton>
            }
            width="250px"
            searchable={true}
            searchPlaceholder="Search team members..."
          >
            <SafDropdownItem value="all" selected={true}>
              All Team Members
            </SafDropdownItem>
            
            <SafDropdownSeparator />
            
            <SafDropdownGroup label="Partners">
              <SafDropdownItem value="sarah" icon="user">
                Sarah Johnson (Senior Partner)
              </SafDropdownItem>
              <SafDropdownItem value="michael" icon="user">
                Michael Chen (Partner)
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownGroup label="Associates">
              <SafDropdownItem value="emily" icon="user">
                Emily Rodriguez (Associate)
              </SafDropdownItem>
              <SafDropdownItem value="david" icon="user">
                David Park (Associate)
              </SafDropdownItem>
            </SafDropdownGroup>

            <SafDropdownGroup label="Paralegals">
              <SafDropdownItem value="lisa" icon="user">
                Lisa Wong (Paralegal)
              </SafDropdownItem>
              <SafDropdownItem value="james" icon="user">
                James Miller (Paralegal)
              </SafDropdownItem>
            </SafDropdownGroup>
          </SafDropdown>
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-document-actions-menu.component.ts
import { Component } from '@angular/core';

interface DocumentData {
  id: string;
  name: string;
  type: string;
  status: string;
  size: string;
  lastModified: Date;
  version: string;
  confidentiality: string;
  permissions: {
    canEdit: boolean;
    canDelete: boolean;
    canShare: boolean;
    canDownload: boolean;
    canComment: boolean;
    canVersion: boolean;
  };
}

@Component({
  selector: 'app-legal-document-actions-menu',
  template: `
    <div class="legal-document-actions-demo">
      <h2>Legal Document Management</h2>

      <!-- Document Card with Actions -->
      <div class="document-card">
        <div class="document-info">
          <div class="document-header">
            <saf-icon name="file-text" size="large"></saf-icon>
            <div class="document-details">
              <h3>{{ documentData.name }}</h3>
              <div class="document-meta">
                <saf-chip [label]="documentData.type" variant="soft" color="primary" size="small"></saf-chip>
                <saf-chip [label]="documentData.status" variant="soft" color="warning" size="small"></saf-chip>
                <saf-chip [label]="documentData.confidentiality" variant="soft" color="danger" size="small"></saf-chip>
                <span class="document-size">{{ documentData.size }}</span>
                <span class="document-version">v{{ documentData.version }}</span>
              </div>
            </div>
          </div>
        </div>

        <div class="document-actions">
          <!-- Primary Actions -->
          <saf-button
            variant="primary"
            size="small"
            icon="eye"
            (click)="viewDocument()">
            View
          </saf-button>

          <saf-button
            variant="secondary"
            size="small"
            icon="download"
            [loading]="actionLoading === 'download'"
            [disabled]="!documentData.permissions.canDownload"
            (click)="handleAction('download', documentData.id)">
            Download
          </saf-button>

          <!-- More Actions Dropdown -->
          <saf-dropdown
            placement="bottom-end"
            [closeOnSelect]="true"
            [searchable]="true"
            searchPlaceholder="Search actions...">
            
            <saf-button
              safDropdownTrigger
              variant="tertiary"
              size="small"
              icon="more-horizontal"
              aria-label="More document actions">
            </saf-button>

            <saf-dropdown-group label="Edit Actions">
              <saf-dropdown-item
                icon="edit"
                shortcut="Ctrl+E"
                [disabled]="!documentData.permissions.canEdit"
                [loading]="actionLoading === 'edit'"
                (select)="handleAction('edit', documentData.id)">
                Edit Document
                <span class="item-description">Open in document editor</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="message-square"
                shortcut="Ctrl+M"
                [disabled]="!documentData.permissions.canComment"
                [loading]="actionLoading === 'comment'"
                (select)="handleAction('comment', documentData.id)">
                Add Comment
                <span class="item-description">Add review comments</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="git-branch"
                [disabled]="!documentData.permissions.canVersion"
                [loading]="actionLoading === 'version'"
                (select)="handleAction('version', documentData.id)">
                Create Version
                <span class="item-description">Create new document version</span>
              </saf-dropdown-item>
            </saf-dropdown-group>

            <saf-dropdown-separator></saf-dropdown-separator>

            <saf-dropdown-group label="Share & Collaborate">
              <saf-dropdown-item
                icon="share"
                shortcut="Ctrl+S"
                [disabled]="!documentData.permissions.canShare"
                [loading]="actionLoading === 'share'"
                (select)="handleAction('share', documentData.id)">
                Share Document
                <span class="item-description">Share with team members</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="link"
                (select)="handleAction('copy-link', documentData.id)">
                Copy Link
                <span class="item-description">Copy shareable link</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="mail"
                (select)="handleAction('email', documentData.id)">
                Email Document
                <span class="item-description">Send via email</span>
              </saf-dropdown-item>
            </saf-dropdown-group>

            <saf-dropdown-separator></saf-dropdown-separator>

            <saf-dropdown-group label="Organization">
              <saf-dropdown-item
                icon="copy"
                [loading]="actionLoading === 'duplicate'"
                (select)="handleAction('duplicate', documentData.id)">
                Duplicate
                <span class="item-description">Create a copy</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="folder"
                [loading]="actionLoading === 'move'"
                (select)="handleAction('move', documentData.id)">
                Move to Folder
                <span class="item-description">Organize in folder structure</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="tag"
                (select)="handleAction('tags', documentData.id)">
                Manage Tags
                <span class="item-description">Add or edit document tags</span>
              </saf-dropdown-item>
            </saf-dropdown-group>

            <saf-dropdown-separator></saf-dropdown-separator>

            <saf-dropdown-group label="Document Actions">
              <saf-dropdown-item
                icon="archive"
                [loading]="actionLoading === 'archive'"
                (select)="handleAction('archive', documentData.id)">
                Archive Document
                <span class="item-description">Move to archive</span>
              </saf-dropdown-item>

              <saf-dropdown-item
                icon="trash"
                [destructive]="true"
                [disabled]="!documentData.permissions.canDelete"
                [loading]="actionLoading === 'delete'"
                (select)="handleAction('delete', documentData.id)">
                Delete Document
                <span class="item-description">Permanently delete</span>
              </saf-dropdown-item>
            </saf-dropdown-group>
          </saf-dropdown>
        </div>
      </div>

      <!-- Filter Dropdown -->
      <div class="filter-section">
        <h3>Document Filters</h3>
        <div class="filter-controls">
          <saf-dropdown
            width="250px"
            [searchable]="true"
            searchPlaceholder="Search document types...">
            
            <saf-button safDropdownTrigger variant="outline" icon="filter">
              Document Type
            </saf-button>

            <saf-dropdown-item value="all" [selected]="true">
              All Document Types
            </saf-dropdown-item>
            
            <saf-dropdown-separator></saf-dropdown-separator>
            
            <saf-dropdown-group label="Legal Documents">
              <saf-dropdown-item value="contract" icon="file-text">
                Contracts (245)
              </saf-dropdown-item>
              <saf-dropdown-item value="brief" icon="file-text">
                Legal Briefs (89)
              </saf-dropdown-item>
              <saf-dropdown-item value="motion" icon="file-text">
                Motions (156)
              </saf-dropdown-item>
              <saf-dropdown-item value="pleading" icon="file-text">
                Pleadings (67)
              </saf-dropdown-item>
            </saf-dropdown-group>

            <saf-dropdown-group label="Administrative">
              <saf-dropdown-item value="invoice" icon="file-text">
                Invoices (324)
              </saf-dropdown-item>
              <saf-dropdown-item value="correspondence" icon="mail">
                Correspondence (445)
              </saf-dropdown-item>
              <saf-dropdown-item value="notes" icon="edit">
                Notes (678)
              </saf-dropdown-item>
            </saf-dropdown-group>
          </saf-dropdown>

          <saf-dropdown width="200px">
            <saf-button safDropdownTrigger variant="outline" icon="calendar">
              Date Range
            </saf-button>

            <saf-dropdown-item value="today" icon="calendar">
              Today
            </saf-dropdown-item>
            <saf-dropdown-item value="week" icon="calendar">
              This Week
            </saf-dropdown-item>
            <saf-dropdown-item value="month" icon="calendar">
              This Month
            </saf-dropdown-item>
            <saf-dropdown-item value="quarter" icon="calendar">
              This Quarter
            </saf-dropdown-item>
            <saf-dropdown-item value="year" icon="calendar">
              This Year
            </saf-dropdown-item>
            
            <saf-dropdown-separator></saf-dropdown-separator>
            
            <saf-dropdown-item value="custom" icon="settings">
              Custom Range...
            </saf-dropdown-item>
          </saf-dropdown>
        </div>
      </div>
    </div>
  `
})
export class LegalDocumentActionsMenuComponent {
  actionLoading: string | null = null;

  documentData: DocumentData = {
    id: 'DOC-2024-001',
    name: 'Contract Amendment - Global Corp Services Agreement.pdf',
    type: 'Contract',
    status: 'Under Review',
    size: '2.4 MB',
    lastModified: new Date('2024-01-28'),
    version: '2.1',
    confidentiality: 'Confidential',
    permissions: {
      canEdit: true,
      canDelete: true,
      canShare: true,
      canDownload: true,
      canComment: true,
      canVersion: true
    }
  };

  async handleAction(action: string, docId: string) {
    this.actionLoading = action;
    try {
      await new Promise(resolve => setTimeout(resolve, 1500));
      console.log(`Action ${action} performed on document ${docId}`);
      
      switch (action) {
        case 'download':
          console.log('Downloading document...');
          break;
        case 'edit':
          console.log('Opening document for editing...');
          break;
        case 'share':
          console.log('Opening share dialog...');
          break;
        case 'version':
          console.log('Creating new version...');
          break;
        case 'comment':
          console.log('Opening comment panel...');
          break;
        case 'duplicate':
          console.log('Duplicating document...');
          break;
        case 'move':
          console.log('Opening move dialog...');
          break;
        case 'archive':
          console.log('Archiving document...');
          break;
        case 'delete':
          console.log('Deleting document...');
          break;
        default:
          console.log('Unknown action:', action);
      }
    } catch (error) {
      console.error('Error performing action:', error);
    } finally {
      this.actionLoading = null;
    }
  }

  viewDocument() {
    console.log('View document');
  }

  handleBulkAction(action: string) {
    console.log('Bulk action:', action);
  }
}
```

## Best Practices

1. **User Experience**
   - Use appropriate dropdown sizes for content
   - Provide clear item labels and descriptions
   - Group related actions logically
   - Include keyboard shortcuts for common actions

2. **Performance**
   - Implement virtual scrolling for large item lists
   - Lazy load dropdown content when needed
   - Optimize search functionality with debouncing
   - Use portal rendering for proper z-index stacking

3. **Accessibility**
   - Implement proper ARIA attributes
   - Support keyboard navigation (Arrow keys, Enter, Escape)
   - Provide screen reader announcements
   - Ensure sufficient color contrast

4. **Content Organization**
   - Use groups to organize related items
   - Provide search functionality for large lists
   - Include icons and descriptions for clarity
   - Show loading states for async actions

5. **Responsive Design**
   - Adapt positioning for mobile devices
   - Use appropriate touch targets
   - Handle small screen constraints
   - Provide swipe gestures where appropriate

## Accessibility Considerations

1. **Keyboard Navigation**
   - Arrow keys to navigate between items
   - Enter/Space to select items
   - Escape to close dropdown
   - Tab to move focus to next element

2. **Screen Reader Support**
   - Proper ARIA roles and properties
   - Announce dropdown state changes
   - Describe selected items
   - Provide context for grouped items

3. **Focus Management**
   - Return focus to trigger on close
   - Highlight focused items clearly
   - Support focus wrapping in item lists
   - Manage focus during search filtering

4. **Visual Accessibility**
   - High contrast mode support
   - Clear focus indicators
   - Sufficient color contrast
   - Scalable text and interface elements

## Related Components

- **SafButton**: Dropdown trigger elements
- **SafIcon**: Icons for dropdown items
- **SafInput**: Search input within dropdowns
- **SafChip**: Filter and tag selections

## Notes

- Dropdown supports multiple positioning strategies with auto-adjustment
- Built-in search functionality with customizable filtering
- Comprehensive keyboard navigation and accessibility support
- Portal rendering ensures proper z-index stacking
- Group functionality for organizing large item lists
- Support for custom content and complex item layouts
- Loading states and async action handling
- Mobile-responsive design with touch support
- Integration with form validation and selection systems
