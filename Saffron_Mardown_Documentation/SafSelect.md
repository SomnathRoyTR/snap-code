# SafSelect Component (Comprehensive)

## Overview

SafSelect is a comprehensive dropdown selection component that provides advanced functionality including single and multi-selection, searchable options, option grouping, custom rendering, virtual scrolling, and accessibility support. It handles complex selection scenarios from simple dropdowns to advanced multi-select interfaces with search, filtering, and custom option displays.

## React API

### SafSelect

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `value` | `any \| any[]` | No | - | Selected value(s) - single value or array for multi-select |
| `defaultValue` | `any \| any[]` | No | - | Default selected value(s) for uncontrolled usage |
| `options` | `SelectOption[] \| SelectOptionGroup[]` | Yes | - | Available options or option groups |
| `placeholder` | `string` | No | `'Select...'` | Placeholder text when no selection |
| `label` | `string \| ReactNode` | No | - | Label text for the select |
| `description` | `string \| ReactNode` | No | - | Additional descriptive text |
| `helperText` | `string \| ReactNode` | No | - | Helper text below the select |
| `error` | `string \| boolean` | No | `false` | Error state and message |
| `success` | `string \| boolean` | No | `false` | Success state and message |
| `warning` | `string \| boolean` | No | `false` | Warning state and message |
| `required` | `boolean` | No | `false` | Whether selection is required |
| `disabled` | `boolean` | No | `false` | Whether the select is disabled |
| `readOnly` | `boolean` | No | `false` | Whether the select is read-only |
| `multiple` | `boolean` | No | `false` | Whether multiple selection is allowed |
| `searchable` | `boolean` | No | `false` | Whether options can be searched/filtered |
| `clearable` | `boolean` | No | `false` | Whether selection can be cleared |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the select |
| `variant` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `fullWidth` | `boolean` | No | `false` | Whether select takes full container width |
| `maxHeight` | `number` | No | `300` | Maximum height of dropdown in pixels |
| `maxSelections` | `number` | No | - | Maximum number of selections (multi-select) |
| `showSelectAll` | `boolean` | No | `false` | Whether to show select all option (multi-select) |
| `showSelectedCount` | `boolean` | No | `false` | Whether to show count of selected items |
| `groupBy` | `string \| ((option: SelectOption) => string)` | No | - | Property or function to group options by |
| `sortBy` | `string \| ((a: SelectOption, b: SelectOption) => number)` | No | - | Property or function to sort options by |
| `filterBy` | `string[] \| ((option: SelectOption, query: string) => boolean)` | No | `['label']` | Properties to filter by or custom filter function |
| `virtualScrolling` | `boolean` | No | `false` | Whether to enable virtual scrolling for large lists |
| `virtualizationThreshold` | `number` | No | `100` | Minimum options count to enable virtualization |
| `loadOnOpen` | `boolean` | No | `false` | Whether to load options when dropdown opens |
| `closeOnSelect` | `boolean` | No | `true` | Whether to close dropdown after selection (single-select) |
| `showCheckboxes` | `boolean` | No | `false` | Whether to show checkboxes for multi-select |
| `renderOption` | `(option: SelectOption) => ReactNode` | No | - | Custom option rendering function |
| `renderValue` | `(value: any, option?: SelectOption) => ReactNode` | No | - | Custom selected value rendering function |
| `renderGroup` | `(group: string, options: SelectOption[]) => ReactNode` | No | - | Custom group header rendering function |
| `renderNoOptions` | `() => ReactNode` | No | - | Custom no options message rendering |
| `isOptionDisabled` | `(option: SelectOption) => boolean` | No | - | Function to determine if option is disabled |
| `isOptionSelected` | `(option: SelectOption, value: any) => boolean` | No | - | Custom selection comparison function |
| `getOptionValue` | `(option: SelectOption) => any` | No | - | Function to extract value from option |
| `getOptionLabel` | `(option: SelectOption) => string` | No | - | Function to extract label from option |
| `searchPlaceholder` | `string` | No | `'Search options...'` | Placeholder for search input |
| `noOptionsText` | `string` | No | `'No options available'` | Text when no options found |
| `loadingText` | `string` | No | `'Loading...'` | Text shown while loading |
| `selectAllText` | `string` | No | `'Select All'` | Text for select all option |
| `clearSelectionText` | `string` | No | `'Clear Selection'` | Text for clear selection action |
| `debounceMs` | `number` | No | `200` | Debounce delay for search input |
| `onChange` | `(value: any \| any[], option?: SelectOption \| SelectOption[]) => void` | No | - | Callback when selection changes |
| `onOpen` | `() => void` | No | - | Callback when dropdown opens |
| `onClose` | `() => void` | No | - | Callback when dropdown closes |
| `onSearch` | `(query: string) => void` | No | - | Callback when search query changes |
| `onLoadMore` | `() => void` | No | - | Callback for infinite scrolling |
| `onClear` | `() => void` | No | - | Callback when selection is cleared |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### SelectOption Interface

```typescript
interface SelectOption {
  value: any;
  label: string;
  description?: string;
  icon?: string | ReactNode;
  disabled?: boolean;
  group?: string;
  data?: any;
}
```

### SelectOptionGroup Interface

```typescript
interface SelectOptionGroup {
  label: string;
  options: SelectOption[];
  disabled?: boolean;
}
```

## Angular API

### saf-select

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[value]` | `any \| any[]` | No | - | Selected value(s) - single value or array for multi-select |
| `[options]` | `SelectOption[] \| SelectOptionGroup[]` | Yes | - | Available options or option groups |
| `[placeholder]` | `string` | No | `'Select...'` | Placeholder text when no selection |
| `[label]` | `string \| TemplateRef` | No | - | Label text for the select |
| `[description]` | `string \| TemplateRef` | No | - | Additional descriptive text |
| `[helperText]` | `string \| TemplateRef` | No | - | Helper text below the select |
| `[error]` | `string \| boolean` | No | `false` | Error state and message |
| `[success]` | `string \| boolean` | No | `false` | Success state and message |
| `[warning]` | `string \| boolean` | No | `false` | Warning state and message |
| `[required]` | `boolean` | No | `false` | Whether selection is required |
| `[disabled]` | `boolean` | No | `false` | Whether the select is disabled |
| `[readonly]` | `boolean` | No | `false` | Whether the select is read-only |
| `[multiple]` | `boolean` | No | `false` | Whether multiple selection is allowed |
| `[searchable]` | `boolean` | No | `false` | Whether options can be searched/filtered |
| `[clearable]` | `boolean` | No | `false` | Whether selection can be cleared |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the select |
| `[variant]` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `[fullWidth]` | `boolean` | No | `false` | Whether select takes full container width |
| `[maxHeight]` | `number` | No | `300` | Maximum height of dropdown in pixels |
| `[maxSelections]` | `number` | No | - | Maximum number of selections (multi-select) |
| `[showSelectAll]` | `boolean` | No | `false` | Whether to show select all option (multi-select) |
| `[showSelectedCount]` | `boolean` | No | `false` | Whether to show count of selected items |
| `[virtualScrolling]` | `boolean` | No | `false` | Whether to enable virtual scrolling for large lists |
| `[closeOnSelect]` | `boolean` | No | `true` | Whether to close dropdown after selection |
| `[showCheckboxes]` | `boolean` | No | `false` | Whether to show checkboxes for multi-select |
| `[searchPlaceholder]` | `string` | No | `'Search options...'` | Placeholder for search input |
| `[noOptionsText]` | `string` | No | `'No options available'` | Text when no options found |
| `[loadingText]` | `string` | No | `'Loading...'` | Text shown while loading |
| `[debounceMs]` | `number` | No | `200` | Debounce delay for search input |
| `(valueChange)` | `EventEmitter<any \| any[]>` | No | - | Event when selection changes |
| `(open)` | `EventEmitter<void>` | No | - | Event when dropdown opens |
| `(close)` | `EventEmitter<void>` | No | - | Event when dropdown closes |
| `(search)` | `EventEmitter<string>` | No | - | Event when search query changes |
| `(clear)` | `EventEmitter<void>` | No | - | Event when selection is cleared |

## Usage Examples

### Basic Select Usage

#### React
```jsx
import { SafSelect, SafCard, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const BasicSelectExample = () => {
  const [country, setCountry] = useState('');
  const [language, setLanguage] = useState('');
  const [timezone, setTimezone] = useState('');
  const [currency, setCurrency] = useState('');

  const countries = [
    { value: 'us', label: 'United States', icon: '🇺🇸' },
    { value: 'ca', label: 'Canada', icon: '🇨🇦' },
    { value: 'uk', label: 'United Kingdom', icon: '🇬🇧' },
    { value: 'de', label: 'Germany', icon: '🇩🇪' },
    { value: 'fr', label: 'France', icon: '🇫🇷' },
    { value: 'jp', label: 'Japan', icon: '🇯🇵' },
    { value: 'au', label: 'Australia', icon: '🇦🇺' }
  ];

  const languages = [
    { value: 'en', label: 'English', description: 'International language' },
    { value: 'es', label: 'Spanish', description: 'Español' },
    { value: 'fr', label: 'French', description: 'Français' },
    { value: 'de', label: 'German', description: 'Deutsch' },
    { value: 'it', label: 'Italian', description: 'Italiano' },
    { value: 'pt', label: 'Portuguese', description: 'Português' },
    { value: 'ru', label: 'Russian', description: 'Русский' },
    { value: 'zh', label: 'Chinese', description: '中文' },
    { value: 'ja', label: 'Japanese', description: '日本語' },
    { value: 'ko', label: 'Korean', description: '한국어' }
  ];

  const timezones = [
    { value: 'utc-12', label: 'UTC-12:00', description: 'Baker Island' },
    { value: 'utc-11', label: 'UTC-11:00', description: 'American Samoa' },
    { value: 'utc-10', label: 'UTC-10:00', description: 'Hawaii' },
    { value: 'utc-9', label: 'UTC-09:00', description: 'Alaska' },
    { value: 'utc-8', label: 'UTC-08:00', description: 'Pacific Time' },
    { value: 'utc-7', label: 'UTC-07:00', description: 'Mountain Time' },
    { value: 'utc-6', label: 'UTC-06:00', description: 'Central Time' },
    { value: 'utc-5', label: 'UTC-05:00', description: 'Eastern Time' },
    { value: 'utc-4', label: 'UTC-04:00', description: 'Atlantic Time' },
    { value: 'utc+0', label: 'UTC+00:00', description: 'Greenwich Mean Time' },
    { value: 'utc+1', label: 'UTC+01:00', description: 'Central European Time' },
    { value: 'utc+9', label: 'UTC+09:00', description: 'Japan Standard Time' }
  ];

  const currencies = [
    { value: 'usd', label: 'US Dollar', description: '$', disabled: false },
    { value: 'eur', label: 'Euro', description: '€', disabled: false },
    { value: 'gbp', label: 'British Pound', description: '£', disabled: false },
    { value: 'jpy', label: 'Japanese Yen', description: '¥', disabled: false },
    { value: 'cad', label: 'Canadian Dollar', description: 'C$', disabled: false },
    { value: 'aud', label: 'Australian Dollar', description: 'A$', disabled: false },
    { value: 'chf', label: 'Swiss Franc', description: 'Fr', disabled: true },
    { value: 'cny', label: 'Chinese Yuan', description: '¥', disabled: true }
  ];

  return (
    <SafCard className="basic-select-demo">
      <SafCard.Header>
        <h2>User Preferences</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="preferences-form">
          <SafSelect
            label="Country"
            placeholder="Select your country"
            options={countries}
            value={country}
            onChange={setCountry}
            required={true}
            searchable={true}
            clearable={true}
            renderOption={(option) => (
              <div className="country-option">
                <span className="flag">{option.icon}</span>
                <span className="name">{option.label}</span>
              </div>
            )}
            helperText="This affects regional settings and available services"
          />

          <SafSelect
            label="Preferred Language"
            placeholder="Choose your language"
            options={languages}
            value={language}
            onChange={setLanguage}
            required={true}
            searchable={true}
            variant="filled"
            renderOption={(option) => (
              <div className="language-option">
                <div className="main">{option.label}</div>
                <div className="description">{option.description}</div>
              </div>
            )}
          />

          <SafSelect
            label="Timezone"
            placeholder="Select your timezone"
            options={timezones}
            value={timezone}
            onChange={setTimezone}
            searchable={true}
            maxHeight={200}
            filterBy={['label', 'description']}
            renderValue={(value, option) => option ? `${option.label} (${option.description})` : value}
            helperText="Used for scheduling and time-sensitive features"
          />

          <SafSelect
            label="Currency"
            placeholder="Select currency"
            options={currencies}
            value={currency}
            onChange={setCurrency}
            size="small"
            isOptionDisabled={(option) => option.disabled}
            renderOption={(option) => (
              <div className="currency-option">
                <span className="symbol">{option.description}</span>
                <span className="name">{option.label}</span>
                {option.disabled && <SafBadge variant="outline" size="small">Coming Soon</SafBadge>}
              </div>
            )}
          />
        </div>

        <div className="selection-summary">
          <h3>Current Selection:</h3>
          <ul>
            {country && <li>Country: {countries.find(c => c.value === country)?.label}</li>}
            {language && <li>Language: {languages.find(l => l.value === language)?.label}</li>}
            {timezone && <li>Timezone: {timezones.find(t => t.value === timezone)?.label}</li>}
            {currency && <li>Currency: {currencies.find(c => c.value === currency)?.label}</li>}
          </ul>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// basic-select.component.ts
import { Component } from '@angular/core';

interface SelectOption {
  value: string;
  label: string;
  description?: string;
  icon?: string;
  disabled?: boolean;
}

@Component({
  selector: 'app-basic-select',
  template: `
    <saf-card class="basic-select-demo">
      <saf-card-header>
        <h2>User Preferences</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="preferences-form">
          <saf-select
            label="Country"
            placeholder="Select your country"
            [options]="countries"
            [value]="country"
            (valueChange)="country = $event"
            [required]="true"
            [searchable]="true"
            [clearable]="true"
            helperText="This affects regional settings and available services">
            <ng-template #optionTemplate let-option>
              <div class="country-option">
                <span class="flag">{{ option.icon }}</span>
                <span class="name">{{ option.label }}</span>
              </div>
            </ng-template>
          </saf-select>

          <saf-select
            label="Preferred Language"
            placeholder="Choose your language"
            [options]="languages"
            [value]="language"
            (valueChange)="language = $event"
            [required]="true"
            [searchable]="true"
            variant="filled">
            <ng-template #optionTemplate let-option>
              <div class="language-option">
                <div class="main">{{ option.label }}</div>
                <div class="description">{{ option.description }}</div>
              </div>
            </ng-template>
          </saf-select>

          <saf-select
            label="Timezone"
            placeholder="Select your timezone"
            [options]="timezones"
            [value]="timezone"
            (valueChange)="timezone = $event"
            [searchable]="true"
            [maxHeight]="200"
            helperText="Used for scheduling and time-sensitive features">
          </saf-select>

          <saf-select
            label="Currency"
            placeholder="Select currency"
            [options]="currencies"
            [value]="currency"
            (valueChange)="currency = $event"
            size="small">
            <ng-template #optionTemplate let-option>
              <div class="currency-option">
                <span class="symbol">{{ option.description }}</span>
                <span class="name">{{ option.label }}</span>
                <saf-badge 
                  *ngIf="option.disabled" 
                  variant="outline" 
                  size="small">
                  Coming Soon
                </saf-badge>
              </div>
            </ng-template>
          </saf-select>
        </div>

        <div class="selection-summary">
          <h3>Current Selection:</h3>
          <ul>
            <li *ngIf="country">Country: {{ getCountryName() }}</li>
            <li *ngIf="language">Language: {{ getLanguageName() }}</li>
            <li *ngIf="timezone">Timezone: {{ getTimezoneName() }}</li>
            <li *ngIf="currency">Currency: {{ getCurrencyName() }}</li>
          </ul>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class BasicSelectComponent {
  country = '';
  language = '';
  timezone = '';
  currency = '';

  countries: SelectOption[] = [
    { value: 'us', label: 'United States', icon: '🇺🇸' },
    { value: 'ca', label: 'Canada', icon: '🇨🇦' },
    { value: 'uk', label: 'United Kingdom', icon: '🇬🇧' },
    { value: 'de', label: 'Germany', icon: '🇩🇪' },
    { value: 'fr', label: 'France', icon: '🇫🇷' },
    { value: 'jp', label: 'Japan', icon: '🇯🇵' },
    { value: 'au', label: 'Australia', icon: '🇦🇺' }
  ];

  languages: SelectOption[] = [
    { value: 'en', label: 'English', description: 'International language' },
    { value: 'es', label: 'Spanish', description: 'Español' },
    { value: 'fr', label: 'French', description: 'Français' },
    { value: 'de', label: 'German', description: 'Deutsch' },
    { value: 'it', label: 'Italian', description: 'Italiano' },
    { value: 'pt', label: 'Portuguese', description: 'Português' },
    { value: 'ru', label: 'Russian', description: 'Русский' },
    { value: 'zh', label: 'Chinese', description: '中文' },
    { value: 'ja', label: 'Japanese', description: '日本語' },
    { value: 'ko', label: 'Korean', description: '한국어' }
  ];

  timezones: SelectOption[] = [
    { value: 'utc-8', label: 'UTC-08:00', description: 'Pacific Time' },
    { value: 'utc-7', label: 'UTC-07:00', description: 'Mountain Time' },
    { value: 'utc-6', label: 'UTC-06:00', description: 'Central Time' },
    { value: 'utc-5', label: 'UTC-05:00', description: 'Eastern Time' },
    { value: 'utc+0', label: 'UTC+00:00', description: 'Greenwich Mean Time' },
    { value: 'utc+1', label: 'UTC+01:00', description: 'Central European Time' },
    { value: 'utc+9', label: 'UTC+09:00', description: 'Japan Standard Time' }
  ];

  currencies: SelectOption[] = [
    { value: 'usd', label: 'US Dollar', description: '$', disabled: false },
    { value: 'eur', label: 'Euro', description: '€', disabled: false },
    { value: 'gbp', label: 'British Pound', description: '£', disabled: false },
    { value: 'jpy', label: 'Japanese Yen', description: '¥', disabled: false },
    { value: 'cad', label: 'Canadian Dollar', description: 'C$', disabled: false },
    { value: 'aud', label: 'Australian Dollar', description: 'A$', disabled: false },
    { value: 'chf', label: 'Swiss Franc', description: 'Fr', disabled: true },
    { value: 'cny', label: 'Chinese Yuan', description: '¥', disabled: true }
  ];

  getCountryName(): string {
    return this.countries.find(c => c.value === this.country)?.label || '';
  }

  getLanguageName(): string {
    return this.languages.find(l => l.value === this.language)?.label || '';
  }

  getTimezoneName(): string {
    return this.timezones.find(t => t.value === this.timezone)?.label || '';
  }

  getCurrencyName(): string {
    return this.currencies.find(c => c.value === this.currency)?.label || '';
  }
}
```

### Multi-Select with Advanced Features

#### React
```jsx
import { SafSelect, SafCard, SafButton, SafIcon, SafBadge, SafChip } from '@saffron/react';
import { useState } from 'react';

const MultiSelectExample = () => {
  const [selectedSkills, setSelectedSkills] = useState([]);
  const [selectedTeams, setSelectedTeams] = useState([]);
  const [selectedPermissions, setSelectedPermissions] = useState([]);

  const skillsOptions = [
    { value: 'javascript', label: 'JavaScript', group: 'Programming', icon: '🟨' },
    { value: 'typescript', label: 'TypeScript', group: 'Programming', icon: '🔷' },
    { value: 'python', label: 'Python', group: 'Programming', icon: '🐍' },
    { value: 'java', label: 'Java', group: 'Programming', icon: '☕' },
    { value: 'csharp', label: 'C#', group: 'Programming', icon: '💜' },
    { value: 'react', label: 'React', group: 'Frontend', icon: '⚛️' },
    { value: 'vue', label: 'Vue.js', group: 'Frontend', icon: '💚' },
    { value: 'angular', label: 'Angular', group: 'Frontend', icon: '🔴' },
    { value: 'nodejs', label: 'Node.js', group: 'Backend', icon: '💚' },
    { value: 'express', label: 'Express.js', group: 'Backend', icon: '⚡' },
    { value: 'nestjs', label: 'NestJS', group: 'Backend', icon: '🦅' },
    { value: 'mongodb', label: 'MongoDB', group: 'Database', icon: '🍃' },
    { value: 'postgresql', label: 'PostgreSQL', group: 'Database', icon: '🐘' },
    { value: 'mysql', label: 'MySQL', group: 'Database', icon: '🐬' },
    { value: 'aws', label: 'AWS', group: 'Cloud', icon: '☁️' },
    { value: 'azure', label: 'Azure', group: 'Cloud', icon: '🔵' },
    { value: 'docker', label: 'Docker', group: 'DevOps', icon: '🐳' },
    { value: 'kubernetes', label: 'Kubernetes', group: 'DevOps', icon: '⚓' }
  ];

  const teamsOptions = [
    { 
      value: 'frontend',
      label: 'Frontend Team',
      description: '12 members',
      icon: <SafIcon name="monitor" />
    },
    { 
      value: 'backend',
      label: 'Backend Team',
      description: '8 members',
      icon: <SafIcon name="server" />
    },
    { 
      value: 'mobile',
      label: 'Mobile Team',
      description: '6 members',
      icon: <SafIcon name="smartphone" />
    },
    { 
      value: 'devops',
      label: 'DevOps Team',
      description: '4 members',
      icon: <SafIcon name="settings" />
    },
    { 
      value: 'design',
      label: 'Design Team',
      description: '5 members',
      icon: <SafIcon name="palette" />
    },
    { 
      value: 'qa',
      label: 'Quality Assurance',
      description: '7 members',
      icon: <SafIcon name="check-circle" />
    }
  ];

  const permissionsOptions = [
    {
      label: 'User Management',
      options: [
        { value: 'users.read', label: 'View Users', description: 'Read user profiles and information' },
        { value: 'users.write', label: 'Manage Users', description: 'Create, update, and delete users' },
        { value: 'users.admin', label: 'User Administration', description: 'Full user management capabilities' }
      ]
    },
    {
      label: 'Content Management',
      options: [
        { value: 'content.read', label: 'View Content', description: 'Read content and articles' },
        { value: 'content.write', label: 'Manage Content', description: 'Create and edit content' },
        { value: 'content.publish', label: 'Publish Content', description: 'Publish and unpublish content' },
        { value: 'content.admin', label: 'Content Administration', description: 'Full content management' }
      ]
    },
    {
      label: 'System Administration',
      options: [
        { value: 'system.read', label: 'View System Info', description: 'Access system information' },
        { value: 'system.config', label: 'System Configuration', description: 'Modify system settings' },
        { value: 'system.admin', label: 'System Administration', description: 'Full system control' }
      ]
    }
  ];

  const handleSkillsChange = (values) => {
    if (values.length <= 10) { // Limit to 10 skills
      setSelectedSkills(values);
    }
  };

  const getSkillsByGroup = () => {
    const groups = {};
    selectedSkills.forEach(skillValue => {
      const skill = skillsOptions.find(s => s.value === skillValue);
      if (skill) {
        if (!groups[skill.group]) groups[skill.group] = [];
        groups[skill.group].push(skill);
      }
    });
    return groups;
  };

  return (
    <SafCard className="multi-select-demo">
      <SafCard.Header>
        <h2>Team Member Profile</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="profile-form">
          <SafSelect
            label="Technical Skills"
            placeholder="Select your skills..."
            options={skillsOptions}
            value={selectedSkills}
            onChange={handleSkillsChange}
            multiple={true}
            searchable={true}
            showSelectAll={true}
            showSelectedCount={true}
            groupBy="group"
            maxSelections={10}
            showCheckboxes={true}
            clearable={true}
            renderOption={(option) => (
              <div className="skill-option">
                <span className="icon">{option.icon}</span>
                <span className="label">{option.label}</span>
                <SafBadge variant="outline" size="small">{option.group}</SafBadge>
              </div>
            )}
            renderValue={(values) => (
              <div className="skills-display">
                {values.length > 3 ? (
                  <>
                    <span>{values.length} skills selected</span>
                    <SafBadge variant="primary" size="small">
                      {values.length}/10
                    </SafBadge>
                  </>
                ) : (
                  values.map(value => {
                    const skill = skillsOptions.find(s => s.value === value);
                    return skill ? (
                      <SafChip
                        key={value}
                        label={skill.label}
                        icon={skill.icon}
                        size="small"
                        variant="filled"
                      />
                    ) : null;
                  })
                )}
              </div>
            )}
            helperText={`${selectedSkills.length}/10 skills selected`}
            error={selectedSkills.length === 0 ? 'Please select at least one skill' : false}
          />

          <SafSelect
            label="Team Membership"
            placeholder="Select teams to join..."
            options={teamsOptions}
            value={selectedTeams}
            onChange={setSelectedTeams}
            multiple={true}
            searchable={true}
            maxSelections={3}
            closeOnSelect={false}
            renderOption={(option) => (
              <div className="team-option">
                <div className="icon">{option.icon}</div>
                <div className="info">
                  <div className="name">{option.label}</div>
                  <div className="description">{option.description}</div>
                </div>
              </div>
            )}
            helperText="You can join up to 3 teams"
            variant="filled"
          />

          <SafSelect
            label="Permissions"
            placeholder="Select permissions..."
            options={permissionsOptions}
            value={selectedPermissions}
            onChange={setSelectedPermissions}
            multiple={true}
            searchable={true}
            showSelectAll={true}
            virtualScrolling={true}
            maxHeight={400}
            renderGroup={(group, options) => (
              <div className="permission-group">
                <div className="group-header">
                  <SafIcon name="folder" />
                  <span>{group}</span>
                </div>
              </div>
            )}
            renderOption={(option) => (
              <div className="permission-option">
                <div className="main">
                  <SafIcon name="shield" size="small" />
                  <span>{option.label}</span>
                </div>
                <div className="description">{option.description}</div>
              </div>
            )}
            helperText="Select the permissions needed for this role"
          />

          <div className="selection-summary">
            <h3>Selected Skills by Category:</h3>
            {Object.entries(getSkillsByGroup()).map(([group, skills]) => (
              <div key={group} className="skill-group">
                <h4>{group}</h4>
                <div className="skills-list">
                  {skills.map(skill => (
                    <SafChip
                      key={skill.value}
                      label={skill.label}
                      icon={skill.icon}
                      variant="outline"
                      size="small"
                    />
                  ))}
                </div>
              </div>
            ))}
          </div>

          <div className="form-actions">
            <SafButton variant="outline" onClick={() => {
              setSelectedSkills([]);
              setSelectedTeams([]);
              setSelectedPermissions([]);
            }}>
              Clear All
            </SafButton>
            <SafButton 
              variant="primary"
              disabled={selectedSkills.length === 0}
            >
              Save Profile
            </SafButton>
          </div>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// multi-select.component.ts
import { Component } from '@angular/core';

interface SkillOption {
  value: string;
  label: string;
  group: string;
  icon: string;
}

interface TeamOption {
  value: string;
  label: string;
  description: string;
  icon: string;
}

interface PermissionGroup {
  label: string;
  options: {
    value: string;
    label: string;
    description: string;
  }[];
}

@Component({
  selector: 'app-multi-select',
  template: `
    <saf-card class="multi-select-demo">
      <saf-card-header>
        <h2>Team Member Profile</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="profile-form">
          <saf-select
            label="Technical Skills"
            placeholder="Select your skills..."
            [options]="skillsOptions"
            [value]="selectedSkills"
            (valueChange)="handleSkillsChange($event)"
            [multiple]="true"
            [searchable]="true"
            [showSelectAll]="true"
            [showSelectedCount]="true"
            [maxSelections]="10"
            [showCheckboxes]="true"
            [clearable]="true"
            [helperText]="selectedSkills.length + '/10 skills selected'"
            [error]="selectedSkills.length === 0 ? 'Please select at least one skill' : false">
            <ng-template #optionTemplate let-option>
              <div class="skill-option">
                <span class="icon">{{ option.icon }}</span>
                <span class="label">{{ option.label }}</span>
                <saf-badge variant="outline" size="small">{{ option.group }}</saf-badge>
              </div>
            </ng-template>
          </saf-select>

          <saf-select
            label="Team Membership"
            placeholder="Select teams to join..."
            [options]="teamsOptions"
            [value]="selectedTeams"
            (valueChange)="selectedTeams = $event"
            [multiple]="true"
            [searchable]="true"
            [maxSelections]="3"
            [closeOnSelect]="false"
            helperText="You can join up to 3 teams"
            variant="filled">
            <ng-template #optionTemplate let-option>
              <div class="team-option">
                <saf-icon [name]="option.icon"></saf-icon>
                <div class="info">
                  <div class="name">{{ option.label }}</div>
                  <div class="description">{{ option.description }}</div>
                </div>
              </div>
            </ng-template>
          </saf-select>

          <saf-select
            label="Permissions"
            placeholder="Select permissions..."
            [options]="permissionsOptions"
            [value]="selectedPermissions"
            (valueChange)="selectedPermissions = $event"
            [multiple]="true"
            [searchable]="true"
            [showSelectAll]="true"
            [virtualScrolling]="true"
            [maxHeight]="400"
            helperText="Select the permissions needed for this role">
            <ng-template #optionTemplate let-option>
              <div class="permission-option">
                <div class="main">
                  <saf-icon name="shield" size="small"></saf-icon>
                  <span>{{ option.label }}</span>
                </div>
                <div class="description">{{ option.description }}</div>
              </div>
            </ng-template>
          </saf-select>

          <div class="selection-summary">
            <h3>Selected Skills by Category:</h3>
            <div 
              *ngFor="let group of getSkillsByGroup() | keyvalue" 
              class="skill-group">
              <h4>{{ group.key }}</h4>
              <div class="skills-list">
                <saf-chip
                  *ngFor="let skill of group.value"
                  [label]="skill.label"
                  [icon]="skill.icon"
                  variant="outline"
                  size="small">
                </saf-chip>
              </div>
            </div>
          </div>

          <div class="form-actions">
            <saf-button variant="outline" (click)="clearAll()">
              Clear All
            </saf-button>
            <saf-button 
              variant="primary"
              [disabled]="selectedSkills.length === 0">
              Save Profile
            </saf-button>
          </div>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class MultiSelectComponent {
  selectedSkills: string[] = [];
  selectedTeams: string[] = [];
  selectedPermissions: string[] = [];

  skillsOptions: SkillOption[] = [
    { value: 'javascript', label: 'JavaScript', group: 'Programming', icon: '🟨' },
    { value: 'typescript', label: 'TypeScript', group: 'Programming', icon: '🔷' },
    { value: 'python', label: 'Python', group: 'Programming', icon: '🐍' },
    { value: 'react', label: 'React', group: 'Frontend', icon: '⚛️' },
    { value: 'vue', label: 'Vue.js', group: 'Frontend', icon: '💚' },
    { value: 'angular', label: 'Angular', group: 'Frontend', icon: '🔴' },
    { value: 'nodejs', label: 'Node.js', group: 'Backend', icon: '💚' },
    { value: 'mongodb', label: 'MongoDB', group: 'Database', icon: '🍃' },
    { value: 'postgresql', label: 'PostgreSQL', group: 'Database', icon: '🐘' },
    { value: 'aws', label: 'AWS', group: 'Cloud', icon: '☁️' },
    { value: 'docker', label: 'Docker', group: 'DevOps', icon: '🐳' }
  ];

  teamsOptions: TeamOption[] = [
    { value: 'frontend', label: 'Frontend Team', description: '12 members', icon: 'monitor' },
    { value: 'backend', label: 'Backend Team', description: '8 members', icon: 'server' },
    { value: 'mobile', label: 'Mobile Team', description: '6 members', icon: 'smartphone' },
    { value: 'devops', label: 'DevOps Team', description: '4 members', icon: 'settings' },
    { value: 'design', label: 'Design Team', description: '5 members', icon: 'palette' },
    { value: 'qa', label: 'Quality Assurance', description: '7 members', icon: 'check-circle' }
  ];

  permissionsOptions: PermissionGroup[] = [
    {
      label: 'User Management',
      options: [
        { value: 'users.read', label: 'View Users', description: 'Read user profiles and information' },
        { value: 'users.write', label: 'Manage Users', description: 'Create, update, and delete users' },
        { value: 'users.admin', label: 'User Administration', description: 'Full user management capabilities' }
      ]
    },
    {
      label: 'Content Management',
      options: [
        { value: 'content.read', label: 'View Content', description: 'Read content and articles' },
        { value: 'content.write', label: 'Manage Content', description: 'Create and edit content' },
        { value: 'content.publish', label: 'Publish Content', description: 'Publish and unpublish content' }
      ]
    }
  ];

  handleSkillsChange(values: string[]) {
    if (values.length <= 10) {
      this.selectedSkills = values;
    }
  }

  getSkillsByGroup(): { [group: string]: SkillOption[] } {
    const groups: { [group: string]: SkillOption[] } = {};
    this.selectedSkills.forEach(skillValue => {
      const skill = this.skillsOptions.find(s => s.value === skillValue);
      if (skill) {
        if (!groups[skill.group]) groups[skill.group] = [];
        groups[skill.group].push(skill);
      }
    });
    return groups;
  }

  clearAll() {
    this.selectedSkills = [];
    this.selectedTeams = [];
    this.selectedPermissions = [];
  }
}
```

## Best Practices

1. **Option Management**
   - Use consistent option structure across all selects
   - Implement efficient filtering and search algorithms
   - Group related options for better organization

2. **Performance Optimization**
   - Enable virtual scrolling for large option lists
   - Use debouncing for search functionality
   - Implement lazy loading for dynamic options

3. **User Experience**
   - Provide clear visual feedback for selections
   - Use appropriate placeholder and helper text
   - Support keyboard navigation and shortcuts

4. **Multi-Selection Design**
   - Set reasonable limits on maximum selections
   - Provide clear indication of selected items
   - Offer bulk actions like select all/clear all

5. **Accessibility**
   - Use proper ARIA labels and descriptions
   - Support screen reader announcements
   - Ensure keyboard navigation works correctly

## Accessibility Considerations

1. **ARIA Support**
   - Implement proper `aria-expanded`, `aria-selected`, and `aria-describedby`
   - Provide meaningful announcements for option changes
   - Use `aria-activedescendant` for focus management

2. **Keyboard Navigation**
   - Support Arrow keys for option navigation
   - Use Enter/Space for selection
   - Provide Escape key to close dropdown

3. **Screen Reader Compatibility**
   - Announce current selection state
   - Provide clear option descriptions
   - Support both single and multi-selection patterns

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all states
   - Provide clear focus indicators
   - Support high contrast and reduced motion preferences

## Related Components

- **SafAutocomplete**: Type-ahead selection with free text input
- **SafCombobox**: Combination of input and select functionality
- **SafListbox**: List-based selection without dropdown
- **SafChip**: Display selected items in multi-select
- **SafCheckbox**: Individual selection controls

## Notes

- Select automatically handles option filtering, grouping, and virtualization
- Custom CSS variables available for comprehensive theming
- Built-in support for complex option structures and custom rendering
- Optimized for both desktop and mobile interactions
- Compatible with form validation and state management libraries
- Supports both controlled and uncontrolled usage patterns
- Performance optimized with virtual scrolling and efficient filtering algorithms
