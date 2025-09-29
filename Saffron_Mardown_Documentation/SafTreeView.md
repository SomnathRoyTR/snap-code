# SafTreeView

## Overview

SafTreeView is a hierarchical navigation component that displays data in a tree structure with expandable/collapsible nodes, selection capabilities, drag-and-drop support, and search functionality. It provides keyboard navigation, accessibility features, and virtualization for large datasets.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `TreeNode[]` | `[]` | Tree data structure |
| `selected` | `string[]` | `[]` | Selected node IDs |
| `expanded` | `string[]` | `[]` | Expanded node IDs |
| `multiSelect` | `boolean` | `false` | Enable multi-selection |
| `checkable` | `boolean` | `false` | Show checkboxes |
| `draggable` | `boolean` | `false` | Enable drag-and-drop |
| `searchable` | `boolean` | `false` | Enable search functionality |
| `searchQuery` | `string` | `''` | Current search query |
| `virtualScrolling` | `boolean` | `false` | Enable virtual scrolling |
| `itemHeight` | `number` | `32` | Height of each tree item |
| `expandOnClick` | `boolean` | `true` | Expand nodes on click |
| `loadData` | `(node: TreeNode) => Promise<TreeNode[]>` | - | Async data loading function |
| `filterFunction` | `(node: TreeNode, query: string) => boolean` | - | Custom filter function |
| `renderNode` | `(node: TreeNode, props: NodeProps) => ReactNode` | - | Custom node renderer |
| `showLines` | `boolean` | `false` | Show connecting lines |
| `showIcons` | `boolean` | `true` | Show node icons |
| `indentSize` | `number` | `24` | Indentation per level |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onSelect` | `(selectedKeys: string[], info: SelectInfo) => void` | Fired when selection changes |
| `onExpand` | `(expandedKeys: string[], info: ExpandInfo) => void` | Fired when expansion changes |
| `onCheck` | `(checkedKeys: string[], info: CheckInfo) => void` | Fired when check state changes |
| `onDragStart` | `(info: DragInfo) => void` | Fired when drag starts |
| `onDragEnd` | `(info: DragInfo) => void` | Fired when drag ends |
| `onDrop` | `(info: DropInfo) => void` | Fired when drop occurs |
| `onSearch` | `(query: string) => void` | Fired when search query changes |
| `onNodeClick` | `(node: TreeNode, event: MouseEvent) => void` | Fired when node is clicked |
| `onNodeDoubleClick` | `(node: TreeNode, event: MouseEvent) => void` | Fired when node is double-clicked |

### TreeNode Interface

```typescript
interface TreeNode {
  id: string;
  title: string;
  key?: string;
  children?: TreeNode[];
  icon?: ReactElement;
  disabled?: boolean;
  selectable?: boolean;
  checkable?: boolean;
  draggable?: boolean;
  loading?: boolean;
  isLeaf?: boolean;
  data?: any;
}
```

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data` | `TreeNode[]` | `[]` | Tree data structure |
| `selected` | `string[]` | `[]` | Selected node IDs |
| `expanded` | `string[]` | `[]` | Expanded node IDs |
| `multiSelect` | `boolean` | `false` | Enable multi-selection |
| `checkable` | `boolean` | `false` | Show checkboxes |
| `draggable` | `boolean` | `false` | Enable drag-and-drop |
| `searchable` | `boolean` | `false` | Enable search functionality |
| `searchQuery` | `string` | `''` | Current search query |
| `virtualScrolling` | `boolean` | `false` | Enable virtual scrolling |
| `itemHeight` | `number` | `32` | Height of each tree item |
| `expandOnClick` | `boolean` | `true` | Expand nodes on click |
| `showLines` | `boolean` | `false` | Show connecting lines |
| `showIcons` | `boolean` | `true` | Show node icons |
| `indentSize` | `number` | `24` | Indentation per level |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `selectionChange` | `EventEmitter<{selectedKeys: string[], info: SelectInfo}>` | Fired when selection changes |
| `expansionChange` | `EventEmitter<{expandedKeys: string[], info: ExpandInfo}>` | Fired when expansion changes |
| `checkChange` | `EventEmitter<{checkedKeys: string[], info: CheckInfo}>` | Fired when check state changes |
| `dragStart` | `EventEmitter<DragInfo>` | Fired when drag starts |
| `dragEnd` | `EventEmitter<DragInfo>` | Fired when drag ends |
| `drop` | `EventEmitter<DropInfo>` | Fired when drop occurs |
| `search` | `EventEmitter<string>` | Fired when search query changes |
| `nodeClick` | `EventEmitter<{node: TreeNode, event: MouseEvent}>` | Fired when node is clicked |
| `nodeDoubleClick` | `EventEmitter<{node: TreeNode, event: MouseEvent}>` | Fired when node is double-clicked |

## Usage Examples

### Basic Tree View

```typescript
// React
const BasicTreeView = ({ fileStructure, onFileSelect }) => {
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState(['folder1']);

  const treeData = [
    {
      id: 'root',
      title: 'Project Files',
      icon: <SafIcon name="folder" />,
      children: [
        {
          id: 'src',
          title: 'src',
          icon: <SafIcon name="folder" />,
          children: [
            {
              id: 'components',
              title: 'components',
              icon: <SafIcon name="folder" />,
              children: [
                { id: 'button', title: 'Button.tsx', icon: <SafIcon name="file-code" />, isLeaf: true },
                { id: 'input', title: 'Input.tsx', icon: <SafIcon name="file-code" />, isLeaf: true }
              ]
            },
            { id: 'utils', title: 'utils.ts', icon: <SafIcon name="file-code" />, isLeaf: true }
          ]
        },
        {
          id: 'public',
          title: 'public',
          icon: <SafIcon name="folder" />,
          children: [
            { id: 'index', title: 'index.html', icon: <SafIcon name="file" />, isLeaf: true }
          ]
        }
      ]
    }
  ];

  return (
    <div className="basic-tree-view">
      <SafTreeView
        data={treeData}
        selected={selectedKeys}
        expanded={expandedKeys}
        onSelect={(keys, info) => {
          setSelectedKeys(keys);
          onFileSelect(info.node);
        }}
        onExpand={(keys) => setExpandedKeys(keys)}
        showIcons
        expandOnClick
      />
    </div>
  );
};
```

```html
<!-- Angular -->
<div class="basic-tree-view">
  <saf-tree-view
    [data]="treeData"
    [selected]="selectedKeys"
    [expanded]="expandedKeys"
    [showIcons]="true"
    [expandOnClick]="true"
    (selectionChange)="handleSelect($event)"
    (expansionChange)="handleExpand($event)">
  </saf-tree-view>
</div>
```

### Multi-Select Tree with Checkboxes

```typescript
// React
const MultiSelectTree = ({ 
  organizationData,
  selectedUsers,
  onSelectionChange 
}) => {
  const [checkedKeys, setCheckedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState(['company']);

  const handleCheck = (keys, info) => {
    setCheckedKeys(keys);
    
    // Get all selected user nodes
    const selectedUserNodes = info.checkedNodes
      .filter(node => node.isLeaf && node.data?.type === 'user')
      .map(node => node.data);
    
    onSelectionChange(selectedUserNodes);
  };

  return (
    <div className="multi-select-tree">
      <div className="tree-header">
        <h3>Select Team Members</h3>
        {checkedKeys.length > 0 && (
          <SafBadge 
            label={`${checkedKeys.length} selected`}
            color="primary"
          />
        )}
      </div>

      <SafTreeView
        data={organizationData}
        expanded={expandedKeys}
        checkable
        multiSelect
        checked={checkedKeys}
        onCheck={handleCheck}
        onExpand={setExpandedKeys}
        showIcons
        renderNode={(node, props) => (
          <div className="org-tree-node">
            <div className="node-content">
              {node.icon}
              <span className="node-title">{node.title}</span>
              {node.data?.role && (
                <SafBadge 
                  label={node.data.role}
                  size="small"
                  variant="outline"
                />
              )}
            </div>
            {node.data?.email && (
              <div className="node-subtitle">{node.data.email}</div>
            )}
          </div>
        )}
      />

      {checkedKeys.length > 0 && (
        <div className="selection-actions">
          <SafButton
            variant="outline"
            size="small"
            onClick={() => setCheckedKeys([])}
          >
            Clear Selection
          </SafButton>
          <SafButton
            variant="primary"
            size="small"
            onClick={() => console.log('Selected:', checkedKeys)}
          >
            Add Selected ({checkedKeys.length})
          </SafButton>
        </div>
      )}
    </div>
  );
};
```

### Searchable Tree View

```typescript
// React
const SearchableTreeView = ({ 
  knowledgeBase,
  onArticleSelect 
}) => {
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState([]);
  const [filteredData, setFilteredData] = useState(knowledgeBase);

  // Custom filter function
  const filterTreeData = useCallback((data, query) => {
    if (!query) return data;

    const filterNode = (node) => {
      const titleMatch = node.title.toLowerCase().includes(query.toLowerCase());
      const contentMatch = node.data?.content?.toLowerCase().includes(query.toLowerCase());
      const childrenMatch = node.children?.some(child => filterNode(child));

      if (titleMatch || contentMatch || childrenMatch) {
        return {
          ...node,
          children: node.children?.map(filterNode).filter(Boolean)
        };
      }
      return null;
    };

    return data.map(filterNode).filter(Boolean);
  }, []);

  const handleSearch = (query) => {
    setSearchQuery(query);
    const filtered = filterTreeData(knowledgeBase, query);
    setFilteredData(filtered);

    // Auto-expand matched nodes
    if (query) {
      const expandedNodes = [];
      const collectExpandedNodes = (nodes) => {
        nodes.forEach(node => {
          if (node.children?.length > 0) {
            expandedNodes.push(node.id);
            collectExpandedNodes(node.children);
          }
        });
      };
      collectExpandedNodes(filtered);
      setExpandedKeys(expandedNodes);
    }
  };

  const highlightText = (text, query) => {
    if (!query) return text;
    
    const regex = new RegExp(`(${query})`, 'gi');
    const parts = text.split(regex);
    
    return parts.map((part, index) =>
      regex.test(part) ? 
        <mark key={index} className="search-highlight">{part}</mark> : 
        part
    );
  };

  return (
    <div className="searchable-tree-view">
      <div className="tree-search">
        <SafSearchField
          placeholder="Search knowledge base..."
          value={searchQuery}
          onSearch={handleSearch}
          icon={<SafIcon name="search" />}
          clearable
        />
      </div>

      <SafTreeView
        data={filteredData}
        selected={selectedKeys}
        expanded={expandedKeys}
        searchQuery={searchQuery}
        onSelect={(keys, info) => {
          setSelectedKeys(keys);
          if (info.node.isLeaf) {
            onArticleSelect(info.node.data);
          }
        }}
        onExpand={setExpandedKeys}
        renderNode={(node, props) => (
          <div className="kb-tree-node">
            <div className="node-header">
              {node.icon}
              <span className="node-title">
                {highlightText(node.title, searchQuery)}
              </span>
              {node.data?.type && (
                <SafBadge 
                  label={node.data.type}
                  size="small"
                  color={node.data.type === 'article' ? 'primary' : 'secondary'}
                />
              )}
            </div>
            {node.data?.summary && (
              <div className="node-summary">
                {highlightText(node.data.summary, searchQuery)}
              </div>
            )}
          </div>
        )}
        showIcons
        indentSize={20}
      />

      {filteredData.length === 0 && searchQuery && (
        <SafEmptyState
          title="No results found"
          description={`No articles match "${searchQuery}"`}
          icon={<SafIcon name="search" />}
        />
      )}
    </div>
  );
};
```

### Drag-and-Drop Tree

```typescript
// React
const DragDropTreeView = ({ 
  projectStructure,
  onStructureChange 
}) => {
  const [treeData, setTreeData] = useState(projectStructure);
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [draggedNode, setDraggedNode] = useState(null);

  const handleDragStart = (info) => {
    setDraggedNode(info.node);
  };

  const handleDrop = (info) => {
    const { node: dragNode, dragNodesKeys } = info;
    const { node: dropNode, dropPosition, dropToGap } = info;

    // Clone tree data
    const newTreeData = [...treeData];
    
    // Remove dragged node from original position
    const removedNodes = [];
    const removeNodes = (nodes, keys) => {
      return nodes.filter(node => {
        if (keys.includes(node.id)) {
          removedNodes.push(node);
          return false;
        }
        if (node.children) {
          node.children = removeNodes(node.children, keys);
        }
        return true;
      });
    };
    
    const updatedTreeData = removeNodes(newTreeData, dragNodesKeys);
    
    // Insert dragged node at new position
    const insertNodes = (nodes, targetId, position, nodesToInsert) => {
      return nodes.map(node => {
        if (node.id === targetId) {
          if (dropToGap) {
            // Insert as sibling
            const index = position === -1 ? 0 : position + 1;
            return [
              ...nodes.slice(0, index),
              ...nodesToInsert,
              ...nodes.slice(index)
            ];
          } else {
            // Insert as child
            return {
              ...node,
              children: [...(node.children || []), ...nodesToInsert]
            };
          }
        }
        if (node.children) {
          const result = insertNodes(node.children, targetId, position, nodesToInsert);
          if (Array.isArray(result)) {
            return { ...node, children: result };
          }
          return { ...node, children: insertNodes(node.children, targetId, position, nodesToInsert) };
        }
        return node;
      });
    };

    const finalTreeData = insertNodes(updatedTreeData, dropNode.id, dropPosition, removedNodes);
    setTreeData(finalTreeData);
    onStructureChange(finalTreeData);
  };

  const canDrop = (info) => {
    const { dragNode, dropNode } = info;
    
    // Prevent dropping on self or descendants
    const isDescendant = (parent, child) => {
      if (parent.id === child.id) return true;
      if (parent.children) {
        return parent.children.some(c => isDescendant(c, child));
      }
      return false;
    };

    return !isDescendant(dragNode, dropNode);
  };

  return (
    <div className="drag-drop-tree-view">
      <div className="tree-header">
        <h3>Project Structure</h3>
        <div className="tree-controls">
          <SafButton
            variant="outline"
            size="small"
            icon={<SafIcon name="expand" />}
            onClick={() => {
              // Expand all nodes
              const allKeys = [];
              const collectKeys = (nodes) => {
                nodes.forEach(node => {
                  if (node.children?.length > 0) {
                    allKeys.push(node.id);
                    collectKeys(node.children);
                  }
                });
              };
              collectKeys(treeData);
              setSelectedKeys(allKeys);
            }}
          >
            Expand All
          </SafButton>
        </div>
      </div>

      <SafTreeView
        data={treeData}
        selected={selectedKeys}
        draggable
        onSelect={setSelectedKeys}
        onDragStart={handleDragStart}
        onDrop={handleDrop}
        allowDrop={canDrop}
        renderNode={(node, props) => (
          <div className={`draggable-node ${props.isDragging ? 'dragging' : ''}`}>
            <div className="node-content">
              {node.icon}
              <span className="node-title">{node.title}</span>
              {node.data?.size && (
                <span className="file-size">{node.data.size}</span>
              )}
            </div>
            {props.isDragOver && (
              <div className="drop-indicator" />
            )}
          </div>
        )}
        showIcons
        showLines
      />

      {draggedNode && (
        <div className="drag-preview">
          Dragging: {draggedNode.title}
        </div>
      )}
    </div>
  );
};
```

### Async Loading Tree

```typescript
// React
const AsyncLoadingTree = ({ 
  rootNodes,
  onNodeLoad 
}) => {
  const [treeData, setTreeData] = useState(rootNodes);
  const [loadingNodes, setLoadingNodes] = useState(new Set());
  const [expandedKeys, setExpandedKeys] = useState([]);

  const loadChildrenData = async (node) => {
    if (node.children || node.isLeaf) return;

    setLoadingNodes(prev => new Set([...prev, node.id]));

    try {
      const childrenData = await onNodeLoad(node);
      
      setTreeData(prev => {
        const updateNode = (nodes) => {
          return nodes.map(n => {
            if (n.id === node.id) {
              return { ...n, children: childrenData, loading: false };
            }
            if (n.children) {
              return { ...n, children: updateNode(n.children) };
            }
            return n;
          });
        };
        return updateNode(prev);
      });
    } catch (error) {
      console.error('Failed to load node data:', error);
    } finally {
      setLoadingNodes(prev => {
        const next = new Set(prev);
        next.delete(node.id);
        return next;
      });
    }
  };

  const handleExpand = async (keys, info) => {
    setExpandedKeys(keys);
    
    if (info.expanded && !info.node.children && !info.node.isLeaf) {
      await loadChildrenData(info.node);
    }
  };

  return (
    <div className="async-loading-tree">
      <SafTreeView
        data={treeData}
        expanded={expandedKeys}
        onExpand={handleExpand}
        loadData={loadChildrenData}
        renderNode={(node, props) => (
          <div className="async-tree-node">
            <div className="node-content">
              {loadingNodes.has(node.id) ? (
                <SafLoadingSpinner size="small" />
              ) : (
                node.icon || <SafIcon name="folder" />
              )}
              <span className="node-title">{node.title}</span>
              {node.data?.count !== undefined && (
                <SafBadge 
                  label={node.data.count.toString()}
                  size="small"
                  color="secondary"
                />
              )}
            </div>
            {node.data?.description && (
              <div className="node-description">{node.data.description}</div>
            )}
          </div>
        )}
        showIcons
      />
    </div>
  );
};
```

### Virtual Scrolling Tree

```typescript
// React
const VirtualScrollingTree = ({ 
  largeDataset,
  onNodeSelect 
}) => {
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState([]);

  // Flatten tree for virtual scrolling
  const flattenedData = useMemo(() => {
    const flattened = [];
    
    const flattenNode = (node, level = 0) => {
      flattened.push({ ...node, level });
      
      if (expandedKeys.includes(node.id) && node.children) {
        node.children.forEach(child => flattenNode(child, level + 1));
      }
    };
    
    largeDataset.forEach(node => flattenNode(node));
    return flattened;
  }, [largeDataset, expandedKeys]);

  return (
    <div className="virtual-scrolling-tree">
      <div className="tree-stats">
        <SafBadge 
          label={`${flattenedData.length} visible items`}
          color="secondary"
        />
        <SafBadge 
          label={`${expandedKeys.length} expanded`}
          color="primary"
        />
      </div>

      <SafTreeView
        data={largeDataset}
        selected={selectedKeys}
        expanded={expandedKeys}
        virtualScrolling
        itemHeight={36}
        height={400}
        onSelect={(keys, info) => {
          setSelectedKeys(keys);
          onNodeSelect(info.node);
        }}
        onExpand={setExpandedKeys}
        renderNode={(node, props) => (
          <div 
            className="virtual-tree-node"
            style={{ paddingLeft: `${props.level * 20}px` }}
          >
            {!node.isLeaf && (
              <SafButton
                variant="ghost"
                size="small"
                icon={
                  <SafIcon 
                    name={props.expanded ? "chevron-down" : "chevron-right"} 
                    size="small"
                  />
                }
                onClick={() => props.onExpand(!props.expanded)}
              />
            )}
            
            <div className="node-content">
              {node.icon}
              <span className="node-title">{node.title}</span>
              {node.data?.size && (
                <span className="node-size">{node.data.size}</span>
              )}
            </div>
          </div>
        )}
        showIcons
      />
    </div>
  );
};
```

### Directory Browser Tree

```typescript
// React
const DirectoryBrowserTree = ({ 
  initialPath,
  onFileSelect,
  onPathChange 
}) => {
  const [currentPath, setCurrentPath] = useState(initialPath);
  const [treeData, setTreeData] = useState([]);
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState([]);
  const [loading, setLoading] = useState(false);

  const loadDirectory = useCallback(async (path) => {
    setLoading(true);
    try {
      // Simulated API call
      const response = await fetch(`/api/directory?path=${encodeURIComponent(path)}`);
      const items = await response.json();
      
      const treeNodes = items.map(item => ({
        id: item.path,
        title: item.name,
        icon: <SafIcon name={item.type === 'directory' ? 'folder' : getFileIcon(item.extension)} />,
        isLeaf: item.type !== 'directory',
        data: {
          type: item.type,
          size: item.size,
          modified: item.modified,
          path: item.path,
          extension: item.extension
        }
      }));
      
      setTreeData(treeNodes);
    } catch (error) {
      console.error('Failed to load directory:', error);
    } finally {
      setLoading(false);
    }
  }, []);

  const getFileIcon = (extension) => {
    const iconMap = {
      'js': 'file-code',
      'ts': 'file-code',
      'jsx': 'file-code',
      'tsx': 'file-code',
      'html': 'file-code',
      'css': 'file-code',
      'json': 'file-text',
      'md': 'file-text',
      'txt': 'file-text',
      'pdf': 'file',
      'jpg': 'image',
      'jpeg': 'image',
      'png': 'image',
      'gif': 'image'
    };
    return iconMap[extension] || 'file';
  };

  const handleSelect = (keys, info) => {
    setSelectedKeys(keys);
    
    if (info.node.isLeaf) {
      onFileSelect(info.node.data);
    } else {
      // Navigate to directory
      const newPath = info.node.data.path;
      setCurrentPath(newPath);
      onPathChange(newPath);
      loadDirectory(newPath);
    }
  };

  const formatFileSize = (bytes) => {
    if (bytes === 0) return '0 B';
    const k = 1024;
    const sizes = ['B', 'KB', 'MB', 'GB'];
    const i = Math.floor(Math.log(bytes) / Math.log(k));
    return parseFloat((bytes / Math.pow(k, i)).toFixed(1)) + ' ' + sizes[i];
  };

  const formatDate = (timestamp) => {
    return new Date(timestamp).toLocaleDateString();
  };

  useEffect(() => {
    loadDirectory(currentPath);
  }, [currentPath, loadDirectory]);

  return (
    <div className="directory-browser-tree">
      <div className="browser-header">
        <div className="path-breadcrumb">
          <SafBreadcrumb
            items={currentPath.split('/').map((segment, index, array) => ({
              label: segment || 'Root',
              href: array.slice(0, index + 1).join('/') || '/',
              onClick: (path) => setCurrentPath(path)
            }))}
          />
        </div>
        
        <div className="browser-actions">
          <SafButton
            variant="outline"
            size="small"
            icon={<SafIcon name="refresh" />}
            onClick={() => loadDirectory(currentPath)}
            disabled={loading}
          >
            Refresh
          </SafButton>
        </div>
      </div>

      {loading ? (
        <div className="loading-state">
          <SafLoadingSpinner />
          <span>Loading directory...</span>
        </div>
      ) : (
        <SafTreeView
          data={treeData}
          selected={selectedKeys}
          expanded={expandedKeys}
          onSelect={handleSelect}
          onExpand={setExpandedKeys}
          renderNode={(node, props) => (
            <div className="directory-tree-node">
              <div className="node-main">
                {node.icon}
                <span className="node-name">{node.title}</span>
                {!node.isLeaf && (
                  <SafBadge 
                    label="folder"
                    size="small"
                    variant="outline"
                    color="secondary"
                  />
                )}
              </div>
              
              <div className="node-details">
                {node.data.size && (
                  <span className="file-size">{formatFileSize(node.data.size)}</span>
                )}
                <span className="modified-date">
                  {formatDate(node.data.modified)}
                </span>
              </div>
            </div>
          )}
          showIcons
          expandOnClick={false}
        />
      )}

      {!loading && treeData.length === 0 && (
        <SafEmptyState
          title="Empty directory"
          description="This directory contains no files or folders"
          icon={<SafIcon name="folder" />}
        />
      )}
    </div>
  );
};
```

### Accessible Tree Navigation

```typescript
// React
const AccessibleTreeView = ({ 
  navigationData,
  onNavigate,
  ariaLabel = "Navigation tree" 
}) => {
  const [selectedKeys, setSelectedKeys] = useState([]);
  const [expandedKeys, setExpandedKeys] = useState([]);
  const [focusedNode, setFocusedNode] = useState(null);
  const [announcements, setAnnouncements] = useState('');

  const handleKeyDown = (event, node) => {
    switch (event.key) {
      case 'Enter':
      case ' ':
        event.preventDefault();
        handleSelect([node.id], { node });
        break;
        
      case 'ArrowRight':
        if (!node.isLeaf && !expandedKeys.includes(node.id)) {
          setExpandedKeys(prev => [...prev, node.id]);
          setAnnouncements(`Expanded ${node.title}`);
        }
        break;
        
      case 'ArrowLeft':
        if (expandedKeys.includes(node.id)) {
          setExpandedKeys(prev => prev.filter(key => key !== node.id));
          setAnnouncements(`Collapsed ${node.title}`);
        }
        break;
        
      case 'Home':
        event.preventDefault();
        // Focus first node
        setFocusedNode(navigationData[0]?.id);
        break;
        
      case 'End':
        event.preventDefault();
        // Focus last visible node
        const lastNode = getLastVisibleNode(navigationData, expandedKeys);
        setFocusedNode(lastNode?.id);
        break;
    }
  };

  const handleSelect = (keys, info) => {
    setSelectedKeys(keys);
    setAnnouncements(`Selected ${info.node.title}`);
    
    if (info.node.data?.url) {
      onNavigate(info.node.data.url);
    }
  };

  const getLastVisibleNode = (nodes, expanded) => {
    let lastNode = null;
    
    const traverse = (nodeList) => {
      nodeList.forEach(node => {
        lastNode = node;
        if (expanded.includes(node.id) && node.children) {
          traverse(node.children);
        }
      });
    };
    
    traverse(nodes);
    return lastNode;
  };

  return (
    <nav 
      className="accessible-tree-view"
      role="tree"
      aria-label={ariaLabel}
    >
      <SafTreeView
        data={navigationData}
        selected={selectedKeys}
        expanded={expandedKeys}
        onSelect={handleSelect}
        onExpand={setExpandedKeys}
        onNodeFocus={(node) => setFocusedNode(node.id)}
        renderNode={(node, props) => (
          <div 
            role="treeitem"
            aria-expanded={!node.isLeaf ? expandedKeys.includes(node.id) : undefined}
            aria-selected={selectedKeys.includes(node.id)}
            aria-label={`${node.title}. ${node.isLeaf ? 'Item' : expandedKeys.includes(node.id) ? 'Expanded group' : 'Collapsed group'}`}
            tabIndex={focusedNode === node.id ? 0 : -1}
            onKeyDown={(event) => handleKeyDown(event, node)}
            className={`accessible-tree-node ${focusedNode === node.id ? 'focused' : ''}`}
          >
            <div className="node-content">
              {!node.isLeaf && (
                <SafIcon 
                  name={expandedKeys.includes(node.id) ? "chevron-down" : "chevron-right"}
                  size="small"
                  aria-hidden="true"
                />
              )}
              {node.icon}
              <span className="node-label">{node.title}</span>
              {node.data?.badge && (
                <SafBadge 
                  label={node.data.badge}
                  size="small"
                  color="primary"
                  aria-label={`${node.data.badge} notifications`}
                />
              )}
            </div>
          </div>
        )}
        showIcons
        aria-multiselectable="false"
        className="navigation-tree"
      />

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
            <li><kbd>Home</kbd> - First item</li>
            <li><kbd>End</kbd> - Last item</li>
          </ul>
        </details>
      </div>
    </nav>
  );
};
```

## Best Practices

### Data Structure
- **Consistent Node Format**: Use consistent node structure across all tree levels
- **Efficient Loading**: Implement lazy loading for large datasets
- **Proper Hierarchy**: Ensure logical parent-child relationships
- **Unique Identifiers**: Use unique and stable IDs for all nodes

### Interaction Design
- **Clear Expand/Collapse**: Provide obvious visual cues for expandable nodes
- **Selection Feedback**: Give clear visual feedback for selected items
- **Keyboard Navigation**: Support full keyboard navigation
- **Touch Targets**: Ensure adequate touch targets for mobile devices

### Performance
- **Virtual Scrolling**: Use virtual scrolling for large trees
- **Efficient Updates**: Optimize tree updates and re-renders
- **Memory Management**: Clean up resources for unmounted nodes
- **Debounced Search**: Debounce search queries for better performance

### Accessibility
- **ARIA Attributes**: Use proper ARIA roles and attributes
- **Keyboard Support**: Implement complete keyboard navigation
- **Screen Reader Support**: Provide meaningful announcements
- **Focus Management**: Maintain proper focus during tree operations

## Accessibility Considerations

- Uses proper ARIA roles including `tree`, `treeitem`, and `group`
- Supports complete keyboard navigation with arrow keys, Enter, and Space
- Provides screen reader announcements for expand/collapse and selection
- Maintains proper focus management during tree operations
- Includes aria-expanded and aria-selected attributes
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafTreeNode**: Individual tree node component
- **SafCheckbox**: Checkbox component for checkable trees
- **SafLoadingSpinner**: Loading indicator for async operations
- **SafSearchField**: Search input for searchable trees

## Notes

- SafTreeView automatically manages node expansion and selection states
- The component supports both controlled and uncontrolled usage patterns
- Virtual scrolling enables handling of large datasets efficiently
- Drag-and-drop functionality provides intuitive tree reorganization
- Search functionality includes highlighting and auto-expansion
- Async loading supports progressive data fetching
- Performance optimizations handle thousands of nodes smoothly
- Accessibility features provide comprehensive keyboard and screen reader support
