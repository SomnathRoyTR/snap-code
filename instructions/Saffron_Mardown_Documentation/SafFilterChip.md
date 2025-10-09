# SafFilterChip

## Overview

SafFilterChip is a form component that provides removable filter tags with labels for displaying and managing active filters. It supports various visual styles, customizable content, removal interactions, and accessibility features for filter-based interfaces and search experiences.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string \| ReactNode` | - | Chip label content |
| `value` | `any` | - | Associated filter value |
| `removable` | `boolean` | `true` | Show remove button |
| `disabled` | `boolean` | `false` | Disable chip interactions |
| `selected` | `boolean` | `false` | Chip selection state |
| `variant` | `'default' \| 'outline' \| 'filled' \| 'ghost'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Chip size |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | `'primary'` | Color theme |
| `icon` | `ReactElement` | - | Leading icon |
| `avatar` | `ReactElement` | - | Avatar element |
| `removeIcon` | `ReactElement` | `<XIcon />` | Custom remove icon |
| `clickable` | `boolean` | `false` | Enable click interactions |
| `truncate` | `boolean` | `true` | Truncate long labels |
| `maxWidth` | `number \| string` | `200` | Maximum width for truncation |
| `tooltip` | `string \| ReactNode` | - | Tooltip content |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onRemove` | `(value: any) => void` | Fired when chip is removed |
| `onClick` | `(value: any, event: MouseEvent) => void` | Fired when chip is clicked |
| `onSelect` | `(selected: boolean, value: any) => void` | Fired when selection changes |
| `onFocus` | `(event: FocusEvent) => void` | Fired when chip receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when chip loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `string \| TemplateRef` | - | Chip label content |
| `value` | `any` | - | Associated filter value |
| `removable` | `boolean` | `true` | Show remove button |
| `disabled` | `boolean` | `false` | Disable chip interactions |
| `selected` | `boolean` | `false` | Chip selection state |
| `variant` | `'default' \| 'outline' \| 'filled' \| 'ghost'` | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Chip size |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | `'primary'` | Color theme |
| `clickable` | `boolean` | `false` | Enable click interactions |
| `truncate` | `boolean` | `true` | Truncate long labels |
| `maxWidth` | `number \| string` | `200` | Maximum width for truncation |
| `tooltip` | `string` | - | Tooltip content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `remove` | `EventEmitter<any>` | Fired when chip is removed |
| `chipClick` | `EventEmitter<{value: any, event: MouseEvent}>` | Fired when chip is clicked |
| `selectionChange` | `EventEmitter<{selected: boolean, value: any}>` | Fired when selection changes |
| `chipFocus` | `EventEmitter<FocusEvent>` | Fired when chip receives focus |
| `chipBlur` | `EventEmitter<FocusEvent>` | Fired when chip loses focus |

## Usage Examples

### Basic Filter Chips

```typescript
// React
const BasicFilterChips = ({ activeFilters, onFilterRemove }) => {
  return (
    <div className="filter-chips">
      {activeFilters.map(filter => (
        <SafFilterChip 
          key={filter.id}
          label={filter.label}
          value={filter.value}
          onRemove={() => onFilterRemove(filter.id)}
          removable
        />
      ))}
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="filter-chips">
  <saf-filter-chip 
    *ngFor="let filter of activeFilters"
    [label]="filter.label"
    [value]="filter.value"
    [removable]="true"
    (remove)="onFilterRemove(filter.id)">
  </saf-filter-chip>
</div>
```

### Categorized Filter Chips

```typescript
// React
const CategorizedFilterChips = ({ filterCategories, onFilterChange }) => {
  const getColorForCategory = (category) => {
    const colorMap = {
      status: 'success',
      priority: 'warning',
      type: 'primary',
      date: 'secondary'
    };
    return colorMap[category] || 'primary';
  };

  const getIconForCategory = (category) => {
    const iconMap = {
      status: 'check-circle',
      priority: 'alert-triangle',
      type: 'tag',
      date: 'calendar',
      user: 'user'
    };
    return iconMap[category] || 'filter';
  };

  return (
    <div className="categorized-filters">
      {Object.entries(filterCategories).map(([category, filters]) => (
        <div key={category} className="filter-category">
          <span className="category-label">{category}</span>
          <div className="category-chips">
            {filters.map(filter => (
              <SafFilterChip 
                key={`${category}-${filter.value}`}
                label={filter.label}
                value={filter.value}
                color={getColorForCategory(category)}
                icon={<SafIcon name={getIconForCategory(category)} />}
                onRemove={() => onFilterChange(category, filter.value, false)}
                tooltip={`Remove ${category} filter: ${filter.label}`}
              />
            ))}
          </div>
        </div>
      ))}
    </div>
  );
};
```

### Interactive Filter Chips

```typescript
// React
const InteractiveFilterChips = ({ 
  availableFilters, 
  activeFilters,
  onFilterToggle,
  onFilterRemove 
}) => {
  const isFilterActive = (filterId) => {
    return activeFilters.some(filter => filter.id === filterId);
  };

  return (
    <div className="interactive-filters">
      <div className="available-filters">
        <h4>Available Filters</h4>
        <div className="filter-options">
          {availableFilters.map(filter => (
            <SafFilterChip 
              key={filter.id}
              label={filter.label}
              value={filter.value}
              selected={isFilterActive(filter.id)}
              clickable
              removable={false}
              variant={isFilterActive(filter.id) ? 'filled' : 'outline'}
              onClick={() => onFilterToggle(filter)}
              icon={filter.icon && <SafIcon name={filter.icon} />}
            />
          ))}
        </div>
      </div>

      {activeFilters.length > 0 && (
        <div className="active-filters">
          <h4>Active Filters</h4>
          <div className="filter-chips">
            {activeFilters.map(filter => (
              <SafFilterChip 
                key={filter.id}
                label={filter.label}
                value={filter.value}
                variant="filled"
                color="primary"
                onRemove={() => onFilterRemove(filter.id)}
                icon={filter.icon && <SafIcon name={filter.icon} />}
              />
            ))}
          </div>
        </div>
      )}
    </div>
  );
};
```

### Search Result Filter Chips

```typescript
// React
const SearchResultFilterChips = ({ 
  searchQuery, 
  searchFilters, 
  resultCount,
  onQueryClear,
  onFilterClear,
  onClearAll 
}) => {
  const hasActiveFilters = searchFilters.length > 0 || searchQuery;

  return (
    <div className="search-result-filters">
      <div className="filter-header">
        <span className="result-count">
          {resultCount.toLocaleString()} results
        </span>
        
        {hasActiveFilters && (
          <SafButton 
            variant="ghost"
            size="small"
            onClick={onClearAll}
          >
            Clear all
          </SafButton>
        )}
      </div>
      
      <div className="active-filter-chips">
        {searchQuery && (
          <SafFilterChip 
            label={`Search: "${searchQuery}"`}
            value={searchQuery}
            variant="filled"
            color="primary"
            icon={<SafIcon name="search" />}
            onRemove={onQueryClear}
            maxWidth={300}
          />
        )}
        
        {searchFilters.map(filter => (
          <SafFilterChip 
            key={filter.key}
            label={`${filter.category}: ${filter.label}`}
            value={filter.value}
            variant="outline"
            color="secondary"
            onRemove={() => onFilterClear(filter.key)}
            tooltip={filter.description}
            maxWidth={250}
          />
        ))}
      </div>
    </div>
  );
};
```

### Multi-Select Filter Chips

```typescript
// React
const MultiSelectFilterChips = ({ 
  filterOptions, 
  selectedFilters,
  onSelectionChange,
  maxVisible = 5 
}) => {
  const [showAll, setShowAll] = useState(false);
  const [hoveredChip, setHoveredChip] = useState(null);

  const visibleFilters = showAll 
    ? selectedFilters 
    : selectedFilters.slice(0, maxVisible);
    
  const hiddenCount = selectedFilters.length - maxVisible;

  const handleChipToggle = (filter) => {
    const isSelected = selectedFilters.some(f => f.id === filter.id);
    const newSelection = isSelected
      ? selectedFilters.filter(f => f.id !== filter.id)
      : [...selectedFilters, filter];
    
    onSelectionChange(newSelection);
  };

  return (
    <div className="multi-select-filters">
      <div className="filter-selection">
        <span className="selection-label">Filters:</span>
        
        <div className="selected-chips">
          {visibleFilters.map(filter => (
            <SafFilterChip 
              key={filter.id}
              label={filter.label}
              value={filter.value}
              variant="filled"
              size="small"
              onRemove={() => handleChipToggle(filter)}
              onMouseEnter={() => setHoveredChip(filter.id)}
              onMouseLeave={() => setHoveredChip(null)}
              className={hoveredChip === filter.id ? 'hovered' : ''}
              icon={filter.icon && <SafIcon name={filter.icon} />}
            />
          ))}
          
          {hiddenCount > 0 && !showAll && (
            <SafFilterChip 
              label={`+${hiddenCount} more`}
              clickable
              removable={false}
              variant="ghost"
              size="small"
              onClick={() => setShowAll(true)}
            />
          )}
          
          {showAll && hiddenCount > 0 && (
            <SafFilterChip 
              label="Show less"
              clickable
              removable={false}
              variant="ghost"
              size="small"
              onClick={() => setShowAll(false)}
            />
          )}
        </div>
      </div>
      
      {selectedFilters.length > 0 && (
        <div className="selection-summary">
          <SafIcon name="info" size="small" />
          <span>{selectedFilters.length} filter{selectedFilters.length !== 1 ? 's' : ''} applied</span>
        </div>
      )}
    </div>
  );
};
```

### Avatar Filter Chips

```typescript
// React
const AvatarFilterChips = ({ 
  selectedUsers, 
  availableUsers,
  onUserRemove,
  onUserAdd 
}) => {
  const [showUserPicker, setShowUserPicker] = useState(false);

  return (
    <div className="avatar-filter-chips">
      <div className="selected-users">
        <span className="selection-label">Assigned to:</span>
        
        {selectedUsers.map(user => (
          <SafFilterChip 
            key={user.id}
            label={user.name}
            value={user.id}
            avatar={
              <SafAvatar 
                src={user.avatar}
                name={user.name}
                size="small"
              />
            }
            onRemove={() => onUserRemove(user.id)}
            tooltip={`Remove ${user.name} from filter`}
            variant="outline"
          />
        ))}
        
        <SafFilterChip 
          label="Add user"
          clickable
          removable={false}
          variant="ghost"
          icon={<SafIcon name="plus" />}
          onClick={() => setShowUserPicker(true)}
        />
      </div>
      
      {showUserPicker && (
        <SafPopover 
          visible
          onClose={() => setShowUserPicker(false)}
          content={
            <div className="user-picker">
              <h4>Select Users</h4>
              {availableUsers
                .filter(user => !selectedUsers.some(selected => selected.id === user.id))
                .map(user => (
                  <div 
                    key={user.id}
                    className="user-option"
                    onClick={() => {
                      onUserAdd(user);
                      setShowUserPicker(false);
                    }}
                  >
                    <SafAvatar 
                      src={user.avatar}
                      name={user.name}
                      size="small"
                    />
                    <span>{user.name}</span>
                  </div>
                ))}
            </div>
          }
        />
      )}
    </div>
  );
};
```

### Conditional Filter Chips

```typescript
// React
const ConditionalFilterChips = ({ 
  filters, 
  conditions,
  onFilterRemove,
  onConditionChange 
}) => {
  const getChipVariant = (condition) => {
    const variantMap = {
      'equals': 'filled',
      'not-equals': 'outline',
      'contains': 'filled',
      'greater-than': 'outline',
      'less-than': 'outline',
      'between': 'filled'
    };
    return variantMap[condition] || 'filled';
  };

  const getConditionSymbol = (condition) => {
    const symbolMap = {
      'equals': '=',
      'not-equals': '≠',
      'contains': '⊃',
      'greater-than': '>',
      'less-than': '<',
      'between': '⟷'
    };
    return symbolMap[condition] || '=';
  };

  return (
    <div className="conditional-filter-chips">
      {filters.map(filter => {
        const condition = conditions[filter.id] || 'equals';
        
        return (
          <SafFilterChip 
            key={filter.id}
            label={
              <span className="conditional-label">
                <span className="field-name">{filter.field}</span>
                <span className="condition-symbol">
                  {getConditionSymbol(condition)}
                </span>
                <span className="filter-value">{filter.value}</span>
              </span>
            }
            value={filter}
            variant={getChipVariant(condition)}
            onRemove={() => onFilterRemove(filter.id)}
            onClick={() => {
              // Cycle through conditions on click
              const conditionOrder = ['equals', 'not-equals', 'contains', 'greater-than', 'less-than'];
              const currentIndex = conditionOrder.indexOf(condition);
              const nextCondition = conditionOrder[(currentIndex + 1) % conditionOrder.length];
              onConditionChange(filter.id, nextCondition);
            }}
            clickable
            tooltip={`Click to change condition. Current: ${condition.replace('-', ' ')}`}
          />
        );
      })}
    </div>
  );
};
```

### Date Range Filter Chips

```typescript
// React
const DateRangeFilterChips = ({ 
  dateRanges, 
  customDateRanges,
  onDateRangeRemove,
  onCustomDateRemove 
}) => {
  const formatDateRange = (startDate, endDate) => {
    const formatDate = (date) => new Date(date).toLocaleDateString();
    
    if (startDate && endDate) {
      return `${formatDate(startDate)} - ${formatDate(endDate)}`;
    } else if (startDate) {
      return `After ${formatDate(startDate)}`;
    } else if (endDate) {
      return `Before ${formatDate(endDate)}`;
    }
    return 'Date range';
  };

  return (
    <div className="date-filter-chips">
      {/* Predefined date ranges */}
      {dateRanges.map(range => (
        <SafFilterChip 
          key={range.id}
          label={range.label}
          value={range.value}
          icon={<SafIcon name="calendar" />}
          color="secondary"
          onRemove={() => onDateRangeRemove(range.id)}
          tooltip={`Date range: ${range.description}`}
        />
      ))}
      
      {/* Custom date ranges */}
      {customDateRanges.map(range => (
        <SafFilterChip 
          key={range.id}
          label={formatDateRange(range.startDate, range.endDate)}
          value={range}
          icon={<SafIcon name="calendar" />}
          color="primary"
          variant="outline"
          onRemove={() => onCustomDateRemove(range.id)}
          tooltip="Custom date range"
          maxWidth={300}
        />
      ))}
    </div>
  );
};
```

### Animated Filter Chips

```typescript
// React
const AnimatedFilterChips = ({ 
  filters, 
  onFilterRemove,
  onFilterAdd 
}) => {
  const [removingChips, setRemovingChips] = useState(new Set());
  const [addingChips, setAddingChips] = useState(new Set());

  const handleRemove = (filterId) => {
    setRemovingChips(prev => new Set([...prev, filterId]));
    
    setTimeout(() => {
      onFilterRemove(filterId);
      setRemovingChips(prev => {
        const next = new Set(prev);
        next.delete(filterId);
        return next;
      });
    }, 200);
  };

  useEffect(() => {
    // Animate new chips in
    const newChips = filters.filter(filter => !addingChips.has(filter.id));
    if (newChips.length > 0) {
      const newIds = new Set([...addingChips, ...newChips.map(f => f.id)]);
      setAddingChips(newIds);
      
      setTimeout(() => {
        setAddingChips(new Set());
      }, 300);
    }
  }, [filters]);

  return (
    <div className="animated-filter-chips">
      {filters.map(filter => (
        <SafFilterChip 
          key={filter.id}
          label={filter.label}
          value={filter.value}
          onRemove={() => handleRemove(filter.id)}
          className={`
            animated-chip
            ${removingChips.has(filter.id) ? 'removing' : ''}
            ${addingChips.has(filter.id) ? 'adding' : ''}
          `}
          style={{
            animation: addingChips.has(filter.id) 
              ? 'slideInFromRight 0.3s ease-out'
              : removingChips.has(filter.id)
              ? 'slideOutToRight 0.2s ease-in'
              : 'none'
          }}
        />
      ))}
    </div>
  );
};
```

### Accessibility-Enhanced Filter Chips

```typescript
// React
const AccessibleFilterChips = ({ 
  filters, 
  onFilterRemove, 
  regionLabel = "Active filters" 
}) => {
  const [announcements, setAnnouncements] = useState('');
  const [focusedChip, setFocusedChip] = useState(null);

  const handleRemove = (filter) => {
    onFilterRemove(filter.id);
    
    const announcement = `Removed filter: ${filter.label}. ${filters.length - 1} filters remaining.`;
    setAnnouncements(announcement);
    
    setTimeout(() => setAnnouncements(''), 1000);
  };

  const handleKeyDown = (event, filter) => {
    switch (event.key) {
      case 'Delete':
      case 'Backspace':
        event.preventDefault();
        handleRemove(filter);
        break;
        
      case 'ArrowRight':
        event.preventDefault();
        // Focus next chip
        const currentIndex = filters.findIndex(f => f.id === filter.id);
        const nextIndex = (currentIndex + 1) % filters.length;
        setFocusedChip(filters[nextIndex].id);
        break;
        
      case 'ArrowLeft':
        event.preventDefault();
        // Focus previous chip
        const prevCurrentIndex = filters.findIndex(f => f.id === filter.id);
        const prevIndex = prevCurrentIndex > 0 ? prevCurrentIndex - 1 : filters.length - 1;
        setFocusedChip(filters[prevIndex].id);
        break;
    }
  };

  return (
    <div 
      className="accessible-filter-chips"
      role="region"
      aria-label={regionLabel}
    >
      <div className="filter-chips-container">
        {filters.map((filter, index) => (
          <SafFilterChip 
            key={filter.id}
            label={filter.label}
            value={filter.value}
            onRemove={() => handleRemove(filter)}
            onFocus={() => setFocusedChip(filter.id)}
            onBlur={() => setFocusedChip(null)}
            onKeyDown={(event) => handleKeyDown(event, filter)}
            aria-label={`Filter: ${filter.label}. Press Delete or Backspace to remove. ${index + 1} of ${filters.length}.`}
            aria-describedby={`filter-instructions-${filter.id}`}
            tabIndex={0}
            className={focusedChip === filter.id ? 'focused' : ''}
          />
        ))}
      </div>
      
      <div className="sr-only">
        {filters.map(filter => (
          <div key={`instructions-${filter.id}`} id={`filter-instructions-${filter.id}`}>
            Use arrow keys to navigate between filters. Press Delete or Backspace to remove this filter.
          </div>
        ))}
      </div>
      
      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>
      
      {filters.length === 0 && (
        <div className="no-filters" aria-live="polite">
          No active filters
        </div>
      )}
    </div>
  );
};
```

## Best Practices

### Visual Design
- **Consistent Styling**: Use consistent visual treatment across all filter chips
- **Color Coding**: Apply meaningful colors to indicate filter categories or states
- **Clear Labels**: Use concise, descriptive labels that clearly identify the filter
- **Visual Hierarchy**: Differentiate between active, inactive, and removable states

### Interaction Design
- **Easy Removal**: Provide clear and accessible removal methods
- **Click Feedback**: Give immediate visual feedback on interactions
- **Touch Targets**: Ensure adequate touch target size for mobile devices
- **Hover States**: Show hover effects to indicate interactivity

### Accessibility
- **Keyboard Navigation**: Support Tab, Delete, and arrow key navigation
- **Screen Reader Support**: Provide descriptive labels and removal announcements
- **Focus Management**: Maintain proper focus indicators and management
- **Role Attributes**: Use appropriate ARIA roles for filter functionality

### Performance
- **Efficient Rendering**: Optimize for performance with many filter chips
- **Animation Performance**: Use CSS animations over JavaScript where possible
- **Memory Management**: Clean up event listeners when chips are removed
- **Batch Updates**: Handle multiple filter changes efficiently

## Accessibility Considerations

- Uses proper ARIA roles and attributes for filter functionality
- Supports keyboard navigation including Delete/Backspace for removal
- Provides screen reader announcements for filter changes
- Maintains proper focus management during interactions
- Includes descriptive labels and instructions for screen readers
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafFilterGroup**: Container for organizing related filter chips
- **SafSearchField**: Search input that works with filter chips
- **SafBadge**: Basic badge component for status indicators
- **SafTooltip**: Tooltip component for additional information

## Notes

- SafFilterChip automatically handles removal animations and state management
- The component supports both controlled and uncontrolled usage patterns
- Custom content can be provided for complex filter representations
- Truncation ensures chips don't break layouts with long labels
- Color theming allows for consistent visual categorization
- The component integrates seamlessly with form libraries and state management
- Mobile optimizations ensure good touch device experience
- Accessibility features provide comprehensive keyboard and screen reader support
