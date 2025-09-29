# SafTreeItem Component

## Overview
The `SafTreeItem` component represents an individual node in a hierarchical tree structure. It provides expandable/collapsible functionality, selection states, and supports nested items. This component is designed to work within tree containers and supports various content types, drag-and-drop operations, and accessibility features for building complex tree views.

## React API

### Props
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the tree item is expanded (shows children) |
| `selected` | `boolean` | `false` | Whether the tree item is selected |
| `disabled` | `boolean` | `false` | Whether the tree item is disabled |
| `level` | `number` | `0` | Nesting level for indentation and accessibility |
| `hasChildren` | `boolean` | `false` | Whether the item has child items |
| `loading` | `boolean` | `false` | Whether the item is in a loading state |
| `draggable` | `boolean` | `false` | Whether the item can be dragged |
| `droppable` | `boolean` | `false` | Whether items can be dropped on this item |
| `icon` | `string` | `undefined` | Icon name to display before the label |
| `expandIcon` | `string` | `'chevron-right'` | Icon for expand/collapse control |
| `id` | `string` | `undefined` | Unique identifier for the tree item |
| `value` | `any` | `undefined` | Value associated with the tree item |
| `onClick` | `(event: MouseEvent) => void` | `undefined` | Click event handler |
| `onExpand` | `(expanded: boolean) => void` | `undefined` | Expand/collapse event handler |
| `onSelect` | `(selected: boolean) => void` | `undefined` | Selection change handler |
| `onDragStart` | `(event: DragEvent) => void` | `undefined` | Drag start handler |
| `onDrop` | `(event: DragEvent) => void` | `undefined` | Drop handler |
| `className` | `string` | `''` | Additional CSS classes |
| `children` | `ReactNode` | `undefined` | Child tree items and content |

### Events
- `onClick`: Fired when the tree item is clicked
- `onExpand`: Fired when the item is expanded or collapsed
- `onSelect`: Fired when the selection state changes
- `onDragStart`: Fired when drag operation starts
- `onDrop`: Fired when items are dropped on this item
- `onFocus`: Fired when the item receives focus
- `onBlur`: Fired when the item loses focus

## Angular API

### Properties
| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `expanded` | `boolean` | `false` | Whether the tree item is expanded |
| `selected` | `boolean` | `false` | Whether the tree item is selected |
| `disabled` | `boolean` | `false` | Whether the tree item is disabled |
| `level` | `number` | `0` | Nesting level for indentation |
| `hasChildren` | `boolean` | `false` | Whether the item has child items |
| `loading` | `boolean` | `false` | Whether the item is in a loading state |
| `draggable` | `boolean` | `false` | Whether the item can be dragged |
| `droppable` | `boolean` | `false` | Whether items can be dropped on this item |
| `icon` | `string` | `undefined` | Icon name to display |
| `expandIcon` | `string` | `'chevron-right'` | Expand/collapse icon |
| `id` | `string` | `undefined` | Unique identifier |
| `value` | `any` | `undefined` | Associated value |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `(click)` | `EventEmitter<MouseEvent>` | Emitted when clicked |
| `(expand)` | `EventEmitter<boolean>` | Emitted on expand/collapse |
| `(select)` | `EventEmitter<boolean>` | Emitted on selection change |
| `(dragstart)` | `EventEmitter<DragEvent>` | Emitted on drag start |
| `(drop)` | `EventEmitter<DragEvent>` | Emitted on drop |
| `(focus)` | `EventEmitter<FocusEvent>` | Emitted on focus |
| `(blur)` | `EventEmitter<FocusEvent>` | Emitted on blur |

### Content Projection
- **Default slot**: Tree item label and child items
- **`icon` slot**: Custom icon content
- **`actions` slot**: Action buttons (edit, delete, etc.)
- **`loading` slot**: Custom loading indicator

## Usage Examples

### Basic Tree Structure

#### React
```jsx
import { SafTree, SafTreeItem, SafIcon } from '@saffron/core-components';
import { useState } from 'react';

function BasicTreeExample() {
  const [expandedNodes, setExpandedNodes] = useState(new Set(['folder1']));
  const [selectedNode, setSelectedNode] = useState(null);

  const handleExpand = (nodeId, expanded) => {
    const newExpanded = new Set(expandedNodes);
    if (expanded) {
      newExpanded.add(nodeId);
    } else {
      newExpanded.delete(nodeId);
    }
    setExpandedNodes(newExpanded);
  };

  const handleSelect = (nodeId) => {
    setSelectedNode(nodeId);
  };

  return (
    <SafTree>
      <SafTreeItem
        id="folder1"
        hasChildren
        expanded={expandedNodes.has('folder1')}
        selected={selectedNode === 'folder1'}
        icon="folder"
        onExpand={(expanded) => handleExpand('folder1', expanded)}
        onClick={() => handleSelect('folder1')}
      >
        Documents
        
        <SafTreeItem
          id="file1"
          level={1}
          selected={selectedNode === 'file1'}
          icon="document"
          onClick={() => handleSelect('file1')}
        >
          Report.pdf
        </SafTreeItem>
        
        <SafTreeItem
          id="file2"
          level={1}
          selected={selectedNode === 'file2'}
          icon="document"
          onClick={() => handleSelect('file2')}
        >
          Presentation.pptx
        </SafTreeItem>
        
        <SafTreeItem
          id="subfolder1"
          level={1}
          hasChildren
          expanded={expandedNodes.has('subfolder1')}
          selected={selectedNode === 'subfolder1'}
          icon="folder"
          onExpand={(expanded) => handleExpand('subfolder1', expanded)}
          onClick={() => handleSelect('subfolder1')}
        >
          Archive
          
          <SafTreeItem
            id="oldfile1"
            level={2}
            selected={selectedNode === 'oldfile1'}
            icon="document"
            onClick={() => handleSelect('oldfile1')}
          >
            OldReport.pdf
          </SafTreeItem>
        </SafTreeItem>
      </SafTreeItem>
      
      <SafTreeItem
        id="folder2"
        hasChildren
        expanded={expandedNodes.has('folder2')}
        selected={selectedNode === 'folder2'}
        icon="folder"
        onExpand={(expanded) => handleExpand('folder2', expanded)}
        onClick={() => handleSelect('folder2')}
      >
        Images
        
        <SafTreeItem
          id="image1"
          level={1}
          selected={selectedNode === 'image1'}
          icon="image"
          onClick={() => handleSelect('image1')}
        >
          Screenshot.png
        </SafTreeItem>
      </SafTreeItem>
    </SafTree>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-tree',
  template: `
    <saf-tree>
      <saf-tree-item
        id="folder1"
        [hasChildren]="true"
        [expanded]="expandedNodes.has('folder1')"
        [selected]="selectedNode === 'folder1'"
        icon="folder"
        (expand)="handleExpand('folder1', $event)"
        (click)="handleSelect('folder1')"
      >
        Documents
        
        <saf-tree-item
          id="file1"
          [level]="1"
          [selected]="selectedNode === 'file1'"
          icon="document"
          (click)="handleSelect('file1')"
        >
          Report.pdf
        </saf-tree-item>
        
        <saf-tree-item
          id="file2"
          [level]="1"
          [selected]="selectedNode === 'file2'"
          icon="document"
          (click)="handleSelect('file2')"
        >
          Presentation.pptx
        </saf-tree-item>
        
        <saf-tree-item
          id="subfolder1"
          [level]="1"
          [hasChildren]="true"
          [expanded]="expandedNodes.has('subfolder1')"
          [selected]="selectedNode === 'subfolder1'"
          icon="folder"
          (expand)="handleExpand('subfolder1', $event)"
          (click)="handleSelect('subfolder1')"
        >
          Archive
          
          <saf-tree-item
            id="oldfile1"
            [level]="2"
            [selected]="selectedNode === 'oldfile1'"
            icon="document"
            (click)="handleSelect('oldfile1')"
          >
            OldReport.pdf
          </saf-tree-item>
        </saf-tree-item>
      </saf-tree-item>
      
      <saf-tree-item
        id="folder2"
        [hasChildren]="true"
        [expanded]="expandedNodes.has('folder2')"
        [selected]="selectedNode === 'folder2'"
        icon="folder"
        (expand)="handleExpand('folder2', $event)"
        (click)="handleSelect('folder2')"
      >
        Images
        
        <saf-tree-item
          id="image1"
          [level]="1"
          [selected]="selectedNode === 'image1'"
          icon="image"
          (click)="handleSelect('image1')"
        >
          Screenshot.png
        </saf-tree-item>
      </saf-tree-item>
    </saf-tree>
  `
})
export class BasicTreeComponent {
  expandedNodes = new Set(['folder1']);
  selectedNode: string | null = null;

  handleExpand(nodeId: string, expanded: boolean) {
    if (expanded) {
      this.expandedNodes.add(nodeId);
    } else {
      this.expandedNodes.delete(nodeId);
    }
    this.expandedNodes = new Set(this.expandedNodes);
  }

  handleSelect(nodeId: string) {
    this.selectedNode = nodeId;
  }
}
```

### Tree with Actions and Context Menu

#### React
```jsx
import { SafTree, SafTreeItem, SafButton, SafIcon, SafMenu } from '@saffron/core-components';
import { useState } from 'react';

function TreeWithActionsExample() {
  const [tree, setTree] = useState([
    {
      id: 'project1',
      name: 'Project Alpha',
      type: 'project',
      children: [
        { id: 'task1', name: 'Task 1', type: 'task' },
        { id: 'task2', name: 'Task 2', type: 'task' }
      ]
    },
    {
      id: 'project2',
      name: 'Project Beta',
      type: 'project',
      children: [
        { id: 'task3', name: 'Task 3', type: 'task' }
      ]
    }
  ]);
  const [expandedNodes, setExpandedNodes] = useState(new Set(['project1']));
  const [selectedNode, setSelectedNode] = useState(null);

  const addItem = (parentId, type) => {
    const newId = `${type}${Date.now()}`;
    const newItem = {
      id: newId,
      name: `New ${type}`,
      type: type,
      children: type === 'project' ? [] : undefined
    };

    setTree(prevTree => {
      const addToNode = (nodes) => {
        return nodes.map(node => {
          if (node.id === parentId) {
            return {
              ...node,
              children: [...(node.children || []), newItem]
            };
          }
          if (node.children) {
            return { ...node, children: addToNode(node.children) };
          }
          return node;
        });
      };
      return parentId ? addToNode(prevTree) : [...prevTree, newItem];
    });
  };

  const deleteItem = (itemId) => {
    setTree(prevTree => {
      const removeFromNode = (nodes) => {
        return nodes.filter(node => {
          if (node.id === itemId) return false;
          if (node.children) {
            node.children = removeFromNode(node.children);
          }
          return true;
        });
      };
      return removeFromNode(prevTree);
    });
    if (selectedNode === itemId) {
      setSelectedNode(null);
    }
  };

  const renderTreeNode = (node, level = 0) => (
    <SafTreeItem
      key={node.id}
      id={node.id}
      level={level}
      hasChildren={node.children && node.children.length > 0}
      expanded={expandedNodes.has(node.id)}
      selected={selectedNode === node.id}
      icon={node.type === 'project' ? 'folder' : 'document'}
      onExpand={(expanded) => handleExpand(node.id, expanded)}
      onClick={() => setSelectedNode(node.id)}
    >
      <span>{node.name}</span>
      
      <div slot="actions">
        {node.type === 'project' && (
          <SafButton
            variant="ghost"
            size="small"
            onClick={(e) => {
              e.stopPropagation();
              addItem(node.id, 'task');
            }}
          >
            <SafIcon name="plus" />
          </SafButton>
        )}
        <SafButton
          variant="ghost"
          size="small"
          onClick={(e) => {
            e.stopPropagation();
            deleteItem(node.id);
          }}
        >
          <SafIcon name="trash" />
        </SafButton>
      </div>
      
      {node.children && node.children.map(child => 
        renderTreeNode(child, level + 1)
      )}
    </SafTreeItem>
  );

  const handleExpand = (nodeId, expanded) => {
    const newExpanded = new Set(expandedNodes);
    if (expanded) {
      newExpanded.add(nodeId);
    } else {
      newExpanded.delete(nodeId);
    }
    setExpandedNodes(newExpanded);
  };

  return (
    <div>
      <div style={{ marginBottom: '1rem' }}>
        <SafButton onClick={() => addItem(null, 'project')}>
          Add Project
        </SafButton>
      </div>
      
      <SafTree>
        {tree.map(node => renderTreeNode(node))}
      </SafTree>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface TreeNode {
  id: string;
  name: string;
  type: 'project' | 'task';
  children?: TreeNode[];
}

@Component({
  selector: 'app-tree-with-actions',
  template: `
    <div>
      <div style="margin-bottom: 1rem;">
        <saf-button (click)="addItem(null, 'project')">
          Add Project
        </saf-button>
      </div>
      
      <saf-tree>
        <ng-container *ngFor="let node of tree">
          <ng-container *ngTemplateOutlet="treeNodeTemplate; context: { node: node, level: 0 }"></ng-container>
        </ng-container>
      </saf-tree>
    </div>

    <ng-template #treeNodeTemplate let-node="node" let-level="level">
      <saf-tree-item
        [id]="node.id"
        [level]="level"
        [hasChildren]="node.children && node.children.length > 0"
        [expanded]="expandedNodes.has(node.id)"
        [selected]="selectedNode === node.id"
        [icon]="node.type === 'project' ? 'folder' : 'document'"
        (expand)="handleExpand(node.id, $event)"
        (click)="setSelectedNode(node.id)"
      >
        <span>{{node.name}}</span>
        
        <div slot="actions">
          <saf-button
            *ngIf="node.type === 'project'"
            variant="ghost"
            size="small"
            (click)="addItem(node.id, 'task'); $event.stopPropagation()"
          >
            <saf-icon name="plus"></saf-icon>
          </saf-button>
          <saf-button
            variant="ghost"
            size="small"
            (click)="deleteItem(node.id); $event.stopPropagation()"
          >
            <saf-icon name="trash"></saf-icon>
          </saf-button>
        </div>
        
        <ng-container *ngIf="node.children">
          <ng-container *ngFor="let child of node.children">
            <ng-container *ngTemplateOutlet="treeNodeTemplate; context: { node: child, level: level + 1 }"></ng-container>
          </ng-container>
        </ng-container>
      </saf-tree-item>
    </ng-template>
  `
})
export class TreeWithActionsComponent {
  tree: TreeNode[] = [
    {
      id: 'project1',
      name: 'Project Alpha',
      type: 'project',
      children: [
        { id: 'task1', name: 'Task 1', type: 'task' },
        { id: 'task2', name: 'Task 2', type: 'task' }
      ]
    },
    {
      id: 'project2',
      name: 'Project Beta',
      type: 'project',
      children: [
        { id: 'task3', name: 'Task 3', type: 'task' }
      ]
    }
  ];
  expandedNodes = new Set(['project1']);
  selectedNode: string | null = null;

  addItem(parentId: string | null, type: 'project' | 'task') {
    const newId = `${type}${Date.now()}`;
    const newItem: TreeNode = {
      id: newId,
      name: `New ${type}`,
      type: type,
      children: type === 'project' ? [] : undefined
    };

    if (parentId) {
      this.addToNode(this.tree, parentId, newItem);
    } else {
      this.tree = [...this.tree, newItem];
    }
  }

  private addToNode(nodes: TreeNode[], parentId: string, newItem: TreeNode): boolean {
    for (const node of nodes) {
      if (node.id === parentId) {
        node.children = [...(node.children || []), newItem];
        return true;
      }
      if (node.children && this.addToNode(node.children, parentId, newItem)) {
        return true;
      }
    }
    return false;
  }

  deleteItem(itemId: string) {
    this.tree = this.removeFromNodes(this.tree, itemId);
    if (this.selectedNode === itemId) {
      this.selectedNode = null;
    }
  }

  private removeFromNodes(nodes: TreeNode[], itemId: string): TreeNode[] {
    return nodes.filter(node => {
      if (node.id === itemId) return false;
      if (node.children) {
        node.children = this.removeFromNodes(node.children, itemId);
      }
      return true;
    });
  }

  handleExpand(nodeId: string, expanded: boolean) {
    if (expanded) {
      this.expandedNodes.add(nodeId);
    } else {
      this.expandedNodes.delete(nodeId);
    }
    this.expandedNodes = new Set(this.expandedNodes);
  }

  setSelectedNode(nodeId: string) {
    this.selectedNode = nodeId;
  }
}
```

### Lazy Loading Tree

#### React
```jsx
import { SafTree, SafTreeItem, SafSpinner, SafIcon } from '@saffron/core-components';
import { useState } from 'react';

function LazyTreeExample() {
  const [nodes, setNodes] = useState([
    { id: 'root1', name: 'Folder 1', hasChildren: true, loaded: false, children: [] },
    { id: 'root2', name: 'Folder 2', hasChildren: true, loaded: false, children: [] },
    { id: 'file1', name: 'File 1.txt', hasChildren: false, loaded: true, children: [] }
  ]);
  const [expandedNodes, setExpandedNodes] = useState(new Set());
  const [loadingNodes, setLoadingNodes] = useState(new Set());

  const loadChildren = async (nodeId) => {
    if (loadingNodes.has(nodeId)) return;
    
    setLoadingNodes(prev => new Set(prev).add(nodeId));
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const mockChildren = [
      { id: `${nodeId}_child1`, name: 'Subfolder A', hasChildren: true, loaded: false, children: [] },
      { id: `${nodeId}_child2`, name: 'Document.pdf', hasChildren: false, loaded: true, children: [] },
      { id: `${nodeId}_child3`, name: 'Image.png', hasChildren: false, loaded: true, children: [] }
    ];
    
    setNodes(prevNodes => {
      const updateNode = (nodes) => {
        return nodes.map(node => {
          if (node.id === nodeId) {
            return { ...node, children: mockChildren, loaded: true };
          }
          if (node.children) {
            return { ...node, children: updateNode(node.children) };
          }
          return node;
        });
      };
      return updateNode(prevNodes);
    });
    
    setLoadingNodes(prev => {
      const newSet = new Set(prev);
      newSet.delete(nodeId);
      return newSet;
    });
  };

  const handleExpand = async (nodeId, expanded) => {
    const newExpanded = new Set(expandedNodes);
    if (expanded) {
      newExpanded.add(nodeId);
      
      // Load children if not loaded
      const node = findNode(nodes, nodeId);
      if (node && node.hasChildren && !node.loaded) {
        await loadChildren(nodeId);
      }
    } else {
      newExpanded.delete(nodeId);
    }
    setExpandedNodes(newExpanded);
  };

  const findNode = (nodes, id) => {
    for (const node of nodes) {
      if (node.id === id) return node;
      if (node.children) {
        const found = findNode(node.children, id);
        if (found) return found;
      }
    }
    return null;
  };

  const renderNode = (node, level = 0) => (
    <SafTreeItem
      key={node.id}
      id={node.id}
      level={level}
      hasChildren={node.hasChildren}
      expanded={expandedNodes.has(node.id)}
      loading={loadingNodes.has(node.id)}
      icon={node.hasChildren ? 'folder' : 'document'}
      onExpand={(expanded) => handleExpand(node.id, expanded)}
    >
      {node.name}
      
      {loadingNodes.has(node.id) && (
        <SafSpinner slot="loading" size="small" />
      )}
      
      {node.children && node.children.map(child => 
        renderNode(child, level + 1)
      )}
    </SafTreeItem>
  );

  return (
    <SafTree>
      {nodes.map(node => renderNode(node))}
    </SafTree>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface LazyTreeNode {
  id: string;
  name: string;
  hasChildren: boolean;
  loaded: boolean;
  children: LazyTreeNode[];
}

@Component({
  selector: 'app-lazy-tree',
  template: `
    <saf-tree>
      <ng-container *ngFor="let node of nodes">
        <ng-container *ngTemplateOutlet="lazyNodeTemplate; context: { node: node, level: 0 }"></ng-container>
      </ng-container>
    </saf-tree>

    <ng-template #lazyNodeTemplate let-node="node" let-level="level">
      <saf-tree-item
        [id]="node.id"
        [level]="level"
        [hasChildren]="node.hasChildren"
        [expanded]="expandedNodes.has(node.id)"
        [loading]="loadingNodes.has(node.id)"
        [icon]="node.hasChildren ? 'folder' : 'document'"
        (expand)="handleExpand(node.id, $event)"
      >
        {{node.name}}
        
        <saf-spinner 
          *ngIf="loadingNodes.has(node.id)"
          slot="loading" 
          size="small"
        ></saf-spinner>
        
        <ng-container *ngIf="node.children">
          <ng-container *ngFor="let child of node.children">
            <ng-container *ngTemplateOutlet="lazyNodeTemplate; context: { node: child, level: level + 1 }"></ng-container>
          </ng-container>
        </ng-container>
      </saf-tree-item>
    </ng-template>
  `
})
export class LazyTreeComponent {
  nodes: LazyTreeNode[] = [
    { id: 'root1', name: 'Folder 1', hasChildren: true, loaded: false, children: [] },
    { id: 'root2', name: 'Folder 2', hasChildren: true, loaded: false, children: [] },
    { id: 'file1', name: 'File 1.txt', hasChildren: false, loaded: true, children: [] }
  ];
  expandedNodes = new Set<string>();
  loadingNodes = new Set<string>();

  async handleExpand(nodeId: string, expanded: boolean) {
    if (expanded) {
      this.expandedNodes.add(nodeId);
      
      // Load children if not loaded
      const node = this.findNode(this.nodes, nodeId);
      if (node && node.hasChildren && !node.loaded) {
        await this.loadChildren(nodeId);
      }
    } else {
      this.expandedNodes.delete(nodeId);
    }
    this.expandedNodes = new Set(this.expandedNodes);
  }

  async loadChildren(nodeId: string) {
    if (this.loadingNodes.has(nodeId)) return;
    
    this.loadingNodes.add(nodeId);
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const mockChildren: LazyTreeNode[] = [
      { id: `${nodeId}_child1`, name: 'Subfolder A', hasChildren: true, loaded: false, children: [] },
      { id: `${nodeId}_child2`, name: 'Document.pdf', hasChildren: false, loaded: true, children: [] },
      { id: `${nodeId}_child3`, name: 'Image.png', hasChildren: false, loaded: true, children: [] }
    ];
    
    this.updateNode(this.nodes, nodeId, mockChildren);
    this.loadingNodes.delete(nodeId);
  }

  private updateNode(nodes: LazyTreeNode[], nodeId: string, children: LazyTreeNode[]) {
    for (const node of nodes) {
      if (node.id === nodeId) {
        node.children = children;
        node.loaded = true;
        return;
      }
      if (node.children) {
        this.updateNode(node.children, nodeId, children);
      }
    }
  }

  private findNode(nodes: LazyTreeNode[], id: string): LazyTreeNode | null {
    for (const node of nodes) {
      if (node.id === id) return node;
      if (node.children) {
        const found = this.findNode(node.children, id);
        if (found) return found;
      }
    }
    return null;
  }
}
```

### Drag and Drop Tree

#### React
```jsx
import { SafTree, SafTreeItem, SafIcon } from '@saffron/core-components';
import { useState } from 'react';

function DragDropTreeExample() {
  const [treeData, setTreeData] = useState([
    {
      id: 'folder1',
      name: 'Documents',
      type: 'folder',
      children: [
        { id: 'file1', name: 'Report.pdf', type: 'file' },
        { id: 'file2', name: 'Notes.txt', type: 'file' }
      ]
    },
    {
      id: 'folder2',
      name: 'Images',
      type: 'folder',
      children: [
        { id: 'file3', name: 'Photo.jpg', type: 'file' }
      ]
    }
  ]);
  const [expandedNodes, setExpandedNodes] = useState(new Set(['folder1', 'folder2']));
  const [draggedItem, setDraggedItem] = useState(null);

  const handleDragStart = (e, nodeId) => {
    setDraggedItem(nodeId);
    e.dataTransfer.effectAllowed = 'move';
    e.dataTransfer.setData('text/plain', nodeId);
  };

  const handleDrop = (e, targetId) => {
    e.preventDefault();
    const draggedId = e.dataTransfer.getData('text/plain');
    
    if (draggedId === targetId) return;
    
    // Move the dragged item to the target folder
    setTreeData(prevData => {
      const newData = JSON.parse(JSON.stringify(prevData));
      const draggedNode = removeNode(newData, draggedId);
      
      if (draggedNode) {
        addNodeToFolder(newData, targetId, draggedNode);
      }
      
      return newData;
    });
    
    setDraggedItem(null);
  };

  const handleDragOver = (e) => {
    e.preventDefault();
    e.dataTransfer.dropEffect = 'move';
  };

  const removeNode = (nodes, nodeId) => {
    for (let i = 0; i < nodes.length; i++) {
      if (nodes[i].id === nodeId) {
        return nodes.splice(i, 1)[0];
      }
      if (nodes[i].children) {
        const found = removeNode(nodes[i].children, nodeId);
        if (found) return found;
      }
    }
    return null;
  };

  const addNodeToFolder = (nodes, folderId, nodeToAdd) => {
    for (const node of nodes) {
      if (node.id === folderId && node.type === 'folder') {
        if (!node.children) node.children = [];
        node.children.push(nodeToAdd);
        return true;
      }
      if (node.children && addNodeToFolder(node.children, folderId, nodeToAdd)) {
        return true;
      }
    }
    return false;
  };

  const renderNode = (node, level = 0) => (
    <SafTreeItem
      key={node.id}
      id={node.id}
      level={level}
      hasChildren={node.children && node.children.length > 0}
      expanded={expandedNodes.has(node.id)}
      draggable={true}
      droppable={node.type === 'folder'}
      icon={node.type === 'folder' ? 'folder' : 'document'}
      onExpand={(expanded) => handleExpand(node.id, expanded)}
      onDragStart={(e) => handleDragStart(e, node.id)}
      onDrop={(e) => handleDrop(e, node.id)}
      onDragOver={handleDragOver}
      style={{
        opacity: draggedItem === node.id ? 0.5 : 1
      }}
    >
      {node.name}
      
      {node.children && node.children.map(child => 
        renderNode(child, level + 1)
      )}
    </SafTreeItem>
  );

  const handleExpand = (nodeId, expanded) => {
    const newExpanded = new Set(expandedNodes);
    if (expanded) {
      newExpanded.add(nodeId);
    } else {
      newExpanded.delete(nodeId);
    }
    setExpandedNodes(newExpanded);
  };

  return (
    <div>
      <p>Drag files and folders to reorganize the tree structure.</p>
      <SafTree>
        {treeData.map(node => renderNode(node))}
      </SafTree>
    </div>
  );
}
```

#### Angular
```typescript
// Component
import { Component } from '@angular/core';

interface DragTreeNode {
  id: string;
  name: string;
  type: 'folder' | 'file';
  children?: DragTreeNode[];
}

@Component({
  selector: 'app-drag-drop-tree',
  template: `
    <div>
      <p>Drag files and folders to reorganize the tree structure.</p>
      <saf-tree>
        <ng-container *ngFor="let node of treeData">
          <ng-container *ngTemplateOutlet="dragNodeTemplate; context: { node: node, level: 0 }"></ng-container>
        </ng-container>
      </saf-tree>
    </div>

    <ng-template #dragNodeTemplate let-node="node" let-level="level">
      <saf-tree-item
        [id]="node.id"
        [level]="level"
        [hasChildren]="node.children && node.children.length > 0"
        [expanded]="expandedNodes.has(node.id)"
        [draggable]="true"
        [droppable]="node.type === 'folder'"
        [icon]="node.type === 'folder' ? 'folder' : 'document'"
        [style.opacity]="draggedItem === node.id ? 0.5 : 1"
        (expand)="handleExpand(node.id, $event)"
        (dragstart)="handleDragStart($event, node.id)"
        (drop)="handleDrop($event, node.id)"
        (dragover)="handleDragOver($event)"
      >
        {{node.name}}
        
        <ng-container *ngIf="node.children">
          <ng-container *ngFor="let child of node.children">
            <ng-container *ngTemplateOutlet="dragNodeTemplate; context: { node: child, level: level + 1 }"></ng-container>
          </ng-container>
        </ng-container>
      </saf-tree-item>
    </ng-template>
  `
})
export class DragDropTreeComponent {
  treeData: DragTreeNode[] = [
    {
      id: 'folder1',
      name: 'Documents',
      type: 'folder',
      children: [
        { id: 'file1', name: 'Report.pdf', type: 'file' },
        { id: 'file2', name: 'Notes.txt', type: 'file' }
      ]
    },
    {
      id: 'folder2',
      name: 'Images',
      type: 'folder',
      children: [
        { id: 'file3', name: 'Photo.jpg', type: 'file' }
      ]
    }
  ];
  expandedNodes = new Set(['folder1', 'folder2']);
  draggedItem: string | null = null;

  handleDragStart(e: DragEvent, nodeId: string) {
    this.draggedItem = nodeId;
    if (e.dataTransfer) {
      e.dataTransfer.effectAllowed = 'move';
      e.dataTransfer.setData('text/plain', nodeId);
    }
  }

  handleDrop(e: DragEvent, targetId: string) {
    e.preventDefault();
    if (!e.dataTransfer) return;
    
    const draggedId = e.dataTransfer.getData('text/plain');
    
    if (draggedId === targetId) return;
    
    // Move the dragged item to the target folder
    const newData = JSON.parse(JSON.stringify(this.treeData));
    const draggedNode = this.removeNode(newData, draggedId);
    
    if (draggedNode) {
      this.addNodeToFolder(newData, targetId, draggedNode);
      this.treeData = newData;
    }
    
    this.draggedItem = null;
  }

  handleDragOver(e: DragEvent) {
    e.preventDefault();
    if (e.dataTransfer) {
      e.dataTransfer.dropEffect = 'move';
    }
  }

  handleExpand(nodeId: string, expanded: boolean) {
    if (expanded) {
      this.expandedNodes.add(nodeId);
    } else {
      this.expandedNodes.delete(nodeId);
    }
    this.expandedNodes = new Set(this.expandedNodes);
  }

  private removeNode(nodes: DragTreeNode[], nodeId: string): DragTreeNode | null {
    for (let i = 0; i < nodes.length; i++) {
      if (nodes[i].id === nodeId) {
        return nodes.splice(i, 1)[0];
      }
      if (nodes[i].children) {
        const found = this.removeNode(nodes[i].children, nodeId);
        if (found) return found;
      }
    }
    return null;
  }

  private addNodeToFolder(nodes: DragTreeNode[], folderId: string, nodeToAdd: DragTreeNode): boolean {
    for (const node of nodes) {
      if (node.id === folderId && node.type === 'folder') {
        if (!node.children) node.children = [];
        node.children.push(nodeToAdd);
        return true;
      }
      if (node.children && this.addNodeToFolder(node.children, folderId, nodeToAdd)) {
        return true;
      }
    }
    return false;
  }
}
```

## Best Practices

1. **Hierarchical Structure**: Maintain clear parent-child relationships
2. **Performance**: Use lazy loading for large tree structures
3. **State Management**: Properly handle expanded/selected state across renders
4. **Keyboard Navigation**: Support arrow keys for navigation, Enter/Space for selection
5. **Visual Indentation**: Use appropriate indentation to show hierarchy levels
6. **Loading States**: Show loading indicators when fetching child nodes
7. **Drag Operations**: Provide clear visual feedback during drag and drop
8. **Memory Management**: Clean up event listeners and avoid memory leaks

## Accessibility Considerations

- Use proper ARIA attributes (role="treeitem", aria-expanded, aria-level)
- Support keyboard navigation (Arrow keys, Enter, Space, Home, End)
- Provide clear focus indicators
- Use semantic markup for tree structure
- Announce state changes to screen readers
- Ensure sufficient color contrast for all states
- Support screen reader navigation with proper labeling

## Related Components

- `SafTree`: Container component for tree structures
- `SafIcon`: For node icons and expand/collapse indicators
- `SafButton`: For action buttons within tree items
- `SafSpinner`: For loading states
- `SafMenu`: For context menus on tree items
- `SafCheckbox`: For multi-selection tree functionality

## Notes

- Tree items should be used within `SafTree` containers
- The `level` prop is important for proper indentation and accessibility
- Use `hasChildren` to show expand/collapse controls even when children aren't loaded yet
- Drag and drop functionality requires careful state management
- Consider virtualization for very large trees to maintain performance
- Always provide unique `id` props for proper state management and accessibility
