# SafDataGridRow

## Overview

SafDataGridRow represents an individual row within a SafDataGrid component. It handles row-level interactions, selection states, expansion behavior, and provides customizable rendering options for complex data table scenarios with accessibility and performance optimizations.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `object` | - | Row data object |
| `columns` | `DataGridColumn[]` | `[]` | Column configuration array |
| `index` | `number` | - | Row index in the dataset |
| `selected` | `boolean` | `false` | Whether row is selected |
| `expanded` | `boolean` | `false` | Whether row is expanded |
| `selectable` | `boolean` | `false` | Enable row selection |
| `expandable` | `boolean` | `false` | Enable row expansion |
| `disabled` | `boolean` | `false` | Disable row interactions |
| `highlighted` | `boolean` | `false` | Highlight row (e.g., search match) |
| `striped` | `boolean` | `false` | Alternating row color |
| `dense` | `boolean` | `false` | Compact row spacing |
| `height` | `number` | `48` | Fixed row height |
| `hover` | `boolean` | `true` | Enable hover effects |
| `clickable` | `boolean` | `true` | Enable click interactions |
| `rowKey` | `string \| function` | `'id'` | Unique row identifier |
| `cellRenderer` | `function` | - | Custom cell renderer |
| `expandedContent` | `ReactElement \| function` | - | Content for expanded row |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(row: object, index: number, event: MouseEvent) => void` | Fired when row is clicked |
| `onDoubleClick` | `(row: object, index: number, event: MouseEvent) => void` | Fired when row is double-clicked |
| `onSelect` | `(selected: boolean, row: object, index: number) => void` | Fired when row selection changes |
| `onExpand` | `(expanded: boolean, row: object, index: number) => void` | Fired when row expansion changes |
| `onMouseEnter` | `(row: object, index: number, event: MouseEvent) => void` | Fired when mouse enters row |
| `onMouseLeave` | `(row: object, index: number, event: MouseEvent) => void` | Fired when mouse leaves row |
| `onContextMenu` | `(row: object, index: number, event: MouseEvent) => void` | Fired on right-click |
| `onKeyDown` | `(row: object, index: number, event: KeyboardEvent) => void` | Fired on key press |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `any` | - | Row data object |
| `columns` | `DataGridColumn[]` | `[]` | Column configuration array |
| `index` | `number` | - | Row index in the dataset |
| `selected` | `boolean` | `false` | Whether row is selected |
| `expanded` | `boolean` | `false` | Whether row is expanded |
| `selectable` | `boolean` | `false` | Enable row selection |
| `expandable` | `boolean` | `false` | Enable row expansion |
| `disabled` | `boolean` | `false` | Disable row interactions |
| `highlighted` | `boolean` | `false` | Highlight row |
| `striped` | `boolean` | `false` | Alternating row color |
| `dense` | `boolean` | `false` | Compact row spacing |
| `height` | `number` | `48` | Fixed row height |
| `hover` | `boolean` | `true` | Enable hover effects |
| `clickable` | `boolean` | `true` | Enable click interactions |
| `rowKey` | `string` | `'id'` | Unique row identifier |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `rowClick` | `EventEmitter<{row: any, index: number, event: MouseEvent}>` | Fired when row is clicked |
| `rowDoubleClick` | `EventEmitter<{row: any, index: number, event: MouseEvent}>` | Fired when row is double-clicked |
| `rowSelect` | `EventEmitter<{selected: boolean, row: any, index: number}>` | Fired when row selection changes |
| `rowExpand` | `EventEmitter<{expanded: boolean, row: any, index: number}>` | Fired when row expansion changes |
| `rowMouseEnter` | `EventEmitter<{row: any, index: number, event: MouseEvent}>` | Fired when mouse enters row |
| `rowContextMenu` | `EventEmitter<{row: any, index: number, event: MouseEvent}>` | Fired on right-click |

## Usage Examples

### Basic Data Grid Row

```typescript
// React
const BasicRow = ({ rowData, columns, index }) => (
  <SafDataGridRow 
    data={rowData}
    columns={columns}
    index={index}
    onClick={(row, index) => console.log('Clicked row:', row)}
  />
);
```

```html
<!-- Angular -->
<saf-data-grid-row 
  [data]="rowData"
  [columns]="columns"
  [index]="index"
  (rowClick)="onRowClick($event)">
</saf-data-grid-row>
```

### Selectable Row

```typescript
// React
const SelectableRow = ({ rowData, columns, index, selected, onSelectionChange }) => (
  <SafDataGridRow 
    data={rowData}
    columns={columns}
    index={index}
    selectable
    selected={selected}
    onSelect={(selected, row, index) => onSelectionChange(row.id, selected)}
  />
);
```

### Expandable Row

```typescript
// React
const ExpandableRow = ({ rowData, columns, index, expanded, onExpandChange }) => (
  <SafDataGridRow 
    data={rowData}
    columns={columns}
    index={index}
    expandable
    expanded={expanded}
    onExpand={(expanded, row) => onExpandChange(row.id, expanded)}
    expandedContent={
      <div className="expanded-row-content">
        <h4>Additional Details</h4>
        <p>Description: {rowData.description}</p>
        <p>Created: {new Date(rowData.createdAt).toLocaleDateString()}</p>
        <p>Modified: {new Date(rowData.modifiedAt).toLocaleDateString()}</p>
      </div>
    }
  />
);
```

### Custom Cell Renderer

```typescript
// React
const customCellRenderer = (value, column, row, index) => {
  switch (column.key) {
    case 'avatar':
      return <SafAvatar src={value} name={row.name} size="small" />;
    
    case 'status':
      return (
        <SafStatus variant={value === 'active' ? 'success' : 'error'}>
          {value}
        </SafStatus>
      );
    
    case 'actions':
      return (
        <div className="row-actions">
          <SafIconButton 
            icon="edit" 
            size="small"
            onClick={() => editRow(row)}
          />
          <SafIconButton 
            icon="delete" 
            size="small"
            onClick={() => deleteRow(row)}
          />
        </div>
      );
    
    default:
      return value;
  }
};

const CustomRow = ({ rowData, columns, index }) => (
  <SafDataGridRow 
    data={rowData}
    columns={columns}
    index={index}
    cellRenderer={customCellRenderer}
  />
);
```

### Row with Context Menu

```typescript
// React
const RowWithContextMenu = ({ rowData, columns, index }) => {
  const [contextMenuOpen, setContextMenuOpen] = useState(false);
  const [contextMenuPosition, setContextMenuPosition] = useState({ x: 0, y: 0 });

  const handleContextMenu = (row, index, event) => {
    event.preventDefault();
    setContextMenuPosition({ x: event.clientX, y: event.clientY });
    setContextMenuOpen(true);
  };

  return (
    <>
      <SafDataGridRow 
        data={rowData}
        columns={columns}
        index={index}
        onContextMenu={handleContextMenu}
      />
      
      <SafContextMenu 
        open={contextMenuOpen}
        onClose={() => setContextMenuOpen(false)}
        position={contextMenuPosition}
      >
        <SafContextMenuItem 
          icon="edit"
          onClick={() => editRow(rowData)}
        >
          Edit
        </SafContextMenuItem>
        <SafContextMenuItem 
          icon="copy"
          onClick={() => copyRow(rowData)}
        >
          Duplicate
        </SafContextMenuItem>
        <SafContextMenuDivider />
        <SafContextMenuItem 
          icon="delete"
          onClick={() => deleteRow(rowData)}
          destructive
        >
          Delete
        </SafContextMenuItem>
      </SafContextMenu>
    </>
  );
};
```

### Highlighted Search Row

```typescript
// React
const SearchHighlightRow = ({ rowData, columns, index, searchTerm }) => {
  const isHighlighted = searchTerm && 
    Object.values(rowData).some(value => 
      String(value).toLowerCase().includes(searchTerm.toLowerCase())
    );

  const highlightCellRenderer = (value, column, row) => {
    if (!searchTerm || typeof value !== 'string') return value;
    
    const regex = new RegExp(`(${searchTerm})`, 'gi');
    const parts = value.split(regex);
    
    return parts.map((part, index) => 
      regex.test(part) ? 
        <mark key={index} className="search-highlight">{part}</mark> : 
        part
    );
  };

  return (
    <SafDataGridRow 
      data={rowData}
      columns={columns}
      index={index}
      highlighted={isHighlighted}
      cellRenderer={highlightCellRenderer}
    />
  );
};
```

### Row with Loading State

```typescript
// React
const LoadingRow = ({ columns, index }) => (
  <SafDataGridRow 
    data={{}}
    columns={columns}
    index={index}
    disabled
    cellRenderer={(value, column) => (
      <SafSkeleton 
        variant="text" 
        width={column.width ? `${column.width - 20}px` : '80%'} 
        height="20px"
      />
    )}
  />
);
```

### Editable Row

```typescript
// React
const EditableRow = ({ rowData, columns, index, editingRow, onSave, onCancel }) => {
  const [editedData, setEditedData] = useState(rowData);
  const isEditing = editingRow === rowData.id;

  const editableCellRenderer = (value, column, row) => {
    if (!isEditing) return value;

    switch (column.type) {
      case 'text':
        return (
          <SafInput 
            value={editedData[column.key]}
            onChange={(value) => setEditedData({...editedData, [column.key]: value})}
            size="small"
          />
        );
      
      case 'select':
        return (
          <SafSelect 
            value={editedData[column.key]}
            onChange={(value) => setEditedData({...editedData, [column.key]: value})}
            size="small"
          >
            {column.options.map(option => (
              <SafOption key={option.value} value={option.value}>
                {option.label}
              </SafOption>
            ))}
          </SafSelect>
        );
      
      case 'actions':
        return (
          <div className="edit-actions">
            <SafIconButton 
              icon="check" 
              size="small"
              onClick={() => onSave(editedData)}
            />
            <SafIconButton 
              icon="close" 
              size="small"
              onClick={() => onCancel()}
            />
          </div>
        );
      
      default:
        return value;
    }
  };

  return (
    <SafDataGridRow 
      data={isEditing ? editedData : rowData}
      columns={columns}
      index={index}
      cellRenderer={editableCellRenderer}
      className={isEditing ? 'editing-row' : ''}
    />
  );
};
```

### Row with Drag and Drop

```typescript
// React
const DraggableRow = ({ rowData, columns, index, onDragStart, onDragEnd }) => {
  const [isDragging, setIsDragging] = useState(false);

  const handleDragStart = (event) => {
    setIsDragging(true);
    event.dataTransfer.setData('text/plain', JSON.stringify(rowData));
    onDragStart?.(rowData, index);
  };

  const handleDragEnd = () => {
    setIsDragging(false);
    onDragEnd?.(rowData, index);
  };

  return (
    <SafDataGridRow 
      data={rowData}
      columns={columns}
      index={index}
      draggable
      onDragStart={handleDragStart}
      onDragEnd={handleDragEnd}
      className={isDragging ? 'dragging-row' : ''}
      style={{
        opacity: isDragging ? 0.5 : 1,
        cursor: 'move'
      }}
    />
  );
};
```

### Master-Detail Row

```typescript
// React
const MasterDetailRow = ({ rowData, columns, index, detailTemplate }) => {
  const [expanded, setExpanded] = useState(false);

  const masterColumns = [
    {
      key: 'expand',
      title: '',
      width: 50,
      render: () => (
        <SafIconButton 
          icon={expanded ? 'expand-less' : 'expand-more'}
          size="small"
          onClick={() => setExpanded(!expanded)}
        />
      )
    },
    ...columns
  ];

  return (
    <SafDataGridRow 
      data={rowData}
      columns={masterColumns}
      index={index}
      expanded={expanded}
      expandedContent={
        <div className="detail-content">
          {detailTemplate(rowData)}
        </div>
      }
    />
  );
};
```

### Conditional Row Styling

```typescript
// React
const ConditionalStyledRow = ({ rowData, columns, index }) => {
  const getRowClassName = (row) => {
    const classes = [];
    
    if (row.priority === 'high') classes.push('high-priority-row');
    if (row.status === 'error') classes.push('error-row');
    if (row.isNew) classes.push('new-row');
    if (row.expires && new Date(row.expires) < new Date()) classes.push('expired-row');
    
    return classes.join(' ');
  };

  const getRowStyle = (row) => {
    const style = {};
    
    if (row.category === 'urgent') {
      style.borderLeft = '4px solid #ff4444';
    }
    
    if (row.confidence < 0.5) {
      style.backgroundColor = 'rgba(255, 193, 7, 0.1)';
    }
    
    return style;
  };

  return (
    <SafDataGridRow 
      data={rowData}
      columns={columns}
      index={index}
      className={getRowClassName(rowData)}
      style={getRowStyle(rowData)}
    />
  );
};
```

### Row with Inline Actions

```typescript
// React
const RowWithInlineActions = ({ rowData, columns, index, permissions }) => {
  const [showActions, setShowActions] = useState(false);

  const actionsColumn = {
    key: 'actions',
    title: 'Actions',
    width: 120,
    render: (value, row) => (
      <div 
        className={`inline-actions ${showActions ? 'visible' : ''}`}
        style={{ opacity: showActions ? 1 : 0 }}
      >
        {permissions.canEdit && (
          <SafIconButton 
            icon="edit" 
            size="small"
            tooltip="Edit"
            onClick={() => editRow(row)}
          />
        )}
        {permissions.canDelete && (
          <SafIconButton 
            icon="delete" 
            size="small"
            tooltip="Delete"
            onClick={() => deleteRow(row)}
          />
        )}
        {permissions.canView && (
          <SafIconButton 
            icon="eye" 
            size="small"
            tooltip="View Details"
            onClick={() => viewRow(row)}
          />
        )}
      </div>
    )
  };

  const enhancedColumns = [...columns, actionsColumn];

  return (
    <SafDataGridRow 
      data={rowData}
      columns={enhancedColumns}
      index={index}
      onMouseEnter={() => setShowActions(true)}
      onMouseLeave={() => setShowActions(false)}
    />
  );
};
```

### Row with Progress Indicator

```typescript
// React
const ProgressRow = ({ rowData, columns, index }) => {
  const progressColumns = columns.map(col => {
    if (col.key === 'progress') {
      return {
        ...col,
        render: (value) => (
          <div className="progress-cell">
            <SafProgressRing 
              value={value} 
              size="small" 
              showValue={false}
            />
            <span className="progress-text">{value}%</span>
          </div>
        )
      };
    }
    return col;
  });

  const getProgressRowStyle = (row) => {
    if (row.progress === 100) {
      return { backgroundColor: 'rgba(76, 175, 80, 0.1)' };
    }
    if (row.progress < 25) {
      return { backgroundColor: 'rgba(244, 67, 54, 0.1)' };
    }
    return {};
  };

  return (
    <SafDataGridRow 
      data={rowData}
      columns={progressColumns}
      index={index}
      style={getProgressRowStyle(rowData)}
    />
  );
};
```

### Grouped Row Header

```typescript
// React
const GroupedRowHeader = ({ group, columns, expanded, onToggle }) => {
  const headerColumns = [
    {
      key: 'group',
      title: 'Group',
      render: () => (
        <div className="group-header">
          <SafIconButton 
            icon={expanded ? 'expand-less' : 'expand-more'}
            size="small"
            onClick={onToggle}
          />
          <strong>{group.name}</strong>
          <SafBadge size="small">{group.count}</SafBadge>
        </div>
      )
    }
  ];

  return (
    <SafDataGridRow 
      data={{}}
      columns={headerColumns}
      index={-1}
      className="group-header-row"
      style={{
        backgroundColor: 'var(--saf-color-neutral-50)',
        fontWeight: 'bold'
      }}
    />
  );
};
```

## Best Practices

### Performance
- **Memoization**: Memoize row components when data doesn't change frequently
- **Virtual Rendering**: Use virtual scrolling for large datasets
- **Efficient Updates**: Update only changed rows rather than re-rendering all rows
- **Event Delegation**: Use event delegation for better performance with many rows

### User Experience
- **Visual Feedback**: Provide clear hover, selection, and interaction states
- **Loading States**: Show appropriate loading indicators for async operations
- **Error Handling**: Display error states clearly within rows
- **Responsive Design**: Adapt row layout for different screen sizes

### Accessibility
- **Keyboard Navigation**: Support full keyboard navigation between rows
- **Screen Readers**: Provide proper ARIA labels and descriptions
- **Focus Management**: Maintain logical focus order
- **High Contrast**: Ensure proper contrast ratios for all row states

### Data Management
- **Unique Keys**: Always provide unique row identifiers
- **Immutable Updates**: Use immutable data patterns for better performance
- **State Management**: Keep row state minimal and derived when possible
- **Event Handling**: Handle events efficiently without causing unnecessary re-renders

## Accessibility Considerations

- Uses proper table row semantics with ARIA attributes
- Supports keyboard navigation with Tab, Enter, Space, and arrow keys
- Provides screen reader announcements for selection and expansion changes
- Maintains focus within rows and proper focus order
- Supports high contrast mode and respects reduced motion preferences
- Includes proper ARIA labels for interactive elements within rows

## Related Components

- **SafDataGrid**: Parent data grid component
- **SafDataGridCell**: Individual cell component
- **SafTable**: Basic table component
- **SafTableRow**: Basic table row component
- **SafCheckbox**: Row selection component
- **SafIconButton**: Action buttons within rows

## Notes

- SafDataGridRow automatically handles virtualization when used within SafDataGrid
- Row selection state is managed through the parent DataGrid component
- Custom cell renderers receive row context for dynamic rendering
- The component supports both fixed and dynamic row heights
- Event handlers are optimized to prevent unnecessary re-renders
- Row expansion content can be lazy-loaded for performance
- The component integrates with keyboard navigation patterns
- Custom styling can be applied through className and style props
