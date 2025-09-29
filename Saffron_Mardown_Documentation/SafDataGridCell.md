# SafDataGridCell

## Overview

SafDataGridCell represents an individual cell within a SafDataGrid component. It handles cell-level interactions, editing states, custom rendering, validation, and provides accessibility features for complex data presentation and manipulation scenarios.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `any` | - | Cell value |
| `column` | `DataGridColumn` | - | Column configuration |
| `row` | `object` | - | Row data object |
| `rowIndex` | `number` | - | Row index |
| `columnIndex` | `number` | - | Column index |
| `editable` | `boolean` | `false` | Enable cell editing |
| `editing` | `boolean` | `false` | Cell is in edit mode |
| `disabled` | `boolean` | `false` | Disable cell interactions |
| `selected` | `boolean` | `false` | Cell is selected |
| `focused` | `boolean` | `false` | Cell has focus |
| `invalid` | `boolean` | `false` | Cell has validation error |
| `readonly` | `boolean` | `false` | Cell is read-only |
| `align` | `'left' \| 'center' \| 'right'` | `'left'` | Text alignment |
| `wrap` | `boolean` | `false` | Enable text wrapping |
| `truncate` | `boolean` | `true` | Truncate overflowing text |
| `width` | `number \| string` | - | Cell width |
| `height` | `number \| string` | - | Cell height |
| `renderer` | `function` | - | Custom cell renderer |
| `editor` | `ReactElement \| function` | - | Custom cell editor |
| `validator` | `function` | - | Cell value validator |
| `formatter` | `function` | - | Value formatter function |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(value: any, column: DataGridColumn, row: object, event: MouseEvent) => void` | Fired when cell is clicked |
| `onDoubleClick` | `(value: any, column: DataGridColumn, row: object, event: MouseEvent) => void` | Fired when cell is double-clicked |
| `onEdit` | `(value: any, column: DataGridColumn, row: object) => void` | Fired when cell enters edit mode |
| `onChange` | `(newValue: any, oldValue: any, column: DataGridColumn, row: object) => void` | Fired when cell value changes |
| `onCommit` | `(value: any, column: DataGridColumn, row: object) => void` | Fired when edit is committed |
| `onCancel` | `(value: any, column: DataGridColumn, row: object) => void` | Fired when edit is cancelled |
| `onFocus` | `(value: any, column: DataGridColumn, row: object, event: FocusEvent) => void` | Fired when cell receives focus |
| `onBlur` | `(value: any, column: DataGridColumn, row: object, event: FocusEvent) => void` | Fired when cell loses focus |
| `onKeyDown` | `(event: KeyboardEvent, value: any, column: DataGridColumn, row: object) => void` | Fired on key press |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `any` | - | Cell value |
| `column` | `DataGridColumn` | - | Column configuration |
| `row` | `any` | - | Row data object |
| `rowIndex` | `number` | - | Row index |
| `columnIndex` | `number` | - | Column index |
| `editable` | `boolean` | `false` | Enable cell editing |
| `editing` | `boolean` | `false` | Cell is in edit mode |
| `disabled` | `boolean` | `false` | Disable cell interactions |
| `selected` | `boolean` | `false` | Cell is selected |
| `focused` | `boolean` | `false` | Cell has focus |
| `invalid` | `boolean` | `false` | Cell has validation error |
| `readonly` | `boolean` | `false` | Cell is read-only |
| `align` | `'left' \| 'center' \| 'right'` | `'left'` | Text alignment |
| `wrap` | `boolean` | `false` | Enable text wrapping |
| `truncate` | `boolean` | `true` | Truncate overflowing text |
| `width` | `number \| string` | - | Cell width |
| `height` | `number \| string` | - | Cell height |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `cellClick` | `EventEmitter<{value: any, column: DataGridColumn, row: any, event: MouseEvent}>` | Fired when cell is clicked |
| `cellDoubleClick` | `EventEmitter<{value: any, column: DataGridColumn, row: any, event: MouseEvent}>` | Fired when cell is double-clicked |
| `cellEdit` | `EventEmitter<{value: any, column: DataGridColumn, row: any}>` | Fired when cell enters edit mode |
| `cellChange` | `EventEmitter<{newValue: any, oldValue: any, column: DataGridColumn, row: any}>` | Fired when cell value changes |
| `cellCommit` | `EventEmitter<{value: any, column: DataGridColumn, row: any}>` | Fired when edit is committed |
| `cellCancel` | `EventEmitter<{value: any, column: DataGridColumn, row: any}>` | Fired when edit is cancelled |

## Usage Examples

### Basic Cell

```typescript
// React
const BasicCell = ({ value, column, row, rowIndex, columnIndex }) => (
  <SafDataGridCell 
    value={value}
    column={column}
    row={row}
    rowIndex={rowIndex}
    columnIndex={columnIndex}
    onClick={(value, column, row) => console.log('Cell clicked:', value)}
  />
);
```

```html
<!-- Angular -->
<saf-data-grid-cell 
  [value]="value"
  [column]="column"
  [row]="row"
  [rowIndex]="rowIndex"
  [columnIndex]="columnIndex"
  (cellClick)="onCellClick($event)">
</saf-data-grid-cell>
```

### Custom Rendered Cell

```typescript
// React
const CustomRenderedCell = ({ value, column, row }) => {
  const customRenderer = (value, column, row) => {
    switch (column.type) {
      case 'avatar':
        return <SafAvatar src={value} name={row.name} size="small" />;
      
      case 'status':
        return (
          <SafStatus variant={value === 'active' ? 'success' : 'error'}>
            {value}
          </SafStatus>
        );
      
      case 'currency':
        return (
          <span className="currency-cell">
            ${value.toLocaleString()}
          </span>
        );
      
      case 'date':
        return new Date(value).toLocaleDateString();
      
      case 'percentage':
        return (
          <div className="percentage-cell">
            <SafProgressRing value={value} size="small" />
            <span>{value}%</span>
          </div>
        );
      
      default:
        return value;
    }
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={customRenderer}
    />
  );
};
```

### Editable Cell

```typescript
// React
const EditableCell = ({ value, column, row, onCellChange }) => {
  const [isEditing, setIsEditing] = useState(false);
  const [editValue, setEditValue] = useState(value);

  const customEditor = (value, column, row, onChange, onCommit, onCancel) => {
    switch (column.type) {
      case 'text':
        return (
          <SafInput 
            value={editValue}
            onChange={setEditValue}
            onKeyPress={(e) => {
              if (e.key === 'Enter') {
                onChange(editValue);
                onCommit(editValue);
              } else if (e.key === 'Escape') {
                onCancel();
              }
            }}
            onBlur={() => onCommit(editValue)}
            autoFocus
          />
        );
      
      case 'select':
        return (
          <SafSelect 
            value={editValue}
            onChange={(newValue) => {
              setEditValue(newValue);
              onChange(newValue);
              onCommit(newValue);
            }}
            autoFocus
          >
            {column.options.map(option => (
              <SafOption key={option.value} value={option.value}>
                {option.label}
              </SafOption>
            ))}
          </SafSelect>
        );
      
      case 'number':
        return (
          <SafInput 
            type="number"
            value={editValue}
            onChange={setEditValue}
            onKeyPress={(e) => {
              if (e.key === 'Enter') {
                onChange(Number(editValue));
                onCommit(Number(editValue));
              }
            }}
            onBlur={() => onCommit(Number(editValue))}
            autoFocus
          />
        );
      
      default:
        return value;
    }
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      editable
      editing={isEditing}
      editor={customEditor}
      onDoubleClick={() => setIsEditing(true)}
      onCommit={(newValue) => {
        setIsEditing(false);
        onCellChange(newValue);
      }}
      onCancel={() => {
        setIsEditing(false);
        setEditValue(value);
      }}
    />
  );
};
```

### Cell with Validation

```typescript
// React
const ValidatedCell = ({ value, column, row, onCellChange }) => {
  const [error, setError] = useState(null);

  const validator = (value, column, row) => {
    switch (column.key) {
      case 'email':
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(value) ? null : 'Invalid email format';
      
      case 'age':
        const age = Number(value);
        if (isNaN(age)) return 'Age must be a number';
        if (age < 0 || age > 150) return 'Age must be between 0 and 150';
        return null;
      
      case 'required':
        return value && value.toString().trim() ? null : 'This field is required';
      
      default:
        return null;
    }
  };

  const handleChange = (newValue) => {
    const validationError = validator(newValue, column, row);
    setError(validationError);
    onCellChange(newValue, validationError);
  };

  return (
    <div className="validated-cell">
      <SafDataGridCell 
        value={value}
        column={column}
        row={row}
        editable
        invalid={!!error}
        validator={validator}
        onChange={handleChange}
      />
      {error && (
        <SafTooltip content={error}>
          <SafIcon name="error" color="error" size="small" />
        </SafTooltip>
      )}
    </div>
  );
};
```

### Action Cell

```typescript
// React
const ActionCell = ({ row, onEdit, onDelete, onView }) => {
  const actionRenderer = () => (
    <div className="action-cell">
      <SafIconButton 
        icon="eye"
        size="small"
        tooltip="View"
        onClick={() => onView(row)}
      />
      <SafIconButton 
        icon="edit"
        size="small"
        tooltip="Edit"
        onClick={() => onEdit(row)}
      />
      <SafIconButton 
        icon="delete"
        size="small"
        tooltip="Delete"
        onClick={() => onDelete(row)}
      />
    </div>
  );

  return (
    <SafDataGridCell 
      value={null}
      column={{ key: 'actions', type: 'actions' }}
      row={row}
      renderer={actionRenderer}
      align="center"
    />
  );
};
```

### Expandable Cell

```typescript
// React
const ExpandableCell = ({ value, column, row, maxLength = 100 }) => {
  const [expanded, setExpanded] = useState(false);
  
  const shouldTruncate = value && value.length > maxLength;
  const displayValue = expanded || !shouldTruncate 
    ? value 
    : `${value.substring(0, maxLength)}...`;

  const expandableRenderer = () => (
    <div className="expandable-cell">
      <span>{displayValue}</span>
      {shouldTruncate && (
        <SafButton 
          variant="text" 
          size="small"
          onClick={() => setExpanded(!expanded)}
        >
          {expanded ? 'Show Less' : 'Show More'}
        </SafButton>
      )}
    </div>
  );

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={expandableRenderer}
      wrap
    />
  );
};
```

### Link Cell

```typescript
// React
const LinkCell = ({ value, column, row }) => {
  const linkRenderer = (value, column, row) => {
    const href = column.href 
      ? typeof column.href === 'function' 
        ? column.href(value, row) 
        : column.href
      : value;

    return (
      <SafLink 
        href={href}
        target={column.external ? '_blank' : '_self'}
        onClick={(e) => {
          if (column.onClick) {
            e.preventDefault();
            column.onClick(value, row);
          }
        }}
      >
        {value}
      </SafLink>
    );
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={linkRenderer}
    />
  );
};
```

### Sortable Header Cell

```typescript
// React
const SortableHeaderCell = ({ column, sortBy, sortDirection, onSort }) => {
  const headerRenderer = () => (
    <div 
      className="sortable-header"
      onClick={() => column.sortable && onSort(column.key)}
    >
      <span>{column.title}</span>
      {column.sortable && (
        <SafIcon 
          name={
            sortBy === column.key 
              ? sortDirection === 'asc' 
                ? 'arrow-up' 
                : 'arrow-down'
              : 'unfold-more'
          }
          size="small"
          className="sort-icon"
        />
      )}
    </div>
  );

  return (
    <SafDataGridCell 
      value={column.title}
      column={column}
      row={{}}
      renderer={headerRenderer}
      className={`header-cell ${column.sortable ? 'sortable' : ''}`}
    />
  );
};
```

### Multi-Value Cell

```typescript
// React
const MultiValueCell = ({ value, column, row }) => {
  const multiValueRenderer = (values) => {
    if (!Array.isArray(values)) return values;

    return (
      <div className="multi-value-cell">
        {values.map((val, index) => (
          <SafBadge 
            key={index} 
            size="small" 
            variant="secondary"
            className="value-badge"
          >
            {val}
          </SafBadge>
        ))}
      </div>
    );
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={multiValueRenderer}
      wrap
    />
  );
};
```

### Conditional Cell

```typescript
// React
const ConditionalCell = ({ value, column, row }) => {
  const conditionalRenderer = (value, column, row) => {
    const conditions = column.conditions || [];
    
    for (const condition of conditions) {
      if (condition.test(value, row)) {
        return condition.render(value, row);
      }
    }
    
    return column.defaultRender ? column.defaultRender(value, row) : value;
  };

  // Example conditions
  const columnWithConditions = {
    ...column,
    conditions: [
      {
        test: (value, row) => row.priority === 'high',
        render: (value, row) => (
          <div className="high-priority-cell">
            <SafIcon name="priority-high" color="error" size="small" />
            <strong>{value}</strong>
          </div>
        )
      },
      {
        test: (value, row) => row.status === 'completed',
        render: (value, row) => (
          <div className="completed-cell">
            <SafIcon name="check-circle" color="success" size="small" />
            {value}
          </div>
        )
      }
    ],
    defaultRender: (value) => <span>{value}</span>
  };

  return (
    <SafDataGridCell 
      value={value}
      column={columnWithConditions}
      row={row}
      renderer={conditionalRenderer}
    />
  );
};
```

### Image Cell

```typescript
// React
const ImageCell = ({ value, column, row }) => {
  const imageRenderer = (value) => {
    if (!value) return <SafIcon name="image-placeholder" size="small" />;

    return (
      <div className="image-cell">
        <img 
          src={value}
          alt={row.name || 'Image'}
          style={{ 
            width: column.imageWidth || 40, 
            height: column.imageHeight || 40,
            objectFit: 'cover',
            borderRadius: column.rounded ? '50%' : '4px'
          }}
          onError={(e) => {
            e.target.style.display = 'none';
            e.target.nextSibling.style.display = 'block';
          }}
        />
        <SafIcon 
          name="broken-image" 
          size="small" 
          style={{ display: 'none' }}
        />
      </div>
    );
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={imageRenderer}
      align="center"
    />
  );
};
```

### Copy-to-Clipboard Cell

```typescript
// React
const CopyableCell = ({ value, column, row }) => {
  const [copied, setCopied] = useState(false);

  const copyableRenderer = (value) => (
    <div className="copyable-cell">
      <span className="cell-value">{value}</span>
      <SafIconButton 
        icon={copied ? "check" : "copy"}
        size="small"
        tooltip={copied ? "Copied!" : "Copy to clipboard"}
        onClick={async () => {
          try {
            await navigator.clipboard.writeText(value.toString());
            setCopied(true);
            setTimeout(() => setCopied(false), 2000);
          } catch (err) {
            console.error('Failed to copy:', err);
          }
        }}
      />
    </div>
  );

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={copyableRenderer}
    />
  );
};
```

### Rating Cell

```typescript
// React
const RatingCell = ({ value, column, row, onRatingChange }) => {
  const ratingRenderer = (rating) => (
    <div className="rating-cell">
      {[1, 2, 3, 4, 5].map(star => (
        <SafIconButton 
          key={star}
          icon={star <= rating ? "star" : "star-outline"}
          size="small"
          className={star <= rating ? "filled-star" : "empty-star"}
          onClick={() => column.editable && onRatingChange(star)}
        />
      ))}
      <span className="rating-value">({rating}/5)</span>
    </div>
  );

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={ratingRenderer}
      align="center"
    />
  );
};
```

### Date Range Cell

```typescript
// React
const DateRangeCell = ({ value, column, row }) => {
  const dateRangeRenderer = (dateRange) => {
    if (!dateRange || !dateRange.start || !dateRange.end) return '-';

    const startDate = new Date(dateRange.start);
    const endDate = new Date(dateRange.end);
    const now = new Date();
    
    const isActive = startDate <= now && endDate >= now;
    const isPast = endDate < now;
    const isFuture = startDate > now;

    return (
      <div className={`date-range-cell ${isActive ? 'active' : isPast ? 'past' : 'future'}`}>
        <div className="date-start">{startDate.toLocaleDateString()}</div>
        <SafIcon name="arrow-right" size="small" />
        <div className="date-end">{endDate.toLocaleDateString()}</div>
        {isActive && <SafBadge size="small" variant="success">Active</SafBadge>}
      </div>
    );
  };

  return (
    <SafDataGridCell 
      value={value}
      column={column}
      row={row}
      renderer={dateRangeRenderer}
      align="center"
    />
  );
};
```

## Best Practices

### Performance
- **Memoization**: Memoize cell components and renderers for better performance
- **Virtual Rendering**: Use efficient rendering for large datasets
- **Conditional Rendering**: Only render complex components when necessary
- **Event Optimization**: Use event delegation and avoid inline functions

### User Experience
- **Clear Visual States**: Provide distinct visual feedback for different cell states
- **Intuitive Editing**: Make editing behavior predictable and easy to use
- **Consistent Formatting**: Apply consistent formatting across similar data types
- **Loading States**: Show appropriate loading indicators for async operations

### Accessibility
- **Keyboard Navigation**: Support full keyboard navigation within cells
- **Screen Reader Support**: Provide proper ARIA labels and descriptions
- **Focus Management**: Maintain proper focus order during editing
- **High Contrast**: Ensure adequate contrast for all cell states

### Data Handling
- **Type Safety**: Validate and handle different data types appropriately
- **Error Handling**: Handle validation errors gracefully
- **State Management**: Keep cell state minimal and predictable
- **Performance**: Optimize rendering for large datasets

## Accessibility Considerations

- Uses proper table cell semantics with ARIA attributes
- Supports keyboard navigation including Tab, Enter, Escape, and arrow keys
- Provides screen reader announcements for editing state changes
- Maintains focus within cells during editing operations
- Supports high contrast mode and respects reduced motion preferences
- Includes proper ARIA labels for interactive elements within cells

## Related Components

- **SafDataGrid**: Parent data grid component
- **SafDataGridRow**: Parent row component  
- **SafTable**: Basic table component
- **SafTableCell**: Basic table cell component
- **SafInput**: Input component for cell editing
- **SafSelect**: Select component for dropdown cells

## Notes

- SafDataGridCell automatically handles focus management during editing
- Custom renderers receive full context including value, column, and row data
- Cell validation occurs in real-time and on commit
- The component supports both controlled and uncontrolled editing modes
- Event handlers are optimized to prevent unnecessary re-renders
- Custom editors can be provided for complex data types
- The component integrates with keyboard navigation patterns
- Cell content can be formatted using built-in or custom formatters
