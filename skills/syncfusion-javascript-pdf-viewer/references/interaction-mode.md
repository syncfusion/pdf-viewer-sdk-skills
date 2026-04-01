# Interaction Mode

**Description**: The Interaction Mode feature in the Syncfusion TypeScript PDF Viewer provides two primary modes to control how users interact with PDF documents: Selection Mode for text selection and copying, and Panning Mode for touch-based scrolling and navigation. Use when implementing document viewing experiences that need to switch between reading workflows (panning) and content extraction workflows (text selection), or when optimizing for touch-enabled devices versus desktop environments.

## Table of Contents
- [When to Use Interaction Modes](#when-to-use-interaction-modes)
- [Selection Mode](#selection-mode)
- [Panning Mode](#panning-mode)
- [Decision Guide: Choosing the Right Mode](#decision-guide-choosing-the-right-mode)
- [Switching Between Modes](#switching-between-modes)
- [Required Services](#required-services)
- [Edge Cases and Troubleshooting](#edge-cases-and-troubleshooting)
- [Key Implementation Notes](#key-implementation-notes)

---

## When to Use Interaction Modes

Guide users to configure interaction modes when they need to:
- **Enable text selection and copying** for document review, quotation, or content extraction workflows
- **Enable touch-based scrolling** for mobile or tablet PDF viewing experiences
- **Switch between modes dynamically** based on user actions (e.g., toggle button, toolbar selection)
- **Optimize for specific use cases**: Reading mode (panning) vs. editing/review mode (selection)
- **Control user interactions** in restricted environments (view-only vs. interactive documents)

**Why this matters:** The interaction mode directly affects how users engage with PDF content. Selection mode supports text-based workflows (copying, highlighting, searching), while Panning mode provides fluid navigation for quick document browsing.

---

## Selection Mode

**User Need:** Users need to select and copy text from the loaded PDF document for quotations, citations, or documentation.

**When to use:** Document review workflows, research applications, content extraction tasks, or any scenario where users need to interact with PDF text.

### Property
`enableTextSelection`

### Description
A boolean property that controls whether text selection is enabled in the PDF Viewer. When set to `true`, users can select and copy text from the document.

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  enableTextSelection: true
});
viewer.appendTo('#PdfViewer');
```

**Result:** Users can click and drag to select text, then copy it to the clipboard. Panning is disabled to prevent accidental scrolling during text selection.

### Behavior
- When `enableTextSelection` is `true`, text selection mode is active
- Users can select text by clicking and dragging across content
- Text can be copied to clipboard
- Panning and touch scrolling are disabled to prevent selection interference

### Note
Text selection requires the `TextSelection` service to be injected in the component.

---

## Panning Mode

**User Need:** Users need to navigate through PDF documents quickly using drag gestures or touch scrolling, especially on mobile/tablet devices.

**When to use:** Mobile-friendly reading experiences, presentation mode, quick document browsing, or touch-enabled kiosks where text selection is not required.

### Property
`interactionMode`

### Description
Controls the interaction mode of the PDF Viewer. This property determines whether the viewer should be in panning mode or selection mode for document interaction.

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, InteractionMode } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  interactionMode: InteractionMode.Pan
});
viewer.appendTo('#PdfViewer');
```

**Alternative approach using enableTextSelection:**
```typescript
let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  enableTextSelection: false
});
viewer.appendTo('#PdfViewer');
```

**Result:** Users can drag the document to scroll through pages. Touch gestures work smoothly on mobile devices. Text selection is disabled.

### Behavior
- When `enableTextSelection` is `false` or `interactionMode` is set to `InteractionMode.Pan`, panning mode is active
- Users can drag the document to navigate through pages
- Touch scrolling is enabled for mobile and tablet devices
- Text selection is disabled to enable smooth panning

---

## Decision Guide: Choosing the Right Mode

**User wants to copy text or highlight content?**
→ Use Selection Mode (`enableTextSelection: true`)

**User needs fluid scrolling on touch devices?**
→ Use Panning Mode (`enableTextSelection: false` or `interactionMode: InteractionMode.Pan`)

**User switches between reading and annotation tasks?**
→ Implement dynamic mode switching with programmatic control (see example below)

**Application is mobile-first or kiosk-style?**
→ Default to Panning Mode for better touch UX

**Application is for research, legal review, or documentation?**
→ Default to Selection Mode for text interaction

---

## Switching Between Modes

**User Need:** Users need to switch between reading mode (panning) and review mode (text selection) without reloading the document.

**When to use:** Applications that support both casual browsing and detailed review workflows (e.g., document management systems, legal review tools).

### Implementation Strategy

To switch between modes dynamically, update the `enableTextSelection` property or `interactionMode` property programmatically:

- **Selection Mode**: Set `enableTextSelection = true` - Enables text selection, disables panning
- **Panning Mode**: Set `enableTextSelection = false` or `interactionMode = InteractionMode.Pan` - Enables panning, disables text selection

### Complete Example: Dynamic Mode Switching
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, InteractionMode } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  enableTextSelection: true
});
viewer.appendTo('#PdfViewer');

// Function to toggle between modes
const toggleMode = (): void => {
  viewer.enableTextSelection = !viewer.enableTextSelection;
  console.log(`Mode switched to: ${viewer.enableTextSelection ? 'Selection' : 'Panning'}`);
};

// Alternative approach using interactionMode
const switchToPanMode = (): void => {
  viewer.interactionMode = InteractionMode.Pan;
  console.log('Switched to Panning Mode');
};

const switchToSelectionMode = (): void => {
  viewer.interactionMode = InteractionMode.TextSelection;
  console.log('Switched to Selection Mode');
};

// Event handlers for buttons:
document.getElementById('toggleMode')?.addEventListener('click', toggleMode);
document.getElementById('panMode')?.addEventListener('click', switchToPanMode);
document.getElementById('selectionMode')?.addEventListener('click', switchToSelectionMode);
```

### Example with UI State Tracking
```typescript
let isSelectionMode: boolean = true;

const updateModeUI = (isSelection: boolean): void => {
  const button = document.getElementById('modeToggleBtn');
  if (button) {
    button.textContent = `Mode: ${isSelection ? 'Selection' : 'Panning'}`;
  }
};

const toggleInteractionMode = (): void => {
  isSelectionMode = !isSelectionMode;
  viewer.enableTextSelection = isSelectionMode;
  updateModeUI(isSelectionMode);
};

document.getElementById('modeToggleBtn')?.addEventListener('click', toggleInteractionMode);

// Initialize UI
updateModeUI(isSelectionMode);
```

---

## Required Services

Both interaction modes require specific services to be injected:

- **TextSelection Service**: Required for text selection functionality
- **Toolbar Service**: Recommended for user interface controls
- **Navigation Service**: For page navigation support
- **Magnification Service**: For zoom functionality

### Service Injection
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, Print } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(
  Toolbar, 
  Magnification, 
  Navigation, 
  Annotation, 
  LinkAnnotation, 
  ThumbnailView, 
  BookmarkView, 
  TextSelection, 
  TextSearch, 
  Print
);
```

---

## Edge Cases and Troubleshooting

**Text selection not working:**
- Verify `TextSelection` service is injected: `PdfViewer.Inject(..., TextSelection)`
- Ensure `enableTextSelection` is set to `true`
- Check that the PDF contains selectable text (not scanned images)
- Verify the document has loaded successfully before attempting selection

**Panning feels unresponsive:**
- Confirm `enableTextSelection` is set to `false` or `interactionMode` is set to `InteractionMode.Pan` (text selection blocks panning)
- On mobile devices, ensure touch events aren't blocked by other UI elements
- Test on actual devices, not just browser emulators
- Check for Javascript (ES6) errors that might prevent event handling

**Mode switching doesn't take effect:**
- Verify property assignment is executed: `viewer.enableTextSelection = false`
- Check that the viewer instance is properly initialized before changing modes
- Ensure no conflicting props override the mode setting
- Verify the document is loaded before switching modes

**Users accidentally select text when trying to scroll:**
- This indicates Selection Mode is active when Panning Mode is needed
- Set `enableTextSelection = false` or `interactionMode = InteractionMode.Pan` for reading-focused UX
- Provide a clear toggle button so users can switch modes intentionally
- Consider defaulting to Panning Mode for touch devices

**Touch scrolling not working on mobile:**
- Ensure Panning Mode is active (`enableTextSelection = false`)
- Check that viewport meta tags are properly configured in HTML
- Verify no CSS properties (like `touch-action`) are blocking touch events
- Test with different mobile browsers for compatibility

---

## Key Implementation Notes

- **Default Behavior**: By default, `enableTextSelection` is typically `true`, enabling text interaction
- **Performance**: Panning mode provides better scroll performance on lower-end devices when text selection is not needed
- **User Experience**: Selection mode is ideal for document review and text extraction; Panning mode is ideal for quick navigation and mobile browsing
- **Touch Devices**: Both modes support touch gestures, but Panning mode provides more intuitive touch scrolling
- **Service Dependencies**: TextSelection service is required for Selection Mode functionality
- **InteractionMode Enum**: The `InteractionMode` enum provides `Pan` and `TextSelection` values for explicit mode control
- **Dynamic Switching**: Mode can be changed at runtime without reloading the document, providing flexible user experiences
- **Mobile Optimization**: Consider detecting device type and setting appropriate default mode:
  ```typescript
  const isMobile = /Android|iPhone|iPad|iPod/i.test(navigator.userAgent);
  let viewer: PdfViewer = new PdfViewer({
    documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
    resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
    enableTextSelection: !isMobile // Panning for mobile, Selection for desktop
  });
  viewer.appendTo('#PdfViewer');
  ```
