# SafProgress - Linear Progress Indicator Component

## Overview
`SafProgress` is a linear progress bar component for showing task completion, loading states, and operation progress. It supports both determinate and indeterminate modes with various status colors and accessibility features.

## Component API

### Attributes
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `value` | `number` | `null` | Current progress value |
| `min` | `number` | `0` | Minimum value |
| `max` | `number` | `100` | Maximum value |
| `indeterminate` | `boolean` | `false` | Whether progress is indeterminate |
| `status-color` | `'error' \| 'loading' \| 'paused' \| 'success'` | `'loading'` | Status color theme |
| `label` | `string` | `undefined` | Descriptive label for the progress |
| `complete-label` | `string` | `'complete'` | Text shown with completion percentage |
| `aria-label` | `string` | `undefined` | ARIA label for accessibility |
| `aria-valuenow` | `string` | `undefined` | Current value for screen readers |

### Slots
| Slot | Description |
|------|-------------|
| `indeterminate` | Custom indeterminate indicator |

### CSS Parts
| Part | Description |
|------|-------------|
| `progress` | The main progress container |
| `determinate` | The determinate progress bar |
| `indeterminate` | The indeterminate progress indicator |

### Properties
| Property | Type | Description |
|----------|------|-------------|
| `percentComplete` | `number` | Calculated percentage (0-100) |

## Usage Examples

### Basic Determinate Progress
```typescript
// React
import { SafProgress } from '@saffron/react';

export const BasicProgress = () => {
  const [progress, setProgress] = useState(0);
  
  useEffect(() => {
    const timer = setInterval(() => {
      setProgress(prev => {
        if (prev >= 100) {
          clearInterval(timer);
          return 100;
        }
        return prev + 10;
      });
    }, 500);
    
    return () => clearInterval(timer);
  }, []);
  
  return (
    <SafProgress
      value={progress}
      max={100}
      label="Loading application..."
      aria-label="Application loading progress"
    />
  );
};

// Angular
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  template: `
    <saf-progress
      [value]="progress"
      [max]="100"
      label="Loading application..."
      aria-label="Application loading progress">
    </saf-progress>
  `
})
export class BasicProgressComponent implements OnInit, OnDestroy {
  progress = 0;
  private timer: any;
  
  ngOnInit() {
    this.timer = setInterval(() => {
      if (this.progress >= 100) {
        clearInterval(this.timer);
        return;
      }
      this.progress += 10;
    }, 500);
  }
  
  ngOnDestroy() {
    if (this.timer) clearInterval(this.timer);
  }
}
```

### File Upload Progress
```typescript
// React
export const FileUploadProgress = () => {
  const [uploads, setUploads] = useState([]);
  
  const simulateUpload = (fileName: string) => {
    const uploadId = Date.now();
    const newUpload = {
      id: uploadId,
      fileName,
      progress: 0,
      status: 'loading' as const
    };
    
    setUploads(prev => [...prev, newUpload]);
    
    const interval = setInterval(() => {
      setUploads(prev => prev.map(upload => {
        if (upload.id !== uploadId) return upload;
        
        const newProgress = Math.min(100, upload.progress + Math.random() * 15);
        
        if (newProgress >= 100) {
          clearInterval(interval);
          return { ...upload, progress: 100, status: 'success' as const };
        }
        
        return { ...upload, progress: Math.round(newProgress) };
      }));
    }, 300);
  };
  
  const removeUpload = (id: number) => {
    setUploads(prev => prev.filter(upload => upload.id !== id));
  };
  
  return (
    <div>
      <SafButton 
        onClick={() => simulateUpload(`file-${uploads.length + 1}.pdf`)}
        appearance="primary"
      >
        Upload File
      </SafButton>
      
      <div style={{ marginTop: '20px' }}>
        {uploads.map(upload => (
          <div key={upload.id} style={{ marginBottom: '16px' }}>
            <div style={{ 
              display: 'flex', 
              justifyContent: 'space-between', 
              alignItems: 'center',
              marginBottom: '8px'
            }}>
              <span>{upload.fileName}</span>
              <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
                <span>{upload.progress}%</span>
                {upload.progress === 100 && (
                  <SafButton 
                    appearance="ghost" 
                    onClick={() => removeUpload(upload.id)}
                  >
                    Remove
                  </SafButton>
                )}
              </div>
            </div>
            
            <SafProgress
              value={upload.progress}
              max={100}
              status-color={upload.status}
              label={`Uploading ${upload.fileName}`}
            />
          </div>
        ))}
      </div>
    </div>
  );
};
```

### Multi-Step Process Progress
```typescript
// React
export const MultiStepProgress = () => {
  const [currentStep, setCurrentStep] = useState(0);
  
  const steps = [
    { name: 'Personal Info', description: 'Enter your details' },
    { name: 'Address', description: 'Provide address information' },
    { name: 'Payment', description: 'Payment method setup' },
    { name: 'Confirmation', description: 'Review and submit' }
  ];
  
  const progress = ((currentStep + 1) / steps.length) * 100;
  
  return (
    <div>
      <div style={{ marginBottom: '24px' }}>
        <h3>Account Setup</h3>
        <p>Step {currentStep + 1} of {steps.length}: {steps[currentStep].description}</p>
        
        <SafProgress
          value={progress}
          max={100}
          status-color="loading"
          label={`Step ${currentStep + 1} of ${steps.length}`}
        />
      </div>
      
      <div style={{ display: 'flex', justifyContent: 'space-between' }}>
        <SafButton 
          onClick={() => setCurrentStep(Math.max(0, currentStep - 1))}
          disabled={currentStep === 0}
          appearance="outline"
        >
          Previous
        </SafButton>
        
        <SafButton 
          onClick={() => setCurrentStep(Math.min(steps.length - 1, currentStep + 1))}
          disabled={currentStep === steps.length - 1}
          appearance="primary"
        >
          Next
        </SafButton>
      </div>
    </div>
  );
};
```

### Indeterminate Progress
```typescript
// React
export const IndeterminateProgress = () => {
  const [loading, setLoading] = useState(false);
  
  const startProcess = async () => {
    setLoading(true);
    
    // Simulate async operation
    await new Promise(resolve => setTimeout(resolve, 3000));
    
    setLoading(false);
  };
  
  return (
    <div>
      <SafButton 
        onClick={startProcess} 
        disabled={loading}
        appearance="primary"
      >
        {loading ? 'Processing...' : 'Start Process'}
      </SafButton>
      
      {loading && (
        <div style={{ marginTop: '16px' }}>
          <SafProgress
            indeterminate
            status-color="loading"
            label="Processing your request..."
            aria-label="Processing in progress"
          />
        </div>
      )}
    </div>
  );
};
```

### Status Color Variants
```typescript
// React
export const StatusProgressBars = () => {
  const statuses = [
    { color: 'loading', value: 45, label: 'Loading data...' },
    { color: 'success', value: 100, label: 'Upload complete' },
    { color: 'error', value: 67, label: 'Upload failed' },
    { color: 'paused', value: 30, label: 'Process paused' }
  ] as const;
  
  return (
    <div style={{ display: 'flex', flexDirection: 'column', gap: '24px' }}>
      {statuses.map((status, index) => (
        <div key={index}>
          <h4 style={{ margin: '0 0 8px 0', textTransform: 'capitalize' }}>
            {status.color} State
          </h4>
          <SafProgress
            value={status.value}
            max={100}
            status-color={status.color}
            label={status.label}
          />
          <p style={{ margin: '4px 0 0 0', fontSize: '0.875rem', color: '#666' }}>
            {status.label} - {status.value}%
          </p>
        </div>
      ))}
    </div>
  );
};
```

### Download Progress with Cancel
```typescript
// React
export const DownloadProgress = () => {
  const [downloads, setDownloads] = useState([]);
  
  const startDownload = (fileName: string, size: string) => {
    const downloadId = Date.now();
    const newDownload = {
      id: downloadId,
      fileName,
      size,
      progress: 0,
      status: 'loading' as const,
      cancelled: false
    };
    
    setDownloads(prev => [...prev, newDownload]);
    
    const interval = setInterval(() => {
      setDownloads(prev => prev.map(download => {
        if (download.id !== downloadId || download.cancelled) {
          if (download.cancelled) clearInterval(interval);
          return download;
        }
        
        const increment = Math.random() * 8;
        const newProgress = Math.min(100, download.progress + increment);
        
        if (newProgress >= 100) {
          clearInterval(interval);
          return { ...download, progress: 100, status: 'success' as const };
        }
        
        return { ...download, progress: Math.round(newProgress) };
      }));
    }, 200);
  };
  
  const cancelDownload = (id: number) => {
    setDownloads(prev => prev.map(download => 
      download.id === id 
        ? { ...download, cancelled: true, status: 'error' as const }
        : download
    ));
  };
  
  const removeDownload = (id: number) => {
    setDownloads(prev => prev.filter(download => download.id !== id));
  };
  
  return (
    <div>
      <div style={{ display: 'flex', gap: '8px', marginBottom: '20px' }}>
        <SafButton 
          onClick={() => startDownload('document.pdf', '2.4 MB')}
          appearance="primary"
        >
          Download PDF
        </SafButton>
        <SafButton 
          onClick={() => startDownload('presentation.pptx', '15.8 MB')}
          appearance="primary"
        >
          Download Presentation
        </SafButton>
      </div>
      
      {downloads.map(download => (
        <div 
          key={download.id} 
          style={{ 
            marginBottom: '16px',
            padding: '16px',
            border: '1px solid #e0e0e0',
            borderRadius: '8px'
          }}
        >
          <div style={{ 
            display: 'flex', 
            justifyContent: 'space-between', 
            alignItems: 'center',
            marginBottom: '8px'
          }}>
            <div>
              <strong>{download.fileName}</strong>
              <span style={{ marginLeft: '8px', color: '#666' }}>
                ({download.size})
              </span>
            </div>
            
            <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
              <span>{download.progress}%</span>
              {!download.cancelled && download.progress < 100 && (
                <SafButton 
                  appearance="ghost"
                  onClick={() => cancelDownload(download.id)}
                >
                  Cancel
                </SafButton>
              )}
              {(download.progress === 100 || download.cancelled) && (
                <SafButton 
                  appearance="ghost"
                  onClick={() => removeDownload(download.id)}
                >
                  Remove
                </SafButton>
              )}
            </div>
          </div>
          
          <SafProgress
            value={download.progress}
            max={100}
            status-color={download.status}
            label={`Downloading ${download.fileName}`}
          />
          
          {download.cancelled && (
            <p style={{ margin: '4px 0 0 0', color: '#d32f2f', fontSize: '0.875rem' }}>
              Download cancelled
            </p>
          )}
        </div>
      ))}
    </div>
  );
};
```

### Form Validation Progress
```typescript
// React
export const FormValidationProgress = () => {
  const [form, setForm] = useState({
    name: '',
    email: '',
    phone: '',
    address: ''
  });
  
  const validationRules = {
    name: (value: string) => value.length >= 2,
    email: (value: string) => /\S+@\S+\.\S+/.test(value),
    phone: (value: string) => /^\+?[\d\s-()]+$/.test(value) && value.length >= 10,
    address: (value: string) => value.length >= 10
  };
  
  const validFields = Object.entries(form).filter(([key, value]) => 
    validationRules[key as keyof typeof validationRules]?.(value)
  ).length;
  
  const totalFields = Object.keys(validationRules).length;
  const completionProgress = (validFields / totalFields) * 100;
  
  const updateField = (field: string, value: string) => {
    setForm(prev => ({ ...prev, [field]: value }));
  };
  
  return (
    <div style={{ maxWidth: '400px' }}>
      <h3>Profile Setup</h3>
      <div style={{ marginBottom: '20px' }}>
        <SafProgress
          value={completionProgress}
          max={100}
          status-color={completionProgress === 100 ? 'success' : 'loading'}
          label="Form completion progress"
        />
        <p style={{ margin: '4px 0 0 0', fontSize: '0.875rem' }}>
          {validFields} of {totalFields} fields completed
        </p>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '16px' }}>
        <SafTextField
          label="Full Name"
          value={form.name}
          onChange={(e) => updateField('name', e.target.value)}
          required
        />
        
        <SafTextField
          label="Email"
          type="email"
          value={form.email}
          onChange={(e) => updateField('email', e.target.value)}
          required
        />
        
        <SafTextField
          label="Phone"
          value={form.phone}
          onChange={(e) => updateField('phone', e.target.value)}
          required
        />
        
        <SafTextField
          label="Address"
          value={form.address}
          onChange={(e) => updateField('address', e.target.value)}
          required
        />
        
        <SafButton
          appearance="primary"
          disabled={completionProgress < 100}
          style={{ marginTop: '16px' }}
        >
          Submit Profile
        </SafButton>
      </div>
    </div>
  );
};
```

## Accessibility Features

- **ARIA Progressbar**: Implements WAI-ARIA progressbar pattern
- **Value Announcements**: Screen reader announcements for value changes
- **Descriptive Labels**: Support for aria-label and descriptive text
- **Status Communication**: Clear indication of progress state
- **High Contrast**: Excellent visibility in high contrast mode
- **Live Regions**: Dynamic progress updates announced to assistive technology

## Best Practices

1. **Clear Labels**: Provide descriptive labels for progress context
2. **Value Ranges**: Use appropriate min/max values for your use case
3. **Status Colors**: Use consistent status colors throughout your application
4. **Indeterminate Use**: Use indeterminate for unknown duration processes
5. **Performance**: Avoid too frequent updates (debounce if necessary)
6. **Cancellation**: Provide cancel options for long-running processes
7. **Feedback**: Show completion states and error handling

## Advanced Usage

### Custom Progress Animation
```css
/* Custom progress bar styling */
saf-progress::part(determinate) {
  transition: width 0.3s ease-in-out;
}

saf-progress[status-color="success"]::part(determinate) {
  background: linear-gradient(90deg, #4caf50, #81c784);
}

saf-progress[indeterminate]::part(indeterminate) {
  animation: progress-indeterminate 2s infinite;
}

@keyframes progress-indeterminate {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
```

### Integration with Upload Service
```typescript
// React
export const ServiceIntegratedProgress = () => {
  const uploadWithProgress = async (file: File, onProgress: (progress: number) => void) => {
    const formData = new FormData();
    formData.append('file', file);
    
    const xhr = new XMLHttpRequest();
    
    return new Promise((resolve, reject) => {
      xhr.upload.addEventListener('progress', (e) => {
        if (e.lengthComputable) {
          const progress = (e.loaded / e.total) * 100;
          onProgress(Math.round(progress));
        }
      });
      
      xhr.addEventListener('load', () => {
        if (xhr.status === 200) {
          resolve(xhr.response);
        } else {
          reject(new Error('Upload failed'));
        }
      });
      
      xhr.addEventListener('error', () => reject(new Error('Upload failed')));
      
      xhr.open('POST', '/api/upload');
      xhr.send(formData);
    });
  };
  
  // Implementation would use real upload service
  return null;
};
```

## Notes

- Supports both determinate and indeterminate progress modes
- Provides status color variants for different contexts
- Implements full ARIA progressbar accessibility pattern
- Allows custom min/max ranges beyond 0-100
- Integrates well with file uploads and multi-step processes
- Supports customization through CSS parts and custom properties
