# SafTreeNode

## Overview

SafTreeNode is an individual node component within a tree structure that provides expand/collapse functionality, selection states, drag-and-drop support, and content rendering. It works within SafTreeView or as a standalone component for building custom tree interfaces with full accessibility support.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string` | - | Unique node identifier |
| `title` | `string \| ReactNode` | - | Node title/label content |
| `selected` | `boolean` | `false` | Selection state |
| `expanded` | `boolean` | `false` | Expansion state |
| `checked` | `boolean` | `false` | Checkbox state |
| `indeterminate` | `boolean` | `false` | Indeterminate checkbox state |
| `disabled` | `boolean` | `false` | Disable node interactions |
| `loading` | `boolean` | `false` | Loading state for async operations |
| `draggable` | `boolean` | `false` | Enable drag functionality |
| `droppable` | `boolean` | `true` | Enable drop functionality |
| `level` | `number` | `0` | Nesting level |
| `isLeaf` | `boolean` | `false` | Leaf node indicator |
| `icon` | `ReactElement` | - | Node icon |
| `expandIcon` | `ReactElement` | - | Custom expand/collapse icon |
| `avatar` | `ReactElement` | - | Avatar element |
| `badge` | `ReactElement` | - | Badge element |
| `children` | `TreeNode[]` | - | Child nodes |
| `indentSize` | `number` | `24` | Indentation per level |
| `showLines` | `boolean` | `false` | Show connecting lines |
| `checkable` | `boolean` | `false` | Show checkbox |
| `selectable` | `boolean` | `true` | Enable selection |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(node: TreeNode, event: MouseEvent) => void` | Fired when node is clicked |
| `onDoubleClick` | `(node: TreeNode, event: MouseEvent) => void` | Fired when node is double-clicked |
| `onExpand` | `(expanded: boolean, node: TreeNode) => void` | Fired when expansion changes |
| `onSelect` | `(selected: boolean, node: TreeNode) => void` | Fired when selection changes |
| `onCheck` | `(checked: boolean, node: TreeNode) => void` | Fired when check state changes |
| `onDragStart` | `(event: DragEvent, node: TreeNode) => void` | Fired when drag starts |
| `onDragEnd` | `(event: DragEvent, node: TreeNode) => void` | Fired when drag ends |
| `onDragOver` | `(event: DragEvent, node: TreeNode) => void` | Fired during drag over |
| `onDrop` | `(event: DragEvent, node: TreeNode) => void` | Fired when drop occurs |
| `onContextMenu` | `(event: MouseEvent, node: TreeNode) => void` | Fired on right-click |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string` | - | Unique node identifier |
| `title` | `string \| TemplateRef` | - | Node title/label content |
| `selected` | `boolean` | `false` | Selection state |
| `expanded` | `boolean` | `false` | Expansion state |
| `checked` | `boolean` | `false` | Checkbox state |
| `indeterminate` | `boolean` | `false` | Indeterminate checkbox state |
| `disabled` | `boolean` | `false` | Disable node interactions |
| `loading` | `boolean` | `false` | Loading state for async operations |
| `draggable` | `boolean` | `false` | Enable drag functionality |
| `droppable` | `boolean` | `true` | Enable drop functionality |
| `level` | `number` | `0` | Nesting level |
| `isLeaf` | `boolean` | `false` | Leaf node indicator |
| `children` | `TreeNode[]` | - | Child nodes |
| `indentSize` | `number` | `24` | Indentation per level |
| `showLines` | `boolean` | `false` | Show connecting lines |
| `checkable` | `boolean` | `false` | Show checkbox |
| `selectable` | `boolean` | `true` | Enable selection |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `nodeClick` | `EventEmitter<{node: TreeNode, event: MouseEvent}>` | Fired when node is clicked |
| `nodeDoubleClick` | `EventEmitter<{node: TreeNode, event: MouseEvent}>` | Fired when node is double-clicked |
| `expandChange` | `EventEmitter<{expanded: boolean, node: TreeNode}>` | Fired when expansion changes |
| `selectionChange` | `EventEmitter<{selected: boolean, node: TreeNode}>` | Fired when selection changes |
| `checkChange` | `EventEmitter<{checked: boolean, node: TreeNode}>` | Fired when check state changes |
| `dragStart` | `EventEmitter<{event: DragEvent, node: TreeNode}>` | Fired when drag starts |
| `dragEnd` | `EventEmitter<{event: DragEvent, node: TreeNode}>` | Fired when drag ends |
| `dragOver` | `EventEmitter<{event: DragEvent, node: TreeNode}>` | Fired during drag over |
| `drop` | `EventEmitter<{event: DragEvent, node: TreeNode}>` | Fired when drop occurs |
| `contextMenu` | `EventEmitter<{event: MouseEvent, node: TreeNode}>` | Fired on right-click |

## Usage Examples

### Basic Tree Nodes

```typescript
// React
const BasicTreeNodes = ({ nodeData, onNodeSelect }) => {
  const [selectedNode, setSelectedNode] = useState(null);
  const [expandedNodes, setExpandedNodes] = useState(['folder1']);

  const handleNodeClick = (node, event) => {
    setSelectedNode(node.id);
    onNodeSelect(node);
  };

  const handleExpand = (expanded, node) => {
    setExpandedNodes(prev => 
      expanded 
        ? [...prev, node.id]
        : prev.filter(id => id !== node.id)
    );
  };

  return (
    <div className="basic-tree-nodes">
      {nodeData.map(node => (
        <SafTreeNode
          key={node.id}
          id={node.id}
          title={node.title}
          selected={selectedNode === node.id}
          expanded={expandedNodes.includes(node.id)}
          isLeaf={!node.children?.length}
          icon={<SafIcon name={node.type === 'folder' ? 'folder' : 'file'} />}
          onClick={handleNodeClick}
          onExpand={handleExpand}
        >
          {node.children?.map(child => (
            <SafTreeNode
              key={child.id}
              id={child.id}
              title={child.title}
              level={1}
              isLeaf={true}
              selected={selectedNode === child.id}
              icon={<SafIcon name="file" />}
              onClick={handleNodeClick}
            />
          ))}
        </SafTreeNode>
      ))}
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-tree-nodes">
  <saf-tree-node
    *ngFor="let node of nodeData"
    [id]="node.id"
    [title]="node.title"
    [selected]="selectedNode === node.id"
    [expanded]="expandedNodes.includes(node.id)"
    [isLeaf]="!node.children?.length"
    (nodeClick)="handleNodeClick($event)"
    (expandChange)="handleExpand($event)">
    
    <saf-tree-node
      *ngFor="let child of node.children"
      [id]="child.id"
      [title]="child.title"
      [level]="1"
      [isLeaf]="true"
      [selected]="selectedNode === child.id"
      (nodeClick)="handleNodeClick($event)">
    </saf-tree-node>
  </saf-tree-node>
</div>
```

### Checkable Tree Nodes

```typescript
// React
const CheckableTreeNodes = ({ 
  treeData,
  checkedNodes,
  onCheckChange 
}) => {
  const [expandedNodes, setExpandedNodes] = useState(['team1', 'team2']);

  const isChecked = (nodeId) => checkedNodes.includes(nodeId);
  
  const isIndeterminate = (node) => {
    if (!node.children) return false;
    
    const childrenChecked = node.children.filter(child => 
      isChecked(child.id)
    );
    
    return childrenChecked.length > 0 && childrenChecked.length < node.children.length;
  };

  const handleCheck = (checked, node) => {
    let newCheckedNodes = [...checkedNodes];
    
    if (checked) {
      // Add node and all children
      newCheckedNodes.push(node.id);
      if (node.children) {
        node.children.forEach(child => {
          if (!newCheckedNodes.includes(child.id)) {
            newCheckedNodes.push(child.id);
          }
        });
      }
    } else {
      // Remove node and all children
      newCheckedNodes = newCheckedNodes.filter(id => id !== node.id);
      if (node.children) {
        node.children.forEach(child => {
          newCheckedNodes = newCheckedNodes.filter(id => id !== child.id);
        });
      }
    }
    
    onCheckChange(newCheckedNodes);
  };

  return (
    <div className="checkable-tree-nodes">
      <div className="tree-header">
        <h3>Select Team Members</h3>
        <SafBadge 
          label={`${checkedNodes.length} selected`}
          color="primary"
        />
      </div>

      {treeData.map(team => (
        <SafTreeNode
          key={team.id}
          id={team.id}
          title={team.name}
          expanded={expandedNodes.includes(team.id)}
          checked={isChecked(team.id)}
          indeterminate={isIndeterminate(team)}
          checkable
          icon={<SafIcon name="users" />}
          onExpand={(expanded) => {
            setExpandedNodes(prev => 
              expanded 
                ? [...prev, team.id]
                : prev.filter(id => id !== team.id)
            );
          }}
          onCheck={(checked) => handleCheck(checked, team)}
        >
          {team.members?.map(member => (
            <SafTreeNode
              key={member.id}
              id={member.id}
              title={member.name}
              level={1}
              isLeaf={true}
              checked={isChecked(member.id)}
              checkable
              avatar={
                <SafAvatar 
                  src={member.avatar}
                  name={member.name}
                  size="small"
                />
              }
              badge={
                member.role && (
                  <SafBadge 
                    label={member.role}
                    size="small"
                    variant="outline"
                  />
                )
              }
              onCheck={(checked) => handleCheck(checked, member)}
            />
          ))}
        </SafTreeNode>
      ))}
    </div>
  );
};
```

### Draggable Tree Nodes

```typescript
// React
const DraggableTreeNodes = ({ 
  fileStructure,
  onStructureChange 
}) => {
  const [draggedNode, setDraggedNode] = useState(null);
  const [dropTarget, setDropTarget] = useState(null);
  const [expandedNodes, setExpandedNodes] = useState(['root']);

  const handleDragStart = (event, node) => {
    setDraggedNode(node);
    event.dataTransfer.effectAllowed = 'move';
    event.dataTransfer.setData('text/plain', node.id);
  };

  const handleDragOver = (event, node) => {
    if (draggedNode && draggedNode.id !== node.id) {
      event.preventDefault();
      event.dataTransfer.dropEffect = 'move';
      setDropTarget(node.id);
    }
  };

  const handleDrop = (event, targetNode) => {
    event.preventDefault();
    
    if (draggedNode && draggedNode.id !== targetNode.id) {
      // Create new structure with moved node
      const newStructure = moveNode(fileStructure, draggedNode.id, targetNode.id);
      onStructureChange(newStructure);
    }
    
    setDraggedNode(null);
    setDropTarget(null);
  };

  const moveNode = (structure, draggedId, targetId) => {
    // Implementation for moving nodes in tree structure
    // This would be a recursive function to find and move nodes
    return structure; // Simplified for example
  };

  const renderNode = (node, level = 0) => (
    <SafTreeNode
      key={node.id}
      id={node.id}
      title={node.name}
      level={level}
      expanded={expandedNodes.includes(node.id)}
      isLeaf={!node.children?.length}
      draggable={node.type !== 'root'}
      droppable={node.type === 'folder'}
      loading={node.loading}
      icon={<SafIcon name={node.type === 'folder' ? 'folder' : 'file'} />}
      onExpand={(expanded) => {
        setExpandedNodes(prev => 
          expanded 
            ? [...prev, node.id]
            : prev.filter(id => id !== node.id)
        );
      }}
      onDragStart={(event) => handleDragStart(event, node)}
      onDragOver={(event) => handleDragOver(event, node)}
      onDrop={(event) => handleDrop(event, node)}
      className={`
        draggable-node
        ${draggedNode?.id === node.id ? 'dragging' : ''}
        ${dropTarget === node.id ? 'drop-target' : ''}
      `}
    >
      {node.children?.map(child => renderNode(child, level + 1))}
    </SafTreeNode>
  );

  return (
    <div className="draggable-tree-nodes">
      <div className="tree-header">
        <h3>File Explorer</h3>
        {draggedNode && (
          <div className="drag-preview">
            Moving: {draggedNode.name}
          </div>
        )}
      </div>

      {fileStructure.map(node => renderNode(node))}
    </div>
  );
};
```

### Custom Rendered Tree Nodes

```typescript
// React
const CustomRenderedTreeNodes = ({ 
  organizationChart,
  selectedEmployee,
  onEmployeeSelect 
}) => {
  const [expandedNodes, setExpandedNodes] = useState(['ceo']);

  const renderEmployeeNode = (employee, level = 0) => {
    const isManager = employee.reports?.length > 0;
    const isExpanded = expandedNodes.includes(employee.id);
    const isSelected = selectedEmployee === employee.id;

    return (
      <SafTreeNode
        key={employee.id}
        id={employee.id}
        level={level}
        expanded={isExpanded}
        selected={isSelected}
        isLeaf={!isManager}
        selectable
        showLines
        indentSize={32}
        onExpand={(expanded) => {
          setExpandedNodes(prev => 
            expanded 
              ? [...prev, employee.id]
              : prev.filter(id => id !== employee.id)
          );
        }}
        onSelect={() => onEmployeeSelect(employee.id)}
        title={
          <div className="employee-node">
            <div className="employee-header">
              <SafAvatar 
                src={employee.photo}
                name={employee.name}
                size="medium"
                status={employee.onlineStatus}
              />
              <div className="employee-info">
                <div className="employee-name">{employee.name}</div>
                <div className="employee-title">{employee.title}</div>
              </div>
              <div className="employee-actions">
                {employee.department && (
                  <SafBadge 
                    label={employee.department}
                    color="secondary"
                    size="small"
                  />
                )}
                {isManager && (
                  <SafBadge 
                    label={`${employee.reports.length} reports`}
                    color="primary"
                    size="small"
                  />
                )}
              </div>
            </div>
            
            <div className="employee-details">
              <div className="contact-info">
                <SafIcon name="mail" size="small" />
                <span>{employee.email}</span>
              </div>
              {employee.phone && (
                <div className="contact-info">
                  <SafIcon name="phone" size="small" />
                  <span>{employee.phone}</span>
                </div>
              )}
            </div>
          </div>
        }
        className={`employee-tree-node ${isSelected ? 'selected' : ''}`}
      >
        {employee.reports?.map(report => 
          renderEmployeeNode(report, level + 1)
        )}
      </SafTreeNode>
    );
  };

  return (
    <div className="custom-rendered-tree-nodes">
      <div className="org-chart-header">
        <h2>Organization Chart</h2>
        <div className="chart-legend">
          <div className="legend-item">
            <SafIcon name="user" size="small" />
            <span>Individual Contributor</span>
          </div>
          <div className="legend-item">
            <SafIcon name="users" size="small" />
            <span>Manager</span>
          </div>
        </div>
      </div>

      <div className="org-chart-tree">
        {organizationChart.map(employee => renderEmployeeNode(employee))}
      </div>
    </div>
  );
};
```

### Loading Tree Nodes

```typescript
// React
const LoadingTreeNodes = ({ 
  rootNodes,
  onLoadChildren 
}) => {
  const [expandedNodes, setExpandedNodes] = useState([]);
  const [loadingNodes, setLoadingNodes] = useState(new Set());
  const [nodeData, setNodeData] = useState(rootNodes);

  const handleExpand = async (expanded, node) => {
    if (expanded && !node.children && !node.isLeaf) {
      // Load children asynchronously
      setLoadingNodes(prev => new Set([...prev, node.id]));
      
      try {
        const children = await onLoadChildren(node);
        
        setNodeData(prev => updateNodeChildren(prev, node.id, children));
        setExpandedNodes(prev => [...prev, node.id]);
      } catch (error) {
        console.error('Failed to load children:', error);
      } finally {
        setLoadingNodes(prev => {
          const next = new Set(prev);
          next.delete(node.id);
          return next;
        });
      }
    } else {
      setExpandedNodes(prev => 
        expanded 
          ? [...prev, node.id]
          : prev.filter(id => id !== node.id)
      );
    }
  };

  const updateNodeChildren = (nodes, nodeId, children) => {
    return nodes.map(node => {
      if (node.id === nodeId) {
        return { ...node, children, loading: false };
      }
      if (node.children) {
        return { ...node, children: updateNodeChildren(node.children, nodeId, children) };
      }
      return node;
    });
  };

  const renderNode = (node, level = 0) => (
    <SafTreeNode
      key={node.id}
      id={node.id}
      title={node.title}
      level={level}
      expanded={expandedNodes.includes(node.id)}
      loading={loadingNodes.has(node.id)}
      isLeaf={node.isLeaf}
      icon={
        loadingNodes.has(node.id) ? 
          <SafLoadingSpinner size="small" /> :
          <SafIcon name={node.icon || 'folder'} />
      }
      onExpand={(expanded) => handleExpand(expanded, node)}
      badge={
        node.count !== undefined && (
          <SafBadge 
            label={node.count.toString()}
            size="small"
            color="secondary"
          />
        )
      }
    >
      {node.children?.map(child => renderNode(child, level + 1))}
    </SafTreeNode>
  );

  return (
    <div className="loading-tree-nodes">
      <div className="tree-header">
        <h3>Dynamic Content Tree</h3>
        <div className="loading-indicators">
          {loadingNodes.size > 0 && (
            <SafBadge 
              label={`Loading ${loadingNodes.size} node${loadingNodes.size > 1 ? 's' : ''}...`}
              color="primary"
            />
          )}
        </div>
      </div>

      {nodeData.map(node => renderNode(node))}
    </div>
  );
};
```

### Context Menu Tree Nodes

```typescript
// React
const ContextMenuTreeNodes = ({ 
  fileTree,
  onAction 
}) => {
  const [contextMenu, setContextMenu] = useState(null);
  const [selectedNode, setSelectedNode] = useState(null);

  const handleContextMenu = (event, node) => {
    event.preventDefault();
    setContextMenu({
      x: event.clientX,
      y: event.clientY,
      node: node
    });
  };

  const handleMenuAction = (action, node) => {
    onAction(action, node);
    setContextMenu(null);
  };

  const getContextMenuItems = (node) => {
    const baseItems = [
      { id: 'copy', label: 'Copy', icon: 'copy' },
      { id: 'cut', label: 'Cut', icon: 'scissors' },
      { id: 'delete', label: 'Delete', icon: 'trash', dangerous: true }
    ];

    if (node.type === 'folder') {
      baseItems.unshift(
        { id: 'new-file', label: 'New File', icon: 'file-plus' },
        { id: 'new-folder', label: 'New Folder', icon: 'folder-plus' },
        { id: 'separator' }
      );
    }

    return baseItems;
  };

  const renderNode = (node, level = 0) => (
    <SafTreeNode
      key={node.id}
      id={node.id}
      title={node.name}
      level={level}
      selected={selectedNode === node.id}
      isLeaf={node.type !== 'folder'}
      icon={<SafIcon name={node.type === 'folder' ? 'folder' : 'file'} />}
      onSelect={() => setSelectedNode(node.id)}
      onContextMenu={(event) => handleContextMenu(event, node)}
      className="context-menu-node"
    >
      {node.children?.map(child => renderNode(child, level + 1))}
    </SafTreeNode>
  );

  return (
    <div className="context-menu-tree-nodes">
      {fileTree.map(node => renderNode(node))}

      {contextMenu && (
        <SafContextMenu
          visible
          x={contextMenu.x}
          y={contextMenu.y}
          onClose={() => setContextMenu(null)}
          items={getContextMenuItems(contextMenu.node)}
          onItemClick={(item) => handleMenuAction(item.id, contextMenu.node)}
        />
      )}
    </div>
  );
};
```

### Accessible Tree Nodes

```typescript
// React
const AccessibleTreeNodes = ({ 
  navigationData,
  onNavigate,
  ariaLabel = "Navigation tree" 
}) => {
  const [selectedNode, setSelectedNode] = useState(null);
  const [expandedNodes, setExpandedNodes] = useState([]);
  const [focusedNode, setFocusedNode] = useState(null);
  const [announcements, setAnnouncements] = useState('');

  const handleKeyDown = (event, node) => {
    switch (event.key) {
      case 'Enter':
      case ' ':
        event.preventDefault();
        handleSelect(node);
        break;
        
      case 'ArrowRight':
        if (!node.isLeaf && !expandedNodes.includes(node.id)) {
          handleExpand(true, node);
        }
        break;
        
      case 'ArrowLeft':
        if (expandedNodes.includes(node.id)) {
          handleExpand(false, node);
        }
        break;
    }
  };

  const handleSelect = (node) => {
    setSelectedNode(node.id);
    setAnnouncements(`Selected ${node.title}`);
    
    if (node.url) {
      onNavigate(node.url);
    }
  };

  const handleExpand = (expanded, node) => {
    setExpandedNodes(prev => 
      expanded 
        ? [...prev, node.id]
        : prev.filter(id => id !== node.id)
    );
    
    setAnnouncements(
      `${expanded ? 'Expanded' : 'Collapsed'} ${node.title}`
    );
  };

  const renderNode = (node, level = 0) => (
    <SafTreeNode
      key={node.id}
      id={node.id}
      title={node.title}
      level={level}
      selected={selectedNode === node.id}
      expanded={expandedNodes.includes(node.id)}
      isLeaf={node.isLeaf}
      selectable
      icon={<SafIcon name={node.icon || 'folder'} />}
      onSelect={() => handleSelect(node)}
      onExpand={(expanded) => handleExpand(expanded, node)}
      onKeyDown={(event) => handleKeyDown(event, node)}
      onFocus={() => setFocusedNode(node.id)}
      role="treeitem"
      aria-expanded={!node.isLeaf ? expandedNodes.includes(node.id) : undefined}
      aria-selected={selectedNode === node.id}
      aria-label={`${node.title}. ${node.isLeaf ? 'Item' : expandedNodes.includes(node.id) ? 'Expanded group' : 'Collapsed group'}`}
      tabIndex={focusedNode === node.id ? 0 : -1}
      className={`accessible-tree-node ${focusedNode === node.id ? 'focused' : ''}`}
    >
      {node.children?.map(child => renderNode(child, level + 1))}
    </SafTreeNode>
  );

  return (
    <div 
      className="accessible-tree-nodes"
      role="tree"
      aria-label={ariaLabel}
    >
      {navigationData.map(node => renderNode(node))}

      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>

      <div className="keyboard-help">
        <details>
          <summary>Keyboard shortcuts</summary>
          <ul>
            <li><kbd>Arrow keys</kbd> - Navigate between items</li>
            <li><kbd>Enter/Space</kbd> - Select item</li>
            <li><kbd>Right arrow</kbd> - Expand group</li>
            <li><kbd>Left arrow</kbd> - Collapse group</li>
          </ul>
        </details>
      </div>
    </div>
  );
};
```

## Best Practices

### Content Design
- **Clear Labels**: Use descriptive titles that clearly identify the node content
- **Consistent Icons**: Apply consistent icon usage across similar node types
- **Visual Hierarchy**: Use proper indentation and visual cues for hierarchy
- **Meaningful Badges**: Display relevant metadata through badges and avatars

### Interaction Design
- **Intuitive Expansion**: Provide clear visual cues for expandable nodes
- **Selection Feedback**: Give immediate visual feedback for selections
- **Drag-and-Drop**: Support intuitive drag-and-drop operations where appropriate
- **Context Actions**: Provide relevant actions through context menus

### Performance
- **Efficient Rendering**: Optimize rendering for large trees with many nodes
- **Lazy Loading**: Load child nodes on demand for better performance
- **Event Handling**: Use efficient event delegation for better performance
- **Memory Management**: Clean up resources when nodes are unmounted

### Accessibility
- **ARIA Attributes**: Use proper ARIA roles and attributes for tree structure
- **Keyboard Navigation**: Support full keyboard navigation
- **Screen Reader Support**: Provide meaningful announcements for state changes
- **Focus Management**: Maintain proper focus during tree operations

## Accessibility Considerations

- Uses proper ARIA roles including `treeitem`, `group`, and appropriate states
- Supports complete keyboard navigation with arrow keys, Enter, and Space
- Provides screen reader announcements for expand/collapse and selection
- Maintains proper focus management during tree operations
- Includes aria-expanded, aria-selected, and aria-level attributes
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafTreeView**: Parent tree container component
- **SafIcon**: Icons for node states and content types
- **SafCheckbox**: Checkbox component for checkable nodes
- **SafAvatar**: Avatar elements for user representations

## Notes

- SafTreeNode can be used standalone or within SafTreeView containers
- The component supports both controlled and uncontrolled usage patterns
- Drag-and-drop functionality provides intuitive tree reorganization
- Context menu integration enables rich interaction possibilities
- Loading states support async operations and progressive loading
- Custom rendering allows for complex node content and layouts
- Accessibility features provide comprehensive keyboard and screen reader support
- Performance optimizations enable smooth operation with many nodes
