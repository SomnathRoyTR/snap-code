# SafTooltip Component

## Overview

SafTooltip is a contextual help component that displays informative text when users hover over, focus on, or click trigger elements. It provides additional context, explanations, or instructions without cluttering the interface. SafTooltip supports multiple trigger methods, positioning options, rich content, and interactive behaviors for enhanced user experience.

## React API

### SafTooltip

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `content` | `string \| ReactNode` | Yes | - | Tooltip content to display |
| `children` | `ReactNode` | Yes | - | Trigger element that activates tooltip |
| `trigger` | `'hover' \| 'click' \| 'focus' \| 'manual'` | No | `'hover'` | How tooltip is triggered |
| `position` | `'top' \| 'bottom' \| 'left' \| 'right' \| 'auto'` | No | `'top'` | Tooltip positioning relative to trigger |
| `alignment` | `'start' \| 'center' \| 'end'` | No | `'center'` | Tooltip alignment on its axis |
| `delay` | `number \| { show: number, hide: number }` | No | `500` | Show/hide delay in milliseconds |
| `duration` | `number \| 'persistent'` | No | `'persistent'` | Auto-hide duration or persistent |
| `interactive` | `boolean` | No | `false` | Whether tooltip content is interactive |
| `disabled` | `boolean` | No | `false` | Whether tooltip is disabled |
| `arrow` | `boolean` | No | `true` | Whether to show pointing arrow |
| `maxWidth` | `string` | No | `'300px'` | Maximum width of tooltip |
| `offset` | `number` | No | `8` | Distance from trigger element |
| `zIndex` | `number` | No | `1000` | Z-index for tooltip positioning |
| `animation` | `'fade' \| 'slide' \| 'scale' \| 'none'` | No | `'fade'` | Tooltip animation type |
| `theme` | `'dark' \| 'light' \| 'custom'` | No | `'dark'` | Tooltip visual theme |
| `followCursor` | `boolean` | No | `false` | Whether tooltip follows mouse cursor |
| `boundary` | `Element \| string` | No | `'viewport'` | Boundary for tooltip positioning |
| `onShow` | `() => void` | No | - | Callback when tooltip shows |
| `onHide` | `() => void` | No | - | Callback when tooltip hides |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

## Angular API

### saf-tooltip

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[content]` | `string \| TemplateRef` | Yes | - | Tooltip content to display |
| `[trigger]` | `'hover' \| 'click' \| 'focus' \| 'manual'` | No | `'hover'` | How tooltip is triggered |
| `[position]` | `'top' \| 'bottom' \| 'left' \| 'right' \| 'auto'` | No | `'top'` | Tooltip positioning relative to trigger |
| `[alignment]` | `'start' \| 'center' \| 'end'` | No | `'center'` | Tooltip alignment on its axis |
| `[delay]` | `number \| { show: number, hide: number }` | No | `500` | Show/hide delay in milliseconds |
| `[duration]` | `number \| 'persistent'` | No | `'persistent'` | Auto-hide duration or persistent |
| `[interactive]` | `boolean` | No | `false` | Whether tooltip content is interactive |
| `[disabled]` | `boolean` | No | `false` | Whether tooltip is disabled |
| `[arrow]` | `boolean` | No | `true` | Whether to show pointing arrow |
| `[maxWidth]` | `string` | No | `'300px'` | Maximum width of tooltip |
| `[offset]` | `number` | No | `8` | Distance from trigger element |
| `[zIndex]` | `number` | No | `1000` | Z-index for tooltip positioning |
| `[animation]` | `'fade' \| 'slide' \| 'scale' \| 'none'` | No | `'fade'` | Tooltip animation type |
| `[theme]` | `'dark' \| 'light' \| 'custom'` | No | `'dark'` | Tooltip visual theme |
| `[followCursor]` | `boolean` | No | `false` | Whether tooltip follows mouse cursor |
| `[boundary]` | `Element \| string` | No | `'viewport'` | Boundary for tooltip positioning |
| `(show)` | `EventEmitter<void>` | No | - | Event when tooltip shows |
| `(hide)` | `EventEmitter<void>` | No | - | Event when tooltip hides |

### Directive Usage

```typescript
// Alternative directive usage
<button safTooltip="This is a tooltip" position="bottom">
  Hover me
</button>
```

## Usage Examples

### Basic Tooltips

#### React
```jsx
import { SafTooltip, SafButton, SafIcon } from '@saffron/react';

const BasicTooltipExample = () => {
  return (
    <div className="tooltip-demo">
      <h2>Basic Tooltips</h2>
      
      <div className="tooltip-examples">
        {/* Simple text tooltip */}
        <SafTooltip content="This button saves your current work">
          <SafButton>
            <SafIcon name="save" />
            Save
          </SafButton>
        </SafTooltip>

        {/* Tooltip with different positions */}
        <SafTooltip content="Top positioned tooltip" position="top">
          <SafButton variant="outline">Top</SafButton>
        </SafTooltip>

        <SafTooltip content="Bottom positioned tooltip" position="bottom">
          <SafButton variant="outline">Bottom</SafButton>
        </SafTooltip>

        <SafTooltip content="Left positioned tooltip" position="left">
          <SafButton variant="outline">Left</SafButton>
        </SafTooltip>

        <SafTooltip content="Right positioned tooltip" position="right">
          <SafButton variant="outline">Right</SafButton>
        </SafTooltip>

        {/* Tooltip with custom delay */}
        <SafTooltip 
          content="This tooltip appears after 1 second"
          delay={1000}
        >
          <SafButton variant="secondary">Delayed Tooltip</SafButton>
        </SafTooltip>

        {/* Disabled tooltip */}
        <SafTooltip 
          content="This tooltip won't show"
          disabled={true}
        >
          <SafButton variant="ghost">Disabled Tooltip</SafButton>
        </SafTooltip>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// basic-tooltip.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-tooltip',
  template: `
    <div class="tooltip-demo">
      <h2>Basic Tooltips</h2>
      
      <div class="tooltip-examples">
        <!-- Simple text tooltip -->
        <saf-tooltip content="This button saves your current work">
          <saf-button>
            <saf-icon name="save"></saf-icon>
            Save
          </saf-button>
        </saf-tooltip>

        <!-- Tooltip with different positions -->
        <saf-tooltip content="Top positioned tooltip" position="top">
          <saf-button variant="outline">Top</saf-button>
        </saf-tooltip>

        <saf-tooltip content="Bottom positioned tooltip" position="bottom">
          <saf-button variant="outline">Bottom</saf-button>
        </saf-tooltip>

        <saf-tooltip content="Left positioned tooltip" position="left">
          <saf-button variant="outline">Left</saf-button>
        </saf-tooltip>

        <saf-tooltip content="Right positioned tooltip" position="right">
          <saf-button variant="outline">Right</saf-button>
        </saf-tooltip>

        <!-- Tooltip with custom delay -->
        <saf-tooltip 
          content="This tooltip appears after 1 second"
          [delay]="1000">
          <saf-button variant="secondary">Delayed Tooltip</saf-button>
        </saf-tooltip>

        <!-- Disabled tooltip -->
        <saf-tooltip 
          content="This tooltip won't show"
          [disabled]="true">
          <saf-button variant="ghost">Disabled Tooltip</saf-button>
        </saf-tooltip>

        <!-- Directive usage -->
        <saf-button 
          safTooltip="Simple directive tooltip" 
          position="bottom">
          Directive Tooltip
        </saf-button>
      </div>
    </div>
  `
})
export class BasicTooltipComponent {}
```

### Interactive Tooltips with Rich Content

#### React
```jsx
import { SafTooltip, SafButton, SafIcon, SafCard } from '@saffron/react';

const InteractiveTooltipExample = () => {
  const handleTooltipAction = (action) => {
    console.log('Tooltip action:', action);
  };

  const richTooltipContent = (
    <div className="rich-tooltip-content">
      <div className="tooltip-header">
        <SafIcon name="info-circle" />
        <strong>User Profile</strong>
      </div>
      <div className="tooltip-body">
        <p><strong>John Doe</strong></p>
        <p>Senior Developer</p>
        <p>Last active: 2 hours ago</p>
      </div>
      <div className="tooltip-actions">
        <SafButton 
          size="small" 
          variant="primary"
          onClick={() => handleTooltipAction('view')}
        >
          View Profile
        </SafButton>
        <SafButton 
          size="small" 
          variant="ghost"
          onClick={() => handleTooltipAction('message')}
        >
          Send Message
        </SafButton>
      </div>
    </div>
  );

  const helpTooltipContent = (
    <div className="help-tooltip-content">
      <h4>Password Requirements</h4>
      <ul>
        <li>At least 8 characters long</li>
        <li>Include uppercase and lowercase letters</li>
        <li>Include at least one number</li>
        <li>Include at least one special character</li>
      </ul>
    </div>
  );

  return (
    <div className="interactive-tooltip-demo">
      <h2>Interactive Tooltips</h2>
      
      <div className="tooltip-examples">
        {/* Rich content tooltip */}
        <SafTooltip
          content={richTooltipContent}
          trigger="click"
          interactive={true}
          position="bottom"
          maxWidth="250px"
          theme="light"
        >
          <SafButton variant="outline">
            <SafIcon name="user" />
            User Info
          </SafButton>
        </SafTooltip>

        {/* Help tooltip */}
        <SafTooltip
          content={helpTooltipContent}
          trigger="click"
          interactive={true}
          position="right"
          maxWidth="300px"
          arrow={true}
        >
          <SafIcon 
            name="help-circle" 
            className="help-icon clickable"
            size="small"
          />
        </SafTooltip>

        {/* Auto-hiding tooltip */}
        <SafTooltip
          content="This tooltip disappears after 3 seconds"
          duration={3000}
          position="top"
          animation="slide"
        >
          <SafButton variant="success">Auto-hide Tooltip</SafButton>
        </SafTooltip>

        {/* Following cursor tooltip */}
        <SafTooltip
          content="This tooltip follows your mouse"
          followCursor={true}
          delay={{ show: 200, hide: 100 }}
        >
          <div className="cursor-follow-area">
            <p>Hover anywhere in this area</p>
          </div>
        </SafTooltip>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// interactive-tooltip.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-interactive-tooltip',
  template: `
    <div class="interactive-tooltip-demo">
      <h2>Interactive Tooltips</h2>
      
      <div class="tooltip-examples">
        <!-- Rich content tooltip -->
        <saf-tooltip
          [content]="richTooltipTemplate"
          trigger="click"
          [interactive]="true"
          position="bottom"
          maxWidth="250px"
          theme="light">
          <saf-button variant="outline">
            <saf-icon name="user"></saf-icon>
            User Info
          </saf-button>
        </saf-tooltip>

        <!-- Help tooltip -->
        <saf-tooltip
          [content]="helpTooltipTemplate"
          trigger="click"
          [interactive]="true"
          position="right"
          maxWidth="300px"
          [arrow]="true">
          <saf-icon 
            name="help-circle" 
            class="help-icon clickable"
            size="small">
          </saf-icon>
        </saf-tooltip>

        <!-- Auto-hiding tooltip -->
        <saf-tooltip
          content="This tooltip disappears after 3 seconds"
          [duration]="3000"
          position="top"
          animation="slide">
          <saf-button variant="success">Auto-hide Tooltip</saf-button>
        </saf-tooltip>

        <!-- Following cursor tooltip -->
        <saf-tooltip
          content="This tooltip follows your mouse"
          [followCursor]="true"
          [delay]="{ show: 200, hide: 100 }">
          <div class="cursor-follow-area">
            <p>Hover anywhere in this area</p>
          </div>
        </saf-tooltip>
      </div>
    </div>

    <!-- Rich tooltip template -->
    <ng-template #richTooltipTemplate>
      <div class="rich-tooltip-content">
        <div class="tooltip-header">
          <saf-icon name="info-circle"></saf-icon>
          <strong>User Profile</strong>
        </div>
        <div class="tooltip-body">
          <p><strong>John Doe</strong></p>
          <p>Senior Developer</p>
          <p>Last active: 2 hours ago</p>
        </div>
        <div class="tooltip-actions">
          <saf-button 
            size="small" 
            variant="primary"
            (click)="handleTooltipAction('view')">
            View Profile
          </saf-button>
          <saf-button 
            size="small" 
            variant="ghost"
            (click)="handleTooltipAction('message')">
            Send Message
          </saf-button>
        </div>
      </div>
    </ng-template>

    <!-- Help tooltip template -->
    <ng-template #helpTooltipTemplate>
      <div class="help-tooltip-content">
        <h4>Password Requirements</h4>
        <ul>
          <li>At least 8 characters long</li>
          <li>Include uppercase and lowercase letters</li>
          <li>Include at least one number</li>
          <li>Include at least one special character</li>
        </ul>
      </div>
    </ng-template>
  `
})
export class InteractiveTooltipComponent {
  handleTooltipAction(action: string) {
    console.log('Tooltip action:', action);
  }
}
```

### Form Field Tooltips

#### React
```jsx
import { SafTooltip, SafTextInput, SafIcon, SafButton } from '@saffron/react';
import { useState } from 'react';

const FormTooltipExample = () => {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: ''
  });

  const [errors, setErrors] = useState({});

  const validateField = (name, value) => {
    let error = '';
    
    switch (name) {
      case 'username':
        if (value.length < 3) error = 'Username must be at least 3 characters';
        break;
      case 'email':
        if (!/\S+@\S+\.\S+/.test(value)) error = 'Please enter a valid email';
        break;
      case 'password':
        if (value.length < 8) error = 'Password must be at least 8 characters';
        break;
    }
    
    setErrors(prev => ({ ...prev, [name]: error }));
  };

  const handleInputChange = (name, value) => {
    setFormData(prev => ({ ...prev, [name]: value }));
    validateField(name, value);
  };

  return (
    <div className="form-tooltip-demo">
      <h2>Form Field Tooltips</h2>
      
      <form className="tooltip-form">
        <div className="form-field">
          <label htmlFor="username">
            Username
            <SafTooltip
              content="Choose a unique username that will be visible to other users"
              position="right"
              delay={300}
            >
              <SafIcon name="help-circle" className="field-help-icon" />
            </SafTooltip>
          </label>
          <SafTextInput
            id="username"
            value={formData.username}
            onChange={(e) => handleInputChange('username', e.target.value)}
            error={errors.username}
            placeholder="Enter username"
          />
        </div>

        <div className="form-field">
          <label htmlFor="email">
            Email Address
            <SafTooltip
              content="We'll use this email for account notifications and password recovery"
              position="right"
              maxWidth="200px"
            >
              <SafIcon name="help-circle" className="field-help-icon" />
            </SafTooltip>
          </label>
          <SafTextInput
            id="email"
            type="email"
            value={formData.email}
            onChange={(e) => handleInputChange('email', e.target.value)}
            error={errors.email}
            placeholder="Enter email address"
          />
        </div>

        <div className="form-field">
          <label htmlFor="password">
            Password
            <SafTooltip
              content={(
                <div className="password-requirements">
                  <p><strong>Password must include:</strong></p>
                  <ul>
                    <li>At least 8 characters</li>
                    <li>Uppercase and lowercase letters</li>
                    <li>At least one number</li>
                    <li>At least one special character</li>
                  </ul>
                </div>
              )}
              position="right"
              interactive={true}
              maxWidth="250px"
            >
              <SafIcon name="help-circle" className="field-help-icon" />
            </SafTooltip>
          </label>
          <SafTextInput
            id="password"
            type="password"
            value={formData.password}
            onChange={(e) => handleInputChange('password', e.target.value)}
            error={errors.password}
            placeholder="Enter password"
          />
        </div>

        <SafTooltip
          content={
            Object.values(errors).some(error => error) 
              ? "Please fix the errors above before submitting"
              : "All fields are valid. Click to submit the form"
          }
          position="top"
          disabled={!Object.values(errors).some(error => error)}
        >
          <SafButton 
            type="submit" 
            variant="primary"
            disabled={Object.values(errors).some(error => error)}
          >
            Create Account
          </SafButton>
        </SafTooltip>
      </form>
    </div>
  );
};
```

#### Angular
```typescript
// form-tooltip.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-form-tooltip',
  template: `
    <div class="form-tooltip-demo">
      <h2>Form Field Tooltips</h2>
      
      <form class="tooltip-form" #form="ngForm">
        <div class="form-field">
          <label for="username">
            Username
            <saf-tooltip
              content="Choose a unique username that will be visible to other users"
              position="right"
              [delay]="300">
              <saf-icon name="help-circle" class="field-help-icon"></saf-icon>
            </saf-tooltip>
          </label>
          <saf-text-input
            id="username"
            [(ngModel)]="formData.username"
            name="username"
            #username="ngModel"
            [error]="getFieldError('username')"
            placeholder="Enter username"
            (blur)="validateField('username', formData.username)">
          </saf-text-input>
        </div>

        <div class="form-field">
          <label for="email">
            Email Address
            <saf-tooltip
              content="We'll use this email for account notifications and password recovery"
              position="right"
              maxWidth="200px">
              <saf-icon name="help-circle" class="field-help-icon"></saf-icon>
            </saf-tooltip>
          </label>
          <saf-text-input
            id="email"
            type="email"
            [(ngModel)]="formData.email"
            name="email"
            #email="ngModel"
            [error]="getFieldError('email')"
            placeholder="Enter email address"
            (blur)="validateField('email', formData.email)">
          </saf-text-input>
        </div>

        <div class="form-field">
          <label for="password">
            Password
            <saf-tooltip
              [content]="passwordRequirementsTemplate"
              position="right"
              [interactive]="true"
              maxWidth="250px">
              <saf-icon name="help-circle" class="field-help-icon"></saf-icon>
            </saf-tooltip>
          </label>
          <saf-text-input
            id="password"
            type="password"
            [(ngModel)]="formData.password"
            name="password"
            #password="ngModel"
            [error]="getFieldError('password')"
            placeholder="Enter password"
            (blur)="validateField('password', formData.password)">
          </saf-text-input>
        </div>

        <saf-tooltip
          [content]="hasErrors() ? 'Please fix the errors above before submitting' : 'All fields are valid. Click to submit the form'"
          position="top"
          [disabled]="!hasErrors()">
          <saf-button 
            type="submit" 
            variant="primary"
            [disabled]="hasErrors() || form.invalid">
            Create Account
          </saf-button>
        </saf-tooltip>
      </form>
    </div>

    <!-- Password requirements template -->
    <ng-template #passwordRequirementsTemplate>
      <div class="password-requirements">
        <p><strong>Password must include:</strong></p>
        <ul>
          <li>At least 8 characters</li>
          <li>Uppercase and lowercase letters</li>
          <li>At least one number</li>
          <li>At least one special character</li>
        </ul>
      </div>
    </ng-template>
  `
})
export class FormTooltipComponent {
  formData = {
    username: '',
    email: '',
    password: ''
  };

  errors: { [key: string]: string } = {};

  validateField(name: string, value: string) {
    let error = '';
    
    switch (name) {
      case 'username':
        if (value.length < 3) error = 'Username must be at least 3 characters';
        break;
      case 'email':
        if (!/\S+@\S+\.\S+/.test(value)) error = 'Please enter a valid email';
        break;
      case 'password':
        if (value.length < 8) error = 'Password must be at least 8 characters';
        break;
    }
    
    this.errors[name] = error;
  }

  getFieldError(name: string): string {
    return this.errors[name] || '';
  }

  hasErrors(): boolean {
    return Object.values(this.errors).some(error => error);
  }
}
```

### Data Visualization Tooltips

#### React
```jsx
import { SafTooltip, SafCard, SafBadge } from '@saffron/react';
import { useState } from 'react';

const DataVisualizationTooltipExample = () => {
  const chartData = [
    { quarter: 'Q1', value: 85, target: 90, trend: 'up', details: { revenue: '$2.1M', customers: '1,250' } },
    { quarter: 'Q2', value: 92, target: 90, trend: 'up', details: { revenue: '$2.4M', customers: '1,380' } },
    { quarter: 'Q3', value: 78, target: 90, trend: 'down', details: { revenue: '$1.9M', customers: '1,120' } },
    { quarter: 'Q4', value: 95, target: 90, trend: 'up', details: { revenue: '$2.8M', customers: '1,540' } }
  ];

  const getTooltipContent = (dataPoint) => (
    <div className="chart-tooltip-content">
      <div className="tooltip-title">
        <strong>{dataPoint.quarter} Performance</strong>
        <SafBadge 
          variant={dataPoint.trend === 'up' ? 'success' : 'warning'}
          size="small"
        >
          {dataPoint.trend === 'up' ? '↗' : '↘'} {dataPoint.trend}
        </SafBadge>
      </div>
      <div className="tooltip-metrics">
        <div className="metric">
          <span className="label">Actual:</span>
          <span className="value">{dataPoint.value}%</span>
        </div>
        <div className="metric">
          <span className="label">Target:</span>
          <span className="value">{dataPoint.target}%</span>
        </div>
        <div className="metric">
          <span className="label">Revenue:</span>
          <span className="value">{dataPoint.details.revenue}</span>
        </div>
        <div className="metric">
          <span className="label">Customers:</span>
          <span className="value">{dataPoint.details.customers}</span>
        </div>
      </div>
      <div className="tooltip-variance">
        <span className={`variance ${dataPoint.value >= dataPoint.target ? 'positive' : 'negative'}`}>
          {dataPoint.value >= dataPoint.target ? '+' : ''}
          {dataPoint.value - dataPoint.target} vs target
        </span>
      </div>
    </div>
  );

  return (
    <SafCard className="data-visualization-demo">
      <SafCard.Header>
        <h2>Quarterly Performance Dashboard</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="chart-container">
          <div className="chart-bars">
            {chartData.map((dataPoint, index) => (
              <SafTooltip
                key={dataPoint.quarter}
                content={getTooltipContent(dataPoint)}
                position="top"
                interactive={true}
                maxWidth="280px"
                delay={200}
                theme="light"
              >
                <div className="chart-bar-container">
                  <div 
                    className={`chart-bar ${dataPoint.trend}`}
                    style={{ 
                      height: `${dataPoint.value * 2}px`,
                      backgroundColor: dataPoint.value >= dataPoint.target ? '#4CAF50' : '#FF9800'
                    }}
                  />
                  <div className="chart-label">{dataPoint.quarter}</div>
                </div>
              </SafTooltip>
            ))}
          </div>
        </div>

        <div className="legend">
          <SafTooltip content="Actual performance vs quarterly targets">
            <div className="legend-item">
              <div className="legend-color success"></div>
              <span>Met Target</span>
            </div>
          </SafTooltip>
          <SafTooltip content="Performance below quarterly targets">
            <div className="legend-item">
              <div className="legend-color warning"></div>
              <span>Below Target</span>
            </div>
          </SafTooltip>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// data-visualization-tooltip.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-data-visualization-tooltip',
  template: `
    <saf-card class="data-visualization-demo">
      <saf-card-header>
        <h2>Quarterly Performance Dashboard</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="chart-container">
          <div class="chart-bars">
            <div 
              *ngFor="let dataPoint of chartData"
              class="chart-bar-container">
              <saf-tooltip
                [content]="getTooltipTemplate(dataPoint)"
                position="top"
                [interactive]="true"
                maxWidth="280px"
                [delay]="200"
                theme="light">
                <div 
                  class="chart-bar"
                  [class]="dataPoint.trend"
                  [style.height.px]="dataPoint.value * 2"
                  [style.background-color]="dataPoint.value >= dataPoint.target ? '#4CAF50' : '#FF9800'">
                </div>
              </saf-tooltip>
              <div class="chart-label">{{ dataPoint.quarter }}</div>
            </div>
          </div>
        </div>

        <div class="legend">
          <saf-tooltip content="Actual performance vs quarterly targets">
            <div class="legend-item">
              <div class="legend-color success"></div>
              <span>Met Target</span>
            </div>
          </saf-tooltip>
          <saf-tooltip content="Performance below quarterly targets">
            <div class="legend-item">
              <div class="legend-color warning"></div>
              <span>Below Target</span>
            </div>
          </saf-tooltip>
        </div>
      </saf-card-content>
    </saf-card>

    <!-- Tooltip template -->
    <ng-template #chartTooltipTemplate let-dataPoint="dataPoint">
      <div class="chart-tooltip-content">
        <div class="tooltip-title">
          <strong>{{ dataPoint.quarter }} Performance</strong>
          <saf-badge 
            [variant]="dataPoint.trend === 'up' ? 'success' : 'warning'"
            size="small">
            {{ dataPoint.trend === 'up' ? '↗' : '↘' }} {{ dataPoint.trend }}
          </saf-badge>
        </div>
        <div class="tooltip-metrics">
          <div class="metric">
            <span class="label">Actual:</span>
            <span class="value">{{ dataPoint.value }}%</span>
          </div>
          <div class="metric">
            <span class="label">Target:</span>
            <span class="value">{{ dataPoint.target }}%</span>
          </div>
          <div class="metric">
            <span class="label">Revenue:</span>
            <span class="value">{{ dataPoint.details.revenue }}</span>
          </div>
          <div class="metric">
            <span class="label">Customers:</span>
            <span class="value">{{ dataPoint.details.customers }}</span>
          </div>
        </div>
        <div class="tooltip-variance">
          <span 
            class="variance"
            [class.positive]="dataPoint.value >= dataPoint.target"
            [class.negative]="dataPoint.value < dataPoint.target">
            {{ dataPoint.value >= dataPoint.target ? '+' : '' }}{{ dataPoint.value - dataPoint.target }} vs target
          </span>
        </div>
      </div>
    </ng-template>
  `
})
export class DataVisualizationTooltipComponent {
  chartData = [
    { quarter: 'Q1', value: 85, target: 90, trend: 'up', details: { revenue: '$2.1M', customers: '1,250' } },
    { quarter: 'Q2', value: 92, target: 90, trend: 'up', details: { revenue: '$2.4M', customers: '1,380' } },
    { quarter: 'Q3', value: 78, target: 90, trend: 'down', details: { revenue: '$1.9M', customers: '1,120' } },
    { quarter: 'Q4', value: 95, target: 90, trend: 'up', details: { revenue: '$2.8M', customers: '1,540' } }
  ];

  getTooltipTemplate(dataPoint: any) {
    // Return template reference with context
    return this.chartTooltipTemplate;
  }
}
```

## Best Practices

1. **Content Strategy**
   - Keep tooltip content concise and informative
   - Use tooltips for non-essential, helpful information
   - Avoid repeating information already visible on screen

2. **Positioning and Timing**
   - Use auto positioning for responsive layouts
   - Set appropriate delays to prevent accidental triggers
   - Position tooltips to avoid covering important content

3. **Accessibility**
   - Ensure tooltips work with keyboard navigation
   - Provide alternative ways to access tooltip information
   - Use appropriate ARIA attributes for screen readers

4. **Interactive Content**
   - Use interactive tooltips sparingly for rich content
   - Ensure interactive elements are accessible
   - Provide clear ways to dismiss interactive tooltips

5. **Performance**
   - Lazy load complex tooltip content
   - Limit the number of simultaneous tooltips
   - Use debouncing for frequently triggered tooltips

## Accessibility Considerations

1. **ARIA Support**
   - Use `role="tooltip"` for tooltip content
   - Implement `aria-describedby` linking trigger to tooltip
   - Provide `aria-expanded` for interactive tooltips

2. **Keyboard Navigation**
   - Support focus trigger for keyboard accessibility
   - Enable Escape key to dismiss tooltips
   - Ensure interactive content is keyboard navigable

3. **Screen Reader Compatibility**
   - Announce tooltip content when activated
   - Provide alternative access methods for critical information
   - Use semantic markup for structured content

4. **Visual Accessibility**
   - Ensure sufficient contrast for tooltip text
   - Provide clear visual indicators for interactive triggers
   - Support high contrast and reduced motion preferences

## Related Components

- **SafPopover**: Larger overlay content with advanced positioning
- **SafModal**: Full overlay for complex interactions
- **SafIcon**: Common tooltip triggers for help information
- **SafButton**: Interactive tooltip triggers
- **SafCard**: Container for rich tooltip content

## Notes

- Tooltips automatically handle viewport boundary detection
- Custom CSS variables available for theming tooltip appearance
- Built-in support for RTL (right-to-left) layouts
- Tooltip positioning uses collision detection for optimal placement
- Performance optimized with virtual positioning and lazy rendering
- Compatible with touch devices with appropriate touch handling
- Supports nested tooltips with proper z-index management
