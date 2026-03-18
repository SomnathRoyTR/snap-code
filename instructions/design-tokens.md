# Saffron Design Tokens Reference

## Overview
This document maps common CSS values to Saffron design tokens. Always use Saffron tokens instead of hardcoded values to ensure design consistency and theme support.

## How to Use Tokens
Use CSS custom properties in SCSS files:
```scss
.my-class {
  color: var(--saffron-color-text-primary);
  font-size: var(--saffron-font-size-base);
  padding: var(--saffron-spacing-md);
}
```

## Color Tokens

### Primary Colors
| CSS Value | Saffron Token |
|---|---|
| `#0d6efd` | `--saffron-color-primary` |
| `#0b5ed7` | `--saffron-color-primary-hover` |
| `#0a58ca` | `--saffron-color-primary-active` |

### Text Colors
| CSS Value | Saffron Token |
|---|---|
| `#212529` | `--saffron-color-text-primary` |
| `#6c757d` | `--saffron-color-text-secondary` |
| `#adb5bd` | `--saffron-color-text-disabled` |
| `#ffffff` | `--saffron-color-text-inverse` |
| `#0d6efd` | `--saffron-color-text-link` |

### Background Colors
| CSS Value | Saffron Token |
|---|---|
| `#ffffff` | `--saffron-color-background` |
| `#f8f9fa` | `--saffron-color-background-secondary` |
| `#e9ecef` | `--saffron-color-background-tertiary` |

### Status Colors
| CSS Value | Saffron Token |
|---|---|
| `#198754` | `--saffron-color-success` |
| `#dc3545` | `--saffron-color-error` |
| `#ffc107` | `--saffron-color-warning` |
| `#0dcaf0` | `--saffron-color-info` |

### Border Colors
| CSS Value | Saffron Token |
|---|---|
| `#dee2e6` | `--saffron-color-border` |
| `#0d6efd` | `--saffron-color-border-focus` |
| `#dc3545` | `--saffron-color-border-error` |

## Typography Tokens

### Font Size
| CSS Value | Saffron Token |
|---|---|
| `12px` | `--saffron-font-size-xs` |
| `14px` | `--saffron-font-size-sm` |
| `16px` | `--saffron-font-size-base` |
| `18px` | `--saffron-font-size-md` |
| `20px` | `--saffron-font-size-lg` |
| `24px` | `--saffron-font-size-xl` |
| `32px` | `--saffron-font-size-2xl` |

### Font Weight
| CSS Value | Saffron Token |
|---|---|
| `300` | `--saffron-font-weight-light` |
| `400` | `--saffron-font-weight-regular` |
| `500` | `--saffron-font-weight-medium` |
| `600` | `--saffron-font-weight-semibold` |
| `700` | `--saffron-font-weight-bold` |

### Line Height
| CSS Value | Saffron Token |
|---|---|
| `1.2` | `--saffron-line-height-tight` |
| `1.5` | `--saffron-line-height-base` |
| `1.75` | `--saffron-line-height-relaxed` |

## Spacing Tokens

| CSS Value | Saffron Token |
|---|---|
| `0` | `--saffron-spacing-none` |
| `4px` | `--saffron-spacing-xs` |
| `8px` | `--saffron-spacing-sm` |
| `12px` | `--saffron-spacing-md` |
| `16px` | `--saffron-spacing-lg` |
| `24px` | `--saffron-spacing-xl` |
| `32px` | `--saffron-spacing-2xl` |
| `48px` | `--saffron-spacing-3xl` |
| `64px` | `--saffron-spacing-4xl` |

## Border Radius Tokens

| CSS Value | Saffron Token |
|---|---|
| `2px` | `--saffron-border-radius-sm` |
| `4px` | `--saffron-border-radius-base` |
| `8px` | `--saffron-border-radius-md` |
| `16px` | `--saffron-border-radius-lg` |
| `50%` | `--saffron-border-radius-circle` |

## Shadow Tokens

| CSS Value | Saffron Token |
|---|---|
| `0 1px 2px rgba(0,0,0,0.05)` | `--saffron-shadow-sm` |
| `0 4px 6px rgba(0,0,0,0.1)` | `--saffron-shadow-base` |
| `0 10px 15px rgba(0,0,0,0.1)` | `--saffron-shadow-md` |
| `0 20px 25px rgba(0,0,0,0.15)` | `--saffron-shadow-lg` |

## Z-Index Tokens

| CSS Value | Saffron Token |
|---|---|
| `100` | `--saffron-z-index-dropdown` |
| `200` | `--saffron-z-index-sticky` |
| `300` | `--saffron-z-index-fixed` |
| `400` | `--saffron-z-index-modal-backdrop` |
| `500` | `--saffron-z-index-modal` |
| `600` | `--saffron-z-index-popover` |
| `700` | `--saffron-z-index-tooltip` |

## Transition Tokens

| CSS Value | Saffron Token |
|---|---|
| `150ms ease-in-out` | `--saffron-transition-fast` |
| `250ms ease-in-out` | `--saffron-transition-base` |
| `350ms ease-in-out` | `--saffron-transition-slow` |

## MCP Server Integration
Use `get-saffron-tokens` MCP tool to find the correct token for any CSS value:
```
get-saffron-tokens(["#0d6efd", "16px", "8px"])
```
This returns the exact Saffron token names for the given values.

**Always verify token names with the MCP server before using them in code.**
