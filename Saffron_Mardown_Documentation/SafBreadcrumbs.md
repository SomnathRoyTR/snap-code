# SafBreadcrumbs Component

## Overview

SafBreadcrumbs is a navigation component that provides hierarchical breadcrumb navigation, allowing users to understand their current location within an application and navigate back to parent pages. The component supports various display styles, custom separators, dynamic breadcrumb generation, and accessibility features to ensure seamless navigation experiences across different application contexts.

## React API

### SafBreadcrumbs

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `items` | `BreadcrumbItem[]` | Yes | - | Array of breadcrumb items to display |
| `separator` | `string \| ReactNode` | No | `'/'` | Separator between breadcrumb items |
| `maxItems` | `number` | No | - | Maximum number of items to display |
| `showHome` | `boolean` | No | `true` | Whether to show home/root item |
| `homeIcon` | `string \| ReactNode` | No | `'home'` | Icon for home breadcrumb |
| `homeLabel` | `string` | No | `'Home'` | Label for home breadcrumb |
| `homeHref` | `string` | No | `'/'` | URL for home breadcrumb |
| `variant` | `'default' \| 'minimal' \| 'rounded' \| 'underlined'` | No | `'default'` | Visual style variant |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant |
| `collapsible` | `boolean` | No | `false` | Enable collapsing of middle items |
| `collapseFrom` | `'start' \| 'middle' \| 'end'` | No | `'middle'` | Where to collapse items |
| `showTooltips` | `boolean` | No | `false` | Show tooltips on collapsed items |
| `interactive` | `boolean` | No | `true` | Whether breadcrumbs are clickable |
| `loading` | `boolean` | No | `false` | Show loading state |
| `showIcons` | `boolean` | No | `false` | Show icons for each breadcrumb |
| `truncate` | `boolean \| 'start' \| 'middle' \| 'end'` | No | `false` | Text truncation behavior |
| `maxWidth` | `string \| number` | No | - | Maximum width for breadcrumb container |
| `onItemClick` | `(item: BreadcrumbItem, index: number) => void` | No | - | Callback when breadcrumb is clicked |
| `onHomeClick` | `() => void` | No | - | Callback when home is clicked |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### BreadcrumbItem Interface

```typescript
interface BreadcrumbItem {
  id: string;
  label: string;
  href?: string;
  icon?: string | ReactNode;
  current?: boolean;
  disabled?: boolean;
  metadata?: { [key: string]: any };
  tooltip?: string;
  badge?: string | ReactNode;
  subItems?: BreadcrumbItem[];
}
```

## Angular API

### saf-breadcrumbs

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[items]` | `BreadcrumbItem[]` | Yes | - | Array of breadcrumb items to display |
| `[separator]` | `string \| TemplateRef` | No | `'/'` | Separator between breadcrumb items |
| `[maxItems]` | `number` | No | - | Maximum number of items to display |
| `[showHome]` | `boolean` | No | `true` | Whether to show home/root item |
| `[homeIcon]` | `string \| TemplateRef` | No | `'home'` | Icon for home breadcrumb |
| `[homeLabel]` | `string` | No | `'Home'` | Label for home breadcrumb |
| `[homeHref]` | `string` | No | `'/'` | URL for home breadcrumb |
| `[variant]` | `'default' \| 'minimal' \| 'rounded' \| 'underlined'` | No | `'default'` | Visual style variant |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant |
| `[collapsible]` | `boolean` | No | `false` | Enable collapsing of middle items |
| `[collapseFrom]` | `'start' \| 'middle' \| 'end'` | No | `'middle'` | Where to collapse items |
| `[showTooltips]` | `boolean` | No | `false` | Show tooltips on collapsed items |
| `[interactive]` | `boolean` | No | `true` | Whether breadcrumbs are clickable |
| `[loading]` | `boolean` | No | `false` | Show loading state |
| `[showIcons]` | `boolean` | No | `false` | Show icons for each breadcrumb |
| `[truncate]` | `boolean \| 'start' \| 'middle' \| 'end'` | No | `false` | Text truncation behavior |
| `[maxWidth]` | `string \| number` | No | - | Maximum width for breadcrumb container |
| `(itemClick)` | `EventEmitter<{item: BreadcrumbItem, index: number}>` | No | - | Event when breadcrumb is clicked |
| `(homeClick)` | `EventEmitter<void>` | No | - | Event when home is clicked |

## Usage Examples

### Legal Document Navigation

#### React
```jsx
import { SafBreadcrumbs, SafIcon, SafBadge } from '@saffron/react';
import { useState, useEffect } from 'react';

const LegalDocumentBreadcrumbsExample = () => {
  const [currentPath, setCurrentPath] = useState([]);
  const [loading, setLoading] = useState(false);

  // Legal document hierarchy navigation
  const documentHierarchy = {
    home: {
      id: 'home',
      label: 'Legal Hub',
      href: '/legal',
      icon: 'home'
    },
    contracts: {
      id: 'contracts',
      label: 'Contracts',
      href: '/legal/contracts',
      icon: 'file-text',
      badge: '124'
    },
    commercial: {
      id: 'commercial',
      label: 'Commercial Agreements',
      href: '/legal/contracts/commercial',
      icon: 'briefcase'
    },
    masterService: {
      id: 'master-service',
      label: 'Master Service Agreement',
      href: '/legal/contracts/commercial/master-service',
      icon: 'file'
    },
    currentDoc: {
      id: 'current-doc',
      label: 'MSA-TR-2024-001.docx',
      href: '/legal/contracts/commercial/master-service/MSA-TR-2024-001',
      current: true,
      icon: 'file-check',
      metadata: {
        version: 'v2.1',
        status: 'Under Review',
        lastModified: '2024-01-15'
      }
    }
  };

  // Different navigation scenarios
  const navigationScenarios = {
    document: [
      documentHierarchy.home,
      documentHierarchy.contracts,
      documentHierarchy.commercial,
      documentHierarchy.masterService,
      documentHierarchy.currentDoc
    ],
    searchResults: [
      documentHierarchy.home,
      {
        id: 'search',
        label: 'Search Results',
        href: '/legal/search',
        icon: 'search',
        badge: '47 results'
      },
      {
        id: 'search-query',
        label: '"termination clause"',
        current: true,
        disabled: true
      }
    ],
    templates: [
      documentHierarchy.home,
      {
        id: 'templates',
        label: 'Document Templates',
        href: '/legal/templates',
        icon: 'template'
      },
      {
        id: 'contract-templates',
        label: 'Contract Templates',
        href: '/legal/templates/contracts',
        icon: 'file-plus'
      },
      {
        id: 'template-category',
        label: 'Employment Agreements',
        href: '/legal/templates/contracts/employment',
        current: true
      }
    ],
    workflow: [
      documentHierarchy.home,
      {
        id: 'workflows',
        label: 'Document Workflows',
        href: '/legal/workflows',
        icon: 'workflow'
      },
      {
        id: 'approval-workflow',
        label: 'Contract Approval Workflow',
        href: '/legal/workflows/contract-approval',
        icon: 'check-circle'
      },
      {
        id: 'current-step',
        label: 'Legal Review - Step 3 of 5',
        current: true,
        disabled: true,
        badge: '2 pending'
      }
    ]
  };

  useEffect(() => {
    setCurrentPath(navigationScenarios.document);
  }, []);

  const handleBreadcrumbClick = async (item, index) => {
    if (item.disabled || item.current) return;
    
    setLoading(true);
    console.log('Navigating to:', item.label, item.href);
    
    // Simulate navigation delay
    await new Promise(resolve => setTimeout(resolve, 500));
    
    // Update current path to reflect navigation
    const newPath = currentPath.slice(0, index + 1);
    setCurrentPath(newPath);
    setLoading(false);
  };

  const handleHomeClick = () => {
    console.log('Navigating to home');
    setCurrentPath([documentHierarchy.home]);
  };

  const switchScenario = (scenarioKey) => {
    setCurrentPath(navigationScenarios[scenarioKey]);
  };

  return (
    <div className="legal-breadcrumbs-demo">
      <h2>Legal Document Navigation</h2>

      {/* Scenario Switcher */}
      <div className="scenario-switcher">
        <h3>Navigation Scenarios</h3>
        <div className="scenario-buttons">
          <button onClick={() => switchScenario('document')}>
            Document Hierarchy
          </button>
          <button onClick={() => switchScenario('searchResults')}>
            Search Results
          </button>
          <button onClick={() => switchScenario('templates')}>
            Document Templates
          </button>
          <button onClick={() => switchScenario('workflow')}>
            Workflow Navigation
          </button>
        </div>
      </div>

      {/* Different Breadcrumb Variants */}
      <div className="breadcrumb-variants">
        {/* Default Style */}
        <div className="variant-section">
          <h3>Default Breadcrumbs</h3>
          <SafBreadcrumbs
            items={currentPath}
            separator={<SafIcon name="chevron-right" size="small" />}
            showHome={true}
            showIcons={true}
            interactive={true}
            loading={loading}
            onItemClick={handleBreadcrumbClick}
            onHomeClick={handleHomeClick}
          />
        </div>

        {/* Minimal Style */}
        <div className="variant-section">
          <h3>Minimal Style</h3>
          <SafBreadcrumbs
            items={currentPath}
            variant="minimal"
            separator=">"
            showHome={false}
            showIcons={false}
            size="small"
            onItemClick={handleBreadcrumbClick}
          />
        </div>

        {/* Collapsible Breadcrumbs */}
        <div className="variant-section">
          <h3>Collapsible (Max 3 Items)</h3>
          <SafBreadcrumbs
            items={currentPath}
            variant="rounded"
            maxItems={3}
            collapsible={true}
            collapseFrom="middle"
            showTooltips={true}
            showIcons={true}
            onItemClick={handleBreadcrumbClick}
          />
        </div>

        {/* With Custom Separator */}
        <div className="variant-section">
          <h3>Custom Separator with Truncation</h3>
          <SafBreadcrumbs
            items={currentPath}
            variant="underlined"
            separator={<SafIcon name="arrow-right" size="small" />}
            truncate="middle"
            maxWidth="600px"
            showIcons={true}
            showTooltips={true}
            onItemClick={handleBreadcrumbClick}
          />
        </div>
      </div>

      {/* Complex Navigation Example */}
      <div className="complex-navigation">
        <h3>Complex Navigation with Sub-paths</h3>
        
        <SafBreadcrumbs
          items={[
            {
              id: 'workspace',
              label: 'TR Legal Workspace',
              href: '/workspace',
              icon: 'building',
              tooltip: 'Thomson Reuters Legal Workspace'
            },
            {
              id: 'client',
              label: 'Global Corp Inc.',
              href: '/workspace/clients/global-corp',
              icon: 'users',
              badge: 'Premium',
              subItems: [
                { id: 'overview', label: 'Client Overview', href: '/workspace/clients/global-corp' },
                { id: 'documents', label: 'Documents', href: '/workspace/clients/global-corp/documents' },
                { id: 'contacts', label: 'Contacts', href: '/workspace/clients/global-corp/contacts' }
              ]
            },
            {
              id: 'matter',
              label: 'M&A Transaction #2024-15',
              href: '/workspace/clients/global-corp/matters/ma-2024-15',
              icon: 'folder',
              badge: <SafBadge variant="warning" size="small">Active</SafBadge>
            },
            {
              id: 'documents',
              label: 'Transaction Documents',
              href: '/workspace/clients/global-corp/matters/ma-2024-15/documents',
              icon: 'files'
            },
            {
              id: 'due-diligence',
              label: 'Due Diligence Reports',
              href: '/workspace/clients/global-corp/matters/ma-2024-15/documents/due-diligence',
              current: true,
              badge: '12 files'
            }
          ]}
          variant="default"
          separator={<SafIcon name="chevron-right" size="small" />}
          maxItems={4}
          collapsible={true}
          showIcons={true}
          showTooltips={true}
          onItemClick={handleBreadcrumbClick}
        />
      </div>

      {/* Mobile-Responsive Breadcrumbs */}
      <div className="mobile-responsive">
        <h3>Mobile-Responsive Navigation</h3>
        
        <SafBreadcrumbs
          items={currentPath}
          variant="minimal"
          maxItems={2}
          collapsible={true}
          collapseFrom="start"
          truncate="end"
          size="small"
          showHome={true}
          homeIcon={<SafIcon name="home" />}
          onItemClick={handleBreadcrumbClick}
        />
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-document-breadcrumbs.component.ts
import { Component, OnInit } from '@angular/core';

interface BreadcrumbItem {
  id: string;
  label: string;
  href?: string;
  icon?: string;
  current?: boolean;
  disabled?: boolean;
  metadata?: { [key: string]: any };
  tooltip?: string;
  badge?: string;
  subItems?: BreadcrumbItem[];
}

@Component({
  selector: 'app-legal-document-breadcrumbs',
  template: `
    <div class="legal-breadcrumbs-demo">
      <h2>Legal Document Navigation</h2>

      <!-- Scenario Switcher -->
      <div class="scenario-switcher">
        <h3>Navigation Scenarios</h3>
        <div class="scenario-buttons">
          <button (click)="switchScenario('document')">Document Hierarchy</button>
          <button (click)="switchScenario('searchResults')">Search Results</button>
          <button (click)="switchScenario('templates')">Document Templates</button>
          <button (click)="switchScenario('workflow')">Workflow Navigation</button>
        </div>
      </div>

      <!-- Different Breadcrumb Variants -->
      <div class="breadcrumb-variants">
        <!-- Default Style -->
        <div class="variant-section">
          <h3>Default Breadcrumbs</h3>
          <saf-breadcrumbs
            [items]="currentPath"
            [showHome]="true"
            [showIcons]="true"
            [interactive]="true"
            [loading]="loading"
            (itemClick)="handleBreadcrumbClick($event.item, $event.index)"
            (homeClick)="handleHomeClick()">
            <saf-icon name="chevron-right" size="small" slot="separator"></saf-icon>
          </saf-breadcrumbs>
        </div>

        <!-- Minimal Style -->
        <div class="variant-section">
          <h3>Minimal Style</h3>
          <saf-breadcrumbs
            [items]="currentPath"
            variant="minimal"
            separator=">"
            [showHome]="false"
            [showIcons]="false"
            size="small"
            (itemClick)="handleBreadcrumbClick($event.item, $event.index)">
          </saf-breadcrumbs>
        </div>

        <!-- Collapsible Breadcrumbs -->
        <div class="variant-section">
          <h3>Collapsible (Max 3 Items)</h3>
          <saf-breadcrumbs
            [items]="currentPath"
            variant="rounded"
            [maxItems]="3"
            [collapsible]="true"
            collapseFrom="middle"
            [showTooltips]="true"
            [showIcons]="true"
            (itemClick)="handleBreadcrumbClick($event.item, $event.index)">
          </saf-breadcrumbs>
        </div>

        <!-- With Custom Separator -->
        <div class="variant-section">
          <h3>Custom Separator with Truncation</h3>
          <saf-breadcrumbs
            [items]="currentPath"
            variant="underlined"
            truncate="middle"
            maxWidth="600px"
            [showIcons]="true"
            [showTooltips]="true"
            (itemClick)="handleBreadcrumbClick($event.item, $event.index)">
            <saf-icon name="arrow-right" size="small" slot="separator"></saf-icon>
          </saf-breadcrumbs>
        </div>
      </div>

      <!-- Complex Navigation Example -->
      <div class="complex-navigation">
        <h3>Complex Navigation with Sub-paths</h3>
        
        <saf-breadcrumbs
          [items]="complexNavigationItems"
          variant="default"
          [maxItems]="4"
          [collapsible]="true"
          [showIcons]="true"
          [showTooltips]="true"
          (itemClick)="handleBreadcrumbClick($event.item, $event.index)">
          <saf-icon name="chevron-right" size="small" slot="separator"></saf-icon>
        </saf-breadcrumbs>
      </div>

      <!-- Mobile-Responsive Breadcrumbs -->
      <div class="mobile-responsive">
        <h3>Mobile-Responsive Navigation</h3>
        
        <saf-breadcrumbs
          [items]="currentPath"
          variant="minimal"
          [maxItems]="2"
          [collapsible]="true"
          collapseFrom="start"
          truncate="end"
          size="small"
          [showHome]="true"
          homeIcon="home"
          (itemClick)="handleBreadcrumbClick($event.item, $event.index)">
        </saf-breadcrumbs>
      </div>
    </div>
  `
})
export class LegalDocumentBreadcrumbsComponent implements OnInit {
  currentPath: BreadcrumbItem[] = [];
  loading = false;

  // Document hierarchy data
  documentHierarchy = {
    home: {
      id: 'home',
      label: 'Legal Hub',
      href: '/legal',
      icon: 'home'
    },
    contracts: {
      id: 'contracts',
      label: 'Contracts',
      href: '/legal/contracts',
      icon: 'file-text',
      badge: '124'
    },
    commercial: {
      id: 'commercial',
      label: 'Commercial Agreements',
      href: '/legal/contracts/commercial',
      icon: 'briefcase'
    },
    masterService: {
      id: 'master-service',
      label: 'Master Service Agreement',
      href: '/legal/contracts/commercial/master-service',
      icon: 'file'
    },
    currentDoc: {
      id: 'current-doc',
      label: 'MSA-TR-2024-001.docx',
      href: '/legal/contracts/commercial/master-service/MSA-TR-2024-001',
      current: true,
      icon: 'file-check',
      metadata: {
        version: 'v2.1',
        status: 'Under Review',
        lastModified: '2024-01-15'
      }
    }
  };

  navigationScenarios = {
    document: [
      this.documentHierarchy.home,
      this.documentHierarchy.contracts,
      this.documentHierarchy.commercial,
      this.documentHierarchy.masterService,
      this.documentHierarchy.currentDoc
    ],
    searchResults: [
      this.documentHierarchy.home,
      {
        id: 'search',
        label: 'Search Results',
        href: '/legal/search',
        icon: 'search',
        badge: '47 results'
      },
      {
        id: 'search-query',
        label: '"termination clause"',
        current: true,
        disabled: true
      }
    ],
    templates: [
      this.documentHierarchy.home,
      {
        id: 'templates',
        label: 'Document Templates',
        href: '/legal/templates',
        icon: 'template'
      },
      {
        id: 'contract-templates',
        label: 'Contract Templates',
        href: '/legal/templates/contracts',
        icon: 'file-plus'
      },
      {
        id: 'template-category',
        label: 'Employment Agreements',
        href: '/legal/templates/contracts/employment',
        current: true
      }
    ],
    workflow: [
      this.documentHierarchy.home,
      {
        id: 'workflows',
        label: 'Document Workflows',
        href: '/legal/workflows',
        icon: 'workflow'
      },
      {
        id: 'approval-workflow',
        label: 'Contract Approval Workflow',
        href: '/legal/workflows/contract-approval',
        icon: 'check-circle'
      },
      {
        id: 'current-step',
        label: 'Legal Review - Step 3 of 5',
        current: true,
        disabled: true,
        badge: '2 pending'
      }
    ]
  };

  complexNavigationItems: BreadcrumbItem[] = [
    {
      id: 'workspace',
      label: 'TR Legal Workspace',
      href: '/workspace',
      icon: 'building',
      tooltip: 'Thomson Reuters Legal Workspace'
    },
    {
      id: 'client',
      label: 'Global Corp Inc.',
      href: '/workspace/clients/global-corp',
      icon: 'users',
      badge: 'Premium'
    },
    {
      id: 'matter',
      label: 'M&A Transaction #2024-15',
      href: '/workspace/clients/global-corp/matters/ma-2024-15',
      icon: 'folder',
      badge: 'Active'
    },
    {
      id: 'documents',
      label: 'Transaction Documents',
      href: '/workspace/clients/global-corp/matters/ma-2024-15/documents',
      icon: 'files'
    },
    {
      id: 'due-diligence',
      label: 'Due Diligence Reports',
      href: '/workspace/clients/global-corp/matters/ma-2024-15/documents/due-diligence',
      current: true,
      badge: '12 files'
    }
  ];

  ngOnInit() {
    this.currentPath = this.navigationScenarios.document;
  }

  async handleBreadcrumbClick(item: BreadcrumbItem, index: number) {
    if (item.disabled || item.current) return;
    
    this.loading = true;
    console.log('Navigating to:', item.label, item.href);
    
    // Simulate navigation delay
    await new Promise(resolve => setTimeout(resolve, 500));
    
    // Update current path to reflect navigation
    const newPath = this.currentPath.slice(0, index + 1);
    this.currentPath = newPath;
    this.loading = false;
  }

  handleHomeClick() {
    console.log('Navigating to home');
    this.currentPath = [this.documentHierarchy.home];
  }

  switchScenario(scenarioKey: keyof typeof this.navigationScenarios) {
    this.currentPath = this.navigationScenarios[scenarioKey];
  }
}
```

### Research Navigation System

#### React
```jsx
import { SafBreadcrumbs, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const ResearchNavigationExample = () => {
  const [researchPath, setResearchPath] = useState([]);

  // Research database navigation structure
  const researchPaths = {
    caselaw: [
      {
        id: 'westlaw',
        label: 'Westlaw',
        href: '/research/westlaw',
        icon: 'database',
        badge: <SafBadge variant="primary" size="small">Premium</SafBadge>
      },
      {
        id: 'jurisdiction',
        label: 'Federal Courts',
        href: '/research/westlaw/federal',
        icon: 'building'
      },
      {
        id: 'court-level',
        label: 'Circuit Courts',
        href: '/research/westlaw/federal/circuit',
        icon: 'courthouse'
      },
      {
        id: 'circuit',
        label: '2nd Circuit',
        href: '/research/westlaw/federal/circuit/2nd',
        badge: '1,247 cases'
      },
      {
        id: 'search-results',
        label: 'Contract Interpretation',
        current: true,
        badge: '34 results',
        metadata: {
          query: '"contract interpretation" AND "good faith"',
          dateRange: '2020-2024',
          citationCount: '50+'
        }
      }
    ],
    practical: [
      {
        id: 'practical-law',
        label: 'Practical Law',
        href: '/research/practical-law',
        icon: 'book',
        badge: <SafBadge variant="success" size="small">Current</SafBadge>
      },
      {
        id: 'practice-area',
        label: 'Corporate & Securities',
        href: '/research/practical-law/corporate',
        icon: 'briefcase'
      },
      {
        id: 'resource-type',
        label: 'Standard Documents',
        href: '/research/practical-law/corporate/documents',
        icon: 'file-text'
      },
      {
        id: 'document-category',
        label: 'M&A Documents',
        href: '/research/practical-law/corporate/documents/ma',
        badge: '156 documents'
      },
      {
        id: 'specific-doc',
        label: 'Asset Purchase Agreement',
        current: true,
        icon: 'file-check',
        metadata: {
          jurisdiction: 'Delaware',
          lastUpdated: '2024-01-10',
          complexity: 'Advanced'
        }
      }
    ],
    news: [
      {
        id: 'reuters-news',
        label: 'Reuters Legal News',
        href: '/research/news',
        icon: 'newspaper',
        badge: 'Live'
      },
      {
        id: 'topic',
        label: 'Financial Services',
        href: '/research/news/financial-services',
        icon: 'trending-up'
      },
      {
        id: 'subtopic',
        label: 'Banking Regulation',
        href: '/research/news/financial-services/banking',
        badge: '23 articles today'
      },
      {
        id: 'article',
        label: 'Fed Announces New Capital Requirements',
        current: true,
        metadata: {
          publishDate: '2024-01-15',
          author: 'Reuters Staff',
          readTime: '4 min'
        }
      }
    ]
  };

  const handlePathSwitch = (pathKey) => {
    setResearchPath(researchPaths[pathKey]);
  };

  const handleBreadcrumbNavigation = (item, index) => {
    if (item.current || item.disabled) return;
    
    console.log('Navigating to research item:', item.label);
    // Update path based on navigation
    const newPath = researchPath.slice(0, index + 1);
    setResearchPath(newPath);
  };

  return (
    <div className="research-navigation-demo">
      <h2>Legal Research Navigation</h2>

      {/* Research Source Switcher */}
      <div className="research-sources">
        <h3>Research Sources</h3>
        <div className="source-buttons">
          <button onClick={() => handlePathSwitch('caselaw')}>
            <SafIcon name="scale" /> Case Law Research
          </button>
          <button onClick={() => handlePathSwitch('practical')}>
            <SafIcon name="book" /> Practical Law
          </button>
          <button onClick={() => handlePathSwitch('news')}>
            <SafIcon name="newspaper" /> Legal News
          </button>
        </div>
      </div>

      {/* Research Breadcrumbs */}
      <div className="research-breadcrumbs">
        <h3>Current Research Path</h3>
        
        {researchPath.length > 0 && (
          <SafBreadcrumbs
            items={researchPath}
            variant="default"
            separator={<SafIcon name="chevron-right" size="small" />}
            showHome={false}
            showIcons={true}
            showTooltips={true}
            maxWidth="800px"
            truncate="middle"
            onItemClick={handleBreadcrumbNavigation}
          />
        )}
      </div>

      {/* Different Research Navigation Styles */}
      <div className="navigation-styles">
        <h3>Navigation Styles for Different Research Types</h3>

        {/* Compact for Mobile Research */}
        <div className="style-section">
          <h4>Mobile Research Navigation</h4>
          <SafBreadcrumbs
            items={researchPath}
            variant="minimal"
            size="small"
            maxItems={2}
            collapsible={true}
            collapseFrom="start"
            showIcons={false}
            truncate="end"
            onItemClick={handleBreadcrumbNavigation}
          />
        </div>

        {/* Detailed for Desktop Research */}
        <div className="style-section">
          <h4>Desktop Research Navigation</h4>
          <SafBreadcrumbs
            items={researchPath}
            variant="rounded"
            size="medium"
            showIcons={true}
            showTooltips={true}
            maxItems={5}
            separator={<SafIcon name="arrow-right" size="small" />}
            onItemClick={handleBreadcrumbNavigation}
          />
        </div>

        {/* Citation-Style Navigation */}
        <div className="style-section">
          <h4>Citation-Style Navigation</h4>
          <SafBreadcrumbs
            items={researchPath}
            variant="underlined"
            separator=" › "
            showIcons={false}
            truncate={false}
            interactive={true}
            onItemClick={handleBreadcrumbNavigation}
          />
        </div>
      </div>

      {/* Complex Multi-Database Search */}
      <div className="multi-database-search">
        <h3>Cross-Database Research Navigation</h3>
        
        <SafBreadcrumbs
          items={[
            {
              id: 'search-home',
              label: 'Research Hub',
              href: '/research',
              icon: 'search',
              tooltip: 'All Research Databases'
            },
            {
              id: 'search-query',
              label: 'Global Search',
              href: '/research/search',
              icon: 'globe',
              badge: 'Cross-Database'
            },
            {
              id: 'search-term',
              label: '"artificial intelligence patents"',
              badge: '2,341 results',
              tooltip: 'Search across all databases'
            },
            {
              id: 'filtered-results',
              label: 'Westlaw Results',
              href: '/research/search/westlaw',
              badge: '847 results',
              icon: 'filter'
            },
            {
              id: 'current-result',
              label: 'Patent Application #US20240001234',
              current: true,
              icon: 'file',
              metadata: {
                database: 'Westlaw',
                relevance: '98%',
                citeCount: '15'
              }
            }
          ]}
          variant="default"
          showIcons={true}
          showTooltips={true}
          collapsible={true}
          maxItems={4}
          separator={<SafIcon name="chevron-right" size="small" />}
          onItemClick={handleBreadcrumbNavigation}
        />
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// research-navigation.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-research-navigation',
  template: `
    <div class="research-navigation-demo">
      <h2>Legal Research Navigation</h2>

      <!-- Research Source Switcher -->
      <div class="research-sources">
        <h3>Research Sources</h3>
        <div class="source-buttons">
          <button (click)="handlePathSwitch('caselaw')">
            <saf-icon name="scale"></saf-icon> Case Law Research
          </button>
          <button (click)="handlePathSwitch('practical')">
            <saf-icon name="book"></saf-icon> Practical Law
          </button>
          <button (click)="handlePathSwitch('news')">
            <saf-icon name="newspaper"></saf-icon> Legal News
          </button>
        </div>
      </div>

      <!-- Research Breadcrumbs -->
      <div class="research-breadcrumbs">
        <h3>Current Research Path</h3>
        
        <saf-breadcrumbs
          *ngIf="researchPath.length > 0"
          [items]="researchPath"
          variant="default"
          [showHome]="false"
          [showIcons]="true"
          [showTooltips]="true"
          maxWidth="800px"
          truncate="middle"
          (itemClick)="handleBreadcrumbNavigation($event.item, $event.index)">
          <saf-icon name="chevron-right" size="small" slot="separator"></saf-icon>
        </saf-breadcrumbs>
      </div>

      <!-- Different Research Navigation Styles -->
      <div class="navigation-styles">
        <h3>Navigation Styles for Different Research Types</h3>

        <!-- Compact for Mobile Research -->
        <div class="style-section">
          <h4>Mobile Research Navigation</h4>
          <saf-breadcrumbs
            [items]="researchPath"
            variant="minimal"
            size="small"
            [maxItems]="2"
            [collapsible]="true"
            collapseFrom="start"
            [showIcons]="false"
            truncate="end"
            (itemClick)="handleBreadcrumbNavigation($event.item, $event.index)">
          </saf-breadcrumbs>
        </div>

        <!-- Detailed for Desktop Research -->
        <div class="style-section">
          <h4>Desktop Research Navigation</h4>
          <saf-breadcrumbs
            [items]="researchPath"
            variant="rounded"
            size="medium"
            [showIcons]="true"
            [showTooltips]="true"
            [maxItems]="5"
            (itemClick)="handleBreadcrumbNavigation($event.item, $event.index)">
            <saf-icon name="arrow-right" size="small" slot="separator"></saf-icon>
          </saf-breadcrumbs>
        </div>

        <!-- Citation-Style Navigation -->
        <div class="style-section">
          <h4>Citation-Style Navigation</h4>
          <saf-breadcrumbs
            [items]="researchPath"
            variant="underlined"
            separator=" › "
            [showIcons]="false"
            [truncate]="false"
            [interactive]="true"
            (itemClick)="handleBreadcrumbNavigation($event.item, $event.index)">
          </saf-breadcrumbs>
        </div>
      </div>

      <!-- Complex Multi-Database Search -->
      <div class="multi-database-search">
        <h3>Cross-Database Research Navigation</h3>
        
        <saf-breadcrumbs
          [items]="multiDatabasePath"
          variant="default"
          [showIcons]="true"
          [showTooltips]="true"
          [collapsible]="true"
          [maxItems]="4"
          (itemClick)="handleBreadcrumbNavigation($event.item, $event.index)">
          <saf-icon name="chevron-right" size="small" slot="separator"></saf-icon>
        </saf-breadcrumbs>
      </div>
    </div>
  `
})
export class ResearchNavigationComponent {
  researchPath: BreadcrumbItem[] = [];

  researchPaths = {
    caselaw: [
      {
        id: 'westlaw',
        label: 'Westlaw',
        href: '/research/westlaw',
        icon: 'database',
        badge: 'Premium'
      },
      {
        id: 'jurisdiction',
        label: 'Federal Courts',
        href: '/research/westlaw/federal',
        icon: 'building'
      },
      {
        id: 'court-level',
        label: 'Circuit Courts',
        href: '/research/westlaw/federal/circuit',
        icon: 'courthouse'
      },
      {
        id: 'circuit',
        label: '2nd Circuit',
        href: '/research/westlaw/federal/circuit/2nd',
        badge: '1,247 cases'
      },
      {
        id: 'search-results',
        label: 'Contract Interpretation',
        current: true,
        badge: '34 results'
      }
    ],
    practical: [
      {
        id: 'practical-law',
        label: 'Practical Law',
        href: '/research/practical-law',
        icon: 'book',
        badge: 'Current'
      },
      {
        id: 'practice-area',
        label: 'Corporate & Securities',
        href: '/research/practical-law/corporate',
        icon: 'briefcase'
      },
      {
        id: 'resource-type',
        label: 'Standard Documents',
        href: '/research/practical-law/corporate/documents',
        icon: 'file-text'
      },
      {
        id: 'document-category',
        label: 'M&A Documents',
        href: '/research/practical-law/corporate/documents/ma',
        badge: '156 documents'
      },
      {
        id: 'specific-doc',
        label: 'Asset Purchase Agreement',
        current: true,
        icon: 'file-check'
      }
    ],
    news: [
      {
        id: 'reuters-news',
        label: 'Reuters Legal News',
        href: '/research/news',
        icon: 'newspaper',
        badge: 'Live'
      },
      {
        id: 'topic',
        label: 'Financial Services',
        href: '/research/news/financial-services',
        icon: 'trending-up'
      },
      {
        id: 'subtopic',
        label: 'Banking Regulation',
        href: '/research/news/financial-services/banking',
        badge: '23 articles today'
      },
      {
        id: 'article',
        label: 'Fed Announces New Capital Requirements',
        current: true
      }
    ]
  };

  multiDatabasePath: BreadcrumbItem[] = [
    {
      id: 'search-home',
      label: 'Research Hub',
      href: '/research',
      icon: 'search',
      tooltip: 'All Research Databases'
    },
    {
      id: 'search-query',
      label: 'Global Search',
      href: '/research/search',
      icon: 'globe',
      badge: 'Cross-Database'
    },
    {
      id: 'search-term',
      label: '"artificial intelligence patents"',
      badge: '2,341 results',
      tooltip: 'Search across all databases'
    },
    {
      id: 'filtered-results',
      label: 'Westlaw Results',
      href: '/research/search/westlaw',
      badge: '847 results',
      icon: 'filter'
    },
    {
      id: 'current-result',
      label: 'Patent Application #US20240001234',
      current: true,
      icon: 'file'
    }
  ];

  handlePathSwitch(pathKey: keyof typeof this.researchPaths) {
    this.researchPath = this.researchPaths[pathKey];
  }

  handleBreadcrumbNavigation(item: BreadcrumbItem, index: number) {
    if (item.current || item.disabled) return;
    
    console.log('Navigating to research item:', item.label);
    // Update path based on navigation
    const newPath = this.researchPath.slice(0, index + 1);
    this.researchPath = newPath;
  }
}
```

## Best Practices

1. **Navigation Clarity**
   - Use clear, descriptive labels for breadcrumb items
   - Maintain consistent hierarchy levels
   - Provide visual cues for current location

2. **Responsive Design**
   - Implement collapsible behavior for mobile devices
   - Use appropriate truncation strategies
   - Consider touch-friendly sizing

3. **Performance Optimization**
   - Lazy load breadcrumb data when needed
   - Cache navigation states efficiently
   - Minimize re-renders during navigation

4. **User Experience**
   - Provide tooltips for truncated items
   - Show loading states during navigation
   - Enable keyboard navigation support

5. **Content Strategy**
   - Use meaningful separators that fit your brand
   - Consider icons for better visual hierarchy
   - Balance detail with usability

## Accessibility Considerations

1. **Screen Reader Support**
   - Use proper navigation landmarks
   - Provide clear breadcrumb descriptions
   - Announce current location changes

2. **Keyboard Navigation**
   - Support Tab navigation through breadcrumbs
   - Implement Enter and Space activation
   - Provide keyboard shortcuts where appropriate

3. **Visual Accessibility**
   - Ensure sufficient color contrast for all states
   - Use multiple indicators for current location
   - Support high contrast and reduced motion

4. **Semantic Structure**
   - Use appropriate HTML elements (nav, ol, li)
   - Implement ARIA breadcrumb patterns
   - Provide context for screen readers

## Related Components

- **SafIcon**: Icons for breadcrumb items and separators
- **SafBadge**: Status and count indicators
- **SafTooltip**: Additional context for collapsed items
- **SafButton**: Clickable breadcrumb items
- **SafDropdown**: Dropdown menus for breadcrumb sub-items

## Notes

- Breadcrumbs automatically handle URL routing when href properties are provided
- Component supports both controlled and uncontrolled usage patterns
- Built-in responsive behavior adapts to different screen sizes
- Customizable separators and icons for brand consistency
- Efficient rendering with virtualization for large breadcrumb lists
- Comprehensive keyboard and screen reader accessibility support
