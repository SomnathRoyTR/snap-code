# SafDataGrid

## Overview

SafDataGrid is a powerful and flexible data table component that provides advanced features for displaying, sorting, filtering, and manipulating large datasets. It supports virtual scrolling, row selection, column customization, inline editing, and comprehensive accessibility features for complex data presentation needs.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `object[]` | `[]` | Array of row data objects |
| `columns` | `DataGridColumn[]` | `[]` | Column configuration array |
| `loading` | `boolean` | `false` | Shows loading state |
| `loadingRows` | `number` | `5` | Number of skeleton rows when loading |
| `selectable` | `boolean \| 'single' \| 'multiple'` | `false` | Enable row selection |
| `selectedRows` | `string[] \| string` | - | Selected row keys (controlled) |
| `defaultSelectedRows` | `string[] \| string` | - | Default selected rows (uncontrolled) |
| `sortable` | `boolean` | `true` | Enable column sorting |
| `sortBy` | `string` | - | Current sort column key |
| `sortDirection` | `'asc' \| 'desc'` | `'asc'` | Current sort direction |
| `filterable` | `boolean` | `true` | Enable column filtering |
| `filters` | `object` | - | Current filter values |
| `pagination` | `boolean \| object` | `false` | Enable pagination or config |
| `pageSize` | `number` | `25` | Rows per page |
| `currentPage` | `number` | `1` | Current page number |
| `totalRows` | `number` | - | Total rows count for server-side pagination |
| `virtualScrolling` | `boolean` | `false` | Enable virtual scrolling for performance |
| `rowHeight` | `number` | `48` | Fixed row height for virtual scrolling |
| `height` | `number \| string` | `400` | Grid height |
| `width` | `number \| string` | `'100%'` | Grid width |
| `resizable` | `boolean` | `true` | Enable column resizing |
| `reorderable` | `boolean` | `false` | Enable column reordering |
| `expandable` | `boolean` | `false` | Enable row expansion |
| `expandedRows` | `string[]` | `[]` | Expanded row keys |
| `stickyHeader` | `boolean` | `true` | Sticky table header |
| `stickyColumns` | `number` | `0` | Number of sticky columns from left |
| `bordered` | `boolean` | `true` | Show table borders |
| `striped` | `boolean` | `false` | Alternating row colors |
| `dense` | `boolean` | `false` | Compact row spacing |
| `rowKey` | `string \| function` | `'id'` | Unique row identifier |
| `emptyMessage` | `string \| ReactElement` | `'No data available'` | Empty state message |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### DataGridColumn Interface

```typescript
interface DataGridColumn {
  key: string;
  title: string;
  dataIndex?: string;
  width?: number | string;
  minWidth?: number;
  maxWidth?: number;
  resizable?: boolean;
  sortable?: boolean;
  filterable?: boolean;
  filterType?: 'text' | 'select' | 'date' | 'number';
  filterOptions?: string[] | object[];
  align?: 'left' | 'center' | 'right';
  fixed?: 'left' | 'right';
  render?: (value: any, row: object, index: number) => ReactNode;
  headerRender?: () => ReactNode;
  cellClassName?: string | ((value: any, row: object) => string);
  cellStyle?: object | ((value: any, row: object) => object);
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onSelectionChange` | `(selection: string[] \| string) => void` | Fired when row selection changes |
| `onSortChange` | `(sortBy: string, direction: 'asc' \| 'desc') => void` | Fired when sort changes |
| `onFilterChange` | `(filters: object) => void` | Fired when filters change |
| `onPageChange` | `(page: number) => void` | Fired when page changes |
| `onPageSizeChange` | `(pageSize: number) => void` | Fired when page size changes |
| `onRowClick` | `(row: object, index: number) => void` | Fired when row is clicked |
| `onRowDoubleClick` | `(row: object, index: number) => void` | Fired when row is double-clicked |
| `onCellClick` | `(value: any, row: object, column: DataGridColumn) => void` | Fired when cell is clicked |
| `onColumnResize` | `(columnKey: string, width: number) => void` | Fired when column is resized |
| `onColumnReorder` | `(columns: DataGridColumn[]) => void` | Fired when columns are reordered |
| `onExpandedRowsChange` | `(expandedRows: string[]) => void` | Fired when row expansion changes |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `any[]` | `[]` | Array of row data objects |
| `columns` | `DataGridColumn[]` | `[]` | Column configuration array |
| `loading` | `boolean` | `false` | Shows loading state |
| `loadingRows` | `number` | `5` | Number of skeleton rows when loading |
| `selectable` | `boolean \| 'single' \| 'multiple'` | `false` | Enable row selection |
| `selectedRows` | `string[] \| string` | - | Selected row keys |
| `sortable` | `boolean` | `true` | Enable column sorting |
| `sortBy` | `string` | - | Current sort column key |
| `sortDirection` | `'asc' \| 'desc'` | `'asc'` | Current sort direction |
| `filterable` | `boolean` | `true` | Enable column filtering |
| `filters` | `object` | - | Current filter values |
| `pagination` | `boolean \| object` | `false` | Enable pagination or config |
| `pageSize` | `number` | `25` | Rows per page |
| `currentPage` | `number` | `1` | Current page number |
| `totalRows` | `number` | - | Total rows count |
| `virtualScrolling` | `boolean` | `false` | Enable virtual scrolling |
| `rowHeight` | `number` | `48` | Fixed row height |
| `height` | `number \| string` | `400` | Grid height |
| `resizable` | `boolean` | `true` | Enable column resizing |
| `reorderable` | `boolean` | `false` | Enable column reordering |
| `expandable` | `boolean` | `false` | Enable row expansion |
| `stickyHeader` | `boolean` | `true` | Sticky table header |
| `bordered` | `boolean` | `true` | Show table borders |
| `striped` | `boolean` | `false` | Alternating row colors |
| `dense` | `boolean` | `false` | Compact row spacing |
| `rowKey` | `string` | `'id'` | Unique row identifier |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `selectionChange` | `EventEmitter<string[] \| string>` | Fired when row selection changes |
| `sortChange` | `EventEmitter<{sortBy: string, direction: string}>` | Fired when sort changes |
| `filterChange` | `EventEmitter<object>` | Fired when filters change |
| `pageChange` | `EventEmitter<number>` | Fired when page changes |
| `pageSizeChange` | `EventEmitter<number>` | Fired when page size changes |
| `rowClick` | `EventEmitter<{row: any, index: number}>` | Fired when row is clicked |
| `cellClick` | `EventEmitter<{value: any, row: any, column: DataGridColumn}>` | Fired when cell is clicked |
| `columnResize` | `EventEmitter<{columnKey: string, width: number}>` | Fired when column is resized |

## Usage Examples

### Basic Data Grid

```typescript
// React
const columns = [
  { key: 'id', title: 'ID', width: 80 },
  { key: 'name', title: 'Name', width: 200 },
  { key: 'email', title: 'Email', width: 250 },
  { key: 'role', title: 'Role', width: 120 },
  { key: 'status', title: 'Status', width: 100 }
];

const data = [
  { id: 1, name: 'John Doe', email: 'john@example.com', role: 'Admin', status: 'Active' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com', role: 'User', status: 'Active' },
  { id: 3, name: 'Bob Johnson', email: 'bob@example.com', role: 'Editor', status: 'Inactive' }
];

<SafDataGrid 
  data={data}
  columns={columns}
  height={400}
/>
```

```html
<!-- Angular -->
<saf-data-grid 
  [data]="data"
  [columns]="columns"
  [height]="400">
</saf-data-grid>
```

### Data Grid with Selection

```typescript
// React
const [selectedRows, setSelectedRows] = useState([]);

<SafDataGrid 
  data={data}
  columns={columns}
  selectable="multiple"
  selectedRows={selectedRows}
  onSelectionChange={setSelectedRows}
  onRowClick={(row) => console.log('Clicked row:', row)}
/>
```

### Data Grid with Custom Columns

```typescript
// React
const customColumns = [
  { 
    key: 'avatar', 
    title: 'Avatar', 
    width: 80,
    render: (value, row) => (
      <SafAvatar src={row.avatar} name={row.name} size="small" />
    )
  },
  { key: 'name', title: 'Name', width: 200, sortable: true },
  { key: 'email', title: 'Email', width: 250, filterable: true },
  {
    key: 'role',
    title: 'Role',
    width: 120,
    filterType: 'select',
    filterOptions: ['Admin', 'User', 'Editor'],
    render: (value) => (
      <SafBadge variant={value === 'Admin' ? 'primary' : 'secondary'}>
        {value}
      </SafBadge>
    )
  },
  {
    key: 'status',
    title: 'Status',
    width: 100,
    align: 'center',
    render: (value) => (
      <SafStatus variant={value === 'Active' ? 'success' : 'error'}>
        {value}
      </SafStatus>
    )
  },
  {
    key: 'actions',
    title: 'Actions',
    width: 120,
    render: (value, row) => (
      <div className="action-buttons">
        <SafIconButton 
          icon="edit" 
          size="small"
          onClick={() => editUser(row.id)}
        />
        <SafIconButton 
          icon="delete" 
          size="small"
          onClick={() => deleteUser(row.id)}
        />
      </div>
    )
  }
];

<SafDataGrid 
  data={userData}
  columns={customColumns}
  sortable
  filterable
  pagination
  pageSize={10}
/>
```

### Data Grid with Pagination

```typescript
// React
const [currentPage, setCurrentPage] = useState(1);
const [pageSize, setPageSize] = useState(25);

<SafDataGrid 
  data={data}
  columns={columns}
  pagination={{
    showSizeChanger: true,
    showQuickJumper: true,
    showTotal: (total, range) => 
      `${range[0]}-${range[1]} of ${total} items`
  }}
  currentPage={currentPage}
  pageSize={pageSize}
  totalRows={data.length}
  onPageChange={setCurrentPage}
  onPageSizeChange={setPageSize}
/>
```

### Virtual Scrolling Data Grid

```typescript
// React
const largeDataset = Array.from({ length: 10000 }, (_, index) => ({
  id: index + 1,
  name: `User ${index + 1}`,
  email: `user${index + 1}@example.com`,
  department: departments[index % departments.length],
  salary: Math.floor(Math.random() * 100000) + 30000
}));

<SafDataGrid 
  data={largeDataset}
  columns={columns}
  virtualScrolling
  height={500}
  rowHeight={48}
/>
```

### Expandable Rows Data Grid

```typescript
// React
const [expandedRows, setExpandedRows] = useState([]);

const expandableColumns = [
  { key: 'orderId', title: 'Order ID', width: 120 },
  { key: 'customer', title: 'Customer', width: 200 },
  { key: 'total', title: 'Total', width: 120, render: (value) => `$${value}` },
  { key: 'status', title: 'Status', width: 120 },
  {
    key: 'expand',
    title: '',
    width: 50,
    render: (value, row) => (
      <SafIconButton 
        icon={expandedRows.includes(row.orderId) ? 'expand-less' : 'expand-more'}
        size="small"
        onClick={() => toggleRowExpansion(row.orderId)}
      />
    )
  }
];

const expandedRowRender = (row) => (
  <div className="expanded-content">
    <h4>Order Items</h4>
    <SafTable size="small">
      <SafTableHead>
        <SafTableRow>
          <SafTableHeaderCell>Product</SafTableHeaderCell>
          <SafTableHeaderCell>Quantity</SafTableHeaderCell>
          <SafTableHeaderCell>Price</SafTableHeaderCell>
        </SafTableRow>
      </SafTableHead>
      <SafTableBody>
        {row.items.map(item => (
          <SafTableRow key={item.productId}>
            <SafTableCell>{item.name}</SafTableCell>
            <SafTableCell>{item.quantity}</SafTableCell>
            <SafTableCell>${item.price}</SafTableCell>
          </SafTableRow>
        ))}
      </SafTableBody>
    </SafTable>
  </div>
);

<SafDataGrid 
  data={ordersData}
  columns={expandableColumns}
  expandable
  expandedRows={expandedRows}
  onExpandedRowsChange={setExpandedRows}
  expandedRowRender={expandedRowRender}
/>
```

### Server-Side Data Grid

```typescript
// React
const ServerSideDataGrid = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [currentPage, setCurrentPage] = useState(1);
  const [pageSize, setPageSize] = useState(25);
  const [sortBy, setSortBy] = useState('');
  const [sortDirection, setSortDirection] = useState('asc');
  const [filters, setFilters] = useState({});
  const [totalRows, setTotalRows] = useState(0);

  const fetchData = async (page, size, sort, direction, filterParams) => {
    setLoading(true);
    try {
      const response = await api.getData({
        page,
        pageSize: size,
        sortBy: sort,
        sortDirection: direction,
        ...filterParams
      });
      
      setData(response.data);
      setTotalRows(response.totalCount);
    } catch (error) {
      console.error('Failed to fetch data:', error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchData(currentPage, pageSize, sortBy, sortDirection, filters);
  }, [currentPage, pageSize, sortBy, sortDirection, filters]);

  return (
    <SafDataGrid 
      data={data}
      columns={columns}
      loading={loading}
      pagination
      currentPage={currentPage}
      pageSize={pageSize}
      totalRows={totalRows}
      sortBy={sortBy}
      sortDirection={sortDirection}
      filters={filters}
      onPageChange={setCurrentPage}
      onPageSizeChange={setPageSize}
      onSortChange={(column, direction) => {
        setSortBy(column);
        setSortDirection(direction);
      }}
      onFilterChange={setFilters}
    />
  );
};
```

### Advanced Filtering Data Grid

```typescript
// React
const advancedColumns = [
  { 
    key: 'name', 
    title: 'Name', 
    width: 200,
    filterable: true,
    filterType: 'text'
  },
  {
    key: 'department',
    title: 'Department',
    width: 150,
    filterable: true,
    filterType: 'select',
    filterOptions: ['Engineering', 'Marketing', 'Sales', 'HR']
  },
  {
    key: 'salary',
    title: 'Salary',
    width: 120,
    filterable: true,
    filterType: 'number',
    render: (value) => `$${value.toLocaleString()}`
  },
  {
    key: 'startDate',
    title: 'Start Date',
    width: 150,
    filterable: true,
    filterType: 'date',
    render: (value) => new Date(value).toLocaleDateString()
  }
];

<SafDataGrid 
  data={employeeData}
  columns={advancedColumns}
  filterable
  onFilterChange={(filters) => {
    console.log('Applied filters:', filters);
    // Handle filtering logic
  }}
/>
```

### Editable Data Grid

```typescript
// React
const EditableDataGrid = ({ data, onDataChange }) => {
  const [editingCell, setEditingCell] = useState(null);
  const [tempValue, setTempValue] = useState('');

  const editableColumns = [
    { key: 'id', title: 'ID', width: 80 },
    {
      key: 'name',
      title: 'Name',
      width: 200,
      render: (value, row, index) => (
        editingCell?.row === index && editingCell?.column === 'name' ? (
          <SafInput 
            value={tempValue}
            onChange={setTempValue}
            onBlur={() => saveEdit(index, 'name', tempValue)}
            onKeyPress={(e) => {
              if (e.key === 'Enter') {
                saveEdit(index, 'name', tempValue);
              }
            }}
            autoFocus
          />
        ) : (
          <span onClick={() => startEdit(index, 'name', value)}>
            {value}
          </span>
        )
      )
    },
    {
      key: 'email',
      title: 'Email',
      width: 250,
      render: (value, row, index) => (
        editingCell?.row === index && editingCell?.column === 'email' ? (
          <SafInput 
            type="email"
            value={tempValue}
            onChange={setTempValue}
            onBlur={() => saveEdit(index, 'email', tempValue)}
            autoFocus
          />
        ) : (
          <span onClick={() => startEdit(index, 'email', value)}>
            {value}
          </span>
        )
      )
    }
  ];

  const startEdit = (row, column, value) => {
    setEditingCell({ row, column });
    setTempValue(value);
  };

  const saveEdit = (row, column, value) => {
    const newData = [...data];
    newData[row][column] = value;
    onDataChange(newData);
    setEditingCell(null);
  };

  return (
    <SafDataGrid 
      data={data}
      columns={editableColumns}
      onCellClick={(value, row, column) => {
        if (column.key !== 'id') {
          startEdit(data.indexOf(row), column.key, value);
        }
      }}
    />
  );
};
```

### Data Grid with Column Customization

```typescript
// React
const CustomizableDataGrid = ({ data }) => {
  const [columns, setColumns] = useState(defaultColumns);
  const [columnVisibility, setColumnVisibility] = useState({});

  const handleColumnReorder = (newColumns) => {
    setColumns(newColumns);
  };

  const handleColumnResize = (columnKey, width) => {
    setColumns(columns.map(col => 
      col.key === columnKey ? { ...col, width } : col
    ));
  };

  const toggleColumnVisibility = (columnKey) => {
    setColumnVisibility(prev => ({
      ...prev,
      [columnKey]: !prev[columnKey]
    }));
  };

  const visibleColumns = columns.filter(col => 
    columnVisibility[col.key] !== false
  );

  return (
    <div>
      <div className="column-controls">
        <SafPopover 
          content={
            <div className="column-visibility-menu">
              {columns.map(col => (
                <SafCheckbox 
                  key={col.key}
                  checked={columnVisibility[col.key] !== false}
                  onChange={() => toggleColumnVisibility(col.key)}
                  label={col.title}
                />
              ))}
            </div>
          }
        >
          <SafButton variant="outline" icon="settings">
            Customize Columns
          </SafButton>
        </SafPopover>
      </div>

      <SafDataGrid 
        data={data}
        columns={visibleColumns}
        resizable
        reorderable
        onColumnReorder={handleColumnReorder}
        onColumnResize={handleColumnResize}
      />
    </div>
  );
};
```

### Data Grid with Row Actions

```typescript
// React
const DataGridWithActions = ({ data, onEdit, onDelete, onView }) => {
  const [selectedRows, setSelectedRows] = useState([]);

  const columns = [
    { key: 'id', title: 'ID', width: 80 },
    { key: 'name', title: 'Name', width: 200 },
    { key: 'email', title: 'Email', width: 250 },
    {
      key: 'actions',
      title: 'Actions',
      width: 150,
      render: (value, row) => (
        <SafDropdownMenu
          trigger={
            <SafIconButton icon="more-vertical" size="small" />
          }
        >
          <SafDropdownMenuItem 
            icon="eye"
            onClick={() => onView(row)}
          >
            View Details
          </SafDropdownMenuItem>
          <SafDropdownMenuItem 
            icon="edit"
            onClick={() => onEdit(row)}
          >
            Edit
          </SafDropdownMenuItem>
          <SafDropdownMenuDivider />
          <SafDropdownMenuItem 
            icon="delete"
            onClick={() => onDelete(row)}
            destructive
          >
            Delete
          </SafDropdownMenuItem>
        </SafDropdownMenu>
      )
    }
  ];

  const handleBulkAction = (action) => {
    switch (action) {
      case 'delete':
        selectedRows.forEach(rowId => {
          const row = data.find(r => r.id === rowId);
          if (row) onDelete(row);
        });
        break;
      case 'export':
        exportSelectedRows(selectedRows);
        break;
    }
    setSelectedRows([]);
  };

  return (
    <div>
      {selectedRows.length > 0 && (
        <div className="bulk-actions">
          <span>{selectedRows.length} rows selected</span>
          <SafButton 
            variant="outline" 
            size="small"
            onClick={() => handleBulkAction('export')}
          >
            Export
          </SafButton>
          <SafButton 
            variant="outline" 
            size="small"
            onClick={() => handleBulkAction('delete')}
          >
            Delete
          </SafButton>
        </div>
      )}

      <SafDataGrid 
        data={data}
        columns={columns}
        selectable="multiple"
        selectedRows={selectedRows}
        onSelectionChange={setSelectedRows}
      />
    </div>
  );
};
```

### Responsive Data Grid

```typescript
// React
const ResponsiveDataGrid = ({ data }) => {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    handleResize();
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  const desktopColumns = [
    { key: 'id', title: 'ID', width: 80 },
    { key: 'name', title: 'Name', width: 200 },
    { key: 'email', title: 'Email', width: 250 },
    { key: 'department', title: 'Department', width: 150 },
    { key: 'role', title: 'Role', width: 120 },
    { key: 'status', title: 'Status', width: 100 }
  ];

  const mobileColumns = [
    {
      key: 'summary',
      title: 'Employee',
      render: (value, row) => (
        <div className="mobile-cell">
          <div className="primary-text">{row.name}</div>
          <div className="secondary-text">{row.email}</div>
          <SafBadge size="small">{row.role}</SafBadge>
        </div>
      )
    }
  ];

  return (
    <SafDataGrid 
      data={data}
      columns={isMobile ? mobileColumns : desktopColumns}
      height={isMobile ? '60vh' : 400}
      dense={isMobile}
    />
  );
};
```

## Best Practices

### Performance
- **Virtual Scrolling**: Use virtual scrolling for datasets > 1000 rows
- **Server-Side Operations**: Implement server-side sorting/filtering/pagination for large datasets
- **Memoization**: Memoize column configurations and render functions
- **Lazy Loading**: Load data incrementally when possible

### Data Management
- **Unique Keys**: Always provide unique row keys for proper rendering
- **Data Normalization**: Structure data consistently for better performance
- **State Management**: Use proper state management for complex data operations
- **Caching**: Implement caching for frequently accessed data

### User Experience
- **Loading States**: Show appropriate loading indicators
- **Empty States**: Provide meaningful empty state messages
- **Error Handling**: Handle and display data loading errors gracefully
- **Responsive Design**: Adapt grid layout for different screen sizes

### Accessibility
- **Keyboard Navigation**: Support full keyboard navigation
- **Screen Reader Support**: Provide proper ARIA labels and descriptions
- **Focus Management**: Maintain logical focus order
- **High Contrast**: Ensure proper contrast ratios

## Accessibility Considerations

- Uses proper table semantics with ARIA grid pattern
- Supports full keyboard navigation including arrow keys, Tab, Enter, Space
- Provides screen reader announcements for sorting, filtering, and selection changes
- Maintains focus within the grid and proper focus order
- Supports high contrast mode and respects reduced motion preferences
- Includes proper ARIA labels for all interactive elements

## Related Components

- **SafDataGridRow**: Individual row component
- **SafDataGridCell**: Individual cell component
- **SafTable**: Basic table component
- **SafPagination**: Pagination component
- **SafEmptyState**: Empty state component
- **SafSkeleton**: Loading skeleton component

## Notes

- SafDataGrid automatically handles virtualization for performance optimization
- The component supports both client-side and server-side data operations
- Column configurations are memoized to prevent unnecessary re-renders
- Selection state is maintained internally but can be controlled externally
- The grid supports both fixed and fluid column widths
- Sorting and filtering can be combined for advanced data exploration
- The component integrates with form validation for inline editing scenarios
- Export functionality can be implemented through custom column actions
