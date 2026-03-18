---
name: tracker-conventions
description: Legal Tracker Angular coding conventions reference
user_invocable: false
---

# Legal Tracker Angular Conventions

This skill provides quick reference to Legal Tracker Angular coding conventions.

## Reference
See `instructions/tracker-conventions.md` for the full conventions guide.

## Mandatory Conventions Checklist
- [ ] `ChangeDetectionStrategy.OnPush` on ALL components
- [ ] `standalone: false` (NgModules, NOT standalone components)
- [ ] Constructor injection (NOT `inject()` function)
- [ ] `@core/*` and `@shared/*` path aliases
- [ ] `destroy$` Subject with `takeUntil` for subscription cleanup
- [ ] `ResourcesService` for all user-facing strings (i18n)
- [ ] `ChangeDetectorRef.markForCheck()` after async data loads
- [ ] `SharedModule` imported in feature modules
- [ ] `CUSTOM_ELEMENTS_SCHEMA` in modules with Saffron web components

## Quick Reference

### Component Skeleton
```typescript
@Component({
  selector: 'app-feature',
  templateUrl: './feature.component.html',
  styleUrls: ['./feature.component.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class FeatureComponent implements OnInit, OnDestroy {
  private destroy$ = new Subject<void>();

  constructor(
    private readonly cdr: ChangeDetectorRef,
    private readonly resourcesService: ResourcesService
  ) {}

  ngOnInit(): void {
    // subscribe with takeUntil(this.destroy$)
  }

  ngOnDestroy(): void {
    this.destroy$.next();
    this.destroy$.complete();
  }
}
```

### Module Skeleton
```typescript
@NgModule({
  declarations: [FeatureComponent],
  imports: [CommonModule, SharedModule, FeatureRoutingModule],
  schemas: [CUSTOM_ELEMENTS_SCHEMA]
})
export class FeatureModule {}
```
