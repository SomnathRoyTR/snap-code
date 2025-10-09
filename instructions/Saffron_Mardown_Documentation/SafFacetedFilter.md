# SafFacetedFilter

A comprehensive filtering component that enables users to select from hierarchical categories and subcategories. SafFacetedFilter provides an intuitive interface for complex data filtering with support for nested facet items, counter badges, and bulk operations like clearing all selections.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `filterTitle` | `string` | `'Filters'` | Main heading for the filtering section |
| `resetButtonLabel` | `string` | `'Clear filters'` | Label text for the reset/clear button |
| `ariaTitleLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `2` | Hierarchical level of the title element for accessibility |
| `filterSubtitle` | `string` | `'Filter by:'` | Secondary heading for the filtering section |
| `ariaSubtitleLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `3` | Hierarchical level of the subtitle element for accessibility |
| `instructionalText` | `string` | - | Additional instructional text for user guidance |
| `showCounterBadges` | `boolean` | `false` | Whether to display item count badges on facet items |
| `children` | `ReactNode` | - | Facet categories and items to display |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClear` | `() => void` | Fires when the clear/reset button is clicked |

### Examples

#### Basic Product Filtering
```jsx
import { SafFacetedFilter, SafFacetCategory, SafFacetItem } from '@saffron/core-components/react';

function ProductFilter() {
  const [appliedFilters, setAppliedFilters] = useState(new Set());

  const handleFacetChange = (facetId, checked) => {
    const newFilters = new Set(appliedFilters);
    if (checked) {
      newFilters.add(facetId);
    } else {
      newFilters.delete(facetId);
    }
    setAppliedFilters(newFilters);
  };

  const handleClearFilters = () => {
    setAppliedFilters(new Set());
    console.log('All filters cleared');
  };

  return (
    <SafFacetedFilter
      filterTitle="Product Filters"
      filterSubtitle="Narrow your search:"
      instructionalText="Select categories to filter products"
      showCounterBadges={true}
      onClear={handleClearFilters}>
      
      <SafFacetCategory 
        id="category" 
        summary="Product Category"
        hideCaret={false}>
        <SafFacetItem
          id="electronics"
          facetName="Electronics"
          itemCount={245}
          checked={appliedFilters.has('electronics')}
          onChange={(e) => handleFacetChange('electronics', e.target.checked)}>
          
          <SafFacetItem
            id="laptops"
            facetName="Laptops"
            itemCount={89}
            checked={appliedFilters.has('laptops')}
            onChange={(e) => handleFacetChange('laptops', e.target.checked)}
          />
          
          <SafFacetItem
            id="smartphones"
            facetName="Smartphones"
            itemCount={156}
            checked={appliedFilters.has('smartphones')}
            onChange={(e) => handleFacetChange('smartphones', e.target.checked)}
          />
        </SafFacetItem>
        
        <SafFacetItem
          id="clothing"
          facetName="Clothing"
          itemCount={178}
          checked={appliedFilters.has('clothing')}
          onChange={(e) => handleFacetChange('clothing', e.target.checked)}>
          
          <SafFacetItem
            id="mens-clothing"
            facetName="Men's Clothing"
            itemCount={95}
            checked={appliedFilters.has('mens-clothing')}
            onChange={(e) => handleFacetChange('mens-clothing', e.target.checked)}
          />
          
          <SafFacetItem
            id="womens-clothing"
            facetName="Women's Clothing"
            itemCount={83}
            checked={appliedFilters.has('womens-clothing')}
            onChange={(e) => handleFacetChange('womens-clothing', e.target.checked)}
          />
        </SafFacetItem>
      </SafFacetCategory>
      
      <SafFacetCategory 
        id="price-range" 
        summary="Price Range">
        <SafFacetItem
          id="under-50"
          facetName="Under $50"
          itemCount={123}
          checked={appliedFilters.has('under-50')}
          onChange={(e) => handleFacetChange('under-50', e.target.checked)}
        />
        
        <SafFacetItem
          id="50-100"
          facetName="$50 - $100"
          itemCount={87}
          checked={appliedFilters.has('50-100')}
          onChange={(e) => handleFacetChange('50-100', e.target.checked)}
        />
        
        <SafFacetItem
          id="over-100"
          facetName="Over $100"
          itemCount={213}
          checked={appliedFilters.has('over-100')}
          onChange={(e) => handleFacetChange('over-100', e.target.checked)}
        />
      </SafFacetCategory>
    </SafFacetedFilter>
  );
}
```

#### Advanced Search Filtering
```jsx
import { SafFacetedFilter, SafFacetCategory, SafFacetItem } from '@saffron/core-components/react';

function AdvancedSearchFilter() {
  const [filters, setFilters] = useState({
    contentType: new Set(),
    dateRange: new Set(),
    author: new Set(),
    language: new Set()
  });

  const updateFilter = (category, facetId, checked) => {
    setFilters(prev => {
      const newFilters = { ...prev };
      if (checked) {
        newFilters[category].add(facetId);
      } else {
        newFilters[category].delete(facetId);
      }
      return newFilters;
    });
  };

  const handleClearAll = () => {
    setFilters({
      contentType: new Set(),
      dateRange: new Set(),
      author: new Set(),
      language: new Set()
    });
    
    // Also trigger search refresh
    onSearchRefresh();
  };

  const onSearchRefresh = () => {
    console.log('Refreshing search with filters:', filters);
    // Implement search logic here
  };

  // Calculate total selected filters
  const totalSelected = Object.values(filters).reduce((total, filterSet) => total + filterSet.size, 0);

  return (
    <div>
      <div style={{ marginBottom: '16px', padding: '12px', backgroundColor: '#f5f5f5', borderRadius: '4px' }}>
        <strong>Active Filters: {totalSelected}</strong>
        {totalSelected > 0 && (
          <button 
            style={{ marginLeft: '12px', fontSize: '0.875rem' }}
            onClick={onSearchRefresh}>
            Apply Filters
          </button>
        )}
      </div>
      
      <SafFacetedFilter
        filterTitle="Search Filters"
        filterSubtitle="Refine your search:"
        instructionalText="Use the categories below to narrow your search results"
        showCounterBadges={true}
        ariaTitleLevel={2}
        ariaSubtitleLevel={3}
        onClear={handleClearAll}>
        
        <SafFacetCategory id="content-type" summary="Content Type">
          <SafFacetItem
            id="articles"
            facetName="Articles"
            itemCount={1245}
            checked={filters.contentType.has('articles')}
            onChange={(e) => updateFilter('contentType', 'articles', e.target.checked)}
          />
          
          <SafFacetItem
            id="reports"
            facetName="Reports"
            itemCount={89}
            checked={filters.contentType.has('reports')}
            onChange={(e) => updateFilter('contentType', 'reports', e.target.checked)}
          />
          
          <SafFacetItem
            id="case-studies"
            facetName="Case Studies"
            itemCount={156}
            checked={filters.contentType.has('case-studies')}
            onChange={(e) => updateFilter('contentType', 'case-studies', e.target.checked)}
          />
        </SafFacetCategory>
        
        <SafFacetCategory id="date-range" summary="Publication Date">
          <SafFacetItem
            id="last-week"
            facetName="Last Week"
            itemCount={45}
            checked={filters.dateRange.has('last-week')}
            onChange={(e) => updateFilter('dateRange', 'last-week', e.target.checked)}
          />
          
          <SafFacetItem
            id="last-month"
            facetName="Last Month"
            itemCount={178}
            checked={filters.dateRange.has('last-month')}
            onChange={(e) => updateFilter('dateRange', 'last-month', e.target.checked)}
          />
          
          <SafFacetItem
            id="last-year"
            facetName="Last Year"
            itemCount={823}
            checked={filters.dateRange.has('last-year')}
            onChange={(e) => updateFilter('dateRange', 'last-year', e.target.checked)}
          />
        </SafFacetCategory>
        
        <SafFacetCategory id="author" summary="Author">
          <SafFacetItem
            id="john-smith"
            facetName="John Smith"
            itemCount={23}
            checked={filters.author.has('john-smith')}
            onChange={(e) => updateFilter('author', 'john-smith', e.target.checked)}
          />
          
          <SafFacetItem
            id="jane-doe"
            facetName="Jane Doe"
            itemCount={18}
            checked={filters.author.has('jane-doe')}
            onChange={(e) => updateFilter('author', 'jane-doe', e.target.checked)}
          />
        </SafFacetCategory>
      </SafFacetedFilter>
    </div>
  );
}
```

#### Dynamic Faceted Filter with API
```jsx
import { SafFacetedFilter, SafFacetCategory, SafFacetItem } from '@saffron/core-components/react';

function DynamicFacetedFilter() {
  const [filterData, setFilterData] = useState(null);
  const [selectedFilters, setSelectedFilters] = useState(new Map());
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulate API call for filter data
    fetchFilterData();
  }, []);

  const fetchFilterData = async () => {
    setLoading(true);
    try {
      // Mock API response
      const response = await new Promise(resolve => 
        setTimeout(() => resolve({
          categories: [
            {
              id: 'industries',
              name: 'Industries',
              items: [
                { id: 'tech', name: 'Technology', count: 1245, children: [
                  { id: 'software', name: 'Software', count: 567 },
                  { id: 'hardware', name: 'Hardware', count: 678 }
                ]},
                { id: 'finance', name: 'Finance', count: 892 },
                { id: 'healthcare', name: 'Healthcare', count: 456 }
              ]
            },
            {
              id: 'regions',
              name: 'Regions',
              items: [
                { id: 'north-america', name: 'North America', count: 1567 },
                { id: 'europe', name: 'Europe', count: 1234 },
                { id: 'asia', name: 'Asia', count: 2345 }
              ]
            }
          ]
        }), 1500)
      );
      setFilterData(response);
    } catch (error) {
      console.error('Failed to load filter data:', error);
    } finally {
      setLoading(false);
    }
  };

  const handleFilterChange = (filterId, checked) => {
    const newFilters = new Map(selectedFilters);
    if (checked) {
      newFilters.set(filterId, true);
    } else {
      newFilters.delete(filterId);
    }
    setSelectedFilters(newFilters);
  };

  const handleClearFilters = () => {
    setSelectedFilters(new Map());
  };

  const renderFacetItem = (item, level = 0) => (
    <SafFacetItem
      key={item.id}
      id={item.id}
      facetName={item.name}
      itemCount={item.count}
      checked={selectedFilters.has(item.id)}
      onChange={(e) => handleFilterChange(item.id, e.target.checked)}
      style={{ paddingLeft: `${level * 16}px` }}>
      
      {item.children?.map(child => renderFacetItem(child, level + 1))}
    </SafFacetItem>
  );

  if (loading) {
    return (
      <div style={{ padding: '24px', textAlign: 'center' }}>
        <div>Loading filters...</div>
      </div>
    );
  }

  return (
    <SafFacetedFilter
      filterTitle="Dynamic Filters"
      filterSubtitle="Filter your data:"
      instructionalText="These filters are loaded dynamically from our API"
      showCounterBadges={true}
      onClear={handleClearFilters}>
      
      {filterData?.categories?.map(category => (
        <SafFacetCategory 
          key={category.id}
          id={category.id} 
          summary={category.name}>
          
          {category.items.map(item => renderFacetItem(item))}
        </SafFacetCategory>
      ))}
      
      {selectedFilters.size > 0 && (
        <div style={{ marginTop: '16px', padding: '12px', backgroundColor: '#e8f4f8', borderRadius: '4px' }}>
          <strong>Selected Filters ({selectedFilters.size}):</strong>
          <ul style={{ margin: '8px 0', paddingLeft: '20px' }}>
            {Array.from(selectedFilters.keys()).map(filterId => (
              <li key={filterId}>{filterId}</li>
            ))}
          </ul>
        </div>
      )}
    </SafFacetedFilter>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `filterTitle` | `string` | `'Filters'` | Main heading for the filtering section |
| `resetButtonLabel` | `string` | `'Clear filters'` | Label text for the reset/clear button |
| `ariaTitleLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `2` | Hierarchical level of the title element for accessibility |
| `filterSubtitle` | `string` | `'Filter by:'` | Secondary heading for the filtering section |
| `ariaSubtitleLevel` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `3` | Hierarchical level of the subtitle element for accessibility |
| `instructionalText` | `string` | - | Additional instructional text for user guidance |
| `showCounterBadges` | `boolean` | `false` | Whether to display item count badges on facet items |

### Events

| Output | Type | Description |
|--------|------|-------------|
| `clear` | `EventEmitter<void>` | Fires when the clear/reset button is clicked |

### Examples

#### Basic Product Filtering
```html
<saf-faceted-filter
  filterTitle="Product Filters"
  filterSubtitle="Narrow your search:"
  instructionalText="Select categories to filter products"
  [showCounterBadges]="true"
  (clear)="handleClearFilters()">
  
  <saf-facet-category 
    id="category" 
    summary="Product Category"
    [hideCaret]="false">
    
    <saf-facet-item
      id="electronics"
      facetName="Electronics"
      [itemCount]="245"
      [checked]="appliedFilters.has('electronics')"
      (change)="handleFacetChange('electronics', $event.target.checked)">
      
      <saf-facet-item
        id="laptops"
        facetName="Laptops"
        [itemCount]="89"
        [checked]="appliedFilters.has('laptops')"
        (change)="handleFacetChange('laptops', $event.target.checked)">
      </saf-facet-item>
      
      <saf-facet-item
        id="smartphones"
        facetName="Smartphones"
        [itemCount]="156"
        [checked]="appliedFilters.has('smartphones')"
        (change)="handleFacetChange('smartphones', $event.target.checked)">
      </saf-facet-item>
    </saf-facet-item>
    
    <saf-facet-item
      id="clothing"
      facetName="Clothing"
      [itemCount]="178"
      [checked]="appliedFilters.has('clothing')"
      (change)="handleFacetChange('clothing', $event.target.checked)">
      
      <saf-facet-item
        id="mens-clothing"
        facetName="Men's Clothing"
        [itemCount]="95"
        [checked]="appliedFilters.has('mens-clothing')"
        (change)="handleFacetChange('mens-clothing', $event.target.checked)">
      </saf-facet-item>
    </saf-facet-item>
  </saf-facet-category>
  
  <saf-facet-category 
    id="price-range" 
    summary="Price Range">
    
    <saf-facet-item
      id="under-50"
      facetName="Under $50"
      [itemCount]="123"
      [checked]="appliedFilters.has('under-50')"
      (change)="handleFacetChange('under-50', $event.target.checked)">
    </saf-facet-item>
    
    <saf-facet-item
      id="50-100"
      facetName="$50 - $100"
      [itemCount]="87"
      [checked]="appliedFilters.has('50-100')"
      (change)="handleFacetChange('50-100', $event.target.checked)">
    </saf-facet-item>
  </saf-facet-category>
</saf-faceted-filter>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-product-filter',
  templateUrl: './product-filter.component.html'
})
export class ProductFilterComponent {
  appliedFilters = new Set<string>();

  handleFacetChange(facetId: string, checked: boolean) {
    if (checked) {
      this.appliedFilters.add(facetId);
    } else {
      this.appliedFilters.delete(facetId);
    }
    
    // Trigger filter update
    this.onFiltersChanged();
  }

  handleClearFilters() {
    this.appliedFilters.clear();
    console.log('All filters cleared');
    this.onFiltersChanged();
  }

  private onFiltersChanged() {
    // Implement filter logic here
    console.log('Applied filters:', Array.from(this.appliedFilters));
  }
}
```

#### Dynamic Faceted Filter
```html
<div *ngIf="loading" class="loading-state">
  Loading filters...
</div>

<saf-faceted-filter
  *ngIf="!loading && filterData"
  filterTitle="Dynamic Filters"
  filterSubtitle="Filter your data:"
  instructionalText="These filters are loaded dynamically from our API"
  [showCounterBadges]="true"
  (clear)="handleClearFilters()">
  
  <saf-facet-category 
    *ngFor="let category of filterData.categories"
    [id]="category.id"
    [summary]="category.name">
    
    <ng-container *ngFor="let item of category.items">
      <saf-facet-item
        [id]="item.id"
        [facetName]="item.name"
        [itemCount]="item.count"
        [checked]="selectedFilters.has(item.id)"
        (change)="handleFilterChange(item.id, $event.target.checked)">
        
        <saf-facet-item
          *ngFor="let child of item.children || []"
          [id]="child.id"
          [facetName]="child.name"
          [itemCount]="child.count"
          [checked]="selectedFilters.has(child.id)"
          (change)="handleFilterChange(child.id, $event.target.checked)"
          [style.padding-left.px]="16">
        </saf-facet-item>
      </saf-facet-item>
    </ng-container>
  </saf-facet-category>
  
  <div *ngIf="selectedFilters.size > 0" class="selected-filters">
    <strong>Selected Filters ({{ selectedFilters.size }}):</strong>
    <ul>
      <li *ngFor="let filterId of getSelectedFilterIds()">{{ filterId }}</li>
    </ul>
  </div>
</saf-faceted-filter>
```

```typescript
import { Component, OnInit } from '@angular/core';

interface FilterItem {
  id: string;
  name: string;
  count: number;
  children?: FilterItem[];
}

interface FilterCategory {
  id: string;
  name: string;
  items: FilterItem[];
}

interface FilterData {
  categories: FilterCategory[];
}

@Component({
  selector: 'app-dynamic-faceted-filter',
  templateUrl: './dynamic-faceted-filter.component.html',
  styleUrls: ['./dynamic-faceted-filter.component.scss']
})
export class DynamicFacetedFilterComponent implements OnInit {
  filterData: FilterData | null = null;
  selectedFilters = new Map<string, boolean>();
  loading = true;

  ngOnInit() {
    this.fetchFilterData();
  }

  async fetchFilterData() {
    this.loading = true;
    try {
      // Simulate API call
      const response = await new Promise<FilterData>(resolve => 
        setTimeout(() => resolve({
          categories: [
            {
              id: 'industries',
              name: 'Industries',
              items: [
                { 
                  id: 'tech', 
                  name: 'Technology', 
                  count: 1245, 
                  children: [
                    { id: 'software', name: 'Software', count: 567 },
                    { id: 'hardware', name: 'Hardware', count: 678 }
                  ]
                },
                { id: 'finance', name: 'Finance', count: 892 },
                { id: 'healthcare', name: 'Healthcare', count: 456 }
              ]
            }
          ]
        }), 1500)
      );
      this.filterData = response;
    } catch (error) {
      console.error('Failed to load filter data:', error);
    } finally {
      this.loading = false;
    }
  }

  handleFilterChange(filterId: string, checked: boolean) {
    if (checked) {
      this.selectedFilters.set(filterId, true);
    } else {
      this.selectedFilters.delete(filterId);
    }
  }

  handleClearFilters() {
    this.selectedFilters.clear();
  }

  getSelectedFilterIds(): string[] {
    return Array.from(this.selectedFilters.keys());
  }
}
```

## Best Practices

- **Use hierarchical structure**: Organize filters logically with parent-child relationships to help users understand the data structure.
- **Show item counts**: Enable `showCounterBadges` to display the number of items in each category, helping users make informed decisions.
- **Provide clear labels**: Use descriptive `filterTitle`, `filterSubtitle`, and `instructionalText` to guide users.
- **Handle accessibility**: Set appropriate `ariaTitleLevel` and `ariaSubtitleLevel` values to maintain proper heading hierarchy.
- **Implement clear functionality**: Always provide a way to clear all selections quickly.
- **Consider performance**: For large datasets, implement lazy loading or virtualization for facet items.
- **Maintain state**: Persist filter selections across page navigations when appropriate.
- **Provide feedback**: Show loading states and confirmation when filters are applied or cleared.

## Notes

- SafFacetedFilter works in conjunction with SafFacetCategory and SafFacetItem components to create the complete filtering interface.
- The component automatically manages the counter badge display for all nested facet items when `showCounterBadges` is enabled.
- The clear functionality recursively unchecks all facet items throughout the hierarchy.
- Facet items support indeterminate states for parent items when some but not all children are selected.
- The component emits events that can be used to trigger search or filtering operations in your application.
- Consider implementing debounced search functionality when filters change frequently to improve performance.
