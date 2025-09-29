# SafSlider

## Overview

SafSlider is a customizable range input component that allows users to select numeric values within a specified range. It supports single and dual-handle configurations, custom styling, step increments, value formatting, and accessibility features for precise value selection.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number \| [number, number]` | `0` | Current slider value (controlled) |
| `defaultValue` | `number \| [number, number]` | `0` | Initial slider value (uncontrolled) |
| `min` | `number` | `0` | Minimum value |
| `max` | `number` | `100` | Maximum value |
| `step` | `number` | `1` | Step increment between values |
| `range` | `boolean` | `false` | Enable dual-handle range selection |
| `disabled` | `boolean` | `false` | Disables the slider |
| `vertical` | `boolean` | `false` | Vertical orientation |
| `reverse` | `boolean` | `false` | Reverse the slider direction |
| `marks` | `boolean \| object[]` | `false` | Show marks on the slider track |
| `showTooltip` | `boolean \| 'always' \| 'hover' \| 'focus'` | `'hover'` | Tooltip display behavior |
| `tooltipFormatter` | `(value: number) => string` | - | Custom tooltip value formatter |
| `formatLabel` | `(value: number) => string` | - | Custom value label formatter |
| `trackStyle` | `object` | - | Custom track styling |
| `handleStyle` | `object \| object[]` | - | Custom handle styling |
| `railStyle` | `object` | - | Custom rail styling |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Slider size variant |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'error' \| 'warning'` | `'primary'` | Color theme |
| `showLabels` | `boolean` | `false` | Show min/max labels |
| `showValue` | `boolean` | `false` | Show current value label |
| `name` | `string` | - | Form field name |
| `id` | `string` | - | Component identifier |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onChange` | `(value: number \| [number, number]) => void` | Fired when value changes |
| `onChangeComplete` | `(value: number \| [number, number]) => void` | Fired when drag operation completes |
| `onFocus` | `() => void` | Fired when slider receives focus |
| `onBlur` | `() => void` | Fired when slider loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `number \| [number, number]` | `0` | Current slider value |
| `min` | `number` | `0` | Minimum value |
| `max` | `number` | `100` | Maximum value |
| `step` | `number` | `1` | Step increment between values |
| `range` | `boolean` | `false` | Enable dual-handle range selection |
| `disabled` | `boolean` | `false` | Disables the slider |
| `vertical` | `boolean` | `false` | Vertical orientation |
| `reverse` | `boolean` | `false` | Reverse the slider direction |
| `marks` | `boolean \| object[]` | `false` | Show marks on the slider track |
| `showTooltip` | `boolean \| 'always' \| 'hover' \| 'focus'` | `'hover'` | Tooltip display behavior |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Slider size variant |
| `color` | `'primary' \| 'secondary' \| 'success' \| 'error' \| 'warning'` | `'primary'` | Color theme |
| `showLabels` | `boolean` | `false` | Show min/max labels |
| `showValue` | `boolean` | `false` | Show current value label |
| `name` | `string` | - | Form field name |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `valueChange` | `EventEmitter<number \| [number, number]>` | Fired when value changes |
| `changeComplete` | `EventEmitter<number \| [number, number]>` | Fired when drag operation completes |
| `focus` | `EventEmitter<void>` | Fired when slider receives focus |
| `blur` | `EventEmitter<void>` | Fired when slider loses focus |

## Usage Examples

### Basic Slider

```typescript
// React
const [volume, setVolume] = useState(50);

<SafFormField label="Volume">
  <SafSlider 
    value={volume}
    onChange={setVolume}
    min={0}
    max={100}
    showValue
    showLabels
  />
</SafFormField>
```

```html
<!-- Angular -->
<saf-form-field label="Volume">
  <saf-slider 
    [(value)]="volume"
    [min]="0"
    [max]="100"
    [showValue]="true"
    [showLabels]="true">
  </saf-slider>
</saf-form-field>
```

### Range Slider

```typescript
// React
const [priceRange, setPriceRange] = useState([20, 80]);

<SafFormField label="Price Range">
  <SafSlider 
    value={priceRange}
    onChange={setPriceRange}
    min={0}
    max={100}
    range
    formatLabel={(value) => `$${value}`}
    showTooltip="always"
  />
</SafFormField>
```

### Slider with Custom Steps

```typescript
// React
<SafSlider 
  value={rating}
  onChange={setRating}
  min={0}
  max={5}
  step={0.5}
  marks={[
    { value: 0, label: '0' },
    { value: 1, label: '1' },
    { value: 2, label: '2' },
    { value: 3, label: '3' },
    { value: 4, label: '4' },
    { value: 5, label: '5' }
  ]}
  tooltipFormatter={(value) => `${value} stars`}
/>
```

### Vertical Slider

```typescript
// React
<div style={{ height: '200px', display: 'flex', alignItems: 'center' }}>
  <SafSlider 
    value={temperature}
    onChange={setTemperature}
    min={-10}
    max={40}
    vertical
    showValue
    formatLabel={(value) => `${value}°C`}
    color="error"
  />
</div>
```

### Volume Control

```typescript
// React
const VolumeControl = ({ volume, onVolumeChange }) => (
  <div className="volume-control">
    <SafIcon name="volume-down" />
    <SafSlider 
      value={volume}
      onChange={onVolumeChange}
      min={0}
      max={100}
      step={5}
      showTooltip="hover"
      tooltipFormatter={(value) => `${value}%`}
      size="small"
    />
    <SafIcon name="volume-up" />
  </div>
);
```

### Color Opacity Slider

```typescript
// React
const ColorOpacitySlider = ({ opacity, onChange }) => (
  <SafFormField label="Opacity">
    <SafSlider 
      value={opacity}
      onChange={onChange}
      min={0}
      max={1}
      step={0.01}
      formatLabel={(value) => `${Math.round(value * 100)}%`}
      showValue
      trackStyle={{ 
        background: `linear-gradient(to right, transparent, currentColor)` 
      }}
    />
  </SafFormField>
);
```

### Age Range Filter

```typescript
// React
const AgeRangeFilter = ({ ageRange, onAgeRangeChange }) => (
  <SafFormField label="Age Range">
    <SafSlider 
      value={ageRange}
      onChange={onAgeRangeChange}
      min={18}
      max={100}
      range
      marks={[
        { value: 18, label: '18' },
        { value: 30, label: '30' },
        { value: 50, label: '50' },
        { value: 70, label: '70' },
        { value: 100, label: '100+' }
      ]}
      tooltipFormatter={(value) => `${value} years`}
    />
  </SafFormField>
);
```

### Time Slider

```typescript
// React
const TimeSlider = ({ time, onTimeChange }) => {
  const formatTime = (minutes) => {
    const hours = Math.floor(minutes / 60);
    const mins = minutes % 60;
    return `${hours.toString().padStart(2, '0')}:${mins.toString().padStart(2, '0')}`;
  };

  return (
    <SafFormField label="Time">
      <SafSlider 
        value={time}
        onChange={onTimeChange}
        min={0}
        max={1440} // 24 hours in minutes
        step={15}
        formatLabel={formatTime}
        tooltipFormatter={formatTime}
        showValue
        marks={[
          { value: 0, label: '00:00' },
          { value: 360, label: '06:00' },
          { value: 720, label: '12:00' },
          { value: 1080, label: '18:00' },
          { value: 1440, label: '24:00' }
        ]}
      />
    </SafFormField>
  );
};
```

### Progress Slider

```typescript
// React
const ProgressSlider = ({ progress, onProgressChange, total }) => (
  <div className="progress-slider">
    <SafSlider 
      value={progress}
      onChange={onProgressChange}
      min={0}
      max={total}
      showTooltip="always"
      tooltipFormatter={(value) => `${Math.round((value / total) * 100)}%`}
      color="success"
      trackStyle={{
        background: `linear-gradient(to right, 
          var(--saf-color-success) 0%, 
          var(--saf-color-success) ${(progress / total) * 100}%, 
          var(--saf-color-neutral-200) ${(progress / total) * 100}%)`
      }}
    />
    <div className="progress-info">
      <span>{progress} of {total} completed</span>
    </div>
  </div>
);
```

### Zoom Slider

```typescript
// React
const ZoomControl = ({ zoom, onZoomChange }) => {
  const zoomLevels = [25, 50, 75, 100, 125, 150, 200, 300];
  
  return (
    <div className="zoom-control">
      <SafButton 
        variant="text" 
        size="small"
        onClick={() => onZoomChange(Math.max(25, zoom - 25))}
        disabled={zoom <= 25}
      >
        <SafIcon name="zoom-out" />
      </SafButton>
      
      <SafSlider 
        value={zoom}
        onChange={onZoomChange}
        min={25}
        max={300}
        step={25}
        marks={zoomLevels.map(level => ({ 
          value: level, 
          label: `${level}%` 
        }))}
        tooltipFormatter={(value) => `${value}%`}
        size="small"
      />
      
      <SafButton 
        variant="text" 
        size="small"
        onClick={() => onZoomChange(Math.min(300, zoom + 25))}
        disabled={zoom >= 300}
      >
        <SafIcon name="zoom-in" />
      </SafButton>
    </div>
  );
};
```

### Budget Allocation Slider

```typescript
// React
const BudgetAllocation = ({ budgets, onBudgetChange, total }) => {
  const categories = ['Marketing', 'Development', 'Operations', 'Research'];
  
  return (
    <div className="budget-allocation">
      <h3>Budget Allocation (${total.toLocaleString()})</h3>
      {categories.map((category, index) => (
        <SafFormField key={category} label={category}>
          <div className="budget-slider-row">
            <SafSlider 
              value={budgets[index]}
              onChange={(value) => onBudgetChange(index, value)}
              min={0}
              max={total}
              step={1000}
              showValue
              formatLabel={(value) => `$${value.toLocaleString()}`}
              tooltipFormatter={(value) => `$${value.toLocaleString()}`}
              color={index === 0 ? 'primary' : index === 1 ? 'secondary' : index === 2 ? 'success' : 'warning'}
            />
            <span className="budget-percentage">
              {Math.round((budgets[index] / total) * 100)}%
            </span>
          </div>
        </SafFormField>
      ))}
      
      <div className="remaining-budget">
        Remaining: ${(total - budgets.reduce((sum, budget) => sum + budget, 0)).toLocaleString()}
      </div>
    </div>
  );
};
```

### Media Player Seek Bar

```typescript
// React
const MediaSeekBar = ({ currentTime, duration, onSeek, buffered }) => {
  const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60);
    const secs = Math.floor(seconds % 60);
    return `${mins}:${secs.toString().padStart(2, '0')}`;
  };

  return (
    <div className="media-seek-bar">
      <span className="time-current">{formatTime(currentTime)}</span>
      
      <SafSlider 
        value={currentTime}
        onChange={onSeek}
        min={0}
        max={duration}
        step={0.1}
        showTooltip="hover"
        tooltipFormatter={(value) => formatTime(value)}
        trackStyle={{
          background: `linear-gradient(to right, 
            var(--saf-color-primary) 0%, 
            var(--saf-color-primary) ${(currentTime / duration) * 100}%, 
            var(--saf-color-primary-alpha-30) ${(buffered / duration) * 100}%, 
            var(--saf-color-neutral-200) ${(buffered / duration) * 100}%)`
        }}
        size="small"
      />
      
      <span className="time-duration">{formatTime(duration)}</span>
    </div>
  );
};
```

### Temperature Range Control

```typescript
// React
const TemperatureControl = ({ tempRange, onTempChange, unit }) => (
  <SafFormField label={`Temperature Range (°${unit})`}>
    <SafSlider 
      value={tempRange}
      onChange={onTempChange}
      min={unit === 'C' ? -20 : -4}
      max={unit === 'C' ? 50 : 122}
      range
      step={unit === 'C' ? 1 : 2}
      marks={unit === 'C' ? [
        { value: -20, label: '-20°' },
        { value: 0, label: '0°' },
        { value: 20, label: '20°' },
        { value: 50, label: '50°' }
      ] : [
        { value: -4, label: '-4°' },
        { value: 32, label: '32°' },
        { value: 68, label: '68°' },
        { value: 122, label: '122°' }
      ]}
      tooltipFormatter={(value) => `${value}°${unit}`}
      color={tempRange[0] < (unit === 'C' ? 0 : 32) ? 'primary' : 
             tempRange[1] > (unit === 'C' ? 30 : 86) ? 'error' : 'success'}
    />
  </SafFormField>
);
```

### Custom Styled Slider

```typescript
// React
const CustomStyledSlider = ({ value, onChange }) => (
  <SafSlider 
    value={value}
    onChange={onChange}
    min={0}
    max={100}
    showTooltip="always"
    railStyle={{
      background: 'linear-gradient(90deg, #ff6b6b, #feca57, #48dbfb, #ff9ff3)',
      height: '8px'
    }}
    trackStyle={{
      background: 'rgba(255, 255, 255, 0.8)',
      height: '8px'
    }}
    handleStyle={{
      border: '3px solid white',
      boxShadow: '0 4px 12px rgba(0, 0, 0, 0.2)',
      width: '20px',
      height: '20px'
    }}
  />
);
```

## Best Practices

### Value Management
- **Clear Ranges**: Use appropriate min/max values for the use case
- **Logical Steps**: Choose step values that make sense for the data
- **Default Values**: Set sensible default values within the valid range
- **Validation**: Validate values and handle edge cases gracefully

### Visual Design
- **Appropriate Sizing**: Choose slider size based on importance and space
- **Clear Labels**: Provide clear labels and value indicators when needed
- **Color Usage**: Use colors consistently with your design system
- **Marks and Indicators**: Use marks sparingly for important values

### Interaction
- **Responsive Touch**: Ensure sliders work well on touch devices
- **Keyboard Support**: Support arrow keys and page up/down for keyboard users
- **Tooltips**: Show tooltips on hover/focus for precise value feedback
- **Smooth Animation**: Use smooth transitions for visual feedback

### Accessibility
- **ARIA Labels**: Provide descriptive labels for screen readers
- **Keyboard Navigation**: Support full keyboard interaction
- **Value Announcements**: Announce value changes to assistive technology
- **Focus Indicators**: Provide clear focus indicators

## Accessibility Considerations

- Uses proper ARIA attributes including `role="slider"` and value properties
- Supports keyboard navigation with arrow keys, page up/down, home/end
- Announces value changes to screen readers during interaction
- Provides clear focus indicators and high contrast support
- Maintains proper tab order and focus management
- Supports both horizontal and vertical orientations accessibly

## Related Components

- **SafSliderLabel**: Label component for slider values
- **SafRangeSlider**: Specialized dual-handle range component
- **SafInput**: Text input for precise value entry
- **SafFormField**: Form field wrapper component
- **SafProgressRing**: Circular progress indicator
- **SafProgressText**: Text-based progress component

## Notes

- SafSlider supports both controlled and uncontrolled usage patterns
- Range sliders return an array of two values [min, max]
- Custom formatters can be used for labels and tooltips
- The component handles touch events and gestures automatically
- Marks can be boolean (show all step marks) or array of custom mark objects
- Track styling can be customized for gradients and themes
- Vertical sliders automatically adjust touch/mouse interaction
- The component respects reduced motion accessibility preferences
