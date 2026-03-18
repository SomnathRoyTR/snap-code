# Legal Tracker Angular Conventions

## Overview
This document defines the Angular coding conventions used in the Legal Tracker application. All generated code MUST follow these patterns for consistency with the existing codebase.

## Component Conventions

### Change Detection
All components MUST use `OnPush` change detection strategy:
```typescript
@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styleUrls: ['./my-component.component.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush
})
```

### Module-Based Architecture (NOT Standalone)
Components use `standalone: false` (NgModules pattern, NOT standalone components):
```typescript
@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  changeDetection: ChangeDetectionStrategy.OnPush
  // NO standalone: true
})
```

Components are declared in their feature module:
```typescript
@NgModule({
  declarations: [MyComponent],
  imports: [SharedModule],
  exports: [MyComponent]
})
export class MyFeatureModule {}
```

### Dependency Injection
Use constructor injection (NOT the `inject()` function):
```typescript
// CORRECT
constructor(
  private readonly myService: MyService,
  private readonly cdr: ChangeDetectorRef,
  private readonly resourcesService: ResourcesService
) {}

// WRONG - do not use inject()
private myService = inject(MyService);
```

## Path Aliases
Use TypeScript path aliases defined in `tsconfig.json`:
- `@core/*` → `src/app/core/*`
- `@shared/*` → `src/app/shared/*`

```typescript
// CORRECT
import { MyService } from '@core/services/my.service';
import { SharedComponent } from '@shared/components/shared.component';

// WRONG - relative paths crossing module boundaries
import { MyService } from '../../../core/services/my.service';
```

## Subscription Management
Use the `destroy$` Subject pattern for cleaning up subscriptions:
```typescript
export class MyComponent implements OnInit, OnDestroy {
  private destroy$ = new Subject<void>();

  ngOnInit(): void {
    this.myService.getData()
      .pipe(takeUntil(this.destroy$))
      .subscribe(data => {
        this.data = data;
        this.cdr.markForCheck();
      });
  }

  ngOnDestroy(): void {
    this.destroy$.next();
    this.destroy$.complete();
  }
}
```

## Change Detection with Async Data
After receiving async data with `OnPush`, always call `markForCheck()`:
```typescript
this.myService.getData()
  .pipe(takeUntil(this.destroy$))
  .subscribe(data => {
    this.data = data;
    this.cdr.markForCheck(); // REQUIRED with OnPush
  });
```

## Internationalization (i18n)
Use `ResourcesService` for all user-facing strings:
```typescript
constructor(private readonly resourcesService: ResourcesService) {}

ngOnInit(): void {
  this.buttonLabel = this.resourcesService.get('MyComponent.SaveButton');
  this.pageTitle = this.resourcesService.get('MyComponent.Title');
}
```

In templates:
```html
<saf-button>{{ buttonLabel }}</saf-button>
```

## SharedModule
Feature modules MUST import `SharedModule` for access to shared components, directives, and pipes:
```typescript
@NgModule({
  imports: [
    CommonModule,
    SharedModule,
    MyFeatureRoutingModule
  ],
  declarations: [MyFeatureComponent]
})
export class MyFeatureModule {}
```

## Saffron Web Components (Shadow DOM)
Saffron components use shadow DOM. Key patterns:

### CUSTOM_ELEMENTS_SCHEMA
Modules using Saffron web components need:
```typescript
@NgModule({
  schemas: [CUSTOM_ELEMENTS_SCHEMA]
})
```

### Styling Shadow DOM
Use `::part()` selectors or Saffron CSS custom properties:
```scss
// Using CSS custom properties (preferred)
saf-button {
  --saf-button-background: var(--saffron-color-primary);
}

// Using ::part() selector
saf-text-field::part(input) {
  font-size: var(--saffron-font-size-base);
}
```

### Property Binding
Use Angular property binding for Saffron component properties:
```html
<saf-text-field [value]="myValue" (valueChange)="onValueChange($event)"></saf-text-field>
<saf-button [disabled]="isDisabled" (click)="onSubmit()">Save</saf-button>
```

## Feature Module Structure
```
modules/
  my-feature/
    my-feature.module.ts
    my-feature-routing.module.ts
    components/
      my-feature-list/
        my-feature-list.component.ts
        my-feature-list.component.html
        my-feature-list.component.scss
        my-feature-list.component.spec.ts
      my-feature-detail/
        ...
    services/
      my-feature.service.ts
    models/
      my-feature.model.ts
```

## Testing Conventions
- Test framework: Jasmine + Karma
- Test file naming: `*.component.spec.ts`, `*.service.spec.ts`
- Use `TestBed` for component testing
- Mock services with Jasmine spies
- Follow Arrange-Act-Assert pattern

```typescript
describe('MyComponent', () => {
  let component: MyComponent;
  let fixture: ComponentFixture<MyComponent>;
  let myServiceSpy: jasmine.SpyObj<MyService>;

  beforeEach(async () => {
    myServiceSpy = jasmine.createSpyObj('MyService', ['getData']);
    myServiceSpy.getData.and.returnValue(of(mockData));

    await TestBed.configureTestingModule({
      declarations: [MyComponent],
      imports: [SharedModule],
      providers: [
        { provide: MyService, useValue: myServiceSpy }
      ],
      schemas: [CUSTOM_ELEMENTS_SCHEMA]
    }).compileComponents();

    fixture = TestBed.createComponent(MyComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```
