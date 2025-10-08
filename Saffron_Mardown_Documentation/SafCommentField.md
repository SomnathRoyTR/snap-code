# SafCommentField

A container component designed for creating comment input forms with integrated layout support for avatars, text areas, and action buttons. SafCommentField provides a structured way to build comment interfaces with consistent spacing and accessibility features.

## React

### API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `ariaLabel` | `string` | `'Post a reply'` | Accessible label for the comment region |
| `children` | `ReactNode` | - | The main content, typically a text area for comment input |

### Slots

| Slot | Description |
|------|-------------|
| `start` | Content placed at the start of the form, typically used for user avatars |
| `end` | Content placed at the end of the form, typically used for action buttons |
| `default` | Main form content, typically a text area or input field |

### Examples

#### Basic Comment Form
```jsx
import { SafCommentField, SafTextArea, SafButton, SafAvatar } from '@saffron/core-components/react';

function BasicCommentForm() {
  const [comment, setComment] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (comment.trim()) {
      console.log('Submitting comment:', comment);
      setComment(''); // Clear after submission
    }
  };

  return (
    <SafCommentField ariaLabel="Post a new comment">
      {/* User avatar in start slot */}
      <SafAvatar 
        slot="start"
        appearance="image"
        size="medium"
        imgSrc="/path/to/user-avatar.jpg"
        label="John Doe"
      />
      
      {/* Main comment input */}
      <SafTextArea
        label="Your comment"
        value={comment}
        onChange={(e) => setComment(e.target.value)}
        placeholder="Write your comment here..."
        rows={3}
      />
      
      {/* Action buttons in end slot */}
      <div slot="end" style={{ display: 'flex', gap: '8px', marginTop: '8px' }}>
        <SafButton 
          appearance="secondary" 
          onClick={() => setComment('')}
          disabled={!comment.trim()}>
          Cancel
        </SafButton>
        <SafButton 
          appearance="primary" 
          onClick={handleSubmit}
          disabled={!comment.trim()}>
          Post Comment
        </SafButton>
      </div>
    </SafCommentField>
  );
}
```

#### Reply Form with Validation
```jsx
import { SafCommentField, SafTextArea, SafButton, SafAvatar } from '@saffron/core-components/react';

function ReplyCommentForm({ parentComment, onReply, onCancel }) {
  const [reply, setReply] = useState('');
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [error, setError] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    
    if (!reply.trim()) {
      setError('Reply cannot be empty');
      return;
    }

    if (reply.length > 500) {
      setError('Reply is too long (max 500 characters)');
      return;
    }

    setIsSubmitting(true);
    setError('');

    try {
      await onReply({
        parentId: parentComment.id,
        content: reply.trim(),
        timestamp: new Date()
      });
      setReply('');
    } catch (err) {
      setError('Failed to post reply. Please try again.');
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <SafCommentField ariaLabel={`Reply to ${parentComment.author}`}>
      <SafAvatar 
        slot="start"
        appearance="initials"
        size="small"
        name="Current User"
      />
      
      <SafTextArea
        label={`Replying to ${parentComment.author}`}
        value={reply}
        onChange={(e) => setReply(e.target.value)}
        placeholder="Write your reply..."
        rows={2}
        invalid={!!error}
        validationMessage={error}
      />
      
      <div slot="end" style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginTop: '8px' }}>
        <span style={{ fontSize: '0.875rem', color: '#666' }}>
          {reply.length}/500 characters
        </span>
        
        <div style={{ display: 'flex', gap: '8px' }}>
          <SafButton 
            appearance="secondary" 
            onClick={onCancel}
            disabled={isSubmitting}>
            Cancel
          </SafButton>
          <SafButton 
            appearance="primary" 
            onClick={handleSubmit}
            disabled={!reply.trim() || reply.length > 500 || isSubmitting}>
            {isSubmitting ? 'Posting...' : 'Reply'}
          </SafButton>
        </div>
      </div>
    </SafCommentField>
  );
}
```

#### Rich Comment Form with Attachments
```jsx
import { SafCommentField, SafTextArea, SafButton, SafAvatar, SafFileUpload } from '@saffron/core-components/react';

function RichCommentForm() {
  const [comment, setComment] = useState('');
  const [attachments, setAttachments] = useState([]);
  const [showAttachments, setShowAttachments] = useState(false);

  const handleFileUpload = (files) => {
    setAttachments(prev => [...prev, ...files]);
  };

  const removeAttachment = (index) => {
    setAttachments(prev => prev.filter((_, i) => i !== index));
  };

  const handleSubmit = async () => {
    const formData = new FormData();
    formData.append('comment', comment);
    attachments.forEach((file, index) => {
      formData.append(`attachment_${index}`, file);
    });

    try {
      // Submit comment with attachments
      console.log('Submitting comment with attachments');
      setComment('');
      setAttachments([]);
      setShowAttachments(false);
    } catch (error) {
      console.error('Failed to submit comment:', error);
    }
  };

  return (
    <SafCommentField ariaLabel="Create a new comment with attachments">
      <SafAvatar 
        slot="start"
        appearance="image"
        size="medium"
        imgSrc="/current-user-avatar.jpg"
        label="Current User"
      />
      
      <div>
        <SafTextArea
          label="Your comment"
          value={comment}
          onChange={(e) => setComment(e.target.value)}
          placeholder="Share your thoughts..."
          rows={4}
        />
        
        {showAttachments && (
          <div style={{ marginTop: '12px' }}>
            <SafFileUpload
              accept="image/*,.pdf,.doc,.docx"
              multiple
              onFileSelect={handleFileUpload}
            />
            
            {attachments.length > 0 && (
              <div style={{ marginTop: '8px' }}>
                <h4>Attachments:</h4>
                <ul style={{ listStyle: 'none', padding: 0 }}>
                  {attachments.map((file, index) => (
                    <li key={index} style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', padding: '4px 0' }}>
                      <span>{file.name}</span>
                      <SafButton 
                        appearance="secondary" 
                        size="small"
                        onClick={() => removeAttachment(index)}>
                        Remove
                      </SafButton>
                    </li>
                  ))}
                </ul>
              </div>
            )}
          </div>
        )}
      </div>
      
      <div slot="end" style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginTop: '12px' }}>
        <SafButton 
          appearance="tertiary"
          onClick={() => setShowAttachments(!showAttachments)}>
          {showAttachments ? 'Hide Attachments' : 'Add Attachments'}
        </SafButton>
        
        <div style={{ display: 'flex', gap: '8px' }}>
          <SafButton 
            appearance="secondary"
            onClick={() => {
              setComment('');
              setAttachments([]);
              setShowAttachments(false);
            }}>
            Clear
          </SafButton>
          <SafButton 
            appearance="primary"
            onClick={handleSubmit}
            disabled={!comment.trim()}>
            Post Comment
          </SafButton>
        </div>
      </div>
    </SafCommentField>
  );
}
```

## Angular

### API

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `ariaLabel` | `string` | `'Post a reply'` | Accessible label for the comment region |

### Examples

#### Basic Comment Form
```html
<saf-comment-field ariaLabel="Post a new comment">
  <!-- User avatar in start slot -->
  <saf-avatar 
    slot="start"
    appearance="image"
    size="medium"
    [imgSrc]="currentUser.avatar"
    [label]="currentUser.name">
  </saf-avatar>
  
  <!-- Main comment input -->
  <saf-text-area
    label="Your comment"
    [(ngModel)]="comment"
    placeholder="Write your comment here..."
    [rows]="3">
  </saf-text-area>
  
  <!-- Action buttons in end slot -->
  <div slot="end" class="comment-actions">
    <saf-button 
      appearance="secondary" 
      (click)="clearComment()"
      [disabled]="!comment?.trim()">
      Cancel
    </saf-button>
    <saf-button 
      appearance="primary" 
      (click)="submitComment()"
      [disabled]="!comment?.trim()">
      Post Comment
    </saf-button>
  </div>
</saf-comment-field>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-basic-comment-form',
  templateUrl: './basic-comment-form.component.html',
  styleUrls: ['./basic-comment-form.component.scss']
})
export class BasicCommentFormComponent {
  comment = '';
  currentUser = {
    name: 'John Doe',
    avatar: '/path/to/user-avatar.jpg'
  };

  submitComment() {
    if (this.comment.trim()) {
      console.log('Submitting comment:', this.comment);
      this.comment = ''; // Clear after submission
    }
  }

  clearComment() {
    this.comment = '';
  }
}
```

#### Reply Form with Validation
```html
<saf-comment-field [ariaLabel]="'Reply to ' + parentComment.author">
  <saf-avatar 
    slot="start"
    appearance="initials"
    size="small"
    [name]="currentUser.name">
  </saf-avatar>
  
  <saf-text-area
    [label]="'Replying to ' + parentComment.author"
    [(ngModel)]="reply"
    placeholder="Write your reply..."
    [rows]="2"
    [invalid]="!!error"
    [validationMessage]="error">
  </saf-text-area>
  
  <div slot="end" class="reply-actions">
    <span class="character-count">{{ reply.length }}/500 characters</span>
    
    <div class="button-group">
      <saf-button 
        appearance="secondary" 
        (click)="onCancel()"
        [disabled]="isSubmitting">
        Cancel
      </saf-button>
      <saf-button 
        appearance="primary" 
        (click)="submitReply()"
        [disabled]="!reply?.trim() || reply.length > 500 || isSubmitting">
        {{ isSubmitting ? 'Posting...' : 'Reply' }}
      </saf-button>
    </div>
  </div>
</saf-comment-field>
```

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

interface Comment {
  id: string;
  author: string;
  content: string;
}

@Component({
  selector: 'app-reply-comment-form',
  templateUrl: './reply-comment-form.component.html',
  styleUrls: ['./reply-comment-form.component.scss']
})
export class ReplyCommentFormComponent {
  @Input() parentComment!: Comment;
  @Output() replySubmitted = new EventEmitter<any>();
  @Output() cancelled = new EventEmitter<void>();

  reply = '';
  isSubmitting = false;
  error = '';
  currentUser = { name: 'Current User' };

  async submitReply() {
    if (!this.reply.trim()) {
      this.error = 'Reply cannot be empty';
      return;
    }

    if (this.reply.length > 500) {
      this.error = 'Reply is too long (max 500 characters)';
      return;
    }

    this.isSubmitting = true;
    this.error = '';

    try {
      const replyData = {
        parentId: this.parentComment.id,
        content: this.reply.trim(),
        timestamp: new Date()
      };
      
      this.replySubmitted.emit(replyData);
      this.reply = '';
    } catch (err) {
      this.error = 'Failed to post reply. Please try again.';
    } finally {
      this.isSubmitting = false;
    }
  }

  onCancel() {
    this.cancelled.emit();
  }
}
```

#### Rich Comment Form with Attachments
```html
<saf-comment-field ariaLabel="Create a new comment with attachments">
  <saf-avatar 
    slot="start"
    appearance="image"
    size="medium"
    [imgSrc]="currentUser.avatar"
    [label]="currentUser.name">
  </saf-avatar>
  
  <div>
    <saf-text-area
      label="Your comment"
      [(ngModel)]="comment"
      placeholder="Share your thoughts..."
      [rows]="4">
    </saf-text-area>
    
    <div *ngIf="showAttachments" class="attachments-section">
      <saf-file-upload
        accept="image/*,.pdf,.doc,.docx"
        [multiple]="true"
        (fileSelect)="handleFileUpload($event)">
      </saf-file-upload>
      
      <div *ngIf="attachments.length > 0" class="attachment-list">
        <h4>Attachments:</h4>
        <ul>
          <li *ngFor="let file of attachments; let i = index" class="attachment-item">
            <span>{{ file.name }}</span>
            <saf-button 
              appearance="secondary" 
              size="small"
              (click)="removeAttachment(i)">
              Remove
            </saf-button>
          </li>
        </ul>
      </div>
    </div>
  </div>
  
  <div slot="end" class="rich-comment-actions">
    <saf-button 
      appearance="tertiary"
      (click)="toggleAttachments()">
      {{ showAttachments ? 'Hide Attachments' : 'Add Attachments' }}
    </saf-button>
    
    <div class="button-group">
      <saf-button 
        appearance="secondary"
        (click)="clearAll()">
        Clear
      </saf-button>
      <saf-button 
        appearance="primary"
        (click)="submitComment()"
        [disabled]="!comment?.trim()">
        Post Comment
      </saf-button>
    </div>
  </div>
</saf-comment-field>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-rich-comment-form',
  templateUrl: './rich-comment-form.component.html',
  styleUrls: ['./rich-comment-form.component.scss']
})
export class RichCommentFormComponent {
  comment = '';
  attachments: File[] = [];
  showAttachments = false;
  currentUser = {
    name: 'Current User',
    avatar: '/current-user-avatar.jpg'
  };

  handleFileUpload(files: File[]) {
    this.attachments = [...this.attachments, ...files];
  }

  removeAttachment(index: number) {
    this.attachments = this.attachments.filter((_, i) => i !== index);
  }

  toggleAttachments() {
    this.showAttachments = !this.showAttachments;
  }

  async submitComment() {
    const formData = new FormData();
    formData.append('comment', this.comment);
    this.attachments.forEach((file, index) => {
      formData.append(`attachment_${index}`, file);
    });

    try {
      console.log('Submitting comment with attachments');
      this.clearAll();
    } catch (error) {
      console.error('Failed to submit comment:', error);
    }
  }

  clearAll() {
    this.comment = '';
    this.attachments = [];
    this.showAttachments = false;
  }
}
```

## Best Practices

- **Use semantic slot placement**: Place avatars in the `start` slot, main content in the default slot, and actions in the `end` slot for consistent layout.
- **Provide clear labels**: Use descriptive `ariaLabel` values that help screen reader users understand the purpose of the comment form.
- **Implement validation**: Always validate comment content before submission and provide clear error messages.
- **Handle loading states**: Show appropriate loading indicators during comment submission.
- **Character limits**: Consider implementing character limits for comments to maintain reasonable content length.
- **Clear functionality**: Provide users with an easy way to clear or cancel their input.
- **Keyboard navigation**: Ensure all interactive elements are accessible via keyboard navigation.
- **Auto-resize**: Consider using auto-resizing text areas for better user experience.

## Notes

- SafCommentField automatically creates a form structure with proper ARIA labeling and semantic roles.
- The component uses slots to provide flexible layout options while maintaining consistent styling.
- The form role is applied to the control element to help assistive technologies understand the structure.
- The component is designed to work seamlessly with other Saffron form components like SafTextArea and SafButton.
- Consider implementing auto-save functionality for longer comments to prevent data loss.
- The component provides a foundation for building complex comment interfaces with features like replies, editing, and attachments.
