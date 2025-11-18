# Figma Component Implementation Protocol

## Instructions

You will receive Figma design links that may include:
- **Single Figma Link:** Either full page or component view
- **Two Figma Links:** Typically full page context + specific component
- **Multiple Figma Links:** Various design views, states, or related components

**CRITICAL:** This protocol requires downloading Figma designs as images, analyzing components visually, and mapping them to Saffron Design System components before implementation.

---

## Assessment Protocol

- Count and categorize all Figma links received
- Identify the type and purpose of each design view
- Create a design inventory mapping
- **DOWNLOAD all Figma designs as images immediately**
- Adapt analysis approach based on design resources available

---

## Implementation Steps

### 1. Figma Image Download & Initial Analysis

**STEP 1A: Download Figma Designs as Images**

Use the MCP server to fetch and download Figma images (NOT JSON):

```
1. Extract Figma file ID and node ID from the URL
2. Use fetch_figma tool to download the image
3. Save the image to workspace for visual analysis
4. Confirm image download successful before proceeding
```

**FALLBACK: If Figma Download Fails**

If the Figma image download fails for any reason (network issues, permissions, API errors, etc.):

```
⚠️ Figma Image Download Failed

I was unable to download the Figma design image automatically.

FALLBACK REQUEST:
Please provide a screenshot of the Figma design by:
1. Opening the Figma link in your browser
2. Taking a screenshot of the design (full page or component view)
3. Uploading the screenshot here

Once you provide the screenshot, I will:
- Analyze the design visually
- Identify all UI components
- Map components to Saffron Design System
- Proceed with implementation as planned

Please share the screenshot(s) now.
```

After receiving user-provided screenshot(s), continue with the normal workflow (visual analysis, component mapping, etc.)

**STEP 1B: Create Figma Link Inventory**

#### Figma Link Inventory

- Total Links: `[Count]`
- Link 1: `[URL]` — `[Type: Full Page/Component/State/Variant]` — `[Image: filename.png]`
- Link 2: `[URL]` — `[Type: Description]` — `[Image: filename.png]`
- Link N: `[URL]` — `[Type: Description]` — `[Image: filename.png]`

**STEP 1C: Visual Component Analysis (PIXEL-PERFECT REQUIREMENTS)**

- Review downloaded images to identify UI components
- **MEASURE exact dimensions** of every component using the image
- List each visible component (buttons, inputs, cards, tables, navigation, etc.)
- **EXTRACT exact colors** (use color picker or inspect tools)
- **MEASURE exact spacing** between all elements (margins, padding, gaps)
- **IDENTIFY exact font sizes, weights, and line heights**
- Note component hierarchy and relationships
- **DOCUMENT exact positions** of all elements (left, top, right, bottom)
- Identify primary implementation target
- Note technical constraints, dependencies, and design system references

**CRITICAL:** Every measurement must be exact. No assumptions, no approximations.

---

### 2. Component Identification & Saffron Mapping

**STEP 2A: Identify All UI Components**

From the downloaded Figma images, create a comprehensive component list:

#### Component Inventory (WITH EXACT MEASUREMENTS)

| Component Type | Count | Exact Dimensions | Colors | Spacing | Font Details | Position |
|----------------|-------|------------------|--------|---------|--------------|----------|
| Buttons | X | Primary, Secondary, etc. | Header, Footer, etc. |
| Input Fields | X | Text, Search, etc. | Form area |
| Tables/Grids | X | Data display | Main content |
| Navigation | X | Menu, Tabs, etc. | Header/Sidebar |
| Cards | X | Content containers | Grid layout |
| Icons | X | Various icons | Throughout |
| Typography | X | Headings, Body text | Throughout |
| Other | X | Specify | Location |

**STEP 2B: Map Components to Saffron Design System**

For EACH identified component:

1. **Consult Saffron Component Mapping** (`saffron_component_mapping.md`)
2. **Determine correct Saffron component** to use
3. **Document the mapping**:

#### Saffron Component Mapping

| Figma Component | Saffron Component | Notes |
|-----------------|-------------------|-------|
| Primary Button | `<saf-button appearance="primary">` | Standard primary action |
| Text Input | `<saf-text-field>` | With label and validation |
| Data Table | `<saf-data-grid>` or Wijmo | See table analysis below |
| Card Container | `<saf-card>` | With header and content slots |
| Page Title | `<saf-text appearance="heading-2xl">` | Heading hierarchy |

**STEP 2C: Special Case - Table/Grid Detection**

**IF Figma design contains a table/grid:**

1. **Analyze table complexity:**
   - Simple data display (read-only)
   - Interactive features (sorting, filtering, pagination)
   - Editing capabilities (inline editing, cell editing)
   - Advanced features (grouping, aggregation, export)

2. **Check for existing table implementations:**
   - Search workspace for similar table implementations
   - Check if Wijmo tables are already in use
   - Review existing table patterns

3. **Ask user for table type preference:**

```
I detected a table component in the Figma design with [describe features].

Please specify which table implementation to use:
   a) saf-data-grid (basic Saffron table)
   b) Wijmo FlexGrid (advanced features)
   c) Custom implementation
   d) Use existing pattern from [filename]

If Wijmo: Please confirm which Wijmo table features are needed:
   - Sorting
   - Filtering
   - Inline editing
   - Grouping
   - Pagination
   - Export functionality
   - Other features
```

4. **IF Wijmo is selected:**
   - Use Saffron MCP server to get Wijmo implementation details
   - Call `get-saffron-code` for Wijmo component
   - Get complete package imports and dependencies
   - Include full implementation with proper configuration

---

### 3. Comprehensive Visual Specification Extraction

From downloaded Figma images, extract and document:

#### Core Specifications
- **Dimensions:** Width, height, min/max constraints
- **Positioning:** Absolute/relative, z-index, flex/grid placement
- **Spacing:** Margins, paddings, gaps (document grid system)

#### Visual Properties
- **Colors:**
    - Primary, secondary, tertiary colors
    - State-based color variations (hover, active, disabled)
    - Opacity/transparency values
    - **Map to Saffron design tokens** using MCP server
- **Typography:**
    - Font family, size, weight, style
    - Line height, letter spacing
    - Text alignment and overflow behavior
    - **Map to Saffron text appearances**
- **Effects:**
    - Shadows (box-shadow, text-shadow)
    - Borders (width, style, color, radius)
    - Gradients, filters, transforms
    - **Map to Saffron design tokens**

#### Interaction States (if multiple links/images provided)
- Default/Rest state
- Hover state
- Active/Pressed state
- Focus state
- Disabled state
- Loading state
- Error state
- Success state

#### Responsive Behavior (if breakpoint images provided)
- Desktop (>1200px)
- Tablet (768px - 1199px)
- Mobile (<768px)
- Custom breakpoints

---

### 4. Analysis Strategy by Link Count

#### Single Link Scenario
- Download image
- Determine view type (full page vs. component)
- Extract maximum information from the visual design
- Map all components to Saffron equivalents
- Document context gaps requiring clarification

#### Two Links Scenario
- Download both images
- Link 1: Analyze full page for placement and context
- Link 2: Deep dive into component specifications
- Map relationships between context and component
- Create unified Saffron component mapping

#### Multiple Links Scenario (3+)
- Download all images
- **Categorize Links:**
    - Context/Layout views
    - Component detail views
    - State variations (hover, active, disabled)
    - Responsive breakpoints
    - Edge cases or error states

**Create Analysis Matrix:**

| Link # | Type        | Image File | Purpose         | Key Information        |
|--------|-------------|------------|-----------------|------------------------|
| 1      | Full Page   | page.png   | Desktop Layout  | Component position     |
| 2      | Component   | comp.png   | Default State   | Base specifications    |
| 3      | Component   | hover.png  | Hover State     | Interaction feedback   |
| 4      | Mobile View | mobile.png | Responsive      | Mobile adaptation      |

---

### 5. Information Synthesis & Saffron Integration

#### Complete Information (Multiple Links)
- Cross-reference all downloaded images for consistency
- Identify any design discrepancies between views
- Build complete state machine for components
- Document responsive flow
- **Finalize Saffron component selections**
- **Retrieve Saffron component code using MCP server**

#### Partial Information
- List known specifications from available images
- Document assumptions based on visual analysis
- Flag missing states/views for clarification
- Propose standard Saffron patterns for gaps
- **Use Saffron defaults for unspecified states**

#### Saffron Component Code Retrieval

For each component to implement:

1. Use `get-saffron-code` tool to get complete implementation
2. Use `get-saffron-a11y-attributes` for accessibility requirements
3. Use `get-saffron-tokens` to map colors, spacing, fonts to design tokens
4. For tables: If Wijmo selected, get full package and configuration

---

### 6. Validation & Clarification Protocol

#### Validation Checkpoints

- [ ] All Figma images downloaded successfully
- [ ] All components identified and cataloged
- [ ] **EXACT dimensions measured for every component**
- [ ] **EXACT colors extracted (hex codes or RGB values)**
- [ ] **EXACT spacing measured between ALL elements**
- [ ] **EXACT font sizes, weights, and line heights documented**
- [ ] Each component mapped to Saffron equivalent
- [ ] **Saffron component properties configured to match EXACT measurements**
- [ ] Table implementation approach confirmed (if applicable)
- [ ] All component states identified from images
- [ ] Responsive behavior documented from available images
- [ ] Placement context understood
- [ ] Interaction patterns clear from visual analysis
- [ ] Edge cases covered
- [ ] Accessibility requirements noted
- [ ] Design token mapping complete with EXACT values

#### Clarification Requests (when needed)

##### Clarifications Needed

1. **Missing States**:  
   "From the downloaded Figma image, I see default state. Should I implement hover, focus, and disabled states using standard Saffron patterns?"

2. **Responsive Gaps**:  
   "I have desktop view image. Should tablet/mobile use responsive Saffron patterns or do you have additional Figma designs?"

3. **Table Implementation** (REQUIRED if table detected):  
   "I detected a data table in the Figma design. Please specify:
   - Use saf-data-grid or Wijmo FlexGrid?
   - If Wijmo: Which features needed (sorting, filtering, editing, etc.)?"

4. **Component Variants**:  
   "The image shows [component]. Should I use Saffron's [variant-a] or [variant-b] pattern?"

5. **Animation Details**:  
   "Multiple states shown in images but no transition specifications. Should I use standard Saffron transitions?"

---

### 7. Implementation Generation with Saffron Components

Generate comprehensive implementation using **ONLY Saffron Design System components**:

#### Implementation Checklist

- [ ] Component structure using Saffron components (NO native HTML)
- [ ] **EXACT dimensions applied** (width, height matching Figma)
- [ ] **EXACT colors applied** using closest Saffron design tokens
- [ ] **EXACT spacing applied** (margins, padding, gaps matching Figma)
- [ ] **EXACT font styling applied** (size, weight, line-height matching Figma)
- [ ] **EXACT positioning applied** (alignment, flex/grid properties)
- [ ] Styling using Saffron design tokens (override if needed for exact match)
- [ ] State management logic with Saffron patterns
- [ ] Accessibility attributes from Saffron MCP
- [ ] Responsive adaptations using Saffron responsive tokens
- [ ] Animation/transition using Saffron motion tokens
- [ ] For tables: Complete Wijmo configuration if selected
- [ ] Unit test scaffolding
- [ ] Inline documentation

**PRIORITY: Exact visual match over strict token usage. If a design token doesn't produce the exact Figma design, override with exact CSS values and document the deviation.**

#### Saffron Component Implementation Template

```typescript
/**
 * Component: [Name]
 * Figma References: [Count] images analyzed
 * Figma Files: [list image files]
 * 
 * EXACT MEASUREMENTS FROM FIGMA:
 * - Container: [Width]px × [Height]px
 * - Padding: [Top]px [Right]px [Bottom]px [Left]px
 * - Margin: [Top]px [Right]px [Bottom]px [Left]px
 * - Font: [Size]px / [Weight] / [Line-height]px
 * - Colors: [Hex codes]
 * - Border radius: [Value]px
 * - Spacing between elements: [Gap]px
 * 
 * Saffron Components Used:
 * - saf-button (Primary actions) - [Exact dimensions]
 * - saf-text-field (User input) - [Exact dimensions]
 * - saf-card (Container) - [Exact dimensions]
 * - [etc.]
 * 
 * Design Token Overrides (if needed for exact match):
 * - [List any custom CSS needed to match Figma exactly]
 * 
 * Design Coverage:
 * - States: [X/Y implemented]
 * - Breakpoints: [X/Y implemented]
 * - Accessibility: WCAG 2.1 AA compliant
 * - Visual Match: 100% pixel-perfect
 */

import { SafButton, SafTextField, SafCard } from '@saffron/react';
// or for Angular: already available via module import

// Component implementation with Saffron components ONLY
// All styling via Saffron design tokens
// Full accessibility compliance
```

#### For Wijmo Tables (if selected):

```typescript
/**
 * Table Component with Wijmo FlexGrid
 * Integrated with Saffron Design System
 */

// Full package imports from Saffron MCP
import { WjFlexGrid, WjFlexGridColumn } from '@grapecity/wijmo.react.grid';
import { CollectionView } from '@grapecity/wijmo';

// Complete Wijmo configuration
// Saffron styling integration
// All requested features implementation
```

---

### 8. POST-DEVELOPMENT VALIDATION (CRITICAL STEP)

**After completing the implementation, ALWAYS perform visual validation:**

#### Screenshot Validation Protocol

**STEP 8A: Request Implementation Screenshot**

Once development is complete, ask the user:

```
Development complete! To ensure pixel-perfect accuracy, please:

1. Run the application
2. Navigate to the implemented component/page
3. Take a screenshot of the implementation
4. Share the screenshot here

I will compare it with the original Figma design and identify any discrepancies.
```

**STEP 8B: Compare Screenshots (PIXEL-BY-PIXEL VALIDATION)**

When user provides implementation screenshot:

1. **Load original Figma image(s)** downloaded in Step 1
2. **Load user's implementation screenshot**
3. **Perform DETAILED pixel-by-pixel comparison:**
   - **Component positioning and alignment** (must match exactly to the pixel)
   - **Exact dimensions** (width and height of every element)
   - **Spacing** (margins, padding, gaps - measure each one)
   - **Colors** (compare hex values, check for any shade differences)
   - **Typography** (size, weight, line height, letter spacing)
   - **Component sizes and proportions** (button sizes, icon sizes, etc.)
   - **Border radius, shadows, and effects** (must match exactly)
   - **Interactive states** (if multiple screenshots)
   - **Responsive behavior** (if multiple breakpoints)
   
4. **Measure discrepancies in pixels:**
   - Document EXACT pixel differences (e.g., "3px too wide", "2px padding instead of 4px")
   - No vague descriptions - use precise measurements
   - Create overlay comparison if possible

**STEP 8C: Document Discrepancies**

Create detailed discrepancy report:

#### Visual Comparison Report

| Element | Figma Design | Implementation | Status | Action Needed |
|---------|--------------|----------------|--------|---------------|
| Header height | 64px | 68px | ❌ | Reduce to 64px |
| Button color | #0066CC | #0070D2 | ❌ | Use correct token |
| Card spacing | 24px | 24px | ✅ | Perfect match |
| Font size | 16px | 16px | ✅ | Correct |
| Icon position | Left aligned | Centered | ❌ | Align left |

**STEP 8D: Fix Identified Issues**

- Address each discrepancy immediately
- Make necessary code adjustments
- Ensure Saffron component properties are correctly configured
- Verify design token usage
- Re-request screenshot after fixes
- Repeat comparison until pixel-perfect

**STEP 8E: Final Approval**

```
✅ Visual validation complete!

All elements match the Figma design:
- Layout and positioning: Perfect
- Colors and styling: Perfect  
- Typography: Perfect
- Spacing: Perfect
- Component states: Perfect

Implementation is ready for production.
```

---

## Output Format

### 1. Design Analysis Report

# Component Implementation Specification

## Figma Design Inventory
Total Figma Links Analyzed: `[Count]`

| Link | URL    | Type                 | Image File        | Coverage         |
|------|--------|----------------------|-------------------|------------------|
| 1    | [URL]  | Full Page - Desktop  | page-desktop.png  | Context, Layout  |
| 2    | [URL]  | Component - Default  | component-def.png | Base specs       |
| 3    | [URL]  | Component - States   | component-int.png | Interactions     |
| 4    | [URL]  | Mobile View          | page-mobile.png   | Responsive       |

## Downloaded Images
- ✅ page-desktop.png (1920x1080)
- ✅ component-def.png (400x300)
- ✅ component-int.png (400x300)
- ✅ page-mobile.png (375x812)

## Component Identification

### Detected Components
| Component Type | Count | Figma Visual | Saffron Component |
|----------------|-------|--------------|-------------------|
| Buttons | 3 | Primary, Secondary | `<saf-button>` |
| Input Fields | 2 | Text inputs | `<saf-text-field>` |
| Table | 1 | Data grid | Wijmo FlexGrid |
| Cards | 4 | Content cards | `<saf-card>` |
| Icons | 12 | Various | `<saf-icon>` |

### Table Implementation Decision
- **Table Type:** Wijmo FlexGrid
- **Features Required:** Sorting, Filtering, Pagination, Export
- **Saffron Integration:** Via MCP server code retrieval
- **Package Dependencies:** Retrieved from Saffron MCP

#### Component Specifications

##### Dimensions & Layout
- Desktop: `[Specifications from image]`
- Tablet: `[Specifications or "Inferred"]`
- Mobile: `[Specifications from image]`

##### Visual Design (Mapped to Saffron)
- Colors: `[Design tokens: --saf-color-primary-500, etc.]`
- Typography: `[Saffron text appearances: heading-xl, body-md, etc.]`
- Effects: `[Design tokens: --saf-shadow-md, --saf-border-radius-lg, etc.]`

##### States Matrix

| State   | Figma Image Available | Saffron Implementation         |
|---------|-----------------------|--------------------------------|
| Default | ✅ component-def.png  | Standard Saffron defaults      |
| Hover   | ✅ component-int.png  | Saffron hover state            |
| Active  | ⚠️ Inferred           | Saffron active state pattern   |
| Disabled| ⚠️ Inferred           | Saffron disabled state pattern |
| Focus   | ❌ Missing            | Saffron focus state pattern    |

#### Implementation Notes
- All components mapped to Saffron equivalents
- Design tokens used for all styling
- Accessibility compliance via Saffron MCP
- Table implementation using Wijmo with full feature set
- Visual validation required post-development
| Hover   | ✅               | [Specs]               |
| Active  | ✅               | [Specs]               |
| Disabled| ⚠️ Inferred      | [Proposed specs]      |
| Focus   | ❌ Missing       | [Needs clarification] |

#### Implementation Notes
[Any special considerations or decisions made]

---

### 2. Component Code

```jsx
/**
 * Component: [Name]
 * Figma References: [Count] designs analyzed
 * 
 * Design Coverage:
 * - States: [X/Y implemented]
 * - Breakpoints: [X/Y implemented]
 * - Accessibility: [WCAG compliance level]
 */

// Component implementation with comprehensive documentation
// Annotations for any assumptions or inferred specifications
```

---

### 3. Validation Checklist

## Quality Assurance Checklist

### Design Fidelity
- [ ] Pixel-perfect match for provided designs
- [ ] All provided states implemented
- [ ] Responsive behavior matches all breakpoints
- [ ] Consistent with design system

### Technical Implementation
- [ ] Cross-browser compatible
- [ ] Performance optimized
- [ ] Accessible (WCAG 2.1 AA)
- [ ] Unit tests cover all states

### Documentation
- [ ] Assumptions clearly marked
- [ ] Missing specifications flagged
- [ ] Implementation decisions documented

---

## Adaptive Strategies by Link Count

### Single Link Strategy

**Priority:** Extract maximum detail from available design  
**Approach:** Heavy reliance on design notes/context  
**Output:** Flexible component with documented assumptions

---

### Two Links Strategy

**Priority:** Perfect context-to-detail mapping  
**Approach:** Full analysis of both placement and specifications  
**Output:** Precisely positioned component with complete specs

---

### Multiple Links Strategy

**Priority:** Comprehensive state and responsive coverage  
**Approach:** Systematic analysis of all variations  
**Output:** Full-featured component with complete state machine

---

## Example Interactions

**Example 1: Single Component Link with Figma Image Download**

> "I've received a Figma link for a filter component.  
> 
> **Step 1: Downloading Figma Image...**  
> ✅ Downloaded: filter-component.png (320px × 48px)  
> 
> **Step 2: Component Analysis from Image:**  
> From the downloaded image, I've identified:  
> - Component Type: Search/Filter bar
> - Dimensions: 320px × 48px  
> - Visual Elements: Search icon (16×16), text input, dropdown arrow
> - Styling: White background (#FFFFFF), 1px gray border (#E0E0E0)  
> 
> **Step 3: Saffron Component Mapping:**  
> - Container: `<saf-card>` or custom flex container
> - Search icon: `<saf-icon name="search">`
> - Input field: `<saf-text-field>`
> - Dropdown: `<saf-dropdown>`
> 
> However, I need clarification on:  
> 1. Where does this filter sit on the page? (Header, sidebar, or main content?)  
> 2. Should it be sticky or scroll with content?  
> 3. Are there any interaction states I should implement? (hover, focus, active)
> 
> Can you provide this context, or should I proceed with a standalone component that can be positioned flexibly?"

---

**Example 2: Two Links – Context and Component with Images**

> "I've analyzed two Figma links.  
> 
> **Downloaded Images:**  
> ✅ dashboard-full.png (1920px × 1080px)  
> ✅ filter-detail.png (320px × 48px)  
> 
> **Context Analysis (dashboard-full.png):**  
> - Filter component positioned in top-right of dashboard
> - 24px margin from header
> - Aligned with right edge of content area
> 
> **Component Details (filter-detail.png):**  
> - Dimensions: 320px × 48px  
> - Background: #FFFFFF with 1px border (#E0E0E0) → Maps to `--saf-color-surface-primary` and `--saf-color-border-default`
> - Font: 14px, Regular → Maps to `<saf-text appearance=\"body-default-sm\">`
> - Contains: Search icon (16×16), input field, dropdown arrow  
> 
> **Saffron Component Mapping:**  
> - Main container: `<saf-text-field>` with suffix icon
> - Search icon: `<saf-icon name=\"search\" slot=\"prefix\">`
> - Dropdown trigger: `<saf-icon name=\"chevron-down\" slot=\"suffix\">`
> - Positioning: Flexbox with `justify-content: flex-end`
> 
> Is this understanding correct? Should I proceed with implementation?"

---

**Example 3: Multiple Links with States and Image Analysis**

> "I've analyzed 4 Figma links with downloaded images:  
> 
> **Downloaded Images:**  
> ✅ dashboard-context.png - Shows component placement  
> ✅ search-default.png - Default state (320px × 48px)  
> ✅ search-active.png - Active/expanded state (320px × 200px)  
> ✅ search-mobile.png - Mobile view (100% width × 48px)  
> 
> **Component Inventory:**  
> - Search bar with dropdown functionality
> - Icon: Search (16×16)
> - Input field with placeholder
> - Dropdown menu with 5 filter options
> - Close/clear button when active
> 
> **Saffron Component Mapping:**  
> - Base: `<saf-text-field>` with `<saf-dropdown>`
> - Icons: `<saf-icon>` (search, chevron-down, close)
> - Dropdown items: `<saf-dropdown-item>` (5 items)
> - Mobile adaptation: `width: 100%` using Saffron responsive tokens
> 
> **Identified States:**  
> - Default (search-default.png): Collapsed, 320px width
> - Active (search-active.png): Expanded dropdown, 200px height
> - Mobile (search-mobile.png): Full width, responsive
> - Missing: Hover, Focus, Disabled
> 
> **Design Token Mapping:**  
> - Background: `--saf-color-surface-primary`
> - Border: `--saf-color-border-default`
> - Text: `--saf-text-body-default-sm`
> - Spacing: `--saf-spacing-md` (16px padding)
> 
> Should I proceed with implementation using standard Saffron patterns for the missing hover, focus, and disabled states?"

---

**Example 4: Comprehensive Multi-Link Analysis**

> "The Figma package includes 6 links:
> - 2 layout contexts (dashboard, detail page)
> - 3 component states (default, hover, selected)
> - 1 error state variation
> I notice the component appears in different contexts with slight variations:
> - Dashboard: Compact mode (200px width)
> - Detail page: Expanded mode (320px width)
> Should I create a single flexible component with size variants, or separate components?"

---

## Best Practices

- **Always Start with Inventory:** List and categorize all available designs
- **Cross-Reference Designs:** Look for consistency and variations
- **Document Everything:** Clear notes on what's provided vs. inferred
- **Progressive Enhancement:** Build from minimum viable to fully featured
- **Maintain Flexibility:** Components should adapt to context variations
- **Seek Clarification Early:** Don’t assume critical specifications

---

## Quality Standards

Regardless of the number of Figma links provided:
- **Pixel-Perfect Accuracy:** For all provided designs
- **Clear Documentation:** Distinguish confirmed vs. assumed specs
- **Flexible Implementation:** Adaptable to various contexts
- **Complete Coverage:** All states and breakpoints addressed
- **Accessibility First:** WCAG compliance built-in
- **Performance Optimized:** Efficient rendering and interactions

---

## Constraints

- Ensure zero tolerance for inaccuracies in layout or style replication for provided designs
- Confirm all design components align pixel-perfect with the Figma source
- If uncertainties arise, always seek user input
- Document all assumptions clearly in code comments and documentation

---

**Example 4: Comprehensive Multi-Link Analysis with Table Detection**

> "The Figma package includes 6 links with downloaded images:  
> 
> **Downloaded Images:**  
> ✅ dashboard-view.png - Full dashboard context  
> ✅ detail-page.png - Detail page context  
> ✅ table-default.png - Data table default state  
> ✅ table-hover.png - Row hover state  
> ✅ table-selected.png - Selected row state  
> ✅ table-error.png - Error state variation  
> 
> **🔍 TABLE DETECTED:**  
> I've identified a data table component with the following features from the images:
> - Sortable columns (ascending/descending indicators visible)
> - Row selection (checkboxes in first column)
> - Hover states (highlighted row background)
> - Pagination controls (bottom of table)
> - 8 columns with mixed data types (text, numbers, dates, status badges)
> 
> **Please specify table implementation:**  
> a) `saf-data-grid` (basic Saffron table)  
> b) Wijmo FlexGrid (advanced features)  
> c) Custom implementation  
> 
> **If Wijmo, which features are needed?**  
> ☐ Sorting (detected in Figma)  
> ☐ Filtering  
> ☐ Row selection (detected in Figma)  
> ☐ Inline editing  
> ☐ Grouping  
> ☐ Pagination (detected in Figma)  
> ☐ Export functionality  
> ☐ Other: _______
> 
> **Other Component Mappings:**  
> - Dashboard context shows table in compact mode (800px width)
> - Detail page shows table in expanded mode (1200px width)
> - Status badges: `<saf-chip>` with color variants
> - Action buttons: `<saf-button appearance="tertiary">`
> 
> Should I create a single flexible table component with size variants, or separate implementations?"

---

**Example 5: Post-Development Screenshot Validation**

> "✅ Implementation complete! Build successful.
> 
> **VISUAL VALIDATION REQUIRED:**
> 
> Please provide a screenshot of the implemented component so I can compare it with the original Figma design.
> 
> I will verify:
> ✓ Component positioning matches dashboard-full.png
> ✓ Dimensions are exactly 320px × 48px
> ✓ Colors match Saffron design tokens
> ✓ Spacing and padding are pixel-perfect
> ✓ Font sizes match the design
> ✓ Icon sizes and positions are correct
> 
> Once you share the screenshot, I'll create a detailed comparison report and fix any discrepancies."

---

**Example 6: Screenshot Comparison and Fix**

> "**📊 VISUAL COMPARISON REPORT**
> 
> Comparing: filter-detail.png (Figma) vs implementation-screenshot.png (Your implementation)
> 
> **✅ MATCHES:**
> - Width: 320px ✓
> - Border color: #E0E0E0 ✓
> - Icon size: 16×16 ✓
> - Font: 14px Regular ✓
> - Overall layout structure ✓
> 
> **⚠️ DISCREPANCIES FOUND:**
> 
> | Element | Figma Design | Implementation | Action |
> |---------|--------------|----------------|--------|
> | Height | 48px | 52px | Reduce height to 48px |
> | Padding | 12px left/right | 16px left/right | Adjust to 12px |
> | Background | #FFFFFF | #F8F8F8 | Use --saf-color-surface-primary |
> | Icon position | 12px from left | 16px from left | Reposition to 12px |
> 
> **🔧 APPLYING FIXES NOW...**
> 
> I'll update the component with the correct values and then request a new screenshot for re-validation."

---

**Example 7: Figma Download Failed - Fallback to User Screenshot**

> "I've received a Figma link for a dashboard component.  
> 
> **Step 1: Attempting Figma Image Download...**  
> ❌ Download Failed: [Network error / Permission denied / API timeout]
> 
> **⚠️ FALLBACK MECHANISM ACTIVATED**
> 
> I was unable to download the Figma design image automatically.
> 
> **Please provide a screenshot by:**
> 1. Opening this Figma link in your browser: [URL]
> 2. Taking a screenshot of the design (use browser screenshot or snipping tool)
> 3. Uploading the screenshot here
> 
> I need screenshot(s) of:
> - Full page view (if available)
> - Component detail view
> - Any interaction states shown in Figma (hover, active, etc.)
> 
> Once you share the screenshot(s), I will:
> ✓ Analyze the design visually
> ✓ Identify all UI components
> ✓ Map components to Saffron Design System
> ✓ Extract colors, spacing, fonts, and sizes
> ✓ Proceed with implementation
> 
> **Please upload the screenshot(s) now.**"

---

**Example 8: Received User Screenshot After Download Failure**

> "Thank you for providing the screenshot!
> 
> **Received Image:**  
> ✅ user-dashboard-screenshot.png (1920px × 1080px)  
> 
> **Proceeding with Visual Analysis:**
> 
> From your screenshot, I've identified:
> 
> **Component Inventory:**
> - Header: Navigation bar with logo and user menu
> - Sidebar: Left navigation panel (260px width)
> - Main Content: Data table with 6 columns
> - Filter Bar: Search input with dropdown filters
> - Action Buttons: Primary and secondary buttons
> - Status Badges: Color-coded status indicators
> 
> **Saffron Component Mapping:**
> - Header: `<saf-product-header>`
> - Sidebar: `<saf-side-nav>`
> - Table: Detected! Please specify: saf-data-grid or Wijmo FlexGrid?
> - Filter: `<saf-text-field>` + `<saf-dropdown>`
> - Buttons: `<saf-button appearance="primary/secondary">`
> - Badges: `<saf-chip>`
> 
> **Visual Specifications Extracted:**
> - Colors: #FFFFFF (background), #0066CC (primary), #6C757D (secondary)
> - Spacing: 24px between sections, 16px card padding
> - Typography: 16px body text, 24px headings
> - Table: 8 rows visible, sortable columns, pagination
> 
> **Design Token Mapping:**
> - Background: `--saf-color-surface-primary`
> - Primary: `--saf-color-primary-500`
> - Spacing: `--saf-spacing-lg` (24px), `--saf-spacing-md` (16px)
> 
> Ready to proceed with implementation. Please confirm table type preference."

---

## Best Practices

- **Always Attempt Image Download First:** Try automatic Figma download before asking user
- **Use Fallback When Needed:** If download fails, immediately request user screenshot
- **Accept User Screenshots:** Treat user-provided screenshots same as downloaded Figma images
- **Start with Component Inventory:** List and categorize all UI components from images
- **Map to Saffron Immediately:** Every component must have a Saffron equivalent
- **Detect Tables Early:** Identify tables and confirm implementation approach before coding
- **Cross-Reference Designs:** Look for consistency and variations across multiple images
- **Document Everything:** Clear notes on what's provided vs. inferred
- **Use Design Tokens:** Always map colors, fonts, spacing to Saffron design tokens
- **Screenshot Validation:** Always compare implementation with original Figma images or user screenshots
- **Progressive Enhancement:** Build from minimum viable to fully featured
- **Maintain Flexibility:** Components should adapt to context variations
- **Seek Clarification Early:** Don't assume critical specifications

---

## Updated Quality Standards

Regardless of the number of Figma links provided:
- **Image Required:** ALL Figma designs must have images (downloaded OR user-provided screenshots)
- **Fallback Mechanism:** If automatic download fails, request user screenshots immediately
- **Pixel-Perfect Accuracy:** For all provided designs after screenshot comparison
- **Saffron Components Only:** No native HTML elements allowed
- **Design Token Usage:** All styling via Saffron design tokens
- **Clear Documentation:** Distinguish confirmed vs. assumed specs
- **Table Implementation:** Proper selection between saf-data-grid and Wijmo
- **Complete Coverage:** All states and breakpoints addressed
- **Accessibility First:** WCAG 2.1 AA compliance built-in via Saffron MCP
- **Visual Validation:** Screenshot comparison before final approval
- **Performance Optimized:** Efficient rendering and interactions

---

## Updated Constraints

- **MUST have design images** - Downloaded Figma images OR user-provided screenshots
- **FALLBACK required** - If Figma download fails, request user screenshots before proceeding
- **MUST use Saffron components** - No native HTML elements
- **MUST map to design tokens** - No hardcoded CSS values
- **MUST validate with screenshots** - Compare implementation with design images
- **MUST ask about tables** - Confirm saf-data-grid vs Wijmo before implementation
- Ensure zero tolerance for inaccuracies in layout or style replication
- Confirm all design components align pixel-perfect via screenshot validation
- If uncertainties arise, always seek user input
- Document all assumptions clearly in code comments
- Fix all discrepancies immediately after screenshot comparison
- Never proceed without visual design reference (downloaded or user-provided)
