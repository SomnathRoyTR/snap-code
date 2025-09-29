# SafTextarea Component

## Overview

SafTextarea is a multi-line text input component designed for longer text content such as comments, descriptions, messages, and formatted text entry. It provides advanced features including auto-resizing, character counting, formatting assistance, validation, and accessibility support. SafTextarea is optimized for various use cases from simple comments to complex text editing with rich formatting capabilities.

## React API

### SafTextarea

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `value` | `string` | No | `''` | Current textarea value |
| `defaultValue` | `string` | No | `''` | Default value for uncontrolled usage |
| `placeholder` | `string` | No | - | Placeholder text when textarea is empty |
| `label` | `string \| ReactNode` | No | - | Label text for the textarea |
| `description` | `string \| ReactNode` | No | - | Additional descriptive text |
| `helperText` | `string \| ReactNode` | No | - | Helper text below the textarea |
| `error` | `string \| boolean` | No | `false` | Error state and message |
| `success` | `string \| boolean` | No | `false` | Success state and message |
| `warning` | `string \| boolean` | No | `false` | Warning state and message |
| `required` | `boolean` | No | `false` | Whether the textarea is required |
| `disabled` | `boolean` | No | `false` | Whether the textarea is disabled |
| `readOnly` | `boolean` | No | `false` | Whether the textarea is read-only |
| `autoComplete` | `string` | No | - | Autocomplete attribute value |
| `autoFocus` | `boolean` | No | `false` | Whether to auto-focus the textarea |
| `size` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the textarea |
| `variant` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `fullWidth` | `boolean` | No | `false` | Whether textarea takes full container width |
| `rows` | `number` | No | `3` | Initial number of visible rows |
| `minRows` | `number` | No | - | Minimum number of rows |
| `maxRows` | `number` | No | - | Maximum number of rows for auto-resize |
| `maxLength` | `number` | No | - | Maximum number of characters |
| `minLength` | `number` | No | - | Minimum number of characters |
| `autoResize` | `boolean` | No | `false` | Whether to auto-resize based on content |
| `resizable` | `'none' \| 'vertical' \| 'horizontal' \| 'both'` | No | `'vertical'` | Resize behavior |
| `showCharacterCount` | `boolean` | No | `false` | Whether to show character counter |
| `showWordCount` | `boolean` | No | `false` | Whether to show word counter |
| `showLineCount` | `boolean` | No | `false` | Whether to show line counter |
| `spellCheck` | `boolean` | No | `true` | Whether to enable spell checking |
| `wrap` | `'soft' \| 'hard' \| 'off'` | No | `'soft'` | Text wrapping behavior |
| `debounceMs` | `number` | No | `0` | Debounce delay for onChange callback |
| `validateOnChange` | `boolean` | No | `true` | Whether to validate on each change |
| `validateOnBlur` | `boolean` | No | `true` | Whether to validate on blur |
| `formatOnBlur` | `boolean` | No | `false` | Whether to format content on blur |
| `selectOnFocus` | `boolean` | No | `false` | Whether to select all text on focus |
| `enableFormatting` | `boolean` | No | `false` | Whether to enable text formatting tools |
| `formatButtons` | `FormatButton[]` | No | - | Custom formatting buttons |
| `onChange` | `(value: string, event: ChangeEvent) => void` | No | - | Callback when textarea value changes |
| `onBlur` | `(event: FocusEvent) => void` | No | - | Callback when textarea loses focus |
| `onFocus` | `(event: FocusEvent) => void` | No | - | Callback when textarea gains focus |
| `onKeyDown` | `(event: KeyboardEvent) => void` | No | - | Callback for key down events |
| `onResize` | `(height: number) => void` | No | - | Callback when textarea is resized |
| `validate` | `(value: string) => string \| null` | No | - | Custom validation function |
| `format` | `(value: string) => string` | No | - | Custom formatting function |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

## Angular API

### saf-textarea

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[value]` | `string` | No | `''` | Current textarea value |
| `[placeholder]` | `string` | No | - | Placeholder text when textarea is empty |
| `[label]` | `string \| TemplateRef` | No | - | Label text for the textarea |
| `[description]` | `string \| TemplateRef` | No | - | Additional descriptive text |
| `[helperText]` | `string \| TemplateRef` | No | - | Helper text below the textarea |
| `[error]` | `string \| boolean` | No | `false` | Error state and message |
| `[success]` | `string \| boolean` | No | `false` | Success state and message |
| `[warning]` | `string \| boolean` | No | `false` | Warning state and message |
| `[required]` | `boolean` | No | `false` | Whether the textarea is required |
| `[disabled]` | `boolean` | No | `false` | Whether the textarea is disabled |
| `[readonly]` | `boolean` | No | `false` | Whether the textarea is read-only |
| `[autoComplete]` | `string` | No | - | Autocomplete attribute value |
| `[size]` | `'small' \| 'medium' \| 'large'` | No | `'medium'` | Size variant of the textarea |
| `[variant]` | `'outlined' \| 'filled' \| 'standard'` | No | `'outlined'` | Visual style variant |
| `[fullWidth]` | `boolean` | No | `false` | Whether textarea takes full container width |
| `[rows]` | `number` | No | `3` | Initial number of visible rows |
| `[minRows]` | `number` | No | - | Minimum number of rows |
| `[maxRows]` | `number` | No | - | Maximum number of rows for auto-resize |
| `[maxLength]` | `number` | No | - | Maximum number of characters |
| `[minLength]` | `number` | No | - | Minimum number of characters |
| `[autoResize]` | `boolean` | No | `false` | Whether to auto-resize based on content |
| `[resizable]` | `'none' \| 'vertical' \| 'horizontal' \| 'both'` | No | `'vertical'` | Resize behavior |
| `[showCharacterCount]` | `boolean` | No | `false` | Whether to show character counter |
| `[showWordCount]` | `boolean` | No | `false` | Whether to show word counter |
| `[showLineCount]` | `boolean` | No | `false` | Whether to show line counter |
| `[spellCheck]` | `boolean` | No | `true` | Whether to enable spell checking |
| `[wrap]` | `'soft' \| 'hard' \| 'off'` | No | `'soft'` | Text wrapping behavior |
| `[debounceMs]` | `number` | No | `0` | Debounce delay for valueChange event |
| `[validateOnChange]` | `boolean` | No | `true` | Whether to validate on each change |
| `[validateOnBlur]` | `boolean` | No | `true` | Whether to validate on blur |
| `[selectOnFocus]` | `boolean` | No | `false` | Whether to select all text on focus |
| `[enableFormatting]` | `boolean` | No | `false` | Whether to enable text formatting tools |
| `(valueChange)` | `EventEmitter<string>` | No | - | Event when textarea value changes |
| `(blur)` | `EventEmitter<FocusEvent>` | No | - | Event when textarea loses focus |
| `(focus)` | `EventEmitter<FocusEvent>` | No | - | Event when textarea gains focus |
| `(keydown)` | `EventEmitter<KeyboardEvent>` | No | - | Event for key down events |
| `(resize)` | `EventEmitter<number>` | No | - | Event when textarea is resized |

## Usage Examples

### Basic Textarea Examples

#### React
```jsx
import { SafTextarea, SafCard, SafButton, SafIcon } from '@saffron/react';
import { useState } from 'react';

const BasicTextareaExample = () => {
  const [feedback, setFeedback] = useState('');
  const [description, setDescription] = useState('');
  const [comments, setComments] = useState('');
  const [notes, setNotes] = useState('');

  const handleSubmit = () => {
    console.log('Form submitted:', {
      feedback,
      description,
      comments,
      notes
    });
  };

  return (
    <SafCard className="textarea-demo">
      <SafCard.Header>
        <h2>Feedback Form</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="form-section">
          <SafTextarea
            label="General Feedback"
            placeholder="Share your thoughts about our service..."
            value={feedback}
            onChange={setFeedback}
            required={true}
            rows={4}
            maxLength={500}
            showCharacterCount={true}
            helperText="Please provide detailed feedback to help us improve"
          />

          <SafTextarea
            label="Product Description"
            placeholder="Describe the product features and benefits..."
            value={description}
            onChange={setDescription}
            rows={6}
            autoResize={true}
            maxRows={10}
            showWordCount={true}
            spellCheck={true}
            variant="filled"
          />

          <SafTextarea
            label="Additional Comments (Optional)"
            placeholder="Any additional information you'd like to share..."
            value={comments}
            onChange={setComments}
            rows={3}
            minRows={2}
            maxRows={8}
            autoResize={true}
            resizable="vertical"
            size="small"
          />

          <SafTextarea
            label="Internal Notes"
            placeholder="These notes are for internal use only..."
            value={notes}
            onChange={setNotes}
            rows={3}
            variant="standard"
            helperText="Internal notes won't be visible to customers"
            showLineCount={true}
          />

          <SafButton 
            variant="primary" 
            onClick={handleSubmit}
            disabled={!feedback.trim()}
          >
            Submit Feedback
          </SafButton>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// basic-textarea.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-textarea',
  template: `
    <saf-card class="textarea-demo">
      <saf-card-header>
        <h2>Feedback Form</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="form-section">
          <saf-textarea
            label="General Feedback"
            placeholder="Share your thoughts about our service..."
            [value]="feedback"
            (valueChange)="feedback = $event"
            [required]="true"
            [rows]="4"
            [maxLength]="500"
            [showCharacterCount]="true"
            helperText="Please provide detailed feedback to help us improve">
          </saf-textarea>

          <saf-textarea
            label="Product Description"
            placeholder="Describe the product features and benefits..."
            [value]="description"
            (valueChange)="description = $event"
            [rows]="6"
            [autoResize]="true"
            [maxRows]="10"
            [showWordCount]="true"
            [spellCheck]="true"
            variant="filled">
          </saf-textarea>

          <saf-textarea
            label="Additional Comments (Optional)"
            placeholder="Any additional information you'd like to share..."
            [value]="comments"
            (valueChange)="comments = $event"
            [rows]="3"
            [minRows]="2"
            [maxRows]="8"
            [autoResize]="true"
            resizable="vertical"
            size="small">
          </saf-textarea>

          <saf-textarea
            label="Internal Notes"
            placeholder="These notes are for internal use only..."
            [value]="notes"
            (valueChange)="notes = $event"
            [rows]="3"
            variant="standard"
            helperText="Internal notes won't be visible to customers"
            [showLineCount]="true">
          </saf-textarea>

          <saf-button 
            variant="primary" 
            (click)="handleSubmit()"
            [disabled]="!feedback.trim()">
            Submit Feedback
          </saf-button>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class BasicTextareaComponent {
  feedback = '';
  description = '';
  comments = '';
  notes = '';

  handleSubmit() {
    console.log('Form submitted:', {
      feedback: this.feedback,
      description: this.description,
      comments: this.comments,
      notes: this.notes
    });
  }
}
```

### Advanced Textarea with Validation and Formatting

#### React
```jsx
import { SafTextarea, SafCard, SafButton, SafIcon, SafBadge } from '@saffron/react';
import { useState } from 'react';

const AdvancedTextareaExample = () => {
  const [formData, setFormData] = useState({
    message: '',
    review: '',
    bio: '',
    code: ''
  });

  const [errors, setErrors] = useState({});
  const [touched, setTouched] = useState({});

  const validateMessage = (value) => {
    if (!value.trim()) return 'Message is required';
    if (value.length < 10) return 'Message must be at least 10 characters';
    if (value.length > 1000) return 'Message must not exceed 1000 characters';
    return null;
  };

  const validateReview = (value) => {
    if (!value.trim()) return 'Review is required';
    const wordCount = value.trim().split(/\s+/).length;
    if (wordCount < 5) return 'Review must be at least 5 words';
    if (wordCount > 200) return 'Review must not exceed 200 words';
    return null;
  };

  const validateBio = (value) => {
    if (value && value.length > 500) return 'Bio must not exceed 500 characters';
    return null;
  };

  const validateCode = (value) => {
    if (!value.trim()) return 'Code snippet is required';
    try {
      // Basic syntax validation for JSON/JavaScript
      if (value.includes('{') || value.includes('[')) {
        JSON.parse(value);
      }
    } catch {
      return 'Invalid JSON/JavaScript syntax';
    }
    return null;
  };

  const handleInputChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }));

    // Validate field
    let error = null;
    switch (field) {
      case 'message': error = validateMessage(value); break;
      case 'review': error = validateReview(value); break;
      case 'bio': error = validateBio(value); break;
      case 'code': error = validateCode(value); break;
    }

    setErrors(prev => ({
      ...prev,
      [field]: error
    }));
  };

  const handleBlur = (field) => {
    setTouched(prev => ({
      ...prev,
      [field]: true
    }));
  };

  const formatCode = (value) => {
    try {
      if (value.includes('{') || value.includes('[')) {
        return JSON.stringify(JSON.parse(value), null, 2);
      }
    } catch {
      // Return original if formatting fails
    }
    return value;
  };

  const getWordCount = (text) => {
    return text.trim() ? text.trim().split(/\s+/).length : 0;
  };

  const getReadingTime = (text) => {
    const wordCount = getWordCount(text);
    const wordsPerMinute = 200;
    const minutes = Math.ceil(wordCount / wordsPerMinute);
    return minutes;
  };

  const getMessageTone = (text) => {
    const positiveWords = ['great', 'excellent', 'amazing', 'love', 'wonderful', 'fantastic'];
    const negativeWords = ['bad', 'terrible', 'awful', 'hate', 'horrible', 'worst'];
    
    const words = text.toLowerCase().split(/\s+/);
    const positiveCount = words.filter(word => positiveWords.includes(word)).length;
    const negativeCount = words.filter(word => negativeWords.includes(word)).length;
    
    if (positiveCount > negativeCount) return { tone: 'Positive', color: 'success' };
    if (negativeCount > positiveCount) return { tone: 'Critical', color: 'error' };
    return { tone: 'Neutral', color: 'primary' };
  };

  const messageTone = getMessageTone(formData.message);

  return (
    <SafCard className="advanced-textarea-demo">
      <SafCard.Header>
        <h2>Content Submission Form</h2>
      </SafCard.Header>
      <SafCard.Content>
        <div className="form-sections">
          <div className="form-section">
            <SafTextarea
              label="Message"
              placeholder="Write your message here..."
              value={formData.message}
              onChange={(value) => handleInputChange('message', value)}
              onBlur={() => handleBlur('message')}
              error={touched.message ? errors.message : false}
              required={true}
              rows={5}
              minRows={3}
              maxRows={10}
              autoResize={true}
              maxLength={1000}
              showCharacterCount={true}
              debounceMs={300}
              helperText={
                <div className="message-stats">
                  <span>Words: {getWordCount(formData.message)}</span>
                  <span>Reading time: ~{getReadingTime(formData.message)} min</span>
                  <SafBadge variant={messageTone.color} size="small">
                    {messageTone.tone}
                  </SafBadge>
                </div>
              }
            />
          </div>

          <div className="form-section">
            <SafTextarea
              label="Product Review"
              placeholder="Share your detailed review of the product..."
              value={formData.review}
              onChange={(value) => handleInputChange('review', value)}
              onBlur={() => handleBlur('review')}
              error={touched.review ? errors.review : false}
              success={
                formData.review && !errors.review && getWordCount(formData.review) >= 10
                  ? 'Great review length!'
                  : false
              }
              required={true}
              rows={6}
              autoResize={true}
              showWordCount={true}
              spellCheck={true}
              helperText={`${getWordCount(formData.review)}/200 words (5 word minimum)`}
            />
          </div>

          <div className="form-section">
            <SafTextarea
              label="Personal Bio (Optional)"
              placeholder="Tell us about yourself..."
              value={formData.bio}
              onChange={(value) => handleInputChange('bio', value)}
              onBlur={() => handleBlur('bio')}
              error={touched.bio ? errors.bio : false}
              rows={4}
              maxLength={500}
              showCharacterCount={true}
              selectOnFocus={true}
              variant="filled"
              helperText="This will be displayed on your public profile"
            />
          </div>

          <div className="form-section">
            <SafTextarea
              label="Code Snippet"
              placeholder='{"example": "JSON or JavaScript code"}'
              value={formData.code}
              onChange={(value) => handleInputChange('code', value)}
              onBlur={() => handleBlur('code')}
              error={touched.code ? errors.code : false}
              required={true}
              rows={8}
              maxRows={15}
              autoResize={true}
              formatOnBlur={true}
              format={formatCode}
              spellCheck={false}
              wrap="off"
              variant="standard"
              helperText="JSON will be auto-formatted on blur"
              className="code-textarea"
            />
          </div>

          <div className="form-actions">
            <SafButton variant="outline" onClick={() => {
              setFormData({ message: '', review: '', bio: '', code: '' });
              setErrors({});
              setTouched({});
            }}>
              Clear All
            </SafButton>
            <SafButton 
              variant="primary"
              disabled={Object.values(errors).some(error => error) || !formData.message || !formData.review || !formData.code}
            >
              Submit Content
            </SafButton>
          </div>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// advanced-textarea.component.ts
import { Component } from '@angular/core';

interface FormData {
  message: string;
  review: string;
  bio: string;
  code: string;
}

@Component({
  selector: 'app-advanced-textarea',
  template: `
    <saf-card class="advanced-textarea-demo">
      <saf-card-header>
        <h2>Content Submission Form</h2>
      </saf-card-header>
      <saf-card-content>
        <div class="form-sections">
          <div class="form-section">
            <saf-textarea
              label="Message"
              placeholder="Write your message here..."
              [value]="formData.message"
              (valueChange)="handleInputChange('message', $event)"
              (blur)="handleBlur('message')"
              [error]="getFieldError('message')"
              [required]="true"
              [rows]="5"
              [minRows]="3"
              [maxRows]="10"
              [autoResize]="true"
              [maxLength]="1000"
              [showCharacterCount]="true"
              [debounceMs]="300">
              <div slot="helper-text" class="message-stats">
                <span>Words: {{ getWordCount(formData.message) }}</span>
                <span>Reading time: ~{{ getReadingTime(formData.message) }} min</span>
                <saf-badge 
                  [variant]="messageTone.color" 
                  size="small">
                  {{ messageTone.tone }}
                </saf-badge>
              </div>
            </saf-textarea>
          </div>

          <div class="form-section">
            <saf-textarea
              label="Product Review"
              placeholder="Share your detailed review of the product..."
              [value]="formData.review"
              (valueChange)="handleInputChange('review', $event)"
              (blur)="handleBlur('review')"
              [error]="getFieldError('review')"
              [success]="getFieldSuccess('review')"
              [required]="true"
              [rows]="6"
              [autoResize]="true"
              [showWordCount]="true"
              [spellCheck]="true"
              [helperText]="getWordCount(formData.review) + '/200 words (5 word minimum)'">
            </saf-textarea>
          </div>

          <div class="form-section">
            <saf-textarea
              label="Personal Bio (Optional)"
              placeholder="Tell us about yourself..."
              [value]="formData.bio"
              (valueChange)="handleInputChange('bio', $event)"
              (blur)="handleBlur('bio')"
              [error]="getFieldError('bio')"
              [rows]="4"
              [maxLength]="500"
              [showCharacterCount]="true"
              [selectOnFocus]="true"
              variant="filled"
              helperText="This will be displayed on your public profile">
            </saf-textarea>
          </div>

          <div class="form-section">
            <saf-textarea
              label="Code Snippet"
              placeholder='{"example": "JSON or JavaScript code"}'
              [value]="formData.code"
              (valueChange)="handleInputChange('code', $event)"
              (blur)="handleBlur('code')"
              [error]="getFieldError('code')"
              [required]="true"
              [rows]="8"
              [maxRows]="15"
              [autoResize]="true"
              [spellCheck]="false"
              wrap="off"
              variant="standard"
              helperText="JSON will be auto-formatted on blur"
              class="code-textarea">
            </saf-textarea>
          </div>

          <div class="form-actions">
            <saf-button variant="outline" (click)="clearAll()">
              Clear All
            </saf-button>
            <saf-button 
              variant="primary"
              [disabled]="hasErrors() || !isFormValid()">
              Submit Content
            </saf-button>
          </div>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class AdvancedTextareaComponent {
  formData: FormData = {
    message: '',
    review: '',
    bio: '',
    code: ''
  };

  errors: { [key: string]: string } = {};
  touched: { [key: string]: boolean } = {};

  handleInputChange(field: keyof FormData, value: string) {
    this.formData = {
      ...this.formData,
      [field]: value
    };

    // Validate field
    let error = '';
    switch (field) {
      case 'message': error = this.validateMessage(value); break;
      case 'review': error = this.validateReview(value); break;
      case 'bio': error = this.validateBio(value); break;
      case 'code': error = this.validateCode(value); break;
    }

    this.errors[field] = error;
  }

  handleBlur(field: string) {
    this.touched[field] = true;
  }

  validateMessage(value: string): string {
    if (!value.trim()) return 'Message is required';
    if (value.length < 10) return 'Message must be at least 10 characters';
    if (value.length > 1000) return 'Message must not exceed 1000 characters';
    return '';
  }

  validateReview(value: string): string {
    if (!value.trim()) return 'Review is required';
    const wordCount = this.getWordCount(value);
    if (wordCount < 5) return 'Review must be at least 5 words';
    if (wordCount > 200) return 'Review must not exceed 200 words';
    return '';
  }

  validateBio(value: string): string {
    if (value && value.length > 500) return 'Bio must not exceed 500 characters';
    return '';
  }

  validateCode(value: string): string {
    if (!value.trim()) return 'Code snippet is required';
    try {
      if (value.includes('{') || value.includes('[')) {
        JSON.parse(value);
      }
    } catch {
      return 'Invalid JSON/JavaScript syntax';
    }
    return '';
  }

  getFieldError(field: string): string | boolean {
    return this.touched[field] ? this.errors[field] || false : false;
  }

  getFieldSuccess(field: string): string | boolean {
    if (field === 'review') {
      return this.formData.review && !this.errors.review && this.getWordCount(this.formData.review) >= 10
        ? 'Great review length!'
        : false;
    }
    return false;
  }

  getWordCount(text: string): number {
    return text.trim() ? text.trim().split(/\s+/).length : 0;
  }

  getReadingTime(text: string): number {
    const wordCount = this.getWordCount(text);
    const wordsPerMinute = 200;
    return Math.ceil(wordCount / wordsPerMinute);
  }

  get messageTone() {
    const text = this.formData.message;
    const positiveWords = ['great', 'excellent', 'amazing', 'love', 'wonderful', 'fantastic'];
    const negativeWords = ['bad', 'terrible', 'awful', 'hate', 'horrible', 'worst'];
    
    const words = text.toLowerCase().split(/\s+/);
    const positiveCount = words.filter(word => positiveWords.includes(word)).length;
    const negativeCount = words.filter(word => negativeWords.includes(word)).length;
    
    if (positiveCount > negativeCount) return { tone: 'Positive', color: 'success' };
    if (negativeCount > positiveCount) return { tone: 'Critical', color: 'error' };
    return { tone: 'Neutral', color: 'primary' };
  }

  clearAll() {
    this.formData = { message: '', review: '', bio: '', code: '' };
    this.errors = {};
    this.touched = {};
  }

  hasErrors(): boolean {
    return Object.values(this.errors).some(error => error);
  }

  isFormValid(): boolean {
    return !!(this.formData.message && this.formData.review && this.formData.code);
  }
}
```

### Rich Text Editor with Formatting Tools

#### React
```jsx
import { SafTextarea, SafCard, SafButton, SafIcon, SafButtonGroup } from '@saffron/react';
import { useState, useRef } from 'react';

const RichTextEditorExample = () => {
  const [content, setContent] = useState('');
  const [formatState, setFormatState] = useState({
    bold: false,
    italic: false,
    underline: false
  });
  const textareaRef = useRef(null);

  const formatButtons = [
    { name: 'bold', icon: 'bold', label: 'Bold (Ctrl+B)' },
    { name: 'italic', icon: 'italic', label: 'Italic (Ctrl+I)' },
    { name: 'underline', icon: 'underline', label: 'Underline (Ctrl+U)' },
    { name: 'link', icon: 'link', label: 'Insert Link' },
    { name: 'list', icon: 'list', label: 'Bullet List' },
    { name: 'numbered-list', icon: 'numbered-list', label: 'Numbered List' },
    { name: 'quote', icon: 'quote', label: 'Quote' },
    { name: 'code', icon: 'code', label: 'Code Block' }
  ];

  const insertText = (before, after = '') => {
    const textarea = textareaRef.current;
    if (!textarea) return;

    const start = textarea.selectionStart;
    const end = textarea.selectionEnd;
    const selectedText = content.substring(start, end);
    
    const newText = content.substring(0, start) + 
                   before + selectedText + after + 
                   content.substring(end);
    
    setContent(newText);
    
    // Restore cursor position
    setTimeout(() => {
      textarea.focus();
      textarea.setSelectionRange(
        start + before.length,
        start + before.length + selectedText.length
      );
    }, 0);
  };

  const handleFormat = (format) => {
    switch (format) {
      case 'bold':
        insertText('**', '**');
        break;
      case 'italic':
        insertText('*', '*');
        break;
      case 'underline':
        insertText('_', '_');
        break;
      case 'link':
        insertText('[', '](url)');
        break;
      case 'list':
        insertText('- ');
        break;
      case 'numbered-list':
        insertText('1. ');
        break;
      case 'quote':
        insertText('> ');
        break;
      case 'code':
        insertText('```\n', '\n```');
        break;
    }
  };

  const handleKeyDown = (event) => {
    // Handle keyboard shortcuts
    if (event.ctrlKey || event.metaKey) {
      switch (event.key) {
        case 'b':
          event.preventDefault();
          handleFormat('bold');
          break;
        case 'i':
          event.preventDefault();
          handleFormat('italic');
          break;
        case 'u':
          event.preventDefault();
          handleFormat('underline');
          break;
      }
    }

    // Handle Tab for indentation
    if (event.key === 'Tab') {
      event.preventDefault();
      insertText('  ');
    }
  };

  const getPreview = () => {
    return content
      .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
      .replace(/\*(.*?)\*/g, '<em>$1</em>')
      .replace(/_(.*?)_/g, '<u>$1</u>')
      .replace(/\[(.*?)\]\((.*?)\)/g, '<a href="$2">$1</a>')
      .replace(/^- (.+)/gm, '<li>$1</li>')
      .replace(/^> (.+)/gm, '<blockquote>$1</blockquote>')
      .replace(/```([\s\S]*?)```/g, '<pre><code>$1</code></pre>')
      .replace(/\n/g, '<br>');
  };

  const [showPreview, setShowPreview] = useState(false);

  return (
    <SafCard className="rich-editor-demo">
      <SafCard.Header>
        <h2>Rich Text Editor</h2>
        <SafButtonGroup size="small">
          <SafButton 
            variant={!showPreview ? 'primary' : 'outline'}
            onClick={() => setShowPreview(false)}
          >
            Edit
          </SafButton>
          <SafButton 
            variant={showPreview ? 'primary' : 'outline'}
            onClick={() => setShowPreview(true)}
          >
            Preview
          </SafButton>
        </SafButtonGroup>
      </SafCard.Header>
      <SafCard.Content>
        {!showPreview ? (
          <div className="editor-container">
            <div className="formatting-toolbar">
              {formatButtons.map(button => (
                <SafButton
                  key={button.name}
                  variant="ghost"
                  size="small"
                  onClick={() => handleFormat(button.name)}
                  title={button.label}
                  className={formatState[button.name] ? 'active' : ''}
                >
                  <SafIcon name={button.icon} />
                </SafButton>
              ))}
            </div>

            <SafTextarea
              ref={textareaRef}
              placeholder="Start writing your content... Use Markdown formatting or the toolbar above."
              value={content}
              onChange={setContent}
              onKeyDown={handleKeyDown}
              rows={15}
              autoResize={true}
              maxRows={25}
              showCharacterCount={true}
              showWordCount={true}
              spellCheck={true}
              variant="outlined"
              className="rich-textarea"
              helperText="Supports Markdown formatting. Use Ctrl+B, Ctrl+I, Ctrl+U for quick formatting."
            />

            <div className="editor-stats">
              <span>Characters: {content.length}</span>
              <span>Words: {content.trim() ? content.trim().split(/\s+/).length : 0}</span>
              <span>Lines: {content.split('\n').length}</span>
            </div>
          </div>
        ) : (
          <div className="preview-container">
            <div className="preview-content" 
                 dangerouslySetInnerHTML={{ __html: getPreview() }} />
            {!content && (
              <div className="empty-preview">
                <SafIcon name="eye" size="large" />
                <p>Nothing to preview yet. Switch to Edit mode to start writing.</p>
              </div>
            )}
          </div>
        )}

        <div className="editor-actions">
          <SafButton variant="outline" onClick={() => setContent('')}>
            Clear Content
          </SafButton>
          <SafButton 
            variant="primary"
            disabled={!content.trim()}
          >
            Save Document
          </SafButton>
        </div>
      </SafCard.Content>
    </SafCard>
  );
};
```

#### Angular
```typescript
// rich-text-editor.component.ts
import { Component, ViewChild, ElementRef } from '@angular/core';

interface FormatButton {
  name: string;
  icon: string;
  label: string;
}

@Component({
  selector: 'app-rich-text-editor',
  template: `
    <saf-card class="rich-editor-demo">
      <saf-card-header>
        <h2>Rich Text Editor</h2>
        <saf-button-group size="small">
          <saf-button 
            [variant]="!showPreview ? 'primary' : 'outline'"
            (click)="showPreview = false">
            Edit
          </saf-button>
          <saf-button 
            [variant]="showPreview ? 'primary' : 'outline'"
            (click)="showPreview = true">
            Preview
          </saf-button>
        </saf-button-group>
      </saf-card-header>
      <saf-card-content>
        <div *ngIf="!showPreview" class="editor-container">
          <div class="formatting-toolbar">
            <saf-button
              *ngFor="let button of formatButtons"
              variant="ghost"
              size="small"
              (click)="handleFormat(button.name)"
              [title]="button.label"
              [class.active]="formatState[button.name]">
              <saf-icon [name]="button.icon"></saf-icon>
            </saf-button>
          </div>

          <saf-textarea
            #textareaRef
            placeholder="Start writing your content... Use Markdown formatting or the toolbar above."
            [value]="content"
            (valueChange)="content = $event"
            (keydown)="handleKeyDown($event)"
            [rows]="15"
            [autoResize]="true"
            [maxRows]="25"
            [showCharacterCount]="true"
            [showWordCount]="true"
            [spellCheck]="true"
            variant="outlined"
            class="rich-textarea"
            helperText="Supports Markdown formatting. Use Ctrl+B, Ctrl+I, Ctrl+U for quick formatting.">
          </saf-textarea>

          <div class="editor-stats">
            <span>Characters: {{ content.length }}</span>
            <span>Words: {{ getWordCount() }}</span>
            <span>Lines: {{ content.split('\\n').length }}</span>
          </div>
        </div>

        <div *ngIf="showPreview" class="preview-container">
          <div 
            class="preview-content" 
            [innerHTML]="getPreview()">
          </div>
          <div 
            *ngIf="!content" 
            class="empty-preview">
            <saf-icon name="eye" size="large"></saf-icon>
            <p>Nothing to preview yet. Switch to Edit mode to start writing.</p>
          </div>
        </div>

        <div class="editor-actions">
          <saf-button variant="outline" (click)="content = ''">
            Clear Content
          </saf-button>
          <saf-button 
            variant="primary"
            [disabled]="!content.trim()">
            Save Document
          </saf-button>
        </div>
      </saf-card-content>
    </saf-card>
  `
})
export class RichTextEditorComponent {
  @ViewChild('textareaRef') textareaRef!: ElementRef<HTMLTextAreaElement>;

  content = '';
  showPreview = false;
  formatState = {
    bold: false,
    italic: false,
    underline: false
  };

  formatButtons: FormatButton[] = [
    { name: 'bold', icon: 'bold', label: 'Bold (Ctrl+B)' },
    { name: 'italic', icon: 'italic', label: 'Italic (Ctrl+I)' },
    { name: 'underline', icon: 'underline', label: 'Underline (Ctrl+U)' },
    { name: 'link', icon: 'link', label: 'Insert Link' },
    { name: 'list', icon: 'list', label: 'Bullet List' },
    { name: 'numbered-list', icon: 'numbered-list', label: 'Numbered List' },
    { name: 'quote', icon: 'quote', label: 'Quote' },
    { name: 'code', icon: 'code', label: 'Code Block' }
  ];

  insertText(before: string, after: string = '') {
    const textarea = this.textareaRef?.nativeElement;
    if (!textarea) return;

    const start = textarea.selectionStart;
    const end = textarea.selectionEnd;
    const selectedText = this.content.substring(start, end);
    
    this.content = this.content.substring(0, start) + 
                   before + selectedText + after + 
                   this.content.substring(end);
    
    // Restore cursor position
    setTimeout(() => {
      textarea.focus();
      textarea.setSelectionRange(
        start + before.length,
        start + before.length + selectedText.length
      );
    }, 0);
  }

  handleFormat(format: string) {
    switch (format) {
      case 'bold':
        this.insertText('**', '**');
        break;
      case 'italic':
        this.insertText('*', '*');
        break;
      case 'underline':
        this.insertText('_', '_');
        break;
      case 'link':
        this.insertText('[', '](url)');
        break;
      case 'list':
        this.insertText('- ');
        break;
      case 'numbered-list':
        this.insertText('1. ');
        break;
      case 'quote':
        this.insertText('> ');
        break;
      case 'code':
        this.insertText('```\n', '\n```');
        break;
    }
  }

  handleKeyDown(event: KeyboardEvent) {
    // Handle keyboard shortcuts
    if (event.ctrlKey || event.metaKey) {
      switch (event.key) {
        case 'b':
          event.preventDefault();
          this.handleFormat('bold');
          break;
        case 'i':
          event.preventDefault();
          this.handleFormat('italic');
          break;
        case 'u':
          event.preventDefault();
          this.handleFormat('underline');
          break;
      }
    }

    // Handle Tab for indentation
    if (event.key === 'Tab') {
      event.preventDefault();
      this.insertText('  ');
    }
  }

  getPreview(): string {
    return this.content
      .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
      .replace(/\*(.*?)\*/g, '<em>$1</em>')
      .replace(/_(.*?)_/g, '<u>$1</u>')
      .replace(/\[(.*?)\]\((.*?)\)/g, '<a href="$2">$1</a>')
      .replace(/^- (.+)/gm, '<li>$1</li>')
      .replace(/^> (.+)/gm, '<blockquote>$1</blockquote>')
      .replace(/```([\s\S]*?)```/g, '<pre><code>$1</code></pre>')
      .replace(/\n/g, '<br>');
  }

  getWordCount(): number {
    return this.content.trim() ? this.content.trim().split(/\s+/).length : 0;
  }
}
```

## Best Practices

1. **Auto-Resize and Sizing**
   - Use auto-resize for dynamic content that varies in length
   - Set appropriate minimum and maximum row limits
   - Consider the user's viewport and container constraints

2. **Validation and Feedback**
   - Implement real-time validation for immediate user feedback
   - Provide character, word, and line counters when relevant
   - Use clear, actionable error messages

3. **Content Formatting**
   - Enable spell checking for user-generated content
   - Provide formatting assistance for structured content
   - Support keyboard shortcuts for common formatting actions

4. **Performance Optimization**
   - Use debouncing for expensive validation or processing
   - Optimize auto-resize calculations for large content
   - Implement efficient text analysis and preview generation

5. **User Experience**
   - Provide clear labels and helpful placeholder text
   - Support keyboard navigation and shortcuts
   - Offer formatting tools and content assistance when appropriate

## Accessibility Considerations

1. **ARIA Support**
   - Use proper ARIA labels and descriptions
   - Announce character and word count updates to screen readers
   - Provide meaningful error and validation announcements

2. **Keyboard Navigation**
   - Support Tab navigation and focus management
   - Implement keyboard shortcuts for formatting actions
   - Ensure proper focus indicators for all interactive elements

3. **Screen Reader Compatibility**
   - Announce validation errors and success messages
   - Provide meaningful labels for formatting tools
   - Support text selection and navigation

4. **Visual Accessibility**
   - Ensure sufficient color contrast for all states
   - Provide clear visual indicators for active formatting
   - Support high contrast and reduced motion preferences

## Related Components

- **SafTextInput**: Single-line text input alternative
- **SafSelect**: Dropdown selection for predefined options
- **SafRichTextEditor**: Advanced editor with rich formatting
- **SafLabel**: Standalone labels for custom layouts
- **SafButton**: Form submission and formatting actions

## Notes

- Textarea automatically handles text wrapping and line breaks
- Custom CSS variables available for comprehensive theming
- Built-in support for content analysis and formatting assistance
- Optimized for mobile touch interactions and responsive design
- Compatible with popular rich text editing libraries
- Supports both controlled and uncontrolled usage patterns
- Performance optimized with efficient auto-resize and content processing
