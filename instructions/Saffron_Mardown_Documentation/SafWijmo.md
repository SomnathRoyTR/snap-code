# SafWijmo Integration

The `SafWijmo` integration provides Thomson Reuters-styled implementation of Wijmo FlexGrid in the Saffron Design System. This integration includes Saffron styling, accessibility enhancements, and best practices for using the third-party Wijmo FlexGrid component with Saffron components.

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Styling](#styling)
- [Components](#components)
- [Accessibility](#accessibility)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Overview

SafWijmo is not a standalone component but a comprehensive integration that styles and configures the third-party Wijmo FlexGrid to work seamlessly with the Saffron Design System. It provides enhanced accessibility, Saffron visual styling, and integration with other Saffron components.

Key Features:
- **Saffron Styling**: Complete visual integration with Saffron design tokens
- **Accessibility Enhanced**: Improved keyboard navigation and screen reader support
- **Component Integration**: Works with SafToolbar, SafPagination, and other Saffron components
- **Multiple Styles**: Support for both spreadsheet and list styles
- **Responsive Design**: Mobile-friendly responsive behavior
- **Thomson Reuters Branding**: Consistent with TR design standards

### What's Included

The SafWijmo integration includes:
- **Saffron Core Styles**: CSS styling for Wijmo FlexGrid components
- **Accessibility Enhancements**: ARIA attributes and keyboard navigation improvements
- **Manage Columns Component**: React/Angular component for column management
- **Kitchen Sink Demo**: Comprehensive example implementation
- **Integration Utilities**: Helper functions for Saffron-Wijmo integration

## Installation

### Prerequisites

1. **Wijmo License**: Request Thomson Reuters Wijmo enterprise key
2. **Saffron Packages**: Install core Saffron packages

### Step 1: Request Wijmo Access Key

Contact Thomson Reuters IT to request the enterprise Wijmo access key. The TR distribution key works for all domains without whitelisting.

### Step 2: Install Saffron Packages

```bash
# Using npm
npm install @saffron/core-components @saffron/core-styles

# Using yarn
yarn add @saffron/core-components @saffron/core-styles
```

### Step 3: Install Wijmo

#### For Angular

```bash
# Using npm
npm install @grapecity/wijmo.angular2.all

# Using yarn
yarn add @grapecity/wijmo.angular2.all
```

#### For React

```bash
# Using npm
npm install @grapecity/wijmo.react.all

# Using yarn
yarn add @grapecity/wijmo.react.all
```

### Step 4: Import Saffron Wijmo Styles

```css
/* Import Saffron Wijmo styles */
@import '@saffron/core-styles/dist/wijmo.css';
```

## Styling

The SafWijmo integration provides two main visual styles:

### Spreadsheet Style
- Similar to Excel appearance
- All cells have borders
- Best for data manipulation and calculation

### List Style
- Lightweight presentation
- Borders only between rows
- Best for data display and selection

### Design Tokens

The styling uses Saffron design tokens for:
- **Colors**: Background, borders, text, and state colors
- **Typography**: Font families, sizes, and weights
- **Spacing**: Padding, margins, and gaps
- **Interactive States**: Hover, focus, selected, and disabled states

## Components

### Manage Columns Component

A React/Angular component that provides column management functionality:

```typescript
interface ManageColumnsProps {
  columns: ColumnConfig[];
  onColumnsChange: (columns: ColumnConfig[]) => void;
  visible?: boolean;
  onVisibilityChange?: (visible: boolean) => void;
}
```

### Kitchen Sink Demo

A comprehensive example that includes:
- Full FlexGrid implementation
- Column management
- Sorting and filtering
- Pagination integration
- Toolbar integration
- Accessibility features

## Accessibility

The SafWijmo integration includes extensive accessibility enhancements:

### ARIA Implementation
- **Grid Role**: Proper grid and gridcell roles
- **Headers**: Associated column and row headers
- **Labels**: Descriptive labels for grid regions
- **State Communication**: Selection and edit states announced

### Keyboard Navigation
- **Arrow Keys**: Navigate between cells
- **Tab Navigation**: Move to next focusable element
- **F2**: Enter edit mode
- **Enter**: Confirm edit and move down
- **Escape**: Cancel edit mode
- **Space**: Toggle checkboxes or select rows
- **Home/End**: Navigate to first/last column
- **Ctrl+Home/End**: Navigate to first/last cell

### Required Accessibility Features

#### Grid Labeling
```html
<!-- Option 1: Using aria-labelledby -->
<h2 id="dataGridHeading">Financial Data</h2>
<wj-flex-grid aria-labelledby="dataGridHeading">
  <!-- Grid content -->
</wj-flex-grid>

<!-- Option 2: Using aria-label -->
<wj-flex-grid aria-label="Financial Data">
  <!-- Grid content -->
</wj-flex-grid>
```

#### Header Focusability
```html
<wj-flex-grid headersFocusability="All">
  <!-- Grid content -->
</wj-flex-grid>
```

#### Accessible Links
```html
<div class="wj-cell" role="gridcell">
  <a href="/details/123" aria-label="Link: View details for Item 123">
    View Details
  </a>
</div>
```

#### Accessible Checkboxes
```html
<label>
  <input type="checkbox" class="wj-cell-check">
  <span>Select Item 123</span>
  <saf-sr-only>Checkbox, Unchecked</saf-sr-only>
</label>
```

## React Integration

### Basic Implementation

```tsx
import { FlexGrid, FlexGridColumn } from '@grapecity/wijmo.react.grid';
import { CollectionView } from '@grapecity/wijmo';
import '@saffron/core-styles/dist/wijmo.css';

interface DataItem {
  id: number;
  name: string;
  value: number;
  status: string;
}

function DataGrid() {
  const [data] = useState<DataItem[]>([
    { id: 1, name: 'Item 1', value: 100, status: 'Active' },
    { id: 2, name: 'Item 2', value: 200, status: 'Inactive' },
    // More data...
  ]);

  const collectionView = new CollectionView(data);

  return (
    <FlexGrid
      itemsSource={collectionView}
      aria-label="Data grid"
      headersFocusability="All"
      allowResizing="Both"
      allowSorting={true}
    >
      <FlexGridColumn binding="id" header="ID" width={80} />
      <FlexGridColumn binding="name" header="Name" width={200} />
      <FlexGridColumn binding="value" header="Value" width={120} />
      <FlexGridColumn binding="status" header="Status" width={100} />
    </FlexGrid>
  );
}
```

### With Toolbar Integration

```tsx
import SafToolbar from '@saffron/react/toolbar';
import SafButton from '@saffron/react/button';
import SafSearchField from '@saffron/react/search-field';
import { FlexGrid, FlexGridColumn } from '@grapecity/wijmo.react.grid';

function GridWithToolbar() {
  const [searchText, setSearchText] = useState('');
  const [collectionView, setCollectionView] = useState<CollectionView>();

  const handleSearch = (text: string) => {
    setSearchText(text);
    if (collectionView) {
      collectionView.filter = (item) => 
        item.name.toLowerCase().includes(text.toLowerCase());
    }
  };

  const handleExport = () => {
    // Export functionality
  };

  return (
    <div>
      <SafToolbar ariaLabel="Grid actions">
        <div slot="top-row-start">
          <SafButton appearance="primary" onClick={handleExport}>
            Export Data
          </SafButton>
        </div>
        <div slot="top-row-end">
          <SafSearchField 
            value={searchText}
            onInput={(e) => handleSearch(e.target.value)}
            placeholder="Search items..."
          />
        </div>
      </SafToolbar>

      <FlexGrid
        itemsSource={collectionView}
        aria-label="Filtered data grid"
        headersFocusability="All"
      >
        <FlexGridColumn binding="name" header="Name" />
        <FlexGridColumn binding="value" header="Value" />
        <FlexGridColumn binding="status" header="Status" />
      </FlexGrid>
    </div>
  );
}
```

### With Manage Columns

```tsx
import { ManageColumns } from '@saffron/wijmo/manage-columns';

function GridWithColumnManagement() {
  const [columns, setColumns] = useState([
    { key: 'name', header: 'Name', visible: true, width: 200 },
    { key: 'value', header: 'Value', visible: true, width: 120 },
    { key: 'status', header: 'Status', visible: false, width: 100 },
  ]);

  const [manageColumnsVisible, setManageColumnsVisible] = useState(false);

  return (
    <div>
      <SafToolbar ariaLabel="Grid with column management">
        <div slot="top-row-end">
          <SafButton 
            appearance="tertiary"
            onClick={() => setManageColumnsVisible(true)}
          >
            Manage Columns
          </SafButton>
        </div>
      </SafToolbar>

      <FlexGrid itemsSource={data} aria-label="Customizable data grid">
        {columns
          .filter(col => col.visible)
          .map(col => (
            <FlexGridColumn 
              key={col.key}
              binding={col.key} 
              header={col.header}
              width={col.width}
            />
          ))
        }
      </FlexGrid>

      <ManageColumns
        columns={columns}
        onColumnsChange={setColumns}
        visible={manageColumnsVisible}
        onVisibilityChange={setManageColumnsVisible}
      />
    </div>
  );
}
```

## Angular Integration

### Basic Implementation

```typescript
import { Component } from '@angular/core';
import { CollectionView } from '@grapecity/wijmo';

@Component({
  selector: 'app-data-grid',
  template: `
    <wj-flex-grid 
      [itemsSource]="collectionView"
      [aria-label]="'Data grid'"
      [headersFocusability]="'All'"
      [allowResizing]="'Both'"
      [allowSorting]="true">
      
      <wj-flex-grid-column 
        [binding]="'id'" 
        [header]="'ID'" 
        [width]="80">
      </wj-flex-grid-column>
      
      <wj-flex-grid-column 
        [binding]="'name'" 
        [header]="'Name'" 
        [width]="200">
      </wj-flex-grid-column>
      
      <wj-flex-grid-column 
        [binding]="'value'" 
        [header]="'Value'" 
        [width]="120">
      </wj-flex-grid-column>
      
      <wj-flex-grid-column 
        [binding]="'status'" 
        [header]="'Status'" 
        [width]="100">
      </wj-flex-grid-column>
    </wj-flex-grid>
  `
})
export class DataGridComponent {
  data = [
    { id: 1, name: 'Item 1', value: 100, status: 'Active' },
    { id: 2, name: 'Item 2', value: 200, status: 'Inactive' },
    // More data...
  ];

  collectionView = new CollectionView(this.data);
}
```

### With Service Integration

```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject, Observable } from 'rxjs';
import { CollectionView } from '@grapecity/wijmo';

@Injectable({
  providedIn: 'root'
})
export class GridDataService {
  private dataSubject = new BehaviorSubject<any[]>([]);
  public data$: Observable<any[]> = this.dataSubject.asObservable();
  
  private collectionViewSubject = new BehaviorSubject<CollectionView | null>(null);
  public collectionView$: Observable<CollectionView | null> = this.collectionViewSubject.asObservable();

  constructor() {
    this.data$.subscribe(data => {
      const cv = new CollectionView(data);
      this.collectionViewSubject.next(cv);
    });
  }

  loadData(data: any[]): void {
    this.dataSubject.next(data);
  }

  filterData(filterFn: (item: any) => boolean): void {
    const cv = this.collectionViewSubject.value;
    if (cv) {
      cv.filter = filterFn;
    }
  }

  sortData(property: string, ascending: boolean = true): void {
    const cv = this.collectionViewSubject.value;
    if (cv) {
      cv.sortDescriptions.clear();
      cv.sortDescriptions.push(new SortDescription(property, ascending));
    }
  }
}
```

### Component with Service

```typescript
@Component({
  selector: 'app-advanced-grid',
  template: `
    <saf-toolbar aria-label="Advanced grid controls">
      <div slot="top-row-start">
        <saf-button 
          appearance="primary"
          (click)="exportData()">
          Export
        </saf-button>
        <saf-button 
          appearance="secondary"
          (click)="refreshData()">
          Refresh
        </saf-button>
      </div>
      
      <div slot="top-row-end">
        <saf-search-field 
          [value]="searchText"
          placeholder="Search..."
          (input)="onSearch($event)">
        </saf-search-field>
      </div>
    </saf-toolbar>

    <wj-flex-grid 
      *ngIf="collectionView"
      [itemsSource]="collectionView"
      [aria-label]="'Advanced data grid'"
      [headersFocusability]="'All'"
      (selectionChanged)="onSelectionChanged($event)">
      
      <wj-flex-grid-column 
        *ngFor="let column of visibleColumns"
        [binding]="column.binding"
        [header]="column.header"
        [width]="column.width"
        [format]="column.format">
      </wj-flex-grid-column>
    </wj-flex-grid>

    <saf-pagination
      *ngIf="collectionView"
      [totalItemCount]="collectionView.totalItemCount"
      [currentPageIndex]="currentPage"
      [itemsPerPage]="pageSize"
      (change)="onPageChange($event)"
      (items-per-page-change)="onPageSizeChange($event)">
    </saf-pagination>
  `
})
export class AdvancedGridComponent implements OnInit {
  collectionView: CollectionView | null = null;
  searchText = '';
  currentPage = 1;
  pageSize = 25;
  
  visibleColumns = [
    { binding: 'id', header: 'ID', width: 80 },
    { binding: 'name', header: 'Name', width: 200 },
    { binding: 'value', header: 'Value', width: 120, format: 'c' },
    { binding: 'date', header: 'Date', width: 150, format: 'd' },
  ];

  constructor(private gridDataService: GridDataService) {}

  ngOnInit() {
    this.gridDataService.collectionView$.subscribe(cv => {
      this.collectionView = cv;
      if (cv) {
        cv.pageSize = this.pageSize;
      }
    });

    // Load initial data
    this.refreshData();
  }

  onSearch(event: Event) {
    const target = event.target as HTMLInputElement;
    this.searchText = target.value;
    
    this.gridDataService.filterData(item => 
      item.name.toLowerCase().includes(this.searchText.toLowerCase())
    );
  }

  onSelectionChanged(event: any) {
    const selectedItem = event.grid.selectedItem;
    console.log('Selected item:', selectedItem);
  }

  onPageChange(event: CustomEvent) {
    this.currentPage = event.detail;
    if (this.collectionView) {
      this.collectionView.moveToPage(this.currentPage - 1);
    }
  }

  onPageSizeChange(event: CustomEvent) {
    this.pageSize = event.detail;
    if (this.collectionView) {
      this.collectionView.pageSize = this.pageSize;
    }
  }

  exportData() {
    // Export implementation
  }

  refreshData() {
    // Load data from service
    const data = [
      // Your data here
    ];
    this.gridDataService.loadData(data);
  }
}
```

## Usage Examples

### Basic Spreadsheet Style Grid

```html
<wj-flex-grid
  aria-label="Financial data spreadsheet"
  headers-focusability="All"
  class="spreadsheet-style">
  
  <wj-flex-grid-column binding="account" header="Account"></wj-flex-grid-column>
  <wj-flex-grid-column binding="amount" header="Amount" format="c"></wj-flex-grid-column>
  <wj-flex-grid-column binding="date" header="Date" format="d"></wj-flex-grid-column>
</wj-flex-grid>
```

### List Style Grid

```html
<wj-flex-grid
  aria-label="Document list"
  headers-focusability="All"
  class="list-style">
  
  <wj-flex-grid-column binding="title" header="Document Title"></wj-flex-grid-column>
  <wj-flex-grid-column binding="author" header="Author"></wj-flex-grid-column>
  <wj-flex-grid-column binding="modified" header="Last Modified"></wj-flex-grid-column>
</wj-flex-grid>
```

### Grid with Custom Cell Templates

```typescript
// React example with custom cells
function CustomCellGrid() {
  return (
    <FlexGrid itemsSource={data} aria-label="Custom cell grid">
      <FlexGridColumn 
        binding="status" 
        header="Status"
        cellTemplate={(ctx) => (
          <div className="status-cell">
            <span className={`status-dot status-${ctx.item.status.toLowerCase()}`}></span>
            {ctx.item.status}
          </div>
        )}
      />
      <FlexGridColumn 
        binding="actions" 
        header="Actions"
        cellTemplate={(ctx) => (
          <div className="action-buttons">
            <button onClick={() => editItem(ctx.item.id)}>Edit</button>
            <button onClick={() => deleteItem(ctx.item.id)}>Delete</button>
          </div>
        )}
      />
    </FlexGrid>
  );
}
```

## Best Practices

### Accessibility
- Always provide meaningful `aria-label` or `aria-labelledby` for grids
- Set `headersFocusability="All"` for keyboard navigation
- Include alternative text for status indicators and icons
- Test with screen readers and keyboard navigation
- Ensure sufficient color contrast for all grid states

### Performance
- Use CollectionView for large datasets
- Implement virtual scrolling for very large datasets
- Optimize cell templates to avoid heavy DOM manipulation
- Use efficient filtering and sorting operations

### Responsive Design
- Test grid behavior at various screen sizes
- Consider horizontal scrolling for wide grids on mobile
- Use appropriate column widths and resizing options
- Consider collapsing less important columns on small screens

### Integration
- Use Saffron components (Toolbar, Pagination) for consistent UX
- Coordinate grid state with application state management
- Handle loading and error states appropriately
- Provide clear feedback for user actions

### Content
- Use descriptive column headers
- Provide consistent data formatting
- Handle empty states gracefully
- Follow TR content guidelines for labels and messaging

## Troubleshooting

### Common Issues

#### Styling Not Applied
- Ensure `@saffron/core-styles/dist/wijmo.css` is imported
- Check that Wijmo components are properly registered
- Verify CSS import order

#### Accessibility Issues
- Confirm `headersFocusability` is set correctly
- Check that grid has proper aria-label
- Verify interactive elements are keyboard accessible

#### Performance Issues
- Use CollectionView for data binding
- Optimize cell templates
- Consider pagination for large datasets

#### Integration Issues
- Ensure Saffron and Wijmo versions are compatible
- Check for CSS conflicts
- Verify proper component registration

### Getting Help

For Wijmo-specific issues:
- Check [Wijmo documentation](https://developer.mescius.com/wijmo)
- Review [Wijmo demos](https://developer.mescius.com/wijmo/demos)

For Saffron integration issues:
- Review the [SafWijmo demo](/?path=/docs/third-party-integrations-wijmo-flexgrid-demo--docs)
- Check Thomson Reuters Wijmo accessibility tracker
- Contact the Saffron team for integration support

The SafWijmo integration provides a robust, accessible solution for complex data grids while maintaining consistency with the Saffron Design System and Thomson Reuters brand standards.
