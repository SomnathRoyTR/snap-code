# SafSlider - Range Input Component

## Overview
`SafSlider` is an interactive slider component for selecting numeric values within a specified range. It supports horizontal/vertical orientations, custom step values, and full accessibility compliance with ARIA slider pattern.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `value` | `string \| number` | `0` | Current slider value |
| `min` | `number` | `0` | Minimum allowed value |
| `max` | `number` | `10` | Maximum allowed value |
| `step` | `number` | `undefined` | Step increment for value changes |
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` | Slider orientation |
| `mode` | `'single-value'` | `'single-value'` | Selection mode |
| `readonly` | `boolean` | `false` | Whether slider is read-only |
| `disabled` | `boolean` | `false` | Whether slider is disabled |
| `required` | `boolean` | `false` | Whether value is required |
| `required-text` | `string` | `'*'` | Text for required indicator |
| `autocomplete` | `string` | `undefined` | Browser autocomplete attribute |

### Slots
| Slot | Description |
|------|-------------|
| `track` | Custom track element |
| `track-start` | Visual indicator for track start |
| `thumb` | Custom thumb element |
| (default) | Labels and additional content |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `change` | `CustomEvent<number>` | Fired when slider value changes |
| `input` | `InputEvent` | Fired during value input |

### Methods
| Method | Description |
|--------|-------------|
| `increment()` | Increase value by step amount |
| `decrement()` | Decrease value by step amount |
| `focus()` | Focus the slider control |
| `blur()` | Remove focus from slider |

### Properties
| Property | Type | Description |
|----------|------|-------------|
| `valueAsNumber` | `number` | Current value as number |
| `valueTextFormatter` | `Function` | Custom formatter for aria-valuetext |

## Usage Examples

### Basic Horizontal Slider
```typescript
// React
import { SafSlider } from '@saffron/react';

export const BasicSlider = () => {
  const [value, setValue] = useState(50);
  
  return (
    <SafSlider
      min={0}
      max={100}
      step={1}
      value={value}
      onChange={(e) => setValue(e.target.valueAsNumber)}
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-slider
      [min]="0"
      [max]="100"
      [step]="1"
      [value]="value"
      (change)="onValueChange($event)">
    </saf-slider>
  `
})
export class BasicSliderComponent {
  value = 50;
  
  onValueChange(event: CustomEvent<number>) {
    this.value = event.target.valueAsNumber;
  }
}
```

### Vertical Slider with Custom Range
```typescript
// React
export const VerticalSlider = () => {
  const [temperature, setTemperature] = useState(20);
  
  return (
    <div style={{ height: '200px', display: 'flex', alignItems: 'center' }}>
      <SafSlider
        orientation="vertical"
        min={-10}
        max={40}
        step={0.5}
        value={temperature}
        onChange={(e) => setTemperature(e.target.valueAsNumber)}
      />
      <span style={{ marginLeft: '20px' }}>
        {temperature}°C
      </span>
    </div>
  );
};
```

### Volume Control Slider
```typescript
// React
export const VolumeSlider = () => {
  const [volume, setVolume] = useState(75);
  
  const formatVolumeText = (value: string) => {
    const vol = parseInt(value);
    if (vol === 0) return 'Muted';
    if (vol < 30) return 'Low volume';
    if (vol < 70) return 'Medium volume';
    return 'High volume';
  };
  
  return (
    <SafSlider
      min={0}
      max={100}
      value={volume}
      onChange={(e) => setVolume(e.target.valueAsNumber)}
      valueTextFormatter={formatVolumeText}
      aria-label="Volume control"
    >
      <div style={{ display: 'flex', justifyContent: 'space-between' }}>
        <span>🔇</span>
        <span>Volume: {volume}%</span>
        <span>🔊</span>
      </div>
    </SafSlider>
  );
};
```

### Price Range Slider
```typescript
// React
export const PriceSlider = () => {
  const [price, setPrice] = useState(250);
  
  return (
    <div>
      <label htmlFor="price-slider">
        Max Price: ${price.toLocaleString()}
      </label>
      <SafSlider
        id="price-slider"
        min={0}
        max={1000}
        step={25}
        value={price}
        onChange={(e) => setPrice(e.target.valueAsNumber)}
      >
        <div style={{ display: 'flex', justifyContent: 'space-between', fontSize: '0.8rem' }}>
          <span>$0</span>
          <span>$500</span>
          <span>$1,000</span>
        </div>
      </SafSlider>
    </div>
  );
};
```

### Custom Styled Slider
```typescript
// React
export const CustomSlider = () => {
  const [progress, setProgress] = useState(30);
  
  return (
    <SafSlider
      min={0}
      max={100}
      value={progress}
      onChange={(e) => setProgress(e.target.valueAsNumber)}
      style={{
        '--track-color': '#e0e0e0',
        '--thumb-color': '#007acc',
        '--track-height': '8px'
      }}
    >
      <div slot="track-start" style={{ 
        background: 'linear-gradient(90deg, #4CAF50, #FFC107, #F44336)',
        height: '100%',
        borderRadius: '4px'
      }} />
      <div slot="thumb" style={{
        width: '20px',
        height: '20px',
        borderRadius: '50%',
        background: '#fff',
        border: '3px solid #007acc',
        boxShadow: '0 2px 4px rgba(0,0,0,0.2)'
      }} />
      Progress: {progress}%
    </SafSlider>
  );
};
```

### Form Integration
```typescript
// React with validation
export const FormSlider = () => {
  const [rating, setRating] = useState(3);
  const [error, setError] = useState('');
  
  const validateRating = (value: number) => {
    if (value < 1) {
      setError('Rating must be at least 1');
    } else {
      setError('');
    }
  };
  
  return (
    <div>
      <label>
        Rate this product (1-5 stars)
        <SafSlider
          min={1}
          max={5}
          step={1}
          value={rating}
          onChange={(e) => {
            setRating(e.target.valueAsNumber);
            validateRating(e.target.valueAsNumber);
          }}
          required
          aria-describedby={error ? 'rating-error' : undefined}
        >
          <div style={{ display: 'flex', justifyContent: 'space-between' }}>
            {[1, 2, 3, 4, 5].map(star => (
              <span key={star} style={{ opacity: star <= rating ? 1 : 0.3 }}>
                ⭐
              </span>
            ))}
          </div>
        </SafSlider>
      </label>
      {error && <div id="rating-error" role="alert" style={{ color: 'red' }}>
        {error}
      </div>}
    </div>
  );
};
```

## Accessibility Features

- **ARIA Slider Pattern**: Implements WAI-ARIA slider specification
- **Keyboard Navigation**: Full arrow key, Home, End key support
- **Screen Reader Support**: Proper value announcements and state changes
- **Focus Indicators**: Clear visual focus indicators
- **Value Text**: Customizable aria-valuetext for better context
- **Labeling**: Supports aria-label and associated label elements
- **High Contrast**: Full high contrast mode support

## Best Practices

1. **Labeling**: Always provide clear labels for sliders
2. **Value Display**: Show current value visually when possible
3. **Step Size**: Choose appropriate step values for the use case
4. **Range Indication**: Show min/max values or meaningful markers
5. **Validation**: Provide clear feedback for invalid ranges
6. **Touch Targets**: Ensure thumb is large enough for touch interaction
7. **Context**: Use valueTextFormatter for meaningful value descriptions

## Advanced Usage

### Responsive Slider
```typescript
// React
export const ResponsiveSlider = () => {
  const [orientation, setOrientation] = useState('horizontal');
  const [value, setValue] = useState(50);
  
  useEffect(() => {
    const handleResize = () => {
      setOrientation(window.innerWidth < 600 ? 'vertical' : 'horizontal');
    };
    
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);
  
  return (
    <SafSlider
      orientation={orientation}
      min={0}
      max={100}
      value={value}
      onChange={(e) => setValue(e.target.valueAsNumber)}
      style={{
        height: orientation === 'vertical' ? '150px' : 'auto',
        width: orientation === 'horizontal' ? '300px' : 'auto'
      }}
    />
  );
};
```

### Integration with Form Libraries
```typescript
// React Hook Form integration
import { useForm, Controller } from 'react-hook-form';

interface FormData {
  satisfaction: number;
}

export const HookFormSlider = () => {
  const { control, handleSubmit } = useForm<FormData>({
    defaultValues: { satisfaction: 5 }
  });
  
  return (
    <form onSubmit={handleSubmit(console.log)}>
      <Controller
        name="satisfaction"
        control={control}
        rules={{ min: 1, max: 10 }}
        render={({ field, fieldState }) => (
          <div>
            <label>Satisfaction Level: {field.value}/10</label>
            <SafSlider
              {...field}
              min={1}
              max={10}
              step={1}
              aria-invalid={!!fieldState.error}
            >
              <div style={{ display: 'flex', justifyContent: 'space-between' }}>
                <span>Very Poor</span>
                <span>Excellent</span>
              </div>
            </SafSlider>
          </div>
        )}
      />
    </form>
  );
};
```

## Notes

- Supports both horizontal and vertical orientations
- Provides smooth drag interaction with mouse and touch
- Implements full keyboard accessibility
- Allows custom styling through CSS custom properties
- Integrates seamlessly with form validation
- Supports fractional step values for precise control
