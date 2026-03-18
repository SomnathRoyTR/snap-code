---
name: saffron-patterns
description: Saffron Design System component reference and patterns
user_invocable: false
---

# Saffron Component Patterns

This skill provides quick reference to Saffron Design System component usage patterns.

## Reference
See `instructions/saffron-component-mapping.md` for the full component mapping guide.
See `instructions/saffron-mcp-server.md` for MCP server integration details.

## Key Rules
1. **Always use MCP tools** to verify component names and APIs before generating code
2. **Never generate Saffron code from memory** - always verify with `get-saffron-code`
3. **Include accessibility attributes** from `get-saffron-a11y-attributes` for every component
4. **Use design tokens** from `get-saffron-tokens` instead of hardcoded CSS values
5. **Angular naming**: kebab-case with `saf-` prefix (e.g., `saf-button`, `saf-text-field`)
6. **Shadow DOM**: Use CSS custom properties or `::part()` for styling

## Common Component Patterns

### Form Pattern
```html
<saf-card>
  <saf-label>Field Label</saf-label>
  <saf-text-field [value]="fieldValue" (valueChange)="onFieldChange($event)"
    aria-label="Field description"></saf-text-field>
  <saf-button appearance="primary" (click)="onSubmit()">{{ submitLabel }}</saf-button>
</saf-card>
```

### Data Grid Pattern
```html
<saf-card>
  <saf-toolbar>
    <saf-search (valueChange)="onSearch($event)"></saf-search>
    <saf-button (click)="onAdd()">{{ addLabel }}</saf-button>
  </saf-toolbar>
  <saf-grid [data]="gridData" (selectionChange)="onSelect($event)">
  </saf-grid>
  <saf-pager [total]="total" [pageSize]="pageSize"></saf-pager>
</saf-card>
```

### Dialog Pattern
```html
<saf-dialog [opened]="isOpen" (close)="onClose()">
  <saf-dialog-titlebar>{{ dialogTitle }}</saf-dialog-titlebar>
  <div class="dialog-content">
    <!-- content -->
  </div>
  <saf-dialog-actions>
    <saf-button appearance="secondary" (click)="onCancel()">{{ cancelLabel }}</saf-button>
    <saf-button appearance="primary" (click)="onConfirm()">{{ confirmLabel }}</saf-button>
  </saf-dialog-actions>
</saf-dialog>
```
