# SafTextArea Component Documentation

## Overview

The **SafTextArea** component is a multi-line text input control that allows users to enter and edit larger amounts of text. It implements comprehensive accessibility features, validation support, customizable resize behavior, and character counting functionality.

## React Implementation

### Basic Usage

```tsx
import { SafTextArea } from '@saffron/react-components';
import { useState } from 'react';

function BasicTextArea() {
  const [message, setMessage] = useState('');

  return (
    <SafTextArea
      value={message}
      onChange={(event) => setMessage(event.target.value)}
      placeholder="Enter your message here..."
      rows={4}
    >
      <label>Your Message</label>
    </SafTextArea>
  );
}
```

### Advanced Usage with Validation

```tsx
import { SafTextArea } from '@saffron/react-components';
import { useState } from 'react';

function AdvancedTextArea() {
  const [formData, setFormData] = useState({
    description: '',
    comments: '',
    feedback: ''
  });
  const [errors, setErrors] = useState({});
  const [charCounts, setCharCounts] = useState({});

  const textAreaConfigs = {
    description: {
      label: 'Project Description',
      placeholder: 'Describe your project in detail...',
      minLength: 50,
      maxLength: 500,
      rows: 4,
      required: true
    },
    comments: {
      label: 'Additional Comments',
      placeholder: 'Any additional information...',
      maxLength: 1000,
      rows: 6,
      required: false
    },
    feedback: {
      label: 'Feedback',
      placeholder: 'Please provide your feedback...',
      minLength: 10,
      maxLength: 250,
      rows: 3,
      required: true,
      resize: 'vertical'
    }
  };

  const handleTextAreaChange = (field: string) => (event: React.ChangeEvent<HTMLTextAreaElement>) => {
    const value = event.target.value;
    const config = textAreaConfigs[field];

    setFormData(prev => ({
      ...prev,
      [field]: value
    }));

    setCharCounts(prev => ({
      ...prev,
      [field]: value.length
    }));

    // Validate in real-time for character limits
    const newErrors = { ...errors };
    if (config.maxLength && value.length > config.maxLength) {
      newErrors[field] = `Maximum ${config.maxLength} characters allowed`;
    } else if (config.minLength && value.length > 0 && value.length < config.minLength) {
      newErrors[field] = `Minimum ${config.minLength} characters required`;
    } else {
      delete newErrors[field];
    }
    setErrors(newErrors);
  };

  const validateForm = () => {
    const newErrors = {};
    
    Object.entries(textAreaConfigs).forEach(([field, config]) => {
      const value = formData[field];
      const trimmedValue = value.trim();

      if (config.required && !trimmedValue) {
        newErrors[field] = `${config.label} is required`;
      } else if (config.minLength && trimmedValue.length < config.minLength) {
        newErrors[field] = `${config.label} must be at least ${config.minLength} characters`;
      } else if (config.maxLength && value.length > config.maxLength) {
        newErrors[field] = `${config.label} must not exceed ${config.maxLength} characters`;
      }
    });

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const getCharacterDisplay = (field: string) => {
    const config = textAreaConfigs[field];
    const count = charCounts[field] || 0;
    const isNearLimit = config.maxLength && count > config.maxLength * 0.8;
    const isOverLimit = config.maxLength && count > config.maxLength;
    
    return (
      <div className={`char-count ${isNearLimit ? 'warning' : ''} ${isOverLimit ? 'error' : ''}`}>
        {count}{config.maxLength ? ` / ${config.maxLength}` : ''}
      </div>
    );
  };

  return (
    <form className="project-form">
      <h3>Project Information Form</h3>

      {Object.entries(textAreaConfigs).map(([field, config]) => (
        <div key={field} className="textarea-group">
          <SafTextArea
            name={field}
            value={formData[field]}
            onChange={handleTextAreaChange(field)}
            placeholder={config.placeholder}
            rows={config.rows}
            minLength={config.minLength}
            maxLength={config.maxLength}
            resize={config.resize || 'both'}
            invalid={!!errors[field]}
            validationMessage={errors[field]}
            required={config.required}
            density="comfortable"
            a11yAriaDescription={`${config.label}${config.required ? ' (required)' : ''}`}
          >
            <label>
              {config.label} {config.required && '*'}
            </label>
          </SafTextArea>
          {getCharacterDisplay(field)}
        </div>
      ))}

      <div className="form-actions">
        <button type="button" onClick={validateForm}>
          Submit Project
        </button>
        <button type="button" onClick={() => {
          setFormData({ description: '', comments: '', feedback: '' });
          setCharCounts({});
          setErrors({});
        }}>
          Clear Form
        </button>
      </div>
    </form>
  );
}
```

### Auto-Expanding TextArea

```tsx
import { SafTextArea } from '@saffron/react-components';
import { useState, useRef, useEffect } from 'react';

function AutoExpandingTextArea() {
  const [content, setContent] = useState('');
  const textAreaRef = useRef<HTMLTextAreaElement>(null);

  useEffect(() => {
    const textArea = textAreaRef.current;
    if (textArea) {
      // Reset height to auto to get the correct scrollHeight
      textArea.style.height = 'auto';
      // Set the height to the scrollHeight
      textArea.style.height = `${textArea.scrollHeight}px`;
    }
  }, [content]);

  const handleChange = (event: React.ChangeEvent<HTMLTextAreaElement>) => {
    setContent(event.target.value);
  };

  return (
    <div className="auto-expanding-container">
      <SafTextArea
        ref={textAreaRef}
        value={content}
        onChange={handleChange}
        placeholder="Start typing... This textarea will expand as you type."
        rows={3}
        resize="none"
        style={{ 
          minHeight: '80px',
          maxHeight: '300px',
          overflow: content.length > 500 ? 'auto' : 'hidden'
        }}
      >
        <label>Auto-Expanding Notes</label>
      </SafTextArea>
      
      <small className="helper-text">
        This textarea automatically adjusts its height based on content.
      </small>
    </div>
  );
}
```

### Rich Text Preview

```tsx
import { SafTextArea } from '@saffron/react-components';
import { useState } from 'react';

function RichTextPreview() {
  const [markdownContent, setMarkdownContent] = useState('# Heading\n\nType your **markdown** content here!\n\n- List item 1\n- List item 2\n\n[Link example](https://example.com)');
  const [showPreview, setShowPreview] = useState(false);

  // Simple markdown to HTML converter (for demo purposes)
  const convertMarkdownToHTML = (markdown: string) => {
    return markdown
      .replace(/^# (.*$)/gim, '<h1>$1</h1>')
      .replace(/^\## (.*$)/gim, '<h2>$1</h2>')
      .replace(/\*\*(.*)\*\*/gim, '<strong>$1</strong>')
      .replace(/\*(.*)\*/gim, '<em>$1</em>')
      .replace(/^\- (.*$)/gim, '<li>$1</li>')
      .replace(/\[(.*?)\]\((.*?)\)/gim, '<a href="$2" target="_blank">$1</a>')
      .replace(/\n/gim, '<br>');
  };

  return (
    <div className="markdown-editor">
      <div className="editor-controls">
        <button
          type="button"
          onClick={() => setShowPreview(!showPreview)}
          className={showPreview ? 'active' : ''}
        >
          {showPreview ? 'Edit' : 'Preview'}
        </button>
      </div>

      {showPreview ? (
        <div 
          className="markdown-preview"
          dangerouslySetInnerHTML={{ 
            __html: convertMarkdownToHTML(markdownContent) 
          }}
        />
      ) : (
        <SafTextArea
          value={markdownContent}
          onChange={(e) => setMarkdownContent(e.target.value)}
          placeholder="Enter markdown content..."
          rows={15}
          resize="vertical"
          style={{ fontFamily: 'monospace', fontSize: '14px' }}
        >
          <label>Markdown Editor</label>
        </SafTextArea>
      )}

      <div className="editor-help">
        <small>
          Supports: **bold**, *italic*, # headers, - lists, [links](url)
        </small>
      </div>
    </div>
  );
}
```

### API Reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `undefined` | The text content of the textarea |
| `placeholder` | `string` | `undefined` | Placeholder text displayed when empty |
| `disabled` | `boolean` | `false` | Disables the textarea |
| `readOnly` | `boolean` | `false` | Makes the textarea read-only |
| `invalid` | `boolean` | `false` | Indicates validation error state |
| `validationMessage` | `string` | `undefined` | Error message displayed when invalid |
| `required` | `boolean` | `false` | Indicates if the field is required |
| `name` | `string` | `undefined` | Name attribute for form submission |
| `rows` | `number` | `3` | Number of visible text lines |
| `cols` | `number` | `undefined` | Width of the textarea in characters |
| `minLength` | `number` | `undefined` | Minimum number of characters |
| `maxLength` | `number` | `undefined` | Maximum number of characters |
| `wrap` | `'hard' \| 'soft' \| 'off'` | `'soft'` | How text wrapping is handled |
| `resize` | `'none' \| 'both' \| 'horizontal' \| 'vertical'` | `'both'` | Resize behavior |
| `autofocus` | `boolean` | `false` | Automatically focus on page load |
| `spellCheck` | `boolean` | `undefined` | Enable/disable spell checking |
| `density` | `'compact' \| 'comfortable' \| 'spacious'` | `'comfortable'` | Visual density |
| `a11yAriaLabel` | `string` | `undefined` | Accessible label for screen readers |
| `a11yAriaDescription` | `string` | `undefined` | Additional description for accessibility |
| `onChange` | `(event: ChangeEvent) => void` | `undefined` | Handler for content changes |
| `onFocus` | `(event: FocusEvent) => void` | `undefined` | Handler for focus events |
| `onBlur` | `(event: FocusEvent) => void` | `undefined` | Handler for blur events |
| `onInput` | `(event: InputEvent) => void` | `undefined` | Handler for input events |

## Angular Implementation

### Basic Usage

```typescript
// component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-textarea',
  template: `
    <saf-text-area
      [value]="message"
      (change)="onMessageChange($event)"
      placeholder="Enter your message here..."
      rows="4">
      <label>Your Message</label>
    </saf-text-area>
  `
})
export class BasicTextAreaComponent {
  message = '';

  onMessageChange(event: any) {
    this.message = event.target.value;
  }
}
```

### Advanced Usage with Forms

```typescript
// component.ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-advanced-textarea',
  template: `
    <form [formGroup]="projectForm" (ngSubmit)="onSubmit()">
      <h3>Project Information Form</h3>

      <div class="textarea-group">
        <saf-text-area
          formControlName="description"
          placeholder="Describe your project in detail..."
          rows="4"
          [min-length]="50"
          [max-length]="500"
          [invalid]="isFieldInvalid('description')"
          [validation-message]="getErrorMessage('description')"
          density="comfortable"
          a11y-aria-description="Project description (required)">
          <label>Project Description *</label>
        </saf-text-area>
        <div class="char-count" 
             [class.warning]="getCharCount('description') > 400"
             [class.error]="getCharCount('description') > 500">
          {{ getCharCount('description') }} / 500
        </div>
      </div>

      <div class="textarea-group">
        <saf-text-area
          formControlName="comments"
          placeholder="Any additional information..."
          rows="6"
          [max-length]="1000"
          resize="vertical">
          <label>Additional Comments</label>
        </saf-text-area>
        <div class="char-count">
          {{ getCharCount('comments') }} / 1000
        </div>
      </div>

      <div class="textarea-group">
        <saf-text-area
          formControlName="feedback"
          placeholder="Please provide your feedback..."
          rows="3"
          [min-length]="10"
          [max-length]="250"
          [invalid]="isFieldInvalid('feedback')"
          [validation-message]="getErrorMessage('feedback')"
          resize="vertical">
          <label>Feedback *</label>
        </saf-text-area>
        <div class="char-count"
             [class.warning]="getCharCount('feedback') > 200"
             [class.error]="getCharCount('feedback') > 250">
          {{ getCharCount('feedback') }} / 250
        </div>
      </div>

      <div class="form-actions">
        <button type="submit" [disabled]="projectForm.invalid">
          Submit Project
        </button>
        <button type="button" (click)="clearForm()">
          Clear Form
        </button>
      </div>
    </form>
  `
})
export class AdvancedTextAreaComponent implements OnInit {
  projectForm: FormGroup;

  constructor(private fb: FormBuilder) {}

  ngOnInit() {
    this.projectForm = this.fb.group({
      description: ['', [
        Validators.required,
        Validators.minLength(50),
        Validators.maxLength(500)
      ]],
      comments: ['', [Validators.maxLength(1000)]],
      feedback: ['', [
        Validators.required,
        Validators.minLength(10),
        Validators.maxLength(250)
      ]]
    });
  }

  isFieldInvalid(fieldName: string): boolean {
    const field = this.projectForm.get(fieldName);
    return !!(field && field.invalid && (field.dirty || field.touched));
  }

  getErrorMessage(fieldName: string): string {
    const field = this.projectForm.get(fieldName);
    if (field?.errors?.['required']) {
      return `${this.getFieldLabel(fieldName)} is required`;
    }
    if (field?.errors?.['minlength']) {
      const minLength = field.errors['minlength'].requiredLength;
      return `${this.getFieldLabel(fieldName)} must be at least ${minLength} characters`;
    }
    if (field?.errors?.['maxlength']) {
      const maxLength = field.errors['maxlength'].requiredLength;
      return `${this.getFieldLabel(fieldName)} must not exceed ${maxLength} characters`;
    }
    return '';
  }

  getFieldLabel(fieldName: string): string {
    const labels = {
      description: 'Project Description',
      comments: 'Additional Comments',
      feedback: 'Feedback'
    };
    return labels[fieldName] || fieldName;
  }

  getCharCount(fieldName: string): number {
    const value = this.projectForm.get(fieldName)?.value || '';
    return value.length;
  }

  clearForm() {
    this.projectForm.reset();
  }

  onSubmit() {
    if (this.projectForm.valid) {
      console.log('Form submitted:', this.projectForm.value);
    } else {
      this.markFormGroupTouched();
    }
  }

  private markFormGroupTouched() {
    Object.keys(this.projectForm.controls).forEach(key => {
      this.projectForm.get(key)?.markAsTouched();
    });
  }
}
```

### API Reference

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `value` | `string` | `undefined` | Textarea content |
| `placeholder` | `string` | `undefined` | Placeholder text |
| `disabled` | `boolean` | `false` | Disabled state |
| `readOnly` | `boolean` | `false` | Read-only state |
| `invalid` | `boolean` | `false` | Error state |
| `validationMessage` | `string` | `undefined` | Error message |
| `required` | `boolean` | `false` | Required field |
| `name` | `string` | `undefined` | Form field name |
| `rows` | `number` | `3` | Visible text lines |
| `cols` | `number` | `undefined` | Width in characters |
| `minLength` | `number` | `undefined` | Minimum characters |
| `maxLength` | `number` | `undefined` | Maximum characters |
| `wrap` | `string` | `'soft'` | Text wrapping |
| `resize` | `string` | `'both'` | Resize behavior |
| `autofocus` | `boolean` | `false` | Auto-focus |
| `spellCheck` | `boolean` | `undefined` | Spell checking |
| `density` | `string` | `'comfortable'` | Visual density |
| `a11yAriaLabel` | `string` | `undefined` | Accessibility label |
| `a11yAriaDescription` | `string` | `undefined` | Accessibility description |

| Output | Type | Description |
|--------|------|-------------|
| `change` | `Event` | Emitted when content changes |
| `input` | `Event` | Emitted during text input |
| `focus` | `Event` | Emitted when textarea receives focus |
| `blur` | `Event` | Emitted when textarea loses focus |

## Best Practices

### Accessibility
- **Clear labels**: Provide descriptive labels that explain the purpose of the textarea
- **Character limits**: Announce character limits and remaining characters to screen readers
- **Error messages**: Provide clear, specific error messages for validation failures
- **Focus management**: Ensure proper focus handling and visual focus indicators

### UX Guidelines
- **Appropriate sizing**: Size textareas appropriately for expected content length
- **Resize behavior**: Enable resizing for long-form content, disable for short inputs
- **Character counting**: Display character counts for fields with limits
- **Placeholder guidance**: Use helpful placeholder text that doesn't replace labels

### Form Design
- **Validation timing**: Validate on blur or form submission for better user experience
- **Progressive validation**: Show character warnings before hitting limits
- **Auto-save**: Consider auto-saving for long-form content to prevent data loss
- **Clear actions**: Provide clear actions for submitting and clearing content

### Performance
- **Debounced validation**: Debounce validation for real-time character counting
- **Large content**: Consider virtual scrolling for very large text content
- **Auto-expanding**: Implement smooth auto-expansion for dynamic height adjustments

## Accessibility Notes

The SafTextArea component provides comprehensive accessibility support:

- **ARIA compliance**: Full implementation of ARIA textbox role and properties
- **Screen reader support**: Proper announcements for content, limits, and validation
- **Keyboard navigation**: Standard textarea keyboard interactions
- **Focus management**: Clear focus indicators and logical focus behavior
- **Error handling**: Screen reader accessible validation messages

## Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile support**: iOS Safari 13+, Chrome Mobile 80+ with touch optimization
- **Resize functionality**: CSS resize property support across all modern browsers
- **Accessibility**: NVDA, JAWS, VoiceOver support

## Migration Notes

When upgrading to newer versions:

- **v2.x to v3.x**: The `value` prop is now controlled by default, requires proper state management
- **v1.x to v2.x**: `resize` prop values changed to match CSS resize property values
- **Deprecated props**: `defaultValue` replaced with `value` and proper state management

---

*This documentation provides comprehensive guidance for implementing SafTextArea in both React and Angular applications with proper accessibility, validation, and user experience considerations.*
