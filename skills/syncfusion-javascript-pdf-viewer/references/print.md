# Print in TypeScript Syncfusion PDFViewer Component

## Table of Contents
- [Overview](#overview)
- [When to Use This Feature](#when-to-use-this-feature)
- [Quick Implementation](#quick-implementation)
- [Common Scenarios](#common-scenarios)
- [Print API Reference](#print-api-reference)
- [Decision Guide: Choosing Print Settings](#decision-guide-choosing-print-settings)
- [Troubleshooting & Edge Cases](#troubleshooting--edge-cases)
- [Key Implementation Notes](#key-implementation-notes)

## Overview
Guide users to implement print functionality in TypeScript PDF Viewer for document printing with customizable quality, mode, rotation, and event handling. This reference helps Claude assist users in configuring print behavior based on their specific requirements.

The Javascript (ES6) PDF Viewer includes built-in printing via the toolbar and APIs so users can control how documents are printed and monitor the process. Select Print in the built-in toolbar to open the browser print dialog.

## When to Use This Feature
**Direct users to print configuration when they need to:**
- Enable or disable printing capability
- Control print quality for different document types
- Handle landscape document rotation during printing
- Implement print mode selection (default browser dialog vs new window)
- Track print operations with event handlers
- Customize print behavior based on document characteristics

## Quick Implementation

### Basic Print Trigger
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';
viewer.appendTo('#pdfViewer');
// Print on button click
document.getElementById('printButton')?.addEventListener('click', () => {
    viewer.print.print(); // Opens browser's default print dialog
});
```

## Common Scenarios
### Scenario 1: User Wants to Print a Document
**Need:** Trigger print dialog from a button or toolbar action
**Implementation:**
```typescript
// Trigger print programmatically
const printButton = document.getElementById('print');
if (printButton) {
    printButton.onclick = function () {
        viewer.print.print();
    }
}
```
**Result:** Browser print dialog opens with the loaded PDF document

### Scenario 2: User Wants High-Quality Printing
**Need:** Print with better quality than default for documents with small text or fine details
**When to use:** Technical drawings, detailed charts, documents with small fonts
**Implementation:**
```typescript
viewer.printScaleFactor = 2.0; // Range: 0.5 to 5.0
```
**Why:** Higher scale factor (1.5-3.0) improves print clarity but increases processing time
**Trade-off:** Quality vs. performance - use 2.0-3.0 for small documents, 1.0-1.5 for large documents

### Scenario 3: User Wants to Disable Printing
**Need:** Prevent users from printing sensitive or confidential documents
**Implementation:**
```typescript
viewer.enablePrint = false; // Removes print button from toolbar
```
**Result:** Print option is hidden from UI; users cannot print the document

### Scenario 4: User Wants to Control Landscape Rotation
**Need:** Prevent automatic rotation of landscape pages during printing
**When to use:** Documents with intentional landscape orientation that shouldn't be rotated
**Implementation:**
```typescript
viewer.enablePrintRotation = false; // Suppress landscape rotation
```
**Default behavior (true):** Landscape pages automatically rotate to fit printer orientation
**When false:** Pages print in their original orientation

**Note:** The `enablePrintRotation` property enables automatic rotation of landscape pages during printing so they match the paper orientation. Enable this setting to reduce clipping of landscape pages; disable it to preserve the document's original orientation.

### Scenario 5: User Wants to Print in a New Window
**Need:** Open print preview in a separate window instead of browser dialog
**When to use:** Provide users with more control over print preview and settings
**Implementation:**
```typescript
viewer.printMode = 'NewWindow'; // 'Default' or 'NewWindow'
```
**Decision Guide:**
- **Default:** Quick print, familiar browser dialog, most common use case
- **NewWindow:** Advanced preview, custom print UI, more user control

**Note:** Browser pop-up blockers must allow new windows or tabs when using `printMode = 'NewWindow'`.

### Scenario 6: User Wants to Track Print Operations
**Need:** Log print events, validate before printing, or perform post-print actions
**Implementation:**
```typescript
let viewer: PdfViewer = new PdfViewer({
    printStart: (args: PrintStartEventArgs) => {
        console.log('Printing:', args.fileName);
        
        // Conditional validation
        const needsApproval = true; // Your validation logic
        if (needsApproval) {
            args.cancel = true; // Prevent print
            alert('Document requires approval before printing');
            return;
        }
    },
    printEnd: (args: PrintEndEventArgs) => {
        console.log('Print completed:', args.fileName);
        // Log to audit trail, update print count, etc.
    }
});
```
**Use cases:** Audit logging, print quotas, approval workflows, analytics

**Note:** Setting `args.cancel = true` in the `printStart` event prevents the print action and, depending on the environment, prevents the print dialog from appearing. In server-backed printing, cancellation prevents the service call that generates print output.

## Print API Reference

### List of Print Properties and Methods

| **API Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enablePrint** | If it is set as false, then the print option in the toolbar of the PDF Viewer will be disabled. | `boolean` | `true` |
| **enablePrintRotation** | If it is set as FALSE, will suppress the page rotation of Landscape document on print action. | `boolean` | `true` |
| **print()** | Print the PDF document being loaded in the PDF Viewer. | Method | - |
| **printMode** | Specifies the print mode in the PDF Viewer. Options: `'Default'` or `'NewWindow'` | `PrintMode` | `'Default'` |
| **printScaleFactor** | Specifies the document printing quality. The default printing quality is set to 1.0. Valid range: 0.5 to 5.0 | `number` | `1.0` |
| **printStart** | Event triggered when the print action starts. | Event | - |
| **printEnd** | Event triggered when the print action ends. | Event | - |

### Supporting Classes/Types

#### PrintMode
The `printMode` property accepts the following values:

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Default** | Prints the document from the same browser window. Use this when printing should remain in the current browsing context. | `string` |
| **NewWindow** | Prints the document from a new window or tab. Use this to avoid interference with the current page. | `string` |

### Print Events
#### PrintStartEventArgs
Event arguments for the `printStart` event:

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **cancel** | If it is true then the print operation will not work. Set to `true` to cancel the print operation. | `boolean` |
| **fileName** | File name of the currently loaded PDF document in the PDF Viewer. | `string` |

#### PrintEndEventArgs
Event arguments for the `printEnd` event:

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **fileName** | File name of the currently loaded PDF document in the PDF Viewer. | `string` |

### Usage Examples
#### Enable or Disable Print
```typescript
let viewer: PdfViewer = new PdfViewer();
viewer.enablePrint = true;
viewer.enablePrintRotation = false;
```

#### Set Print Quality
```typescript
let viewer: PdfViewer = new PdfViewer();
viewer.printScaleFactor = 2.0; // Higher quality for technical documents
```

#### Set Print Mode
```typescript
let viewer: PdfViewer = new PdfViewer();
viewer.printMode = 'NewWindow'; // Opens print in new window
```

#### Handle Print Events
```typescript
let viewer: PdfViewer = new PdfViewer({
    printStart: (args: PrintStartEventArgs) => {
        console.log('Print operation started for file:', args.fileName);
        // Perform custom validation or logging
        // args.cancel = true; // Set to true to prevent print
    },
    printEnd: (args: PrintEndEventArgs) => {
        console.log('Print operation completed for file:', args.fileName);
        // Perform post-print actions
    }
});
```

## Decision Guide: Choosing Print Settings
### Print Quality (printScaleFactor)
**Guide users based on document characteristics:**
The PDF Viewer adjusts print rendering quality using the `printScaleFactor` property. This numeric property accepts values from 0.5 to 5. Higher values improve printed image sharpness but increase rendering time and memory usage. By default, `printScaleFactor` is `1`.

**Note:** Values outside the supported range (0.5–5) revert to the default print quality (`1`).

| **Document Type** | **Recommended Scale** | **Why** |
|-----|-----|-----|
| Large PDFs (100+ pages) | 1.0 - 1.5 | Balances quality with processing time |
| Technical drawings | 2.0 - 3.0 | Fine lines and small text need higher quality |
| Text-heavy documents | 1.5 - 2.0 | Good readability without excessive processing |
| Image-heavy documents | 1.0 - 1.5 | Images already high-res, avoid over-processing |
| Small documents (<10 pages) | 2.0 - 5.0 | Can afford higher quality without performance hit |

**Trade-off:** Higher values = better quality but slower processing

**Implementation Examples:**
```typescript
viewer.printScaleFactor = 3.0; // High quality for fine details
```

```typescript
viewer.printScaleFactor = 1.0; // Standard quality, faster processing
```

### Print Mode Selection
**Help users choose between Default and NewWindow:**

The `printMode` property specifies how the PDF Viewer prints documents.

| **Use Case** | **Recommended Mode** | **Why** |
|-----|-----|-----|
| Simple print workflow | Default | Familiar browser dialog, quick access |
| Advanced print preview | NewWindow | More control, separate preview window |
| Mobile/responsive apps | Default | Better mobile browser compatibility |
| Desktop enterprise apps | NewWindow | Professional print preview experience |

**Implementation Examples:**

```typescript
viewer.printMode = 'Default'; // Browser's default print dialog
```

```typescript
viewer.printMode = 'NewWindow'; // Opens in new window
```

## Troubleshooting & Edge Cases
### Issue: Print Button Not Visible
**Cause:** `enablePrint` is set to false or Print module not injected
**Solution:**
```typescript
viewer.enablePrint = true; // Enable print functionality
```

### Issue: Landscape Pages Print Incorrectly
**Cause:** Browser auto-rotation conflicts with document orientation
**Solution:** Set `enablePrintRotation = false` to preserve original orientation

```typescript
viewer.enablePrintRotation = false; // Preserve original orientation
```

### Issue: Print Quality Too Low for Detailed Documents
**Cause:** Default `printScaleFactor = 1.0` insufficient for fine details
**Solution:** Increase to 2.0-3.0 for technical documents, CAD drawings, or small fonts

```typescript
viewer.printScaleFactor = 2.5; // Increase quality for fine details
```

### Issue: Print Dialog Takes Too Long to Open
**Cause:** High `printScaleFactor` on large documents
**Solution:** Reduce scale factor to 1.0-1.5 or warn users about processing time

```typescript
let viewer: PdfViewer = new PdfViewer({
    printScaleFactor: 1.2, // Lower scale for better performance
    printStart: (args: PrintStartEventArgs) => {
        console.log('Preparing print... this may take a moment for large documents');
    }
});
```

### Issue: Need to Prevent Printing Based on Conditions
**Cause:** No validation before print operation
**Solution:** Use `printStart` event and set `args.cancel = true`:

```typescript
let viewer: PdfViewer = new PdfViewer({
    printStart: (args: PrintStartEventArgs) => {
        const userHasPermission = false; // Your permission check logic
        if (!userHasPermission) {
            args.cancel = true;
            alert('You do not have permission to print this document');
        }
    }
});
```

### Issue: Print from New Window Blocked by Browser
**Cause:** Pop-up blocker preventing new window when using `printMode = 'NewWindow'`
**Solution:** Inform users to allow pop-ups or switch to Default mode

```typescript
let viewer: PdfViewer = new PdfViewer({
    printMode: 'NewWindow',
    printStart: (args: PrintStartEventArgs) => {
        console.log('If print window does not open, please allow pop-ups for this site');
    }
});
```

## Key Implementation Notes

- **Print Module Injection:** The Print module MUST be injected via `PdfViewer.Inject()` for print functionality to work
- **Scale Factor Range:** Valid range is 0.5 to 5.0; values outside this range will be clamped to default (1.0)
- **Performance Impact:** `printScaleFactor > 2.0` significantly increases memory usage and processing time for large documents
- **Browser Compatibility:** Print mode behavior may vary across browsers; test in target environments
- **Event Cancellation:** Only `printStart` supports cancellation via `args.cancel = true`; `printEnd` is informational only
- **Calling print() Method:** To start printing from code, call the `viewer.print.print()` method after the document is fully loaded. Calling print before the document finishes loading can result in no output or an empty print dialog
- **Resource URL:** Ensure the `resourceUrl` value matches the deployed `ej2-pdfviewer-lib` version when using standalone mode
- **Browser Behavior:** Calling `print()` launches the browser print dialog; behavior varies by browser and may be affected by popup blockers or browser settings

### Complete Example with All Print Settings

```typescript
// Initialize viewer with print settings
let viewer: PdfViewer = new PdfViewer({
    // Enable print feature
    enablePrint: true,
    // Control landscape rotation
    enablePrintRotation: true,
    // Set print quality (0.5 to 5.0)
    printScaleFactor: 2.0,
    // Set print mode
    printMode: 'Default', // 'Default' or 'NewWindow'
    // Handle print start event
    printStart: (args: PrintStartEventArgs) => {
        console.log('Print started for:', args.fileName);
        // Example: Validate before printing
        const canPrint = true; // Your validation logic
        if (!canPrint) {
            args.cancel = true;
            alert('Printing is not allowed at this time');
        }
    },
    // Handle print end event
    printEnd: (args: PrintEndEventArgs) => {
        console.log('Print completed for:', args.fileName);
        // Log to analytics, update print count, etc.
    }
});
// Programmatic print trigger
document.getElementById('customPrintBtn')?.addEventListener('click', () => {
    // Ensure document is loaded before printing
    if (viewer.pageCount > 0) {
        viewer.print.print();
    } else {
        console.warn('Document not loaded yet');
    }
});
```