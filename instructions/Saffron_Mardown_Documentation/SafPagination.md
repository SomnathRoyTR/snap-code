# SafPagination Component

The `SafPagination` component provides comprehensive pagination controls for managing large datasets in the Saffron Design System. Built on FAST Element, it offers navigation controls, page information display, items-per-page selection, and accessibility features for data tables and lists.

## Table of Contents

- [Overview](#overview)
- [Component Properties](#component-properties)
- [Events](#events)
- [Methods](#methods)
- [Parts](#parts)
- [CSS Custom Properties](#css-custom-properties)
- [React Integration](#react-integration)
- [Angular Integration](#angular-integration)
- [Usage Examples](#usage-examples)
- [Accessibility](#accessibility)
- [Best Practices](#best-practices)

## Overview

The SafPagination component provides a complete pagination solution with navigation controls, page indicators, and items-per-page selection. It can operate in controlled or uncontrolled modes to support different state management patterns.

Key Features:
- **Page Navigation**: Previous/next buttons with proper disabled states
- **Page Information**: Current page, total pages, and result ranges
- **Items Per Page**: Configurable selection dropdown
- **Direct Navigation**: "Go to page" input field with validation
- **Responsive Design**: Adapts layout based on available width
- **Accessibility**: Full ARIA support with live region announcements
- **Controlled Mode**: Supports external state management patterns

## Component Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `ariaLabel` | `string` | `"Pagination"` | ARIA label for the pagination region |
| `pageResultsLabel` | `string` | `"Page"` | Text for the page label |
| `pageOfLabel` | `string` | `"of"` | Text for the "of" separator |
| `previousButton` | `string` | `"Previous"` | Text for the previous button |
| `nextButton` | `string` | `"Next"` | Text for the next button |
| `resultsLabel` | `string` | `"Showing"` | Text for the results label |
| `toLabel` | `string` | `"to"` | Text for the "to" separator |
| `itemsInputLabel` | `string` | `"Items per page"` | Label for items per page select |
| `pageInputLabel` | `string` | `"Go to page:"` | Label for page input field |
| `pageButton` | `string` | `"Go"` | Text for the go button |
| `itemsLabel` | `string` | `""` | Label for items (e.g., "results", "rows") |
| `hasBorder` | `boolean` | `false` | Whether to show component border |
| `totalItemCount` | `number` | - | Total number of items in dataset |
| `currentPageIndex` | `number` | `1` | Current page number (1-based) |
| `itemsArray` | `number[]` | `[10, 25, 50, 100]` | Options for items per page |
| `itemsPerPage` | `number` | `25` | Current items per page |
| `dataAriaLive` | `PaginationAriaLive` | `"off"` | ARIA live region setting |
| `density` | `ComponentDensity` | `inherit` | Controls spacing and sizing |
| `controlled` | `boolean` | `false` | Enables controlled mode |

### Read-Only Properties

| Property | Type | Description |
|----------|------|-------------|
| `startIndex` | `number` | Starting index of current page results |
| `endIndex` | `number` | Ending index of current page results |
| `totalPages` | `number` | Total number of pages |
| `dividerOrientation` | `boolean` | Responsive divider orientation |

### ARIA Live Options

The `dataAriaLive` property accepts these values:
- `"off"` - No live region announcements
- `"polite"` - Announcements when convenient
- `"assertive"` - Immediate announcements

## Events

| Event | Bubbles | Cancelable | Detail | Description |
|-------|---------|------------|--------|-------------|
| `previous` | `true` | `false` | `number` | Fired when previous button is clicked |
| `next` | `true` | `false` | `number` | Fired when next button is clicked |
| `change` | `true` | `false` | `number` | Fired when page changes via input |
| `items-per-page-change` | `true` | `false` | `number` | Fired when items per page changes |

## Methods

### Navigation Methods

```typescript
// Go to previous page
pagination.previous(): void

// Go to next page  
pagination.next(): void

// Update page value
pagination.updatePageValue(value: unknown): void

// Update items per page
pagination.updateFormValue(value: unknown): void

// Navigate via button
pagination.buttonPageValue(): void
```

### Internal Calculation Methods

```typescript
// Calculate start index
pagination.getStartIndex(): number

// Calculate end index
pagination.getEndIndex(): number

// Calculate total pages
pagination.getTotalPages(): number
```

## Parts

| Part | Description |
|------|-------------|
| `control` | The main pagination container |
| `content` | The content wrapper |
| `all-page-controls` | Page navigation controls container |
| `flipper-content` | Page info and navigation buttons |
| `flipper-label` | Page information text |
| `u-emphasis` | Emphasized numbers in labels |
| `flipper-controls` | Navigation buttons container |
| `flipper-control-previous` | Previous button |
| `flipper-control-next` | Next button |
| `flipper-divider` | Responsive divider |
| `page-controls` | Go to page controls |
| `page-control` | Page input field |
| `page-control-button` | Go button |
| `items-content-container` | Results info and controls |
| `items-content` | Results information text |
| `items-controls` | Items per page controls |
| `item-control` | Items per page select |

## CSS Custom Properties

The SafPagination component uses the design system's spacing and typography tokens:

```css
saf-pagination {
  /* Density affects spacing */
  --density: inherit;
  
  /* Responsive breakpoint */
  --responsive-width: 594px;
}
```

## React Integration

### Basic Usage

```tsx
import SafPagination from '@saffron/react/pagination';

function MyTable() {
  return (
    <SafPagination
      totalItemCount={1000}
      itemsPerPage={25}
      currentPageIndex={1}
    />
  );
}
```

### Controlled Pagination

```tsx
import SafPagination from '@saffron/react/pagination';
import { useState } from 'react';

function ControlledPagination() {
  const [currentPage, setCurrentPage] = useState(1);
  const [itemsPerPage, setItemsPerPage] = useState(25);
  const totalItems = 1000;

  const handlePageChange = (event: CustomEvent) => {
    setCurrentPage(event.detail);
  };

  const handleItemsPerPageChange = (event: CustomEvent) => {
    setItemsPerPage(event.detail);
    setCurrentPage(1); // Reset to first page
  };

  return (
    <SafPagination
      controlled
      totalItemCount={totalItems}
      currentPageIndex={currentPage}
      itemsPerPage={itemsPerPage}
      onChange={handlePageChange}
      onItemsPerPageChange={handleItemsPerPageChange}
    />
  );
}
```

### With Custom Labels

```tsx
import SafPagination from '@saffron/react/pagination';

function CustomLabelsPagination() {
  return (
    <SafPagination
      totalItemCount={500}
      resultsLabel="Displaying"
      toLabel="through"
      pageOfLabel="out of"
      itemsLabel="records"
      pageResultsLabel="Record set"
      itemsInputLabel="Records per page"
    />
  );
}
```

### With ARIA Live Announcements

```tsx
import SafPagination from '@saffron/react/pagination';

function AccessiblePagination() {
  return (
    <SafPagination
      totalItemCount={750}
      dataAriaLive="polite"
      ariaLabel="Search results pagination"
      itemsLabel="search results"
    />
  );
}
```

### With Custom Items Per Page Options

```tsx
import SafPagination from '@saffron/react/pagination';

function CustomItemsPagination() {
  const customOptions = [5, 15, 30, 60];
  
  return (
    <SafPagination
      totalItemCount={300}
      itemsArray={customOptions}
      itemsPerPage={15}
    />
  );
}
```

## Angular Integration

### Basic Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <saf-pagination
      [totalItemCount]="1000"
      [itemsPerPage]="25"
      [currentPageIndex]="1">
    </saf-pagination>
  `
})
export class ExampleComponent {}
```

### With Event Handling

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-pagination-example',
  template: `
    <saf-pagination
      [controlled]="true"
      [totalItemCount]="totalItems"
      [currentPageIndex]="currentPage"
      [itemsPerPage]="itemsPerPage"
      (change)="onPageChange($event)"
      (items-per-page-change)="onItemsPerPageChange($event)"
      (previous)="onPrevious($event)"
      (next)="onNext($event)">
    </saf-pagination>
  `
})
export class PaginationExampleComponent {
  totalItems = 1000;
  currentPage = 1;
  itemsPerPage = 25;

  onPageChange(event: CustomEvent) {
    this.currentPage = event.detail;
    this.loadData();
  }

  onItemsPerPageChange(event: CustomEvent) {
    this.itemsPerPage = event.detail;
    this.currentPage = 1;
    this.loadData();
  }

  onPrevious(event: CustomEvent) {
    console.log('Previous clicked, current page:', event.detail);
  }

  onNext(event: CustomEvent) {
    console.log('Next clicked, current page:', event.detail);
  }

  private loadData() {
    // Load data based on current page and items per page
  }
}
```

### With Property Binding and Customization

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-custom-pagination',
  template: `
    <saf-pagination
      [totalItemCount]="data.totalCount"
      [currentPageIndex]="pagination.currentPage"
      [itemsPerPage]="pagination.itemsPerPage"
      [itemsArray]="itemsPerPageOptions"
      [hasBorder]="true"
      [density]="'normal'"
      [dataAriaLive]="'polite'"
      [resultsLabel]="'Showing'"
      [toLabel]="'through'"
      [pageOfLabel]="'of'"
      [itemsLabel]="'products'"
      [ariaLabel]="'Product list pagination'"
      (change)="handlePageChange($event)"
      (items-per-page-change)="handleItemsPerPageChange($event)">
    </saf-pagination>
  `
})
export class CustomPaginationComponent {
  data = {
    totalCount: 750
  };

  pagination = {
    currentPage: 1,
    itemsPerPage: 20
  };

  itemsPerPageOptions = [10, 20, 50, 100];

  handlePageChange(event: CustomEvent) {
    this.pagination.currentPage = event.detail;
  }

  handleItemsPerPageChange(event: CustomEvent) {
    this.pagination.itemsPerPage = event.detail;
    this.pagination.currentPage = 1;
  }
}
```

### Reactive Forms Integration

```typescript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-reactive-pagination',
  template: `
    <form [formGroup]="paginationForm">
      <saf-pagination
        [controlled]="true"
        [totalItemCount]="totalItems"
        [currentPageIndex]="paginationForm.get('currentPage')?.value"
        [itemsPerPage]="paginationForm.get('itemsPerPage')?.value"
        (change)="updateCurrentPage($event)"
        (items-per-page-change)="updateItemsPerPage($event)">
      </saf-pagination>
    </form>
  `
})
export class ReactivePaginationComponent implements OnInit {
  paginationForm: FormGroup;
  totalItems = 500;

  constructor(private fb: FormBuilder) {}

  ngOnInit() {
    this.paginationForm = this.fb.group({
      currentPage: [1],
      itemsPerPage: [25]
    });

    // Subscribe to form changes
    this.paginationForm.valueChanges.subscribe(values => {
      this.loadData(values.currentPage, values.itemsPerPage);
    });
  }

  updateCurrentPage(event: CustomEvent) {
    this.paginationForm.patchValue({ currentPage: event.detail });
  }

  updateItemsPerPage(event: CustomEvent) {
    this.paginationForm.patchValue({ 
      itemsPerPage: event.detail,
      currentPage: 1 
    });
  }

  private loadData(page: number, itemsPerPage: number) {
    // Load data logic
  }
}
```

## Usage Examples

### Basic Pagination

```html
<saf-pagination
  total-item-count="1000"
  items-per-page="25">
</saf-pagination>
```

### With Custom Labels

```html
<saf-pagination
  total-item-count="500"
  results-label="Displaying"
  to-label="through"
  page-of-label="out of"
  items-label="records">
</saf-pagination>
```

### Controlled Mode

```html
<saf-pagination
  controlled
  total-item-count="750"
  current-page-index="3"
  items-per-page="50">
</saf-pagination>
```

### With Border and Density

```html
<saf-pagination
  total-item-count="300"
  has-border="true"
  density="tight">
</saf-pagination>
```

### Accessible with Live Region

```html
<saf-pagination
  total-item-count="1200"
  data-aria-live="polite"
  aria-label="Search results pagination"
  items-label="search results">
</saf-pagination>
```

### No Results State

```html
<saf-pagination
  total-item-count="0"
  items-label="results">
</saf-pagination>
```

### Custom Items Per Page

```html
<saf-pagination
  total-item-count="800"
  items-per-page="15"
  :items-array="[5, 15, 30, 60]">
</saf-pagination>
```

### Responsive Layout

```html
<saf-pagination
  total-item-count="2000"
  items-per-page="100"
  style="width: 400px;">
</saf-pagination>
```

## Accessibility

The SafPagination component provides comprehensive accessibility support:

### ARIA Implementation
- **role="navigation"**: Identifies pagination as navigation landmark
- **aria-label**: Customizable label for the pagination region
- **aria-describedby**: Links items per page control to results display
- **aria-labelledby**: Groups page controls with appropriate labels

### Live Region Support
- **data-aria-live**: Configurable live region announcements
- **Automatic Announcements**: Results changes announced to screen readers
- **Polite/Assertive**: Respect user preferences for announcement urgency

### Keyboard Support
- **Tab Navigation**: All interactive elements focusable
- **Enter/Space**: Activates buttons and controls
- **Arrow Keys**: Navigate within select and number field controls
- **Form Controls**: Standard keyboard interaction for inputs

### Screen Reader Support
- **Clear Labels**: All controls have descriptive labels
- **State Announcements**: Page changes and results announced
- **Context Information**: Current page and total pages clearly indicated

### Focus Management
- **Visible Focus**: Clear focus indicators on all interactive elements
- **Logical Order**: Tab order follows visual layout
- **No Focus Traps**: Users can navigate away from pagination

## Best Practices

### State Management
- Use controlled mode for complex applications with external state management
- Handle pagination state changes in parent components
- Reset to page 1 when changing items per page or filters

### Performance Considerations
- Implement virtual scrolling for very large datasets
- Debounce page input changes to avoid excessive API calls
- Use appropriate page sizes based on data complexity

### User Experience
- Provide clear feedback when pagination is loading
- Disable navigation buttons appropriately at boundaries
- Show meaningful empty states when no results exist

### Internationalization
- Customize all text labels for different languages
- Consider RTL layouts for right-to-left languages
- Use appropriate number formatting for different locales

### Responsive Design
- Component automatically adapts layout at 594px breakpoint
- Test pagination at various screen sizes
- Consider mobile-first pagination patterns for small screens

### Accessibility
- Always provide meaningful aria-label for the pagination region
- Use appropriate live region settings based on user needs
- Test with keyboard navigation and screen readers

### Integration
- Coordinate pagination with data loading states
- Handle error states gracefully
- Provide loading indicators during page transitions

The SafPagination component provides a complete, accessible solution for navigating large datasets while maintaining excellent user experience across all devices and assistive technologies.
