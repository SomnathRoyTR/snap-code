# SafFileUpload - File Upload Component

## Overview
`SafFileUpload` is a component for displaying file upload progress and status. It provides visual feedback during upload operations with progress indicators, status messages, and file information.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `status` | `'paused' \| 'info' \| 'error' \| 'success' \| 'warning'` | `undefined` | Current upload status |
| `file-name` | `string` | `undefined` | Name of the file being uploaded |
| `progress-value` | `number` | `undefined` | Upload progress (0-100) |
| `validation-message` | `string` | `undefined` | Status or error message |
| `file-types-text` | `string` | `undefined` | Description of allowed file types |
| `instructional-text` | `string` | `undefined` | Additional guidance text |

### Slots
| Slot | Description |
|------|-------------|
| (default) | Additional content or custom elements |
| `icon` | Custom icon for the upload status |
| `actions` | Action buttons (cancel, retry, etc.) |

### Events
| Event | Type | Description |
|-------|------|-------------|
| `cancel` | `CustomEvent<void>` | Fired when upload is cancelled |
| `retry` | `CustomEvent<void>` | Fired when retry is requested |
| `remove` | `CustomEvent<void>` | Fired when file is removed |

## Usage Examples

### Basic File Upload Display
```typescript
// React
import { SafFileUpload } from '@saffron/react';

export const BasicFileUpload = () => {
  return (
    <SafFileUpload
      file-name="document.pdf"
      status="info"
      progress-value={45}
      validation-message="Uploading..."
    />
  );
};

// Angular
import { Component } from '@angular/core';

@Component({
  template: `
    <saf-file-upload
      file-name="document.pdf"
      status="info"
      [progress-value]="45"
      validation-message="Uploading...">
    </saf-file-upload>
  `
})
export class BasicFileUploadComponent {}
```

### Complete Upload Flow
```typescript
// React
export const FileUploadFlow = () => {
  const [uploads, setUploads] = useState([]);
  
  const handleFileSelect = (files: FileList) => {
    Array.from(files).forEach(file => {
      const uploadId = Date.now() + Math.random();
      
      // Add to uploads list
      setUploads(prev => [...prev, {
        id: uploadId,
        file,
        fileName: file.name,
        status: 'info',
        progress: 0,
        message: 'Starting upload...'
      }]);
      
      // Simulate upload progress
      simulateUpload(uploadId, file);
    });
  };
  
  const simulateUpload = (uploadId: number, file: File) => {
    const interval = setInterval(() => {
      setUploads(prev => prev.map(upload => {
        if (upload.id !== uploadId) return upload;
        
        const newProgress = Math.min(100, upload.progress + Math.random() * 10);
        
        if (newProgress >= 100) {
          clearInterval(interval);
          return {
            ...upload,
            progress: 100,
            status: 'success',
            message: 'Upload complete!'
          };
        }
        
        return {
          ...upload,
          progress: newProgress,
          message: `Uploading... ${Math.round(newProgress)}%`
        };
      }));
    }, 200);
  };
  
  const removeUpload = (uploadId: number) => {
    setUploads(prev => prev.filter(upload => upload.id !== uploadId));
  };
  
  return (
    <div>
      <input
        type="file"
        multiple
        onChange={(e) => e.target.files && handleFileSelect(e.target.files)}
      />
      
      <div>
        {uploads.map(upload => (
          <SafFileUpload
            key={upload.id}
            file-name={upload.fileName}
            status={upload.status}
            progress-value={upload.progress}
            validation-message={upload.message}
          >
            <SafButton 
              slot="actions"
              appearance="ghost"
              onClick={() => removeUpload(upload.id)}
            >
              Remove
            </SafButton>
          </SafFileUpload>
        ))}
      </div>
    </div>
  );
};
```

### Error State with Retry
```typescript
// React
export const FileUploadWithRetry = () => {
  const [uploadState, setUploadState] = useState({
    fileName: 'large-document.pdf',
    status: 'error',
    progress: 67,
    message: 'Upload failed: Connection timeout'
  });
  
  const retryUpload = () => {
    setUploadState(prev => ({
      ...prev,
      status: 'info',
      message: 'Retrying upload...'
    }));
    
    // Simulate retry logic
    setTimeout(() => {
      setUploadState(prev => ({
        ...prev,
        progress: 100,
        status: 'success',
        message: 'Upload completed successfully!'
      }));
    }, 2000);
  };
  
  return (
    <SafFileUpload
      file-name={uploadState.fileName}
      status={uploadState.status}
      progress-value={uploadState.progress}
      validation-message={uploadState.message}
    >
      {uploadState.status === 'error' && (
        <SafButton 
          slot="actions"
          appearance="outline"
          onClick={retryUpload}
        >
          Retry
        </SafButton>
      )}
    </SafFileUpload>
  );
};
```

### Multiple File Upload Queue
```typescript
// React
export const FileUploadQueue = () => {
  const [queue, setQueue] = useState([
    { id: 1, name: 'report.xlsx', status: 'success', progress: 100, message: 'Completed' },
    { id: 2, name: 'presentation.pptx', status: 'info', progress: 78, message: 'Uploading...' },
    { id: 3, name: 'image.jpg', status: 'paused', progress: 23, message: 'Upload paused' },
    { id: 4, name: 'video.mp4', status: 'error', progress: 12, message: 'File too large' }
  ]);
  
  const updateUploadStatus = (id: number, updates: Partial<typeof queue[0]>) => {
    setQueue(prev => prev.map(item => 
      item.id === id ? { ...item, ...updates } : item
    ));
  };
  
  return (
    <div>
      <h3>Upload Queue</h3>
      {queue.map(item => (
        <SafFileUpload
          key={item.id}
          file-name={item.name}
          status={item.status}
          progress-value={item.progress}
          validation-message={item.message}
        >
          <div slot="actions">
            {item.status === 'paused' && (
              <SafButton
                appearance="ghost"
                onClick={() => updateUploadStatus(item.id, { 
                  status: 'info', 
                  message: 'Resuming...' 
                })}
              >
                Resume
              </SafButton>
            )}
            {item.status === 'info' && (
              <SafButton
                appearance="ghost"
                onClick={() => updateUploadStatus(item.id, { 
                  status: 'paused', 
                  message: 'Upload paused' 
                })}
              >
                Pause
              </SafButton>
            )}
            {item.status === 'error' && (
              <SafButton
                appearance="outline"
                onClick={() => updateUploadStatus(item.id, { 
                  status: 'info', 
                  progress: 0,
                  message: 'Retrying...' 
                })}
              >
                Retry
              </SafButton>
            )}
            <SafButton
              appearance="ghost"
              onClick={() => setQueue(prev => prev.filter(i => i.id !== item.id))}
            >
              Remove
            </SafButton>
          </div>
        </SafFileUpload>
      ))}
    </div>
  );
};
```

### File Type Validation Display
```typescript
// React
export const FileUploadWithValidation = () => {
  const allowedTypes = ['.pdf', '.doc', '.docx', '.jpg', '.png'];
  const maxSize = 10 * 1024 * 1024; // 10MB
  
  const [uploadInfo, setUploadInfo] = useState({
    fileName: 'document.txt',
    status: 'warning',
    progress: 0,
    message: 'File type not supported'
  });
  
  return (
    <div>
      <SafFileUpload
        file-name={uploadInfo.fileName}
        status={uploadInfo.status}
        progress-value={uploadInfo.progress}
        validation-message={uploadInfo.message}
        file-types-text={`Allowed: ${allowedTypes.join(', ')}`}
        instructional-text={`Maximum file size: ${maxSize / 1024 / 1024}MB`}
      >
        <SafButton 
          slot="actions"
          appearance="ghost"
          onClick={() => setUploadInfo(prev => ({ ...prev, status: null }))}
        >
          Choose Different File
        </SafButton>
      </SafFileUpload>
    </div>
  );
};
```

### Drag and Drop Upload
```typescript
// React
export const DragDropUpload = () => {
  const [dragOver, setDragOver] = useState(false);
  const [uploads, setUploads] = useState([]);
  
  const handleDrop = (e: React.DragEvent) => {
    e.preventDefault();
    setDragOver(false);
    
    const files = Array.from(e.dataTransfer.files);
    files.forEach(file => {
      setUploads(prev => [...prev, {
        id: Date.now() + Math.random(),
        fileName: file.name,
        status: 'info',
        progress: 0,
        message: 'Preparing upload...'
      }]);
    });
  };
  
  return (
    <div>
      <div
        onDrop={handleDrop}
        onDragOver={(e) => { e.preventDefault(); setDragOver(true); }}
        onDragLeave={() => setDragOver(false)}
        style={{
          border: `2px dashed ${dragOver ? '#007acc' : '#ccc'}`,
          borderRadius: '8px',
          padding: '40px',
          textAlign: 'center',
          backgroundColor: dragOver ? '#f0f8ff' : '#fafafa'
        }}
      >
        <p>Drag and drop files here or click to browse</p>
        <p>Supported formats: PDF, DOC, DOCX, JPG, PNG</p>
      </div>
      
      {uploads.map(upload => (
        <SafFileUpload
          key={upload.id}
          file-name={upload.fileName}
          status={upload.status}
          progress-value={upload.progress}
          validation-message={upload.message}
        />
      ))}
    </div>
  );
};
```

## Status States

### Success State
```typescript
// React
export const SuccessUpload = () => (
  <SafFileUpload
    file-name="contract.pdf"
    status="success"
    progress-value={100}
    validation-message="File uploaded successfully!"
  />
);
```

### Error State
```typescript
// React
export const ErrorUpload = () => (
  <SafFileUpload
    file-name="large-file.zip"
    status="error"
    progress-value={34}
    validation-message="Upload failed: File size exceeds 50MB limit"
  />
);
```

### Warning State
```typescript
// React
export const WarningUpload = () => (
  <SafFileUpload
    file-name="image.bmp"
    status="warning"
    progress-value={100}
    validation-message="File uploaded but format not optimal for web use"
  />
);
```

## Accessibility Features

- **ARIA Labels**: Proper labeling for progress and status
- **Progress Announcements**: Screen reader announcements for progress changes
- **Status Communication**: Clear communication of upload states
- **Focus Management**: Keyboard accessibility for action buttons
- **High Contrast**: Supports high contrast mode for status indicators

## Best Practices

1. **Clear Messaging**: Provide descriptive status messages
2. **Progress Indication**: Show accurate upload progress when possible
3. **Error Handling**: Offer clear error messages and recovery options
4. **File Validation**: Validate file types and sizes before upload
5. **Action Buttons**: Provide relevant actions for each status
6. **Performance**: Handle large file uploads efficiently
7. **User Feedback**: Keep users informed throughout the process

## Advanced Usage

### Chunked Upload Progress
```typescript
// React
export const ChunkedUpload = () => {
  const [upload, setUpload] = useState({
    fileName: 'large-video.mp4',
    status: 'info',
    progress: 0,
    message: 'Uploading chunk 1 of 10...',
    chunksCompleted: 0,
    totalChunks: 10
  });
  
  useEffect(() => {
    const interval = setInterval(() => {
      setUpload(prev => {
        if (prev.chunksCompleted >= prev.totalChunks) {
          clearInterval(interval);
          return {
            ...prev,
            progress: 100,
            status: 'success',
            message: 'Upload completed!'
          };
        }
        
        const newChunksCompleted = prev.chunksCompleted + 1;
        const progress = (newChunksCompleted / prev.totalChunks) * 100;
        
        return {
          ...prev,
          chunksCompleted: newChunksCompleted,
          progress: Math.round(progress),
          message: `Uploading chunk ${newChunksCompleted} of ${prev.totalChunks}...`
        };
      });
    }, 500);
    
    return () => clearInterval(interval);
  }, []);
  
  return (
    <SafFileUpload
      file-name={upload.fileName}
      status={upload.status}
      progress-value={upload.progress}
      validation-message={upload.message}
    />
  );
};
```

### Integration with Upload Service
```typescript
// React
export const ServiceIntegratedUpload = () => {
  const uploadFile = async (file: File) => {
    const formData = new FormData();
    formData.append('file', file);
    
    try {
      const response = await fetch('/api/upload', {
        method: 'POST',
        body: formData,
      });
      
      if (response.ok) {
        return { success: true, message: 'Upload successful' };
      } else {
        throw new Error('Upload failed');
      }
    } catch (error) {
      return { success: false, message: error.message };
    }
  };
  
  // Implementation would integrate with actual upload service
  return null;
};
```

## Notes

- Provides visual feedback for upload operations
- Supports various status states with appropriate styling
- Allows customization through slots for actions and icons
- Integrates well with file input and drag-drop interfaces
- Handles progress indication and status messaging
- Supports accessibility requirements for upload feedback
