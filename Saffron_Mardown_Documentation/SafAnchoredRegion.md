# SafAnchoredRegion

A flexible positioning component that anchors content relative to another element with intelligent positioning and viewport constraints. SafAnchoredRegion is ideal for tooltips, dropdowns, popover menus, and any floating content that needs to maintain spatial relationships with anchor elements.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `anchor` | `string` | `''` | The HTML ID of the anchor element this region is positioned relative to |
| `viewport` | `string` | `''` | The ID of the element that serves as the viewport for the region |
| `horizontalPositioningMode` | `'uncontrolled' \| 'locktodefault' \| 'dynamic'` | `'uncontrolled'` | Logic for determining horizontal placement |
| `horizontalDefaultPosition` | `'start' \| 'end' \| 'left' \| 'right' \| 'center' \| 'unset'` | `'unset'` | Default horizontal position relative to the anchor element |
| `horizontalViewportLock` | `boolean` | `false` | Whether the region remains in the viewport (detaches from anchor) on horizontal axis |
| `horizontalInset` | `boolean` | `false` | Whether the region overlaps the anchor on the horizontal axis |
| `horizontalThreshold` | `number` | - | How narrow the space has to be before widest area is selected for layout |
| `horizontalScaling` | `'anchor' \| 'content' \| 'fill'` | `'content'` | Defines how the width of the region is calculated |
| `verticalPositioningMode` | `'uncontrolled' \| 'locktodefault' \| 'dynamic'` | `'uncontrolled'` | Logic for determining vertical placement |
| `verticalDefaultPosition` | `'top' \| 'bottom' \| 'center' \| 'unset'` | `'unset'` | Default vertical position relative to the anchor element |
| `verticalViewportLock` | `boolean` | `false` | Whether the region remains in the viewport (detaches from anchor) on vertical axis |
| `verticalInset` | `boolean` | `false` | Whether the region overlaps the anchor on the vertical axis |
| `verticalThreshold` | `number` | - | How short the space has to be before tallest area is selected for layout |
| `verticalScaling` | `'anchor' \| 'content' \| 'fill'` | `'content'` | Defines how the height of the region is calculated |
| `autoUpdateMode` | `'anchor' \| 'auto'` | `'anchor'` | Defines if the component updates its position automatically |
| `fixedPlacement` | `boolean` | `false` | Whether the region uses fixed positioning |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onLoaded` | `CustomEvent` | Fires when the region is loaded and visible |
| `onPositionChange` | `CustomEvent` | Fires when the position has changed |

### Examples

#### Basic Dropdown Menu
```jsx
import { SafAnchoredRegion, SafButton, SafMenu, SafMenuItem } from '@saffron/core-components/react';

function DropdownExample() {
  const [isOpen, setIsOpen] = useState(false);
  const anchorId = useId();

  return (
    <div>
      {/* Anchor button */}
      <SafButton 
        id={anchorId}
        onClick={() => setIsOpen(!isOpen)}
      >
        Open Menu
      </SafButton>
      
      {/* Anchored menu that positions itself relative to the button */}
      {isOpen && (
        <SafAnchoredRegion
          anchor={anchorId}
          horizontalPositioningMode="dynamic"
          verticalPositioningMode="dynamic"
          horizontalDefaultPosition="start"
          verticalDefaultPosition="bottom"
          horizontalViewportLock={true}
          verticalViewportLock={true}
        >
          <SafMenu aria-label="Dropdown Menu">
            <SafMenuItem>Menu Item 1</SafMenuItem>
            <SafMenuItem>Menu Item 2</SafMenuItem>
            <SafMenuItem>Menu Item 3</SafMenuItem>
          </SafMenu>
        </SafAnchoredRegion>
      )}
    </div>
  );
}
```

#### Tooltip with Smart Positioning
```jsx
import { SafAnchoredRegion, SafButton } from '@saffron/core-components/react';

function TooltipExample() {
  const [showTooltip, setShowTooltip] = useState(false);
  const buttonId = useId();

  return (
    <div>
      <SafButton
        id={buttonId}
        onMouseEnter={() => setShowTooltip(true)}
        onMouseLeave={() => setShowTooltip(false)}
        onFocus={() => setShowTooltip(true)}
        onBlur={() => setShowTooltip(false)}
      >
        Hover for tooltip
      </SafButton>
      
      {showTooltip && (
        <SafAnchoredRegion
          anchor={buttonId}
          horizontalPositioningMode="dynamic"
          verticalPositioningMode="dynamic"
          horizontalDefaultPosition="center"
          verticalDefaultPosition="top"
          horizontalViewportLock={true}
          verticalViewportLock={true}
          horizontalScaling="content"
          verticalScaling="content"
        >
          <div className="tooltip">
            This is a helpful tooltip that positions itself intelligently
          </div>
        </SafAnchoredRegion>
      )}
    </div>
  );
}
```

#### Advanced Popover with Viewport Constraints
```jsx
import { SafAnchoredRegion, SafButton, SafCard } from '@saffron/core-components/react';

function PopoverExample() {
  const [isOpen, setIsOpen] = useState(false);
  const triggerRef = useRef(null);
  const popoverId = useId();

  return (
    <div>
      <SafButton
        ref={triggerRef}
        id={popoverId}
        onClick={() => setIsOpen(!isOpen)}
        aria-expanded={isOpen}
        aria-haspopup="dialog"
      >
        Open Popover
      </SafButton>
      
      {isOpen && (
        <SafAnchoredRegion
          anchor={popoverId}
          horizontalPositioningMode="dynamic"
          verticalPositioningMode="dynamic"
          horizontalDefaultPosition="start"
          verticalDefaultPosition="bottom"
          horizontalViewportLock={true}
          verticalViewportLock={true}
          horizontalThreshold={200}
          verticalThreshold={150}
          onPositionChange={(e) => console.log('Position changed:', e.detail)}
        >
          <SafCard>
            <div style={{ padding: '16px', minWidth: '200px' }}>
              <h3>Popover Content</h3>
              <p>This popover adjusts its position based on available space.</p>
              <SafButton 
                appearance="secondary" 
                onClick={() => setIsOpen(false)}
              >
                Close
              </SafButton>
            </div>
          </SafCard>
        </SafAnchoredRegion>
      )}
    </div>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `anchor` | `string` | `''` | The HTML ID of the anchor element this region is positioned relative to |
| `viewport` | `string` | `''` | The ID of the element that serves as the viewport for the region |
| `horizontalPositioningMode` | `'uncontrolled' \| 'locktodefault' \| 'dynamic'` | `'uncontrolled'` | Logic for determining horizontal placement |
| `horizontalDefaultPosition` | `'start' \| 'end' \| 'left' \| 'right' \| 'center' \| 'unset'` | `'unset'` | Default horizontal position relative to the anchor element |
| `horizontalViewportLock` | `boolean` | `false` | Whether the region remains in the viewport (detaches from anchor) on horizontal axis |
| `horizontalInset` | `boolean` | `false` | Whether the region overlaps the anchor on the horizontal axis |
| `horizontalThreshold` | `number` | - | How narrow the space has to be before widest area is selected for layout |
| `horizontalScaling` | `'anchor' \| 'content' \| 'fill'` | `'content'` | Defines how the width of the region is calculated |
| `verticalPositioningMode` | `'uncontrolled' \| 'locktodefault' \| 'dynamic'` | `'uncontrolled'` | Logic for determining vertical placement |
| `verticalDefaultPosition` | `'top' \| 'bottom' \| 'center' \| 'unset'` | `'unset'` | Default vertical position relative to the anchor element |
| `verticalViewportLock` | `boolean` | `false` | Whether the region remains in the viewport (detaches from anchor) on vertical axis |
| `verticalInset` | `boolean` | `false` | Whether the region overlaps the anchor on the vertical axis |
| `verticalThreshold` | `number` | - | How short the space has to be before tallest area is selected for layout |
| `verticalScaling` | `'anchor' \| 'content' \| 'fill'` | `'content'` | Defines how the height of the region is calculated |
| `autoUpdateMode` | `'anchor' \| 'auto'` | `'anchor'` | Defines if the component updates its position automatically |
| `fixedPlacement` | `boolean` | `false` | Whether the region uses fixed positioning |
| `density` | `'extra-compact' \| 'compact' \| 'standard' \| 'relaxed' \| 'inherit'` | `'inherit'` | Spacing in and around the component |

### Events

| Output | Type | Description |
|--------|------|-------------|
| `loaded` | `EventEmitter<CustomEvent>` | Fires when the region is loaded and visible |
| `positionchange` | `EventEmitter<CustomEvent>` | Fires when the position has changed |

### Examples

#### Basic Dropdown Menu
```html
<!-- Anchor button -->
<saf-button #anchorButton (click)="toggleMenu()">
  Open Menu
</saf-button>

<!-- Anchored menu that positions itself relative to the button -->
<saf-anchored-region
  *ngIf="isMenuOpen"
  [anchor]="anchorButton.id"
  horizontalPositioningMode="dynamic"
  verticalPositioningMode="dynamic"
  horizontalDefaultPosition="start"
  verticalDefaultPosition="bottom"
  [horizontalViewportLock]="true"
  [verticalViewportLock]="true">
  <saf-menu aria-label="Dropdown Menu">
    <saf-menu-item>Menu Item 1</saf-menu-item>
    <saf-menu-item>Menu Item 2</saf-menu-item>
    <saf-menu-item>Menu Item 3</saf-menu-item>
  </saf-menu>
</saf-anchored-region>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-dropdown-example',
  templateUrl: './dropdown-example.component.html'
})
export class DropdownExampleComponent {
  isMenuOpen = false;

  toggleMenu() {
    this.isMenuOpen = !this.isMenuOpen;
  }
}
```

#### Tooltip with Smart Positioning
```html
<saf-button
  #tooltipAnchor
  (mouseenter)="showTooltip = true"
  (mouseleave)="showTooltip = false"
  (focus)="showTooltip = true"
  (blur)="showTooltip = false">
  Hover for tooltip
</saf-button>

<saf-anchored-region
  *ngIf="showTooltip"
  [anchor]="tooltipAnchor.id"
  horizontalPositioningMode="dynamic"
  verticalPositioningMode="dynamic"
  horizontalDefaultPosition="center"
  verticalDefaultPosition="top"
  [horizontalViewportLock]="true"
  [verticalViewportLock]="true"
  horizontalScaling="content"
  verticalScaling="content">
  <div class="tooltip">
    This is a helpful tooltip that positions itself intelligently
  </div>
</saf-anchored-region>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-tooltip-example',
  templateUrl: './tooltip-example.component.html',
  styleUrls: ['./tooltip-example.component.scss']
})
export class TooltipExampleComponent {
  showTooltip = false;
}
```

#### Advanced Popover with Event Handling
```html
<saf-button
  #popoverTrigger
  (click)="togglePopover()"
  [attr.aria-expanded]="isPopoverOpen"
  attr.aria-haspopup="dialog">
  Open Popover
</saf-button>

<saf-anchored-region
  *ngIf="isPopoverOpen"
  [anchor]="popoverTrigger.id"
  horizontalPositioningMode="dynamic"
  verticalPositioningMode="dynamic"
  horizontalDefaultPosition="start"
  verticalDefaultPosition="bottom"
  [horizontalViewportLock]="true"
  [verticalViewportLock]="true"
  [horizontalThreshold]="200"
  [verticalThreshold]="150"
  (positionchange)="onPositionChange($event)">
  <saf-card>
    <div style="padding: 16px; min-width: 200px;">
      <h3>Popover Content</h3>
      <p>This popover adjusts its position based on available space.</p>
      <saf-button
        appearance="secondary"
        (click)="closePopover()">
        Close
      </saf-button>
    </div>
  </saf-card>
</saf-anchored-region>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-popover-example',
  templateUrl: './popover-example.component.html'
})
export class PopoverExampleComponent {
  isPopoverOpen = false;

  togglePopover() {
    this.isPopoverOpen = !this.isPopoverOpen;
  }

  closePopover() {
    this.isPopoverOpen = false;
  }

  onPositionChange(event: CustomEvent) {
    console.log('Position changed:', event.detail);
  }
}
```

## Best Practices

- **Use unique anchor IDs**: Ensure each anchor element has a unique ID to avoid positioning conflicts.
- **Set appropriate positioning modes**: Use `'dynamic'` for automatic smart positioning, `'locktodefault'` to force a specific position.
- **Enable viewport lock**: Set `horizontalViewportLock` and `verticalViewportLock` to `true` for dropdowns and tooltips to keep them visible.
- **Consider thresholds**: Set `horizontalThreshold` and `verticalThreshold` to control when dynamic positioning kicks in.
- **Handle events**: Listen to `positionchange` events to update dependent UI or accessibility attributes.
- **Accessibility**: Ensure proper ARIA attributes on anchor elements (`aria-expanded`, `aria-haspopup`) for interactive regions.
- **Performance**: Use `autoUpdateMode="anchor"` for better performance unless you need constant position updates.

## Notes

- SafAnchoredRegion automatically handles window resize and scroll events to maintain proper positioning.
- The component uses intelligent positioning algorithms to avoid viewport edges and optimize space usage.
- When `fixedPlacement` is true, the region uses CSS `position: fixed` instead of absolute positioning.
- Scaling modes affect size calculation: `'content'` sizes to content, `'anchor'` matches anchor size, `'fill'` fills available space.
- Inset positioning allows the region to overlap the anchor element, useful for certain dropdown patterns.
- The component works with both mouse and keyboard interactions for accessibility compliance.
