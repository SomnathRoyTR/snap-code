# SafComboboxOption

## Overview

SafComboboxOption is a list item component that represents selectable options within a combobox dropdown. It provides support for text content, icons, descriptions, grouping, keyboard navigation, and accessibility features for building rich dropdown selection interfaces.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `any` | - | Option value |
| `label` | `string \| ReactNode` | - | Option label/content |
| `description` | `string \| ReactNode` | - | Optional description text |
| `selected` | `boolean` | `false` | Selection state |
| `highlighted` | `boolean` | `false` | Highlight state for keyboard navigation |
| `disabled` | `boolean` | `false` | Disable option |
| `icon` | `ReactElement` | - | Leading icon |
| `avatar` | `ReactElement` | - | Avatar element |
| `badge` | `ReactElement` | - | Trailing badge |
| `group` | `string` | - | Option group identifier |
| `sortIndex` | `number` | - | Sort order within group |
| `searchable` | `boolean` | `true` | Include in search filtering |
| `searchText` | `string` | - | Custom search text (defaults to label) |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Option size |
| `truncate` | `boolean` | `true` | Truncate long text |
| `multiline` | `boolean` | `false` | Allow multiline content |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(value: any, option: OptionData) => void` | Fired when option is clicked |
| `onSelect` | `(selected: boolean, value: any) => void` | Fired when selection changes |
| `onHover` | `(value: any, hovered: boolean) => void` | Fired when hover state changes |
| `onFocus` | `(event: FocusEvent) => void` | Fired when option receives focus |
| `onKeyDown` | `(event: KeyboardEvent) => void` | Fired on keyboard events |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `any` | - | Option value |
| `label` | `string \| TemplateRef` | - | Option label/content |
| `description` | `string \| TemplateRef` | - | Optional description text |
| `selected` | `boolean` | `false` | Selection state |
| `highlighted` | `boolean` | `false` | Highlight state for keyboard navigation |
| `disabled` | `boolean` | `false` | Disable option |
| `group` | `string` | - | Option group identifier |
| `sortIndex` | `number` | - | Sort order within group |
| `searchable` | `boolean` | `true` | Include in search filtering |
| `searchText` | `string` | - | Custom search text (defaults to label) |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Option size |
| `truncate` | `boolean` | `true` | Truncate long text |
| `multiline` | `boolean` | `false` | Allow multiline content |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `optionClick` | `EventEmitter<{value: any, option: OptionData}>` | Fired when option is clicked |
| `selectionChange` | `EventEmitter<{selected: boolean, value: any}>` | Fired when selection changes |
| `hover` | `EventEmitter<{value: any, hovered: boolean}>` | Fired when hover state changes |
| `optionFocus` | `EventEmitter<FocusEvent>` | Fired when option receives focus |
| `keydown` | `EventEmitter<KeyboardEvent>` | Fired on keyboard events |

## Usage Examples

### Basic Options

```typescript
// React
const BasicComboboxOptions = ({ options, selectedValue, onSelect }) => {
  return (
    <div className="combobox-options">
      {options.map(option => (
        <SafComboboxOption
          key={option.value}
          value={option.value}
          label={option.label}
          selected={selectedValue === option.value}
          onClick={(value) => onSelect(value)}
        />
      ))}
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="combobox-options">
  <saf-combobox-option
    *ngFor="let option of options"
    [value]="option.value"
    [label]="option.label"
    [selected]="selectedValue === option.value"
    (optionClick)="onSelect($event.value)">
  </saf-combobox-option>
</div>
```

### Rich Content Options

```typescript
// React
const RichContentOptions = ({ 
  users, 
  selectedUsers,
  onUserSelect,
  searchQuery 
}) => {
  const highlightMatch = (text, query) => {
    if (!query) return text;
    
    const regex = new RegExp(`(${query})`, 'gi');
    const parts = text.split(regex);
    
    return parts.map((part, index) => 
      regex.test(part) ? 
        <mark key={index}>{part}</mark> : 
        part
    );
  };

  return (
    <div className="rich-content-options">
      {users.map(user => (
        <SafComboboxOption
          key={user.id}
          value={user.id}
          selected={selectedUsers.includes(user.id)}
          onClick={() => onUserSelect(user.id)}
          multiline
          size="large"
          avatar={
            <SafAvatar
              src={user.avatar}
              name={user.name}
              size="medium"
              status={user.status}
            />
          }
          badge={
            user.isOnline && (
              <SafBadge
                variant="dot"
                color="success"
                label="Online"
              />
            )
          }
          label={
            <div className="user-option-content">
              <div className="user-name">
                {highlightMatch(user.name, searchQuery)}
              </div>
              <div className="user-title">
                {highlightMatch(user.title, searchQuery)}
              </div>
            </div>
          }
          description={
            <div className="user-details">
              <span className="user-department">{user.department}</span>
              <span className="user-location">{user.location}</span>
            </div>
          }
          searchText={`${user.name} ${user.title} ${user.department} ${user.email}`}
        />
      ))}
    </div>
  );
};
```

### Grouped Options

```typescript
// React
const GroupedComboboxOptions = ({ 
  optionsGroups,
  selectedValues,
  onSelectionChange 
}) => {
  const [expandedGroups, setExpandedGroups] = useState(new Set());

  const toggleGroup = (groupId) => {
    const newExpanded = new Set(expandedGroups);
    if (newExpanded.has(groupId)) {
      newExpanded.delete(groupId);
    } else {
      newExpanded.add(groupId);
    }
    setExpandedGroups(newExpanded);
  };

  return (
    <div className="grouped-combobox-options">
      {optionsGroups.map(group => (
        <div key={group.id} className="option-group">
          <div 
            className="group-header"
            onClick={() => toggleGroup(group.id)}
          >
            <SafIcon 
              name={expandedGroups.has(group.id) ? "chevron-down" : "chevron-right"} 
              size="small"
            />
            <span className="group-title">{group.title}</span>
            <SafBadge 
              label={group.options.length.toString()}
              variant="outline"
              size="small"
            />
          </div>

          {expandedGroups.has(group.id) && (
            <div className="group-options">
              {group.options.map(option => (
                <SafComboboxOption
                  key={option.value}
                  value={option.value}
                  label={option.label}
                  description={option.description}
                  icon={option.icon && <SafIcon name={option.icon} />}
                  selected={selectedValues.includes(option.value)}
                  group={group.id}
                  onClick={(value) => onSelectionChange(value)}
                  className="grouped-option"
                />
              ))}
            </div>
          )}
        </div>
      ))}
    </div>
  );
};
```

### Searchable Options with Highlighting

```typescript
// React
const SearchableComboboxOptions = ({ 
  options,
  searchQuery,
  selectedValues,
  onSelect,
  maxResults = 10 
}) => {
  const [highlightedIndex, setHighlightedIndex] = useState(-1);

  // Filter and highlight options based on search
  const filteredOptions = useMemo(() => {
    if (!searchQuery) return options.slice(0, maxResults);

    return options
      .filter(option => 
        option.searchable !== false &&
        (option.searchText || option.label)
          .toLowerCase()
          .includes(searchQuery.toLowerCase())
      )
      .slice(0, maxResults)
      .map(option => ({
        ...option,
        highlightedText: highlightSearchTerms(
          option.label, 
          searchQuery
        )
      }));
  }, [options, searchQuery, maxResults]);

  const highlightSearchTerms = (text, query) => {
    if (!query) return text;

    const regex = new RegExp(`(${escapeRegExp(query)})`, 'gi');
    const parts = text.split(regex);

    return (
      <span>
        {parts.map((part, index) => 
          regex.test(part) ? 
            <strong key={index} className="search-highlight">{part}</strong> : 
            part
        )}
      </span>
    );
  };

  const handleKeyDown = (event) => {
    switch (event.key) {
      case 'ArrowDown':
        event.preventDefault();
        setHighlightedIndex(prev => 
          prev < filteredOptions.length - 1 ? prev + 1 : 0
        );
        break;
        
      case 'ArrowUp':
        event.preventDefault();
        setHighlightedIndex(prev => 
          prev > 0 ? prev - 1 : filteredOptions.length - 1
        );
        break;
        
      case 'Enter':
        event.preventDefault();
        if (highlightedIndex >= 0) {
          const option = filteredOptions[highlightedIndex];
          onSelect(option.value);
        }
        break;
    }
  };

  useEffect(() => {
    document.addEventListener('keydown', handleKeyDown);
    return () => document.removeEventListener('keydown', handleKeyDown);
  }, [highlightedIndex, filteredOptions]);

  return (
    <div className="searchable-options">
      {filteredOptions.length === 0 && searchQuery && (
        <div className="no-results">
          <SafEmptyState
            title="No results found"
            description={`No options match "${searchQuery}"`}
            icon={<SafIcon name="search" />}
            size="small"
          />
        </div>
      )}

      {filteredOptions.map((option, index) => (
        <SafComboboxOption
          key={option.value}
          value={option.value}
          label={option.highlightedText}
          description={option.description}
          selected={selectedValues.includes(option.value)}
          highlighted={index === highlightedIndex}
          icon={option.icon && <SafIcon name={option.icon} />}
          onClick={() => onSelect(option.value)}
          onHover={(value, hovered) => {
            if (hovered) {
              setHighlightedIndex(index);
            }
          }}
          className="searchable-option"
        />
      ))}

      {filteredOptions.length === maxResults && (
        <div className="result-limit-notice">
          <SafIcon name="info" size="small" />
          <span>Showing first {maxResults} results. Refine search for more specific results.</span>
        </div>
      )}
    </div>
  );
};
```

### Multi-Select Options

```typescript
// React
const MultiSelectComboboxOptions = ({ 
  options,
  selectedValues,
  onSelectionChange,
  maxSelections 
}) => {
  const [selectAll, setSelectAll] = useState(false);

  const isSelected = (value) => selectedValues.includes(value);
  const isMaxReached = maxSelections && selectedValues.length >= maxSelections;

  const handleOptionToggle = (value) => {
    if (isSelected(value)) {
      // Deselect
      onSelectionChange(selectedValues.filter(v => v !== value));
    } else if (!isMaxReached) {
      // Select
      onSelectionChange([...selectedValues, value]);
    }
  };

  const handleSelectAll = () => {
    if (selectAll) {
      onSelectionChange([]);
    } else {
      const allValues = options
        .filter(option => !option.disabled)
        .map(option => option.value);
      onSelectionChange(allValues.slice(0, maxSelections || allValues.length));
    }
    setSelectAll(!selectAll);
  };

  const getSelectionStatus = (value) => {
    if (isSelected(value)) return 'selected';
    if (isMaxReached) return 'disabled';
    return 'available';
  };

  return (
    <div className="multi-select-options">
      {options.length > 1 && (
        <div className="select-all-option">
          <SafComboboxOption
            value="__select_all__"
            onClick={handleSelectAll}
            icon={
              <SafCheckbox
                checked={selectAll}
                indeterminate={selectedValues.length > 0 && !selectAll}
                onChange={handleSelectAll}
              />
            }
            label={`Select All${maxSelections ? ` (max ${maxSelections})` : ''}`}
            className="select-all-option"
          />
          <div className="options-divider" />
        </div>
      )}

      {options.map(option => {
        const status = getSelectionStatus(option.value);
        const isDisabled = option.disabled || status === 'disabled';

        return (
          <SafComboboxOption
            key={option.value}
            value={option.value}
            label={option.label}
            description={option.description}
            selected={status === 'selected'}
            disabled={isDisabled}
            onClick={() => !isDisabled && handleOptionToggle(option.value)}
            icon={
              <SafCheckbox
                checked={status === 'selected'}
                disabled={isDisabled}
                onChange={() => handleOptionToggle(option.value)}
              />
            }
            badge={
              status === 'disabled' && (
                <SafBadge
                  label="Max reached"
                  variant="outline"
                  color="warning"
                  size="small"
                />
              )
            }
            className={`multi-select-option ${status}`}
          />
        );
      })}

      {selectedValues.length > 0 && (
        <div className="selection-summary">
          <SafIcon name="check" size="small" />
          <span>
            {selectedValues.length} of {options.length} selected
            {maxSelections && ` (${maxSelections} max)`}
          </span>
        </div>
      )}
    </div>
  );
};
```

### Dynamic Loading Options

```typescript
// React
const DynamicLoadingOptions = ({ 
  searchQuery,
  selectedValues,
  onSelect,
  loadOptions 
}) => {
  const [options, setOptions] = useState([]);
  const [loading, setLoading] = useState(false);
  const [hasMore, setHasMore] = useState(true);
  const [page, setPage] = useState(1);

  const loadMoreOptions = useCallback(async (reset = false) => {
    if (loading) return;

    setLoading(true);
    try {
      const result = await loadOptions({
        query: searchQuery,
        page: reset ? 1 : page,
        limit: 20
      });

      setOptions(prev => reset ? result.options : [...prev, ...result.options]);
      setHasMore(result.hasMore);
      setPage(prev => reset ? 2 : prev + 1);
    } catch (error) {
      console.error('Failed to load options:', error);
    } finally {
      setLoading(false);
    }
  }, [searchQuery, page, loading, loadOptions]);

  // Reset and load when search changes
  useEffect(() => {
    setOptions([]);
    setPage(1);
    setHasMore(true);
    loadMoreOptions(true);
  }, [searchQuery]);

  return (
    <div className="dynamic-loading-options">
      {options.map(option => (
        <SafComboboxOption
          key={option.value}
          value={option.value}
          label={option.label}
          description={option.description}
          selected={selectedValues.includes(option.value)}
          icon={option.icon && <SafIcon name={option.icon} />}
          onClick={() => onSelect(option.value)}
        />
      ))}

      {loading && (
        <div className="loading-option">
          <SafLoadingSpinner size="small" />
          <span>Loading options...</span>
        </div>
      )}

      {!loading && hasMore && options.length > 0 && (
        <SafComboboxOption
          value="__load_more__"
          onClick={() => loadMoreOptions()}
          icon={<SafIcon name="chevron-down" />}
          label="Load more options"
          className="load-more-option"
        />
      )}

      {!loading && options.length === 0 && searchQuery && (
        <div className="no-results">
          <SafEmptyState
            title="No options found"
            description={`No results for "${searchQuery}"`}
            icon={<SafIcon name="search" />}
            size="small"
          />
        </div>
      )}
    </div>
  );
};
```

### Custom Rendered Options

```typescript
// React
const CustomRenderedOptions = ({ 
  products,
  selectedProduct,
  onProductSelect,
  currency = 'USD' 
}) => {
  const formatPrice = (price) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: currency
    }).format(price);
  };

  const getStockStatus = (stock) => {
    if (stock > 10) return { label: 'In Stock', color: 'success' };
    if (stock > 0) return { label: 'Low Stock', color: 'warning' };
    return { label: 'Out of Stock', color: 'error' };
  };

  return (
    <div className="custom-rendered-options">
      {products.map(product => {
        const stockStatus = getStockStatus(product.stock);
        
        return (
          <SafComboboxOption
            key={product.id}
            value={product.id}
            selected={selectedProduct === product.id}
            onClick={() => onProductSelect(product)}
            multiline
            size="large"
            disabled={product.stock === 0}
            label={
              <div className="product-option">
                <div className="product-header">
                  <div className="product-image">
                    <SafImage
                      src={product.image}
                      alt={product.name}
                      width={40}
                      height={40}
                      placeholder="product"
                    />
                  </div>
                  <div className="product-info">
                    <div className="product-name">{product.name}</div>
                    <div className="product-sku">SKU: {product.sku}</div>
                  </div>
                  <div className="product-price">
                    {formatPrice(product.price)}
                  </div>
                </div>
                
                <div className="product-details">
                  <div className="product-category">
                    <SafBadge
                      label={product.category}
                      variant="outline"
                      size="small"
                    />
                  </div>
                  <div className="product-rating">
                    {[...Array(5)].map((_, i) => (
                      <SafIcon
                        key={i}
                        name="star"
                        size="small"
                        className={i < product.rating ? 'filled' : 'empty'}
                      />
                    ))}
                    <span>({product.reviews})</span>
                  </div>
                </div>
              </div>
            }
            badge={
              <SafBadge
                label={stockStatus.label}
                color={stockStatus.color}
                variant="outline"
                size="small"
              />
            }
            className={`product-option ${product.stock === 0 ? 'out-of-stock' : ''}`}
          />
        );
      })}
    </div>
  );
};
```

### Accessible Option Navigation

```typescript
// React
const AccessibleComboboxOptions = ({ 
  options,
  selectedValue,
  highlightedIndex,
  onSelect,
  onHighlight,
  listId,
  activeDescendant 
}) => {
  const optionRefs = useRef([]);

  // Scroll highlighted option into view
  useEffect(() => {
    if (highlightedIndex >= 0 && optionRefs.current[highlightedIndex]) {
      optionRefs.current[highlightedIndex].scrollIntoView({
        block: 'nearest',
        behavior: 'smooth'
      });
    }
  }, [highlightedIndex]);

  const handleOptionFocus = (index) => {
    onHighlight(index);
  };

  const handleKeyDown = (event, index) => {
    switch (event.key) {
      case 'Enter':
      case ' ':
        event.preventDefault();
        onSelect(options[index].value);
        break;
        
      case 'ArrowDown':
        event.preventDefault();
        onHighlight(index < options.length - 1 ? index + 1 : 0);
        break;
        
      case 'ArrowUp':
        event.preventDefault();
        onHighlight(index > 0 ? index - 1 : options.length - 1);
        break;
        
      case 'Home':
        event.preventDefault();
        onHighlight(0);
        break;
        
      case 'End':
        event.preventDefault();
        onHighlight(options.length - 1);
        break;
    }
  };

  return (
    <ul
      id={listId}
      role="listbox"
      aria-label="Combobox options"
      className="accessible-combobox-options"
    >
      {options.map((option, index) => (
        <SafComboboxOption
          key={option.value}
          ref={el => optionRefs.current[index] = el}
          value={option.value}
          label={option.label}
          description={option.description}
          selected={selectedValue === option.value}
          highlighted={highlightedIndex === index}
          disabled={option.disabled}
          onClick={() => onSelect(option.value)}
          onFocus={() => handleOptionFocus(index)}
          onKeyDown={(event) => handleKeyDown(event, index)}
          role="option"
          id={`${listId}-option-${index}`}
          aria-selected={selectedValue === option.value}
          aria-describedby={option.description ? `${listId}-option-${index}-desc` : undefined}
          tabIndex={highlightedIndex === index ? 0 : -1}
          className={`accessible-option ${highlightedIndex === index ? 'highlighted' : ''}`}
        />
      ))}
      
      {options.length === 0 && (
        <li role="option" className="no-options">
          No options available
        </li>
      )}
    </ul>
  );
};
```

## Best Practices

### Content Design
- **Clear Labels**: Use descriptive labels that clearly identify the option
- **Consistent Formatting**: Maintain consistent text formatting across options
- **Meaningful Icons**: Use icons that enhance understanding, not decoration
- **Appropriate Grouping**: Group related options logically

### Interaction Design
- **Keyboard Support**: Ensure full keyboard navigation with arrow keys
- **Visual Feedback**: Provide clear hover and selection states
- **Touch Targets**: Use adequate touch target size for mobile devices
- **Loading States**: Show loading indicators for async operations

### Accessibility
- **ARIA Attributes**: Use proper ARIA roles and attributes for screen readers
- **Focus Management**: Maintain proper focus during keyboard navigation
- **Screen Reader Support**: Provide descriptive labels and announcements
- **High Contrast**: Ensure options are visible in high contrast mode

### Performance
- **Virtual Scrolling**: Implement virtual scrolling for large option lists
- **Efficient Filtering**: Optimize search filtering for performance
- **Lazy Loading**: Load options on demand for better performance
- **Memory Management**: Clean up resources when options are unmounted

## Accessibility Considerations

- Uses proper ARIA roles and attributes including `option`, `selected`, and `describedby`
- Supports full keyboard navigation with arrow keys, Enter, and Space
- Provides screen reader announcements for selection changes
- Maintains proper focus management during navigation
- Includes descriptive labels and descriptions for screen readers
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafCombobox**: Parent combobox component containing options
- **SafCheckbox**: Checkbox for multi-select options
- **SafAvatar**: Avatar elements within rich options
- **SafBadge**: Badge elements for option status or metadata

## Notes

- SafComboboxOption is typically used within SafCombobox or similar container components
- The component supports both single and multi-select scenarios
- Rich content options can include custom elements and complex layouts
- Search highlighting automatically handles text matching and emphasis
- Grouping functionality enables organized option presentation
- Virtual scrolling support handles large datasets efficiently
- Accessibility features provide comprehensive keyboard and screen reader support
- Performance optimizations ensure smooth operation with many options
