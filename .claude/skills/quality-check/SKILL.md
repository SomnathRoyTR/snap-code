---
name: quality-check
description: Automated quality gates for SNAP Code implementations
user_invocable: true
---

# /quality-check - SNAP Code Quality Gates

Runs automated quality checks on generated Angular code.

## Usage
```
/quality-check
/quality-check [file-or-directory-path]
```

## Quality Gates

### 1. Token Compliance Check
Scan SCSS files for hardcoded values that should use Saffron tokens:
- Hex color codes (e.g., `#ffffff`, `#0d6efd`)
- Hardcoded pixel values for common spacings (e.g., `padding: 16px`)
- Hardcoded font sizes and weights

**How to check:**
```bash
# Find hardcoded hex colors in SCSS files
grep -rn '#[0-9a-fA-F]\{3,8\}' --include="*.scss" [path]

# Find hardcoded pixel values in padding/margin
grep -rn 'padding:\s*[0-9]' --include="*.scss" [path]
grep -rn 'margin:\s*[0-9]' --include="*.scss" [path]
```

### 2. Import Path Check
Verify `@core/*` and `@shared/*` aliases are used instead of relative paths:
```bash
# Find relative imports crossing module boundaries
grep -rn "from '\.\./\.\./\.\." --include="*.ts" [path]
```

### 3. Convention Compliance Check
Verify Legal Tracker conventions:
```bash
# Check for standalone components (should not exist)
grep -rn 'standalone:\s*true' --include="*.ts" [path]

# Check for inject() usage (should use constructor injection)
grep -rn '= inject(' --include="*.ts" [path]

# Check for missing OnPush
grep -rn 'changeDetection:' --include="*.ts" [path]
```

### 4. Build Check
```bash
cd Development/WebApplication/Angular && ng build --configuration=production
```

### 5. Lint Check
```bash
cd Development/WebApplication/Angular && ng lint
```

### 6. Test Check
```bash
cd Development/WebApplication/Angular && ng test --watch=false
```

## Output Format
```
## Quality Check Results

### Token Compliance: PASS/FAIL
- [Findings if any]

### Import Paths: PASS/FAIL
- [Findings if any]

### Convention Compliance: PASS/FAIL
- [Findings if any]

### Build: PASS/FAIL
### Lint: PASS/FAIL
### Tests: [X/Y passing]

### Overall: PASS/FAIL
```
