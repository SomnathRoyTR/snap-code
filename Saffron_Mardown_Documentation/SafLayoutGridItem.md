# SafLayoutGridItem

The SafLayoutGridItem component represents an individual item within a SafLayoutGrid system. It provides flexible layout positioning with responsive grid capabilities and supports various sizing and alignment options.

## React

### API

| Prop          | Type                    | Default     | Description                                    |
| ------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `gridColumn`  | `string \| number`      | `undefined` | CSS grid-column property value                 |
| `gridRow`     | `string \| number`      | `undefined` | CSS grid-row property value                    |
| `colSpan`     | `number`                | `1`         | Number of columns to span                      |
| `rowSpan`     | `number`                | `1`         | Number of rows to span                         |
| `justifySelf` | `string`                | `undefined` | CSS justify-self property value                |
| `alignSelf`   | `string`                | `undefined` | CSS align-self property value                  |
| `order`       | `number`                | `undefined` | CSS order property value                       |
| `className`   | `string`                | `undefined` | Additional CSS class names                     |
| `style`       | `CSSProperties`         | `undefined` | Inline styles                                  |
| `children`    | `ReactNode`             | `undefined` | The content to display within the grid item    |

### Examples

#### Basic Usage

```jsx
import { SafLayoutGrid, SafLayoutGridItem } from '@saffron/core-components';

function BasicGridItem() {
  return (
    <SafLayoutGrid>
      <SafLayoutGridItem>
        Grid Item 1
      </SafLayoutGridItem>
      <SafLayoutGridItem>
        Grid Item 2
      </SafLayoutGridItem>
      <SafLayoutGridItem>
        Grid Item 3
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
}
```

#### Column and Row Spanning

```jsx
import { SafLayoutGrid, SafLayoutGridItem } from '@saffron/core-components';

function SpanningGridItems() {
  return (
    <SafLayoutGrid columns={4} rows={3}>
      <SafLayoutGridItem colSpan={2} rowSpan={1}>
        Header (spans 2 columns)
      </SafLayoutGridItem>
      <SafLayoutGridItem colSpan={2} rowSpan={1}>
        Navigation (spans 2 columns)
      </SafLayoutGridItem>
      <SafLayoutGridItem colSpan={1} rowSpan={2}>
        Sidebar
      </SafLayoutGridItem>
      <SafLayoutGridItem colSpan={3} rowSpan={1}>
        Main Content (spans 3 columns)
      </SafLayoutGridItem>
      <SafLayoutGridItem colSpan={3} rowSpan={1}>
        Footer (spans 3 columns)
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
}
```

#### Advanced Usage with Positioning

```jsx
import { SafLayoutGrid, SafLayoutGridItem } from '@saffron/core-components';

function AdvancedGridLayout() {
  return (
    <SafLayoutGrid columns={3} rows={3} gap="20px">
      <SafLayoutGridItem 
        gridColumn="1 / 3" 
        gridRow="1"
        justifySelf="center"
        alignSelf="center"
      >
        Centered Header
      </SafLayoutGridItem>
      <SafLayoutGridItem 
        gridColumn="3" 
        gridRow="1 / 4"
        alignSelf="stretch"
      >
        Right Sidebar
      </SafLayoutGridItem>
      <SafLayoutGridItem 
        gridColumn="1 / 3" 
        gridRow="2"
        className="main-content"
      >
        Main Content Area
      </SafLayoutGridItem>
      <SafLayoutGridItem 
        gridColumn="1 / 3" 
        gridRow="3"
        order={-1}
      >
        Footer (reordered to appear first)
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
}
```

#### Responsive Grid Items

```jsx
import { SafLayoutGrid, SafLayoutGridItem } from '@saffron/core-components';
import { useState, useEffect } from 'react';

function ResponsiveGridItems() {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const checkScreenSize = () => {
      setIsMobile(window.innerWidth < 768);
    };
    
    checkScreenSize();
    window.addEventListener('resize', checkScreenSize);
    
    return () => window.removeEventListener('resize', checkScreenSize);
  }, []);

  return (
    <SafLayoutGrid columns={isMobile ? 1 : 3}>
      <SafLayoutGridItem 
        colSpan={isMobile ? 1 : 3}
        className="header-item"
      >
        Responsive Header
      </SafLayoutGridItem>
      <SafLayoutGridItem 
        colSpan={isMobile ? 1 : 2}
        className="content-item"
      >
        Main Content
      </SafLayoutGridItem>
      <SafLayoutGridItem 
        colSpan={1}
        className="sidebar-item"
      >
        Sidebar
      </SafLayoutGridItem>
    </SafLayoutGrid>
  );
}
```

## Angular

### API

| Input         | Type                    | Default     | Description                                    |
| ------------- | ----------------------- | ----------- | ---------------------------------------------- |
| `gridColumn`  | `string \| number`      | `undefined` | CSS grid-column property value                 |
| `gridRow`     | `string \| number`      | `undefined` | CSS grid-row property value                    |
| `colSpan`     | `number`                | `1`         | Number of columns to span                      |
| `rowSpan`     | `number`                | `1`         | Number of rows to span                         |
| `justifySelf` | `string`                | `undefined` | CSS justify-self property value                |
| `alignSelf`   | `string`                | `undefined` | CSS align-self property value                  |
| `order`       | `number`                | `undefined` | CSS order property value                       |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<saf-layout-grid>
  <saf-layout-grid-item>
    Grid Item 1
  </saf-layout-grid-item>
  <saf-layout-grid-item>
    Grid Item 2
  </saf-layout-grid-item>
  <saf-layout-grid-item>
    Grid Item 3
  </saf-layout-grid-item>
</saf-layout-grid>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-grid',
  template: `
    <saf-layout-grid>
      <saf-layout-grid-item>
        Grid Item 1
      </saf-layout-grid-item>
      <saf-layout-grid-item>
        Grid Item 2
      </saf-layout-grid-item>
      <saf-layout-grid-item>
        Grid Item 3
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class BasicGridComponent {}
```

#### Column and Row Spanning

```html
<!-- Angular template -->
<saf-layout-grid [columns]="4" [rows]="3">
  <saf-layout-grid-item [colSpan]="2" [rowSpan]="1">
    Header (spans 2 columns)
  </saf-layout-grid-item>
  <saf-layout-grid-item [colSpan]="2" [rowSpan]="1">
    Navigation (spans 2 columns)
  </saf-layout-grid-item>
  <saf-layout-grid-item [colSpan]="1" [rowSpan]="2">
    Sidebar
  </saf-layout-grid-item>
  <saf-layout-grid-item [colSpan]="3" [rowSpan]="1">
    Main Content (spans 3 columns)
  </saf-layout-grid-item>
  <saf-layout-grid-item [colSpan]="3" [rowSpan]="1">
    Footer (spans 3 columns)
  </saf-layout-grid-item>
</saf-layout-grid>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-spanning-grid',
  template: `
    <saf-layout-grid [columns]="4" [rows]="3">
      <saf-layout-grid-item [colSpan]="2" [rowSpan]="1">
        Header (spans 2 columns)
      </saf-layout-grid-item>
      <saf-layout-grid-item [colSpan]="2" [rowSpan]="1">
        Navigation (spans 2 columns)
      </saf-layout-grid-item>
      <saf-layout-grid-item [colSpan]="1" [rowSpan]="2">
        Sidebar
      </saf-layout-grid-item>
      <saf-layout-grid-item [colSpan]="3" [rowSpan]="1">
        Main Content (spans 3 columns)
      </saf-layout-grid-item>
      <saf-layout-grid-item [colSpan]="3" [rowSpan]="1">
        Footer (spans 3 columns)
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class SpanningGridComponent {}
```

#### Advanced Usage with Positioning

```html
<!-- Angular template -->
<saf-layout-grid [columns]="3" [rows]="3" gap="20px">
  <saf-layout-grid-item 
    gridColumn="1 / 3" 
    gridRow="1"
    justifySelf="center"
    alignSelf="center">
    Centered Header
  </saf-layout-grid-item>
  <saf-layout-grid-item 
    gridColumn="3" 
    gridRow="1 / 4"
    alignSelf="stretch">
    Right Sidebar
  </saf-layout-grid-item>
  <saf-layout-grid-item 
    gridColumn="1 / 3" 
    gridRow="2"
    class="main-content">
    Main Content Area
  </saf-layout-grid-item>
  <saf-layout-grid-item 
    gridColumn="1 / 3" 
    gridRow="3"
    [order]="-1">
    Footer (reordered to appear first)
  </saf-layout-grid-item>
</saf-layout-grid>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-advanced-grid',
  template: `
    <saf-layout-grid [columns]="3" [rows]="3" gap="20px">
      <saf-layout-grid-item 
        gridColumn="1 / 3" 
        gridRow="1"
        justifySelf="center"
        alignSelf="center">
        Centered Header
      </saf-layout-grid-item>
      <saf-layout-grid-item 
        gridColumn="3" 
        gridRow="1 / 4"
        alignSelf="stretch">
        Right Sidebar
      </saf-layout-grid-item>
      <saf-layout-grid-item 
        gridColumn="1 / 3" 
        gridRow="2"
        class="main-content">
        Main Content Area
      </saf-layout-grid-item>
      <saf-layout-grid-item 
        gridColumn="1 / 3" 
        gridRow="3"
        [order]="-1">
        Footer (reordered to appear first)
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class AdvancedGridComponent {}
```

#### Responsive Grid Items

```html
<!-- Angular template -->
<saf-layout-grid [columns]="isMobile ? 1 : 3">
  <saf-layout-grid-item 
    [colSpan]="isMobile ? 1 : 3"
    class="header-item">
    Responsive Header
  </saf-layout-grid-item>
  <saf-layout-grid-item 
    [colSpan]="isMobile ? 1 : 2"
    class="content-item">
    Main Content
  </saf-layout-grid-item>
  <saf-layout-grid-item 
    [colSpan]="1"
    class="sidebar-item">
    Sidebar
  </saf-layout-grid-item>
</saf-layout-grid>
```

```typescript
// Angular component
import { Component, OnInit, OnDestroy, HostListener } from '@angular/core';

@Component({
  selector: 'app-responsive-grid',
  template: `
    <saf-layout-grid [columns]="isMobile ? 1 : 3">
      <saf-layout-grid-item 
        [colSpan]="isMobile ? 1 : 3"
        class="header-item">
        Responsive Header
      </saf-layout-grid-item>
      <saf-layout-grid-item 
        [colSpan]="isMobile ? 1 : 2"
        class="content-item">
        Main Content
      </saf-layout-grid-item>
      <saf-layout-grid-item 
        [colSpan]="1"
        class="sidebar-item">
        Sidebar
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class ResponsiveGridComponent implements OnInit {
  isMobile = false;

  ngOnInit(): void {
    this.checkScreenSize();
  }

  @HostListener('window:resize', ['$event'])
  onResize(event: Event): void {
    this.checkScreenSize();
  }

  private checkScreenSize(): void {
    this.isMobile = window.innerWidth < 768;
  }
}
```

#### Dynamic Grid Items

```html
<!-- Angular template -->
<saf-layout-grid [columns]="gridColumns" [rows]="gridRows">
  <saf-layout-grid-item 
    *ngFor="let item of gridItems; trackBy: trackByFn"
    [colSpan]="item.colSpan"
    [rowSpan]="item.rowSpan"
    [gridColumn]="item.gridColumn"
    [gridRow]="item.gridRow"
    [class]="item.cssClass">
    {{ item.content }}
  </saf-layout-grid-item>
</saf-layout-grid>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface GridItemConfig {
  id: number;
  content: string;
  colSpan: number;
  rowSpan: number;
  gridColumn?: string;
  gridRow?: string;
  cssClass?: string;
}

@Component({
  selector: 'app-dynamic-grid',
  template: `
    <saf-layout-grid [columns]="gridColumns" [rows]="gridRows">
      <saf-layout-grid-item 
        *ngFor="let item of gridItems; trackBy: trackByFn"
        [colSpan]="item.colSpan"
        [rowSpan]="item.rowSpan"
        [gridColumn]="item.gridColumn"
        [gridRow]="item.gridRow"
        [class]="item.cssClass">
        {{ item.content }}
      </saf-layout-grid-item>
    </saf-layout-grid>
  `
})
export class DynamicGridComponent {
  gridColumns = 4;
  gridRows = 3;

  gridItems: GridItemConfig[] = [
    { id: 1, content: 'Header', colSpan: 4, rowSpan: 1, cssClass: 'header' },
    { id: 2, content: 'Sidebar', colSpan: 1, rowSpan: 2, cssClass: 'sidebar' },
    { id: 3, content: 'Main Content', colSpan: 3, rowSpan: 1, cssClass: 'main' },
    { id: 4, content: 'Footer', colSpan: 3, rowSpan: 1, cssClass: 'footer' }
  ];

  trackByFn(index: number, item: GridItemConfig): number {
    return item.id;
  }
}
```

### Best Practices

- **Semantic structure**: Use grid items to create meaningful layout sections (header, main, sidebar, footer)
- **Responsive design**: Adjust `colSpan` and `rowSpan` based on screen size for optimal mobile experience
- **Grid alignment**: Use `justifySelf` and `alignSelf` properties to fine-tune item positioning within grid cells
- **Performance**: Use `trackBy` functions in Angular when rendering dynamic grid items to optimize change detection
- **Accessibility**: Ensure grid items maintain logical reading order even when visually repositioned
- **Content overflow**: Consider how content will behave when it exceeds the allocated grid space
- **Grid gaps**: Coordinate with parent SafLayoutGrid gap settings for consistent spacing

### Notes

- SafLayoutGridItem components should always be direct children of SafLayoutGrid
- Grid positioning properties (`gridColumn`, `gridRow`) override span properties when both are specified
- The `order` property allows visual reordering without changing the DOM structure
- CSS Grid properties are automatically applied based on the provided props
- Responsive behavior should be coordinated between parent grid and child items for best results
- Consider using CSS custom properties for dynamic grid layouts in complex scenarios
