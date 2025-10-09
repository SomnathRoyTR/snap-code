# SafChip Component

## Overview

SafChip is a versatile component for displaying tags, filters, and selectable items in a compact, pill-shaped format. It supports various interaction modes including removable chips, selectable states, category grouping, and custom styling. The component is ideal for tag management, filter interfaces, category selection, skill badges, and any scenario requiring compact, interactive labels with clear visual hierarchy.

## React API

### SafChip

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `label` | `string \| ReactNode` | Yes | - | Text or content to display in the chip |
| `variant` | `'default' \| 'outlined' \| 'filled' \| 'soft'` | No | `'default'` | Visual style variant |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'danger' \| 'info' \| 'neutral'` | No | `'neutral'` | Color theme for the chip |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant |
| `icon` | `string \| ReactNode` | No | - | Icon to display in the chip |
| `iconPosition` | `'start' \| 'end'` | No | `'start'` | Position of the icon |
| `avatar` | `string \| ReactNode` | No | - | Avatar image or component |
| `removable` | `boolean` | No | `false` | Whether chip can be removed |
| `removeIcon` | `string \| ReactNode` | No | `'x'` | Icon for remove button |
| `selectable` | `boolean` | No | `false` | Whether chip can be selected |
| `selected` | `boolean` | No | `false` | Whether chip is currently selected |
| `disabled` | `boolean` | No | `false` | Whether chip is disabled |
| `clickable` | `boolean` | No | `false` | Whether chip is clickable |
| `rounded` | `boolean` | No | `true` | Whether chip has rounded corners |
| `maxWidth` | `string \| number` | No | - | Maximum width with text truncation |
| `tooltip` | `string \| ReactNode` | No | - | Tooltip text for the chip |
| `badge` | `string \| number \| ReactNode` | No | - | Badge or count to display |
| `href` | `string` | No | - | URL for link chips |
| `target` | `string` | No | - | Target for link chips |
| `value` | `any` | No | - | Value associated with the chip |
| `category` | `string` | No | - | Category for grouping chips |
| `priority` | `'low' \| 'medium' \| 'high'` | No | - | Priority level indicator |
| `status` | `'active' \| 'inactive' \| 'pending' \| 'completed'` | No | - | Status indicator |
| `onClick` | `(chip: ChipData) => void` | No | - | Callback when chip is clicked |
| `onRemove` | `(chip: ChipData) => void` | No | - | Callback when chip is removed |
| `onSelect` | `(chip: ChipData, selected: boolean) => void` | No | - | Callback when chip selection changes |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### SafChipGroup

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `chips` | `ChipData[]` | Yes | - | Array of chip data objects |
| `variant` | `'default' \| 'outlined' \| 'filled' \| 'soft'` | No | `'default'` | Default variant for all chips |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'danger' \| 'info' \| 'neutral'` | No | `'neutral'` | Default color for all chips |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Default size for all chips |
| `layout` | `'horizontal' \| 'vertical' \| 'wrap'` | No | `'wrap'` | Layout arrangement |
| `spacing` | `'none' \| 'small' \| 'medium' \| 'large'` | No | `'medium'` | Spacing between chips |
| `groupBy` | `'category' \| 'priority' \| 'status' \| 'none'` | No | `'none'` | How to group chips |
| `showGroupLabels` | `boolean` | No | `false` | Whether to show group labels |
| `maxItems` | `number` | No | - | Maximum number of chips to display |
| `collapsible` | `boolean` | No | `false` | Enable collapsing excess chips |
| `searchable` | `boolean` | No | `false` | Enable chip search functionality |
| `sortable` | `boolean` | No | `false` | Enable drag-and-drop sorting |
| `multiSelect` | `boolean` | No | `false` | Allow multiple chip selection |
| `clearAll` | `boolean` | No | `false` | Show clear all button |
| `onChipClick` | `(chip: ChipData) => void` | No | - | Callback when any chip is clicked |
| `onChipRemove` | `(chip: ChipData) => void` | No | - | Callback when any chip is removed |
| `onChipSelect` | `(chip: ChipData, selected: boolean) => void` | No | - | Callback when any chip is selected |
| `onClearAll` | `() => void` | No | - | Callback when clear all is clicked |
| `onReorder` | `(newOrder: ChipData[]) => void` | No | - | Callback when chips are reordered |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### ChipData Interface

```typescript
interface ChipData {
  id: string;
  label: string | ReactNode;
  variant?: 'default' | 'outlined' | 'filled' | 'soft';
  color?: 'primary' | 'secondary' | 'success' | 'warning' | 'danger' | 'info' | 'neutral';
  size?: 'small' | 'medium' | 'large';
  icon?: string | ReactNode;
  iconPosition?: 'start' | 'end';
  avatar?: string | ReactNode;
  removable?: boolean;
  removeIcon?: string | ReactNode;
  selectable?: boolean;
  selected?: boolean;
  disabled?: boolean;
  clickable?: boolean;
  rounded?: boolean;
  maxWidth?: string | number;
  tooltip?: string | ReactNode;
  badge?: string | number | ReactNode;
  href?: string;
  target?: string;
  value?: any;
  category?: string;
  priority?: 'low' | 'medium' | 'high';
  status?: 'active' | 'inactive' | 'pending' | 'completed';
  metadata?: { [key: string]: any };
}
```

## Angular API

### saf-chip

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[label]` | `string \| TemplateRef` | Yes | - | Text or content to display in the chip |
| `[variant]` | `'default' \| 'outlined' \| 'filled' \| 'soft'` | No | `'default'` | Visual style variant |
| `[color]` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'danger' \| 'info' \| 'neutral'` | No | `'neutral'` | Color theme for the chip |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant |
| `[icon]` | `string \| TemplateRef` | No | - | Icon to display in the chip |
| `[iconPosition]` | `'start' \| 'end'` | No | `'start'` | Position of the icon |
| `[avatar]` | `string \| TemplateRef` | No | - | Avatar image or component |
| `[removable]` | `boolean` | No | `false` | Whether chip can be removed |
| `[removeIcon]` | `string \| TemplateRef` | No | `'x'` | Icon for remove button |
| `[selectable]` | `boolean` | No | `false` | Whether chip can be selected |
| `[selected]` | `boolean` | No | `false` | Whether chip is currently selected |
| `[disabled]` | `boolean` | No | `false` | Whether chip is disabled |
| `[clickable]` | `boolean` | No | `false` | Whether chip is clickable |
| `[rounded]` | `boolean` | No | `true` | Whether chip has rounded corners |
| `[maxWidth]` | `string \| number` | No | - | Maximum width with text truncation |
| `[tooltip]` | `string \| TemplateRef` | No | - | Tooltip text for the chip |
| `[badge]` | `string \| number \| TemplateRef` | No | - | Badge or count to display |
| `[href]` | `string` | No | - | URL for link chips |
| `[target]` | `string` | No | - | Target for link chips |
| `[value]` | `any` | No | - | Value associated with the chip |
| `[category]` | `string` | No | - | Category for grouping chips |
| `[priority]` | `'low' \| 'medium' \| 'high'` | No | - | Priority level indicator |
| `[status]` | `'active' \| 'inactive' \| 'pending' \| 'completed'` | No | - | Status indicator |
| `(click)` | `EventEmitter<ChipData>` | No | - | Event when chip is clicked |
| `(remove)` | `EventEmitter<ChipData>` | No | - | Event when chip is removed |
| `(select)` | `EventEmitter<{chip: ChipData, selected: boolean}>` | No | - | Event when chip selection changes |

### saf-chip-group

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[chips]` | `ChipData[]` | Yes | - | Array of chip data objects |
| `[variant]` | `'default' \| 'outlined' \| 'filled' \| 'soft'` | No | `'default'` | Default variant for all chips |
| `[color]` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'danger' \| 'info' \| 'neutral'` | No | `'neutral'` | Default color for all chips |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Default size for all chips |
| `[layout]` | `'horizontal' \| 'vertical' \| 'wrap'` | No | `'wrap'` | Layout arrangement |
| `[spacing]` | `'none' \| 'small' \| 'medium' \| 'large'` | No | `'medium'` | Spacing between chips |
| `[groupBy]` | `'category' \| 'priority' \| 'status' \| 'none'` | No | `'none'` | How to group chips |
| `[showGroupLabels]` | `boolean` | No | `false` | Whether to show group labels |
| `[maxItems]` | `number` | No | - | Maximum number of chips to display |
| `[collapsible]` | `boolean` | No | `false` | Enable collapsing excess chips |
| `[searchable]` | `boolean` | No | `false` | Enable chip search functionality |
| `[sortable]` | `boolean` | No | `false` | Enable drag-and-drop sorting |
| `[multiSelect]` | `boolean` | No | `false` | Allow multiple chip selection |
| `[clearAll]` | `boolean` | No | `false` | Show clear all button |
| `(chipClick)` | `EventEmitter<ChipData>` | No | - | Event when any chip is clicked |
| `(chipRemove)` | `EventEmitter<ChipData>` | No | - | Event when any chip is removed |
| `(chipSelect)` | `EventEmitter<{chip: ChipData, selected: boolean}>` | No | - | Event when any chip is selected |
| `(clearAll)` | `EventEmitter<void>` | No | - | Event when clear all is clicked |
| `(reorder)` | `EventEmitter<ChipData[]>` | No | - | Event when chips are reordered |

## Usage Examples

### Legal Practice Area Tags

#### React
```jsx
import { SafChip, SafChipGroup, SafIcon, SafAvatar } from '@saffron/react';
import { useState } from 'react';

const LegalPracticeAreaChips = () => {
  const [selectedAreas, setSelectedAreas] = useState([]);
  const [documentTags, setDocumentTags] = useState([]);
  const [expertiseTags, setExpertiseTags] = useState([]);

  // Practice area chips for legal specializations
  const practiceAreas = [
    {
      id: 'corporate',
      label: 'Corporate Law',
      color: 'primary',
      icon: 'building',
      category: 'Business',
      selectable: true,
      value: 'corporate-law'
    },
    {
      id: 'litigation',
      label: 'Litigation',
      color: 'danger',
      icon: 'gavel',
      category: 'Dispute Resolution',
      selectable: true,
      value: 'litigation'
    },
    {
      id: 'ip',
      label: 'Intellectual Property',
      color: 'info',
      icon: 'lightbulb',
      category: 'Technology',
      selectable: true,
      value: 'intellectual-property'
    },
    {
      id: 'employment',
      label: 'Employment Law',
      color: 'warning',
      icon: 'users',
      category: 'Human Resources',
      selectable: true,
      value: 'employment-law'
    },
    {
      id: 'real-estate',
      label: 'Real Estate',
      color: 'success',
      icon: 'home',
      category: 'Property',
      selectable: true,
      value: 'real-estate'
    },
    {
      id: 'tax',
      label: 'Tax Law',
      color: 'secondary',
      icon: 'calculator',
      category: 'Financial',
      selectable: true,
      value: 'tax-law'
    },
    {
      id: 'mergers',
      label: 'M&A',
      color: 'primary',
      icon: 'trending-up',
      category: 'Business',
      selectable: true,
      value: 'mergers-acquisitions',
      badge: 'Hot'
    },
    {
      id: 'compliance',
      label: 'Regulatory Compliance',
      color: 'neutral',
      icon: 'shield-check',
      category: 'Regulatory',
      selectable: true,
      value: 'compliance'
    }
  ];

  // Document classification tags
  const documentClassificationTags = [
    {
      id: 'contract',
      label: 'Contract',
      variant: 'filled',
      color: 'primary',
      removable: true,
      icon: 'file-text'
    },
    {
      id: 'confidential',
      label: 'Confidential',
      variant: 'filled',
      color: 'danger',
      removable: true,
      icon: 'lock',
      priority: 'high'
    },
    {
      id: 'draft',
      label: 'Draft',
      variant: 'outlined',
      color: 'warning',
      removable: true,
      icon: 'edit'
    },
    {
      id: 'reviewed',
      label: 'Legal Review Complete',
      variant: 'filled',
      color: 'success',
      removable: true,
      icon: 'check-circle',
      status: 'completed'
    },
    {
      id: 'urgent',
      label: 'Urgent',
      variant: 'filled',
      color: 'danger',
      removable: true,
      icon: 'alert-triangle',
      priority: 'high',
      badge: '!'
    },
    {
      id: 'template',
      label: 'Template',
      variant: 'soft',
      color: 'info',
      removable: true,
      icon: 'copy'
    }
  ];

  // Legal expertise and skill tags
  const expertiseSkillTags = [
    {
      id: 'expert-corporate',
      label: 'Corporate Law Expert',
      variant: 'filled',
      color: 'primary',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=expert1',
      removable: true,
      badge: '15 years'
    },
    {
      id: 'specialist-ip',
      label: 'IP Specialist',
      variant: 'filled',
      color: 'info',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=expert2',
      removable: true,
      badge: 'Certified'
    },
    {
      id: 'junior-associate',
      label: 'Junior Associate',
      variant: 'outlined',
      color: 'secondary',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=junior',
      removable: true,
      badge: '2 years'
    },
    {
      id: 'partner',
      label: 'Senior Partner',
      variant: 'filled',
      color: 'success',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=partner',
      removable: true,
      badge: 'Partner',
      priority: 'high'
    }
  ];

  useState(() => {
    setDocumentTags(documentClassificationTags);
    setExpertiseTags(expertiseSkillTags);
  }, []);

  const handlePracticeAreaSelect = (chip, selected) => {
    if (selected) {
      setSelectedAreas(prev => [...prev, chip.id]);
    } else {
      setSelectedAreas(prev => prev.filter(id => id !== chip.id));
    }
    console.log('Practice area selection:', chip.label, selected);
  };

  const handleDocumentTagRemove = (chip) => {
    setDocumentTags(prev => prev.filter(tag => tag.id !== chip.id));
    console.log('Document tag removed:', chip.label);
  };

  const handleExpertiseTagRemove = (chip) => {
    setExpertiseTags(prev => prev.filter(tag => tag.id !== chip.id));
    console.log('Expertise tag removed:', chip.label);
  };

  const handleAddDocumentTag = (newTag) => {
    const tag = {
      id: `tag-${Date.now()}`,
      label: newTag,
      variant: 'outlined',
      color: 'neutral',
      removable: true,
      icon: 'tag'
    };
    setDocumentTags(prev => [...prev, tag]);
  };

  const handleClearAllAreas = () => {
    setSelectedAreas([]);
    console.log('All practice areas cleared');
  };

  return (
    <div className="legal-practice-area-chips-demo">
      <h2>Legal Practice Area Management</h2>

      {/* Practice Area Selection */}
      <div className="chip-section">
        <h3>Practice Area Specializations</h3>
        <p>Select your areas of legal expertise:</p>
        
        <SafChipGroup
          chips={practiceAreas.map(area => ({
            ...area,
            selected: selectedAreas.includes(area.id)
          }))}
          layout="wrap"
          spacing="medium"
          groupBy="category"
          showGroupLabels={true}
          multiSelect={true}
          clearAll={true}
          onChipSelect={handlePracticeAreaSelect}
          onClearAll={handleClearAllAreas}
        />

        <div className="selection-summary">
          <h4>Selected Areas ({selectedAreas.length}):</h4>
          {selectedAreas.length > 0 ? (
            <div className="selected-chips">
              {practiceAreas
                .filter(area => selectedAreas.includes(area.id))
                .map(area => (
                  <SafChip
                    key={area.id}
                    label={area.label}
                    variant="filled"
                    color={area.color}
                    icon={area.icon}
                    size="small"
                    removable={true}
                    onRemove={() => {
                      setSelectedAreas(prev => prev.filter(id => id !== area.id));
                    }}
                  />
                ))
              }
            </div>
          ) : (
            <p>No practice areas selected</p>
          )}
        </div>
      </div>

      {/* Document Classification Tags */}
      <div className="chip-section">
        <h3>Document Classification Tags</h3>
        <p>Tags for legal document management:</p>
        
        <SafChipGroup
          chips={documentTags}
          layout="wrap"
          spacing="small"
          groupBy="priority"
          showGroupLabels={false}
          onChipRemove={handleDocumentTagRemove}
          onChipClick={(chip) => console.log('Document tag clicked:', chip.label)}
        />

        <div className="tag-input-demo">
          <h4>Add Custom Document Tag:</h4>
          <input
            type="text"
            placeholder="Enter tag name"
            onKeyPress={(e) => {
              if (e.key === 'Enter' && e.target.value.trim()) {
                handleAddDocumentTag(e.target.value.trim());
                e.target.value = '';
              }
            }}
          />
          <p><small>Press Enter to add tag</small></p>
        </div>
      </div>

      {/* Legal Team Expertise Tags */}
      <div className="chip-section">
        <h3>Legal Team Expertise</h3>
        <p>Team member skills and experience levels:</p>
        
        <SafChipGroup
          chips={expertiseTags}
          layout="wrap"
          spacing="medium"
          groupBy="none"
          onChipRemove={handleExpertiseTagRemove}
          onChipClick={(chip) => console.log('Expertise tag clicked:', chip.label)}
        />
      </div>

      {/* Different Chip Variants Showcase */}
      <div className="chip-section">
        <h3>Legal Status Indicators</h3>
        
        <div className="variant-showcase">
          <div className="variant-group">
            <h4>Case Status</h4>
            <SafChip label="Active Case" variant="filled" color="success" icon="play" />
            <SafChip label="Pending Review" variant="filled" color="warning" icon="clock" />
            <SafChip label="Closed" variant="outlined" color="neutral" icon="check" />
            <SafChip label="On Hold" variant="soft" color="secondary" icon="pause" />
          </div>

          <div className="variant-group">
            <h4>Priority Levels</h4>
            <SafChip 
              label="Critical" 
              variant="filled" 
              color="danger" 
              icon="alert-triangle"
              badge="!"
              priority="high"
            />
            <SafChip 
              label="High Priority" 
              variant="filled" 
              color="warning" 
              icon="arrow-up"
              priority="high"
            />
            <SafChip 
              label="Normal" 
              variant="outlined" 
              color="neutral" 
              icon="minus"
              priority="medium"
            />
            <SafChip 
              label="Low Priority" 
              variant="soft" 
              color="info" 
              icon="arrow-down"
              priority="low"
            />
          </div>

          <div className="variant-group">
            <h4>Document Types</h4>
            <SafChip 
              label="Contract" 
              variant="filled" 
              color="primary" 
              icon="file-text"
              clickable={true}
              href="/contracts"
            />
            <SafChip 
              label="Legal Brief" 
              variant="filled" 
              color="info" 
              icon="file"
              clickable={true}
              href="/briefs"
            />
            <SafChip 
              label="Motion" 
              variant="outlined" 
              color="secondary" 
              icon="file-plus"
              clickable={true}
              href="/motions"
            />
            <SafChip 
              label="Discovery" 
              variant="soft" 
              color="neutral" 
              icon="search"
              clickable={true}
              href="/discovery"
            />
          </div>
        </div>
      </div>

      {/* Interactive Features Demo */}
      <div className="chip-section">
        <h3>Interactive Features</h3>
        
        <div className="interactive-demo">
          <div className="feature-demo">
            <h4>Sortable Legal Categories</h4>
            <SafChipGroup
              chips={[
                { id: 'cat1', label: 'Corporate', icon: 'building', removable: true },
                { id: 'cat2', label: 'Litigation', icon: 'gavel', removable: true },
                { id: 'cat3', label: 'IP Law', icon: 'lightbulb', removable: true },
                { id: 'cat4', label: 'Employment', icon: 'users', removable: true }
              ]}
              sortable={true}
              layout="horizontal"
              spacing="medium"
              onReorder={(newOrder) => console.log('New order:', newOrder)}
              onChipRemove={(chip) => console.log('Removed:', chip.label)}
            />
          </div>

          <div className="feature-demo">
            <h4>Searchable Legal Terms</h4>
            <SafChipGroup
              chips={[
                { id: 'term1', label: 'Due Diligence', selectable: true },
                { id: 'term2', label: 'Force Majeure', selectable: true },
                { id: 'term3', label: 'Indemnification', selectable: true },
                { id: 'term4', label: 'Liquidated Damages', selectable: true },
                { id: 'term5', label: 'Breach of Contract', selectable: true },
                { id: 'term6', label: 'Intellectual Property', selectable: true }
              ]}
              searchable={true}
              multiSelect={true}
              layout="wrap"
              maxItems={4}
              collapsible={true}
              onChipSelect={(chip, selected) => 
                console.log('Term selection:', chip.label, selected)
              }
            />
          </div>
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-practice-area-chips.component.ts
import { Component, OnInit } from '@angular/core';

interface ChipData {
  id: string;
  label: string;
  color?: string;
  variant?: string;
  icon?: string;
  category?: string;
  selectable?: boolean;
  selected?: boolean;
  removable?: boolean;
  value?: any;
  badge?: string;
  priority?: string;
  status?: string;
  avatar?: string;
  clickable?: boolean;
  href?: string;
}

@Component({
  selector: 'app-legal-practice-area-chips',
  template: `
    <div class="legal-practice-area-chips-demo">
      <h2>Legal Practice Area Management</h2>

      <!-- Practice Area Selection -->
      <div class="chip-section">
        <h3>Practice Area Specializations</h3>
        <p>Select your areas of legal expertise:</p>
        
        <saf-chip-group
          [chips]="practiceAreasWithSelection"
          layout="wrap"
          spacing="medium"
          groupBy="category"
          [showGroupLabels]="true"
          [multiSelect]="true"
          [clearAll]="true"
          (chipSelect)="handlePracticeAreaSelect($event.chip, $event.selected)"
          (clearAll)="handleClearAllAreas()">
        </saf-chip-group>

        <div class="selection-summary">
          <h4>Selected Areas ({{ selectedAreas.length }}):</h4>
          <div *ngIf="selectedAreas.length > 0; else noSelection" class="selected-chips">
            <saf-chip
              *ngFor="let area of getSelectedPracticeAreas()"
              [label]="area.label"
              variant="filled"
              [color]="area.color"
              [icon]="area.icon"
              size="small"
              [removable]="true"
              (remove)="removeSelectedArea(area.id)">
            </saf-chip>
          </div>
          <ng-template #noSelection>
            <p>No practice areas selected</p>
          </ng-template>
        </div>
      </div>

      <!-- Document Classification Tags -->
      <div class="chip-section">
        <h3>Document Classification Tags</h3>
        <p>Tags for legal document management:</p>
        
        <saf-chip-group
          [chips]="documentTags"
          layout="wrap"
          spacing="small"
          groupBy="priority"
          [showGroupLabels]="false"
          (chipRemove)="handleDocumentTagRemove($event)"
          (chipClick)="handleDocumentTagClick($event)">
        </saf-chip-group>

        <div class="tag-input-demo">
          <h4>Add Custom Document Tag:</h4>
          <input
            type="text"
            placeholder="Enter tag name"
            (keypress)="handleTagInput($event)">
          <p><small>Press Enter to add tag</small></p>
        </div>
      </div>

      <!-- Legal Team Expertise Tags -->
      <div class="chip-section">
        <h3>Legal Team Expertise</h3>
        <p>Team member skills and experience levels:</p>
        
        <saf-chip-group
          [chips]="expertiseTags"
          layout="wrap"
          spacing="medium"
          groupBy="none"
          (chipRemove)="handleExpertiseTagRemove($event)"
          (chipClick)="handleExpertiseTagClick($event)">
        </saf-chip-group>
      </div>

      <!-- Different Chip Variants Showcase -->
      <div class="chip-section">
        <h3>Legal Status Indicators</h3>
        
        <div class="variant-showcase">
          <div class="variant-group">
            <h4>Case Status</h4>
            <saf-chip label="Active Case" variant="filled" color="success" icon="play"></saf-chip>
            <saf-chip label="Pending Review" variant="filled" color="warning" icon="clock"></saf-chip>
            <saf-chip label="Closed" variant="outlined" color="neutral" icon="check"></saf-chip>
            <saf-chip label="On Hold" variant="soft" color="secondary" icon="pause"></saf-chip>
          </div>

          <div class="variant-group">
            <h4>Priority Levels</h4>
            <saf-chip 
              label="Critical" 
              variant="filled" 
              color="danger" 
              icon="alert-triangle"
              badge="!"
              priority="high">
            </saf-chip>
            <saf-chip 
              label="High Priority" 
              variant="filled" 
              color="warning" 
              icon="arrow-up"
              priority="high">
            </saf-chip>
            <saf-chip 
              label="Normal" 
              variant="outlined" 
              color="neutral" 
              icon="minus"
              priority="medium">
            </saf-chip>
            <saf-chip 
              label="Low Priority" 
              variant="soft" 
              color="info" 
              icon="arrow-down"
              priority="low">
            </saf-chip>
          </div>

          <div class="variant-group">
            <h4>Document Types</h4>
            <saf-chip 
              label="Contract" 
              variant="filled" 
              color="primary" 
              icon="file-text"
              [clickable]="true"
              href="/contracts">
            </saf-chip>
            <saf-chip 
              label="Legal Brief" 
              variant="filled" 
              color="info" 
              icon="file"
              [clickable]="true"
              href="/briefs">
            </saf-chip>
            <saf-chip 
              label="Motion" 
              variant="outlined" 
              color="secondary" 
              icon="file-plus"
              [clickable]="true"
              href="/motions">
            </saf-chip>
            <saf-chip 
              label="Discovery" 
              variant="soft" 
              color="neutral" 
              icon="search"
              [clickable]="true"
              href="/discovery">
            </saf-chip>
          </div>
        </div>
      </div>

      <!-- Interactive Features Demo -->
      <div class="chip-section">
        <h3>Interactive Features</h3>
        
        <div class="interactive-demo">
          <div class="feature-demo">
            <h4>Sortable Legal Categories</h4>
            <saf-chip-group
              [chips]="sortableCategories"
              [sortable]="true"
              layout="horizontal"
              spacing="medium"
              (reorder)="handleCategoryReorder($event)"
              (chipRemove)="handleCategoryRemove($event)">
            </saf-chip-group>
          </div>

          <div class="feature-demo">
            <h4>Searchable Legal Terms</h4>
            <saf-chip-group
              [chips]="legalTerms"
              [searchable]="true"
              [multiSelect]="true"
              layout="wrap"
              [maxItems]="4"
              [collapsible]="true"
              (chipSelect)="handleTermSelect($event.chip, $event.selected)">
            </saf-chip-group>
          </div>
        </div>
      </div>
    </div>
  `
})
export class LegalPracticeAreaChipsComponent implements OnInit {
  selectedAreas: string[] = [];
  documentTags: ChipData[] = [];
  expertiseTags: ChipData[] = [];

  practiceAreas: ChipData[] = [
    {
      id: 'corporate',
      label: 'Corporate Law',
      color: 'primary',
      icon: 'building',
      category: 'Business',
      selectable: true,
      value: 'corporate-law'
    },
    {
      id: 'litigation',
      label: 'Litigation',
      color: 'danger',
      icon: 'gavel',
      category: 'Dispute Resolution',
      selectable: true,
      value: 'litigation'
    },
    {
      id: 'ip',
      label: 'Intellectual Property',
      color: 'info',
      icon: 'lightbulb',
      category: 'Technology',
      selectable: true,
      value: 'intellectual-property'
    },
    {
      id: 'employment',
      label: 'Employment Law',
      color: 'warning',
      icon: 'users',
      category: 'Human Resources',
      selectable: true,
      value: 'employment-law'
    },
    {
      id: 'real-estate',
      label: 'Real Estate',
      color: 'success',
      icon: 'home',
      category: 'Property',
      selectable: true,
      value: 'real-estate'
    },
    {
      id: 'tax',
      label: 'Tax Law',
      color: 'secondary',
      icon: 'calculator',
      category: 'Financial',
      selectable: true,
      value: 'tax-law'
    },
    {
      id: 'mergers',
      label: 'M&A',
      color: 'primary',
      icon: 'trending-up',
      category: 'Business',
      selectable: true,
      value: 'mergers-acquisitions',
      badge: 'Hot'
    },
    {
      id: 'compliance',
      label: 'Regulatory Compliance',
      color: 'neutral',
      icon: 'shield-check',
      category: 'Regulatory',
      selectable: true,
      value: 'compliance'
    }
  ];

  sortableCategories: ChipData[] = [
    { id: 'cat1', label: 'Corporate', icon: 'building', removable: true },
    { id: 'cat2', label: 'Litigation', icon: 'gavel', removable: true },
    { id: 'cat3', label: 'IP Law', icon: 'lightbulb', removable: true },
    { id: 'cat4', label: 'Employment', icon: 'users', removable: true }
  ];

  legalTerms: ChipData[] = [
    { id: 'term1', label: 'Due Diligence', selectable: true },
    { id: 'term2', label: 'Force Majeure', selectable: true },
    { id: 'term3', label: 'Indemnification', selectable: true },
    { id: 'term4', label: 'Liquidated Damages', selectable: true },
    { id: 'term5', label: 'Breach of Contract', selectable: true },
    { id: 'term6', label: 'Intellectual Property', selectable: true }
  ];

  get practiceAreasWithSelection(): ChipData[] {
    return this.practiceAreas.map(area => ({
      ...area,
      selected: this.selectedAreas.includes(area.id)
    }));
  }

  ngOnInit() {
    this.loadDocumentTags();
    this.loadExpertiseTags();
  }

  loadDocumentTags() {
    this.documentTags = [
      {
        id: 'contract',
        label: 'Contract',
        variant: 'filled',
        color: 'primary',
        removable: true,
        icon: 'file-text'
      },
      {
        id: 'confidential',
        label: 'Confidential',
        variant: 'filled',
        color: 'danger',
        removable: true,
        icon: 'lock',
        priority: 'high'
      },
      {
        id: 'draft',
        label: 'Draft',
        variant: 'outlined',
        color: 'warning',
        removable: true,
        icon: 'edit'
      },
      {
        id: 'reviewed',
        label: 'Legal Review Complete',
        variant: 'filled',
        color: 'success',
        removable: true,
        icon: 'check-circle',
        status: 'completed'
      },
      {
        id: 'urgent',
        label: 'Urgent',
        variant: 'filled',
        color: 'danger',
        removable: true,
        icon: 'alert-triangle',
        priority: 'high',
        badge: '!'
      },
      {
        id: 'template',
        label: 'Template',
        variant: 'soft',
        color: 'info',
        removable: true,
        icon: 'copy'
      }
    ];
  }

  loadExpertiseTags() {
    this.expertiseTags = [
      {
        id: 'expert-corporate',
        label: 'Corporate Law Expert',
        variant: 'filled',
        color: 'primary',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=expert1',
        removable: true,
        badge: '15 years'
      },
      {
        id: 'specialist-ip',
        label: 'IP Specialist',
        variant: 'filled',
        color: 'info',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=expert2',
        removable: true,
        badge: 'Certified'
      },
      {
        id: 'junior-associate',
        label: 'Junior Associate',
        variant: 'outlined',
        color: 'secondary',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=junior',
        removable: true,
        badge: '2 years'
      },
      {
        id: 'partner',
        label: 'Senior Partner',
        variant: 'filled',
        color: 'success',
        avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=partner',
        removable: true,
        badge: 'Partner',
        priority: 'high'
      }
    ];
  }

  handlePracticeAreaSelect(chip: ChipData, selected: boolean) {
    if (selected) {
      this.selectedAreas = [...this.selectedAreas, chip.id];
    } else {
      this.selectedAreas = this.selectedAreas.filter(id => id !== chip.id);
    }
    console.log('Practice area selection:', chip.label, selected);
  }

  handleClearAllAreas() {
    this.selectedAreas = [];
    console.log('All practice areas cleared');
  }

  getSelectedPracticeAreas(): ChipData[] {
    return this.practiceAreas.filter(area => this.selectedAreas.includes(area.id));
  }

  removeSelectedArea(areaId: string) {
    this.selectedAreas = this.selectedAreas.filter(id => id !== areaId);
  }

  handleDocumentTagRemove(chip: ChipData) {
    this.documentTags = this.documentTags.filter(tag => tag.id !== chip.id);
    console.log('Document tag removed:', chip.label);
  }

  handleDocumentTagClick(chip: ChipData) {
    console.log('Document tag clicked:', chip.label);
  }

  handleExpertiseTagRemove(chip: ChipData) {
    this.expertiseTags = this.expertiseTags.filter(tag => tag.id !== chip.id);
    console.log('Expertise tag removed:', chip.label);
  }

  handleExpertiseTagClick(chip: ChipData) {
    console.log('Expertise tag clicked:', chip.label);
  }

  handleTagInput(event: KeyboardEvent) {
    if (event.key === 'Enter') {
      const input = event.target as HTMLInputElement;
      const value = input.value.trim();
      if (value) {
        this.addDocumentTag(value);
        input.value = '';
      }
    }
  }

  addDocumentTag(tagName: string) {
    const tag: ChipData = {
      id: `tag-${Date.now()}`,
      label: tagName,
      variant: 'outlined',
      color: 'neutral',
      removable: true,
      icon: 'tag'
    };
    this.documentTags = [...this.documentTags, tag];
  }

  handleCategoryReorder(newOrder: ChipData[]) {
    this.sortableCategories = newOrder;
    console.log('New category order:', newOrder);
  }

  handleCategoryRemove(chip: ChipData) {
    this.sortableCategories = this.sortableCategories.filter(cat => cat.id !== chip.id);
    console.log('Category removed:', chip.label);
  }

  handleTermSelect(chip: ChipData, selected: boolean) {
    console.log('Term selection:', chip.label, selected);
  }
}
```

### Research Filter Chips

#### React
```jsx
import { SafChip, SafChipGroup, SafIcon } from '@saffron/react';
import { useState, useEffect } from 'react';

const ResearchFilterChips = () => {
  const [activeFilters, setActiveFilters] = useState({});
  const [searchResults, setSearchResults] = useState(null);

  // Research database filter options
  const filterOptions = {
    jurisdiction: [
      { id: 'federal', label: 'Federal', value: 'federal', selectable: true },
      { id: 'state', label: 'State', value: 'state', selectable: true },
      { id: 'international', label: 'International', value: 'international', selectable: true }
    ],
    courtLevel: [
      { id: 'supreme', label: 'Supreme Court', value: 'supreme', selectable: true },
      { id: 'appellate', label: 'Appellate Courts', value: 'appellate', selectable: true },
      { id: 'district', label: 'District Courts', value: 'district', selectable: true },
      { id: 'specialty', label: 'Specialty Courts', value: 'specialty', selectable: true }
    ],
    dateRange: [
      { id: 'recent', label: 'Last 30 days', value: '30d', selectable: true, color: 'success' },
      { id: 'quarter', label: 'Last 3 months', value: '3m', selectable: true, color: 'info' },
      { id: 'year', label: 'Last year', value: '1y', selectable: true, color: 'warning' },
      { id: 'all', label: 'All time', value: 'all', selectable: true, color: 'neutral' }
    ],
    contentType: [
      { id: 'cases', label: 'Case Law', value: 'cases', selectable: true, icon: 'gavel' },
      { id: 'statutes', label: 'Statutes', value: 'statutes', selectable: true, icon: 'book' },
      { id: 'regulations', label: 'Regulations', value: 'regulations', selectable: true, icon: 'shield' },
      { id: 'secondary', label: 'Secondary Sources', value: 'secondary', selectable: true, icon: 'bookmark' }
    ],
    practiceArea: [
      { id: 'corporate', label: 'Corporate', value: 'corporate', selectable: true },
      { id: 'litigation', label: 'Litigation', value: 'litigation', selectable: true },
      { id: 'ip', label: 'IP Law', value: 'ip', selectable: true },
      { id: 'employment', label: 'Employment', value: 'employment', selectable: true },
      { id: 'tax', label: 'Tax', value: 'tax', selectable: true }
    ]
  };

  // Applied filter chips (dynamic based on selections)
  const getAppliedFilters = () => {
    const applied = [];
    
    Object.entries(activeFilters).forEach(([category, selectedIds]) => {
      if (selectedIds && selectedIds.length > 0) {
        selectedIds.forEach(id => {
          const filterOption = filterOptions[category]?.find(opt => opt.id === id);
          if (filterOption) {
            applied.push({
              ...filterOption,
              category,
              removable: true,
              variant: 'filled'
            });
          }
        });
      }
    });
    
    return applied;
  };

  // Suggested filter chips (commonly used combinations)
  const suggestedFilters = [
    {
      id: 'recent-cases',
      label: 'Recent Federal Cases',
      variant: 'outlined',
      color: 'primary',
      icon: 'trending-up',
      clickable: true,
      tooltip: 'Federal cases from last 30 days',
      filters: {
        jurisdiction: ['federal'],
        contentType: ['cases'],
        dateRange: ['recent']
      }
    },
    {
      id: 'corporate-law',
      label: 'Corporate Law Research',
      variant: 'outlined',
      color: 'info',
      icon: 'building',
      clickable: true,
      tooltip: 'All corporate law content',
      filters: {
        practiceArea: ['corporate'],
        contentType: ['cases', 'statutes', 'regulations']
      }
    },
    {
      id: 'appellate-decisions',
      label: 'Appellate Decisions',
      variant: 'outlined',
      color: 'warning',
      icon: 'trending-up',
      clickable: true,
      tooltip: 'Appellate court decisions',
      filters: {
        courtLevel: ['appellate'],
        contentType: ['cases']
      }
    },
    {
      id: 'ip-recent',
      label: 'Recent IP Cases',
      variant: 'outlined',
      color: 'success',
      icon: 'lightbulb',
      clickable: true,
      tooltip: 'Recent intellectual property cases',
      filters: {
        practiceArea: ['ip'],
        contentType: ['cases'],
        dateRange: ['quarter']
      }
    }
  ];

  useEffect(() => {
    // Simulate search results update when filters change
    const appliedCount = Object.values(activeFilters).flat().length;
    if (appliedCount > 0) {
      setSearchResults({
        total: Math.max(100 - (appliedCount * 15), 10),
        categories: {
          cases: Math.max(50 - (appliedCount * 8), 5),
          statutes: Math.max(30 - (appliedCount * 4), 2),
          regulations: Math.max(15 - (appliedCount * 2), 1),
          secondary: Math.max(25 - (appliedCount * 3), 2)
        }
      });
    } else {
      setSearchResults({
        total: 1247,
        categories: {
          cases: 756,
          statutes: 234,
          regulations: 123,
          secondary: 134
        }
      });
    }
  }, [activeFilters]);

  const handleFilterSelect = (category, chip, selected) => {
    setActiveFilters(prev => {
      const categoryFilters = prev[category] || [];
      if (selected) {
        return {
          ...prev,
          [category]: [...categoryFilters, chip.id]
        };
      } else {
        return {
          ...prev,
          [category]: categoryFilters.filter(id => id !== chip.id)
        };
      }
    });
  };

  const handleAppliedFilterRemove = (chip) => {
    setActiveFilters(prev => {
      const categoryFilters = prev[chip.category] || [];
      return {
        ...prev,
        [chip.category]: categoryFilters.filter(id => id !== chip.id)
      };
    });
  };

  const handleSuggestedFilterClick = (suggestedFilter) => {
    // Apply all filters from the suggested combination
    setActiveFilters(prev => {
      const newFilters = { ...prev };
      Object.entries(suggestedFilter.filters).forEach(([category, values]) => {
        newFilters[category] = [...(newFilters[category] || []), ...values];
      });
      return newFilters;
    });
  };

  const handleClearAllFilters = () => {
    setActiveFilters({});
  };

  const getFilterChipsWithSelection = (category) => {
    const selectedIds = activeFilters[category] || [];
    return filterOptions[category].map(filter => ({
      ...filter,
      selected: selectedIds.includes(filter.id)
    }));
  };

  return (
    <div className="research-filter-chips-demo">
      <h2>Legal Research Filter Interface</h2>

      {/* Search Results Summary */}
      <div className="search-results-summary">
        <h3>Search Results</h3>
        {searchResults && (
          <div className="results-info">
            <SafChip
              label={`${searchResults.total} total results`}
              variant="filled"
              color="primary"
              icon="search"
              size="large"
            />
            <div className="result-breakdown">
              <SafChip label={`${searchResults.categories.cases} Cases`} variant="soft" color="info" />
              <SafChip label={`${searchResults.categories.statutes} Statutes`} variant="soft" color="success" />
              <SafChip label={`${searchResults.categories.regulations} Regulations`} variant="soft" color="warning" />
              <SafChip label={`${searchResults.categories.secondary} Secondary`} variant="soft" color="neutral" />
            </div>
          </div>
        )}
      </div>

      {/* Applied Filters */}
      <div className="applied-filters-section">
        <div className="section-header">
          <h3>Applied Filters</h3>
          {getAppliedFilters().length > 0 && (
            <button onClick={handleClearAllFilters} className="clear-all-btn">
              <SafIcon name="x" /> Clear All
            </button>
          )}
        </div>
        
        {getAppliedFilters().length > 0 ? (
          <SafChipGroup
            chips={getAppliedFilters()}
            layout="wrap"
            spacing="small"
            onChipRemove={handleAppliedFilterRemove}
          />
        ) : (
          <p className="no-filters">No filters applied</p>
        )}
      </div>

      {/* Suggested Filter Combinations */}
      <div className="suggested-filters-section">
        <h3>Suggested Filter Combinations</h3>
        <SafChipGroup
          chips={suggestedFilters}
          layout="wrap"
          spacing="medium"
          onChipClick={handleSuggestedFilterClick}
        />
      </div>

      {/* Filter Categories */}
      <div className="filter-categories">
        {/* Jurisdiction Filters */}
        <div className="filter-category">
          <h4>
            <SafIcon name="map" /> Jurisdiction
          </h4>
          <SafChipGroup
            chips={getFilterChipsWithSelection('jurisdiction')}
            layout="horizontal"
            spacing="small"
            multiSelect={true}
            onChipSelect={(chip, selected) => handleFilterSelect('jurisdiction', chip, selected)}
          />
        </div>

        {/* Court Level Filters */}
        <div className="filter-category">
          <h4>
            <SafIcon name="building" /> Court Level
          </h4>
          <SafChipGroup
            chips={getFilterChipsWithSelection('courtLevel')}
            layout="horizontal"
            spacing="small"
            multiSelect={true}
            onChipSelect={(chip, selected) => handleFilterSelect('courtLevel', chip, selected)}
          />
        </div>

        {/* Date Range Filters */}
        <div className="filter-category">
          <h4>
            <SafIcon name="calendar" /> Date Range
          </h4>
          <SafChipGroup
            chips={getFilterChipsWithSelection('dateRange')}
            layout="horizontal"
            spacing="small"
            multiSelect={false} // Single selection for date range
            onChipSelect={(chip, selected) => {
              if (selected) {
                // Clear other date selections and set this one
                setActiveFilters(prev => ({
                  ...prev,
                  dateRange: [chip.id]
                }));
              }
            }}
          />
        </div>

        {/* Content Type Filters */}
        <div className="filter-category">
          <h4>
            <SafIcon name="file" /> Content Type
          </h4>
          <SafChipGroup
            chips={getFilterChipsWithSelection('contentType')}
            layout="horizontal"
            spacing="small"
            multiSelect={true}
            onChipSelect={(chip, selected) => handleFilterSelect('contentType', chip, selected)}
          />
        </div>

        {/* Practice Area Filters */}
        <div className="filter-category">
          <h4>
            <SafIcon name="briefcase" /> Practice Area
          </h4>
          <SafChipGroup
            chips={getFilterChipsWithSelection('practiceArea')}
            layout="wrap"
            spacing="small"
            multiSelect={true}
            maxItems={6}
            collapsible={true}
            onChipSelect={(chip, selected) => handleFilterSelect('practiceArea', chip, selected)}
          />
        </div>
      </div>

      {/* Advanced Filter Features */}
      <div className="advanced-features">
        <h3>Advanced Filter Features</h3>
        
        <div className="feature-showcase">
          <div className="feature-item">
            <h4>Smart Filter Suggestions</h4>
            <p>AI-powered filter recommendations based on your search query and history</p>
            <div className="smart-suggestions">
              <SafChip
                label="Similar to previous searches"
                variant="soft"
                color="info"
                icon="brain"
                clickable={true}
              />
              <SafChip
                label="Trending in your practice area"
                variant="soft"
                color="warning"
                icon="trending-up"
                clickable={true}
              />
            </div>
          </div>

          <div className="feature-item">
            <h4>Saved Filter Sets</h4>
            <p>Save and reuse common filter combinations</p>
            <div className="saved-filters">
              <SafChip
                label="Corporate M&A Research"
                variant="outlined"
                color="primary"
                icon="bookmark"
                clickable={true}
                badge="Saved"
              />
              <SafChip
                label="Federal Tax Cases"
                variant="outlined"
                color="secondary"
                icon="bookmark"
                clickable={true}
                badge="Saved"
              />
            </div>
          </div>

          <div className="feature-item">
            <h4>Filter Analytics</h4>
            <p>Track filter usage and optimization suggestions</p>
            <div className="filter-analytics">
              <SafChip
                label="Most used this month"
                variant="soft"
                color="success"
                icon="bar-chart"
                badge="5x"
              />
              <SafChip
                label="Optimize for better results"
                variant="soft"
                color="warning"
                icon="zap"
                clickable={true}
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};
```

## Best Practices

1. **Visual Hierarchy**
   - Use consistent color coding for different chip types
   - Implement appropriate spacing and grouping
   - Apply consistent sizing across related chips

2. **Interaction Design**
   - Provide clear visual feedback for different states
   - Use intuitive icons and labels
   - Implement smooth transitions and animations

3. **Content Management**
   - Keep chip labels concise and descriptive
   - Use tooltips for additional context
   - Implement efficient filtering and searching

4. **Performance Optimization**
   - Virtualize large chip collections
   - Implement lazy loading for chip data
   - Use efficient state management for selections

5. **User Experience**
   - Group related chips logically
   - Provide clear removal and selection mechanisms
   - Support keyboard navigation throughout

## Accessibility Considerations

1. **Screen Reader Support**
   - Provide clear chip descriptions and states
   - Announce selection and removal actions
   - Use semantic markup for chip groups

2. **Keyboard Navigation**
   - Support Tab navigation through chips
   - Implement Enter/Space for selection
   - Support arrow keys for chip navigation

3. **Visual Accessibility**
   - Ensure sufficient color contrast for all variants
   - Use multiple indicators for states (color, icons, text)
   - Support high contrast and reduced motion

4. **Focus Management**
   - Provide clear focus indicators
   - Maintain logical focus order
   - Handle focus appropriately on removal

## Related Components

- **SafIcon**: Icons for chip visual identification
- **SafAvatar**: User avatars in chip displays
- **SafBadge**: Additional indicators and counts
- **SafButton**: Chip interaction behaviors
- **SafTooltip**: Additional context for chips

## Notes

- Chip component supports both controlled and uncontrolled usage patterns
- Built-in support for drag-and-drop reordering in chip groups
- Customizable remove icons and behaviors
- Automatic text truncation with configurable widths
- Comprehensive keyboard and screen reader accessibility
- Mobile-responsive design with touch-friendly interactions
- Integration with form validation and data management systems
