# SafPicker

## Overview

SafPicker is a multi-column scrollable selection component that provides an intuitive interface for selecting values from multiple related lists, commonly used for date/time selection, location selection, or any hierarchical data selection with smooth scrolling and touch-friendly interactions.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `columns` | `PickerColumn[]` | `[]` | Array of picker column configurations |
| `value` | `any[]` | `[]` | Selected values for each column |
| `defaultValue` | `any[]` | `[]` | Default selected values (uncontrolled) |
| `disabled` | `boolean` | `false` | Disable the picker |
| `loading` | `boolean` | `false` | Show loading state |
| `height` | `number \| string` | `200` | Picker height |
| `itemHeight` | `number` | `44` | Height of each picker item |
| `visibleItemCount` | `number` | `5` | Number of visible items per column |
| `infinite` | `boolean` | `false` | Enable infinite scrolling |
| `snapToItem` | `boolean` | `true` | Snap to items when scrolling |
| `momentum` | `boolean` | `true` | Enable momentum scrolling |
| `cascading` | `boolean` | `false` | Enable cascading column updates |
| `separator` | `string \| ReactElement` | - | Separator between columns |
| `showSeparator` | `boolean` | `true` | Show separators between columns |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### PickerColumn Interface

```typescript
interface PickerColumn {
  key: string;
  options: PickerOption[];
  defaultIndex?: number;
  width?: number | string;
  align?: 'left' | 'center' | 'right';
  formatter?: (option: PickerOption) => string;
  disabled?: boolean;
  infinite?: boolean;
}

interface PickerOption {
  label: string;
  value: any;
  disabled?: boolean;
  children?: PickerOption[];
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onChange` | `(values: any[], indexes: number[]) => void` | Fired when selection changes |
| `onColumnChange` | `(columnIndex: number, value: any, index: number) => void` | Fired when specific column changes |
| `onScrollStart` | `(columnIndex: number) => void` | Fired when scrolling starts |
| `onScrollEnd` | `(columnIndex: number, value: any, index: number) => void` | Fired when scrolling ends |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `columns` | `PickerColumn[]` | `[]` | Array of picker column configurations |
| `value` | `any[]` | `[]` | Selected values for each column |
| `disabled` | `boolean` | `false` | Disable the picker |
| `loading` | `boolean` | `false` | Show loading state |
| `height` | `number \| string` | `200` | Picker height |
| `itemHeight` | `number` | `44` | Height of each picker item |
| `visibleItemCount` | `number` | `5` | Number of visible items per column |
| `infinite` | `boolean` | `false` | Enable infinite scrolling |
| `snapToItem` | `boolean` | `true` | Snap to items when scrolling |
| `momentum` | `boolean` | `true` | Enable momentum scrolling |
| `cascading` | `boolean` | `false` | Enable cascading column updates |
| `showSeparator` | `boolean` | `true` | Show separators between columns |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `valueChange` | `EventEmitter<any[]>` | Fired when selection changes |
| `columnChange` | `EventEmitter<{columnIndex: number, value: any, index: number}>` | Fired when specific column changes |
| `scrollStart` | `EventEmitter<number>` | Fired when scrolling starts |
| `scrollEnd` | `EventEmitter<{columnIndex: number, value: any, index: number}>` | Fired when scrolling ends |

## Usage Examples

### Basic Time Picker

```typescript
// React
const TimePicker = ({ time, onTimeChange }) => {
  const hours = Array.from({ length: 24 }, (_, i) => ({
    label: i.toString().padStart(2, '0'),
    value: i
  }));

  const minutes = Array.from({ length: 60 }, (_, i) => ({
    label: i.toString().padStart(2, '0'),
    value: i
  }));

  const columns = [
    {
      key: 'hours',
      options: hours,
      width: '50%'
    },
    {
      key: 'minutes',
      options: minutes,
      width: '50%'
    }
  ];

  const handleChange = (values) => {
    const [hour, minute] = values;
    onTimeChange({ hour, minute });
  };

  return (
    <SafPicker 
      columns={columns}
      value={[time.hour, time.minute]}
      onChange={handleChange}
      separator=":"
      height={200}
      itemHeight={44}
    />
  );
};
```

```html
<!-- Angular -->
<saf-picker 
  [columns]="timeColumns"
  [value]="timeValue"
  (valueChange)="onTimeChange($event)"
  separator=":"
  [height]="200"
  [itemHeight]="44">
</saf-picker>
```

### Date Picker

```typescript
// React
const DatePicker = ({ date, onDateChange }) => {
  const currentYear = new Date().getFullYear();
  
  const years = Array.from({ length: 10 }, (_, i) => ({
    label: (currentYear - 5 + i).toString(),
    value: currentYear - 5 + i
  }));

  const months = [
    { label: 'January', value: 0 },
    { label: 'February', value: 1 },
    { label: 'March', value: 2 },
    { label: 'April', value: 3 },
    { label: 'May', value: 4 },
    { label: 'June', value: 5 },
    { label: 'July', value: 6 },
    { label: 'August', value: 7 },
    { label: 'September', value: 8 },
    { label: 'October', value: 9 },
    { label: 'November', value: 10 },
    { label: 'December', value: 11 }
  ];

  const getDaysInMonth = (year, month) => {
    const daysCount = new Date(year, month + 1, 0).getDate();
    return Array.from({ length: daysCount }, (_, i) => ({
      label: (i + 1).toString(),
      value: i + 1
    }));
  };

  const [days, setDays] = useState(getDaysInMonth(date.year, date.month));

  const columns = [
    {
      key: 'year',
      options: years,
      width: '30%'
    },
    {
      key: 'month',
      options: months,
      width: '40%'
    },
    {
      key: 'day',
      options: days,
      width: '30%'
    }
  ];

  const handleChange = (values) => {
    const [year, month, day] = values;
    
    // Update days when year or month changes
    const newDays = getDaysInMonth(year, month);
    setDays(newDays);
    
    onDateChange({ year, month, day: Math.min(day, newDays.length) });
  };

  return (
    <SafPicker 
      columns={columns}
      value={[date.year, date.month, date.day]}
      onChange={handleChange}
      cascading
      height={220}
    />
  );
};
```

### Location Picker with Cascading

```typescript
// React
const LocationPicker = ({ location, onLocationChange, locations }) => {
  const [countries, setCountries] = useState(locations.countries);
  const [states, setStates] = useState([]);
  const [cities, setCities] = useState([]);

  useEffect(() => {
    // Load states when country changes
    if (location.country) {
      const countryData = locations.countries.find(c => c.value === location.country);
      setStates(countryData?.states || []);
    }
  }, [location.country, locations]);

  useEffect(() => {
    // Load cities when state changes
    if (location.state) {
      const stateData = states.find(s => s.value === location.state);
      setCities(stateData?.cities || []);
    }
  }, [location.state, states]);

  const columns = [
    {
      key: 'country',
      options: countries,
      width: '35%'
    },
    {
      key: 'state',
      options: states,
      width: '35%'
    },
    {
      key: 'city',
      options: cities,
      width: '30%'
    }
  ];

  const handleColumnChange = (columnIndex, value) => {
    const columnKeys = ['country', 'state', 'city'];
    const columnKey = columnKeys[columnIndex];
    
    const newLocation = { ...location, [columnKey]: value };
    
    // Reset dependent columns
    if (columnIndex === 0) {
      newLocation.state = null;
      newLocation.city = null;
    } else if (columnIndex === 1) {
      newLocation.city = null;
    }
    
    onLocationChange(newLocation);
  };

  return (
    <SafPicker 
      columns={columns}
      value={[location.country, location.state, location.city]}
      onColumnChange={handleColumnChange}
      cascading
      loading={!countries.length}
    />
  );
};
```

### Custom Formatted Picker

```typescript
// React
const CustomFormattedPicker = () => {
  const sizes = [
    { label: 'XS', value: 'xs' },
    { label: 'Small', value: 's' },
    { label: 'Medium', value: 'm' },
    { label: 'Large', value: 'l' },
    { label: 'XL', value: 'xl' },
    { label: 'XXL', value: 'xxl' }
  ];

  const colors = [
    { label: 'Red', value: '#ff0000' },
    { label: 'Blue', value: '#0000ff' },
    { label: 'Green', value: '#00ff00' },
    { label: 'Yellow', value: '#ffff00' },
    { label: 'Purple', value: '#800080' },
    { label: 'Orange', value: '#ffa500' }
  ];

  const quantities = Array.from({ length: 10 }, (_, i) => ({
    label: `${i + 1} ${i === 0 ? 'item' : 'items'}`,
    value: i + 1
  }));

  const colorFormatter = (option) => (
    <div className="color-option">
      <div 
        className="color-swatch" 
        style={{ backgroundColor: option.value }}
      />
      <span>{option.label}</span>
    </div>
  );

  const columns = [
    {
      key: 'size',
      options: sizes,
      width: '25%'
    },
    {
      key: 'color',
      options: colors,
      width: '40%',
      formatter: colorFormatter
    },
    {
      key: 'quantity',
      options: quantities,
      width: '35%'
    }
  ];

  return (
    <SafPicker 
      columns={columns}
      defaultValue={['m', '#0000ff', 1]}
      height={240}
      itemHeight={50}
    />
  );
};
```

### Infinite Scrolling Picker

```typescript
// React
const InfiniteTimePicker = ({ time, onTimeChange }) => {
  const createInfiniteOptions = (max, formatter) => {
    return Array.from({ length: max }, (_, i) => ({
      label: formatter ? formatter(i) : i.toString(),
      value: i
    }));
  };

  const hours = createInfiniteOptions(24, (i) => i.toString().padStart(2, '0'));
  const minutes = createInfiniteOptions(60, (i) => i.toString().padStart(2, '0'));
  const seconds = createInfiniteOptions(60, (i) => i.toString().padStart(2, '0'));

  const columns = [
    {
      key: 'hours',
      options: hours,
      infinite: true,
      width: '33.33%'
    },
    {
      key: 'minutes',
      options: minutes,
      infinite: true,
      width: '33.33%'
    },
    {
      key: 'seconds',
      options: seconds,
      infinite: true,
      width: '33.33%'
    }
  ];

  return (
    <SafPicker 
      columns={columns}
      value={[time.hours, time.minutes, time.seconds]}
      onChange={([hours, minutes, seconds]) => 
        onTimeChange({ hours, minutes, seconds })
      }
      infinite
      momentum
      separator=":"
    />
  );
};
```

### Multi-Language Picker

```typescript
// React
const MultiLanguagePicker = ({ selectedLanguage, onLanguageChange }) => {
  const languages = [
    { 
      label: 'English', 
      value: 'en',
      flag: '🇺🇸'
    },
    { 
      label: 'Español', 
      value: 'es',
      flag: '🇪🇸'
    },
    { 
      label: 'Français', 
      value: 'fr',
      flag: '🇫🇷'
    },
    { 
      label: 'Deutsch', 
      value: 'de',
      flag: '🇩🇪'
    },
    { 
      label: '中文', 
      value: 'zh',
      flag: '🇨🇳'
    },
    { 
      label: '日本語', 
      value: 'ja',
      flag: '🇯🇵'
    }
  ];

  const regions = {
    'en': [
      { label: 'United States', value: 'US' },
      { label: 'United Kingdom', value: 'GB' },
      { label: 'Canada', value: 'CA' },
      { label: 'Australia', value: 'AU' }
    ],
    'es': [
      { label: 'España', value: 'ES' },
      { label: 'México', value: 'MX' },
      { label: 'Argentina', value: 'AR' }
    ],
    'fr': [
      { label: 'France', value: 'FR' },
      { label: 'Canada', value: 'CA' },
      { label: 'Belgique', value: 'BE' }
    ]
  };

  const languageFormatter = (option) => (
    <div className="language-option">
      <span className="flag">{option.flag}</span>
      <span className="language-name">{option.label}</span>
    </div>
  );

  const [currentRegions, setCurrentRegions] = useState(regions[selectedLanguage] || []);

  const handleLanguageChange = (values) => {
    const [language, region] = values;
    setCurrentRegions(regions[language] || []);
    onLanguageChange({ language, region });
  };

  const columns = [
    {
      key: 'language',
      options: languages,
      formatter: languageFormatter,
      width: '60%'
    },
    {
      key: 'region',
      options: currentRegions,
      width: '40%'
    }
  ];

  return (
    <SafPicker 
      columns={columns}
      value={[selectedLanguage.language, selectedLanguage.region]}
      onChange={handleLanguageChange}
      cascading
      height={200}
      itemHeight={48}
    />
  );
};
```

### Measurement Picker

```typescript
// React
const MeasurementPicker = ({ measurement, onMeasurementChange }) => {
  const units = [
    { label: 'Meters', value: 'm', decimals: 2 },
    { label: 'Feet', value: 'ft', decimals: 1 },
    { label: 'Inches', value: 'in', decimals: 0 },
    { label: 'Centimeters', value: 'cm', decimals: 0 }
  ];

  const integers = Array.from({ length: 100 }, (_, i) => ({
    label: i.toString(),
    value: i
  }));

  const decimals = Array.from({ length: 100 }, (_, i) => ({
    label: i.toString().padStart(2, '0'),
    value: i
  }));

  const columns = [
    {
      key: 'integer',
      options: integers,
      width: '30%',
      align: 'right'
    },
    {
      key: 'decimal',
      options: decimals,
      width: '30%',
      align: 'left'
    },
    {
      key: 'unit',
      options: units,
      width: '40%'
    }
  ];

  const handleChange = (values) => {
    const [integer, decimal, unit] = values;
    const unitData = units.find(u => u.value === unit);
    const value = parseFloat(`${integer}.${decimal.toString().padStart(2, '0')}`);
    
    onMeasurementChange({
      value,
      unit,
      formatted: `${value.toFixed(unitData.decimals)} ${unit}`
    });
  };

  return (
    <div className="measurement-picker">
      <SafPicker 
        columns={columns}
        value={[
          Math.floor(measurement.value),
          Math.round((measurement.value % 1) * 100),
          measurement.unit
        ]}
        onChange={handleChange}
        separator="."
        height={180}
      />
    </div>
  );
};
```

### Custom Styled Picker

```typescript
// React
const CustomStyledPicker = ({ theme, onThemeChange }) => {
  const themes = [
    { 
      label: 'Light', 
      value: 'light',
      preview: '#ffffff'
    },
    { 
      label: 'Dark', 
      value: 'dark',
      preview: '#1a1a1a'
    },
    { 
      label: 'Blue', 
      value: 'blue',
      preview: '#2196f3'
    },
    { 
      label: 'Purple', 
      value: 'purple',
      preview: '#9c27b0'
    }
  ];

  const fonts = [
    { label: 'System', value: 'system-ui' },
    { label: 'Arial', value: 'arial' },
    { label: 'Helvetica', value: 'helvetica' },
    { label: 'Georgia', value: 'georgia' },
    { label: 'Times', value: 'times' }
  ];

  const sizes = [
    { label: 'Small', value: 'small' },
    { label: 'Medium', value: 'medium' },
    { label: 'Large', value: 'large' },
    { label: 'Extra Large', value: 'xl' }
  ];

  const themeFormatter = (option) => (
    <div className="theme-option">
      <div 
        className="theme-preview"
        style={{ backgroundColor: option.preview }}
      />
      <span>{option.label}</span>
    </div>
  );

  const fontFormatter = (option) => (
    <span style={{ fontFamily: option.value }}>
      {option.label}
    </span>
  );

  const columns = [
    {
      key: 'theme',
      options: themes,
      formatter: themeFormatter,
      width: '40%'
    },
    {
      key: 'font',
      options: fonts,
      formatter: fontFormatter,
      width: '35%'
    },
    {
      key: 'size',
      options: sizes,
      width: '25%'
    }
  ];

  return (
    <SafPicker 
      columns={columns}
      value={[theme.theme, theme.font, theme.size]}
      onChange={([theme, font, size]) => 
        onThemeChange({ theme, font, size })
      }
      height={200}
      itemHeight={44}
      className="custom-themed-picker"
    />
  );
};
```

### Loading State Picker

```typescript
// React
const LoadingStatePicker = ({ data, loading, onSelectionChange }) => {
  const skeletonColumns = [
    {
      key: 'loading1',
      options: Array.from({ length: 5 }, (_, i) => ({
        label: <SafSkeleton width="80px" height="20px" />,
        value: i,
        disabled: true
      })),
      width: '33.33%'
    },
    {
      key: 'loading2',
      options: Array.from({ length: 5 }, (_, i) => ({
        label: <SafSkeleton width="60px" height="20px" />,
        value: i,
        disabled: true
      })),
      width: '33.33%'
    },
    {
      key: 'loading3',
      options: Array.from({ length: 5 }, (_, i) => ({
        label: <SafSkeleton width="40px" height="20px" />,
        value: i,
        disabled: true
      })),
      width: '33.33%'
    }
  ];

  if (loading) {
    return (
      <SafPicker 
        columns={skeletonColumns}
        disabled
        loading
        height={200}
      />
    );
  }

  return (
    <SafPicker 
      columns={data.columns}
      onChange={onSelectionChange}
      height={200}
    />
  );
};
```

## Best Practices

### Performance
- **Virtual Scrolling**: Use virtual scrolling for large datasets
- **Memoization**: Memoize column configurations and formatters
- **Debounced Updates**: Debounce rapid scroll events
- **Lazy Loading**: Load column data on demand when possible

### User Experience
- **Smooth Scrolling**: Ensure smooth scrolling performance across devices
- **Visual Feedback**: Provide clear visual feedback for selected items
- **Touch Gestures**: Support intuitive touch interactions
- **Momentum**: Enable momentum scrolling for natural feel

### Data Management
- **Cascading Updates**: Handle dependent column updates efficiently
- **State Synchronization**: Keep picker state synchronized with parent
- **Validation**: Validate selections and handle edge cases
- **Default Values**: Provide sensible default selections

### Accessibility
- **Keyboard Navigation**: Support keyboard navigation between columns
- **Screen Readers**: Provide proper ARIA labels and descriptions
- **Focus Management**: Maintain proper focus indicators
- **Value Announcements**: Announce selection changes

## Accessibility Considerations

- Uses proper ARIA roles and attributes for picker functionality
- Supports keyboard navigation with Tab, arrow keys, Enter, and Escape
- Provides screen reader announcements for selection changes
- Maintains proper focus management across columns
- Supports high contrast mode and reduced motion preferences
- Includes proper labeling for each column and selected values

## Related Components

- **SafPickerColumn**: Individual picker column component
- **SafPickerOption**: Individual picker option component
- **SafSelect**: Dropdown selection component
- **SafDatePicker**: Specialized date picker component
- **SafTimePicker**: Specialized time picker component
- **SafModal**: Modal container for picker overlays

## Notes

- SafPicker automatically handles touch and mouse interactions
- The component supports both controlled and uncontrolled usage patterns
- Column dependencies are handled through cascading updates
- Infinite scrolling creates seamless looping for appropriate data types
- Custom formatters allow rich content rendering within options
- The component optimizes performance through virtual scrolling for large datasets
- Momentum scrolling provides natural interaction feel on touch devices
- Column widths can be specified as percentages, pixels, or flexible values
