# SafProgressRing

## Overview

SafProgressRing is a circular progress indicator component that displays progress as a ring/donut chart. It provides visual feedback for loading states, task completion, and goal achievement with customizable appearance, sizing, and content options including text labels and interactive features.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | - | Progress value (0-100) |
| `max` | `number` | `100` | Maximum value for progress calculation |
| `size` | `'small' \| 'medium' \| 'large' \| number` | `'medium'` | Size variant or custom pixel size |
| `thickness` | `'thin' \| 'medium' \| 'thick' \| number` | `'medium'` | Ring thickness variant or custom pixel width |
| `variant` | `'primary' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'primary'` | Color variant |
| `appearance` | `'filled' \| 'gradient'` | `'filled'` | Visual style of progress ring |
| `showValue` | `boolean` | `false` | Display progress value in center |
| `valueFormat` | `'percentage' \| 'fraction' \| 'value' \| (value: number, max: number) => string` | `'percentage'` | Format for displayed value |
| `label` | `string` | - | Accessible label for screen readers |
| `indeterminate` | `boolean` | `false` | Shows spinning animation for unknown progress |
| `interactive` | `boolean` | `false` | Makes progress ring clickable |
| `disabled` | `boolean` | `false` | Disables interaction and applies disabled styling |
| `className` | `string` | - | Additional CSS classes |
| `children` | `ReactNode` | - | Custom content to display in center |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onClick` | `(event: MouseEvent) => void` | Fired when interactive progress ring is clicked |
| `onAnimationComplete` | `() => void` | Fired when progress animation completes |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number` | - | Progress value (0-100) |
| `max` | `number` | `100` | Maximum value for progress calculation |
| `size` | `'small' \| 'medium' \| 'large' \| number` | `'medium'` | Size variant or custom pixel size |
| `thickness` | `'thin' \| 'medium' \| 'thick' \| number` | `'medium'` | Ring thickness variant or custom pixel width |
| `variant` | `'primary' \| 'success' \| 'warning' \| 'error' \| 'neutral'` | `'primary'` | Color variant |
| `appearance` | `'filled' \| 'gradient'` | `'filled'` | Visual style of progress ring |
| `showValue` | `boolean` | `false` | Display progress value in center |
| `valueFormat` | `'percentage' \| 'fraction' \| 'value'` | `'percentage'` | Format for displayed value |
| `label` | `string` | - | Accessible label for screen readers |
| `indeterminate` | `boolean` | `false` | Shows spinning animation for unknown progress |
| `interactive` | `boolean` | `false` | Makes progress ring clickable |
| `disabled` | `boolean` | `false` | Disables interaction and applies disabled styling |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `click` | `EventEmitter<MouseEvent>` | Fired when interactive progress ring is clicked |
| `animationComplete` | `EventEmitter<void>` | Fired when progress animation completes |

## Usage Examples

### Basic Progress Ring

```typescript
// React
<SafProgressRing value={75} />
<SafProgressRing value={50} variant="success" />
<SafProgressRing value={25} variant="warning" />
<SafProgressRing value={10} variant="error" />
```

```html
<!-- Angular -->
<saf-progress-ring [value]="75"></saf-progress-ring>
<saf-progress-ring [value]="50" variant="success"></saf-progress-ring>
<saf-progress-ring [value]="25" variant="warning"></saf-progress-ring>
<saf-progress-ring [value]="10" variant="error"></saf-progress-ring>
```

### Progress Ring with Value Display

```typescript
// React
<SafProgressRing value={85} showValue />
<SafProgressRing value={42} showValue valueFormat="fraction" />
<SafProgressRing value={150} max={200} showValue valueFormat="value" />
<SafProgressRing 
  value={75} 
  showValue 
  valueFormat={(value, max) => `${value}/${max} tasks`} 
/>
```

```html
<!-- Angular -->
<saf-progress-ring [value]="85" [showValue]="true"></saf-progress-ring>
<saf-progress-ring [value]="42" [showValue]="true" valueFormat="fraction"></saf-progress-ring>
<saf-progress-ring [value]="150" [max]="200" [showValue]="true" valueFormat="value"></saf-progress-ring>
```

### Size Variants

```typescript
// React
<SafProgressRing value={60} size="small" />
<SafProgressRing value={60} size="medium" />
<SafProgressRing value={60} size="large" />
<SafProgressRing value={60} size={120} /> {/* Custom pixel size */}
```

```html
<!-- Angular -->
<saf-progress-ring [value]="60" size="small"></saf-progress-ring>
<saf-progress-ring [value]="60" size="medium"></saf-progress-ring>
<saf-progress-ring [value]="60" size="large"></saf-progress-ring>
<saf-progress-ring [value]="60" [size]="120"></saf-progress-ring>
```

### Ring Thickness Options

```typescript
// React
<SafProgressRing value={70} thickness="thin" />
<SafProgressRing value={70} thickness="medium" />
<SafProgressRing value={70} thickness="thick" />
<SafProgressRing value={70} thickness={8} /> {/* Custom pixel thickness */}
```

```html
<!-- Angular -->
<saf-progress-ring [value]="70" thickness="thin"></saf-progress-ring>
<saf-progress-ring [value]="70" thickness="medium"></saf-progress-ring>
<saf-progress-ring [value]="70" thickness="thick"></saf-progress-ring>
<saf-progress-ring [value]="70" [thickness]="8"></saf-progress-ring>
```

### Indeterminate Loading

```typescript
// React
<SafProgressRing indeterminate />
<SafProgressRing indeterminate variant="primary" size="large" />
<SafProgressRing indeterminate thickness="thin">
  Loading...
</SafProgressRing>
```

```html
<!-- Angular -->
<saf-progress-ring [indeterminate]="true"></saf-progress-ring>
<saf-progress-ring [indeterminate]="true" variant="primary" size="large"></saf-progress-ring>
<saf-progress-ring [indeterminate]="true" thickness="thin">
  Loading...
</saf-progress-ring>
```

### Custom Center Content

```typescript
// React
<SafProgressRing value={80} size="large">
  <SafIcon name="check" size="medium" />
</SafProgressRing>

<SafProgressRing value={45} size="large">
  <div style={{ textAlign: 'center' }}>
    <div style={{ fontSize: '24px', fontWeight: 'bold' }}>45%</div>
    <div style={{ fontSize: '12px', color: 'gray' }}>Complete</div>
  </div>
</SafProgressRing>

<SafProgressRing value={90} size="large" variant="success">
  <SafAvatar name="John Doe" size="medium" />
</SafProgressRing>
```

```html
<!-- Angular -->
<saf-progress-ring [value]="80" size="large">
  <saf-icon name="check" size="medium"></saf-icon>
</saf-progress-ring>

<saf-progress-ring [value]="45" size="large">
  <div style="text-align: center;">
    <div style="font-size: 24px; font-weight: bold;">45%</div>
    <div style="font-size: 12px; color: gray;">Complete</div>
  </div>
</saf-progress-ring>
```

### Interactive Progress Rings

```typescript
// React
<SafProgressRing 
  value={65} 
  interactive 
  onClick={() => showProgressDetails()}
  showValue
>
  Click for Details
</SafProgressRing>

<SafProgressRing 
  value={100} 
  variant="success" 
  interactive 
  onClick={() => downloadResults()}
>
  <SafIcon name="download" />
</SafProgressRing>
```

```html
<!-- Angular -->
<saf-progress-ring 
  [value]="65" 
  [interactive]="true"
  (click)="showProgressDetails()"
  [showValue]="true"
>
  Click for Details
</saf-progress-ring>
```

### Progress Ring in Cards

```typescript
// React
<SafCard>
  <SafCardContent>
    <div style={{ display: 'flex', alignItems: 'center', gap: '16px' }}>
      <SafProgressRing value={78} variant="success" />
      <div>
        <h3>Project Alpha</h3>
        <p>78% Complete - On Track</p>
        <SafButton variant="text" size="small">View Details</SafButton>
      </div>
    </div>
  </SafCardContent>
</SafCard>

<SafCard>
  <SafCardContent style={{ textAlign: 'center' }}>
    <SafProgressRing value={92} size="large" showValue>
      <div>
        <SafIcon name="trophy" size="large" color="gold" />
      </div>
    </SafProgressRing>
    <h3>Goal Achievement</h3>
    <p>92% of annual target reached</p>
  </SafCardContent>
</SafCard>
```

### Dashboard Progress Indicators

```typescript
// React
const DashboardMetrics = () => {
  const metrics = [
    { label: 'CPU Usage', value: 45, variant: 'primary' },
    { label: 'Memory', value: 78, variant: 'warning' },
    { label: 'Storage', value: 92, variant: 'error' },
    { label: 'Network', value: 23, variant: 'success' }
  ];

  return (
    <div style={{ display: 'grid', gridTemplateColumns: 'repeat(4, 1fr)', gap: '16px' }}>
      {metrics.map(metric => (
        <div key={metric.label} style={{ textAlign: 'center' }}>
          <SafProgressRing 
            value={metric.value} 
            variant={metric.variant}
            showValue
            size="large"
          />
          <h4>{metric.label}</h4>
        </div>
      ))}
    </div>
  );
};
```

### Multi-Step Process Progress

```typescript
// React
<SafProgressRing value={33} max={3} showValue valueFormat="fraction">
  <div style={{ textAlign: 'center' }}>
    <div style={{ fontSize: '16px', fontWeight: 'bold' }}>Step 1</div>
    <div style={{ fontSize: '12px' }}>of 3</div>
  </div>
</SafProgressRing>

<SafProgressRing value={66} max={3} showValue valueFormat="fraction">
  <div style={{ textAlign: 'center' }}>
    <div style={{ fontSize: '16px', fontWeight: 'bold' }}>Step 2</div>
    <div style={{ fontSize: '12px' }}>of 3</div>
  </div>
</SafProgressRing>

<SafProgressRing value={100} max={3} variant="success" showValue>
  <SafIcon name="check" size="large" />
</SafProgressRing>
```

### Animated Progress Updates

```typescript
// React
const [progress, setProgress] = useState(0);

useEffect(() => {
  const interval = setInterval(() => {
    setProgress(prev => {
      if (prev >= 100) {
        clearInterval(interval);
        return 100;
      }
      return prev + 1;
    });
  }, 50);

  return () => clearInterval(interval);
}, []);

<SafProgressRing 
  value={progress} 
  showValue 
  onAnimationComplete={() => console.log('Animation complete!')}
>
  {progress === 100 && <SafIcon name="check" color="success" />}
</SafProgressRing>
```

### File Upload Progress

```typescript
// React
const FileUploadProgress = ({ file, progress, status }) => (
  <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
    <SafProgressRing 
      value={progress} 
      size="small"
      variant={status === 'error' ? 'error' : status === 'complete' ? 'success' : 'primary'}
      indeterminate={status === 'processing'}
    />
    <div style={{ flex: 1 }}>
      <div style={{ fontWeight: 'bold' }}>{file.name}</div>
      <div style={{ fontSize: '12px', color: 'gray' }}>
        {status === 'uploading' && `${progress}% uploaded`}
        {status === 'processing' && 'Processing...'}
        {status === 'complete' && 'Upload complete'}
        {status === 'error' && 'Upload failed'}
      </div>
    </div>
    {status === 'error' && (
      <SafButton variant="text" size="small">Retry</SafButton>
    )}
  </div>
);
```

## Best Practices

### Progress Representation
- **Accurate Values**: Ensure progress values accurately reflect actual completion
- **Smooth Animation**: Use smooth transitions for progress updates
- **Appropriate Maximum**: Set meaningful maximum values for context
- **Status Indication**: Use variants to indicate different states (success, warning, error)

### Visual Design
- **Size Selection**: Choose appropriate sizes for context and importance
- **Thickness Balance**: Match ring thickness to overall design and legibility
- **Color Meaning**: Use color variants consistently with their semantic meaning
- **Center Content**: Use center space effectively for additional information

### User Experience
- **Loading States**: Use indeterminate rings when progress is unknown
- **Interactive Feedback**: Provide clear affordances for interactive rings
- **Accessibility**: Include proper labels and announcements for screen readers
- **Performance**: Optimize animations for smooth performance

### Content Strategy
- **Value Display**: Show progress values when they provide meaningful information
- **Custom Formatting**: Use appropriate formatting for different contexts
- **Center Utilization**: Leverage center space for icons, avatars, or additional text
- **Progress Context**: Provide context about what the progress represents

## Accessibility Considerations

- Uses appropriate ARIA attributes including `role="progressbar"`
- Provides accessible value announcements to screen readers
- Supports high contrast mode with sufficient color contrast
- Includes proper labeling for screen reader context
- Respects user preferences for reduced motion
- Maintains keyboard accessibility for interactive variants

## Related Components

- **SafProgressBar**: Linear progress indicator alternative
- **SafProgressText**: Text-based progress component
- **SafSpinner**: Simple loading indicator
- **SafStatus**: Status indicator for completed states
- **SafLoader**: Full-page loading component
- **SafCircularProgress**: Alternative circular progress implementation

## Notes

- SafProgressRing automatically animates progress changes with smooth transitions
- Indeterminate mode provides continuous rotation animation for unknown progress
- Custom formatting functions receive both current value and maximum for flexible display
- Interactive variants support keyboard navigation and proper focus management
- The component maintains aspect ratio and scales appropriately across different sizes
- Progress values are automatically clamped between 0 and the maximum value
- Center content can be any React element, allowing for complex custom displays
