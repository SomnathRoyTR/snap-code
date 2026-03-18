---
name: design-tokens
description: Saffron design token mapping reference
user_invocable: false
---

# Saffron Design Token Reference

This skill provides quick reference for mapping CSS values to Saffron design tokens.

## Reference
See `instructions/design-tokens.md` for the full token mapping guide.

## Key Rules
1. **Never hardcode** colors, font sizes, spacing, or shadows in SCSS
2. **Always use** `var(--saffron-*)` CSS custom properties
3. **Verify tokens** with `get-saffron-tokens` MCP tool before using
4. **Common mistakes**: Using `#ffffff` instead of `var(--saffron-color-background)`, using `16px` instead of `var(--saffron-font-size-base)`

## Quick Token Reference

### Colors
- Primary: `--saffron-color-primary`
- Text: `--saffron-color-text-primary`, `--saffron-color-text-secondary`
- Background: `--saffron-color-background`, `--saffron-color-background-secondary`
- Error: `--saffron-color-error`
- Success: `--saffron-color-success`
- Border: `--saffron-color-border`

### Spacing
- `4px` -> `--saffron-spacing-xs`
- `8px` -> `--saffron-spacing-sm`
- `12px` -> `--saffron-spacing-md`
- `16px` -> `--saffron-spacing-lg`
- `24px` -> `--saffron-spacing-xl`
- `32px` -> `--saffron-spacing-2xl`

### Typography
- `14px` -> `--saffron-font-size-sm`
- `16px` -> `--saffron-font-size-base`
- `20px` -> `--saffron-font-size-lg`
- `24px` -> `--saffron-font-size-xl`
