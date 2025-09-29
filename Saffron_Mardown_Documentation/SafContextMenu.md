# SafContextMenu

## Overview

SafContextMenu is a floating menu component that appears on right-click or programmatic trigger, providing contextual actions and options. It supports nested submenus, custom items, keyboard navigation, positioning, and accessibility features for intuitive user interactions.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `boolean` | `false` | Menu visibility state |
| `items` | `MenuItem[]` | `[]` | Menu items array |
| `x` | `number` | `0` | X position (screen coordinates) |
| `y` | `number` | `0` | Y position (screen coordinates) |
| `trigger` | `'contextmenu' \| 'click' \| 'manual'` | `'contextmenu'` | Trigger method |
| `target` | `HTMLElement \| React.RefObject` | - | Target element for positioning |
| `placement` | `'auto' \| 'top' \| 'bottom' \| 'left' \| 'right'` | `'auto'` | Menu placement |
| `offset` | `{ x: number, y: number }` | `{ x: 0, y: 0 }` | Position offset |
| `closeOnClickAway` | `boolean` | `true` | Close on outside click |
| `closeOnItemClick` | `boolean` | `true` | Close on item selection |
| `preventContextMenu` | `boolean` | `true` | Prevent default context menu |
| `animation` | `'fade' \| 'scale' \| 'slide' \| 'none'` | `'fade'` | Animation type |
| `zIndex` | `number` | `1000` | Menu z-index |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onItemClick` | `(item: MenuItem, event: MouseEvent) => void` | Fired when item is clicked |
| `onShow` | `() => void` | Fired when menu is shown |
| `onHide` | `() => void` | Fired when menu is hidden |
| `onOutsideClick` | `(event: MouseEvent) => void` | Fired on outside click |

### MenuItem Interface

```typescript
interface MenuItem {
  id: string;
  label: string | ReactNode;
  icon?: ReactElement;
  shortcut?: string;
  disabled?: boolean;
  hidden?: boolean;
  checked?: boolean;
  type?: 'item' | 'separator' | 'submenu' | 'checkbox' | 'radio';
  children?: MenuItem[];
  dangerous?: boolean;
  onClick?: (item: MenuItem) => void;
  data?: any;
}
```

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `boolean` | `false` | Menu visibility state |
| `items` | `MenuItem[]` | `[]` | Menu items array |
| `x` | `number` | `0` | X position (screen coordinates) |
| `y` | `number` | `0` | Y position (screen coordinates) |
| `trigger` | `'contextmenu' \| 'click' \| 'manual'` | `'contextmenu'` | Trigger method |
| `target` | `ElementRef` | - | Target element for positioning |
| `placement` | `'auto' \| 'top' \| 'bottom' \| 'left' \| 'right'` | `'auto'` | Menu placement |
| `offset` | `{ x: number, y: number }` | `{ x: 0, y: 0 }` | Position offset |
| `closeOnClickAway` | `boolean` | `true` | Close on outside click |
| `closeOnItemClick` | `boolean` | `true` | Close on item selection |
| `preventContextMenu` | `boolean` | `true` | Prevent default context menu |
| `animation` | `'fade' \| 'scale' \| 'slide' \| 'none'` | `'fade'` | Animation type |
| `zIndex` | `number` | `1000` | Menu z-index |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `itemClick` | `EventEmitter<{item: MenuItem, event: MouseEvent}>` | Fired when item is clicked |
| `show` | `EventEmitter<void>` | Fired when menu is shown |
| `hide` | `EventEmitter<void>` | Fired when menu is hidden |
| `outsideClick` | `EventEmitter<MouseEvent>` | Fired on outside click |

## Usage Examples

### Basic Context Menu

```typescript
// React
const BasicContextMenu = ({ children, menuItems }) => {
  const [contextMenu, setContextMenu] = useState(null);

  const handleContextMenu = (event) => {
    event.preventDefault();
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
  };

  const handleMenuItemClick = (item, event) => {
    console.log('Menu item clicked:', item.id);
    setContextMenu(null);
  };

  const basicMenuItems = [
    {
      id: 'cut',
      label: 'Cut',
      icon: <SafIcon name="scissors" />,
      shortcut: 'Ctrl+X'
    },
    {
      id: 'copy',
      label: 'Copy',
      icon: <SafIcon name="copy" />,
      shortcut: 'Ctrl+C'
    },
    {
      id: 'paste',
      label: 'Paste',
      icon: <SafIcon name="clipboard" />,
      shortcut: 'Ctrl+V',
      disabled: true
    },
    {
      id: 'separator1',
      type: 'separator'
    },
    {
      id: 'delete',
      label: 'Delete',
      icon: <SafIcon name="trash" />,
      dangerous: true
    }
  ];

  return (
    <div 
      className="context-menu-container"
      onContextMenu={handleContextMenu}
    >
      {children}
      
      <SafContextMenu
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={basicMenuItems}
        onItemClick={handleMenuItemClick}
        onHide={() => setContextMenu(null)}
      />
    </div>
  );
};
```

```html
<!-- Angular -->
<div 
  class="context-menu-container"
  (contextmenu)="handleContextMenu($event)">
  
  <ng-content></ng-content>
  
  <saf-context-menu
    [visible]="contextMenu !== null"
    [x]="contextMenu?.x || 0"
    [y]="contextMenu?.y || 0"
    [items]="basicMenuItems"
    (itemClick)="handleMenuItemClick($event)"
    (hide)="contextMenu = null">
  </saf-context-menu>
</div>
```

### File Explorer Context Menu

```typescript
// React
const FileExplorerContextMenu = ({ 
  selectedFiles,
  onAction 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [targetItem, setTargetItem] = useState(null);

  const getContextMenuItems = (item) => {
    const isMultiSelect = selectedFiles.length > 1;
    const isFolder = item?.type === 'folder';
    const isImage = item?.type === 'file' && ['jpg', 'png', 'gif', 'svg'].includes(item.extension);

    const baseItems = [
      {
        id: 'open',
        label: isMultiSelect ? 'Open Selected' : 'Open',
        icon: <SafIcon name="external-link" />,
        disabled: isMultiSelect && selectedFiles.some(f => f.type === 'folder')
      },
      {
        id: 'separator1',
        type: 'separator'
      },
      {
        id: 'cut',
        label: isMultiSelect ? `Cut ${selectedFiles.length} items` : 'Cut',
        icon: <SafIcon name="scissors" />,
        shortcut: 'Ctrl+X'
      },
      {
        id: 'copy',
        label: isMultiSelect ? `Copy ${selectedFiles.length} items` : 'Copy',
        icon: <SafIcon name="copy" />,
        shortcut: 'Ctrl+C'
      },
      {
        id: 'separator2',
        type: 'separator'
      },
      {
        id: 'rename',
        label: 'Rename',
        icon: <SafIcon name="edit" />,
        shortcut: 'F2',
        disabled: isMultiSelect
      },
      {
        id: 'delete',
        label: isMultiSelect ? `Delete ${selectedFiles.length} items` : 'Delete',
        icon: <SafIcon name="trash" />,
        shortcut: 'Delete',
        dangerous: true
      },
      {
        id: 'separator3',
        type: 'separator'
      },
      {
        id: 'properties',
        label: 'Properties',
        icon: <SafIcon name="info" />,
        disabled: isMultiSelect
      }
    ];

    // Add folder-specific items
    if (isFolder && !isMultiSelect) {
      baseItems.splice(1, 0, {
        id: 'new',
        label: 'New',
        icon: <SafIcon name="plus" />,
        type: 'submenu',
        children: [
          {
            id: 'new-folder',
            label: 'Folder',
            icon: <SafIcon name="folder-plus" />
          },
          {
            id: 'new-file',
            label: 'File',
            icon: <SafIcon name="file-plus" />
          },
          {
            id: 'separator-new',
            type: 'separator'
          },
          {
            id: 'new-document',
            label: 'Text Document',
            icon: <SafIcon name="file-text" />
          }
        ]
      });
    }

    // Add image-specific items
    if (isImage && !isMultiSelect) {
      baseItems.splice(-2, 0, {
        id: 'preview',
        label: 'Preview',
        icon: <SafIcon name="eye" />
      }, {
        id: 'edit',
        label: 'Edit Image',
        icon: <SafIcon name="image" />
      });
    }

    return baseItems;
  };

  const handleContextMenu = (event, item) => {
    event.preventDefault();
    setTargetItem(item);
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
  };

  const handleMenuAction = (menuItem) => {
    onAction(menuItem.id, targetItem, selectedFiles);
    setContextMenu(null);
  };

  return (
    <div className="file-explorer-context">
      <div className="file-list">
        {/* File items would be rendered here */}
        <div 
          className="file-item"
          onContextMenu={(e) => handleContextMenu(e, { type: 'folder', name: 'Documents' })}
        >
          <SafIcon name="folder" />
          <span>Documents</span>
        </div>
      </div>

      <SafContextMenu
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={getContextMenuItems(targetItem)}
        onItemClick={(item) => handleMenuAction(item)}
        onHide={() => setContextMenu(null)}
        className="file-explorer-menu"
      />
    </div>
  );
};
```

### Rich Content Context Menu

```typescript
// React
const RichContentContextMenu = ({ 
  content,
  onContentAction 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [selectedText, setSelectedText] = useState('');
  const contentRef = useRef(null);

  const getSelectionMenuItems = () => {
    const hasSelection = selectedText.length > 0;
    const isUrl = /^https?:\/\//.test(selectedText.trim());
    const isEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(selectedText.trim());

    return [
      {
        id: 'copy-text',
        label: 'Copy',
        icon: <SafIcon name="copy" />,
        disabled: !hasSelection,
        shortcut: 'Ctrl+C'
      },
      {
        id: 'search',
        label: `Search "${selectedText.substring(0, 20)}${selectedText.length > 20 ? '...' : '}"`,
        icon: <SafIcon name="search" />,
        disabled: !hasSelection || selectedText.length < 2
      },
      {
        id: 'separator1',
        type: 'separator',
        hidden: !hasSelection
      },
      {
        id: 'open-link',
        label: 'Open Link',
        icon: <SafIcon name="external-link" />,
        hidden: !isUrl
      },
      {
        id: 'copy-link',
        label: 'Copy Link',
        icon: <SafIcon name="link" />,
        hidden: !isUrl
      },
      {
        id: 'send-email',
        label: 'Send Email',
        icon: <SafIcon name="mail" />,
        hidden: !isEmail
      },
      {
        id: 'separator2',
        type: 'separator'
      },
      {
        id: 'format',
        label: 'Format',
        icon: <SafIcon name="type" />,
        type: 'submenu',
        disabled: !hasSelection,
        children: [
          {
            id: 'bold',
            label: 'Bold',
            icon: <SafIcon name="bold" />,
            shortcut: 'Ctrl+B'
          },
          {
            id: 'italic',
            label: 'Italic',
            icon: <SafIcon name="italic" />,
            shortcut: 'Ctrl+I'
          },
          {
            id: 'underline',
            label: 'Underline',
            icon: <SafIcon name="underline" />,
            shortcut: 'Ctrl+U'
          },
          {
            id: 'separator-format',
            type: 'separator'
          },
          {
            id: 'highlight',
            label: 'Highlight',
            icon: <SafIcon name="marker" />
          },
          {
            id: 'color',
            label: 'Text Color',
            icon: <SafIcon name="palette" />
          }
        ]
      },
      {
        id: 'translate',
        label: 'Translate',
        icon: <SafIcon name="globe" />,
        disabled: !hasSelection || selectedText.length < 3,
        type: 'submenu',
        children: [
          { id: 'translate-es', label: 'Spanish', icon: <SafIcon name="globe" /> },
          { id: 'translate-fr', label: 'French', icon: <SafIcon name="globe" /> },
          { id: 'translate-de', label: 'German', icon: <SafIcon name="globe" /> },
          { id: 'translate-ja', label: 'Japanese', icon: <SafIcon name="globe" /> }
        ]
      }
    ];
  };

  const handleContextMenu = (event) => {
    event.preventDefault();
    
    // Get selected text
    const selection = window.getSelection();
    setSelectedText(selection ? selection.toString().trim() : '');
    
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
  };

  const handleMenuAction = (item) => {
    onContentAction(item.id, selectedText, {
      selection: window.getSelection(),
      target: contentRef.current
    });
    setContextMenu(null);
  };

  return (
    <div className="rich-content-container">
      <div 
        ref={contentRef}
        className="content-area"
        onContextMenu={handleContextMenu}
        dangerouslySetInnerHTML={{ __html: content }}
      />

      <SafContextMenu
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={getSelectionMenuItems()}
        onItemClick={handleMenuAction}
        onHide={() => setContextMenu(null)}
        className="rich-content-menu"
      />
    </div>
  );
};
```

### Data Table Context Menu

```typescript
// React
const DataTableContextMenu = ({ 
  selectedRows,
  tableData,
  onRowAction 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [targetRow, setTargetRow] = useState(null);

  const getRowContextMenuItems = (row) => {
    const isMultiSelect = selectedRows.length > 1;
    const canEdit = row?.permissions?.edit !== false;
    const canDelete = row?.permissions?.delete !== false;

    return [
      {
        id: 'view',
        label: isMultiSelect ? `View ${selectedRows.length} items` : 'View Details',
        icon: <SafIcon name="eye" />
      },
      {
        id: 'edit',
        label: 'Edit',
        icon: <SafIcon name="edit" />,
        disabled: !canEdit || isMultiSelect
      },
      {
        id: 'duplicate',
        label: 'Duplicate',
        icon: <SafIcon name="copy" />,
        disabled: isMultiSelect
      },
      {
        id: 'separator1',
        type: 'separator'
      },
      {
        id: 'export',
        label: isMultiSelect ? `Export ${selectedRows.length} items` : 'Export',
        icon: <SafIcon name="download" />,
        type: 'submenu',
        children: [
          {
            id: 'export-csv',
            label: 'Export as CSV',
            icon: <SafIcon name="file-text" />
          },
          {
            id: 'export-excel',
            label: 'Export as Excel',
            icon: <SafIcon name="file" />
          },
          {
            id: 'export-pdf',
            label: 'Export as PDF',
            icon: <SafIcon name="file" />
          }
        ]
      },
      {
        id: 'share',
        label: 'Share',
        icon: <SafIcon name="share" />,
        disabled: isMultiSelect,
        type: 'submenu',
        children: [
          {
            id: 'share-link',
            label: 'Copy Link',
            icon: <SafIcon name="link" />
          },
          {
            id: 'share-email',
            label: 'Send via Email',
            icon: <SafIcon name="mail" />
          },
          {
            id: 'share-team',
            label: 'Share with Team',
            icon: <SafIcon name="users" />
          }
        ]
      },
      {
        id: 'separator2',
        type: 'separator'
      },
      {
        id: 'status',
        label: 'Change Status',
        icon: <SafIcon name="flag" />,
        type: 'submenu',
        children: [
          {
            id: 'status-active',
            label: 'Mark as Active',
            icon: <SafIcon name="check-circle" />,
            checked: row?.status === 'active',
            type: 'radio'
          },
          {
            id: 'status-inactive',
            label: 'Mark as Inactive',
            icon: <SafIcon name="x-circle" />,
            checked: row?.status === 'inactive',
            type: 'radio'
          },
          {
            id: 'status-pending',
            label: 'Mark as Pending',
            icon: <SafIcon name="clock" />,
            checked: row?.status === 'pending',
            type: 'radio'
          }
        ]
      },
      {
        id: 'separator3',
        type: 'separator'
      },
      {
        id: 'delete',
        label: isMultiSelect ? `Delete ${selectedRows.length} items` : 'Delete',
        icon: <SafIcon name="trash" />,
        disabled: !canDelete,
        dangerous: true
      }
    ];
  };

  const handleRowContextMenu = (event, row) => {
    event.preventDefault();
    setTargetRow(row);
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
  };

  const handleMenuAction = (item) => {
    const affectedRows = selectedRows.length > 0 ? selectedRows : [targetRow];
    onRowAction(item.id, affectedRows, targetRow);
    setContextMenu(null);
  };

  return (
    <div className="data-table-context">
      <table className="data-table">
        <thead>
          <tr>
            <th>Name</th>
            <th>Status</th>
            <th>Date</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {tableData.map(row => (
            <tr
              key={row.id}
              className={selectedRows.includes(row.id) ? 'selected' : ''}
              onContextMenu={(e) => handleRowContextMenu(e, row)}
            >
              <td>{row.name}</td>
              <td>{row.status}</td>
              <td>{row.date}</td>
              <td>
                <SafButton
                  variant="ghost"
                  size="small"
                  icon={<SafIcon name="more-vertical" />}
                  onClick={(e) => handleRowContextMenu(e, row)}
                />
              </td>
            </tr>
          ))}
        </tbody>
      </table>

      <SafContextMenu
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={getRowContextMenuItems(targetRow)}
        onItemClick={handleMenuAction}
        onHide={() => setContextMenu(null)}
        className="data-table-menu"
      />
    </div>
  );
};
```

### Custom Trigger Context Menu

```typescript
// React
const CustomTriggerContextMenu = ({ 
  children,
  menuItems,
  triggerType = 'contextmenu' 
}) => {
  const [isVisible, setIsVisible] = useState(false);
  const [position, setPosition] = useState({ x: 0, y: 0 });
  const triggerRef = useRef(null);

  const showMenu = (event) => {
    if (triggerType === 'contextmenu') {
      event.preventDefault();
    }
    
    const rect = triggerRef.current?.getBoundingClientRect();
    
    if (triggerType === 'click' && rect) {
      // Position below the trigger element
      setPosition({
        x: rect.left,
        y: rect.bottom + 5
      });
    } else {
      // Use mouse position
      setPosition({
        x: event.clientX,
        y: event.clientY
      });
    }
    
    setIsVisible(true);
  };

  const hideMenu = () => {
    setIsVisible(false);
  };

  const handleItemClick = (item) => {
    item.onClick?.(item);
    if (item.closeOnClick !== false) {
      hideMenu();
    }
  };

  return (
    <div className="custom-trigger-context">
      <div
        ref={triggerRef}
        className="trigger-element"
        onContextMenu={triggerType === 'contextmenu' ? showMenu : undefined}
        onClick={triggerType === 'click' ? showMenu : undefined}
      >
        {children}
      </div>

      <SafContextMenu
        visible={isVisible}
        x={position.x}
        y={position.y}
        items={menuItems}
        trigger="manual"
        onItemClick={handleItemClick}
        onHide={hideMenu}
        placement={triggerType === 'click' ? 'bottom' : 'auto'}
      />
    </div>
  );
};
```

### Keyboard-Accessible Context Menu

```typescript
// React
const KeyboardAccessibleContextMenu = ({ 
  children,
  menuItems,
  ariaLabel = "Context menu" 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [focusedIndex, setFocusedIndex] = useState(-1);
  const [announcements, setAnnouncements] = useState('');
  const menuRef = useRef(null);

  const flattenedItems = useMemo(() => {
    const flatten = (items, level = 0) => {
      return items.reduce((acc, item) => {
        if (item.type === 'separator' || item.hidden) return acc;
        
        acc.push({ ...item, level });
        
        if (item.children && item.type === 'submenu') {
          acc.push(...flatten(item.children, level + 1));
        }
        
        return acc;
      }, []);
    };
    
    return flatten(menuItems);
  }, [menuItems]);

  const handleContextMenu = (event) => {
    event.preventDefault();
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
    setFocusedIndex(0);
    setAnnouncements(`Context menu opened with ${flattenedItems.length} items`);
  };

  const handleKeyDown = (event) => {
    if (!contextMenu) return;

    switch (event.key) {
      case 'ArrowDown':
        event.preventDefault();
        setFocusedIndex(prev => 
          prev < flattenedItems.length - 1 ? prev + 1 : 0
        );
        break;
        
      case 'ArrowUp':
        event.preventDefault();
        setFocusedIndex(prev => 
          prev > 0 ? prev - 1 : flattenedItems.length - 1
        );
        break;
        
      case 'Enter':
      case ' ':
        event.preventDefault();
        if (focusedIndex >= 0) {
          const item = flattenedItems[focusedIndex];
          handleItemClick(item);
        }
        break;
        
      case 'Escape':
        handleHide();
        break;
        
      case 'Home':
        event.preventDefault();
        setFocusedIndex(0);
        break;
        
      case 'End':
        event.preventDefault();
        setFocusedIndex(flattenedItems.length - 1);
        break;
    }
  };

  const handleItemClick = (item) => {
    if (item.disabled) return;
    
    item.onClick?.(item);
    setAnnouncements(`Activated ${item.label}`);
    handleHide();
  };

  const handleHide = () => {
    setContextMenu(null);
    setFocusedIndex(-1);
    setAnnouncements('Context menu closed');
  };

  useEffect(() => {
    if (contextMenu) {
      document.addEventListener('keydown', handleKeyDown);
      return () => document.removeEventListener('keydown', handleKeyDown);
    }
  }, [contextMenu, focusedIndex, flattenedItems]);

  return (
    <div className="keyboard-accessible-context">
      <div 
        className="content-area"
        onContextMenu={handleContextMenu}
        tabIndex={0}
        role="application"
        aria-label="Content with context menu"
      >
        {children}
      </div>

      <SafContextMenu
        ref={menuRef}
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={menuItems.map((item, index) => ({
          ...item,
          focused: index === focusedIndex,
          onFocus: () => setFocusedIndex(index)
        }))}
        onItemClick={handleItemClick}
        onHide={handleHide}
        role="menu"
        aria-label={ariaLabel}
        aria-activedescendant={
          focusedIndex >= 0 ? `menu-item-${focusedIndex}` : undefined
        }
        className="keyboard-accessible-menu"
      />

      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>
    </div>
  );
};
```

### Multi-Level Submenu Context Menu

```typescript
// React
const MultiLevelSubmenuContextMenu = ({ 
  navigationData,
  onNavigate 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [openSubmenus, setOpenSubmenus] = useState(new Set());

  const buildMenuItems = (navItems) => {
    return navItems.map(item => ({
      id: item.id,
      label: item.title,
      icon: item.icon && <SafIcon name={item.icon} />,
      disabled: item.disabled,
      type: item.children ? 'submenu' : 'item',
      children: item.children ? buildMenuItems(item.children) : undefined,
      onClick: (menuItem) => {
        if (!item.children) {
          onNavigate(item.url || item.id);
        }
      }
    }));
  };

  const handleContextMenu = (event) => {
    event.preventDefault();
    setContextMenu({
      x: event.clientX,
      y: event.clientY
    });
  };

  const handleSubmenuOpen = (submenuId) => {
    setOpenSubmenus(prev => new Set([...prev, submenuId]));
  };

  const handleSubmenuClose = (submenuId) => {
    setOpenSubmenus(prev => {
      const next = new Set(prev);
      next.delete(submenuId);
      return next;
    });
  };

  const menuItems = [
    {
      id: 'file',
      label: 'File',
      icon: <SafIcon name="file" />,
      type: 'submenu',
      children: [
        {
          id: 'new',
          label: 'New',
          icon: <SafIcon name="plus" />,
          type: 'submenu',
          children: [
            { id: 'new-document', label: 'Document', icon: <SafIcon name="file-text" /> },
            { id: 'new-spreadsheet', label: 'Spreadsheet', icon: <SafIcon name="grid" /> },
            { id: 'new-presentation', label: 'Presentation', icon: <SafIcon name="monitor" /> },
            { id: 'separator-new', type: 'separator' },
            { id: 'new-folder', label: 'Folder', icon: <SafIcon name="folder-plus" /> }
          ]
        },
        {
          id: 'open',
          label: 'Open',
          icon: <SafIcon name="folder-open" />,
          shortcut: 'Ctrl+O'
        },
        {
          id: 'recent',
          label: 'Open Recent',
          icon: <SafIcon name="clock" />,
          type: 'submenu',
          children: [
            { id: 'recent-1', label: 'Document1.docx' },
            { id: 'recent-2', label: 'Spreadsheet1.xlsx' },
            { id: 'recent-3', label: 'Presentation1.pptx' },
            { id: 'separator-recent', type: 'separator' },
            { id: 'clear-recent', label: 'Clear Recent Files' }
          ]
        },
        { id: 'separator-file', type: 'separator' },
        { id: 'save', label: 'Save', icon: <SafIcon name="save" />, shortcut: 'Ctrl+S' },
        { id: 'save-as', label: 'Save As...', icon: <SafIcon name="save" />, shortcut: 'Ctrl+Shift+S' }
      ]
    },
    {
      id: 'edit',
      label: 'Edit',
      icon: <SafIcon name="edit" />,
      type: 'submenu',
      children: [
        { id: 'undo', label: 'Undo', icon: <SafIcon name="undo" />, shortcut: 'Ctrl+Z' },
        { id: 'redo', label: 'Redo', icon: <SafIcon name="redo" />, shortcut: 'Ctrl+Y' },
        { id: 'separator-edit', type: 'separator' },
        { id: 'cut', label: 'Cut', icon: <SafIcon name="scissors" />, shortcut: 'Ctrl+X' },
        { id: 'copy', label: 'Copy', icon: <SafIcon name="copy" />, shortcut: 'Ctrl+C' },
        { id: 'paste', label: 'Paste', icon: <SafIcon name="clipboard" />, shortcut: 'Ctrl+V' }
      ]
    },
    {
      id: 'view',
      label: 'View',
      icon: <SafIcon name="eye" />,
      type: 'submenu',
      children: [
        {
          id: 'zoom',
          label: 'Zoom',
          icon: <SafIcon name="zoom-in" />,
          type: 'submenu',
          children: [
            { id: 'zoom-in', label: 'Zoom In', shortcut: 'Ctrl++' },
            { id: 'zoom-out', label: 'Zoom Out', shortcut: 'Ctrl+-' },
            { id: 'zoom-100', label: 'Actual Size', shortcut: 'Ctrl+0' },
            { id: 'zoom-fit', label: 'Fit to Window' }
          ]
        },
        {
          id: 'layout',
          label: 'Layout',
          icon: <SafIcon name="layout" />,
          type: 'submenu',
          children: [
            { id: 'layout-list', label: 'List View', checked: true, type: 'radio' },
            { id: 'layout-grid', label: 'Grid View', checked: false, type: 'radio' },
            { id: 'layout-card', label: 'Card View', checked: false, type: 'radio' }
          ]
        },
        { id: 'separator-view', type: 'separator' },
        { id: 'fullscreen', label: 'Full Screen', shortcut: 'F11', type: 'checkbox', checked: false }
      ]
    }
  ];

  return (
    <div className="multi-level-submenu-context">
      <div 
        className="workspace"
        onContextMenu={handleContextMenu}
      >
        <p>Right-click here to open the multi-level context menu</p>
      </div>

      <SafContextMenu
        visible={!!contextMenu}
        x={contextMenu?.x || 0}
        y={contextMenu?.y || 0}
        items={menuItems}
        onItemClick={(item) => {
          console.log('Menu action:', item.id);
          setContextMenu(null);
        }}
        onHide={() => setContextMenu(null)}
        onSubmenuOpen={handleSubmenuOpen}
        onSubmenuClose={handleSubmenuClose}
        className="multi-level-menu"
      />
    </div>
  );
};
```

## Best Practices

### Menu Design
- **Logical Grouping**: Group related actions together with separators
- **Clear Labels**: Use descriptive labels that clearly indicate the action
- **Icon Usage**: Use consistent icons to enhance recognition
- **Keyboard Shortcuts**: Show keyboard shortcuts when available

### Interaction Design
- **Quick Access**: Position frequently used actions at the top
- **Contextual Relevance**: Show only relevant actions for the current context
- **Visual Hierarchy**: Use proper visual hierarchy for submenus
- **Consistent Behavior**: Maintain consistent interaction patterns

### Performance
- **Lazy Loading**: Load submenu content on demand
- **Efficient Rendering**: Optimize for large menu structures
- **Memory Management**: Clean up event listeners properly
- **Animation Performance**: Use CSS animations for better performance

### Accessibility
- **Keyboard Navigation**: Support full keyboard navigation
- **Screen Reader Support**: Provide proper ARIA attributes and announcements
- **Focus Management**: Maintain proper focus during menu operations
- **Color Contrast**: Ensure menu items meet accessibility contrast requirements

## Accessibility Considerations

- Uses proper ARIA roles including `menu`, `menuitem`, and `separator`
- Supports complete keyboard navigation with arrow keys and Enter/Space
- Provides screen reader announcements for menu state changes
- Maintains proper focus management during submenu navigation
- Includes aria-expanded and aria-haspopup attributes for submenus
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafMenu**: Regular dropdown menu component
- **SafButton**: Button component for menu triggers
- **SafIcon**: Icons used in menu items
- **SafTooltip**: Tooltips for additional item information

## Notes

- SafContextMenu automatically handles positioning and viewport constraints
- The component supports both mouse and keyboard interactions
- Submenu positioning automatically adjusts based on available space
- Context prevention can be disabled for custom implementations
- Animation options provide smooth menu transitions
- Z-index management ensures proper layering in complex interfaces
- Performance optimizations handle large menu structures efficiently
- Accessibility features provide comprehensive keyboard and screen reader support
