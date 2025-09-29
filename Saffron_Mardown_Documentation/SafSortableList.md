# SafSortableList

## Overview

SafSortableList is an interactive component that provides drag-and-drop functionality for reordering list items. It supports touch and mouse interactions, customizable drag handles, visual feedback during sorting, and accessibility features for keyboard-only users with comprehensive sorting capabilities.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `SortableItem[]` | `[]` | Array of sortable list items |
| `disabled` | `boolean` | `false` | Disable all sorting functionality |
| `axis` | `'vertical' \| 'horizontal' \| 'both'` | `'vertical'` | Allowed drag directions |
| `lockAxis` | `boolean` | `true` | Lock dragging to specified axis |
| `dragHandle` | `boolean \| string` | `false` | Enable drag handle or CSS selector |
| `dragDelay` | `number` | `0` | Delay before drag starts (ms) |
| `dragDistance` | `number` | `5` | Distance threshold to start drag |
| `ghost` | `boolean` | `true` | Show ghost/placeholder during drag |
| `animation` | `boolean` | `true` | Enable sort animations |
| `animationDuration` | `number` | `200` | Animation duration in ms |
| `dropIndicator` | `boolean` | `true` | Show drop indicator |
| `constraints` | `SortConstraints` | - | Sorting constraints and rules |
| `multiSelect` | `boolean` | `false` | Allow multiple item selection |
| `groupBy` | `string \| ((item: SortableItem) => string)` | - | Group items for constrained sorting |
| `onSort` | `(oldIndex: number, newIndex: number) => void` | - | Fired when items are reordered |
| `onDragStart` | `(item: SortableItem, index: number) => void` | - | Fired when drag starts |
| `onDragEnd` | `(item: SortableItem, index: number) => void` | - | Fired when drag ends |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### SortableItem Interface

```typescript
interface SortableItem {
  id: string | number;
  content: ReactNode;
  disabled?: boolean;
  group?: string;
  data?: any;
}

interface SortConstraints {
  allowedGroups?: string[];
  preventSort?: (fromIndex: number, toIndex: number) => boolean;
  validateDrop?: (item: SortableItem, targetIndex: number) => boolean;
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onSort` | `(event: SortEvent) => void` | Fired when items are reordered |
| `onDragStart` | `(event: DragStartEvent) => void` | Fired when drag operation begins |
| `onDragMove` | `(event: DragMoveEvent) => void` | Fired during drag movement |
| `onDragEnd` | `(event: DragEndEvent) => void` | Fired when drag operation ends |
| `onSelectionChange` | `(selectedIds: string[]) => void` | Fired when selection changes |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `SortableItem[]` | `[]` | Array of sortable list items |
| `disabled` | `boolean` | `false` | Disable all sorting functionality |
| `axis` | `'vertical' \| 'horizontal' \| 'both'` | `'vertical'` | Allowed drag directions |
| `lockAxis` | `boolean` | `true` | Lock dragging to specified axis |
| `dragHandle` | `boolean \| string` | `false` | Enable drag handle or CSS selector |
| `dragDelay` | `number` | `0` | Delay before drag starts (ms) |
| `dragDistance` | `number` | `5` | Distance threshold to start drag |
| `ghost` | `boolean` | `true` | Show ghost/placeholder during drag |
| `animation` | `boolean` | `true` | Enable sort animations |
| `animationDuration` | `number` | `200` | Animation duration in ms |
| `dropIndicator` | `boolean` | `true` | Show drop indicator |
| `multiSelect` | `boolean` | `false` | Allow multiple item selection |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `sort` | `EventEmitter<SortEvent>` | Fired when items are reordered |
| `dragStart` | `EventEmitter<DragStartEvent>` | Fired when drag operation begins |
| `dragMove` | `EventEmitter<DragMoveEvent>` | Fired during drag movement |
| `dragEnd` | `EventEmitter<DragEndEvent>` | Fired when drag operation ends |
| `selectionChange` | `EventEmitter<string[]>` | Fired when selection changes |

## Usage Examples

### Basic Sortable List

```typescript
// React
const BasicSortableList = ({ items, onItemsChange }) => {
  const handleSort = ({ oldIndex, newIndex }) => {
    const newItems = [...items];
    const [movedItem] = newItems.splice(oldIndex, 1);
    newItems.splice(newIndex, 0, movedItem);
    onItemsChange(newItems);
  };

  const sortableItems = items.map(item => ({
    id: item.id,
    content: (
      <div className="list-item">
        <span className="item-title">{item.title}</span>
        <span className="item-description">{item.description}</span>
      </div>
    ),
    data: item
  }));

  return (
    <SafSortableList 
      items={sortableItems}
      onSort={handleSort}
      axis="vertical"
      animation
    />
  );
};
```

```html
<!-- Angular -->
<saf-sortable-list 
  [items]="sortableItems"
  axis="vertical"
  [animation]="true"
  (sort)="onSort($event)">
</saf-sortable-list>
```

### Sortable List with Drag Handles

```typescript
// React
const SortableListWithHandles = ({ tasks, onTasksReorder }) => {
  const handleSort = ({ oldIndex, newIndex }) => {
    const reorderedTasks = [...tasks];
    const [movedTask] = reorderedTasks.splice(oldIndex, 1);
    reorderedTasks.splice(newIndex, 0, movedTask);
    onTasksReorder(reorderedTasks);
  };

  const sortableItems = tasks.map(task => ({
    id: task.id,
    content: (
      <div className="task-item">
        <div className="drag-handle" data-drag-handle>
          <SafIcon name="menu" />
        </div>
        <div className="task-content">
          <h4>{task.title}</h4>
          <p>{task.description}</p>
          <div className="task-meta">
            <SafBadge variant={task.priority}>{task.priority}</SafBadge>
            <span className="due-date">{task.dueDate}</span>
          </div>
        </div>
        <div className="task-actions">
          <SafButton 
            variant="ghost" 
            size="small"
            icon={<SafIcon name="edit" />}
          />
          <SafButton 
            variant="ghost" 
            size="small"
            icon={<SafIcon name="trash" />}
          />
        </div>
      </div>
    ),
    data: task
  }));

  return (
    <SafSortableList 
      items={sortableItems}
      onSort={handleSort}
      dragHandle="[data-drag-handle]"
      ghost
      dropIndicator
    />
  );
};
```

### Horizontal Sortable List

```typescript
// React
const HorizontalSortableList = ({ tabs, onTabsReorder }) => {
  const handleSort = ({ oldIndex, newIndex }) => {
    const reorderedTabs = [...tabs];
    const [movedTab] = reorderedTabs.splice(oldIndex, 1);
    reorderedTabs.splice(newIndex, 0, movedTab);
    onTabsReorder(reorderedTabs);
  };

  const sortableItems = tabs.map(tab => ({
    id: tab.id,
    content: (
      <div className="tab-item">
        <SafIcon name={tab.icon} />
        <span>{tab.label}</span>
        {tab.closable && (
          <SafButton 
            variant="ghost"
            size="small"
            icon={<SafIcon name="x" />}
            onClick={() => onCloseTab(tab.id)}
          />
        )}
      </div>
    ),
    disabled: tab.pinned,
    data: tab
  }));

  return (
    <div className="tab-bar">
      <SafSortableList 
        items={sortableItems}
        onSort={handleSort}
        axis="horizontal"
        animation
        dragDistance={10}
      />
    </div>
  );
};
```

### Grouped Sortable List

```typescript
// React
const GroupedSortableList = ({ items, onItemsChange }) => {
  const handleSort = ({ oldIndex, newIndex, item }) => {
    // Prevent moving between different groups
    const oldGroup = items[oldIndex].group;
    const newGroup = items[newIndex]?.group;
    
    if (oldGroup !== newGroup) {
      return false; // Prevent sort
    }
    
    const newItems = [...items];
    const [movedItem] = newItems.splice(oldIndex, 1);
    newItems.splice(newIndex, 0, movedItem);
    onItemsChange(newItems);
  };

  const constraints = {
    validateDrop: (item, targetIndex) => {
      const targetItem = items[targetIndex];
      return !targetItem || item.group === targetItem.group;
    }
  };

  const sortableItems = items.map(item => ({
    id: item.id,
    content: (
      <div className={`grouped-item group-${item.group}`}>
        <div className="item-header">
          <SafIcon name={item.icon} />
          <span className="item-title">{item.title}</span>
          <SafBadge variant="outline">{item.group}</SafBadge>
        </div>
        <p className="item-description">{item.description}</p>
      </div>
    ),
    group: item.group,
    data: item
  }));

  return (
    <div className="grouped-sortable-list">
      <SafSortableList 
        items={sortableItems}
        onSort={handleSort}
        constraints={constraints}
        groupBy="group"
        dropIndicator
      />
    </div>
  );
};
```

### Multi-Select Sortable List

```typescript
// React
const MultiSelectSortableList = ({ files, onFilesChange }) => {
  const [selectedItems, setSelectedItems] = useState([]);

  const handleSort = ({ oldIndex, newIndex }) => {
    const newFiles = [...files];
    const [movedFile] = newFiles.splice(oldIndex, 1);
    newFiles.splice(newIndex, 0, movedFile);
    onFilesChange(newFiles);
  };

  const handleSelectionChange = (selectedIds) => {
    setSelectedItems(selectedIds);
  };

  const handleBulkAction = (action) => {
    const selectedFiles = files.filter(file => 
      selectedItems.includes(file.id)
    );
    
    switch (action) {
      case 'delete':
        onFilesChange(files.filter(file => 
          !selectedItems.includes(file.id)
        ));
        setSelectedItems([]);
        break;
      case 'download':
        // Handle bulk download
        break;
    }
  };

  const sortableItems = files.map(file => ({
    id: file.id,
    content: (
      <div className="file-item">
        <SafCheckbox 
          checked={selectedItems.includes(file.id)}
          onChange={(checked) => {
            if (checked) {
              setSelectedItems([...selectedItems, file.id]);
            } else {
              setSelectedItems(selectedItems.filter(id => id !== file.id));
            }
          }}
        />
        <div className="file-icon">
          <SafIcon name={getFileIcon(file.type)} />
        </div>
        <div className="file-info">
          <span className="file-name">{file.name}</span>
          <span className="file-size">{formatFileSize(file.size)}</span>
        </div>
        <div className="file-date">
          {formatDate(file.modifiedDate)}
        </div>
      </div>
    ),
    data: file
  }));

  return (
    <div className="file-manager">
      {selectedItems.length > 0 && (
        <div className="bulk-actions">
          <span>{selectedItems.length} items selected</span>
          <SafButton 
            variant="outline"
            size="small"
            onClick={() => handleBulkAction('download')}
          >
            Download
          </SafButton>
          <SafButton 
            variant="danger"
            size="small"
            onClick={() => handleBulkAction('delete')}
          >
            Delete
          </SafButton>
        </div>
      )}
      
      <SafSortableList 
        items={sortableItems}
        onSort={handleSort}
        onSelectionChange={handleSelectionChange}
        multiSelect
        dragHandle=".file-icon"
      />
    </div>
  );
};
```

### Nested Sortable Lists

```typescript
// React
const NestedSortableList = ({ categories, onCategoriesChange }) => {
  const handleCategorySort = ({ oldIndex, newIndex }) => {
    const newCategories = [...categories];
    const [movedCategory] = newCategories.splice(oldIndex, 1);
    newCategories.splice(newIndex, 0, movedCategory);
    onCategoriesChange(newCategories);
  };

  const handleItemSort = (categoryId, { oldIndex, newIndex }) => {
    const newCategories = categories.map(category => {
      if (category.id === categoryId) {
        const newItems = [...category.items];
        const [movedItem] = newItems.splice(oldIndex, 1);
        newItems.splice(newIndex, 0, movedItem);
        return { ...category, items: newItems };
      }
      return category;
    });
    onCategoriesChange(newCategories);
  };

  const categoryItems = categories.map(category => ({
    id: category.id,
    content: (
      <div className="category-container">
        <div className="category-header">
          <div className="drag-handle" data-drag-handle>
            <SafIcon name="menu" />
          </div>
          <h3>{category.name}</h3>
          <SafBadge>{category.items.length}</SafBadge>
        </div>
        
        <div className="category-items">
          <SafSortableList 
            items={category.items.map(item => ({
              id: item.id,
              content: (
                <div className="nested-item">
                  <SafIcon name="drag-dots" className="item-handle" />
                  <span>{item.name}</span>
                </div>
              ),
              data: item
            }))}
            onSort={(event) => handleItemSort(category.id, event)}
            dragHandle=".item-handle"
            axis="vertical"
          />
        </div>
      </div>
    ),
    data: category
  }));

  return (
    <div className="nested-sortable">
      <SafSortableList 
        items={categoryItems}
        onSort={handleCategorySort}
        dragHandle="[data-drag-handle]"
        axis="vertical"
        animation
      />
    </div>
  );
};
```

### Sortable Kanban Board

```typescript
// React
const SortableKanbanBoard = ({ columns, onColumnsChange }) => {
  const handleColumnSort = ({ oldIndex, newIndex }) => {
    const newColumns = [...columns];
    const [movedColumn] = newColumns.splice(oldIndex, 1);
    newColumns.splice(newIndex, 0, movedColumn);
    onColumnsChange(newColumns);
  };

  const handleCardSort = (columnId, { oldIndex, newIndex }) => {
    const newColumns = columns.map(column => {
      if (column.id === columnId) {
        const newCards = [...column.cards];
        const [movedCard] = newCards.splice(oldIndex, 1);
        newCards.splice(newIndex, 0, movedCard);
        return { ...column, cards: newCards };
      }
      return column;
    });
    onColumnsChange(newColumns);
  };

  const columnItems = columns.map(column => ({
    id: column.id,
    content: (
      <div className="kanban-column">
        <div className="column-header">
          <h3>{column.title}</h3>
          <SafBadge>{column.cards.length}</SafBadge>
          <div className="column-handle" data-column-handle>
            <SafIcon name="more-vertical" />
          </div>
        </div>
        
        <div className="column-cards">
          <SafSortableList 
            items={column.cards.map(card => ({
              id: card.id,
              content: (
                <div className="kanban-card">
                  <h4>{card.title}</h4>
                  <p>{card.description}</p>
                  <div className="card-meta">
                    <SafAvatar 
                      src={card.assignee.avatar}
                      name={card.assignee.name}
                      size="small"
                    />
                    <SafBadge variant={card.priority}>
                      {card.priority}
                    </SafBadge>
                  </div>
                </div>
              ),
              data: card
            }))}
            onSort={(event) => handleCardSort(column.id, event)}
            axis="vertical"
            ghost
            animation
          />
        </div>
        
        <SafButton 
          variant="ghost"
          size="small"
          fullWidth
          icon={<SafIcon name="plus" />}
        >
          Add Card
        </SafButton>
      </div>
    ),
    data: column
  }));

  return (
    <div className="kanban-board">
      <SafSortableList 
        items={columnItems}
        onSort={handleColumnSort}
        dragHandle="[data-column-handle]"
        axis="horizontal"
        animation
        dragDelay={100}
      />
    </div>
  );
};
```

### Mobile-Optimized Sortable List

```typescript
// React
const MobileSortableList = ({ items, onItemsChange }) => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);
  const [draggedItem, setDraggedItem] = useState(null);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  const handleDragStart = ({ item, index }) => {
    setDraggedItem(item);
    
    // Provide haptic feedback on mobile
    if (navigator.vibrate) {
      navigator.vibrate(50);
    }
  };

  const handleDragEnd = ({ item, index }) => {
    setDraggedItem(null);
  };

  const handleSort = ({ oldIndex, newIndex }) => {
    const newItems = [...items];
    const [movedItem] = newItems.splice(oldIndex, 1);
    newItems.splice(newIndex, 0, movedItem);
    onItemsChange(newItems);
  };

  const sortableItems = items.map(item => ({
    id: item.id,
    content: (
      <div className={`mobile-list-item ${draggedItem?.id === item.id ? 'dragging' : ''}`}>
        <div className="mobile-drag-handle" data-drag-handle>
          <SafIcon name="grip-vertical" />
        </div>
        <div className="item-content">
          <div className="item-header">
            <h4>{item.title}</h4>
            <span className="item-time">{item.time}</span>
          </div>
          <p className="item-description">{item.description}</p>
        </div>
        <div className="item-actions">
          <SafButton 
            variant="ghost"
            size="small"
            icon={<SafIcon name="more-horizontal" />}
          />
        </div>
      </div>
    ),
    data: item
  }));

  return (
    <div className={`mobile-sortable ${isMobile ? 'mobile' : 'desktop'}`}>
      <SafSortableList 
        items={sortableItems}
        onSort={handleSort}
        onDragStart={handleDragStart}
        onDragEnd={handleDragEnd}
        dragHandle="[data-drag-handle]"
        dragDelay={isMobile ? 200 : 0}
        dragDistance={isMobile ? 10 : 5}
        animation
        animationDuration={isMobile ? 150 : 200}
      />
    </div>
  );
};
```

### Accessibility-Enhanced Sortable List

```typescript
// React
const AccessibleSortableList = ({ 
  items, 
  onItemsChange, 
  label = "Sortable list" 
}) => {
  const [announcements, setAnnouncements] = useState('');
  const [selectedIndex, setSelectedIndex] = useState(-1);

  const handleSort = ({ oldIndex, newIndex }) => {
    const newItems = [...items];
    const [movedItem] = newItems.splice(oldIndex, 1);
    newItems.splice(newIndex, 0, movedItem);
    onItemsChange(newItems);
    
    // Announce the change
    const announcement = `Moved ${movedItem.title} from position ${oldIndex + 1} to position ${newIndex + 1}`;
    setAnnouncements(announcement);
    
    setTimeout(() => setAnnouncements(''), 1000);
  };

  const handleKeyDown = (event, index) => {
    switch (event.key) {
      case 'ArrowUp':
        if (index > 0) {
          handleSort({ oldIndex: index, newIndex: index - 1 });
        }
        break;
      case 'ArrowDown':
        if (index < items.length - 1) {
          handleSort({ oldIndex: index, newIndex: index + 1 });
        }
        break;
      case 'Enter':
      case ' ':
        setSelectedIndex(selectedIndex === index ? -1 : index);
        break;
    }
  };

  const sortableItems = items.map((item, index) => ({
    id: item.id,
    content: (
      <div 
        className={`accessible-item ${selectedIndex === index ? 'selected' : ''}`}
        role="button"
        tabIndex={0}
        onKeyDown={(e) => handleKeyDown(e, index)}
        aria-label={`${item.title}, position ${index + 1} of ${items.length}. Use arrow keys to reorder.`}
        aria-describedby={`item-description-${item.id}`}
      >
        <div className="item-content">
          <h4>{item.title}</h4>
          <p id={`item-description-${item.id}`}>{item.description}</p>
          <span className="position-indicator">
            Position {index + 1} of {items.length}
          </span>
        </div>
        <div className="accessibility-hint">
          <SafIcon name="move" />
          <span className="sr-only">Use arrow keys to reorder</span>
        </div>
      </div>
    ),
    data: item
  }));

  return (
    <div className="accessible-sortable-list">
      <div 
        role="application"
        aria-label={label}
        aria-describedby="sortable-instructions"
      >
        <div id="sortable-instructions" className="sr-only">
          Use arrow keys to reorder items. Press Enter or Space to select an item.
        </div>
        
        <SafSortableList 
          items={sortableItems}
          onSort={handleSort}
          animation
        />
        
        <div 
          aria-live="assertive"
          aria-atomic="true"
          className="sr-only"
        >
          {announcements}
        </div>
      </div>
    </div>
  );
};
```

## Best Practices

### User Experience
- **Visual Feedback**: Provide clear feedback during drag operations
- **Handle Placement**: Use consistent drag handle placement and styling
- **Animation**: Use smooth animations for better user experience
- **Touch Support**: Optimize for touch devices with appropriate delays

### Accessibility
- **Keyboard Navigation**: Support arrow keys for reordering items
- **Screen Reader Support**: Provide clear announcements for changes
- **Focus Management**: Maintain proper focus during interactions
- **Alternative Methods**: Provide non-drag methods for reordering

### Performance
- **Virtual Scrolling**: Use for large lists with many items
- **Debounced Updates**: Debounce frequent sort operations
- **Memory Management**: Clean up event listeners properly
- **Efficient Rendering**: Minimize re-renders during drag operations

### Data Management
- **State Updates**: Update state efficiently after sort operations
- **Constraints**: Implement proper sorting constraints when needed
- **Persistence**: Handle saving sorted order to backend
- **Validation**: Validate sort operations before applying changes

## Accessibility Considerations

- Uses proper ARIA roles and attributes for sortable functionality
- Supports keyboard navigation with arrow keys for reordering
- Provides screen reader announcements for sort operations
- Maintains proper focus management during interactions
- Includes alternative methods for users who cannot drag
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafSortableListItem**: Individual sortable list item component
- **SafList**: Basic list component for non-sortable content
- **SafDataGrid**: Sortable table component
- **SafTree**: Hierarchical sortable tree component

## Notes

- SafSortableList automatically handles touch and mouse interactions
- The component supports both controlled and uncontrolled usage patterns
- Drag handles can be customized using CSS selectors
- Animation performance is optimized for smooth interactions
- The component works with nested sortable lists
- Constraints allow for complex sorting rules and validation
- Mobile optimizations provide touch-friendly drag interactions
- Accessibility features ensure usability for keyboard-only users
