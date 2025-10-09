# SafDataTable Component

## Overview

SafDataTable is a comprehensive data table component designed for displaying, sorting, filtering, and managing structured data sets. It provides advanced features including column configuration, pagination, row selection, data export, real-time updates, and extensive customization options. The component is ideal for legal case management, document listings, client databases, financial reports, and any application requiring robust data presentation and manipulation capabilities.

## React API

### SafDataTable

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `data` | `any[]` | Yes | - | Array of data objects to display |
| `columns` | `DataTableColumn[]` | Yes | - | Column configuration array |
| `variant` | `'default' \| 'compact' \| 'comfortable' \| 'dense'` | No | `'default'` | Table layout variant |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Overall table size |
| `striped` | `boolean` | No | `false` | Alternate row background colors |
| `bordered` | `boolean` | No | `false` | Show table borders |
| `hoverable` | `boolean` | No | `true` | Highlight rows on hover |
| `sortable` | `boolean` | No | `true` | Enable column sorting |
| `filterable` | `boolean` | No | `false` | Enable column filtering |
| `searchable` | `boolean` | No | `false` | Enable global search |
| `selectable` | `boolean` | No | `false` | Enable row selection |
| `selectMode` | `'single' \| 'multiple'` | No | `'multiple'` | Row selection mode |
| `expandable` | `boolean` | No | `false` | Enable row expansion |
| `resizable` | `boolean` | No | `false` | Enable column resizing |
| `reorderable` | `boolean` | No | `false` | Enable column reordering |
| `virtualized` | `boolean` | No | `false` | Enable virtualization for large datasets |
| `pagination` | `PaginationConfig \| boolean` | No | `false` | Pagination configuration |
| `loading` | `boolean` | No | `false` | Show loading state |
| `error` | `string \| ReactNode` | No | - | Error message to display |
| `emptyMessage` | `string \| ReactNode` | No | `'No data to display'` | Message when table is empty |
| `height` | `string \| number` | No | - | Fixed table height |
| `maxHeight` | `string \| number` | No | - | Maximum table height |
| `stickyHeader` | `boolean` | No | `false` | Make header sticky on scroll |
| `stickyColumns` | `number` | No | `0` | Number of left columns to make sticky |
| `showFooter` | `boolean` | No | `false` | Show table footer |
| `exportable` | `boolean \| ExportConfig` | No | `false` | Enable data export |
| `rowKey` | `string \| ((row: any) => string)` | No | `'id'` | Unique key for each row |
| `defaultSort` | `SortConfig` | No | - | Default sort configuration |
| `selectedRows` | `any[]` | No | `[]` | Currently selected rows |
| `expandedRows` | `any[]` | No | `[]` | Currently expanded rows |
| `onSort` | `(sortConfig: SortConfig) => void` | No | - | Callback when sorting changes |
| `onFilter` | `(filters: FilterConfig) => void` | No | - | Callback when filters change |
| `onSearch` | `(query: string) => void` | No | - | Callback when search query changes |
| `onSelect` | `(selectedRows: any[]) => void` | No | - | Callback when row selection changes |
| `onExpand` | `(expandedRows: any[]) => void` | No | - | Callback when row expansion changes |
| `onRowClick` | `(row: any, index: number) => void` | No | - | Callback when row is clicked |
| `onRowDoubleClick` | `(row: any, index: number) => void` | No | - | Callback when row is double-clicked |
| `onColumnResize` | `(columnId: string, width: number) => void` | No | - | Callback when column is resized |
| `onColumnReorder` | `(newOrder: string[]) => void` | No | - | Callback when columns are reordered |
| `onExport` | `(data: any[], format: string) => void` | No | - | Callback when data is exported |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### DataTableColumn Interface

```typescript
interface DataTableColumn {
  id: string;
  key: string;
  title: string | ReactNode;
  dataType?: 'string' | 'number' | 'date' | 'boolean' | 'currency' | 'custom';
  width?: string | number;
  minWidth?: string | number;
  maxWidth?: string | number;
  sortable?: boolean;
  filterable?: boolean;
  resizable?: boolean;
  fixed?: 'left' | 'right';
  align?: 'left' | 'center' | 'right';
  render?: (value: any, row: any, index: number) => ReactNode;
  headerRender?: () => ReactNode;
  footerRender?: (data: any[]) => ReactNode;
  filterType?: 'text' | 'select' | 'date' | 'range' | 'custom';
  filterOptions?: FilterOption[];
  customFilter?: (value: any, filterValue: any) => boolean;
  sortFunction?: (a: any, b: any) => number;
  exportKey?: string;
  exportFormat?: (value: any) => string;
  visible?: boolean;
  className?: string;
  headerClassName?: string;
  cellClassName?: string | ((value: any, row: any) => string);
}

interface PaginationConfig {
  pageSize?: number;
  pageSizeOptions?: number[];
  showSizeChanger?: boolean;
  showQuickJumper?: boolean;
  showTotal?: boolean;
  position?: 'top' | 'bottom' | 'both';
}

interface SortConfig {
  columnId: string;
  direction: 'asc' | 'desc';
}

interface FilterConfig {
  [columnId: string]: any;
}

interface ExportConfig {
  formats?: ('csv' | 'excel' | 'pdf' | 'json')[];
  filename?: string;
  includeHeaders?: boolean;
  selectedOnly?: boolean;
}
```

## Angular API

### saf-data-table

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[data]` | `any[]` | Yes | - | Array of data objects to display |
| `[columns]` | `DataTableColumn[]` | Yes | - | Column configuration array |
| `[variant]` | `'default' \| 'compact' \| 'comfortable' \| 'dense'` | No | `'default'` | Table layout variant |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Overall table size |
| `[striped]` | `boolean` | No | `false` | Alternate row background colors |
| `[bordered]` | `boolean` | No | `false` | Show table borders |
| `[hoverable]` | `boolean` | No | `true` | Highlight rows on hover |
| `[sortable]` | `boolean` | No | `true` | Enable column sorting |
| `[filterable]` | `boolean` | No | `false` | Enable column filtering |
| `[searchable]` | `boolean` | No | `false` | Enable global search |
| `[selectable]` | `boolean` | No | `false` | Enable row selection |
| `[selectMode]` | `'single' \| 'multiple'` | No | `'multiple'` | Row selection mode |
| `[expandable]` | `boolean` | No | `false` | Enable row expansion |
| `[resizable]` | `boolean` | No | `false` | Enable column resizing |
| `[reorderable]` | `boolean` | No | `false` | Enable column reordering |
| `[virtualized]` | `boolean` | No | `false` | Enable virtualization for large datasets |
| `[pagination]` | `PaginationConfig \| boolean` | No | `false` | Pagination configuration |
| `[loading]` | `boolean` | No | `false` | Show loading state |
| `[error]` | `string \| TemplateRef` | No | - | Error message to display |
| `[emptyMessage]` | `string \| TemplateRef` | No | `'No data to display'` | Message when table is empty |
| `[height]` | `string \| number` | No | - | Fixed table height |
| `[maxHeight]` | `string \| number` | No | - | Maximum table height |
| `[stickyHeader]` | `boolean` | No | `false` | Make header sticky on scroll |
| `[stickyColumns]` | `number` | No | `0` | Number of left columns to make sticky |
| `[showFooter]` | `boolean` | No | `false` | Show table footer |
| `[exportable]` | `boolean \| ExportConfig` | No | `false` | Enable data export |
| `[rowKey]` | `string \| Function` | No | `'id'` | Unique key for each row |
| `[defaultSort]` | `SortConfig` | No | - | Default sort configuration |
| `[selectedRows]` | `any[]` | No | `[]` | Currently selected rows |
| `[expandedRows]` | `any[]` | No | `[]` | Currently expanded rows |
| `(sort)` | `EventEmitter<SortConfig>` | No | - | Event when sorting changes |
| `(filter)` | `EventEmitter<FilterConfig>` | No | - | Event when filters change |
| `(search)` | `EventEmitter<string>` | No | - | Event when search query changes |
| `(select)` | `EventEmitter<any[]>` | No | - | Event when row selection changes |
| `(expand)` | `EventEmitter<any[]>` | No | - | Event when row expansion changes |
| `(rowClick)` | `EventEmitter<{row: any, index: number}>` | No | - | Event when row is clicked |
| `(rowDoubleClick)` | `EventEmitter<{row: any, index: number}>` | No | - | Event when row is double-clicked |
| `(columnResize)` | `EventEmitter<{columnId: string, width: number}>` | No | - | Event when column is resized |
| `(columnReorder)` | `EventEmitter<string[]>` | No | - | Event when columns are reordered |
| `(export)` | `EventEmitter<{data: any[], format: string}>` | No | - | Event when data is exported |

## Usage Examples

### Legal Case Management Table

#### React
```jsx
import { SafDataTable, SafChip, SafIcon, SafAvatar, SafBadge } from '@saffron/react';
import { useState, useEffect } from 'react';

const LegalCaseManagementTable = () => {
  const [caseData, setCaseData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [selectedCases, setSelectedCases] = useState([]);
  const [expandedRows, setExpandedRows] = useState([]);

  // Sample legal case data
  const legalCases = [
    {
      id: 'CASE-2024-001',
      caseNumber: 'CV-2024-001234',
      title: 'Global Corp vs. Tech Innovations LLC',
      type: 'Commercial Litigation',
      status: 'Active',
      priority: 'High',
      assignedLawyer: {
        id: 'lawyer-1',
        name: 'Sarah Johnson',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
        title: 'Senior Partner'
      },
      client: {
        name: 'Global Corp Inc.',
        type: 'Corporate'
      },
      dateOpened: new Date('2024-01-15'),
      lastActivity: new Date('2024-01-28'),
      billableHours: 42.5,
      estimatedValue: 2500000,
      nextDeadline: new Date('2024-02-15'),
      practiceArea: 'Corporate Law',
      jurisdiction: 'Federal',
      court: 'U.S. District Court, Southern District of New York',
      tags: ['Contract Dispute', 'IP Rights', 'Confidential'],
      documents: 127,
      notes: 'Discovery phase ongoing. Expert witness depositions scheduled for next month.'
    },
    {
      id: 'CASE-2024-002',
      caseNumber: 'CR-2024-005678',
      title: 'Employment Discrimination Case',
      type: 'Employment Law',
      status: 'Under Review',
      priority: 'Medium',
      assignedLawyer: {
        id: 'lawyer-2',
        name: 'Michael Chen',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=michael',
        title: 'Associate'
      },
      client: {
        name: 'Individual Client',
        type: 'Individual'
      },
      dateOpened: new Date('2024-01-20'),
      lastActivity: new Date('2024-01-27'),
      billableHours: 18.0,
      estimatedValue: 150000,
      nextDeadline: new Date('2024-02-10'),
      practiceArea: 'Employment Law',
      jurisdiction: 'State',
      court: 'Superior Court of California',
      tags: ['Discrimination', 'Wrongful Termination'],
      documents: 45,
      notes: 'Mediation scheduled. Client interview completed.'
    },
    {
      id: 'CASE-2024-003',
      caseNumber: 'IP-2024-009876',
      title: 'Patent Infringement Dispute',
      type: 'Intellectual Property',
      status: 'Closed',
      priority: 'High',
      assignedLawyer: {
        id: 'lawyer-3',
        name: 'Emily Rodriguez',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emily',
        title: 'IP Specialist'
      },
      client: {
        name: 'Tech Startup Inc.',
        type: 'Corporate'
      },
      dateOpened: new Date('2023-11-10'),
      lastActivity: new Date('2024-01-25'),
      billableHours: 89.5,
      estimatedValue: 1200000,
      nextDeadline: null,
      practiceArea: 'Intellectual Property',
      jurisdiction: 'Federal',
      court: 'U.S. District Court, District of Delaware',
      tags: ['Patent', 'Settlement', 'Confidential'],
      documents: 203,
      notes: 'Successfully settled out of court. Confidentiality agreement in place.'
    },
    {
      id: 'CASE-2024-004',
      caseNumber: 'RE-2024-004567',
      title: 'Commercial Real Estate Transaction',
      type: 'Real Estate',
      status: 'Active',
      priority: 'Low',
      assignedLawyer: {
        id: 'lawyer-4',
        name: 'David Park',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=david',
        title: 'Real Estate Attorney'
      },
      client: {
        name: 'Property Development LLC',
        type: 'Corporate'
      },
      dateOpened: new Date('2024-01-22'),
      lastActivity: new Date('2024-01-29'),
      billableHours: 12.0,
      estimatedValue: 50000,
      nextDeadline: new Date('2024-02-20'),
      practiceArea: 'Real Estate',
      jurisdiction: 'State',
      court: 'N/A',
      tags: ['Transaction', 'Due Diligence'],
      documents: 67,
      notes: 'Title search in progress. Environmental review pending.'
    }
  ];

  // Define table columns
  const caseColumns = [
    {
      id: 'caseNumber',
      key: 'caseNumber',
      title: 'Case Number',
      width: 150,
      sortable: true,
      filterable: true,
      fixed: 'left',
      render: (value, row) => (
        <div className="case-number-cell">
          <strong>{value}</strong>
          <SafBadge 
            variant="soft" 
            color={row.priority === 'High' ? 'danger' : row.priority === 'Medium' ? 'warning' : 'info'}
            size="small"
          >
            {row.priority}
          </SafBadge>
        </div>
      )
    },
    {
      id: 'title',
      key: 'title',
      title: 'Case Title',
      width: 300,
      sortable: true,
      filterable: true,
      render: (value, row) => (
        <div className="case-title-cell">
          <div className="title">{value}</div>
          <div className="subtitle">{row.type}</div>
        </div>
      )
    },
    {
      id: 'status',
      key: 'status',
      title: 'Status',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'select',
      filterOptions: [
        { label: 'Active', value: 'Active' },
        { label: 'Under Review', value: 'Under Review' },
        { label: 'Closed', value: 'Closed' },
        { label: 'On Hold', value: 'On Hold' }
      ],
      render: (value) => (
        <SafChip
          label={value}
          variant="filled"
          color={
            value === 'Active' ? 'success' :
            value === 'Under Review' ? 'warning' :
            value === 'Closed' ? 'neutral' : 'secondary'
          }
          size="small"
        />
      )
    },
    {
      id: 'assignedLawyer',
      key: 'assignedLawyer',
      title: 'Assigned Lawyer',
      width: 200,
      sortable: true,
      render: (value) => (
        <div className="lawyer-cell">
          <SafAvatar
            src={value.avatar}
            name={value.name}
            size="small"
          />
          <div className="lawyer-info">
            <div className="name">{value.name}</div>
            <div className="title">{value.title}</div>
          </div>
        </div>
      )
    },
    {
      id: 'client',
      key: 'client',
      title: 'Client',
      width: 180,
      sortable: true,
      filterable: true,
      render: (value) => (
        <div className="client-cell">
          <div className="client-name">{value.name}</div>
          <SafChip
            label={value.type}
            variant="soft"
            color="info"
            size="small"
          />
        </div>
      )
    },
    {
      id: 'practiceArea',
      key: 'practiceArea',
      title: 'Practice Area',
      width: 150,
      sortable: true,
      filterable: true,
      filterType: 'select',
      filterOptions: [
        { label: 'Corporate Law', value: 'Corporate Law' },
        { label: 'Employment Law', value: 'Employment Law' },
        { label: 'Intellectual Property', value: 'Intellectual Property' },
        { label: 'Real Estate', value: 'Real Estate' }
      ]
    },
    {
      id: 'dateOpened',
      key: 'dateOpened',
      title: 'Date Opened',
      dataType: 'date',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'date',
      render: (value) => value.toLocaleDateString()
    },
    {
      id: 'billableHours',
      key: 'billableHours',
      title: 'Billable Hours',
      dataType: 'number',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'range',
      align: 'right',
      render: (value) => `${value.toFixed(1)}h`
    },
    {
      id: 'estimatedValue',
      key: 'estimatedValue',
      title: 'Est. Value',
      dataType: 'currency',
      width: 130,
      sortable: true,
      filterable: true,
      filterType: 'range',
      align: 'right',
      render: (value) => new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 0
      }).format(value)
    },
    {
      id: 'nextDeadline',
      key: 'nextDeadline',
      title: 'Next Deadline',
      dataType: 'date',
      width: 130,
      sortable: true,
      render: (value) => {
        if (!value) return <span className="no-deadline">No deadline</span>;
        
        const isOverdue = value < new Date();
        const isUpcoming = value <= new Date(Date.now() + 7 * 24 * 60 * 60 * 1000);
        
        return (
          <div className={`deadline-cell ${isOverdue ? 'overdue' : isUpcoming ? 'upcoming' : ''}`}>
            {isOverdue && <SafIcon name="alert-triangle" size="small" />}
            {isUpcoming && !isOverdue && <SafIcon name="clock" size="small" />}
            <span>{value.toLocaleDateString()}</span>
          </div>
        );
      }
    },
    {
      id: 'actions',
      key: 'actions',
      title: 'Actions',
      width: 120,
      sortable: false,
      filterable: false,
      fixed: 'right',
      render: (value, row) => (
        <div className="actions-cell">
          <button
            onClick={() => handleViewCase(row)}
            className="action-btn"
            title="View Details"
          >
            <SafIcon name="eye" size="small" />
          </button>
          <button
            onClick={() => handleEditCase(row)}
            className="action-btn"
            title="Edit Case"
          >
            <SafIcon name="edit" size="small" />
          </button>
          <button
            onClick={() => handleCaseDocuments(row)}
            className="action-btn"
            title="Documents"
          >
            <SafIcon name="file" size="small" />
            <span className="document-count">{row.documents}</span>
          </button>
        </div>
      )
    }
  ];

  useEffect(() => {
    // Simulate data loading
    setLoading(true);
    setTimeout(() => {
      setCaseData(legalCases);
      setLoading(false);
    }, 1000);
  }, []);

  const handleSort = (sortConfig) => {
    console.log('Sort changed:', sortConfig);
    // Implement sorting logic
  };

  const handleFilter = (filters) => {
    console.log('Filters changed:', filters);
    // Implement filtering logic
  };

  const handleSearch = (query) => {
    console.log('Search query:', query);
    // Implement search logic
  };

  const handleRowSelect = (selectedRows) => {
    setSelectedCases(selectedRows);
    console.log('Selected cases:', selectedRows);
  };

  const handleRowExpand = (expandedRows) => {
    setExpandedRows(expandedRows);
    console.log('Expanded rows:', expandedRows);
  };

  const handleViewCase = (caseRow) => {
    console.log('View case:', caseRow);
    // Navigate to case details
  };

  const handleEditCase = (caseRow) => {
    console.log('Edit case:', caseRow);
    // Open edit modal or navigate to edit page
  };

  const handleCaseDocuments = (caseRow) => {
    console.log('View documents for case:', caseRow);
    // Navigate to documents page
  };

  const handleExport = (data, format) => {
    console.log('Export data:', data, 'Format:', format);
    // Implement export functionality
  };

  const renderExpandedRow = (row) => (
    <div className="expanded-row-content">
      <div className="case-details">
        <div className="detail-section">
          <h4>Case Information</h4>
          <div className="detail-grid">
            <div className="detail-item">
              <label>Court:</label>
              <span>{row.court}</span>
            </div>
            <div className="detail-item">
              <label>Jurisdiction:</label>
              <span>{row.jurisdiction}</span>
            </div>
            <div className="detail-item">
              <label>Last Activity:</label>
              <span>{row.lastActivity.toLocaleDateString()}</span>
            </div>
          </div>
        </div>
        
        <div className="detail-section">
          <h4>Tags</h4>
          <div className="case-tags">
            {row.tags.map((tag, index) => (
              <SafChip
                key={index}
                label={tag}
                variant="soft"
                color="primary"
                size="small"
              />
            ))}
          </div>
        </div>
        
        <div className="detail-section">
          <h4>Notes</h4>
          <p>{row.notes}</p>
        </div>
      </div>
    </div>
  );

  return (
    <div className="legal-case-management-demo">
      <h2>Legal Case Management System</h2>

      {/* Table Actions */}
      <div className="table-actions">
        <div className="action-group">
          <button className="action-btn primary">
            <SafIcon name="plus" /> New Case
          </button>
          <button 
            className="action-btn secondary"
            disabled={selectedCases.length === 0}
          >
            <SafIcon name="edit" /> Bulk Edit ({selectedCases.length})
          </button>
          <button 
            className="action-btn secondary"
            disabled={selectedCases.length === 0}
          >
            <SafIcon name="archive" /> Archive Selected
          </button>
        </div>
        
        <div className="view-options">
          <SafChip label="All Cases" variant="filled" color="primary" />
          <SafChip label="Active" variant="soft" color="success" />
          <SafChip label="High Priority" variant="soft" color="danger" />
          <SafChip label="My Cases" variant="soft" color="info" />
        </div>
      </div>

      {/* Main Data Table */}
      <SafDataTable
        data={caseData}
        columns={caseColumns}
        variant="default"
        size="medium"
        striped={true}
        hoverable={true}
        sortable={true}
        filterable={true}
        searchable={true}
        selectable={true}
        selectMode="multiple"
        expandable={true}
        resizable={true}
        loading={loading}
        pagination={{
          pageSize: 10,
          pageSizeOptions: [5, 10, 20, 50],
          showSizeChanger: true,
          showQuickJumper: true,
          showTotal: true,
          position: 'bottom'
        }}
        exportable={{
          formats: ['csv', 'excel', 'pdf'],
          filename: 'legal-cases',
          includeHeaders: true,
          selectedOnly: false
        }}
        stickyHeader={true}
        stickyColumns={1}
        height="600px"
        defaultSort={{ columnId: 'dateOpened', direction: 'desc' }}
        selectedRows={selectedCases}
        expandedRows={expandedRows}
        rowKey="id"
        onSort={handleSort}
        onFilter={handleFilter}
        onSearch={handleSearch}
        onSelect={handleRowSelect}
        onExpand={handleRowExpand}
        onRowClick={(row) => console.log('Row clicked:', row)}
        onRowDoubleClick={handleViewCase}
        onExport={handleExport}
        expandedRowRender={renderExpandedRow}
      />

      {/* Table Summary */}
      <div className="table-summary">
        <div className="summary-stats">
          <div className="stat-item">
            <SafIcon name="briefcase" />
            <span className="stat-value">{caseData.length}</span>
            <span className="stat-label">Total Cases</span>
          </div>
          <div className="stat-item">
            <SafIcon name="clock" />
            <span className="stat-value">
              {caseData.reduce((sum, c) => sum + c.billableHours, 0).toFixed(1)}h
            </span>
            <span className="stat-label">Total Billable Hours</span>
          </div>
          <div className="stat-item">
            <SafIcon name="dollar-sign" />
            <span className="stat-value">
              ${caseData.reduce((sum, c) => sum + c.estimatedValue, 0).toLocaleString()}
            </span>
            <span className="stat-label">Total Estimated Value</span>
          </div>
          <div className="stat-item">
            <SafIcon name="users" />
            <span className="stat-value">
              {new Set(caseData.map(c => c.assignedLawyer.id)).size}
            </span>
            <span className="stat-label">Active Lawyers</span>
          </div>
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-case-management-table.component.ts
import { Component, OnInit } from '@angular/core';

interface CaseData {
  id: string;
  caseNumber: string;
  title: string;
  type: string;
  status: string;
  priority: string;
  assignedLawyer: {
    id: string;
    name: string;
    avatar: string;
    title: string;
  };
  client: {
    name: string;
    type: string;
  };
  dateOpened: Date;
  lastActivity: Date;
  billableHours: number;
  estimatedValue: number;
  nextDeadline: Date | null;
  practiceArea: string;
  jurisdiction: string;
  court: string;
  tags: string[];
  documents: number;
  notes: string;
}

@Component({
  selector: 'app-legal-case-management-table',
  template: `
    <div class="legal-case-management-demo">
      <h2>Legal Case Management System</h2>

      <!-- Table Actions -->
      <div class="table-actions">
        <div class="action-group">
          <button class="action-btn primary">
            <saf-icon name="plus"></saf-icon> New Case
          </button>
          <button 
            class="action-btn secondary"
            [disabled]="selectedCases.length === 0">
            <saf-icon name="edit"></saf-icon> Bulk Edit ({{ selectedCases.length }})
          </button>
          <button 
            class="action-btn secondary"
            [disabled]="selectedCases.length === 0">
            <saf-icon name="archive"></saf-icon> Archive Selected
          </button>
        </div>
        
        <div class="view-options">
          <saf-chip label="All Cases" variant="filled" color="primary"></saf-chip>
          <saf-chip label="Active" variant="soft" color="success"></saf-chip>
          <saf-chip label="High Priority" variant="soft" color="danger"></saf-chip>
          <saf-chip label="My Cases" variant="soft" color="info"></saf-chip>
        </div>
      </div>

      <!-- Main Data Table -->
      <saf-data-table
        [data]="caseData"
        [columns]="caseColumns"
        variant="default"
        size="medium"
        [striped]="true"
        [hoverable]="true"
        [sortable]="true"
        [filterable]="true"
        [searchable]="true"
        [selectable]="true"
        selectMode="multiple"
        [expandable]="true"
        [resizable]="true"
        [loading]="loading"
        [pagination]="paginationConfig"
        [exportable]="exportConfig"
        [stickyHeader]="true"
        [stickyColumns]="1"
        height="600px"
        [defaultSort]="defaultSort"
        [selectedRows]="selectedCases"
        [expandedRows]="expandedRows"
        rowKey="id"
        (sort)="handleSort($event)"
        (filter)="handleFilter($event)"
        (search)="handleSearch($event)"
        (select)="handleRowSelect($event)"
        (expand)="handleRowExpand($event)"
        (rowClick)="handleRowClick($event.row)"
        (rowDoubleClick)="handleViewCase($event.row)"
        (export)="handleExport($event.data, $event.format)">
        
        <!-- Custom expanded row template -->
        <ng-template #expandedRowTemplate let-row="row">
          <div class="expanded-row-content">
            <div class="case-details">
              <div class="detail-section">
                <h4>Case Information</h4>
                <div class="detail-grid">
                  <div class="detail-item">
                    <label>Court:</label>
                    <span>{{ row.court }}</span>
                  </div>
                  <div class="detail-item">
                    <label>Jurisdiction:</label>
                    <span>{{ row.jurisdiction }}</span>
                  </div>
                  <div class="detail-item">
                    <label>Last Activity:</label>
                    <span>{{ row.lastActivity | date }}</span>
                  </div>
                </div>
              </div>
              
              <div class="detail-section">
                <h4>Tags</h4>
                <div class="case-tags">
                  <saf-chip
                    *ngFor="let tag of row.tags"
                    [label]="tag"
                    variant="soft"
                    color="primary"
                    size="small">
                  </saf-chip>
                </div>
              </div>
              
              <div class="detail-section">
                <h4>Notes</h4>
                <p>{{ row.notes }}</p>
              </div>
            </div>
          </div>
        </ng-template>
      </saf-data-table>

      <!-- Table Summary -->
      <div class="table-summary">
        <div class="summary-stats">
          <div class="stat-item">
            <saf-icon name="briefcase"></saf-icon>
            <span class="stat-value">{{ caseData.length }}</span>
            <span class="stat-label">Total Cases</span>
          </div>
          <div class="stat-item">
            <saf-icon name="clock"></saf-icon>
            <span class="stat-value">{{ totalBillableHours }}h</span>
            <span class="stat-label">Total Billable Hours</span>
          </div>
          <div class="stat-item">
            <saf-icon name="dollar-sign"></saf-icon>
            <span class="stat-value">\${{ totalEstimatedValue | number }}</span>
            <span class="stat-label">Total Estimated Value</span>
          </div>
          <div class="stat-item">
            <saf-icon name="users"></saf-icon>
            <span class="stat-value">{{ activeLawyers }}</span>
            <span class="stat-label">Active Lawyers</span>
          </div>
        </div>
      </div>
    </div>
  `
})
export class LegalCaseManagementTableComponent implements OnInit {
  caseData: CaseData[] = [];
  loading = false;
  selectedCases: CaseData[] = [];
  expandedRows: CaseData[] = [];

  paginationConfig = {
    pageSize: 10,
    pageSizeOptions: [5, 10, 20, 50],
    showSizeChanger: true,
    showQuickJumper: true,
    showTotal: true,
    position: 'bottom'
  };

  exportConfig = {
    formats: ['csv', 'excel', 'pdf'],
    filename: 'legal-cases',
    includeHeaders: true,
    selectedOnly: false
  };

  defaultSort = { columnId: 'dateOpened', direction: 'desc' };

  caseColumns = [
    {
      id: 'caseNumber',
      key: 'caseNumber',
      title: 'Case Number',
      width: 150,
      sortable: true,
      filterable: true,
      fixed: 'left'
    },
    {
      id: 'title',
      key: 'title',
      title: 'Case Title',
      width: 300,
      sortable: true,
      filterable: true
    },
    {
      id: 'status',
      key: 'status',
      title: 'Status',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'select',
      filterOptions: [
        { label: 'Active', value: 'Active' },
        { label: 'Under Review', value: 'Under Review' },
        { label: 'Closed', value: 'Closed' },
        { label: 'On Hold', value: 'On Hold' }
      ]
    },
    {
      id: 'assignedLawyer',
      key: 'assignedLawyer',
      title: 'Assigned Lawyer',
      width: 200,
      sortable: true
    },
    {
      id: 'client',
      key: 'client',
      title: 'Client',
      width: 180,
      sortable: true,
      filterable: true
    },
    {
      id: 'practiceArea',
      key: 'practiceArea',
      title: 'Practice Area',
      width: 150,
      sortable: true,
      filterable: true,
      filterType: 'select',
      filterOptions: [
        { label: 'Corporate Law', value: 'Corporate Law' },
        { label: 'Employment Law', value: 'Employment Law' },
        { label: 'Intellectual Property', value: 'Intellectual Property' },
        { label: 'Real Estate', value: 'Real Estate' }
      ]
    },
    {
      id: 'dateOpened',
      key: 'dateOpened',
      title: 'Date Opened',
      dataType: 'date',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'date'
    },
    {
      id: 'billableHours',
      key: 'billableHours',
      title: 'Billable Hours',
      dataType: 'number',
      width: 120,
      sortable: true,
      filterable: true,
      filterType: 'range',
      align: 'right'
    },
    {
      id: 'estimatedValue',
      key: 'estimatedValue',
      title: 'Est. Value',
      dataType: 'currency',
      width: 130,
      sortable: true,
      filterable: true,
      filterType: 'range',
      align: 'right'
    },
    {
      id: 'nextDeadline',
      key: 'nextDeadline',
      title: 'Next Deadline',
      dataType: 'date',
      width: 130,
      sortable: true
    },
    {
      id: 'actions',
      key: 'actions',
      title: 'Actions',
      width: 120,
      sortable: false,
      filterable: false,
      fixed: 'right'
    }
  ];

  get totalBillableHours(): number {
    return this.caseData.reduce((sum, c) => sum + c.billableHours, 0);
  }

  get totalEstimatedValue(): number {
    return this.caseData.reduce((sum, c) => sum + c.estimatedValue, 0);
  }

  get activeLawyers(): number {
    return new Set(this.caseData.map(c => c.assignedLawyer.id)).size;
  }

  ngOnInit() {
    this.loadCaseData();
  }

  loadCaseData() {
    this.loading = true;
    // Simulate API call
    setTimeout(() => {
      this.caseData = [
        {
          id: 'CASE-2024-001',
          caseNumber: 'CV-2024-001234',
          title: 'Global Corp vs. Tech Innovations LLC',
          type: 'Commercial Litigation',
          status: 'Active',
          priority: 'High',
          assignedLawyer: {
            id: 'lawyer-1',
            name: 'Sarah Johnson',
            avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
            title: 'Senior Partner'
          },
          client: {
            name: 'Global Corp Inc.',
            type: 'Corporate'
          },
          dateOpened: new Date('2024-01-15'),
          lastActivity: new Date('2024-01-28'),
          billableHours: 42.5,
          estimatedValue: 2500000,
          nextDeadline: new Date('2024-02-15'),
          practiceArea: 'Corporate Law',
          jurisdiction: 'Federal',
          court: 'U.S. District Court, Southern District of New York',
          tags: ['Contract Dispute', 'IP Rights', 'Confidential'],
          documents: 127,
          notes: 'Discovery phase ongoing. Expert witness depositions scheduled for next month.'
        }
        // Additional case data...
      ];
      this.loading = false;
    }, 1000);
  }

  handleSort(sortConfig: any) {
    console.log('Sort changed:', sortConfig);
  }

  handleFilter(filters: any) {
    console.log('Filters changed:', filters);
  }

  handleSearch(query: string) {
    console.log('Search query:', query);
  }

  handleRowSelect(selectedRows: CaseData[]) {
    this.selectedCases = selectedRows;
    console.log('Selected cases:', selectedRows);
  }

  handleRowExpand(expandedRows: CaseData[]) {
    this.expandedRows = expandedRows;
    console.log('Expanded rows:', expandedRows);
  }

  handleRowClick(row: CaseData) {
    console.log('Row clicked:', row);
  }

  handleViewCase(caseRow: CaseData) {
    console.log('View case:', caseRow);
  }

  handleExport(data: CaseData[], format: string) {
    console.log('Export data:', data, 'Format:', format);
  }
}
```

## Best Practices

1. **Performance Optimization**
   - Use virtualization for large datasets (1000+ rows)
   - Implement server-side pagination and filtering
   - Lazy load data and optimize re-renders
   - Cache frequently accessed data

2. **User Experience**
   - Provide clear visual feedback for all interactions
   - Implement keyboard navigation throughout
   - Show loading states during data operations
   - Use appropriate column widths and responsive design

3. **Data Management**
   - Implement efficient sorting and filtering algorithms
   - Handle real-time data updates gracefully
   - Provide data validation and error handling
   - Support data export in multiple formats

4. **Accessibility**
   - Use semantic table markup
   - Provide keyboard navigation for all features
   - Support screen readers with proper ARIA labels
   - Ensure sufficient color contrast for all elements

5. **Content Organization**
   - Group related columns logically
   - Use consistent data formatting
   - Implement progressive disclosure for complex data
   - Provide contextual actions and tooltips

## Accessibility Considerations

1. **Screen Reader Support**
   - Use proper table markup with headers
   - Provide clear column descriptions
   - Announce sorting and filtering changes
   - Support row selection announcements

2. **Keyboard Navigation**
   - Tab navigation through interactive elements
   - Arrow key navigation within table cells
   - Keyboard shortcuts for common actions
   - Accessible dropdown menus and modals

3. **Visual Accessibility**
   - High contrast mode support
   - Sufficient color contrast for all text
   - Clear focus indicators
   - Scalable text and interface elements

4. **Responsive Design**
   - Mobile-friendly table layouts
   - Touch-friendly interactive elements
   - Adaptive column display for small screens
   - Collapsible detail views on mobile

## Related Components

- **SafDataTableColumn**: Individual column configuration
- **SafDataTablePagination**: Table pagination controls
- **SafIcon**: Icons for actions and indicators
- **SafChip**: Status indicators and tags
- **SafAvatar**: User profile displays

## Notes

- Data table supports both client-side and server-side data operations
- Built-in virtualization handles large datasets efficiently
- Comprehensive export functionality with multiple format support
- Real-time data updates with WebSocket integration capabilities
- Advanced filtering with custom filter components
- Column resizing and reordering with persistent preferences
- Mobile-responsive design with adaptive layouts
- Comprehensive keyboard and screen reader accessibility support
