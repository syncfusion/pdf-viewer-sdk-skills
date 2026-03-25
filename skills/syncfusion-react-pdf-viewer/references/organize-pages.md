# Organize Pages

When users need to prepare PDF documents for sharing—reordering pages, correcting orientation, inserting or removing content—guide them to the Organize Pages panel. This feature provides document management capabilities without external tools.

## Table of Contents
- [When to Use](#when-to-use)
- [Base Component Setup](#base-component-setup)
- [Page Management Actions](#page-management-actions)
  - [Rotate Pages](#rotate-pages)
  - [Rearrange Pages](#rearrange-pages)
  - [Insert Blank Pages](#insert-blank-pages)
  - [Remove Pages](#remove-pages)
  - [Copy Pages](#copy-pages)
  - [Import Pages](#import-pages)
  - [Zoom Pages](#zoom-pages)
- [Extract Pages](#extract-pages)
- [Programmatic Control](#programmatic-control)
- [Toolbar Customization](#toolbar-customization)
- [Mobile Support](#mobile-support)
- [Events](#events)
- [Troubleshooting](#troubleshooting)

---

## When to Use

Guide users to the Organize Pages feature when they need to:
- **Reorder content** - Rearrange pages via drag-and-drop before finalizing documents
- **Correct orientation** - Rotate pages that display incorrectly (scanned documents, mixed orientations)
- **Prepare presentations** - Insert blank pages for notes, remove confidential pages, duplicate important content
- **Merge documents** - Import pages from another PDF into the current document
- **Extract subsets** - Export specific pages or ranges as new PDF files
- **Review thumbnails** - Zoom page thumbnails to verify document structure before sharing

**Decision point:** If users need multi-document workflows (merging 10+ files, batch processing), consider server-side PDF tools. The Organize Pages panel excels at single-document preparation tasks.

---

## Base Component Pattern

All page organizer features require the `PageOrganizer` service and `pageOrganizerSettings` property. Enable the feature with this baseline configuration:

```tsx
<PdfViewerComponent
  enablePageOrganizer={true}
>
</PdfViewerComponent>
```

**Critical:** The `PageOrganizer` service MUST be injected or the toolbar icon won't appear. If users can't see the Organize Pages option, verify injection.

---

## Page Management Actions

Configure `pageOrganizerSettings` to control which actions users can perform. Enable features based on workflow requirements—document review might need only rotation and rearrangement, while document preparation might require the full suite.

### Rotate Pages

**When to guide here:** User has scanned documents with incorrect orientation, mixed landscape/portrait pages, or pages that need correction before sharing.

Enable rotation to allow 90°, 180°, 270° clockwise and counter-clockwise adjustments:

```typescript
const pageOrganizerSettings = { canRotate: true };
```

---

### Rearrange Pages

**When to guide here:** User needs to reorder document sections, move pages to different positions, or reorganize content flow before finalizing.

Enable drag-and-drop rearrangement:

```typescript
const pageOrganizerSettings = { canRearrange: true };
```

---

### Insert Blank Pages

**When to guide here:** User needs to add separator pages, create space for handwritten notes, insert cover pages, or add placeholder pages between sections.

Enable blank page insertion:

```typescript
const pageOrganizerSettings = { canInsert: true };
```

---

### Remove Pages

**When to guide here:** User needs to delete confidential pages, remove draft content, eliminate blank pages, or reduce file size before sharing.

Enable page deletion:

```typescript
const pageOrganizerSettings = { canDelete: true };
```

---

### Copy Pages

**When to guide here:** User needs to duplicate content for multiple recipients, repeat important pages, or create copies within the same document.

Enable page duplication:

```typescript
const pageOrganizerSettings = { canCopy: true };
```

**Note:** If duplicates are not created, verify that the changes are persisted using Save.

---

### Import Pages

**When to guide here:** User needs to merge content from multiple PDFs, insert template pages, combine sections from different documents, or build composite documents.

Enable page import from external PDFs:

```typescript
const pageOrganizerSettings = { canImport: true };
```

---

### Zoom Pages

Change the thumbnail zoom level in the Organize Pages UI so you can view more detail or an overview of more pages. Page thumbnails resize interactively to suit your task.

**Properties:**
- `showImageZoomingSlider`: Show or hide the Zoom Pages button in the Organize Pages toolbar.
- `imageZoom`: Get or set the current thumbnail zoom level.
- `imageZoomMin`: Set the minimum zoom level for thumbnails.
- `imageZoomMax`: Set the maximum zoom level for thumbnails.

```typescript
const pageOrganizerSettings = { 
  showImageZoomingSlider: true, imageZoom: 1, imageZoomMin: 1, imageZoomMax: 5
};
```

**User workflow:** Open Organize Pages → Drag zoom slider → Thumbnails resize interactively

**Why configure min/max:** Limit zoom range to prevent performance issues (very high zoom) or unusably small thumbnails (very low zoom). Default range (1-5x) balances detail and overview needs.

**API Reference:**
- `showImageZoomingSlider`: `true` (show slider) | `false` (hide slider)
- `imageZoom`: Current zoom level (default 1)
- `imageZoomMin`: Minimum zoom boundary (default 1)
- `imageZoomMax`: Maximum zoom boundary (default 5)

---

## Extract Pages

**When to guide here:** User needs to create subset documents (chapters, sections), share specific pages without the full document, or split large PDFs into smaller files for distribution.

Enable page extraction to export selected pages as new PDF files:

```typescript
const pageOrganizerSettings = { 
  canExtractPages: true,          // Enables extraction functionality
  showExtractPagesOption: true    // Shows Extract button in toolbar
};
```

### Methods

**Method: extractPages(pageNumbers)** — Extract pages programmatically. Returns a byte array (Uint8Array) representing the PDF file contents.

```typescript
//  Page numbers are 1-based (the first page is 1). Invalid or out-of-range entries are ignored; only valid pages are processed.
viewer.pageOrganizer.extractPages('1,3,5');  // Extract pages 1, 3, 5
viewer.pageOrganizer.extractPages('2-6');    // Extract pages 2 through 6
viewer.pageOrganizer.extractPages('1,4,7-9'); // Extract pages 1, 4, and 7-9
```

---

## Programmatic Support

The PDF Viewer exposes programmatic APIs for organizing pages so applications can integrate page-management workflows.

### Properties

**Property: enablePageOrganizer** — Enable or disable the page organizer feature. Default: `true`.

**Property: isPageOrganizerOpen** — Control whether the page organizer opens automatically when a document loads. Default: `false`.

**Property: pageOrganizerSettings** — Customize page-management capabilities including:
- `canDelete`, `canInsert`, `canRotate`, `canCopy`, `canRearrange`, `canImport`: Enable/disable specific actions
- `imageZoom`, `imageZoomMin`, `imageZoomMax`: Control thumbnail zoom levels
- `showImageZoomingSlider`: Show/hide zoom slider
- `canExtractPages`, `showExtractPagesOption`: Control extract pages functionality

### Methods

**Method: openPageOrganizer()** — Programmatically opens the page organizer dialog, providing access to page management tools.

**Method: closePageOrganizer()** — Programmatically closes the page organizer dialog.

### Usage

```tsx
const pageOrganizerSettings = { 
  canDelete: true, 
  canInsert: true, 
  canRotate: true, 
  canCopy: true, 
  canRearrange: true, 
  canImport: true
};

const handleOpenOrganizer = () => {
  if (viewer) {
    viewer.pageOrganizer.openPageOrganizer();
  }
};

const handleCloseOrganizer = () => {
  if (viewer) {
    viewer.pageOrganizer.closePageOrganizer();
  }
};

// Buttons:
<button onClick={handleOpenOrganizer}>Open PageOrganizer Pane</button>
<button onClick={handleCloseOrganizer}>Close PageOrganizer Pane</button>

// Component:
<PdfViewerComponent
  enablePageOrganizer={true}
  isPageOrganizerOpen={true}  // Opens panel automatically
>
  <Inject services={[PageOrganizer]} />
</PdfViewerComponent>
```

**Decision point:** Use `isPageOrganizerOpen={true}` for document-prep workflows. Use `isPageOrganizerOpen={false}` (default) for general viewing where users open panel only when needed.

### Disable Page Organizer Completely

**When to guide here:** Application is view-only (no editing), users shouldn't modify documents, or organizational policy prevents document manipulation.

```tsx
<PdfViewerComponent
  enablePageOrganizer={false}  // Removes toolbar icon, disables feature
>
  {/* PageOrganizer service not needed when disabled */}
  <Inject services={[Toolbar, Magnification, Navigation]} />
</PdfViewerComponent>
```

**Result:** Organize Pages toolbar icon disappears, feature is completely unavailable.

### API Reference

**Properties:**
- `enablePageOrganizer`: `true` (feature available) | `false` (feature disabled) — Default: `true`
- `isPageOrganizerOpen`: `true` (auto-open on load) | `false` (manual open) — Default: `false`
- `pageOrganizerSettings`: Object configuring available actions (see [Page Management Actions](#page-management-actions))

**Methods:**
- `viewer.pageOrganizer.openPageOrganizer()`: Opens the panel programmatically
- `viewer.pageOrganizer.closePageOrganizer()`: Closes the panel programmatically
- `viewer.pageOrganizer.extractPages(pageNumbers)`: Extracts pages programmatically (see [Extract Pages](#extract-pages))

---


## Mobile Support

**When to guide here:** Users access the PDF viewer on phones or tablets and need page organization capabilities on touch devices.

The Organize Pages feature automatically adapts to mobile viewports with touch-optimized interactions:

### Mobile-Specific Behaviors

**Touch gestures:**
- **Tap:** Select a page thumbnail
- **Long-press (tap and hold):** Open context menu with actions
- **Drag:** Reorder pages (shows blue line indicating drop position)
- **Pinch:** Zoom thumbnails (if `showImageZoomingSlider` enabled)

### Context Menu Actions

**When to guide here:** User on mobile device needs to perform actions without toolbar buttons (screen space constrained).

Long-press any thumbnail to reveal the context menu:
- **Rotate Clockwise** - 90° rotation
- **Rotate Counter-Clockwise** - 90° rotation
- **Insert Page** - Add blank page at position
- **Copy Page** - Duplicate selected page
- **Delete Page** - Remove selected page
- **Select All** - Select all pages in document

**User workflow:** Long-press thumbnail → Choose action from menu → Change applies immediately

### Responsive Layout

The panel adapts to device orientation:
- **Portrait:** Thumbnails in vertical scrolling grid (2-3 columns)
- **Landscape:** More columns visible, wider thumbnails

**Why this matters:** Users get consistent functionality across devices. No separate mobile configuration needed—responsiveness is automatic.

**Troubleshooting:** If gestures don't work, verify:
1. `pageOrganizerSettings` enables the corresponding action (`canRotate`, `canDelete`, etc.)
2. Device viewport is detected as mobile (browser developer tools can test this)
3. Touch events aren't blocked by parent containers

---

## Events

The PDF Viewer exposes events for the page organizer to track and respond to page manipulation actions.

### Event: pageOrganizerSaveAs

The `pageOrganizerSaveAs` event is triggered when a save action is performed in the page organizer. Fires when the Save as button in the page organizer toolbar is clicked after modifying the document structure.

**Parameters:**
- `fileName`: The name of the currently loaded PDF document.
- `downloadDocument`: A base64-encoded string containing the modified PDF document.
- `cancel`: Boolean; set to `true` to prevent the default save action.

```typescript
pageOrganizerSaveAs={(args) => {
  console.log('File Name: ' + args.fileName);
  console.log('Document data: ' + args.downloadDocument);
}}
```

---

### Event: pageOrganizerZoomChanged

The `pageOrganizerZoomChanged` event fires when the page organizer zoom level changes. This event occurs when the user interacts with the zoom slider in the page organizer. The `showImageZoomingSlider` property in `pageOrganizerSettings` must be set to `true` for the slider to appear.

**Parameters:**
- `previousZoom`: The previous zoom value.
- `currentZoom`: The current zoom value.

```typescript
pageOrganizerZoomChanged={(args) => {
  console.log('Previous Zoom Value: ' + args.previousZoom);
  console.log('Current Zoom Value: ' + args.currentZoom);
}}
```

### Complete Event Example

```tsx
const handleSaveAs = (args: any) => {
  console.log('Saving document: ' + args.fileName);
  // Custom save logic here
};

const handleZoomChange = (args: any) => {
  console.log('Zoom changed from ' + args.previousZoom + ' to ' + args.currentZoom);
};

<PdfViewerComponent
  pageOrganizerSaveAs={handleSaveAs}
>
  <Inject services={[PageOrganizer]} />
</PdfViewerComponent>
```

**API Parameters:**
- `fileName` (string): Name of the loaded PDF document
- `downloadDocument` (string): Base64-encoded modified PDF content
- `cancel` (boolean): Set to `true` to prevent default browser download

**Decision point:** Set `args.cancel = true` when implementing custom save handlers. Leave `false` (default) for standard browser download behavior.

---

### pageOrganizerZoomChanged Event

**When to guide here:** Application needs to track user zoom preferences, sync zoom levels across views, or log interaction patterns.

Fires when user adjusts the thumbnail zoom slider:

```tsx
const handleZoomChange = (args: any) => {
  console.log('Zoom changed from', args.previousZoom, 'to', args.currentZoom);
  
  // Sync zoom level to state
  setThumbnailZoom(args.currentZoom);
  
  // Save user preference
  localStorage.setItem('preferredZoom', args.currentZoom.toString());
};

<PdfViewerComponent
  pageOrganizerZoomChanged={handleZoomChange}
  pageOrganizerSettings={{ showImageZoomingSlider: true }}
>
  <Inject services={[PageOrganizer]} />
</PdfViewerComponent>
```

**API Parameters:**
- `previousZoom` (number): Zoom level before change (e.g., 1.5)
- `currentZoom` (number): New zoom level (e.g., 2.0)

**⚠️ Important:** This event only fires when `showImageZoomingSlider: true` in `pageOrganizerSettings`. Without the slider, zoom doesn't change and the event never triggers.

---

### Complete Event Integration

```tsx
function DocumentEditor() {
  const [zoomLevel, setZoomLevel] = useState(1);

  const handleSaveAs = (args: any) => {
    // Upload to server instead of browser download
    fetch('/api/documents/save', {
      method: 'POST',
      body: JSON.stringify({
        filename: args.fileName,
        content: args.downloadDocument
      })
    })
    .then(response => {
      if (response.ok) {
        alert('Document saved successfully!');
        args.cancel = true; // Prevent default download
      }
    });
  };

  const handleZoomChange = (args: any) => {
    setZoomLevel(args.currentZoom);
    localStorage.setItem('organizerZoom', args.currentZoom);
  };

  return (
    <PdfViewerComponent
      pageOrganizerSaveAs={handleSaveAs}
      pageOrganizerZoomChanged={handleZoomChange}
      pageOrganizerSettings={{ 
        showImageZoomingSlider: true, imageZoom: zoomLevel
      }}
    >
      <Inject services={[PageOrganizer]} />
    </PdfViewerComponent>
  );
}
```

---

## Troubleshooting

### Organize Pages Icon Not Visible

**Symptom:** Toolbar doesn't show the Organize Pages button.

**Solutions:**
1. **Verify PageOrganizer injection:**
   ```tsx
   <PdfViewerComponent>
     <Inject services={[PageOrganizer]} />  {/* MUST include */}
   </PdfViewerComponent>
   ```
2. **Check enablePageOrganizer property:**
   ```tsx
   <PdfViewerComponent enablePageOrganizer={true}>
   ```
3. **Ensure Toolbar service is injected** (page organizer requires toolbar):
   ```tsx
   <Inject services={[Toolbar, PageOrganizer]} />
   ```

---

## Prerequisites

- `PageOrganizer` service injected into `PdfViewerComponent`
- `Extract Pages` only supported in client side rendering.