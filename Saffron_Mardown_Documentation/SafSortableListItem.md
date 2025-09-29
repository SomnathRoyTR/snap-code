# SafSortableListItem

## Overview

SafSortableListItem is an interactive component that represents an individual draggable item within a sortable list. It provides drag-and-drop functionality, visual feedback during sorting operations, and accessibility support with customizable drag handles, selection states, and content rendering.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string \| number` | - | Unique identifier for the item |
| `index` | `number` | - | Current position in the list |
| `content` | `ReactNode` | - | Item content to display |
| `data` | `any` | - | Associated data object |
| `disabled` | `boolean` | `false` | Disable dragging for this item |
| `selected` | `boolean` | `false` | Item selection state |
| `dragging` | `boolean` | `false` | Currently being dragged |
| `dragHandle` | `boolean \| ReactElement` | `false` | Show drag handle or custom handle |
| `dragHandleSelector` | `string` | - | CSS selector for drag handle |
| `ghost` | `boolean` | `true` | Show ghost/placeholder when dragging |
| `animation` | `boolean` | `true` | Enable drag animations |
| `axis` | `'horizontal' \| 'vertical' \| 'both'` | `'vertical'` | Allowed drag directions |
| `constraints` | `DragConstraints` | - | Drag constraints and validation |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### DragConstraints Interface

```typescript
interface DragConstraints {
  allowDrag?: boolean;
  preventDrop?: (targetIndex: number) => boolean;
  validateMove?: (fromIndex: number, toIndex: number) => boolean;
  snapToGrid?: { x: number; y: number };
  boundary?: 'parent' | HTMLElement | string;
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onDragStart` | `(event: DragStartEvent) => void` | Fired when drag starts |
| `onDragMove` | `(event: DragMoveEvent) => void` | Fired during drag movement |
| `onDragEnd` | `(event: DragEndEvent) => void` | Fired when drag ends |
| `onSelect` | `(selected: boolean) => void` | Fired when selection changes |
| `onClick` | `(event: MouseEvent) => void` | Fired when item is clicked |
| `onFocus` | `(event: FocusEvent) => void` | Fired when item receives focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string \| number` | - | Unique identifier for the item |
| `index` | `number` | - | Current position in the list |
| `data` | `any` | - | Associated data object |
| `disabled` | `boolean` | `false` | Disable dragging for this item |
| `selected` | `boolean` | `false` | Item selection state |
| `dragging` | `boolean` | `false` | Currently being dragged |
| `dragHandle` | `boolean` | `false` | Show default drag handle |
| `dragHandleSelector` | `string` | - | CSS selector for drag handle |
| `ghost` | `boolean` | `true` | Show ghost/placeholder when dragging |
| `animation` | `boolean` | `true` | Enable drag animations |
| `axis` | `'horizontal' \| 'vertical' \| 'both'` | `'vertical'` | Allowed drag directions |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `dragStart` | `EventEmitter<DragStartEvent>` | Fired when drag starts |
| `dragMove` | `EventEmitter<DragMoveEvent>` | Fired during drag movement |
| `dragEnd` | `EventEmitter<DragEndEvent>` | Fired when drag ends |
| `selectionChange` | `EventEmitter<boolean>` | Fired when selection changes |
| `itemClick` | `EventEmitter<MouseEvent>` | Fired when item is clicked |
| `itemFocus` | `EventEmitter<FocusEvent>` | Fired when item receives focus |

## Usage Examples

### Basic Sortable Item

```typescript
// React
const BasicSortableItem = ({ item, index, onDragEnd }) => {
  const handleDragEnd = (event) => {
    onDragEnd({
      id: item.id,
      oldIndex: index,
      newIndex: event.newIndex,
      data: item
    });
  };

  return (
    <SafSortableListItem 
      id={item.id}
      index={index}
      data={item}
      onDragEnd={handleDragEnd}
      content={
        <div className="basic-item">
          <h4>{item.title}</h4>
          <p>{item.description}</p>
        </div>
      }
    />
  );
};
```

```html
<!-- Angular -->
<saf-sortable-list-item 
  [id]="item.id"
  [index]="index"
  [data]="item"
  (dragEnd)="onDragEnd($event)">
  
  <div class="basic-item">
    <h4>{{ item.title }}</h4>
    <p>{{ item.description }}</p>
  </div>
</saf-sortable-list-item>
```

### Item with Drag Handle

```typescript
// React
const ItemWithDragHandle = ({ task, index, onTaskMove }) => {
  const [isDragging, setIsDragging] = useState(false);

  const handleDragStart = () => {
    setIsDragging(true);
  };

  const handleDragEnd = (event) => {
    setIsDragging(false);
    onTaskMove(event);
  };

  return (
    <SafSortableListItem 
      id={task.id}
      index={index}
      data={task}
      dragging={isDragging}
      onDragStart={handleDragStart}
      onDragEnd={handleDragEnd}
      dragHandleSelector=".drag-handle"
      content={
        <div className="task-item">
          <div className="drag-handle">
            <SafIcon name="grip-vertical" />
          </div>
          
          <div className="task-content">
            <div className="task-header">
              <h4>{task.title}</h4>
              <SafBadge variant={task.priority.toLowerCase()}>
                {task.priority}
              </SafBadge>
            </div>
            
            <p className="task-description">{task.description}</p>
            
            <div className="task-meta">
              <SafAvatar 
                src={task.assignee.avatar}
                name={task.assignee.name}
                size="small"
              />
              <span className="due-date">{task.dueDate}</span>
            </div>
          </div>
          
          <div className="task-actions">
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name="edit" />}
              onClick={() => onEditTask(task.id)}
            />
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name="trash" />}
              onClick={() => onDeleteTask(task.id)}
            />
          </div>
        </div>
      }
    />
  );
};
```

### Selectable Sortable Item

```typescript
// React
const SelectableSortableItem = ({ 
  file, 
  index, 
  selected, 
  onSelectionChange,
  onMove 
}) => {
  const [isHovered, setIsHovered] = useState(false);

  const handleClick = (event) => {
    if (event.ctrlKey || event.metaKey) {
      onSelectionChange(!selected);
    }
  };

  const getFileIcon = (fileType) => {
    const iconMap = {
      'image': 'image',
      'document': 'file-text',
      'video': 'video',
      'audio': 'music',
      'archive': 'archive'
    };
    return iconMap[fileType] || 'file';
  };

  return (
    <SafSortableListItem 
      id={file.id}
      index={index}
      data={file}
      selected={selected}
      onClick={handleClick}
      onDragEnd={onMove}
      dragHandle={
        <div className="file-drag-handle">
          <SafIcon name="move" />
        </div>
      }
      content={
        <div 
          className={`file-item ${selected ? 'selected' : ''} ${isHovered ? 'hovered' : ''}`}
          onMouseEnter={() => setIsHovered(true)}
          onMouseLeave={() => setIsHovered(false)}
        >
          <SafCheckbox 
            checked={selected}
            onChange={onSelectionChange}
            className="file-checkbox"
          />
          
          <div className="file-icon">
            <SafIcon name={getFileIcon(file.type)} size="large" />
          </div>
          
          <div className="file-info">
            <h4 className="file-name">{file.name}</h4>
            <div className="file-details">
              <span className="file-size">{formatFileSize(file.size)}</span>
              <span className="file-date">{formatDate(file.modifiedDate)}</span>
            </div>
          </div>
          
          <div className="file-actions">
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name="download" />}
              onClick={() => onDownloadFile(file.id)}
            />
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name="more-horizontal" />}
              onClick={() => onShowFileMenu(file.id)}
            />
          </div>
        </div>
      }
    />
  );
};
```

### Card-Style Sortable Item

```typescript
// React
const CardStyleSortableItem = ({ card, index, onCardMove }) => {
  const [isDragging, setIsDragging] = useState(false);

  const handleDragStart = () => {
    setIsDragging(true);
    
    // Provide haptic feedback
    if (navigator.vibrate) {
      navigator.vibrate(50);
    }
  };

  const handleDragEnd = (event) => {
    setIsDragging(false);
    onCardMove(event);
  };

  const getPriorityColor = (priority) => {
    const colors = {
      high: 'red',
      medium: 'orange',
      low: 'green'
    };
    return colors[priority] || 'gray';
  };

  return (
    <SafSortableListItem 
      id={card.id}
      index={index}
      data={card}
      dragging={isDragging}
      onDragStart={handleDragStart}
      onDragEnd={handleDragEnd}
      ghost
      animation
      content={
        <div className={`kanban-card ${isDragging ? 'dragging' : ''}`}>
          <div className="card-header">
            <h4 className="card-title">{card.title}</h4>
            <div 
              className="priority-indicator"
              style={{ backgroundColor: getPriorityColor(card.priority) }}
            />
          </div>
          
          <p className="card-description">{card.description}</p>
          
          {card.tags && (
            <div className="card-tags">
              {card.tags.map(tag => (
                <SafBadge 
                  key={tag}
                  variant="outline"
                  size="small"
                >
                  {tag}
                </SafBadge>
              ))}
            </div>
          )}
          
          <div className="card-footer">
            <div className="card-assignees">
              {card.assignees.map(assignee => (
                <SafAvatar 
                  key={assignee.id}
                  src={assignee.avatar}
                  name={assignee.name}
                  size="small"
                />
              ))}
            </div>
            
            <div className="card-meta">
              {card.dueDate && (
                <span className="due-date">
                  <SafIcon name="calendar" size="small" />
                  {formatDate(card.dueDate)}
                </span>
              )}
              
              {card.comments > 0 && (
                <span className="comments">
                  <SafIcon name="message-circle" size="small" />
                  {card.comments}
                </span>
              )}
            </div>
          </div>
        </div>
      }
    />
  );
};
```

### Constrained Sortable Item

```typescript
// React
const ConstrainedSortableItem = ({ 
  item, 
  index, 
  constraints,
  onMove 
}) => {
  const validateMove = (fromIndex, toIndex) => {
    // Check if move is allowed based on item type
    if (item.type === 'header') {
      return false; // Headers cannot be moved
    }
    
    // Check group constraints
    if (item.group && constraints.groupBy) {
      const targetItem = constraints.items[toIndex];
      if (targetItem && targetItem.group !== item.group) {
        return false;
      }
    }
    
    return true;
  };

  const itemConstraints = {
    allowDrag: !item.locked,
    validateMove,
    preventDrop: (targetIndex) => {
      const targetItem = constraints.items[targetIndex];
      return targetItem?.locked || targetItem?.type === 'separator';
    }
  };

  return (
    <SafSortableListItem 
      id={item.id}
      index={index}
      data={item}
      disabled={item.locked}
      constraints={itemConstraints}
      onDragEnd={onMove}
      content={
        <div className={`constrained-item item-type-${item.type}`}>
          {item.locked && (
            <div className="lock-indicator">
              <SafIcon name="lock" size="small" />
            </div>
          )}
          
          <div className="item-content">
            <h4>{item.title}</h4>
            {item.description && <p>{item.description}</p>}
            
            {item.group && (
              <SafBadge variant="outline" size="small">
                {item.group}
              </SafBadge>
            )}
          </div>
          
          {!item.locked && (
            <div className="drag-indicator">
              <SafIcon name="grip-vertical" />
            </div>
          )}
        </div>
      }
    />
  );
};
```

### Horizontal Sortable Item

```typescript
// React
const HorizontalSortableItem = ({ tab, index, onTabReorder }) => {
  const [isActive, setIsActive] = useState(tab.active);
  const [isDragging, setIsDragging] = useState(false);

  const handleDragStart = () => {
    setIsDragging(true);
  };

  const handleDragEnd = (event) => {
    setIsDragging(false);
    onTabReorder(event);
  };

  const handleTabClick = () => {
    if (!isDragging) {
      onTabSelect(tab.id);
    }
  };

  return (
    <SafSortableListItem 
      id={tab.id}
      index={index}
      data={tab}
      axis="horizontal"
      dragging={isDragging}
      disabled={tab.pinned}
      onDragStart={handleDragStart}
      onDragEnd={handleDragEnd}
      onClick={handleTabClick}
      content={
        <div className={`tab-item ${isActive ? 'active' : ''} ${isDragging ? 'dragging' : ''}`}>
          {tab.icon && (
            <SafIcon name={tab.icon} size="small" />
          )}
          
          <span className="tab-label">{tab.label}</span>
          
          {tab.hasChanges && (
            <div className="changes-indicator" />
          )}
          
          {tab.closable && !tab.pinned && (
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name="x" />}
              onClick={(e) => {
                e.stopPropagation();
                onTabClose(tab.id);
              }}
              className="tab-close"
            />
          )}
          
          {tab.pinned && (
            <SafIcon name="pin" size="small" className="pin-indicator" />
          )}
        </div>
      }
    />
  );
};
```

### Nested Sortable Item

```typescript
// React
const NestedSortableItem = ({ 
  category, 
  index, 
  onCategoryMove,
  onItemMove 
}) => {
  const [isExpanded, setIsExpanded] = useState(category.expanded);
  const [isDragging, setIsDragging] = useState(false);

  const handleCategoryDragEnd = (event) => {
    setIsDragging(false);
    onCategoryMove(event);
  };

  return (
    <SafSortableListItem 
      id={category.id}
      index={index}
      data={category}
      dragging={isDragging}
      onDragStart={() => setIsDragging(true)}
      onDragEnd={handleCategoryDragEnd}
      dragHandleSelector=".category-handle"
      content={
        <div className="nested-category">
          <div className="category-header">
            <div className="category-handle">
              <SafIcon name="grip-vertical" />
            </div>
            
            <SafButton 
              variant="ghost"
              size="small"
              icon={<SafIcon name={isExpanded ? 'chevron-down' : 'chevron-right'} />}
              onClick={() => setIsExpanded(!isExpanded)}
            />
            
            <h3 className="category-title">{category.name}</h3>
            
            <SafBadge variant="outline">
              {category.items.length}
            </SafBadge>
          </div>
          
          {isExpanded && (
            <div className="category-items">
              <SafSortableList 
                items={category.items.map(item => ({
                  id: item.id,
                  content: (
                    <div className="nested-item">
                      <SafIcon name="file" size="small" />
                      <span>{item.name}</span>
                    </div>
                  ),
                  data: item
                }))}
                onSort={(event) => onItemMove(category.id, event)}
                axis="vertical"
                dragHandle=".item-handle"
              />
            </div>
          )}
        </div>
      }
    />
  );
};
```

### Mobile-Optimized Sortable Item

```typescript
// React
const MobileSortableItem = ({ item, index, onMove }) => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);
  const [isLongPress, setIsLongPress] = useState(false);
  const [touchStartTime, setTouchStartTime] = useState(0);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  const handleTouchStart = () => {
    setTouchStartTime(Date.now());
  };

  const handleTouchEnd = () => {
    const touchDuration = Date.now() - touchStartTime;
    if (touchDuration > 500) { // Long press
      setIsLongPress(true);
      
      // Haptic feedback
      if (navigator.vibrate) {
        navigator.vibrate(100);
      }
    }
  };

  const handleDragStart = () => {
    if (isMobile && !isLongPress) {
      return false; // Prevent drag on mobile without long press
    }
    return true;
  };

  return (
    <SafSortableListItem 
      id={item.id}
      index={index}
      data={item}
      onDragStart={handleDragStart}
      onDragEnd={onMove}
      dragHandle={isMobile}
      content={
        <div 
          className={`mobile-item ${isMobile ? 'mobile' : 'desktop'}`}
          onTouchStart={handleTouchStart}
          onTouchEnd={handleTouchEnd}
        >
          {isMobile && (
            <div className="mobile-drag-indicator">
              <SafIcon name="grip-horizontal" />
            </div>
          )}
          
          <div className="item-content">
            <div className="item-header">
              <h4>{item.title}</h4>
              <span className="item-time">{item.time}</span>
            </div>
            
            <p className="item-description">{item.description}</p>
            
            {item.tags && (
              <div className="item-tags">
                {item.tags.map(tag => (
                  <SafBadge key={tag} size="small">
                    {tag}
                  </SafBadge>
                ))}
              </div>
            )}
          </div>
          
          <div className="item-actions">
            <SafButton 
              variant="ghost"
              size={isMobile ? 'medium' : 'small'}
              icon={<SafIcon name="more-horizontal" />}
            />
          </div>
          
          {isMobile && isLongPress && (
            <div className="long-press-hint">
              <SafIcon name="move" />
              <span>Drag to reorder</span>
            </div>
          )}
        </div>
      }
    />
  );
};
```

### Accessibility-Enhanced Sortable Item

```typescript
// React
const AccessibleSortableItem = ({ 
  item, 
  index, 
  totalItems,
  onMove,
  onAnnounce 
}) => {
  const itemRef = useRef(null);
  const [isFocused, setIsFocused] = useState(false);
  const [keyboardMode, setKeyboardMode] = useState(false);

  const handleKeyDown = (event) => {
    setKeyboardMode(true);
    
    switch (event.key) {
      case 'ArrowUp':
        event.preventDefault();
        if (index > 0) {
          onMove({
            id: item.id,
            oldIndex: index,
            newIndex: index - 1,
            data: item
          });
          onAnnounce(`Moved ${item.title} up to position ${index}`);
        }
        break;
        
      case 'ArrowDown':
        event.preventDefault();
        if (index < totalItems - 1) {
          onMove({
            id: item.id,
            oldIndex: index,
            newIndex: index + 1,
            data: item
          });
          onAnnounce(`Moved ${item.title} down to position ${index + 2}`);
        }
        break;
        
      case 'Home':
        event.preventDefault();
        if (index > 0) {
          onMove({
            id: item.id,
            oldIndex: index,
            newIndex: 0,
            data: item
          });
          onAnnounce(`Moved ${item.title} to first position`);
        }
        break;
        
      case 'End':
        event.preventDefault();
        if (index < totalItems - 1) {
          onMove({
            id: item.id,
            oldIndex: index,
            newIndex: totalItems - 1,
            data: item
          });
          onAnnounce(`Moved ${item.title} to last position`);
        }
        break;
    }
  };

  const handleFocus = () => {
    setIsFocused(true);
  };

  const handleBlur = () => {
    setIsFocused(false);
    setKeyboardMode(false);
  };

  return (
    <SafSortableListItem 
      id={item.id}
      index={index}
      data={item}
      onDragEnd={onMove}
      onFocus={handleFocus}
      content={
        <div 
          ref={itemRef}
          className={`accessible-item ${isFocused ? 'focused' : ''} ${keyboardMode ? 'keyboard-mode' : ''}`}
          role="button"
          tabIndex={0}
          onKeyDown={handleKeyDown}
          onFocus={handleFocus}
          onBlur={handleBlur}
          aria-label={`${item.title}, position ${index + 1} of ${totalItems}. Use arrow keys to reorder, Home and End to move to first or last position.`}
          aria-describedby={`item-description-${item.id}`}
        >
          <div className="item-content">
            <h4>{item.title}</h4>
            <p id={`item-description-${item.id}`}>{item.description}</p>
            
            <div className="accessibility-info">
              <span className="position-indicator">
                Position {index + 1} of {totalItems}
              </span>
              
              {keyboardMode && (
                <span className="keyboard-hint">
                  Use arrow keys to reorder
                </span>
              )}
            </div>
          </div>
          
          <div className="accessibility-indicators">
            <SafIcon name="move" />
            <span className="sr-only">
              Draggable item. Use mouse to drag or arrow keys to reorder.
            </span>
          </div>
        </div>
      }
    />
  );
};
```

## Best Practices

### Visual Design
- **Clear Drag Indicators**: Provide obvious drag handles or hover states
- **Visual Feedback**: Show dragging state with opacity, shadow, or highlighting
- **Consistent Spacing**: Maintain consistent spacing and alignment
- **State Indication**: Clearly indicate selection, disabled, and dragging states

### Interaction Design
- **Responsive Dragging**: Ensure dragging works smoothly across devices
- **Touch Support**: Optimize for touch interactions with appropriate delays
- **Prevent Conflicts**: Avoid conflicts between drag and click interactions
- **Feedback Timing**: Provide immediate visual and haptic feedback

### Accessibility
- **Keyboard Support**: Implement arrow key navigation for reordering
- **Screen Reader Support**: Provide descriptive labels and announcements
- **Focus Management**: Maintain proper focus indicators and management
- **Alternative Methods**: Provide non-drag methods for reordering items

### Performance
- **Efficient Rendering**: Minimize re-renders during drag operations
- **Event Handling**: Optimize event listener management
- **Memory Management**: Clean up resources when items unmount
- **Animation Performance**: Use performant CSS animations

## Accessibility Considerations

- Uses proper ARIA roles and attributes for draggable functionality
- Supports comprehensive keyboard navigation for reordering
- Provides screen reader announcements for position changes
- Maintains proper focus management during interactions
- Includes alternative methods for users who cannot drag
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafSortableList**: Parent sortable list container
- **SafList**: Basic list component for non-sortable items
- **SafListItem**: Static list item component
- **SafCard**: Card-based content container

## Notes

- SafSortableListItem automatically handles drag and drop interactions
- The component supports both mouse and touch-based dragging
- Custom drag handles can be specified using CSS selectors
- Visual feedback is provided during drag operations
- The component integrates seamlessly with parent sortable lists
- Constraints allow for complex validation and restriction rules
- Mobile optimizations ensure good touch device experience
- Accessibility features provide keyboard-based reordering capabilities
