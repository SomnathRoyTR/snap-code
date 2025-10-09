# SafToolbar Component

The `SafToolbar` component provides a flexible container for grouping related actions and controls in the Saffron Design System. Built on FAST Element, it supports keyboard navigation, multi-row layouts, density control, and accessibility features for organizing interactive elements.

## Table of Contents

- [Overview](#overview)
- [Component Properties](#component-properties)
- [Events](#events)
- [Methods](#methods)
- [Parts](#parts)
- [Slots](#slots)
- [CSS Custom Properties](#css-custom-properties)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Accessibility](#accessibility)
- [Best Practices](#best-practices)

## Overview

The SafToolbar component serves as a container for grouping related interactive elements such as buttons, form controls, and other actions. It provides sophisticated keyboard navigation, flexible layout options, and automatic focus management.

Key Features:
- **Keyboard Navigation**: Optional arrow key navigation between focusable elements
- **Multi-Row Layout**: Support for top and bottom row organization
- **Focus Management**: Automatic tabindex management for keyboard users
- **Density Control**: Configurable spacing and sizing
- **Accessibility**: Full ARIA support with proper toolbar semantics
- **Direction Support**: RTL (right-to-left) language support

## Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `ariaLabel` | `string` | `"Toolbar"` | ARIA label for the toolbar region |
| `density` | `ComponentDensity` | `inherit` | Controls spacing and sizing |
| `arrowNav` | `boolean` | `false` | Enables arrow key navigation between elements |

### Read-Only Properties

| Property | Type | Description |
|----------|------|-------------|
| `childItems` | `Element[]` | Array of child elements within the toolbar |
| `bottomStartNodes` | `Node[]` | Elements in the bottom-row-start slot |
| `bottomEndNodes` | `Node[]` | Elements in the bottom-row-end slot |
| `direction` | `'ltr' \| 'rtl'` | Text direction based on document/element direction |

### Internal Properties

| Property | Type | Description |
|----------|------|-------------|
| `focusableElements` | `HTMLElement[]` | Array of focusable elements for keyboard navigation |
| `activeIndex` | `number` | Index of currently focused element |

## Events

The SafToolbar component manages focus internally but doesn't emit custom events. It handles:

- **Click Events**: Automatic focus management when elements are clicked
- **Keyboard Events**: Navigation and activation of toolbar items
- **Focus Events**: Managing which element receives focus

## Methods

### Focus Management

```typescript
// Set focus to the toolbar
toolbar.focus(): void

// Handle click events (internal)
toolbar.clickHandler(event: MouseEvent): boolean | void

// Handle keyboard navigation (internal)  
toolbar.handleKeyDown(event: KeyboardEvent): boolean
```

### Internal Methods

```typescript
// Set which element should be focused
toolbar.setFocusedElement(activeIndex?: number): void

// Update list of focusable elements
toolbar.setFocusableElements(): void

// Set initial tabindex values
toolbar.setInitialTabIndexes(): void

// Check for bottom row content
toolbar.ifbottomSlots(): boolean
```

## Parts

| Part | Description |
|------|-------------|
| `top-row` | Container for the top row of toolbar items |
| `separator` | Divider between top and bottom rows |
| `bottom-row` | Container for the bottom row of toolbar items |

## Slots

| Slot | Description |
|------|-------------|
| `top-row-start` | Left-aligned items in the top row |
| `top-row-end` | Right-aligned items in the top row |
| `bottom-row-start` | Left-aligned items in the bottom row |
| `bottom-row-end` | Right-aligned items in the bottom row |

## CSS Custom Properties

The SafToolbar component uses the design system's spacing and layout tokens:

```css
saf-toolbar {
  /* Density affects spacing */
  --density: inherit;
  
  /* Row spacing */
  --toolbar-row-gap: var(--space-md);
  
  /* Item spacing */
  --toolbar-item-gap: var(--space-sm);
}
```

## React Integration

### Basic Usage

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';

function BasicToolbar() {
  return (
    <SafToolbar ariaLabel="Document actions">
      <div slot="top-row-start">
        <SafButton appearance="primary">
          <SafIcon slot="start" iconName="plus" size="16" />
          New Document
        </SafButton>
        <SafButton appearance="secondary">
          <SafIcon slot="start" iconName="folder-open" size="16" />
          Open
        </SafButton>
        <SafButton appearance="secondary">
          <SafIcon slot="start" iconName="floppy-disk" size="16" />
          Save
        </SafButton>
      </div>
      
      <div slot="top-row-end">
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="magnifying-glass" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="gear" size="16" />
        </SafButton>
      </div>
    </SafToolbar>
  );
}
```

### Keyboard Navigation Toolbar

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';

function KeyboardNavigationToolbar() {
  return (
    <SafToolbar 
      arrowNav={true}
      ariaLabel="Text formatting toolbar"
    >
      <div slot="top-row-start">
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="bold" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="italic" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="underline" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="align-left" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="align-center" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="align-right" size="16" />
        </SafButton>
      </div>
    </SafToolbar>
  );
}
```

### Multi-Row Toolbar

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafSelect from '@saffron/react/select';
import SafOption from '@saffron/react/option';
import SafSearchField from '@saffron/react/search-field';
import SafIcon from '@saffron/react/icon';

function MultiRowToolbar() {
  return (
    <SafToolbar ariaLabel="Content management toolbar">
      <div slot="top-row-start">
        <SafButton appearance="primary">
          <SafIcon slot="start" iconName="plus" size="16" />
          Create
        </SafButton>
        <SafButton appearance="secondary">
          <SafIcon slot="start" iconName="upload" size="16" />
          Import
        </SafButton>
        <SafButton appearance="secondary">
          <SafIcon slot="start" iconName="download" size="16" />
          Export
        </SafButton>
      </div>
      
      <div slot="top-row-end">
        <SafSearchField placeholder="Search content..." />
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="filter" size="16" />
        </SafButton>
      </div>
      
      <div slot="bottom-row-start">
        <SafSelect label="Status">
          <SafOption value="all">All Items</SafOption>
          <SafOption value="published">Published</SafOption>
          <SafOption value="draft">Draft</SafOption>
          <SafOption value="archived">Archived</SafOption>
        </SafSelect>
        
        <SafSelect label="Sort by">
          <SafOption value="name">Name</SafOption>
          <SafOption value="date">Date Modified</SafOption>
          <SafOption value="author">Author</SafOption>
        </SafSelect>
      </div>
      
      <div slot="bottom-row-end">
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="list" size="16" />
        </SafButton>
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="grid" size="16" />
        </SafButton>
      </div>
    </SafToolbar>
  );
}
```

### Form Toolbar

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafIcon from '@saffron/react/icon';
import { useState } from 'react';

function FormToolbar() {
  const [isFormDirty, setIsFormDirty] = useState(false);
  
  const handleSave = () => {
    // Save logic
    setIsFormDirty(false);
  };
  
  const handleReset = () => {
    // Reset logic
    setIsFormDirty(false);
  };
  
  return (
    <SafToolbar ariaLabel="Form actions">
      <div slot="top-row-start">
        <SafButton 
          appearance="primary" 
          onClick={handleSave}
          disabled={!isFormDirty}
        >
          <SafIcon slot="start" iconName="floppy-disk" size="16" />
          Save Changes
        </SafButton>
        
        <SafButton 
          appearance="secondary"
          onClick={handleReset}
          disabled={!isFormDirty}
        >
          <SafIcon slot="start" iconName="rotate-left" size="16" />
          Reset
        </SafButton>
      </div>
      
      <div slot="top-row-end">
        <SafButton appearance="tertiary">
          <SafIcon slot="start" iconName="eye" size="16" />
          Preview
        </SafButton>
        
        <SafButton appearance="tertiary">
          <SafIcon slot="start" iconName="circle-question" size="16" />
          Help
        </SafButton>
      </div>
    </SafToolbar>
  );
}
```

### Data Table Toolbar

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafSelect from '@saffron/react/select';
import SafOption from '@saffron/react/option';
import SafIcon from '@saffron/react/icon';

function DataTableToolbar() {
  const [selectedRows, setSelectedRows] = useState(0);
  
  return (
    <SafToolbar 
      arrowNav={true}
      ariaLabel="Data table controls"
    >
      <div slot="top-row-start">
        {selectedRows > 0 ? (
          <>
            <span>{selectedRows} selected</span>
            <SafButton appearance="secondary">
              <SafIcon slot="start" iconName="trash" size="16" />
              Delete Selected
            </SafButton>
            <SafButton appearance="secondary">
              <SafIcon slot="start" iconName="download" size="16" />
              Export Selected
            </SafButton>
          </>
        ) : (
          <>
            <SafButton appearance="primary">
              <SafIcon slot="start" iconName="plus" size="16" />
              Add Row
            </SafButton>
            <SafButton appearance="secondary">
              <SafIcon slot="start" iconName="upload" size="16" />
              Import Data
            </SafButton>
          </>
        )}
      </div>
      
      <div slot="top-row-end">
        <SafSelect label="Rows per page">
          <SafOption value="10">10</SafOption>
          <SafOption value="25">25</SafOption>
          <SafOption value="50">50</SafOption>
          <SafOption value="100">100</SafOption>
        </SafSelect>
        
        <SafButton appearance="tertiary" iconOnly>
          <SafIcon iconName="gear" size="16" />
        </SafButton>
      </div>
    </SafToolbar>
  );
}
```

## Angular Integration

### Basic Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-toolbar',
  template: `
    <saf-toolbar aria-label="Document actions">
      <div slot="top-row-start">
        <saf-button appearance="primary">
          <saf-icon slot="start" icon-name="plus" size="16"></saf-icon>
          New Document
        </saf-button>
        <saf-button appearance="secondary">
          <saf-icon slot="start" icon-name="folder-open" size="16"></saf-icon>
          Open
        </saf-button>
        <saf-button appearance="secondary">
          <saf-icon slot="start" icon-name="floppy-disk" size="16"></saf-icon>
          Save
        </saf-button>
      </div>
      
      <div slot="top-row-end">
        <saf-button appearance="tertiary" icon-only>
          <saf-icon icon-name="magnifying-glass" size="16"></saf-icon>
        </saf-button>
        <saf-button appearance="tertiary" icon-only>
          <saf-icon icon-name="gear" size="16"></saf-icon>
        </saf-button>
      </div>
    </saf-toolbar>
  `
})
export class BasicToolbarComponent {}
```

### Toolbar Service

```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject, Observable } from 'rxjs';

export interface ToolbarAction {
  id: string;
  label: string;
  icon: string;
  appearance: 'primary' | 'secondary' | 'tertiary';
  disabled?: boolean;
  slot: 'top-row-start' | 'top-row-end' | 'bottom-row-start' | 'bottom-row-end';
}

@Injectable({
  providedIn: 'root'
})
export class ToolbarService {
  private actionsSubject = new BehaviorSubject<ToolbarAction[]>([]);
  public actions$: Observable<ToolbarAction[]> = this.actionsSubject.asObservable();
  
  private selectedItemsSubject = new BehaviorSubject<number>(0);
  public selectedItems$: Observable<number> = this.selectedItemsSubject.asObservable();
  
  get actions(): ToolbarAction[] {
    return this.actionsSubject.value;
  }
  
  setActions(actions: ToolbarAction[]): void {
    this.actionsSubject.next(actions);
  }
  
  addAction(action: ToolbarAction): void {
    const currentActions = [...this.actions];
    currentActions.push(action);
    this.actionsSubject.next(currentActions);
  }
  
  updateAction(id: string, updates: Partial<ToolbarAction>): void {
    const currentActions = this.actions.map(action => 
      action.id === id ? { ...action, ...updates } : action
    );
    this.actionsSubject.next(currentActions);
  }
  
  removeAction(id: string): void {
    const currentActions = this.actions.filter(action => action.id !== id);
    this.actionsSubject.next(currentActions);
  }
  
  setSelectedItems(count: number): void {
    this.selectedItemsSubject.next(count);
  }
  
  executeAction(actionId: string): void {
    // Emit action execution event or handle business logic
    console.log(`Executing action: ${actionId}`);
  }
}
```

### Dynamic Toolbar Component

```typescript
import { Component, OnInit, Input } from '@angular/core';
import { ToolbarService, ToolbarAction } from './toolbar.service';

@Component({
  selector: 'app-dynamic-toolbar',
  template: `
    <saf-toolbar 
      [arrow-nav]="enableKeyboardNav"
      [aria-label]="toolbarLabel">
      
      <div slot="top-row-start">
        <ng-container *ngFor="let action of getActionsBySlot('top-row-start')">
          <saf-button 
            [appearance]="action.appearance"
            [disabled]="action.disabled"
            (click)="executeAction(action.id)">
            <saf-icon 
              slot="start" 
              [icon-name]="action.icon" 
              size="16">
            </saf-icon>
            {{ action.label }}
          </saf-button>
        </ng-container>
      </div>
      
      <div slot="top-row-end">
        <ng-container *ngFor="let action of getActionsBySlot('top-row-end')">
          <saf-button 
            [appearance]="action.appearance"
            [disabled]="action.disabled"
            [icon-only]="!action.label"
            (click)="executeAction(action.id)">
            <saf-icon [icon-name]="action.icon" size="16"></saf-icon>
            <span *ngIf="action.label">{{ action.label }}</span>
          </saf-button>
        </ng-container>
      </div>
      
      <div slot="bottom-row-start" *ngIf="hasBottomRowStartActions()">
        <ng-container *ngFor="let action of getActionsBySlot('bottom-row-start')">
          <saf-button 
            [appearance]="action.appearance"
            [disabled]="action.disabled"
            (click)="executeAction(action.id)">
            <saf-icon 
              slot="start" 
              [icon-name]="action.icon" 
              size="16">
            </saf-icon>
            {{ action.label }}
          </saf-button>
        </ng-container>
      </div>
      
      <div slot="bottom-row-end" *ngIf="hasBottomRowEndActions()">
        <ng-container *ngFor="let action of getActionsBySlot('bottom-row-end')">
          <saf-button 
            [appearance]="action.appearance"
            [disabled]="action.disabled"
            [icon-only]="!action.label"
            (click)="executeAction(action.id)">
            <saf-icon [icon-name]="action.icon" size="16"></saf-icon>
            <span *ngIf="action.label">{{ action.label }}</span>
          </saf-button>
        </ng-container>
      </div>
    </saf-toolbar>
  `
})
export class DynamicToolbarComponent implements OnInit {
  @Input() toolbarLabel = 'Actions toolbar';
  @Input() enableKeyboardNav = false;
  
  actions: ToolbarAction[] = [];
  selectedItems = 0;
  
  constructor(private toolbarService: ToolbarService) {}
  
  ngOnInit() {
    this.toolbarService.actions$.subscribe(actions => {
      this.actions = actions;
    });
    
    this.toolbarService.selectedItems$.subscribe(count => {
      this.selectedItems = count;
      this.updateActionsBasedOnSelection();
    });
  }
  
  getActionsBySlot(slot: string): ToolbarAction[] {
    return this.actions.filter(action => action.slot === slot);
  }
  
  hasBottomRowStartActions(): boolean {
    return this.getActionsBySlot('bottom-row-start').length > 0;
  }
  
  hasBottomRowEndActions(): boolean {
    return this.getActionsBySlot('bottom-row-end').length > 0;
  }
  
  executeAction(actionId: string): void {
    this.toolbarService.executeAction(actionId);
  }
  
  private updateActionsBasedOnSelection(): void {
    // Update actions based on selection state
    if (this.selectedItems > 0) {
      this.toolbarService.updateAction('delete', { disabled: false });
      this.toolbarService.updateAction('export', { disabled: false });
    } else {
      this.toolbarService.updateAction('delete', { disabled: true });
      this.toolbarService.updateAction('export', { disabled: true });
    }
  }
}
```

### Data Management Toolbar

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

export interface DataAction {
  type: 'create' | 'edit' | 'delete' | 'export' | 'import' | 'filter' | 'search';
  data?: any;
}

@Component({
  selector: 'app-data-toolbar',
  template: `
    <saf-toolbar [arrow-nav]="true" [aria-label]="ariaLabel">
      <div slot="top-row-start">
        <saf-button 
          appearance="primary"
          (click)="emitAction('create')"
          [disabled]="!canCreate">
          <saf-icon slot="start" icon-name="plus" size="16"></saf-icon>
          {{ createLabel }}
        </saf-button>
        
        <saf-button 
          appearance="secondary"
          (click)="emitAction('import')"
          [disabled]="!canImport">
          <saf-icon slot="start" icon-name="upload" size="16"></saf-icon>
          Import
        </saf-button>
        
        <saf-button 
          *ngIf="selectedCount > 0"
          appearance="secondary"
          (click)="emitAction('delete')"
          [disabled]="!canDelete">
          <saf-icon slot="start" icon-name="trash" size="16"></saf-icon>
          Delete ({{ selectedCount }})
        </saf-button>
        
        <saf-button 
          *ngIf="selectedCount > 0"
          appearance="secondary"
          (click)="emitAction('export')"
          [disabled]="!canExport">
          <saf-icon slot="start" icon-name="download" size="16"></saf-icon>
          Export Selected
        </saf-button>
      </div>
      
      <div slot="top-row-end">
        <saf-search-field 
          [value]="searchValue"
          [placeholder]="searchPlaceholder"
          (input)="onSearchChange($event)">
        </saf-search-field>
        
        <saf-button 
          appearance="tertiary" 
          icon-only
          (click)="emitAction('filter')"
          [aria-label]="'Open filters'">
          <saf-icon icon-name="filter" size="16"></saf-icon>
        </saf-button>
      </div>
      
      <div slot="bottom-row-start" *ngIf="showFilters">
        <saf-select 
          [label]="'Status'"
          [value]="statusFilter"
          (change)="onStatusFilterChange($event)">
          <saf-option value="">All</saf-option>
          <saf-option 
            *ngFor="let status of statusOptions"
            [value]="status.value">
            {{ status.label }}
          </saf-option>
        </saf-select>
        
        <saf-select 
          [label]="'Sort by'"
          [value]="sortBy"
          (change)="onSortChange($event)">
          <saf-option 
            *ngFor="let sort of sortOptions"
            [value]="sort.value">
            {{ sort.label }}
          </saf-option>
        </saf-select>
      </div>
      
      <div slot="bottom-row-end" *ngIf="showViewOptions">
        <saf-button 
          [appearance]="viewMode === 'list' ? 'primary' : 'tertiary'"
          icon-only
          (click)="setViewMode('list')"
          [aria-label]="'List view'">
          <saf-icon icon-name="list" size="16"></saf-icon>
        </saf-button>
        
        <saf-button 
          [appearance]="viewMode === 'grid' ? 'primary' : 'tertiary'"
          icon-only
          (click)="setViewMode('grid')"
          [aria-label]="'Grid view'">
          <saf-icon icon-name="grid" size="16"></saf-icon>
        </saf-button>
      </div>
    </saf-toolbar>
  `
})
export class DataToolbarComponent {
  @Input() ariaLabel = 'Data management toolbar';
  @Input() createLabel = 'Create';
  @Input() searchPlaceholder = 'Search...';
  @Input() selectedCount = 0;
  @Input() canCreate = true;
  @Input() canEdit = true;
  @Input() canDelete = true;
  @Input() canImport = true;
  @Input() canExport = true;
  @Input() showFilters = false;
  @Input() showViewOptions = true;
  @Input() statusOptions: {value: string, label: string}[] = [];
  @Input() sortOptions: {value: string, label: string}[] = [];
  
  @Output() action = new EventEmitter<DataAction>();
  @Output() searchChange = new EventEmitter<string>();
  @Output() statusFilterChange = new EventEmitter<string>();
  @Output() sortChange = new EventEmitter<string>();
  @Output() viewModeChange = new EventEmitter<'list' | 'grid'>();
  
  searchValue = '';
  statusFilter = '';
  sortBy = '';
  viewMode: 'list' | 'grid' = 'list';
  
  emitAction(type: DataAction['type'], data?: any): void {
    this.action.emit({ type, data });
  }
  
  onSearchChange(event: Event): void {
    const target = event.target as HTMLInputElement;
    this.searchValue = target.value;
    this.searchChange.emit(this.searchValue);
  }
  
  onStatusFilterChange(event: CustomEvent): void {
    this.statusFilter = event.detail.value;
    this.statusFilterChange.emit(this.statusFilter);
  }
  
  onSortChange(event: CustomEvent): void {
    this.sortBy = event.detail.value;
    this.sortChange.emit(this.sortBy);
  }
  
  setViewMode(mode: 'list' | 'grid'): void {
    this.viewMode = mode;
    this.viewModeChange.emit(mode);
  }
}
```

## Usage Examples

### Basic Single-Row Toolbar

```html
<saf-toolbar aria-label="Basic actions">
  <div slot="top-row-start">
    <saf-button appearance="primary">Save</saf-button>
    <saf-button appearance="secondary">Cancel</saf-button>
  </div>
  
  <div slot="top-row-end">
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="gear" size="16"></saf-icon>
    </saf-button>
  </div>
</saf-toolbar>
```

### Keyboard Navigation Toolbar

```html
<saf-toolbar arrow-nav="true" aria-label="Formatting toolbar">
  <div slot="top-row-start">
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="bold" size="16"></saf-icon>
    </saf-button>
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="italic" size="16"></saf-icon>
    </saf-button>
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="underline" size="16"></saf-icon>
    </saf-button>
  </div>
</saf-toolbar>
```

### Multi-Row Toolbar

```html
<saf-toolbar aria-label="Content management">
  <div slot="top-row-start">
    <saf-button appearance="primary">
      <saf-icon slot="start" icon-name="plus" size="16"></saf-icon>
      Create
    </saf-button>
    <saf-button appearance="secondary">
      <saf-icon slot="start" icon-name="upload" size="16"></saf-icon>
      Import
    </saf-button>
  </div>
  
  <div slot="top-row-end">
    <saf-search-field placeholder="Search content..."></saf-search-field>
  </div>
  
  <div slot="bottom-row-start">
    <saf-select label="Status">
      <saf-option value="all">All</saf-option>
      <saf-option value="published">Published</saf-option>
      <saf-option value="draft">Draft</saf-option>
    </saf-select>
  </div>
  
  <div slot="bottom-row-end">
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="list" size="16"></saf-icon>
    </saf-button>
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="grid" size="16"></saf-icon>
    </saf-button>
  </div>
</saf-toolbar>
```

### Compact Density Toolbar

```html
<saf-toolbar density="compact" aria-label="Compact toolbar">
  <div slot="top-row-start">
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="floppy-disk" size="16"></saf-icon>
    </saf-button>
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="folder-open" size="16"></saf-icon>
    </saf-button>
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="print" size="16"></saf-icon>
    </saf-button>
  </div>
</saf-toolbar>
```

### Form Controls Toolbar

```html
<saf-toolbar arrow-nav="true" aria-label="Form controls">
  <div slot="top-row-start">
    <saf-select label="Font">
      <saf-option value="arial">Arial</saf-option>
      <saf-option value="helvetica">Helvetica</saf-option>
      <saf-option value="times">Times New Roman</saf-option>
    </saf-select>
    
    <saf-number-field label="Size" min="8" max="72" value="12"></saf-number-field>
  </div>
  
  <div slot="top-row-end">
    <saf-button appearance="tertiary" icon-only>
      <saf-icon icon-name="palette" size="16"></saf-icon>
    </saf-button>
  </div>
</saf-toolbar>
```

### JavaScript Event Handling

```javascript
const toolbar = document.querySelector('saf-toolbar');

// Handle focus events
toolbar.addEventListener('focusin', (event) => {
  console.log('Focus entered toolbar:', event.target);
});

toolbar.addEventListener('focusout', (event) => {
  console.log('Focus left toolbar:', event.target);
});

// Add custom keyboard handling
toolbar.addEventListener('keydown', (event) => {
  if (event.key === 'Escape') {
    // Custom escape handling
    event.target.blur();
  }
});
```

## Accessibility

The SafToolbar component provides comprehensive accessibility support:

### ARIA Implementation
- **role="toolbar"**: Applied when `arrowNav` is enabled for keyboard navigation
- **role="group"**: Applied when keyboard navigation is disabled
- **aria-label**: Configurable label for the toolbar region
- **tabindex**: Automatic management for keyboard navigation focus

### Keyboard Support
- **Tab**: Navigate into and out of the toolbar
- **Arrow Keys**: Navigate between focusable elements (when `arrowNav` enabled)
- **Home/End**: Jump to first/last focusable element (when `arrowNav` enabled)
- **Enter/Space**: Activate focused element

### Focus Management
- **Roving Tabindex**: Only one element focusable at a time during arrow navigation
- **Focus Restoration**: Focus maintained during dynamic content changes
- **Visible Focus**: Clear focus indicators on all interactive elements

### Screen Reader Support
- **Clear Labels**: Descriptive labels for all interactive elements
- **Context Information**: Toolbar purpose communicated through aria-label
- **State Announcements**: Element states announced appropriately

### Direction Support
- **RTL Languages**: Automatic right-to-left layout support
- **Arrow Key Mapping**: Arrows behave correctly in RTL contexts

## Best Practices

### Organization
- Group related actions logically within toolbar slots
- Use top-row for primary actions, bottom-row for secondary/filter controls
- Place most important actions in top-row-start for left-to-right reading order

### Keyboard Navigation
- Enable `arrowNav` for toolbars with many focusable elements
- Use consistent keyboard interaction patterns across similar toolbars
- Provide clear visual focus indicators

### Density and Spacing
- Use appropriate density for the context (compact for data-heavy interfaces)
- Ensure adequate touch targets for mobile interfaces
- Maintain consistent spacing between related elements

### Content Guidelines
- Use clear, concise labels for buttons and controls
- Provide appropriate icons that reinforce button purposes
- Use tooltips for icon-only buttons when context isn't obvious

### Responsive Design
- Consider how toolbar content adapts at different screen sizes
- Use icon-only buttons to save space when necessary
- Consider collapsing less important actions into overflow menus on small screens

### Performance
- Avoid complex DOM manipulation during keyboard navigation
- Use efficient event handling for toolbar interactions
- Consider virtualizing toolbar content for very large action sets

The SafToolbar component provides a flexible, accessible foundation for organizing interactive elements while maintaining excellent usability across all devices and interaction modes.
