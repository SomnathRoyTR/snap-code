# SafSliderLabel

The SafSliderLabel component provides labeling functionality for SafSlider components. It displays labels at specific positions along the slider track, helping users understand the scale and values represented by the slider.

## React

### API

| Prop         | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `position`   | `number`                | `0`         | Position along slider (0-100 percentage)      |
| `value`      | `string \| number`      | `undefined` | The value this label represents                |
| `label`      | `string`                | `undefined` | Text content to display                        |
| `placement`  | `"above" \| "below" \| "start" \| "end"` | `"below"` | Label position relative to slider |
| `size`       | `"small" \| "medium" \| "large"` | `"medium"` | Label text size                       |
| `variant`    | `"primary" \| "secondary" \| "muted"` | `"primary"` | Label style variant            |
| `offset`     | `number`                | `0`         | Additional offset from default position (px)  |
| `align`      | `"start" \| "center" \| "end"` | `"center"` | Text alignment within the label        |
| `interactive`| `boolean`               | `false`     | Whether label is clickable                     |
| `className`  | `string`                | `undefined` | Additional CSS class names                     |
| `onClick`    | `(event: MouseEvent, value: string \| number) => void` | `undefined` | Click handler |
| `children`   | `ReactNode`             | `undefined` | Custom content (overrides label prop)         |

### Examples

#### Basic Usage

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState } from 'react';

function BasicSliderWithLabels() {
  const [value, setValue] = useState(50);

  return (
    <div style={{ padding: '40px 20px' }}>
      <SafSlider
        min={0}
        max={100}
        value={value}
        onChange={setValue}
        aria-label="Volume control"
      >
        <SafSliderLabel position={0} label="Min" value={0} />
        <SafSliderLabel position={25} label="Low" value={25} />
        <SafSliderLabel position={50} label="Medium" value={50} />
        <SafSliderLabel position={75} label="High" value={75} />
        <SafSliderLabel position={100} label="Max" value={100} />
      </SafSlider>
      
      <p>Current value: {value}</p>
    </div>
  );
}
```

#### Different Placements

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState } from 'react';

function SliderWithDifferentPlacements() {
  const [temperature, setTemperature] = useState(72);

  return (
    <div style={{ padding: '60px 20px' }}>
      <SafSlider
        min={32}
        max={100}
        value={temperature}
        onChange={setTemperature}
        aria-label="Temperature control"
      >
        {/* Labels above the slider */}
        <SafSliderLabel 
          position={0} 
          label="Freezing" 
          value={32} 
          placement="above"
          variant="secondary"
        />
        <SafSliderLabel 
          position={20} 
          label="Cold" 
          value={45} 
          placement="above"
          variant="secondary"
        />
        <SafSliderLabel 
          position={50} 
          label="Room Temp" 
          value={72} 
          placement="above"
        />
        <SafSliderLabel 
          position={80} 
          label="Hot" 
          value={90} 
          placement="above"
          variant="secondary"
        />
        
        {/* Labels below the slider */}
        <SafSliderLabel position={0} label="32°F" value={32} />
        <SafSliderLabel position={50} label="72°F" value={72} />
        <SafSliderLabel position={100} label="100°F" value={100} />
      </SafSlider>
      
      <p>Temperature: {temperature}°F</p>
    </div>
  );
}
```

#### Interactive Labels

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState } from 'react';

function InteractiveSliderLabels() {
  const [speed, setSpeed] = useState(5);
  
  const speedLevels = [
    { position: 0, value: 1, label: 'Slow', description: 'Relaxed pace' },
    { position: 25, value: 3, label: 'Easy', description: 'Comfortable pace' },
    { position: 50, value: 5, label: 'Normal', description: 'Standard pace' },
    { position: 75, value: 7, label: 'Fast', description: 'Quick pace' },
    { position: 100, value: 10, label: 'Max', description: 'Maximum speed' }
  ];

  const handleLabelClick = (event, value) => {
    setSpeed(value);
    console.log(`Jumped to speed level: ${value}`);
  };

  return (
    <div style={{ padding: '40px 20px' }}>
      <SafSlider
        min={1}
        max={10}
        value={speed}
        onChange={setSpeed}
        aria-label="Speed control"
      >
        {speedLevels.map((level) => (
          <SafSliderLabel
            key={level.value}
            position={level.position}
            value={level.value}
            label={level.label}
            interactive={true}
            onClick={handleLabelClick}
            className="interactive-label"
            title={level.description}
          />
        ))}
      </SafSlider>
      
      <p>Speed Level: {speed}/10</p>
    </div>
  );
}
```

#### Custom Styled Labels

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState } from 'react';

function CustomStyledLabels() {
  const [quality, setQuality] = useState(3);
  
  const qualityLevels = [
    { position: 0, value: 1, icon: '📱', label: 'Low', color: '#ff4444' },
    { position: 33, value: 2, icon: '💻', label: 'Medium', color: '#ffaa00' },
    { position: 66, value: 3, icon: '🖥️', label: 'High', color: '#00aa44' },
    { position: 100, value: 4, icon: '📺', label: 'Ultra', color: '#0044aa' }
  ];

  return (
    <div style={{ padding: '40px 20px' }}>
      <SafSlider
        min={1}
        max={4}
        step={1}
        value={quality}
        onChange={setQuality}
        aria-label="Video quality"
      >
        {qualityLevels.map((level) => (
          <SafSliderLabel
            key={level.value}
            position={level.position}
            value={level.value}
            interactive={true}
            onClick={(event, value) => setQuality(value)}
            size="large"
            className="quality-label"
            style={{ color: level.color }}
          >
            <div style={{ textAlign: 'center' }}>
              <div style={{ fontSize: '24px' }}>{level.icon}</div>
              <div>{level.label}</div>
            </div>
          </SafSliderLabel>
        ))}
      </SafSlider>
      
      <p>Selected Quality: {qualityLevels.find(l => l.value === quality)?.label}</p>
    </div>
  );
}
```

#### Dynamic Labels with Formatting

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState, useMemo } from 'react';

function DynamicFormattedLabels() {
  const [price, setPrice] = useState(50000);
  
  const priceLabels = useMemo(() => {
    const formatPrice = (value) => {
      if (value >= 1000000) return `$${(value / 1000000).toFixed(1)}M`;
      if (value >= 1000) return `$${(value / 1000).toFixed(0)}K`;
      return `$${value}`;
    };

    return [
      { position: 0, value: 10000 },
      { position: 25, value: 50000 },
      { position: 50, value: 100000 },
      { position: 75, value: 250000 },
      { position: 100, value: 500000 }
    ].map(item => ({
      ...item,
      label: formatPrice(item.value)
    }));
  }, []);

  const formatCurrentPrice = (value) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD'
    }).format(value);
  };

  return (
    <div style={{ padding: '40px 20px' }}>
      <h3>House Price Range</h3>
      <SafSlider
        min={10000}
        max={500000}
        step={5000}
        value={price}
        onChange={setPrice}
        aria-label="Price range"
      >
        {priceLabels.map((level) => (
          <SafSliderLabel
            key={level.value}
            position={level.position}
            value={level.value}
            label={level.label}
            interactive={true}
            onClick={(event, value) => setPrice(value)}
            variant={price === level.value ? 'primary' : 'secondary'}
          />
        ))}
      </SafSlider>
      
      <p>Selected Price: {formatCurrentPrice(price)}</p>
    </div>
  );
}
```

#### Vertical Slider Labels

```jsx
import { SafSlider, SafSliderLabel } from '@saffron/core-components';
import { useState } from 'react';

function VerticalSliderLabels() {
  const [volume, setVolume] = useState(5);

  return (
    <div style={{ padding: '20px', display: 'flex', alignItems: 'center', gap: '20px' }}>
      <SafSlider
        min={0}
        max={10}
        value={volume}
        onChange={setVolume}
        orientation="vertical"
        style={{ height: '300px' }}
        aria-label="Volume level"
      >
        <SafSliderLabel 
          position={100} 
          label="Max" 
          value={10} 
          placement="end"
          variant="primary"
        />
        <SafSliderLabel 
          position={80} 
          label="8" 
          value={8} 
          placement="end"
          variant="secondary"
        />
        <SafSliderLabel 
          position={60} 
          label="6" 
          value={6} 
          placement="end"
          variant="secondary"
        />
        <SafSliderLabel 
          position={40} 
          label="4" 
          value={4} 
          placement="end"
          variant="secondary"
        />
        <SafSliderLabel 
          position={20} 
          label="2" 
          value={2} 
          placement="end"
          variant="secondary"
        />
        <SafSliderLabel 
          position={0} 
          label="Mute" 
          value={0} 
          placement="end"
          variant="muted"
        />
      </SafSlider>
      
      <div>
        <p>Volume: {volume}/10</p>
        <p>Level: {volume === 0 ? 'Muted' : volume > 7 ? 'Loud' : volume > 3 ? 'Medium' : 'Quiet'}</p>
      </div>
    </div>
  );
}
```

## Angular

### API

| Input        | Type                    | Default     | Description                                    |
| ------------ | ----------------------- | ----------- | ---------------------------------------------- |
| `position`   | `number`                | `0`         | Position along slider (0-100 percentage)      |
| `value`      | `string \| number`      | `undefined` | The value this label represents                |
| `label`      | `string`                | `undefined` | Text content to display                        |
| `placement`  | `"above" \| "below" \| "start" \| "end"` | `"below"` | Label position relative to slider |
| `size`       | `"small" \| "medium" \| "large"` | `"medium"` | Label text size                       |
| `variant`    | `"primary" \| "secondary" \| "muted"` | `"primary"` | Label style variant            |
| `offset`     | `number`                | `0`         | Additional offset from default position (px)  |
| `align`      | `"start" \| "center" \| "end"` | `"center"` | Text alignment within the label        |
| `interactive`| `boolean`               | `false`     | Whether label is clickable                     |

### Events

| Output       | Type                    | Description                                    |
| ------------ | ----------------------- | ---------------------------------------------- |
| `click`      | `EventEmitter<{event: MouseEvent, value: string \| number}>` | Emitted when label is clicked |

### Examples

#### Basic Usage

```html
<!-- Angular template -->
<div style="padding: 40px 20px;">
  <saf-slider
    [min]="0"
    [max]="100"
    [value]="value"
    (valueChange)="value = $event"
    aria-label="Volume control">
    <saf-slider-label [position]="0" label="Min" [value]="0"></saf-slider-label>
    <saf-slider-label [position]="25" label="Low" [value]="25"></saf-slider-label>
    <saf-slider-label [position]="50" label="Medium" [value]="50"></saf-slider-label>
    <saf-slider-label [position]="75" label="High" [value]="75"></saf-slider-label>
    <saf-slider-label [position]="100" label="Max" [value]="100"></saf-slider-label>
  </saf-slider>
  
  <p>Current value: {{ value }}</p>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-slider-labels',
  template: `
    <div style="padding: 40px 20px;">
      <saf-slider
        [min]="0"
        [max]="100"
        [value]="value"
        (valueChange)="value = $event"
        aria-label="Volume control">
        <saf-slider-label [position]="0" label="Min" [value]="0"></saf-slider-label>
        <saf-slider-label [position]="25" label="Low" [value]="25"></saf-slider-label>
        <saf-slider-label [position]="50" label="Medium" [value]="50"></saf-slider-label>
        <saf-slider-label [position]="75" label="High" [value]="75"></saf-slider-label>
        <saf-slider-label [position]="100" label="Max" [value]="100"></saf-slider-label>
      </saf-slider>
      
      <p>Current value: {{ value }}</p>
    </div>
  `
})
export class BasicSliderLabelsComponent {
  value = 50;
}
```

#### Interactive Labels

```html
<!-- Angular template -->
<div style="padding: 40px 20px;">
  <saf-slider
    [min]="1"
    [max]="10"
    [value]="speed"
    (valueChange)="speed = $event"
    aria-label="Speed control">
    <saf-slider-label 
      *ngFor="let level of speedLevels"
      [position]="level.position"
      [value]="level.value"
      [label]="level.label"
      [interactive]="true"
      (click)="onLabelClick($event)"
      class="interactive-label"
      [title]="level.description">
    </saf-slider-label>
  </saf-slider>
  
  <p>Speed Level: {{ speed }}/10</p>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface SpeedLevel {
  position: number;
  value: number;
  label: string;
  description: string;
}

@Component({
  selector: 'app-interactive-slider-labels',
  template: `
    <div style="padding: 40px 20px;">
      <saf-slider
        [min]="1"
        [max]="10"
        [value]="speed"
        (valueChange)="speed = $event"
        aria-label="Speed control">
        <saf-slider-label 
          *ngFor="let level of speedLevels"
          [position]="level.position"
          [value]="level.value"
          [label]="level.label"
          [interactive]="true"
          (click)="onLabelClick($event)"
          class="interactive-label"
          [title]="level.description">
        </saf-slider-label>
      </saf-slider>
      
      <p>Speed Level: {{ speed }}/10</p>
    </div>
  `
})
export class InteractiveSliderLabelsComponent {
  speed = 5;
  
  speedLevels: SpeedLevel[] = [
    { position: 0, value: 1, label: 'Slow', description: 'Relaxed pace' },
    { position: 25, value: 3, label: 'Easy', description: 'Comfortable pace' },
    { position: 50, value: 5, label: 'Normal', description: 'Standard pace' },
    { position: 75, value: 7, label: 'Fast', description: 'Quick pace' },
    { position: 100, value: 10, label: 'Max', description: 'Maximum speed' }
  ];

  onLabelClick(event: {event: MouseEvent, value: number}): void {
    this.speed = event.value;
    console.log(`Jumped to speed level: ${event.value}`);
  }
}
```

#### Different Placements

```html
<!-- Angular template -->
<div style="padding: 60px 20px;">
  <saf-slider
    [min]="32"
    [max]="100"
    [value]="temperature"
    (valueChange)="temperature = $event"
    aria-label="Temperature control">
    
    <!-- Labels above the slider -->
    <saf-slider-label 
      [position]="0" 
      label="Freezing" 
      [value]="32" 
      placement="above"
      variant="secondary">
    </saf-slider-label>
    <saf-slider-label 
      [position]="20" 
      label="Cold" 
      [value]="45" 
      placement="above"
      variant="secondary">
    </saf-slider-label>
    <saf-slider-label 
      [position]="50" 
      label="Room Temp" 
      [value]="72" 
      placement="above">
    </saf-slider-label>
    <saf-slider-label 
      [position]="80" 
      label="Hot" 
      [value]="90" 
      placement="above"
      variant="secondary">
    </saf-slider-label>
    
    <!-- Labels below the slider -->
    <saf-slider-label [position]="0" label="32°F" [value]="32"></saf-slider-label>
    <saf-slider-label [position]="50" label="72°F" [value]="72"></saf-slider-label>
    <saf-slider-label [position]="100" label="100°F" [value]="100"></saf-slider-label>
  </saf-slider>
  
  <p>Temperature: {{ temperature }}°F</p>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

@Component({
  selector: 'app-different-placements',
  template: `
    <div style="padding: 60px 20px;">
      <saf-slider
        [min]="32"
        [max]="100"
        [value]="temperature"
        (valueChange)="temperature = $event"
        aria-label="Temperature control">
        
        <!-- Labels above the slider -->
        <saf-slider-label 
          [position]="0" 
          label="Freezing" 
          [value]="32" 
          placement="above"
          variant="secondary">
        </saf-slider-label>
        <saf-slider-label 
          [position]="20" 
          label="Cold" 
          [value]="45" 
          placement="above"
          variant="secondary">
        </saf-slider-label>
        <saf-slider-label 
          [position]="50" 
          label="Room Temp" 
          [value]="72" 
          placement="above">
        </saf-slider-label>
        <saf-slider-label 
          [position]="80" 
          label="Hot" 
          [value]="90" 
          placement="above"
          variant="secondary">
        </saf-slider-label>
        
        <!-- Labels below the slider -->
        <saf-slider-label [position]="0" label="32°F" [value]="32"></saf-slider-label>
        <saf-slider-label [position]="50" label="72°F" [value]="72"></saf-slider-label>
        <saf-slider-label [position]="100" label="100°F" [value]="100"></saf-slider-label>
      </saf-slider>
      
      <p>Temperature: {{ temperature }}°F</p>
    </div>
  `
})
export class DifferentPlacementsComponent {
  temperature = 72;
}
```

#### Custom Content Labels

```html
<!-- Angular template -->
<div style="padding: 40px 20px;">
  <saf-slider
    [min]="1"
    [max]="4"
    [step]="1"
    [value]="quality"
    (valueChange)="quality = $event"
    aria-label="Video quality">
    <saf-slider-label 
      *ngFor="let level of qualityLevels"
      [position]="level.position"
      [value]="level.value"
      [interactive]="true"
      (click)="onQualityClick($event)"
      size="large"
      class="quality-label"
      [style]="{ color: level.color }">
      <div style="text-align: center;">
        <div style="font-size: 24px;">{{ level.icon }}</div>
        <div>{{ level.label }}</div>
      </div>
    </saf-slider-label>
  </saf-slider>
  
  <p>Selected Quality: {{ getQualityName() }}</p>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface QualityLevel {
  position: number;
  value: number;
  icon: string;
  label: string;
  color: string;
}

@Component({
  selector: 'app-custom-content-labels',
  template: `
    <div style="padding: 40px 20px;">
      <saf-slider
        [min]="1"
        [max]="4"
        [step]="1"
        [value]="quality"
        (valueChange)="quality = $event"
        aria-label="Video quality">
        <saf-slider-label 
          *ngFor="let level of qualityLevels"
          [position]="level.position"
          [value]="level.value"
          [interactive]="true"
          (click)="onQualityClick($event)"
          size="large"
          class="quality-label"
          [style]="{ color: level.color }">
          <div style="text-align: center;">
            <div style="font-size: 24px;">{{ level.icon }}</div>
            <div>{{ level.label }}</div>
          </div>
        </saf-slider-label>
      </saf-slider>
      
      <p>Selected Quality: {{ getQualityName() }}</p>
    </div>
  `
})
export class CustomContentLabelsComponent {
  quality = 3;
  
  qualityLevels: QualityLevel[] = [
    { position: 0, value: 1, icon: '📱', label: 'Low', color: '#ff4444' },
    { position: 33, value: 2, icon: '💻', label: 'Medium', color: '#ffaa00' },
    { position: 66, value: 3, icon: '🖥️', label: 'High', color: '#00aa44' },
    { position: 100, value: 4, icon: '📺', label: 'Ultra', color: '#0044aa' }
  ];

  onQualityClick(event: {event: MouseEvent, value: number}): void {
    this.quality = event.value;
  }

  getQualityName(): string {
    return this.qualityLevels.find(l => l.value === this.quality)?.label || '';
  }
}
```

#### Dynamic Price Labels

```html
<!-- Angular template -->
<div style="padding: 40px 20px;">
  <h3>House Price Range</h3>
  <saf-slider
    [min]="10000"
    [max]="500000"
    [step]="5000"
    [value]="price"
    (valueChange)="price = $event"
    aria-label="Price range">
    <saf-slider-label 
      *ngFor="let level of priceLabels"
      [position]="level.position"
      [value]="level.value"
      [label]="level.label"
      [interactive]="true"
      (click)="onPriceClick($event)"
      [variant]="price === level.value ? 'primary' : 'secondary'">
    </saf-slider-label>
  </saf-slider>
  
  <p>Selected Price: {{ formatCurrentPrice(price) }}</p>
</div>
```

```typescript
// Angular component
import { Component } from '@angular/core';

interface PriceLabel {
  position: number;
  value: number;
  label: string;
}

@Component({
  selector: 'app-dynamic-price-labels',
  template: `
    <div style="padding: 40px 20px;">
      <h3>House Price Range</h3>
      <saf-slider
        [min]="10000"
        [max]="500000"
        [step]="5000"
        [value]="price"
        (valueChange)="price = $event"
        aria-label="Price range">
        <saf-slider-label 
          *ngFor="let level of priceLabels"
          [position]="level.position"
          [value]="level.value"
          [label]="level.label"
          [interactive]="true"
          (click)="onPriceClick($event)"
          [variant]="price === level.value ? 'primary' : 'secondary'">
        </saf-slider-label>
      </saf-slider>
      
      <p>Selected Price: {{ formatCurrentPrice(price) }}</p>
    </div>
  `
})
export class DynamicPriceLabelsComponent {
  price = 50000;

  get priceLabels(): PriceLabel[] {
    return [
      { position: 0, value: 10000 },
      { position: 25, value: 50000 },
      { position: 50, value: 100000 },
      { position: 75, value: 250000 },
      { position: 100, value: 500000 }
    ].map(item => ({
      ...item,
      label: this.formatPrice(item.value)
    }));
  }

  private formatPrice(value: number): string {
    if (value >= 1000000) return `$${(value / 1000000).toFixed(1)}M`;
    if (value >= 1000) return `$${(value / 1000).toFixed(0)}K`;
    return `$${value}`;
  }

  formatCurrentPrice(value: number): string {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD'
    }).format(value);
  }

  onPriceClick(event: {event: MouseEvent, value: number}): void {
    this.price = event.value;
  }
}
```

### Best Practices

- **Meaningful positions**: Place labels at logical intervals that correspond to meaningful values
- **Appropriate spacing**: Ensure labels don't overlap, especially on smaller screens
- **Clear hierarchy**: Use different variants to show importance or relationship between labels
- **Interactive feedback**: Provide visual feedback when labels are interactive
- **Accessibility**: Ensure labels are readable and provide context for screen reader users
- **Responsive design**: Consider how labels behave on different screen sizes
- **Value correlation**: Ensure label positions accurately reflect their values on the slider scale
- **Consistent formatting**: Use consistent number/value formatting across all labels

### Notes

- SafSliderLabel components must be children of a SafSlider component
- Position values are percentages (0-100) relative to the slider's length
- Interactive labels allow users to jump to specific values by clicking
- Custom content can be provided through content projection, overriding the label prop
- The component automatically handles positioning for both horizontal and vertical sliders
- Labels inherit orientation context from their parent SafSlider component
- Consider performance when using many labels with complex content or frequent updates
