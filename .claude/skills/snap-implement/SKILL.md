---
name: snap-implement
description: Full UI implementation workflow - orchestrates planning, coding, review, and accessibility audit for Angular pages using Saffron Design System. Use this agent when implementing a new UI page or component from a PBI.
---

# /snap-implement - SNAP Code Implementation Workflow

Orchestrates the full implementation workflow for Angular pages using the Saffron Design System.

## Usage
```
/snap-implement [Azure DevOps URL]
/snap-implement https://dev.azure.com/tr/LegalTracker/_workitems/edit/12345
```

## Workflow

### Step 1: Requirements Gathering
Delegate to the **snap-planner** agent:
- Fetch the PBI from Azure DevOps using the URL provided
- Extract the Figma design URL from the PBI description
- Analyze the Figma design
- Create a detailed implementation plan with section breakdown
- Map all UI elements to Saffron components

**APPROVAL GATE:** Present the plan to the user. Do NOT proceed until the user approves.

### Step 2: Codebase Context
Delegate to the **snap-codebase-context** agent:
- Find similar existing components in the codebase
- Identify reusable services, components, and patterns
- Determine the correct module and file structure

### Step 3: Section-by-Section Implementation
For each section in the approved plan:

1. Delegate to the **snap-coder** agent to generate:
   - Component TypeScript (OnPush, constructor injection, destroy$)
   - Template HTML (Saffron components with accessibility attributes)
   - Styles SCSS (Saffron design tokens only)
   - Module updates (SharedModule, CUSTOM_ELEMENTS_SCHEMA)
   - Service and model files as needed

2. Run quality checks:
   - Verify no hardcoded hex colors or px values in SCSS
   - Verify @core/@shared path aliases used correctly
   - Verify build compiles: `ng build`
   - Verify lint passes: `ng lint`

3. **APPROVAL GATE:** Present generated code for the section. Wait for approval before next section.

### Step 4: Test Generation
Delegate to the **snap-test-generator** agent:
- Generate Jasmine unit tests for all new components
- Generate tests for all new services
- Run tests: `ng test --watch=false`

### Step 5: Code Review
Delegate to the **snap-reviewer** agent:
- Review all generated code against Legal Tracker conventions
- Verify Saffron component usage
- Check visual fidelity against Figma design
- Validate code quality standards

### Step 6: Accessibility Audit
Delegate to the **snap-a11y-auditor** agent:
- Audit all templates for WCAG 2.1 AA compliance
- Verify all ARIA attributes are present
- Check keyboard navigation support
- Validate focus management

### Step 7: Remediation
If review or audit finds critical issues:
- Delegate back to **snap-coder** to fix issues
- Re-run the relevant checks
- Repeat until all checks pass

### Step 8: Final Summary
Present a completion report:
```
## Implementation Complete: [PBI Title] (#[ID])

### Files Created/Modified
- [list of all files]

### Quality Results
- Build: PASS/FAIL
- Lint: PASS/FAIL
- Tests: [X/Y passing]
- Review: APPROVED/NEEDS REVISION
- Accessibility: PASS/FAIL

### Acceptance Criteria Coverage
- [x] Criterion 1 - covered by [section]
- [x] Criterion 2 - covered by [section]
...

### Next Steps
- [ ] Manual visual review
- [ ] Integration testing
- [ ] PR creation
```

**FINAL APPROVAL GATE:** Present the summary. Ask if the user wants to create a PR or make any adjustments.
