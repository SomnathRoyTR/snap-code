# SafSrOnly Component

The **SafSrOnly** component (Screen Reader Only) provides content that is visually hidden but accessible to screen readers and other assistive technologies. This is essential for creating inclusive interfaces that provide context and information to users with visual impairments without cluttering the visual design.

## Basic Usage

```html
<!-- Basic screen reader only text -->
<saf-sr-only>Additional context for screen readers</saf-sr-only>

<!-- Status information -->
<button>
  Delete
  <saf-sr-only>this item</saf-sr-only>
</button>

<!-- Form field descriptions -->
<input type="password" placeholder="Password" />
<saf-sr-only>Password must be at least 8 characters long</saf-sr-only>
```

## API Reference

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | `string` | - | Unique identifier for the element |

### Slots

| Slot | Description |
|------|-------------|
| (default) | Content that will be accessible only to screen readers |

### CSS Parts

| Part | Description |
|------|-------------|
| `root` | The main container element (visually hidden) |

## Comprehensive Examples

### Button Context and Actions

```html
<div class="button-examples">
  <h3>Button Context Examples</h3>
  
  <div class="button-group">
    <!-- Edit button with context -->
    <button class="icon-button" type="button">
      <saf-icon icon-name="edit" appearance="light"></saf-icon>
      <saf-sr-only>Edit user profile</saf-sr-only>
    </button>
    
    <!-- Delete button with context -->
    <button class="icon-button delete" type="button">
      <saf-icon icon-name="trash" appearance="light"></saf-icon>
      <saf-sr-only>Delete this item permanently</saf-sr-only>
    </button>
    
    <!-- Save button with state -->
    <button class="save-button" type="button">
      Save
      <saf-sr-only>changes to document</saf-sr-only>
    </button>
    
    <!-- Navigation button -->
    <button class="nav-button" type="button">
      <saf-icon icon-name="arrow-right" appearance="light"></saf-icon>
      Next
      <saf-sr-only>page in results</saf-sr-only>
    </button>
  </div>
</div>

<style>
.button-examples {
  padding: 2rem;
}

.button-group {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.icon-button {
  width: 44px;
  height: 44px;
  border: 1px solid #ccc;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.icon-button:hover {
  border-color: #007acc;
  background: #f0f8ff;
}

.icon-button.delete:hover {
  border-color: #dc3545;
  background: #fdf2f2;
}

.save-button,
.nav-button {
  padding: 0.75rem 1rem;
  border: 1px solid #007acc;
  background: #007acc;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.2s ease;
}

.save-button:hover,
.nav-button:hover {
  background: #005a9e;
  border-color: #005a9e;
}
</style>
```

### Form Field Enhancements

```html
<div class="form-enhancements">
  <h3>Form Field Enhancements</h3>
  
  <form class="enhanced-form">
    <!-- Password field with instructions -->
    <div class="form-group">
      <label for="password">Password</label>
      <input 
        type="password" 
        id="password" 
        name="password" 
        aria-describedby="password-help"
        required
      />
      <saf-sr-only id="password-help">
        Password must be at least 8 characters long and contain at least one uppercase letter, one lowercase letter, and one number.
      </saf-sr-only>
      <div class="visible-help">Must be at least 8 characters</div>
    </div>
    
    <!-- File upload with additional context -->
    <div class="form-group">
      <label for="document">Upload Document</label>
      <input 
        type="file" 
        id="document" 
        name="document" 
        accept=".pdf,.doc,.docx"
        aria-describedby="file-help"
      />
      <saf-sr-only id="file-help">
        Accepted file formats: PDF, Word Document. Maximum file size: 10MB. Multiple files can be selected.
      </saf-sr-only>
      <div class="visible-help">PDF or Word files only</div>
    </div>
    
    <!-- Required field indicator -->
    <div class="form-group">
      <label for="email">
        Email Address
        <span class="required-indicator" aria-hidden="true">*</span>
        <saf-sr-only>required field</saf-sr-only>
      </label>
      <input 
        type="email" 
        id="email" 
        name="email" 
        required
        aria-describedby="email-help"
      />
      <saf-sr-only id="email-help">
        We'll use this email address to send you account notifications and updates.
      </saf-sr-only>
    </div>
    
    <!-- Complex input with validation -->
    <div class="form-group">
      <label for="phone">Phone Number</label>
      <input 
        type="tel" 
        id="phone" 
        name="phone" 
        placeholder="(555) 123-4567"
        pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
        aria-describedby="phone-format"
      />
      <saf-sr-only id="phone-format">
        Enter your phone number in the format: area code, followed by seven digits. For example: 555-123-4567.
      </saf-sr-only>
      <div class="visible-help">Format: (555) 123-4567</div>
    </div>
    
    <button type="submit" class="submit-btn">
      Create Account
      <saf-sr-only>using the information provided above</saf-sr-only>
    </button>
  </form>
</div>

<style>
.form-enhancements {
  padding: 2rem;
}

.enhanced-form {
  max-width: 500px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #333;
}

.required-indicator {
  color: #dc3545;
  margin-left: 0.25rem;
}

.form-group input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  box-sizing: border-box;
}

.form-group input:focus {
  outline: none;
  border-color: #007acc;
  box-shadow: 0 0 0 2px rgba(0, 122, 204, 0.2);
}

.visible-help {
  font-size: 12px;
  color: #666;
  margin-top: 0.25rem;
}

.submit-btn {
  width: 100%;
  padding: 1rem;
  background: #007acc;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.submit-btn:hover {
  background: #005a9e;
}
</style>
```

### Data Tables and Lists

```html
<div class="table-enhancements">
  <h3>Table and List Enhancements</h3>
  
  <!-- Enhanced data table -->
  <table class="enhanced-table">
    <caption>
      Employee Directory
      <saf-sr-only>
        - This table contains employee information including names, departments, contact details, and employment status. Use arrow keys to navigate between cells and Tab key to move to interactive elements.
      </saf-sr-only>
    </caption>
    
    <thead>
      <tr>
        <th scope="col">
          Name
          <saf-sr-only>sortable column</saf-sr-only>
        </th>
        <th scope="col">
          Department
          <saf-sr-only>sortable column</saf-sr-only>
        </th>
        <th scope="col">
          Status
          <saf-sr-only>employment status</saf-sr-only>
        </th>
        <th scope="col">
          Actions
          <saf-sr-only>available actions for each employee</saf-sr-only>
        </th>
      </tr>
    </thead>
    
    <tbody>
      <tr>
        <td>
          <strong>John Doe</strong>
          <saf-sr-only>Employee ID: EMP001</saf-sr-only>
        </td>
        <td>Engineering</td>
        <td>
          <span class="status active">Active</span>
          <saf-sr-only>Full-time employee since January 2023</saf-sr-only>
        </td>
        <td>
          <button class="action-btn">
            <saf-icon icon-name="envelope" appearance="light"></saf-icon>
            <saf-sr-only>Send email to John Doe</saf-sr-only>
          </button>
          <button class="action-btn">
            <saf-icon icon-name="edit" appearance="light"></saf-icon>
            <saf-sr-only>Edit John Doe's profile</saf-sr-only>
          </button>
        </td>
      </tr>
      
      <tr>
        <td>
          <strong>Jane Smith</strong>
          <saf-sr-only>Employee ID: EMP002</saf-sr-only>
        </td>
        <td>Design</td>
        <td>
          <span class="status on-leave">On Leave</span>
          <saf-sr-only>Currently on medical leave, expected return March 15th</saf-sr-only>
        </td>
        <td>
          <button class="action-btn" disabled>
            <saf-icon icon-name="envelope" appearance="light"></saf-icon>
            <saf-sr-only>Email unavailable - employee is on leave</saf-sr-only>
          </button>
          <button class="action-btn">
            <saf-icon icon-name="edit" appearance="light"></saf-icon>
            <saf-sr-only>Edit Jane Smith's profile</saf-sr-only>
          </button>
        </td>
      </tr>
      
      <tr>
        <td>
          <strong>Mike Johnson</strong>
          <saf-sr-only>Employee ID: EMP003</saf-sr-only>
        </td>
        <td>Marketing</td>
        <td>
          <span class="status active">Active</span>
          <saf-sr-only>Part-time employee, 20 hours per week</saf-sr-only>
        </td>
        <td>
          <button class="action-btn">
            <saf-icon icon-name="envelope" appearance="light"></saf-icon>
            <saf-sr-only>Send email to Mike Johnson</saf-sr-only>
          </button>
          <button class="action-btn">
            <saf-icon icon-name="edit" appearance="light"></saf-icon>
            <saf-sr-only>Edit Mike Johnson's profile</saf-sr-only>
          </button>
        </td>
      </tr>
    </tbody>
  </table>
  
  <!-- Enhanced list with status -->
  <div class="status-list">
    <h4>Project Status List</h4>
    <ul class="project-list" role="list">
      <li class="project-item">
        <div class="project-info">
          <h5>Website Redesign</h5>
          <div class="project-meta">
            <span class="progress-indicator" style="width: 75%"></span>
            <saf-sr-only>Project progress: 75% complete, 3 weeks remaining</saf-sr-only>
          </div>
        </div>
        <div class="project-status">
          <span class="status on-track">On Track</span>
          <saf-sr-only>Expected completion: March 30th, 2024</saf-sr-only>
        </div>
      </li>
      
      <li class="project-item">
        <div class="project-info">
          <h5>Mobile App Development</h5>
          <div class="project-meta">
            <span class="progress-indicator" style="width: 45%"></span>
            <saf-sr-only>Project progress: 45% complete, 6 weeks remaining</saf-sr-only>
          </div>
        </div>
        <div class="project-status">
          <span class="status at-risk">At Risk</span>
          <saf-sr-only>Delayed due to resource constraints, may need additional 2 weeks</saf-sr-only>
        </div>
      </li>
      
      <li class="project-item">
        <div class="project-info">
          <h5>User Research Study</h5>
          <div class="project-meta">
            <span class="progress-indicator" style="width: 100%"></span>
            <saf-sr-only>Project progress: 100% complete</saf-sr-only>
          </div>
        </div>
        <div class="project-status">
          <span class="status completed">Completed</span>
          <saf-sr-only>Successfully completed on February 28th, 2024</saf-sr-only>
        </div>
      </li>
    </ul>
  </div>
</div>

<style>
.table-enhancements {
  padding: 2rem;
}

.enhanced-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 2rem;
  border: 1px solid #e0e0e0;
}

.enhanced-table caption {
  text-align: left;
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #333;
}

.enhanced-table th,
.enhanced-table td {
  padding: 1rem;
  text-align: left;
  border-bottom: 1px solid #e0e0e0;
}

.enhanced-table th {
  background: #f8f9fa;
  font-weight: 600;
  color: #333;
}

.enhanced-table tbody tr:hover {
  background: #f8f9fa;
}

.status {
  padding: 0.25rem 0.5rem;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
}

.status.active {
  background: #d4edda;
  color: #155724;
}

.status.on-leave {
  background: #fff3cd;
  color: #856404;
}

.status.on-track {
  background: #d4edda;
  color: #155724;
}

.status.at-risk {
  background: #fff3cd;
  color: #856404;
}

.status.completed {
  background: #d1ecf1;
  color: #0c5460;
}

.action-btn {
  width: 32px;
  height: 32px;
  border: 1px solid #ccc;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 0.5rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.action-btn:hover:not(:disabled) {
  border-color: #007acc;
  background: #f0f8ff;
}

.action-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.status-list {
  margin-top: 2rem;
}

.status-list h4 {
  margin-bottom: 1rem;
  color: #333;
}

.project-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.project-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  margin-bottom: 0.5rem;
  background: white;
}

.project-info h5 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.project-meta {
  position: relative;
  width: 200px;
  height: 4px;
  background: #e0e0e0;
  border-radius: 2px;
  overflow: hidden;
}

.progress-indicator {
  height: 100%;
  background: #007acc;
  display: block;
  transition: width 0.3s ease;
}

.project-status {
  margin-left: 1rem;
}
</style>
```

### Navigation and Interaction Context

```html
<div class="navigation-context">
  <h3>Navigation and Interaction Context</h3>
  
  <!-- Breadcrumb navigation -->
  <nav aria-label="Breadcrumb">
    <ol class="breadcrumb">
      <li>
        <a href="/dashboard">
          Dashboard
          <saf-sr-only>- Go to main dashboard</saf-sr-only>
        </a>
      </li>
      <li>
        <span aria-hidden="true">/</span>
        <a href="/projects">
          Projects
          <saf-sr-only>- View all projects</saf-sr-only>
        </a>
      </li>
      <li>
        <span aria-hidden="true">/</span>
        <span aria-current="page">
          Website Redesign
          <saf-sr-only>- Current page</saf-sr-only>
        </span>
      </li>
    </ol>
  </nav>
  
  <!-- Pagination with context -->
  <nav class="pagination" aria-label="Page navigation">
    <ul class="page-list">
      <li>
        <button class="page-btn" disabled>
          <saf-icon icon-name="chevron-left" appearance="light"></saf-icon>
          <saf-sr-only>Previous page - no previous pages available</saf-sr-only>
        </button>
      </li>
      <li>
        <button class="page-btn current" aria-current="page">
          1
          <saf-sr-only>Page 1, current page</saf-sr-only>
        </button>
      </li>
      <li>
        <button class="page-btn">
          2
          <saf-sr-only>Go to page 2</saf-sr-only>
        </button>
      </li>
      <li>
        <button class="page-btn">
          3
          <saf-sr-only>Go to page 3</saf-sr-only>
        </button>
      </li>
      <li>
        <span class="page-ellipsis">
          ...
          <saf-sr-only>More pages available</saf-sr-only>
        </span>
      </li>
      <li>
        <button class="page-btn">
          15
          <saf-sr-only>Go to page 15, last page</saf-sr-only>
        </button>
      </li>
      <li>
        <button class="page-btn">
          <saf-icon icon-name="chevron-right" appearance="light"></saf-icon>
          <saf-sr-only>Next page - go to page 2</saf-sr-only>
        </button>
      </li>
    </ul>
    <div class="pagination-info">
      <saf-sr-only>
        Showing items 1 to 20 of 300 total results across 15 pages
      </saf-sr-only>
      <span aria-hidden="true">1-20 of 300</span>
    </div>
  </nav>
  
  <!-- Card with interaction hints -->
  <div class="card-grid">
    <article class="info-card" tabindex="0" role="button">
      <header class="card-header">
        <h4>Project Alpha</h4>
        <saf-sr-only>Clickable card - press Enter or Space to view details</saf-sr-only>
      </header>
      <div class="card-content">
        <p>Website redesign project with modern UI/UX improvements.</p>
        <div class="card-stats">
          <span>75% Complete</span>
          <saf-sr-only>Progress: 75 percent complete, 3 weeks remaining</saf-sr-only>
        </div>
      </div>
      <footer class="card-footer">
        <span class="due-date">Due: March 30</span>
        <saf-sr-only>Due date: March 30th, 2024</saf-sr-only>
      </footer>
    </article>
    
    <article class="info-card" tabindex="0" role="button">
      <header class="card-header">
        <h4>Project Beta</h4>
        <saf-sr-only>Clickable card - press Enter or Space to view details</saf-sr-only>
      </header>
      <div class="card-content">
        <p>Mobile application development for iOS and Android platforms.</p>
        <div class="card-stats">
          <span>45% Complete</span>
          <saf-sr-only>Progress: 45 percent complete, 6 weeks remaining, currently at risk</saf-sr-only>
        </div>
      </div>
      <footer class="card-footer">
        <span class="due-date overdue">Due: April 15</span>
        <saf-sr-only>Due date: April 15th, 2024, project is at risk</saf-sr-only>
      </footer>
    </article>
  </div>
  
  <!-- Search with live results -->
  <div class="search-section">
    <h4>Search with Live Results</h4>
    <div class="search-container">
      <label for="live-search">Search projects:</label>
      <input 
        type="search" 
        id="live-search" 
        placeholder="Type to search..."
        aria-describedby="search-results"
      />
      <saf-sr-only id="search-status" aria-live="polite"></saf-sr-only>
      
      <div id="search-results" class="search-results" role="region" aria-label="Search results">
        <saf-sr-only>Search results will appear here as you type</saf-sr-only>
        <!-- Results would be populated dynamically -->
      </div>
    </div>
  </div>
</div>

<style>
.navigation-context {
  padding: 2rem;
}

.breadcrumb {
  display: flex;
  align-items: center;
  list-style: none;
  padding: 0;
  margin: 0 0 2rem 0;
  font-size: 14px;
}

.breadcrumb li {
  display: flex;
  align-items: center;
}

.breadcrumb a {
  color: #007acc;
  text-decoration: none;
  padding: 0.5rem;
}

.breadcrumb a:hover {
  text-decoration: underline;
}

.breadcrumb [aria-current="page"] {
  color: #666;
  font-weight: 500;
  padding: 0.5rem;
}

.pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 2rem 0;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 4px;
}

.page-list {
  display: flex;
  align-items: center;
  list-style: none;
  padding: 0;
  margin: 0;
  gap: 0.25rem;
}

.page-btn {
  min-width: 36px;
  height: 36px;
  border: 1px solid #ccc;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
}

.page-btn:hover:not(:disabled) {
  border-color: #007acc;
  background: #f0f8ff;
}

.page-btn.current {
  background: #007acc;
  border-color: #007acc;
  color: white;
}

.page-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.page-ellipsis {
  padding: 0.5rem;
  color: #666;
}

.pagination-info {
  font-size: 14px;
  color: #666;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin: 2rem 0;
}

.info-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
  padding: 1.5rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.info-card:hover,
.info-card:focus {
  border-color: #007acc;
  box-shadow: 0 2px 8px rgba(0, 122, 204, 0.1);
  outline: none;
}

.card-header h4 {
  margin: 0 0 1rem 0;
  color: #333;
}

.card-content p {
  margin: 0 0 1rem 0;
  color: #666;
  line-height: 1.5;
}

.card-stats {
  font-size: 14px;
  color: #007acc;
  font-weight: 500;
}

.card-footer {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #f0f0f0;
}

.due-date {
  font-size: 12px;
  color: #666;
}

.due-date.overdue {
  color: #dc3545;
  font-weight: 500;
}

.search-section {
  margin-top: 2rem;
}

.search-section h4 {
  margin-bottom: 1rem;
  color: #333;
}

.search-container {
  max-width: 400px;
}

.search-container label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #333;
}

.search-container input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  box-sizing: border-box;
}

.search-container input:focus {
  outline: none;
  border-color: #007acc;
  box-shadow: 0 0 0 2px rgba(0, 122, 204, 0.2);
}

.search-results {
  margin-top: 0.5rem;
  min-height: 50px;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: #fafafa;
  color: #666;
  font-style: italic;
}
</style>
```

### Status and Loading States

```html
<div class="status-loading">
  <h3>Status and Loading State Context</h3>
  
  <!-- Loading states with context -->
  <div class="loading-examples">
    <div class="loading-card">
      <div class="loading-spinner" aria-hidden="true"></div>
      <p>Loading user data...</p>
      <saf-sr-only>Please wait while we load your user profile information. This may take a few seconds.</saf-sr-only>
    </div>
    
    <div class="upload-progress">
      <div class="progress-bar">
        <div class="progress-fill" style="width: 67%"></div>
      </div>
      <p>Uploading file...</p>
      <saf-sr-only>File upload in progress: 67% complete. Upload speed: 2.3 MB per second. Estimated time remaining: 15 seconds.</saf-sr-only>
    </div>
    
    <div class="sync-status">
      <div class="sync-indicator syncing" aria-hidden="true"></div>
      <p>Syncing changes...</p>
      <saf-sr-only>Synchronizing your changes with the server. 5 items remaining to sync.</saf-sr-only>
    </div>
  </div>
  
  <!-- Alert states with additional context -->
  <div class="alert-examples">
    <div class="alert success" role="alert">
      <div class="alert-icon" aria-hidden="true">✓</div>
      <div class="alert-content">
        <strong>Success!</strong> Your profile has been updated.
        <saf-sr-only>All changes have been saved successfully and are now active.</saf-sr-only>
      </div>
    </div>
    
    <div class="alert warning" role="alert">
      <div class="alert-icon" aria-hidden="true">⚠</div>
      <div class="alert-content">
        <strong>Warning:</strong> Some features may be limited.
        <saf-sr-only>Your current subscription plan limits access to advanced features. Upgrade your plan to access all functionality.</saf-sr-only>
      </div>
    </div>
    
    <div class="alert error" role="alert">
      <div class="alert-icon" aria-hidden="true">✕</div>
      <div class="alert-content">
        <strong>Error:</strong> Unable to save changes.
        <saf-sr-only>There was a connection error while saving your changes. Please check your internet connection and try again. Your work has been temporarily saved locally.</saf-sr-only>
        <button class="retry-btn">Retry</button>
      </div>
    </div>
  </div>
</div>

<style>
.status-loading {
  padding: 2rem;
}

.loading-examples {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.loading-card,
.upload-progress,
.sync-status {
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: white;
  text-align: center;
}

.loading-spinner {
  width: 32px;
  height: 32px;
  border: 3px solid #f3f3f3;
  border-top: 3px solid #007acc;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto 1rem auto;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.progress-bar {
  width: 100%;
  height: 8px;
  background: #e0e0e0;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 1rem;
}

.progress-fill {
  height: 100%;
  background: #007acc;
  transition: width 0.3s ease;
}

.sync-indicator {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  margin: 0 auto 1rem auto;
}

.sync-indicator.syncing {
  background: #007acc;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.alert-examples {
  display: grid;
  gap: 1rem;
}

.alert {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1rem;
  border-radius: 4px;
  border-left: 4px solid;
}

.alert.success {
  background: #d4f6d4;
  border-left-color: #28a745;
  color: #155724;
}

.alert.warning {
  background: #fff3cd;
  border-left-color: #ffc107;
  color: #856404;
}

.alert.error {
  background: #f8d7da;
  border-left-color: #dc3545;
  color: #721c24;
}

.alert-icon {
  font-size: 20px;
  font-weight: bold;
  flex-shrink: 0;
}

.alert-content {
  flex: 1;
}

.alert-content strong {
  display: block;
  margin-bottom: 0.25rem;
}

.retry-btn {
  margin-top: 0.5rem;
  padding: 0.5rem 1rem;
  background: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
}

.retry-btn:hover {
  background: #c82333;
}
</style>
```

## Framework Integration

### React Example

```tsx
import React from 'react';

interface SrOnlyProps {
  children: React.ReactNode;
  id?: string;
  className?: string;
}

const SafSrOnlyComponent: React.FC<SrOnlyProps> = ({
  children,
  id,
  className
}) => {
  return (
    <saf-sr-only id={id} className={className}>
      {children}
    </saf-sr-only>
  );
};

// Form field with screen reader context
interface FormFieldProps {
  label: string;
  type: string;
  id: string;
  required?: boolean;
  helperText?: string;
  srOnlyInstructions?: string;
}

const AccessibleFormField: React.FC<FormFieldProps> = ({
  label,
  type,
  id,
  required,
  helperText,
  srOnlyInstructions
}) => {
  return (
    <div className="form-field">
      <label htmlFor={id}>
        {label}
        {required && (
          <>
            <span className="required-indicator" aria-hidden="true">*</span>
            <SafSrOnlyComponent>required field</SafSrOnlyComponent>
          </>
        )}
      </label>
      
      <input 
        type={type}
        id={id}
        name={id}
        required={required}
        aria-describedby={srOnlyInstructions ? `${id}-instructions` : undefined}
      />
      
      {srOnlyInstructions && (
        <SafSrOnlyComponent id={`${id}-instructions`}>
          {srOnlyInstructions}
        </SafSrOnlyComponent>
      )}
      
      {helperText && (
        <div className="helper-text">{helperText}</div>
      )}
    </div>
  );
};

// Button with contextual information
interface AccessibleButtonProps {
  children: React.ReactNode;
  onClick: () => void;
  srOnlyContext?: string;
  variant?: 'primary' | 'secondary' | 'icon';
  disabled?: boolean;
}

const AccessibleButton: React.FC<AccessibleButtonProps> = ({
  children,
  onClick,
  srOnlyContext,
  variant = 'primary',
  disabled
}) => {
  return (
    <button 
      className={`btn btn-${variant}`}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
      {srOnlyContext && (
        <SafSrOnlyComponent>{srOnlyContext}</SafSrOnlyComponent>
      )}
    </button>
  );
};

// Usage examples
const FormExample: React.FC = () => {
  return (
    <form>
      <AccessibleFormField
        label="Email Address"
        type="email"
        id="email"
        required
        helperText="We'll never share your email"
        srOnlyInstructions="Enter a valid email address for account notifications"
      />
      
      <AccessibleFormField
        label="Password"
        type="password"
        id="password"
        required
        helperText="At least 8 characters"
        srOnlyInstructions="Password must contain at least 8 characters with uppercase, lowercase, and numeric characters"
      />
      
      <div className="button-group">
        <AccessibleButton
          onClick={() => console.log('Submit')}
          srOnlyContext="using the information provided above"
        >
          Create Account
        </AccessibleButton>
        
        <AccessibleButton
          variant="icon"
          onClick={() => console.log('Help')}
          srOnlyContext="- opens help documentation"
        >
          ?
        </AccessibleButton>
      </div>
    </form>
  );
};
```

### Angular Example

```typescript
// sr-only.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-saf-sr-only',
  template: `
    <saf-sr-only [attr.id]="id" [class]="className">
      <ng-content></ng-content>
    </saf-sr-only>
  `
})
export class SafSrOnlyComponent {
  @Input() id?: string;
  @Input() className?: string;
}

// accessible-form-field.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-accessible-form-field',
  template: `
    <div class="form-field">
      <label [for]="id">
        {{ label }}
        <span *ngIf="required" class="required-indicator" aria-hidden="true">*</span>
        <app-saf-sr-only *ngIf="required">required field</app-saf-sr-only>
      </label>
      
      <input 
        [type]="type"
        [id]="id"
        [name]="id"
        [required]="required"
        [attr.aria-describedby]="srOnlyInstructions ? id + '-instructions' : null"
      />
      
      <app-saf-sr-only 
        *ngIf="srOnlyInstructions"
        [id]="id + '-instructions'"
      >
        {{ srOnlyInstructions }}
      </app-saf-sr-only>
      
      <div *ngIf="helperText" class="helper-text">
        {{ helperText }}
      </div>
    </div>
  `
})
export class AccessibleFormFieldComponent {
  @Input() label!: string;
  @Input() type!: string;
  @Input() id!: string;
  @Input() required?: boolean;
  @Input() helperText?: string;
  @Input() srOnlyInstructions?: string;
}

// Usage in component template
/*
<app-accessible-form-field
  label="Email Address"
  type="email"
  id="email"
  [required]="true"
  helperText="We'll never share your email"
  srOnlyInstructions="Enter a valid email address for account notifications">
</app-accessible-form-field>

<button class="btn-primary">
  Save Changes
  <app-saf-sr-only>to your user profile</app-saf-sr-only>
</button>
*/
```

### Vue Example

```vue
<template>
  <saf-sr-only :id="id" :class="className">
    <slot></slot>
  </saf-sr-only>
</template>

<script>
export default {
  name: 'SafSrOnlyComponent',
  props: {
    id: String,
    className: String
  }
};
</script>

<!-- Accessible Form Field Component -->
<template>
  <div class="form-field">
    <label :for="id">
      {{ label }}
      <span v-if="required" class="required-indicator" aria-hidden="true">*</span>
      <SafSrOnlyComponent v-if="required">required field</SafSrOnlyComponent>
    </label>
    
    <input 
      :type="type"
      :id="id"
      :name="id"
      :required="required"
      :aria-describedby="srOnlyInstructions ? `${id}-instructions` : null"
    />
    
    <SafSrOnlyComponent 
      v-if="srOnlyInstructions"
      :id="`${id}-instructions`"
    >
      {{ srOnlyInstructions }}
    </SafSrOnlyComponent>
    
    <div v-if="helperText" class="helper-text">
      {{ helperText }}
    </div>
  </div>
</template>

<script>
import SafSrOnlyComponent from './SafSrOnlyComponent.vue';

export default {
  name: 'AccessibleFormField',
  components: {
    SafSrOnlyComponent
  },
  props: {
    label: {
      type: String,
      required: true
    },
    type: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    },
    required: Boolean,
    helperText: String,
    srOnlyInstructions: String
  }
};
</script>

<!-- Usage Example -->
<!--
<template>
  <form class="accessible-form">
    <AccessibleFormField
      label="Email Address"
      type="email"
      id="email"
      :required="true"
      helper-text="We'll never share your email"
      sr-only-instructions="Enter a valid email address for account notifications"
    />
    
    <button class="btn-primary">
      Create Account
      <SafSrOnlyComponent>using the information provided</SafSrOnlyComponent>
    </button>
  </form>
</template>
-->
```

## Accessibility Features

### Screen Reader Support

- **Visually Hidden Content**: Content is completely hidden from visual display but accessible to screen readers
- **Proper Semantics**: Maintains semantic structure and meaning for assistive technologies
- **Context Enhancement**: Provides additional context without visual clutter
- **Live Regions**: Works well with ARIA live regions for dynamic content announcements

### Keyboard Navigation

- Screen reader only content doesn't interfere with keyboard navigation
- Focus remains on interactive elements while providing additional context
- Compatible with all keyboard navigation patterns

### ARIA Integration

- Works seamlessly with ARIA attributes and roles
- Enhances ARIA descriptions and labels
- Supports aria-describedby relationships
- Compatible with aria-live regions for dynamic updates

## Best Practices

### Content Guidelines

- **Be Descriptive**: Provide meaningful context that helps screen reader users understand the interface
- **Avoid Redundancy**: Don't repeat information that's already available to screen readers
- **Use Natural Language**: Write in clear, conversational language rather than technical jargon
- **Consider Context**: Think about what additional information would be helpful for non-visual users

### Implementation Guidelines

- **Use Sparingly**: Only add screen reader content when it provides genuine value
- **Test with Screen Readers**: Verify content with actual screen reading software
- **Keep Content Updated**: Ensure screen reader content stays current with visual changes
- **Consider Performance**: Large amounts of hidden content can impact screen reader performance

### Common Use Cases

- **Icon Buttons**: Provide context for icons without visible text
- **Form Instructions**: Add detailed instructions without visual clutter
- **Status Information**: Explain status indicators and progress states
- **Navigation Context**: Clarify navigation relationships and current location
- **Data Tables**: Add context for complex data relationships
- **Interactive Elements**: Explain the purpose and result of interactions

### Anti-Patterns to Avoid

- **Visual Duplication**: Don't repeat exactly what's already visible
- **Excessive Content**: Avoid overwhelming screen reader users with too much information
- **Technical Jargon**: Don't use overly technical language that may confuse users
- **Outdated Information**: Ensure hidden content stays synchronized with visual content

## Related Components

- **SafSkipLink**: For keyboard navigation shortcuts
- **SafLabel**: For form field labeling and associations
- **SafAlert**: For announcements and status updates with live regions
- **All Interactive Components**: Any component that benefits from additional context

---

*This documentation covers SafSrOnly v3.x. For migration guides and version-specific changes, see the [Changelog](./CHANGELOG.md).*
