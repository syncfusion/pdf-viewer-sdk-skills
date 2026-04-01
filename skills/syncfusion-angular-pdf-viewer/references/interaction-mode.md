# Interaction Mode

Reference: Official Syncfusion documentation for Angular PDF Viewer Interaction Mode

Brief: The Angular PDF Viewer provides two interaction modes for working with loaded PDF documents - Selection mode for text selection and copying, and Panning mode for touch-based scrolling and navigation. Configure interaction behavior to optimize user experience based on use case requirements.

---

## Table of Contents
- [Selection Mode](#selection-mode)
- [Panning Mode](#panning-mode)
- [Switching Interaction Modes](#switching-interaction-modes)
- [Required Services](#required-services)
- [Mode Behavior Notes](#mode-behavior-notes)

---

## Selection Mode

Enable text selection and copying from the loaded PDF document. Touch-based panning and page scrolling are disabled in this mode.

### Property
`enableTextSelection`

### Type
`boolean`

### Default Value
`true`

### Description
When set to `true`, users can select and copy text from the PDF document. This mode is ideal for document review, research, and content extraction workflows where text interaction is required.

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService
       } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
              <ejs-pdfviewer id="pdfViewer"
                      [enableTextSelection]='true'
                      [documentPath]='document'
                      style="height:640px;display:block">
              </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
}
```

**Result:** Users can click and drag to select text, then copy it to the clipboard. Touch-based panning is disabled to prevent interference with text selection.

### Behavior
- Text selection is enabled when `enableTextSelection` is `true`
- Users can select text by clicking and dragging across content
- Selected text can be copied to clipboard
- Touch panning and page scrolling are disabled to avoid selection conflicts
- Requires `TextSelectionService` to be included in providers

---

## Panning Mode

Enable touch-based panning and page scrolling for fluid navigation through the PDF document. Text selection is disabled in this mode.

### Property
`interactionMode`

### Type
`InteractionMode` (Enum: `'Selection'` | `'Pan'`)

### Default Value
`'Selection'`

### Description
Controls the primary interaction mode of the PDF Viewer. Set to `'Pan'` to enable touch-based scrolling and disable text selection. This mode is ideal for mobile devices, touch screens, and quick document browsing where text interaction is not needed.

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService
       } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
              <ejs-pdfviewer id="pdfViewer"
                      [enableTextSelection]='true'
                      [documentPath]='document'
                      [interactionMode]='interaction'
                      style="height:640px;display:block">
              </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public interaction = 'Pan';
}
```

**Result:** Users can drag the document to scroll through pages. Touch gestures work smoothly on mobile and tablet devices. Text selection is disabled.

### Behavior
- Touch-based panning and scrolling are enabled when `interactionMode` is `'Pan'`
- Users can drag or swipe to navigate through the document
- Text selection is disabled regardless of `enableTextSelection` value
- Provides better scroll performance on touch devices and mobile browsers
- Ideal for presentation mode and quick document browsing

---

## Switching Interaction Modes

Dynamically change interaction mode based on user actions or application state.

### Implementation Strategy

To switch between modes programmatically, update the `interactionMode` property:

- **Selection Mode**: Set `interactionMode='Selection'` and `enableTextSelection={true}`
- **Panning Mode**: Set `interactionMode='Pan'`

### Dynamic Mode Switching Example
```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService
       } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
              <button (click)="toggleMode()">
                Toggle Mode: {{ interaction === 'Pan' ? 'Panning' : 'Selection' }}
              </button>
              <ejs-pdfviewer id="pdfViewer"
                      [enableTextSelection]='enableSelection'
                      [documentPath]='document'
                      [interactionMode]='interaction'
                      style="height:640px;display:block">
              </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public interaction = 'Selection';
  public enableSelection = true;

  toggleMode() {
    if (this.interaction === 'Selection') {
      this.interaction = 'Pan';
      this.enableSelection = false;
    } else {
      this.interaction = 'Selection';
      this.enableSelection = true;
    }
  }
}
```

---

## Required Services

Interaction mode features require specific services to be injected in the providers array:

- **TextSelectionService**: Required for text selection functionality in Selection mode
- **NavigationService**: Required for page navigation in both modes
- **ToolbarService**: Recommended for providing UI controls to switch modes

### Complete Service Injection
```typescript
providers: [
  LinkAnnotationService, 
  BookmarkViewService, 
  MagnificationService,
  ThumbnailViewService, 
  ToolbarService, 
  NavigationService,
  AnnotationService, 
  TextSearchService, 
  TextSelectionService,
  PrintService
]
```

---

## Mode Behavior Notes

**Important Behavior:**
When `interactionMode` is set to `'Pan'`, touch panning is enabled and text selection is **not available** even if `enableTextSelection` is set to `true`. The `interactionMode` property takes priority over `enableTextSelection`.

**Selection Mode Characteristics:**
- Enables text selection and copying
- Disables touch-based panning to prevent conflicts
- Best for desktop applications and document review workflows
- Requires `TextSelectionService` in providers

**Panning Mode Characteristics:**
- Enables smooth touch scrolling and drag navigation
- Disables text selection to enable fluid panning
- Best for mobile devices, tablets, and touch-enabled displays
- Provides better performance for quick document browsing

**Use Case Recommendations:**
- Use Selection mode for research, legal review, content extraction
- Use Panning mode for mobile-first apps, kiosks, presentations
- Implement dynamic switching for applications supporting both workflows

**Troubleshooting:**
- If text selection doesn't work, verify `TextSelectionService` is in providers
- If panning feels unresponsive, ensure `interactionMode` is set to `'Pan'`
- Mode changes require component re-render to take effect
