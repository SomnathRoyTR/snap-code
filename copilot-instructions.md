## **Instructions**
You will build one or more web pages within an existing codebase that strictly uses the **Saffron** from the [instructions](./instructions) folder. The task involves adhering to scalability, maintainability, accessibility, and responsiveness standards while ensuring compliance with TypeScript safety and collaborative workflows.
 
### **Ultimate Objective**
1. Transform the provided UI designs, user requirements, and APIs into components and layouts using the **Saffron**.
2. Collaboratively progress through incremental stages, ensuring alignment and approval for each step.
 
---
 
## **Steps to Follow**
 


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

### **Step 2: Layout Proposal**
Analyze the provided UI design and define the layout structure. Present your proposal clearly while asking for feedback on spacing rules and preferences.
 
#### Example Proposal:
```
**LAYOUT PROPOSAL:**  
- The page design includes the following sections:  
   1. **Header:** Full-width at the top; includes navigation and search.  
   2. **Sidebar:** Left-aligned, vertical menu panel.  
   3. **Main Content:** A responsive grid for forms/cards.  
 
**Spacing Query:**  
Should we include white spaces between the following sections?  
- Header ↔ Sidebar: Yes/No?  
- Sidebar ↔ Main Content: Yes/No?  
 
Type "yes" to approve, "no" for changes, or specify spacing preferences for refinement.
```
 
### **Step 3: Component Mapping**
Determine the specific **Saffron components** required for each layout section and include details about props, themes, and accessibility considerations. Confirm spacing preferences again with explicit questions.
 
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
1. Implement each section incrementally. For Angular projects, follow Angular conventions:
   - Create a feature module if the page is a standalone area (ng generate module feature --routing).
   - Generate isolated components per section (ng generate component header --module=feature).
   - Use component-scoped styles via styleUrls and TypeScript-safe inputs/outputs.
   - Add unit tests using Jasmine/Karma (ng test) or Jest if configured.

2. Before developing each section, download the Figma image of that section and check all color combinations, positions, spacing, fonts, sizes and other properties. Follow the steps under [figma-instructions.md](./figma-instructions.md), verify every detail, and confirm with the user.

3. After implementing each section, prompt the user for feedback on spacing and component behavior.

4. Develop each piece in TypeScript with accompanying SCSS/CSS files, Angular services, and unit tests.

5. Halt after completing each region to seek explicit feedback for white space inclusion and further refinements.

#### Example Implementation (Angular):
```ts
// Header component (Angular)
// filepath: src/app/feature/header/header.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.scss']
})
export class HeaderComponent {}
```

```html
<!-- filepath: src/app/feature/header/header.component.html -->
<!-- Use Saffron web components directly or an Angular wrapper if available -->
<saf-product-header product-name="LegalTracker" aria-label="Main Header"></saf-product-header>
```

```ts
// Sidebar component (Angular)
// filepath: src/app/feature/sidebar/sidebar.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-sidebar',
  templateUrl: './sidebar.component.html',
  styleUrls: ['./sidebar.component.scss']
})
export class SidebarComponent {}
```

```html
<!-- filepath: src/app/feature/sidebar/sidebar.component.html -->
<saf-side-nav aria-label="Main navigation" [state]="open"></saf-side-nav>
```

```scss
/* filepath: src/app/feature/sidebar/sidebar.component.scss */
:host {
  display: block;
  width: 260px;
}
```

Prompt the user:
```
Does the Header meet design expectations?
- Should there be any white spaces around it? If yes, specify spacing (e.g., "Add margin: 20px").
```

 
### **Step 5: Approvals and Refinements**
- Iterate based on feedback before implementing the next section.
- Confirm alignment with spacing preferences dynamically at every stage.
 
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
- For extended guidance, see:
  - [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
  - [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG21/)

---
 
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