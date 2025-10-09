# SafFilterGroup

## Overview

SafFilterGroup is a container component that organizes related filter chips into logical groups with labels, collapse functionality, and batch operations. It provides structured organization for complex filtering interfaces with support for categorization, group actions, and accessibility features.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `title` | `string \| ReactNode` | - | Group title/label |
| `filters` | `Filter[]` | `[]` | Array of filter objects |
| `collapsible` | `boolean` | `false` | Enable collapse functionality |
| `collapsed` | `boolean` | `false` | Collapse state |
| `clearable` | `boolean` | `true` | Show clear all button |
| `disabled` | `boolean` | `false` | Disable entire group |
| `variant` | `'default' \| 'outline' \| 'filled'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Group size |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout direction |
| `wrap` | `boolean` | `true` | Enable chip wrapping |
| `maxVisible` | `number` | - | Maximum visible chips before truncation |
| `spacing` | `'compact' \| 'normal' \| 'loose'` | `'normal'` | Chip spacing |
| `showCount` | `boolean` | `true` | Show filter count in title |
| `icon` | `ReactElement` | - | Group icon |
| `description` | `string` | - | Group description |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onFilterRemove` | `(filterId: string, filter: Filter) => void` | Fired when filter is removed |
| `onClearAll` | `() => void` | Fired when all filters are cleared |
| `onToggleCollapse` | `(collapsed: boolean) => void` | Fired when group is collapsed/expanded |
| `onFilterClick` | `(filterId: string, filter: Filter) => void` | Fired when filter is clicked |
| `onGroupFocus` | `(event: FocusEvent) => void` | Fired when group receives focus |

### Filter Object

```typescript
interface Filter {
  id: string;
  label: string;
  value: any;
  removable?: boolean;
  disabled?: boolean;
  color?: string;
  variant?: string;
  icon?: ReactElement;
  tooltip?: string;
}
```

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `title` | `string \| TemplateRef` | - | Group title/label |
| `filters` | `Filter[]` | `[]` | Array of filter objects |
| `collapsible` | `boolean` | `false` | Enable collapse functionality |
| `collapsed` | `boolean` | `false` | Collapse state |
| `clearable` | `boolean` | `true` | Show clear all button |
| `disabled` | `boolean` | `false` | Disable entire group |
| `variant` | `'default' \| 'outline' \| 'filled'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Group size |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Layout direction |
| `wrap` | `boolean` | `true` | Enable chip wrapping |
| `maxVisible` | `number` | - | Maximum visible chips before truncation |
| `spacing` | `'compact' \| 'normal' \| 'loose'` | `'normal'` | Chip spacing |
| `showCount` | `boolean` | `true` | Show filter count in title |
| `description` | `string` | - | Group description |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `filterRemove` | `EventEmitter<{filterId: string, filter: Filter}>` | Fired when filter is removed |
| `clearAll` | `EventEmitter<void>` | Fired when all filters are cleared |
| `toggleCollapse` | `EventEmitter<boolean>` | Fired when group is collapsed/expanded |
| `filterClick` | `EventEmitter<{filterId: string, filter: Filter}>` | Fired when filter is clicked |
| `groupFocus` | `EventEmitter<FocusEvent>` | Fired when group receives focus |

## Usage Examples

### Basic Filter Groups

```typescript
// React
const BasicFilterGroups = ({ filterGroups, onFiltersChange }) => {
  const handleGroupClear = (groupId) => {
    onFiltersChange(groupId, []);
  };

  const handleFilterRemove = (groupId, filterId) => {
    const group = filterGroups.find(g => g.id === groupId);
    const updatedFilters = group.filters.filter(f => f.id !== filterId);
    onFiltersChange(groupId, updatedFilters);
  };

  return (
    <div className="filter-groups">
      {filterGroups.map(group => (
        <SafFilterGroup
          key={group.id}
          title={group.title}
          filters={group.filters}
          onFilterRemove={(filterId, filter) => handleFilterRemove(group.id, filterId)}
          onClearAll={() => handleGroupClear(group.id)}
          clearable
          showCount
        />
      ))}
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="filter-groups">
  <saf-filter-group
    *ngFor="let group of filterGroups"
    [title]="group.title"
    [filters]="group.filters"
    [clearable]="true"
    [showCount]="true"
    (filterRemove)="handleFilterRemove(group.id, $event)"
    (clearAll)="handleGroupClear(group.id)">
  </saf-filter-group>
</div>
```

### Collapsible Filter Groups

```typescript
// React
const CollapsibleFilterGroups = ({ 
  filterGroups, 
  collapsedGroups,
  onToggleGroup,
  onFiltersChange 
}) => {
  const isGroupCollapsed = (groupId) => {
    return collapsedGroups.includes(groupId);
  };

  return (
    <div className="collapsible-filter-groups">
      <div className="filter-header">
        <h3>Active Filters</h3>
        <SafButton
          variant="ghost"
          size="small"
          onClick={() => {
            // Clear all groups
            filterGroups.forEach(group => {
              onFiltersChange(group.id, []);
            });
          }}
        >
          Clear All Filters
        </SafButton>
      </div>

      {filterGroups.map(group => (
        <SafFilterGroup
          key={group.id}
          title={group.title}
          filters={group.filters}
          collapsible
          collapsed={isGroupCollapsed(group.id)}
          onToggleCollapse={(collapsed) => onToggleGroup(group.id, collapsed)}
          onFilterRemove={(filterId) => {
            const updatedFilters = group.filters.filter(f => f.id !== filterId);
            onFiltersChange(group.id, updatedFilters);
          }}
          onClearAll={() => onFiltersChange(group.id, [])}
          icon={<SafIcon name={group.icon} />}
          description={group.description}
          clearable
          showCount
        />
      ))}
    </div>
  );
};
```

### Categorized Filter Groups

```typescript
// React
const CategorizedFilterGroups = ({ 
  searchFilters,
  tableFilters,
  userFilters,
  dateFilters,
  onFilterUpdate 
}) => {
  const filterCategories = [
    {
      id: 'search',
      title: 'Search Criteria',
      filters: searchFilters,
      icon: 'search',
      variant: 'filled',
      color: 'primary'
    },
    {
      id: 'table',
      title: 'Table Filters',
      filters: tableFilters,
      icon: 'filter',
      variant: 'outline',
      color: 'secondary'
    },
    {
      id: 'users',
      title: 'User Assignments',
      filters: userFilters,
      icon: 'users',
      variant: 'filled',
      color: 'success'
    },
    {
      id: 'dates',
      title: 'Date Ranges',
      filters: dateFilters,
      icon: 'calendar',
      variant: 'outline',
      color: 'warning'
    }
  ];

  return (
    <div className="categorized-filter-groups">
      {filterCategories.map(category => (
        <SafFilterGroup
          key={category.id}
          title={category.title}
          filters={category.filters}
          variant={category.variant}
          icon={<SafIcon name={category.icon} />}
          collapsible
          collapsed={category.filters.length === 0}
          onFilterRemove={(filterId) => {
            const updatedFilters = category.filters.filter(f => f.id !== filterId);
            onFilterUpdate(category.id, updatedFilters);
          }}
          onClearAll={() => onFilterUpdate(category.id, [])}
          showCount
          clearable
          className={`filter-group-${category.color}`}
        />
      ))}
    </div>
  );
};
```

### Advanced Search Filter Groups

```typescript
// React
const AdvancedSearchFilterGroups = ({ 
  activeFilters,
  savedFilters,
  quickFilters,
  onFilterChange,
  onSaveCurrentFilters 
}) => {
  const [showAdvanced, setShowAdvanced] = useState(false);
  
  const hasActiveFilters = Object.values(activeFilters).some(group => group.length > 0);

  return (
    <div className="advanced-search-filter-groups">
      {/* Quick Filters */}
      <SafFilterGroup
        title="Quick Filters"
        filters={quickFilters}
        orientation="horizontal"
        spacing="compact"
        wrap
        maxVisible={8}
        onFilterRemove={(filterId) => {
          // Handle quick filter toggle
          const filter = quickFilters.find(f => f.id === filterId);
          onFilterChange('quick', filter, false);
        }}
        clearable={false}
        showCount={false}
        className="quick-filters-group"
      />

      {/* Advanced Filters Toggle */}
      <div className="advanced-toggle">
        <SafButton
          variant="ghost"
          onClick={() => setShowAdvanced(!showAdvanced)}
          icon={<SafIcon name={showAdvanced ? "chevron-up" : "chevron-down"} />}
        >
          Advanced Filters {hasActiveFilters && `(${Object.keys(activeFilters).length} groups active)`}
        </SafButton>
      </div>

      {/* Advanced Filter Groups */}
      {showAdvanced && (
        <div className="advanced-filter-groups">
          {Object.entries(activeFilters).map(([groupId, filters]) => (
            <SafFilterGroup
              key={groupId}
              title={groupId.charAt(0).toUpperCase() + groupId.slice(1)}
              filters={filters}
              collapsible
              collapsed={filters.length === 0}
              onFilterRemove={(filterId) => {
                onFilterChange(groupId, filterId, false);
              }}
              onClearAll={() => onFilterChange(groupId, null, 'clear')}
              clearable
              showCount
            />
          ))}

          {/* Save Current Filters */}
          {hasActiveFilters && (
            <div className="filter-actions">
              <SafButton
                variant="outline"
                size="small"
                onClick={onSaveCurrentFilters}
                icon={<SafIcon name="bookmark" />}
              >
                Save Current Filters
              </SafButton>
            </div>
          )}
        </div>
      )}

      {/* Saved Filters */}
      {savedFilters.length > 0 && (
        <SafFilterGroup
          title="Saved Filters"
          filters={savedFilters}
          variant="outline"
          collapsible
          collapsed={true}
          onFilterRemove={(filterId) => {
            // Handle saved filter deletion
            onFilterChange('saved', filterId, 'delete');
          }}
          icon={<SafIcon name="bookmark" />}
          description="Previously saved filter combinations"
          clearable
          showCount
        />
      )}
    </div>
  );
};
```

### Dashboard Filter Groups

```typescript
// React
const DashboardFilterGroups = ({ 
  dashboardFilters,
  globalFilters,
  widgetFilters,
  onGlobalFilterChange,
  onWidgetFilterChange,
  onResetFilters 
}) => {
  const [filterMode, setFilterMode] = useState('global'); // 'global' | 'widget'

  return (
    <div className="dashboard-filter-groups">
      <div className="filter-mode-selector">
        <SafRadioGroup
          value={filterMode}
          onChange={setFilterMode}
          options={[
            { value: 'global', label: 'Global Filters' },
            { value: 'widget', label: 'Widget-Specific Filters' }
          ]}
        />
      </div>

      {filterMode === 'global' && (
        <div className="global-filters">
          <SafFilterGroup
            title="Global Dashboard Filters"
            filters={globalFilters}
            variant="filled"
            icon={<SafIcon name="globe" />}
            description="Filters that apply to all dashboard widgets"
            onFilterRemove={(filterId) => {
              onGlobalFilterChange(filterId, 'remove');
            }}
            onClearAll={() => onGlobalFilterChange(null, 'clear')}
            clearable
            showCount
            size="large"
          />
        </div>
      )}

      {filterMode === 'widget' && (
        <div className="widget-filters">
          {Object.entries(widgetFilters).map(([widgetId, filters]) => (
            <SafFilterGroup
              key={widgetId}
              title={`${widgetId} Filters`}
              filters={filters}
              variant="outline"
              collapsible
              collapsed={filters.length === 0}
              onFilterRemove={(filterId) => {
                onWidgetFilterChange(widgetId, filterId, 'remove');
              }}
              onClearAll={() => onWidgetFilterChange(widgetId, null, 'clear')}
              clearable
              showCount
            />
          ))}
        </div>
      )}

      {/* Filter Actions */}
      <div className="filter-actions">
        <SafButton
          variant="outline"
          onClick={onResetFilters}
          icon={<SafIcon name="refresh" />}
        >
          Reset All Filters
        </SafButton>
      </div>
    </div>
  );
};
```

### Mobile-Optimized Filter Groups

```typescript
// React
const MobileFilterGroups = ({ 
  filterGroups,
  onFilterChange,
  showFilterPanel,
  onCloseFilterPanel 
}) => {
  const [activeGroup, setActiveGroup] = useState(null);

  const isMobile = useMediaQuery('(max-width: 768px)');

  if (isMobile) {
    return (
      <SafModal
        visible={showFilterPanel}
        onClose={onCloseFilterPanel}
        title="Filters"
        size="fullscreen"
      >
        <div className="mobile-filter-groups">
          {/* Filter Groups Accordion */}
          {filterGroups.map(group => (
            <div key={group.id} className="mobile-filter-group">
              <div 
                className="group-header"
                onClick={() => setActiveGroup(activeGroup === group.id ? null : group.id)}
              >
                <span className="group-title">
                  {group.title} {group.filters.length > 0 && `(${group.filters.length})`}
                </span>
                <SafIcon 
                  name={activeGroup === group.id ? "chevron-up" : "chevron-down"} 
                />
              </div>

              {activeGroup === group.id && (
                <SafFilterGroup
                  filters={group.filters}
                  orientation="vertical"
                  spacing="loose"
                  size="large"
                  wrap={false}
                  onFilterRemove={(filterId) => {
                    onFilterChange(group.id, filterId, 'remove');
                  }}
                  onClearAll={() => onFilterChange(group.id, null, 'clear')}
                  clearable
                  className="mobile-filter-chips"
                />
              )}
            </div>
          ))}

          {/* Mobile Filter Actions */}
          <div className="mobile-filter-actions">
            <SafButton
              variant="outline"
              size="large"
              onClick={() => {
                filterGroups.forEach(group => {
                  onFilterChange(group.id, null, 'clear');
                });
              }}
            >
              Clear All
            </SafButton>
            
            <SafButton
              variant="primary"
              size="large"
              onClick={onCloseFilterPanel}
            >
              Apply Filters
            </SafButton>
          </div>
        </div>
      </SafModal>
    );
  }

  // Desktop rendering
  return (
    <div className="desktop-filter-groups">
      {filterGroups.map(group => (
        <SafFilterGroup
          key={group.id}
          title={group.title}
          filters={group.filters}
          collapsible
          onFilterRemove={(filterId) => {
            onFilterChange(group.id, filterId, 'remove');
          }}
          onClearAll={() => onFilterChange(group.id, null, 'clear')}
          clearable
          showCount
        />
      ))}
    </div>
  );
};
```

### Batch Operations Filter Groups

```typescript
// React
const BatchOperationFilterGroups = ({ 
  filterGroups,
  selectedItems,
  onBatchOperation,
  onFilterChange 
}) => {
  const [batchMode, setBatchMode] = useState(false);
  const [selectedGroups, setSelectedGroups] = useState(new Set());

  const handleGroupSelection = (groupId, selected) => {
    const newSelection = new Set(selectedGroups);
    if (selected) {
      newSelection.add(groupId);
    } else {
      newSelection.delete(groupId);
    }
    setSelectedGroups(newSelection);
  };

  const handleBatchClear = () => {
    selectedGroups.forEach(groupId => {
      onFilterChange(groupId, null, 'clear');
    });
    setSelectedGroups(new Set());
    setBatchMode(false);
  };

  return (
    <div className="batch-operation-filter-groups">
      <div className="batch-controls">
        <SafCheckbox
          checked={batchMode}
          onChange={setBatchMode}
          label="Batch Operations"
        />
        
        {batchMode && selectedGroups.size > 0 && (
          <div className="batch-actions">
            <SafButton
              variant="outline"
              size="small"
              onClick={handleBatchClear}
              icon={<SafIcon name="trash" />}
            >
              Clear Selected ({selectedGroups.size})
            </SafButton>
          </div>
        )}
      </div>

      {filterGroups.map(group => (
        <div key={group.id} className="batch-filter-group">
          {batchMode && (
            <SafCheckbox
              checked={selectedGroups.has(group.id)}
              onChange={(selected) => handleGroupSelection(group.id, selected)}
              className="group-selector"
            />
          )}
          
          <SafFilterGroup
            title={group.title}
            filters={group.filters}
            disabled={batchMode && !selectedGroups.has(group.id)}
            onFilterRemove={(filterId) => {
              if (!batchMode) {
                onFilterChange(group.id, filterId, 'remove');
              }
            }}
            onClearAll={() => {
              if (!batchMode) {
                onFilterChange(group.id, null, 'clear');
              }
            }}
            clearable={!batchMode}
            showCount
            className={batchMode && selectedGroups.has(group.id) ? 'selected' : ''}
          />
        </div>
      ))}
    </div>
  );
};
```

### Accessible Filter Groups

```typescript
// React
const AccessibleFilterGroups = ({ 
  filterGroups, 
  onFilterChange,
  regionLabel = "Filter groups" 
}) => {
  const [announcements, setAnnouncements] = useState('');
  const [focusedGroup, setFocusedGroup] = useState(null);

  const handleFilterRemove = (groupId, filterId, filterLabel) => {
    onFilterChange(groupId, filterId, 'remove');
    
    const group = filterGroups.find(g => g.id === groupId);
    const remainingCount = group.filters.length - 1;
    
    const announcement = `Removed filter "${filterLabel}" from ${group.title}. ${remainingCount} filters remaining in group.`;
    setAnnouncements(announcement);
    
    setTimeout(() => setAnnouncements(''), 1000);
  };

  const handleGroupClear = (groupId, groupTitle) => {
    onFilterChange(groupId, null, 'clear');
    
    const announcement = `Cleared all filters from ${groupTitle}.`;
    setAnnouncements(announcement);
    
    setTimeout(() => setAnnouncements(''), 1000);
  };

  const getTotalFilterCount = () => {
    return filterGroups.reduce((total, group) => total + group.filters.length, 0);
  };

  return (
    <div 
      className="accessible-filter-groups"
      role="region"
      aria-label={regionLabel}
      aria-describedby="filter-instructions"
    >
      <div id="filter-instructions" className="sr-only">
        Use Tab to navigate between filter groups. Use Enter or Space to expand/collapse groups. Use Delete or Backspace on individual filters to remove them.
      </div>

      <div className="filter-summary" aria-live="polite">
        {getTotalFilterCount()} total filters across {filterGroups.length} groups
      </div>

      {filterGroups.map((group, index) => (
        <SafFilterGroup
          key={group.id}
          title={group.title}
          filters={group.filters}
          collapsible
          onFilterRemove={(filterId, filter) => {
            handleFilterRemove(group.id, filterId, filter.label);
          }}
          onClearAll={() => handleGroupClear(group.id, group.title)}
          onGroupFocus={() => setFocusedGroup(group.id)}
          aria-label={`${group.title} filter group. ${group.filters.length} filters. Group ${index + 1} of ${filterGroups.length}.`}
          aria-describedby={`group-help-${group.id}`}
          className={focusedGroup === group.id ? 'focused' : ''}
          clearable
          showCount
        />
      ))}

      <div 
        aria-live="assertive"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>

      {filterGroups.length === 0 && (
        <div className="no-filter-groups" aria-live="polite">
          No active filter groups
        </div>
      )}
    </div>
  );
};
```

## Best Practices

### Organization
- **Logical Grouping**: Group related filters together by category or function
- **Clear Naming**: Use descriptive group titles that indicate their purpose
- **Consistent Structure**: Maintain consistent group organization across the application
- **Priority Ordering**: Place most commonly used groups first

### Visual Design
- **Visual Hierarchy**: Use consistent visual treatment to establish hierarchy
- **Spacing**: Provide adequate spacing between groups and within groups
- **Collapse States**: Show clear indicators for expandable/collapsible groups
- **Count Display**: Show filter counts to indicate group activity

### Interaction Design
- **Easy Management**: Provide intuitive ways to clear groups and individual filters
- **Batch Operations**: Support bulk actions for managing multiple groups
- **Responsive Design**: Adapt layout for different screen sizes
- **State Management**: Maintain group states consistently

### Performance
- **Efficient Rendering**: Optimize for performance with many filter groups
- **Lazy Loading**: Load filter content on demand for large datasets
- **Memory Management**: Clean up resources when groups are removed
- **Update Optimization**: Batch filter updates to prevent excessive re-renders

## Accessibility Considerations

- Uses proper ARIA roles and attributes for group functionality
- Supports keyboard navigation including Tab and arrow keys
- Provides screen reader announcements for group state changes
- Maintains proper focus management during collapse/expand operations
- Includes descriptive labels and instructions for screen readers
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafFilterChip**: Individual filter chips within groups
- **SafButton**: Buttons for group actions and controls
- **SafCollapsible**: Base collapse functionality for groups
- **SafCheckbox**: Selection controls for batch operations

## Notes

- SafFilterGroup automatically manages internal filter state and interactions
- The component supports both controlled and uncontrolled usage patterns
- Group collapse states can be persisted across application sessions
- Responsive design ensures good experience on all device sizes
- Batch operations enable efficient management of multiple filter groups
- Accessibility features provide comprehensive keyboard and screen reader support
- Performance optimizations handle large numbers of filters efficiently
- Integration with form libraries enables complex filtering workflows
