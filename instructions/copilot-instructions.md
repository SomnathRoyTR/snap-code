## **Instructions**
You will build one or more web pages within an existing codebase that strictly uses the **Saffron Design System**. The task involves adhering to scalability, maintainability, accessibility, and responsiveness standards while ensuring compliance with TypeScript safety and collaborative workflows.

**For Saffron component information, use the [Saffron MCP Server](./saffron-mcp-server.md)** to access:
- Production-ready code examples
- Component accessibility attributes
- HTML to Saffron component mappings
- Design token information
- Visual component screenshots
 
### **Ultimate Objective**
1. Transform the provided UI designs, user requirements, and APIs into components and layouts using the **Saffron**.
2. Collaboratively progress through incremental stages, ensuring alignment and approval for each step.
 
---
 
## **Steps to Follow**

### **Step 0: Create Todo List**
After gathering the initial requirements, create a comprehensive todo list to track progress through all implementation phases. This list should be updated after each completed step.

#### Example Todo List Format:
```
**IMPLEMENTATION TODO LIST:**

Step 1: Gather Input
  ☐ Collect PBI link/ID
  ☐ Review UI Design (Figma links)
  ☐ Document user requirements
  ☐ Identify data sources/APIs
  ☐ Confirm spacing preferences

Step 2: Figma Analysis & Layout Proposal
  ☐ Download ALL Figma images (ensure images, not JSON)
  ☐ Save Figma images to workspace
  ☐ Identify all UI components from images
  ☐ Create component inventory table
  ☐ Map each component to Saffron Design System
  ☐ Detect tables and determine implementation (saf-data-grid vs Wijmo)
  ☐ Extract visual specifications (colors, spacing, fonts, sizes)
  ☐ Map colors/fonts/spacing to Saffron design tokens
  ☐ Define layout sections
  ☐ Get user approval on layout and component mapping

Step 3: Component Mapping & Code Retrieval
  ☐ Use Saffron MCP to get component code for each mapped component
  ☐ Retrieve accessibility attributes for all components
  ☐ Get design token mappings
  ☐ For tables: Get complete Wijmo configuration (if selected)
  ☐ Document all component props and themes
  ☐ Confirm spacing between sections

Step 4: Incremental Implementation
  ☐ Section 1: [Name]
     ☐ Implement with Saffron components only
     ☐ Use design tokens for styling
     ☐ Build verification (no errors)
     ☐ Request user screenshot
     ☐ Compare screenshot with Figma image
     ☐ Fix discrepancies
     ☐ Get user approval
  ☐ Section 2: [Name]
     ☐ Implement with Saffron components only
     ☐ Use design tokens for styling
     ☐ Build verification (no errors)
     ☐ Request user screenshot
     ☐ Compare screenshot with Figma image
     ☐ Fix discrepancies
     ☐ Get user approval
  ☐ Section 3: [Name]
     ☐ [Same steps as above]
  [Add more sections as needed]

Step 5: Final Review & Visual Validation
  ☐ Request complete implementation screenshots
  ☐ Comprehensive visual comparison with ALL Figma images
  ☐ Create discrepancy report
  ☐ Fix all identified issues
  ☐ Re-validate with new screenshots
  ☐ Cross-browser testing
  ☐ Accessibility audit (WCAG 2.1 AA)
  ☐ Responsive design verification
  ☐ Performance check
  ☐ Final user approval
  ☐ Documentation complete
```

**Update this todo list after each completed task, marking items with ✓ when done.**

---

## **Step 1: Gather Input**
```
Hello! I'm here to help you implement your UI designs using the Saffron.
Could you provide the following details to get started?
• PBI link/ID (if applicable)
• Uploaded UI Design
• High-Level User Requirements
• Primary Data Sources / APIs

Additionally, confirm:
- **Should we maintain strict separation between different sections without any white spaces?**
- **If white spaces are necessary, which sections should include them, and at what spacing values?**

Once I have this information, I'll analyze your design and propose a layout structure using the Saffron components.
```
For pbi data processing, follow the steps under [azure-devops-instructions.md](./azure-devops.instructions.md) to ensure accurate retrieval and formatting of work item details.

For accessibility requirements and standards, refer to [sharepoint-instructions.md](./sharepoint-instructions.md) to access organizational accessibility guidelines and ensure compliance throughout the implementation process.

### **Step 2: Layout Proposal & Figma Analysis**

**CRITICAL: Follow the complete Figma workflow in [figma-instructions.md](./figma-instructions.md)**

This step requires:
1. **Download all Figma designs as images** (NOT JSON)
2. **MEASURE exact dimensions, colors, spacing, fonts from images**
3. **Visual component analysis** from downloaded images
4. **Component identification and cataloging with EXACT measurements**
5. **Saffron component mapping** for every UI element
6. **Table detection and implementation planning** (if tables present)

**PIXEL-PERFECT REQUIREMENT:** Every measurement must be exact. Use rulers, measurement tools, or pixel inspection to get precise values.

#### **Figma Image Download & Analysis**

For each Figma link provided:
```
Step 2A: DOWNLOAD FIGMA IMAGES
- Extract Figma file ID and node ID from URLs
- Use MCP server to fetch images (ensure image format, not JSON)
- Save images to workspace for analysis
- Confirm successful downloads before proceeding

Step 2B: VISUAL COMPONENT IDENTIFICATION
- Analyze downloaded images to identify ALL UI components
- Create component inventory: buttons, inputs, tables, cards, navigation, icons, typography, etc.
- Document component hierarchy and relationships
- Verify colors, spacing, fonts, sizes, positions, and other visual properties

Step 2C: SAFFRON COMPONENT MAPPING
For EACH identified component, map to Saffron Design System:
- Consult saffron_component_mapping.md for correct components
- Document mapping (e.g., "Primary Button" → "<saf-button appearance='primary'>")
- Use Saffron MCP server to retrieve component code and accessibility attributes
- Map all colors, fonts, and spacing to Saffron design tokens
```

#### **Table Detection & Implementation Planning**

**IF a table/grid is detected in the Figma images:**

1. Analyze table complexity and features
2. Search workspace for existing table implementations
3. **Ask user for table implementation preference:**

```
🔍 TABLE DETECTED in Figma design

I've identified a data table with [describe features from image].

Please specify which implementation to use:
   a) saf-data-grid (basic Saffron table - simple data display)
   b) Wijmo FlexGrid (advanced features - sorting, filtering, editing, etc.)
   c) Existing pattern from your codebase
   d) Custom implementation

If Wijmo selected, which features are needed?
   □ Sorting
   □ Filtering  
   □ Inline editing
   □ Grouping
   □ Pagination
   □ Export (Excel/CSV)
   □ Other: [specify]
```

4. **If Wijmo selected:** Use Saffron MCP server to get:
   - Complete Wijmo package imports
   - Full implementation code
   - Saffron integration patterns
   - All requested features configuration

#### **Similar Code Analysis**
- **Check for existing similar implementations:** Search the codebase for components or pages with similar layouts or functionality
- **If similar code is found:** Present it to the user as a reference and ask if they want to follow the same patterns
- **If no similar code is found:** Ask the user to provide reference implementations or preferred coding patterns from their existing codebase

#### **File Organization and Naming**
Ask the user about their preferred:
- **File structure:** Where should the new components/pages be placed? (e.g., `src/app/features/`, `src/components/`)
- **Naming conventions:** naming should be understood from existing naming (e.g., kebab-case, camelCase, PascalCase)
- **File organization:** Should components be grouped by feature, type, or other criteria?

#### **Layout Proposal with Saffron Components**

Analyze the downloaded Figma images and define the layout structure with Saffron component mappings:
 
#### Example Proposal:
```
**FIGMA ANALYSIS COMPLETE:**
✅ Downloaded 3 Figma images (desktop.png, component-details.png, mobile.png)
✅ Component inventory created with EXACT measurements
✅ Saffron components mapped

**LAYOUT PROPOSAL:**  
The page design includes the following sections:

1. **Header:** Full-width at the top
   - Figma: Navigation bar with logo, search, and user menu
   - EXACT MEASUREMENTS:
     * Height: 64px
     * Logo width: 120px
     * Search bar: 320px × 40px
     * Padding: 16px left/right
     * Background: #FFFFFF
   - Saffron: <saf-product-header> with <saf-search-input>
   - Components identified: Logo, Search bar, User avatar, Notification badge

2. **Sidebar:** Left-aligned vertical menu panel
   - EXACT MEASUREMENTS:
     * Width: 260px
     * Item height: 48px
     * Icon size: 20px
     * Padding: 12px 16px
     * Gap between items: 4px
     * Background: #F8F9FA
   - Saffron: <saf-side-nav> with <saf-icon> and <saf-text>
   - Components identified: Menu items, Icons, Active state indicator

3. **Main Content:** Responsive grid layout
   - EXACT MEASUREMENTS:
     * Container width: calc(100% - 260px)
     * Padding: 24px
     * Gap between cards: 16px
   - Figma: Data table with filters and action buttons
   - Saffron: <saf-data-grid> OR Wijmo FlexGrid (awaiting your selection)
   - Components identified: Table, Filter dropdowns, Action buttons, Pagination

**SAFFRON COMPONENT SUMMARY WITH EXACT SPECS:**
- Buttons: <saf-button>
  * Primary (140px × 40px): 2 instances
  * Secondary (120px × 40px): 3 instances
  * Font: 14px/600
- Inputs: <saf-text-field>
  * Search (320px × 40px): 1 instance
  * Filters (200px × 40px): 2 instances
  * Font: 14px/400
- Cards: <saf-card>
  * Dimensions: 360px × 240px
  * Padding: 20px
  * Border-radius: 8px
  * Shadow: 0 2px 8px rgba(0,0,0,0.1)

**Spacing Query:**  
Figma shows the following spacing:
- Header ↔ Sidebar: 0px (no gap)
- Sidebar ↔ Main Content: 0px (no gap)
- Between cards in grid: 16px horizontal, 20px vertical

Should I proceed with these EXACT measurements?
```
 
### **Step 3: Component Mapping**
Determine the specific **Saffron components** required for each layout section and include details about props, themes, and accessibility considerations. Confirm spacing preferences again with explicit questions.

For component mapping guidance and examples, refer to [saffron_component_mapping.md](./saffron_component_mapping.md) to ensure correct component selection and implementation patterns.

**For Saffron component details, use the MCP server tools (see [saffron-mcp-server.md](./saffron-mcp-server.md)):**
- Use `get-saffron-code` to generate component code examples
- Use `get-saffron-code-equivalent` to find Saffron equivalents for HTML elements
- Use `get-saffron-a11y-attributes` to get accessibility specifications
- Use `get-saffron-tokens` to find design tokens for CSS values

#### **PBI Analysis and Task Creation**
When a PBI (Product Backlog Item) link or ID is provided:

1. **Extract PBI Details:** Use the azure-devops tools to gather:
   - PBI title and description
   - Acceptance criteria
   - Requirements and specifications
   - Any linked tasks or sub-items

2. **Create Detailed Task List:** Based on the PBI analysis, break down the work into specific, actionable tasks:
   ```
   **DETAILED TASK BREAKDOWN FROM PBI:**
   
   **PBI:** [Title] - [ID]
   **Acceptance Criteria:**
   - [Criterion 1]
   - [Criterion 2]
   - [Criterion 3]
   
   **Implementation Tasks:**
   1. **Setup & Planning**
      - [ ] Analyze Figma design components
      - [ ] Map Saffron components to design elements
      - [ ] Define file structure and naming conventions
      - [ ] Identify data sources and API endpoints
   
   2. **Component Development**
      - [ ] Create [Component Name 1] with props: [list props]
      - [ ] Create [Component Name 2] with accessibility features
      - [ ] Implement responsive design for mobile/tablet/desktop
   
   3. **Integration & Testing**
      - [ ] Integrate components into main layout
      - [ ] Add unit tests for each component
      - [ ] Verify accessibility compliance (WCAG 2.1)
      - [ ] Test responsive breakpoints
   
   4. **Validation Against Acceptance Criteria**
      - [ ] Verify [Criterion 1] implementation
      - [ ] Verify [Criterion 2] implementation
      - [ ] Verify [Criterion 3] implementation
   
   5. **Final Review**
      - [ ] Code review and TypeScript safety check
      - [ ] Visual comparison with Figma design
      - [ ] Performance optimization
      - [ ] Documentation update
   ```

3. **Progress Tracking:** Update task completion status throughout implementation and reference specific acceptance criteria when validating each feature.
 
#### Example Component Mapping Proposal:
```
**COMPONENT MAPPING PROPOSAL:**  
- **Header Section:**  
   - Component: `<saf-product-header>`  
   - Props: `product-name="Legal tracker"`,`
   - Accessibility: Includes `aria-label`.
 
- **Sidebar Section:**  
   - Component: `<saf-side-nav>`  
   - Props: `open-aria-label=Expand side nav`
   - Accessibility: Supports keyboard navigation.
 
**Spacing Preferences:**  
Should white spaces be added between sections? Confirm specific spacing values (e.g., `margin: 10px`).
```
 
## **Step 4: Incremental Implementation**
1. Implement each section incrementally using **ONLY Saffron Design System components**. For Angular projects, follow Angular conventions:
   - Create a feature module if the page is a standalone area (ng generate module feature --routing).
   - Generate isolated components per section (ng generate component header --module=feature).
   - Use component-scoped styles via styleUrls and TypeScript-safe inputs/outputs.
   - Add unit tests using Jasmine/Karma (ng test) or Jest if configured.

2. **Use Saffron components exclusively** - NO native HTML elements (refer to saffron_component_mapping.md)

3. **For table implementations:**
   - If saf-data-grid: Use Saffron MCP to get complete code
   - If Wijmo: Use Saffron MCP to get full package imports, configuration, and all requested features

4. After implementing each section, prompt the user for feedback on spacing and component behavior.

5. Develop each piece in TypeScript with accompanying SCSS/CSS files (using Saffron design tokens only), Angular services, and unit tests.

6. Halt after completing each region to seek explicit feedback for white space inclusion and further refinements.

7. **Build Verification:** After implementing each section, verify the project builds successfully:
   - Run the build command (e.g., `ng build` for Angular, `npm run build` for other frameworks)
   - If build errors occur, fix them immediately before proceeding
   - Ensure TypeScript compilation passes without errors

8. **Visual Verification (CRITICAL - PIXEL-PERFECT VALIDATION):** After successful build, request a screenshot from the user:
   - Ask the user to provide a screenshot of the implemented section
   - **Compare the screenshot with the original downloaded Figma image PIXEL-BY-PIXEL**
   - Use the visual comparison protocol from figma-instructions.md Step 8
   - **MEASURE exact discrepancies in pixels** (not just "close enough")
   - Verify with EXACT measurements:
     * Colors (compare hex values)
     * Spacing (measure each gap, margin, padding in pixels)
     * Fonts (exact size, weight, line-height)
     * Sizes (exact width and height of components)
     * Positioning (exact alignment and placement)
     * Component states
   - Create a detailed discrepancy report with PIXEL measurements
   - **NO TOLERANCE for "close enough" - must be pixel-perfect**
   - Request adjustments and fix issues immediately
   - Re-request screenshot after fixes
   - Repeat until 100% pixel-perfect match achieved

#### Example Implementation (Angular with Saffron):
```ts
// Header component (Angular)
// filepath: src/app/feature/header/header.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.scss']
})
export class HeaderComponent {
  productName = 'LegalTracker';
}
```

```html
<!-- filepath: src/app/feature/header/header.component.html -->
<!-- Using Saffron components ONLY -->
<saf-product-header 
  [product-name]="productName" 
  aria-label="Main application header">
  <saf-search-input 
    slot="search"
    placeholder="Search..."
    aria-label="Search application">
  </saf-search-input>
</saf-product-header>
```

```scss
/* filepath: src/app/feature/header/header.component.scss */
/* Using Saffron design tokens AND exact Figma measurements */
:host {
  display: block;
  background-color: var(--saf-color-surface-primary); /* or #FFFFFF if exact match needed */
  border-bottom: 1px solid var(--saf-color-border-default); /* or #E5E5E5 if exact */
  
  /* EXACT measurements from Figma */
  height: 64px; /* Must match Figma exactly */
  padding: 0 16px; /* Exact padding from Figma */
}

/* If design tokens don't match Figma exactly, override: */
saf-product-header {
  --saf-header-height: 64px; /* Override to match Figma */
  --saf-header-padding: 16px; /* Override to match Figma */
}

/* Document any deviations from design tokens */
/* DEVIATION: Using exact hex #FFFFFF instead of --saf-color-surface-primary */
/* REASON: Figma design requires pure white, token produces #FAFAFA */
```

```ts
// Table component with Wijmo (if selected)
// filepath: src/app/feature/data-table/data-table.component.ts
import { Component, OnInit } from '@angular/core';
import { CollectionView } from '@grapecity/wijmo';
// Additional Wijmo imports from Saffron MCP

@Component({
  selector: 'app-data-table',
  templateUrl: './data-table.component.html',
  styleUrls: ['./data-table.component.scss']
})
export class DataTableComponent implements OnInit {
  data: CollectionView;
  
  ngOnInit() {
    // Wijmo configuration from Saffron MCP
    this.data = new CollectionView(this.getData());
  }
  
  getData() {
    // Data source implementation
    return [];
  }
}
```

```html
<!-- filepath: src/app/feature/data-table/data-table.component.html -->
<!-- Wijmo FlexGrid with Saffron styling -->
<wj-flex-grid 
  [itemsSource]="data"
  [allowSorting]="true"
  [allowFiltering]="true"
  class="saffron-table">
  <wj-flex-grid-column [header]="'Column 1'" [binding]="'field1'"></wj-flex-grid-column>
  <!-- Additional columns from Saffron MCP configuration -->
</wj-flex-grid>
```

Prompt the user:
```
The [Section Name] has been implemented using Saffron components. Let me verify the build...

[After running build command]

✓ Build completed successfully! 

**VISUAL VERIFICATION REQUIRED:**

Please provide a screenshot of the implemented [Section Name] so I can compare it with the original Figma design.

I will verify:
✓ Colors match Saffron design tokens and Figma specifications
✓ Spacing and positioning are pixel-perfect
✓ Font sizes and styles match the design
✓ Component states (hover, active, disabled) are correct
✓ Overall layout aligns with Figma image

**Provide screenshot now for comparison.**

After verification:
- Are there any visual discrepancies I should fix?
- Should there be any white spaces around it? If yes, specify spacing using Saffron tokens.
```

 
### **Step 5: Final Review, Refinements & Visual Validation**

#### **Section-by-Section Iteration**
- Iterate based on feedback before implementing the next section.
- Confirm alignment with spacing preferences dynamically at every stage.
- Fix any discrepancies identified during visual comparison immediately.

#### **Final Visual Validation Protocol**

After ALL sections are implemented, perform comprehensive visual validation:

1. **Request Complete Implementation Screenshots:**
```
🎯 FINAL VALIDATION PHASE

All sections have been implemented. To ensure pixel-perfect accuracy:

Please provide screenshots of:
1. Full page view (desktop)
2. Each major section close-up
3. Mobile/tablet views (if responsive design required)
4. Interactive states (hover, active, disabled) if possible

I will perform detailed comparison with original Figma designs.
```

2. **Comprehensive Visual Comparison:**
   - Load all original Figma images downloaded in Step 2
   - Compare with user's implementation screenshots
   - Create detailed comparison report (see figma-instructions.md Step 8)

3. **Discrepancy Report & Fixes:**

```
📊 VISUAL COMPARISON REPORT

Comparison: Figma Design vs Implementation

✅ MATCHES:
- Header layout and positioning
- Button colors and sizes  
- Typography hierarchy
- Card spacing
- Overall component alignment

⚠️ DISCREPANCIES FOUND:

| Component | Figma Design | Implementation | Priority | Fix Required |
|-----------|--------------|----------------|----------|--------------|
| Table header | 64px height | 68px height | HIGH | Reduce to 64px |
| Primary button | --saf-color-primary-500 | --saf-color-primary-600 | HIGH | Use correct token |
| Card padding | 24px all sides | 16px top/bottom | MEDIUM | Adjust padding |
| Icon size | 20px | 24px | LOW | Resize to 20px |

🔧 FIXING DISCREPANCIES NOW...
```

4. **Apply Fixes:**
   - Address each discrepancy immediately
   - Update Saffron component properties
   - Verify design token usage
   - Re-build and re-test

5. **Re-validation:**
   - Request new screenshots after fixes
   - Repeat comparison
   - Continue until pixel-perfect match

6. **Final Approval:**
```
✅ FINAL VALIDATION COMPLETE

All sections match Figma design specifications:
✓ Layout and positioning: Pixel-perfect
✓ Colors and styling: Exact match (Saffron tokens)
✓ Typography: Matches design hierarchy
✓ Spacing: Precise alignment
✓ Component states: All verified
✓ Responsive behavior: Tested and validated
✓ Accessibility: WCAG 2.1 AA compliant

📋 DELIVERABLES:
- All components implemented with Saffron Design System
- Build successful with no errors
- Visual design matches Figma 100%
- Code follows TypeScript best practices
- Accessibility requirements met
- Unit tests included

Implementation is ready for production! 🚀
```

#### **Additional Quality Checks**
- Cross-browser testing (if required)
- Accessibility audit using automated tools
- Performance metrics validation
- Code review for TypeScript safety
- Documentation completeness

---

# A11y Guidelines
 
## Accessibility Rules for UI Components
 
Below are accessibility rules for each listed component. These rules ensure compliance with **WCAG 2.x** and **ARIA** standards, improving usability for all users, including those relying on assistive technologies such as screen readers and keyboard navigation.
 
---
 
### Accordion
 
- Use `aria-expanded` and `aria-controls` on trigger buttons.
- Panels should have `role="region"` and be referenced via `aria-labelledby`.
- All panels must be keyboard-accessible (Tab, Arrow Up/Down to navigate).
- Focus is managed so expanded content receives focus as appropriate.
 
### Adaptive Panel
 
- Panels should announce state changes (open/close/minimize/maximize) via ARIA live regions or properties.
- All actions (e.g., resizing, collapsing) must be keyboard accessible.
- Provide meaningful labels for actions (e.g., “Minimize panel”).
 
### Alert
 
- Use `role="alert"` or `role="status"` for different importance levels.
- Alerts must be announced automatically to screen readers.
- Content changes in the alert area must be perceivable by assistive technology.
 
### Anchor
 
- Use clear, descriptive link text.
- Apply `aria-label` when context is not clear from text alone.
- Links must be focusable and navigable via keyboard (Tab/Shift+Tab).
 
### Avatar
 
- Provide accessible name via `alt` attribute if image, or `aria-label` if icon-only.
- Decorative avatars should use empty `alt=""` or `aria-hidden="true"`.
 
### Avatar Stack
 
- Each avatar should have an accessible name.
- If representing a group, provide a group label (e.g., `aria-label="Team members"`).
- Indicate overflow count with an accessible label (e.g., “3 more users”).
 
### Badge
 
- Use `aria-label` to describe badge content (e.g., “5 unread messages”).
- Badges used for status should have clear, semantically correct text or ARIA status roles.
 
### Blocker
 
- Use `aria-modal="true"` when displaying overlays or blockers.
- Ensure background content is inaccessible to screen readers and cannot be tabbed to.
 
### Button
 
- Use semantic `<button>` elements or `role="button"` with proper keyboard support.
- All buttons must be focusable.
- Provide accessible names via text, `aria-label`, or `aria-labelledby`.
 
### Checkbox
 
- Use `<input type="checkbox">` with a visible `<label>`.
- Synchronize checked state with `aria-checked`.
- Group checkboxes with `role="group"` and label with `aria-labelledby` where appropriate.
 
### Checkbox Group
 
- Use `role="group"` or `<fieldset>` with a visible legend or label.
- Each checkbox must have its own label.
 
### Control Group
 
- Group related controls with `role="group"` or `<fieldset>`.
- Provide a group label via `aria-labelledby` or `<legend>`.
 
### Count Indicator
 
- Use `aria-label` or hidden screen-reader text to provide a description (e.g., “2 new messages”).
 
### Data Tables
 
- Use semantic `<table>`, `<th>`, `<tr>`, `<td>`.
- Use `scope="col"`/`scope="row"` for headers.
- Provide captions with `<caption>`.
- Ensure table structure is navigable via screen reader and keyboard.
 
### Date Picker
 
- Inputs must be keyboard accessible.
- Provide ARIA roles (`aria-haspopup="dialog"`, `aria-label` for the calendar popup).
- Announce currently selected date and active date.
- Controls for navigation (prev/next month/year) must be labeled and focusable.
 
### Dropdown
 
- Dropdown trigger must be a button or link with an accessible label.
- Popup content should have `role="listbox"` and options `role="option"`.
- Manage focus within dropdown via keyboard (Arrow keys).
- Use `aria-expanded` and `aria-controls` on trigger button.
 
### Dropdown Container
 
- Should support `aria-labelledby` for identification.
- Keyboard navigation for nested dropdowns; Escape closes container.
 
### Dropdown Menu
 
- Use `role="menu"` for menu container and `role="menuitem"` for menu options.
- Support keyboard navigation (Arrow keys, Enter, Escape).
 
### File Upload
 
- Inputs must have a visible, accessible label.
- Announce upload status and error/success messages.
- Support keyboard-triggered file selection.
- Use `aria-describedby` for extra instructions.
 
### Flex Items
 
- Ensure dynamic layout changes are announced if they impact content order.
- For important layout containers, use landmarks or ARIA grouping roles.
 
### Form
 
- Each form control must have a corresponding `<label>` or `aria-label`.
- Use `aria-describedby` for helper or error text.
- Form must be navigable by keyboard (Tab order is logical).
 
### Icon Button
 
- Include `aria-label` describing the button's action.
- Ensure SVGs or icon fonts used are accessible or marked as decorative.
 
### Icon Container
 
- Icons used purely for decoration should use `aria-hidden="true"`.
- Informative icons should have a text label or `aria-label`.
 
### Labeled Input
 
- Must always have visible text label.
- Use `for` attribute to connect `<label>` and input.
 
### Link Button
 
- Use a `<button>` for actions, `<a>` for navigation.
- Provide accessible names and ensure keyboard interaction.
 
### Main Menu
 
- Use `role="menubar"` for navigation menus.
- Items should be `role="menuitem"`.
- Support keyboard navigation (Arrow keys, Enter, Escape, Tab).
 
### Modals
 
- Use `role="dialog"` and `aria-modal="true"`.
- Focus is trapped within the modal.
- Modal has a visible header/label (`aria-labelledby`) and description (`aria-describedby`).
- On close, focus returns to triggering element.
 
### MultiSwitch
 
- Must be navigable by keyboard and indicate selected state with `aria-checked`.
- Use `role="switch"` for each item.
 
### Notification Card
 
- Announce new notifications via `role="status"` or ARIA live region.
- Card actions must be accessible (button/link semantics, keyboard navigable).
 
### Numeric Input
 
- Use `<input type="number">` with `min`/`max` attributes as appropriate.
- Label explicitly.
- Provide incremental steps with up/down arrow keys.
 
### Rich Text View
 
- Ensure correct heading levels and landmarks.
- All text formatting is available to assistive tech through semantic HTML.
 
### Scroll Spy
 
- Ensure visible indication of active section.
- Announce section changes (via ARIA live region) as user scrolls.
 
### Search Input
 
- Provide a label ("Search") and relevant ARIA roles (`role="search"`).
- Announce search results and suggestions.
 
### Slider
 
- Use `role="slider"`, `aria-valuenow`, `aria-valuemin`, `aria-valuemax`.
- Must be keyboard accessible (Arrow keys, Home, End).
- Label slider and current value.
 
### Slider Rating
 
- Announce current rating as value changes.
- Use `aria-valuetext` for custom value presentations.
 
### Spinner
 
- Use `role="status"` or `aria-busy="true"` when active.
- Optional: visually hidden text to indicate loading.
 
### Status Indicator
 
- Use meaningful labels/ARIA attributes to indicate status.
- Use colors and icons with text for color-blind accessibility.
 
### Switch
 
- Use `role="switch"` and `aria-checked`.
- Provide clear labels for on/off state.
 
### Tab Button
 
- Use `role="tab"`; parent container should have `role="tablist"`.
- Selected tab: `aria-selected="true"`.
- Tabs must be keyboard-accessible (Arrow keys).
 
### Tag
 
- Provide accessible names and role if interactive (e.g., `role="button"` or `role="link"`).
- Removable tags should have remove button with `aria-label`.
 
### Text
 
- Text content must have sufficient contrast and readable font.
- Use semantic elements (e.g., `<p>`, `<h1>`-`<h6>`).
 
### Text Area
 
- Require visible label.
- Ensure ARIA attributes for character count or errors.
 
### Text Input
 
- Input must be labeled.
- Use `aria-describedby` for hint/error text.
 
### Text Placeholder
 
- Use placeholder for example input but not as replacement for a label.
- Provide real `<label>`.
 
### Time Picker
 
- Keyboard navigable.
- Announce time selection and changes.
- Use ARIA attributes for popup/picker identification.
 
### Tooltip
 
- Use `role="tooltip"` and point to trigger with `aria-describedby`.
- Tooltip must be dismissible and keyboard accessible.
 
### Tree
 
- Use `role="tree"`, `role="treeitem"`, and manage expanded/collapsed state with `aria-expanded`.
- Support keyboard navigation (Arrow keys).
 
### Vertical Tab Button
 
- Same as Tab Button: use `role="tab"`, parent `role="tablist"`.
- Supports vertical keyboard navigation (Arrow keys).
 
### Virtual List
 
- All items must be navigable via keyboard.
- Manage focus and announcements dynamically as content loads/unloads.
- Use `aria-setsize` and `aria-posinset` as needed.
 
---
 
## Note
 
- Ensure minimum color contrast ratio (WCAG 2.x AA: 4.5:1 normal text, 3:1 large text).
- All interactive elements must be focusable, operable with keyboard, and have visible focus indicators.
- All dynamic content changes should be announced through relevant ARIA live regions.
 
## **Constraints**
1. All code must be **TypeScript-safe** and comply with project scalability, accessibility, and responsiveness rules.
2. Avoid deviations from the **Saffron** unless explicitly authorized.
3. Proactively confirm spacing rules at every implementation stage.
 
---
 
## **Example Feedback Pattern**
1. Approve or request layout tweaks (e.g., "Adjust sidebar spacing").
2. Confirm component props and behavior (e.g., "Enable `isSearchable` for Header").
3. Validate spacing rules for each section (e.g., "Include margin between content and Sidebar").
 
---
 
## **Collaboration Guidelines**
1. **Incremental Progress:** Implement one section at a time for easier reviews.
2. **Modular Design:** Divide page logic cleanly into reusable components.
3. **Feedback Loop:** Seek explicit user approval at every stage, focusing on spacing and component specifications.
 
--- 
## **Notes**
Always ask the user about spacing explicitly. If unclear preferences exist, direct them to clarify decisions before moving forward. Adapt implementation dynamically based on responses.