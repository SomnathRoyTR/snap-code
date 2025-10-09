# SafTable

A comprehensive table component that provides structured data display with built-in styling options, density controls, and accessibility features. SafTable automatically manages global styles for consistent table appearance across your application.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `density` | `'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Controls spacing in and around table cells |
| `alternatingRows` | `boolean` | `true` | Enables zebra striping with alternating row background colors |
| `inlineBorders` | `boolean` | `true` | Controls visibility of vertical column borders |
| `headerBackground` | `'subtle' \| 'default' \| 'strong'` | `'default'` | Sets the background style for table headers |
| `children` | `ReactNode` | - | Table content (thead, tbody, tfoot, tr, th, td elements) |

### Examples

#### Basic Usage
```jsx
import { SafTable } from '@saffron/core-components/react';

function BasicTable() {
  const data = [
    { id: 1, name: 'John Doe', email: 'john@example.com', role: 'Admin' },
    { id: 2, name: 'Jane Smith', email: 'jane@example.com', role: 'User' },
    { id: 3, name: 'Bob Johnson', email: 'bob@example.com', role: 'Editor' }
  ];
  
  return (
    <SafTable>
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Role</th>
        </tr>
      </thead>
      <tbody>
        {data.map(user => (
          <tr key={user.id}>
            <td>{user.id}</td>
            <td>{user.name}</td>
            <td>{user.email}</td>
            <td>{user.role}</td>
          </tr>
        ))}
      </tbody>
    </SafTable>
  );
}
```

#### Advanced Usage
```jsx
import { SafTable, SafButton, SafIcon, SafBadge } from '@saffron/core-components/react';
import { useState } from 'react';

// Table with various configurations
function ConfigurableTable() {
  const [density, setDensity] = useState('standard');
  const [alternatingRows, setAlternatingRows] = useState(true);
  const [inlineBorders, setInlineBorders] = useState(true);
  const [headerBackground, setHeaderBackground] = useState('default');
  
  const products = [
    { id: 'P001', name: 'Laptop Pro', category: 'Electronics', price: 1299.99, stock: 15, status: 'Active' },
    { id: 'P002', name: 'Wireless Mouse', category: 'Accessories', price: 29.99, stock: 50, status: 'Active' },
    { id: 'P003', name: 'Monitor 4K', category: 'Electronics', price: 599.99, stock: 8, status: 'Low Stock' },
    { id: 'P004', name: 'Keyboard Mechanical', category: 'Accessories', price: 129.99, stock: 0, status: 'Out of Stock' }
  ];
  
  const getStatusBadge = (status) => {
    switch (status) {
      case 'Active':
        return <SafBadge appearance="success">Active</SafBadge>;
      case 'Low Stock':
        return <SafBadge appearance="warning">Low Stock</SafBadge>;
      case 'Out of Stock':
        return <SafBadge appearance="error">Out of Stock</SafBadge>;
      default:
        return <SafBadge>{status}</SafBadge>;
    }
  };
  
  return (
    <div>
      {/* Table configuration controls */}
      <div className="table-controls">
        <label>
          Density:
          <select value={density} onChange={(e) => setDensity(e.target.value)}>
            <option value="compact">Compact</option>
            <option value="standard">Standard</option>
            <option value="relaxed">Relaxed</option>
          </select>
        </label>
        
        <label>
          <input
            type="checkbox"
            checked={alternatingRows}
            onChange={(e) => setAlternatingRows(e.target.checked)}
          />
          Alternating Rows
        </label>
        
        <label>
          <input
            type="checkbox"
            checked={inlineBorders}
            onChange={(e) => setInlineBorders(e.target.checked)}
          />
          Column Borders
        </label>
        
        <label>
          Header Background:
          <select value={headerBackground} onChange={(e) => setHeaderBackground(e.target.value)}>
            <option value="subtle">Subtle</option>
            <option value="default">Default</option>
            <option value="strong">Strong</option>
          </select>
        </label>
      </div>
      
      {/* Configured table */}
      <SafTable
        density={density}
        alternatingRows={alternatingRows}
        inlineBorders={inlineBorders}
        headerBackground={headerBackground}
      >
        <thead>
          <tr>
            <th>Product ID</th>
            <th>Name</th>
            <th>Category</th>
            <th>Price</th>
            <th>Stock</th>
            <th>Status</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {products.map(product => (
            <tr key={product.id}>
              <td>{product.id}</td>
              <td>{product.name}</td>
              <td>{product.category}</td>
              <td>${product.price.toFixed(2)}</td>
              <td>{product.stock}</td>
              <td>{getStatusBadge(product.status)}</td>
              <td>
                <SafButton appearance="tertiary" iconOnly={true} aria-label="Edit product">
                  <SafIcon iconName="edit" />
                </SafButton>
                <SafButton appearance="tertiary" iconOnly={true} aria-label="Delete product">
                  <SafIcon iconName="trash" />
                </SafButton>
              </td>
            </tr>
          ))}
        </tbody>
      </SafTable>
    </div>
  );
}

// Sortable table
function SortableTable() {
  const [data, setData] = useState([
    { id: 1, name: 'Alice Johnson', department: 'Engineering', salary: 95000, startDate: '2020-03-15' },
    { id: 2, name: 'Bob Smith', department: 'Marketing', salary: 70000, startDate: '2019-07-22' },
    { id: 3, name: 'Carol Davis', department: 'Engineering', salary: 105000, startDate: '2021-01-10' },
    { id: 4, name: 'David Wilson', department: 'Sales', salary: 80000, startDate: '2018-11-05' }
  ]);
  
  const [sortConfig, setSortConfig] = useState({ key: null, direction: 'asc' });
  
  const handleSort = (key) => {
    let direction = 'asc';
    if (sortConfig.key === key && sortConfig.direction === 'asc') {
      direction = 'desc';
    }
    
    const sortedData = [...data].sort((a, b) => {
      if (a[key] < b[key]) return direction === 'asc' ? -1 : 1;
      if (a[key] > b[key]) return direction === 'asc' ? 1 : -1;
      return 0;
    });
    
    setData(sortedData);
    setSortConfig({ key, direction });
  };
  
  const getSortIcon = (columnKey) => {
    if (sortConfig.key !== columnKey) {
      return <SafIcon iconName="sort" />;
    }
    return sortConfig.direction === 'asc' ? 
      <SafIcon iconName="sort-up" /> : 
      <SafIcon iconName="sort-down" />;
  };
  
  return (
    <SafTable density="standard" headerBackground="subtle">
      <thead>
        <tr>
          <th>
            <button onClick={() => handleSort('name')} className="sort-button">
              Name {getSortIcon('name')}
            </button>
          </th>
          <th>
            <button onClick={() => handleSort('department')} className="sort-button">
              Department {getSortIcon('department')}
            </button>
          </th>
          <th>
            <button onClick={() => handleSort('salary')} className="sort-button">
              Salary {getSortIcon('salary')}
            </button>
          </th>
          <th>
            <button onClick={() => handleSort('startDate')} className="sort-button">
              Start Date {getSortIcon('startDate')}
            </button>
          </th>
        </tr>
      </thead>
      <tbody>
        {data.map(employee => (
          <tr key={employee.id}>
            <td>{employee.name}</td>
            <td>{employee.department}</td>
            <td>${employee.salary.toLocaleString()}</td>
            <td>{new Date(employee.startDate).toLocaleDateString()}</td>
          </tr>
        ))}
      </tbody>
    </SafTable>
  );
}

// Table with selection
function SelectableTable() {
  const [selectedRows, setSelectedRows] = useState(new Set());
  const [selectAll, setSelectAll] = useState(false);
  
  const orders = [
    { id: 'ORD001', customer: 'Acme Corp', amount: 2500.00, status: 'Shipped', date: '2024-01-15' },
    { id: 'ORD002', customer: 'TechStart Inc', amount: 1750.00, status: 'Processing', date: '2024-01-16' },
    { id: 'ORD003', customer: 'Global Solutions', amount: 3200.00, status: 'Delivered', date: '2024-01-14' }
  ];
  
  const handleSelectAll = (checked) => {
    if (checked) {
      setSelectedRows(new Set(orders.map(order => order.id)));
    } else {
      setSelectedRows(new Set());
    }
    setSelectAll(checked);
  };
  
  const handleRowSelect = (orderId, checked) => {
    const newSelected = new Set(selectedRows);
    if (checked) {
      newSelected.add(orderId);
    } else {
      newSelected.delete(orderId);
    }
    setSelectedRows(newSelected);
    setSelectAll(newSelected.size === orders.length);
  };
  
  return (
    <div>
      {selectedRows.size > 0 && (
        <div className="selection-toolbar">
          <span>{selectedRows.size} items selected</span>
          <SafButton appearance="secondary">Export Selected</SafButton>
          <SafButton appearance="tertiary">Delete Selected</SafButton>
        </div>
      )}
      
      <SafTable alternatingRows={true} inlineBorders={true}>
        <thead>
          <tr>
            <th>
              <input
                type="checkbox"
                checked={selectAll}
                onChange={(e) => handleSelectAll(e.target.checked)}
                aria-label="Select all orders"
              />
            </th>
            <th>Order ID</th>
            <th>Customer</th>
            <th>Amount</th>
            <th>Status</th>
            <th>Date</th>
          </tr>
        </thead>
        <tbody>
          {orders.map(order => (
            <tr key={order.id} className={selectedRows.has(order.id) ? 'selected' : ''}>
              <td>
                <input
                  type="checkbox"
                  checked={selectedRows.has(order.id)}
                  onChange={(e) => handleRowSelect(order.id, e.target.checked)}
                  aria-label={`Select order ${order.id}`}
                />
              </td>
              <td>{order.id}</td>
              <td>{order.customer}</td>
              <td>${order.amount.toFixed(2)}</td>
              <td>{order.status}</td>
              <td>{order.date}</td>
            </tr>
          ))}
        </tbody>
      </SafTable>
    </div>
  );
}

// Responsive table
function ResponsiveTable() {
  const [viewMode, setViewMode] = useState('table'); // 'table' or 'cards'
  
  const projects = [
    { id: 1, name: 'Website Redesign', lead: 'Sarah Connor', progress: 75, deadline: '2024-02-15', priority: 'High' },
    { id: 2, name: 'Mobile App', lead: 'John Matrix', progress: 45, deadline: '2024-03-01', priority: 'Medium' },
    { id: 3, name: 'API Integration', lead: 'Ellen Ripley', progress: 90, deadline: '2024-01-30', priority: 'High' }
  ];
  
  if (viewMode === 'cards') {
    return (
      <div>
        <SafButton onClick={() => setViewMode('table')}>Switch to Table View</SafButton>
        <div className="card-grid">
          {projects.map(project => (
            <div key={project.id} className="project-card">
              <h3>{project.name}</h3>
              <p><strong>Lead:</strong> {project.lead}</p>
              <p><strong>Progress:</strong> {project.progress}%</p>
              <p><strong>Deadline:</strong> {project.deadline}</p>
              <p><strong>Priority:</strong> {project.priority}</p>
            </div>
          ))}
        </div>
      </div>
    );
  }
  
  return (
    <div>
      <SafButton onClick={() => setViewMode('cards')}>Switch to Card View</SafButton>
      <SafTable density="compact">
        <thead>
          <tr>
            <th>Project Name</th>
            <th>Project Lead</th>
            <th>Progress</th>
            <th>Deadline</th>
            <th>Priority</th>
          </tr>
        </thead>
        <tbody>
          {projects.map(project => (
            <tr key={project.id}>
              <td>{project.name}</td>
              <td>{project.lead}</td>
              <td>
                <div className="progress-bar">
                  <div 
                    className="progress-fill" 
                    style={{ width: `${project.progress}%` }}
                  ></div>
                  <span>{project.progress}%</span>
                </div>
              </td>
              <td>{project.deadline}</td>
              <td>
                <SafBadge appearance={project.priority === 'High' ? 'error' : 'warning'}>
                  {project.priority}
                </SafBadge>
              </td>
            </tr>
          ))}
        </tbody>
      </SafTable>
    </div>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `density` | `'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Controls spacing in and around table cells |
| `alternating-rows` | `boolean` | `true` | Enables zebra striping with alternating row background colors |
| `inline-borders` | `boolean` | `true` | Controls visibility of vertical column borders |
| `header-background` | `'subtle' \| 'default' \| 'strong'` | `'default'` | Sets the background style for table headers |

### Examples

#### Basic Usage
```html
<saf-table>
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Email</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let user of users">
      <td>{{ user.id }}</td>
      <td>{{ user.name }}</td>
      <td>{{ user.email }}</td>
      <td>{{ user.role }}</td>
    </tr>
  </tbody>
</saf-table>
```

```typescript
import { Component } from '@angular/core';

interface User {
  id: number;
  name: string;
  email: string;
  role: string;
}

@Component({
  selector: 'app-basic-table',
  template: `
    <saf-table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Role</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let user of users">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.role }}</td>
        </tr>
      </tbody>
    </saf-table>
  `
})
export class BasicTableComponent {
  users: User[] = [
    { id: 1, name: 'John Doe', email: 'john@example.com', role: 'Admin' },
    { id: 2, name: 'Jane Smith', email: 'jane@example.com', role: 'User' },
    { id: 3, name: 'Bob Johnson', email: 'bob@example.com', role: 'Editor' }
  ];
}
```

#### Advanced Usage
```html
<!-- Configurable table -->
<div class="table-controls">
  <label>
    Density:
    <select [(ngModel)]="density">
      <option value="compact">Compact</option>
      <option value="standard">Standard</option>
      <option value="relaxed">Relaxed</option>
    </select>
  </label>
  
  <label>
    <input type="checkbox" [(ngModel)]="alternatingRows" />
    Alternating Rows
  </label>
  
  <label>
    <input type="checkbox" [(ngModel)]="inlineBorders" />
    Column Borders
  </label>
  
  <label>
    Header Background:
    <select [(ngModel)]="headerBackground">
      <option value="subtle">Subtle</option>
      <option value="default">Default</option>
      <option value="strong">Strong</option>
    </select>
  </label>
</div>

<saf-table
  [density]="density"
  [alternating-rows]="alternatingRows"
  [inline-borders]="inlineBorders"
  [header-background]="headerBackground">
  <thead>
    <tr>
      <th>Product ID</th>
      <th>Name</th>
      <th>Category</th>
      <th>Price</th>
      <th>Stock</th>
      <th>Status</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let product of products">
      <td>{{ product.id }}</td>
      <td>{{ product.name }}</td>
      <td>{{ product.category }}</td>
      <td>{{ product.price | currency }}</td>
      <td>{{ product.stock }}</td>
      <td>
        <saf-badge [appearance]="getStatusAppearance(product.status)">
          {{ product.status }}
        </saf-badge>
      </td>
      <td>
        <saf-button 
          appearance="tertiary" 
          [icon-only]="true" 
          aria-label="Edit product"
          (click)="editProduct(product)">
          <saf-icon icon-name="edit"></saf-icon>
        </saf-button>
        <saf-button 
          appearance="tertiary" 
          [icon-only]="true" 
          aria-label="Delete product"
          (click)="deleteProduct(product)">
          <saf-icon icon-name="trash"></saf-icon>
        </saf-button>
      </td>
    </tr>
  </tbody>
</saf-table>

<!-- Sortable table -->
<saf-table density="standard" header-background="subtle">
  <thead>
    <tr>
      <th>
        <button (click)="handleSort('name')" class="sort-button">
          Name <saf-icon [icon-name]="getSortIcon('name')"></saf-icon>
        </button>
      </th>
      <th>
        <button (click)="handleSort('department')" class="sort-button">
          Department <saf-icon [icon-name]="getSortIcon('department')"></saf-icon>
        </button>
      </th>
      <th>
        <button (click)="handleSort('salary')" class="sort-button">
          Salary <saf-icon [icon-name]="getSortIcon('salary')"></saf-icon>
        </button>
      </th>
      <th>
        <button (click)="handleSort('startDate')" class="sort-button">
          Start Date <saf-icon [icon-name]="getSortIcon('startDate')"></saf-icon>
        </button>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let employee of sortedEmployees">
      <td>{{ employee.name }}</td>
      <td>{{ employee.department }}</td>
      <td>{{ employee.salary | currency }}</td>
      <td>{{ employee.startDate | date }}</td>
    </tr>
  </tbody>
</saf-table>

<!-- Selectable table -->
<div *ngIf="selectedRows.size > 0" class="selection-toolbar">
  <span>{{ selectedRows.size }} items selected</span>
  <saf-button appearance="secondary" (click)="exportSelected()">Export Selected</saf-button>
  <saf-button appearance="tertiary" (click)="deleteSelected()">Delete Selected</saf-button>
</div>

<saf-table [alternating-rows]="true" [inline-borders]="true">
  <thead>
    <tr>
      <th>
        <input
          type="checkbox"
          [checked]="selectAll"
          (change)="handleSelectAll($event)"
          aria-label="Select all orders" />
      </th>
      <th>Order ID</th>
      <th>Customer</th>
      <th>Amount</th>
      <th>Status</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let order of orders" [class.selected]="selectedRows.has(order.id)">
      <td>
        <input
          type="checkbox"
          [checked]="selectedRows.has(order.id)"
          (change)="handleRowSelect(order.id, $event)"
          [attr.aria-label]="'Select order ' + order.id" />
      </td>
      <td>{{ order.id }}</td>
      <td>{{ order.customer }}</td>
      <td>{{ order.amount | currency }}</td>
      <td>{{ order.status }}</td>
      <td>{{ order.date | date }}</td>
    </tr>
  </tbody>
</saf-table>
```

```typescript
import { Component } from '@angular/core';

interface Product {
  id: string;
  name: string;
  category: string;
  price: number;
  stock: number;
  status: string;
}

interface Employee {
  id: number;
  name: string;
  department: string;
  salary: number;
  startDate: string;
}

interface Order {
  id: string;
  customer: string;
  amount: number;
  status: string;
  date: string;
}

@Component({
  selector: 'app-advanced-table',
  template: `
    <!-- Template content shown above -->
  `,
  styles: [`
    .sort-button {
      background: none;
      border: none;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .selected {
      background-color: var(--color-selected, #e3f2fd);
    }
    
    .selection-toolbar {
      display: flex;
      align-items: center;
      gap: 1rem;
      padding: 1rem;
      background: var(--color-surface-2);
      border-radius: 4px;
      margin-bottom: 1rem;
    }
  `]
})
export class AdvancedTableComponent {
  // Configuration properties
  density = 'standard';
  alternatingRows = true;
  inlineBorders = true;
  headerBackground = 'default';
  
  // Data
  products: Product[] = [
    { id: 'P001', name: 'Laptop Pro', category: 'Electronics', price: 1299.99, stock: 15, status: 'Active' },
    { id: 'P002', name: 'Wireless Mouse', category: 'Accessories', price: 29.99, stock: 50, status: 'Active' },
    { id: 'P003', name: 'Monitor 4K', category: 'Electronics', price: 599.99, stock: 8, status: 'Low Stock' },
    { id: 'P004', name: 'Keyboard Mechanical', category: 'Accessories', price: 129.99, stock: 0, status: 'Out of Stock' }
  ];
  
  employees: Employee[] = [
    { id: 1, name: 'Alice Johnson', department: 'Engineering', salary: 95000, startDate: '2020-03-15' },
    { id: 2, name: 'Bob Smith', department: 'Marketing', salary: 70000, startDate: '2019-07-22' },
    { id: 3, name: 'Carol Davis', department: 'Engineering', salary: 105000, startDate: '2021-01-10' },
    { id: 4, name: 'David Wilson', department: 'Sales', salary: 80000, startDate: '2018-11-05' }
  ];
  
  orders: Order[] = [
    { id: 'ORD001', customer: 'Acme Corp', amount: 2500.00, status: 'Shipped', date: '2024-01-15' },
    { id: 'ORD002', customer: 'TechStart Inc', amount: 1750.00, status: 'Processing', date: '2024-01-16' },
    { id: 'ORD003', customer: 'Global Solutions', amount: 3200.00, status: 'Delivered', date: '2024-01-14' }
  ];
  
  // Sorting
  sortConfig = { key: null, direction: 'asc' };
  sortedEmployees = [...this.employees];
  
  // Selection
  selectedRows = new Set<string>();
  selectAll = false;
  
  // Methods
  getStatusAppearance(status: string): string {
    switch (status) {
      case 'Active':
        return 'success';
      case 'Low Stock':
        return 'warning';
      case 'Out of Stock':
        return 'error';
      default:
        return 'default';
    }
  }
  
  editProduct(product: Product): void {
    console.log('Edit product:', product);
  }
  
  deleteProduct(product: Product): void {
    console.log('Delete product:', product);
  }
  
  handleSort(key: string): void {
    let direction = 'asc';
    if (this.sortConfig.key === key && this.sortConfig.direction === 'asc') {
      direction = 'desc';
    }
    
    this.sortedEmployees = [...this.employees].sort((a, b) => {
      const aValue = a[key as keyof Employee];
      const bValue = b[key as keyof Employee];
      
      if (aValue < bValue) return direction === 'asc' ? -1 : 1;
      if (aValue > bValue) return direction === 'asc' ? 1 : -1;
      return 0;
    });
    
    this.sortConfig = { key, direction };
  }
  
  getSortIcon(columnKey: string): string {
    if (this.sortConfig.key !== columnKey) {
      return 'sort';
    }
    return this.sortConfig.direction === 'asc' ? 'sort-up' : 'sort-down';
  }
  
  handleSelectAll(event: Event): void {
    const checked = (event.target as HTMLInputElement).checked;
    if (checked) {
      this.selectedRows = new Set(this.orders.map(order => order.id));
    } else {
      this.selectedRows = new Set();
    }
    this.selectAll = checked;
  }
  
  handleRowSelect(orderId: string, event: Event): void {
    const checked = (event.target as HTMLInputElement).checked;
    const newSelected = new Set(this.selectedRows);
    
    if (checked) {
      newSelected.add(orderId);
    } else {
      newSelected.delete(orderId);
    }
    
    this.selectedRows = newSelected;
    this.selectAll = newSelected.size === this.orders.length;
  }
  
  exportSelected(): void {
    console.log('Export selected:', this.selectedRows);
  }
  
  deleteSelected(): void {
    console.log('Delete selected:', this.selectedRows);
  }
}
```

### Best Practices

1. **Table structure and semantics:**
   - Always use proper HTML table structure with `thead`, `tbody`, and `tfoot`
   - Use `th` elements for headers with appropriate scope attributes
   - Provide table captions or aria-labels for screen readers
   - Use `rowheader` scope for row headers when applicable

2. **Data presentation:**
   - Choose appropriate density based on data complexity and screen size
   - Use alternating rows for better data readability
   - Apply consistent formatting for similar data types (dates, currencies, etc.)
   - Consider column alignment based on data type (numbers right-aligned)

3. **Interactive features:**
   - Provide clear visual feedback for sortable columns
   - Use appropriate ARIA labels for interactive elements
   - Implement keyboard navigation for accessibility
   - Show loading states during data operations

4. **Performance considerations:**
   - Implement virtual scrolling for large datasets
   - Use pagination or lazy loading when appropriate
   - Optimize re-rendering with proper change detection strategies
   - Consider using trackBy functions in Angular for efficient list updates

5. **Responsive design:**
   - Consider alternative layouts for mobile devices (card view, stacked layout)
   - Use horizontal scrolling sparingly and provide visual indicators
   - Prioritize essential columns for smaller screens
   - Test touch interactions on mobile devices

### Notes

- **Global styles:** SafTable automatically injects global styles into the document for consistent table appearance across the application.
- **Style management:** The component uses CSSStyleSheet API for efficient global style management and cleanup.
- **Browser compatibility:** Modern browsers support the adopted stylesheets feature; ensure fallbacks for older browsers if needed.
- **Customization:** While the component provides built-in styling options, you can still apply custom CSS for additional styling needs.
- **Performance:** The global style injection is optimized to prevent duplicate stylesheets and includes proper cleanup when components are removed.
