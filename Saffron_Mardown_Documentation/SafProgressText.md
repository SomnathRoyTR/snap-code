# SafProgressText

## Overview

SafProgressText is a text-based progress indicator component that displays progress information in readable text format. It provides flexible formatting options for showing completion status, progress descriptions, and time estimates with support for various display styles and interactive features.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | - | Current progress value |
| `max` | `number` | `100` | Maximum value for progress calculation |
| `format` | `'percentage' \| 'fraction' \| 'value' \| 'descriptive' \| (value: number, max: number) => string` | `'percentage'` | Format for progress display |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Text size variant |
| `variant` | `'default' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'default'` | Color variant based on progress status |
| `showLabel` | `boolean` | `false` | Display additional descriptive label |
| `label` | `string` | - | Custom label text |
| `showTime` | `boolean` | `false` | Display estimated time remaining |
| `timeRemaining` | `number` | - | Estimated seconds remaining |
| `precision` | `number` | `0` | Decimal places for percentage display |
| `interactive` | `boolean` | `false` | Makes progress text clickable |
| `loading` | `boolean` | `false` | Shows loading state with animated text |
| `className` | `string` | - | Additional CSS classes |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(event: MouseEvent) => void` | Fired when interactive progress text is clicked |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | - | Current progress value |
| `max` | `number` | `100` | Maximum value for progress calculation |
| `format` | `'percentage' \| 'fraction' \| 'value' \| 'descriptive'` | `'percentage'` | Format for progress display |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Text size variant |
| `variant` | `'default' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'default'` | Color variant based on progress status |
| `showLabel` | `boolean` | `false` | Display additional descriptive label |
| `label` | `string` | - | Custom label text |
| `showTime` | `boolean` | `false` | Display estimated time remaining |
| `timeRemaining` | `number` | - | Estimated seconds remaining |
| `precision` | `number` | `0` | Decimal places for percentage display |
| `interactive` | `boolean` | `false` | Makes progress text clickable |
| `loading` | `boolean` | `false` | Shows loading state with animated text |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `click` | `EventEmitter<MouseEvent>` | Fired when interactive progress text is clicked |

## Usage Examples

### Basic Progress Text

```typescript
// React
<SafProgressText value={75} />
<SafProgressText value={42} format="fraction" />
<SafProgressText value={150} max={200} format="value" />
<SafProgressText value={85.7} precision={1} />
```

```html
<!-- Angular -->
<saf-progress-text [value]="75"></saf-progress-text>
<saf-progress-text [value]="42" format="fraction"></saf-progress-text>
<saf-progress-text [value]="150" [max]="200" format="value"></saf-progress-text>
<saf-progress-text [value]="85.7" [precision]="1"></saf-progress-text>
```

### Progress with Labels

```typescript
// React
<SafProgressText value={67} showLabel label="Upload Progress" />
<SafProgressText value={45} showLabel label="Processing Files" format="fraction" />
<SafProgressText value={90} showLabel label="Installation Complete" variant="success" />
```

```html
<!-- Angular -->
<saf-progress-text [value]="67" [showLabel]="true" label="Upload Progress"></saf-progress-text>
<saf-progress-text [value]="45" [showLabel]="true" label="Processing Files" format="fraction"></saf-progress-text>
<saf-progress-text [value]="90" [showLabel]="true" label="Installation Complete" variant="success"></saf-progress-text>
```

### Progress with Time Estimates

```typescript
// React
<SafProgressText 
  value={35} 
  showTime 
  timeRemaining={120} 
  label="Download in progress"
  showLabel 
/>

<SafProgressText 
  value={78} 
  showTime 
  timeRemaining={45} 
  format="fraction"
/>
```

```html
<!-- Angular -->
<saf-progress-text 
  [value]="35" 
  [showTime]="true"
  [timeRemaining]="120" 
  label="Download in progress"
  [showLabel]="true"
></saf-progress-text>

<saf-progress-text 
  [value]="78" 
  [showTime]="true"
  [timeRemaining]="45" 
  format="fraction"
></saf-progress-text>
```

### Size Variants

```typescript
// React
<SafProgressText value={60} size="small" />
<SafProgressText value={60} size="medium" />
<SafProgressText value={60} size="large" />
```

```html
<!-- Angular -->
<saf-progress-text [value]="60" size="small"></saf-progress-text>
<saf-progress-text [value]="60" size="medium"></saf-progress-text>
<saf-progress-text [value]="60" size="large"></saf-progress-text>
```

### Status Variants

```typescript
// React
<SafProgressText value={100} variant="success" label="Completed" showLabel />
<SafProgressText value={75} variant="warning" label="Almost Done" showLabel />
<SafProgressText value={15} variant="error" label="Failed" showLabel />
<SafProgressText value={50} variant="neutral" label="In Progress" showLabel />
```

```html
<!-- Angular -->
<saf-progress-text [value]="100" variant="success" label="Completed" [showLabel]="true"></saf-progress-text>
<saf-progress-text [value]="75" variant="warning" label="Almost Done" [showLabel]="true"></saf-progress-text>
<saf-progress-text [value]="15" variant="error" label="Failed" [showLabel]="true"></saf-progress-text>
<saf-progress-text [value]="50" variant="neutral" label="In Progress" [showLabel]="true"></saf-progress-text>
```

### Custom Format Function

```typescript
// React
<SafProgressText 
  value={75} 
  format={(value, max) => `${value} of ${max} items processed`} 
/>

<SafProgressText 
  value={8} 
  max={10} 
  format={(value, max) => {
    const remaining = max - value;
    return `${remaining} steps remaining`;
  }} 
/>

<SafProgressText 
  value={150} 
  max={200} 
  format={(value, max) => {
    const percentage = Math.round((value / max) * 100);
    if (percentage < 50) return `Getting started (${percentage}%)`;
    if (percentage < 80) return `Making progress (${percentage}%)`;
    return `Almost there (${percentage}%)`;
  }} 
/>
```

### Loading States

```typescript
// React
<SafProgressText loading label="Initializing..." showLabel />
<SafProgressText loading label="Connecting to server..." showLabel />
<SafProgressText loading label="Processing request..." showLabel />
```

```html
<!-- Angular -->
<saf-progress-text [loading]="true" label="Initializing..." [showLabel]="true"></saf-progress-text>
<saf-progress-text [loading]="true" label="Connecting to server..." [showLabel]="true"></saf-progress-text>
<saf-progress-text [loading]="true" label="Processing request..." [showLabel]="true"></saf-progress-text>
```

### Interactive Progress Text

```typescript
// React
<SafProgressText 
  value={65} 
  interactive 
  onClick={() => showProgressDetails()}
  label="Click for details"
  showLabel
/>

<SafProgressText 
  value={100} 
  variant="success" 
  interactive 
  onClick={() => downloadResults()}
  label="Download ready"
  showLabel
/>
```

```html
<!-- Angular -->
<saf-progress-text 
  [value]="65" 
  [interactive]="true"
  (click)="showProgressDetails()"
  label="Click for details"
  [showLabel]="true"
></saf-progress-text>
```

### File Upload Progress

```typescript
// React
const FileUploadProgress = ({ file, progress, speed, timeRemaining }) => (
  <div className="upload-progress">
    <div className="file-info">
      <span className="filename">{file.name}</span>
      <SafProgressText 
        value={progress} 
        precision={1}
        variant={progress === 100 ? 'success' : 'default'}
      />
    </div>
    <div className="upload-details">
      <SafProgressText 
        value={progress} 
        format="fraction"
        max={file.size}
        showTime
        timeRemaining={timeRemaining}
        size="small"
      />
      <span className="upload-speed">{speed} MB/s</span>
    </div>
  </div>
);
```

### Task Progress Display

```typescript
// React
const TaskProgress = ({ tasks }) => {
  const completed = tasks.filter(task => task.completed).length;
  const total = tasks.length;
  
  return (
    <div className="task-progress">
      <h3>Project Progress</h3>
      <SafProgressText 
        value={completed} 
        max={total} 
        format="fraction"
        label="Tasks Completed"
        showLabel
        variant={completed === total ? 'success' : 'default'}
        size="large"
      />
      <SafProgressText 
        value={completed} 
        max={total} 
        precision={1}
        size="small"
      />
    </div>
  );
};
```

### Data Processing Progress

```typescript
// React
const DataProcessor = ({ processed, total, errors, processingRate }) => {
  const progress = (processed / total) * 100;
  const hasErrors = errors > 0;
  const timeRemaining = (total - processed) / processingRate;
  
  return (
    <div className="processing-status">
      <SafProgressText 
        value={processed} 
        max={total} 
        format={(value, max) => `${value.toLocaleString()} / ${max.toLocaleString()} records`}
        variant={hasErrors ? 'warning' : progress === 100 ? 'success' : 'default'}
        showTime
        timeRemaining={timeRemaining}
        showLabel
        label="Data Processing"
      />
      {hasErrors && (
        <SafProgressText 
          value={errors} 
          format={(value) => `${value} errors encountered`}
          variant="error"
          size="small"
          interactive
          onClick={() => showErrorDetails()}
        />
      )}
    </div>
  );
};
```

### Installation Progress

```typescript
// React
const InstallationProgress = ({ step, totalSteps, currentTask, progress }) => {
  const stepProgress = (step / totalSteps) * 100;
  
  return (
    <div className="installation-progress">
      <h2>Installation Progress</h2>
      <SafProgressText 
        value={step} 
        max={totalSteps} 
        format="fraction"
        label={currentTask}
        showLabel
        size="large"
      />
      <SafProgressText 
        value={stepProgress} 
        precision={0}
        variant={step === totalSteps ? 'success' : 'default'}
      />
      <SafProgressText 
        value={progress} 
        format={(value) => `${value}% of current step`}
        size="small"
        loading={progress === 0}
      />
    </div>
  );
};
```

### Goal Achievement Progress

```typescript
// React
const GoalProgress = ({ current, target, period }) => {
  const progress = (current / target) * 100;
  const isOverTarget = progress > 100;
  const isNearTarget = progress > 80;
  
  return (
    <div className="goal-progress">
      <SafProgressText 
        value={current} 
        max={target} 
        format={(value, max) => {
          if (value > max) return `${value.toLocaleString()} (${Math.round((value/max)*100)}% of target)`;
          return `${value.toLocaleString()} / ${max.toLocaleString()}`;
        }}
        variant={isOverTarget ? 'success' : isNearTarget ? 'warning' : 'default'}
        label={`${period} Goal Progress`}
        showLabel
        size="large"
        interactive
        onClick={() => showGoalDetails()}
      />
    </div>
  );
};
```

### Multi-Stage Progress

```typescript
// React
const MultiStageProgress = ({ stages, currentStage, currentProgress }) => (
  <div className="multi-stage-progress">
    {stages.map((stage, index) => {
      const isActive = index === currentStage;
      const isCompleted = index < currentStage;
      const progress = isCompleted ? 100 : isActive ? currentProgress : 0;
      
      return (
        <div key={stage.id} className={`stage ${isActive ? 'active' : ''} ${isCompleted ? 'completed' : ''}`}>
          <h4>{stage.name}</h4>
          <SafProgressText 
            value={progress} 
            precision={0}
            variant={isCompleted ? 'success' : isActive ? 'default' : 'neutral'}
            size="small"
            loading={isActive && progress === 0}
          />
          <SafProgressText 
            value={progress} 
            format={(value) => isCompleted ? 'Completed' : isActive ? 'In Progress' : 'Pending'}
            variant={isCompleted ? 'success' : isActive ? 'default' : 'neutral'}
            size="small"
          />
        </div>
      );
    })}
  </div>
);
```

## Best Practices

### Progress Communication
- **Clear Language**: Use descriptive labels that clearly communicate what's progressing
- **Appropriate Precision**: Show decimal places only when meaningful
- **Consistent Formatting**: Use consistent progress formats within similar contexts
- **Status Indication**: Use variants to indicate different progress states

### Time and Estimates
- **Realistic Estimates**: Provide time estimates only when reasonably accurate
- **Dynamic Updates**: Update time remaining as progress changes
- **Handle Unknowns**: Use loading states when progress duration is unknown
- **User Expectations**: Set appropriate expectations about completion time

### Visual Hierarchy
- **Size Appropriately**: Match text size to importance and context
- **Information Density**: Balance detail with readability
- **Color Meaning**: Use color variants consistently with their semantic meaning
- **Layout Consideration**: Position progress text appropriately within interfaces

### Interactive Design
- **Meaningful Actions**: Only make progress interactive when it provides value
- **Clear Affordances**: Indicate interactive progress text with appropriate styling
- **Feedback**: Provide clear feedback when interactive elements are used
- **Accessibility**: Ensure interactive elements are keyboard accessible

## Accessibility Considerations

- Uses semantic text elements with appropriate ARIA attributes
- Provides screen reader announcements for progress updates
- Maintains sufficient color contrast for all variants
- Supports keyboard navigation for interactive variants
- Includes proper labeling for screen reader context
- Respects user preferences for reduced motion in loading states

## Related Components

- **SafProgressBar**: Visual progress bar component
- **SafProgressRing**: Circular progress indicator
- **SafStatus**: Status indicator component
- **SafSpinner**: Simple loading indicator
- **SafLoader**: Full-page loading component
- **SafBadge**: Related component for counts and labels

## Notes

- SafProgressText automatically formats progress based on the specified format
- Custom format functions receive both current value and maximum for flexible display
- Loading states provide animated text to indicate ongoing processing
- Time remaining calculations can be provided externally for accuracy
- Interactive variants support keyboard navigation and proper focus management
- The component handles edge cases like values exceeding maximum gracefully
- Precision setting affects only percentage display format
- Variants can be used to indicate different progress states and outcomes
