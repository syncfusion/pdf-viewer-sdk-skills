# Print in Angular PDF Viewer Component

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

Guide users to implement print functionality in Angular PDF Viewer for document printing with customizable quality, mode, rotation, and event handling. This reference helps Claude assist users in configuring print behavior based on their specific requirements.

## When to Use This Feature

**Direct users to print configuration when they need to:**
- Enable or disable printing capability
- Control print quality for different document types
- Handle landscape document rotation during printing
- Implement print mode selection (default browser dialog vs new window)
- Track print operations with event handlers
- Customize print behavior based on document characteristics

## Quick Implementation

### Basic Print Setup

```typescript
import { Component } from '@angular/core';
import { PrintService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<ejs-pdfviewer id="pdfViewer" [documentPath]='document' 
                [enablePrint]='true' style="height:640px;display:block">
            </ejs-pdfviewer>`,
  providers: [PrintService]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
}
```

### Programmatic Print Trigger

```typescript
// Access viewer instance and trigger print
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
pdfViewer.print.print();
```

## Common Scenarios

### Scenario 1: User Wants to Print a Document
**Need:** Trigger print dialog from toolbar or programmatically
**Implementation:**
```typescript
// Programmatic approach
printDocument(): void {
  this.pdfViewer.print.print(); // Opens browser's default print dialog
}
```
**Result:** Browser print dialog opens with the loaded PDF document

### Scenario 2: User Wants High-Quality Printing
**Need:** Print with better quality than default for documents with small text or fine details
**When to use:** Technical drawings, detailed charts, documents with small fonts
**Implementation:**
```typescript
@Component({
  template: `<ejs-pdfviewer [documentPath]='document' 
                [printScaleFactor]='2.0' style="height:640px;display:block">
            </ejs-pdfviewer>`,
  providers: [PrintService]
})
export class AppComponent {
  public document = 'technical-drawing.pdf';
}
```
**Why:** Higher scale factor (1.5-3.0) improves print clarity but increases processing time
**Trade-off:** Quality vs. performance - use 2.0-3.0 for small documents, 1.0-1.5 for large documents

### Scenario 3: User Wants to Disable Printing
**Need:** Prevent users from printing sensitive or confidential documents
**Implementation:**
```typescript
[enablePrint]='false' // Removes print button from toolbar
```
**Result:** Print option is hidden from UI; users cannot print the document

### Scenario 4: User Wants to Control Landscape Rotation
**Need:** Prevent automatic rotation of landscape pages during printing
**When to use:** Documents with intentional landscape orientation that shouldn't be rotated
**Implementation:**
```typescript
[enablePrintRotation]='false' // Suppress landscape rotation
```
**Default behavior (true):** Landscape pages automatically rotate to fit printer orientation
**When false:** Pages print in their original orientation

### Scenario 5: User Wants to Print in a New Window
**Need:** Open print preview in a separate window instead of browser dialog
**When to use:** Provide users with more control over print preview and settings
**Implementation:**
```typescript
public printMode = 'NewWindow'; // 'Default' or 'NewWindow'
```
```html
<ejs-pdfviewer [printMode]='printMode'></ejs-pdfviewer>
```
**Decision Guide:**
- **Default:** Quick print, familiar browser dialog, most common use case
- **NewWindow:** Advanced preview, custom print UI, more user control

### Scenario 6: User Wants to Track Print Operations
**Need:** Log print events, validate before printing, or perform post-print actions
**Implementation:**
```typescript
import { PrintStartEventArgs, PrintEndEventArgs } from '@syncfusion/ej2-angular-pdfviewer';

printStart(args: PrintStartEventArgs): void {
  console.log("Printing:", args.fileName);
  
  // Conditional validation
  if (needsApproval) {
    args.cancel = true; // Prevent print
    alert("Document requires approval before printing");
    return;
  }
}

printEnd(args: PrintEndEventArgs): void {
  console.log("Print completed:", args.fileName);
  // Log to audit trail, update print count, etc.
}
```
```html
<ejs-pdfviewer (printStart)='printStart($event)' (printEnd)='printEnd($event)'></ejs-pdfviewer>
```
**Use cases:** Audit logging, print quotas, approval workflows, analytics

## Print API Reference

### List of Print Properties and Methods

| **API Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enablePrint** | If it is set as false, then the print option in the toolbar of the PDF Viewer will be disabled. | boolean | true |
| **enablePrintRotation** | If it is set as FALSE, will suppress the page rotation of Landscape document on print action. | boolean | true |
| **print()** | Print the PDF document being loaded in the PDF Viewer. | Method | - |
| **printMode** | Specifies the print mode in the PDF Viewer. | string | 'Default' |
| **printScaleFactor** | Specifies the document printing quality. The default printing quality is set to 1.0. | number | 1.0 |
| **printStart** | Event triggered when the print action starts. | Event | - |
| **printEnd** | Event triggered when the print action ends. | Event | - |

### Supporting Classes/Types

#### PrintMode

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Default** | Represents the Print mode Default | string |
| **NewWindow** | Represents the Print mode in New Window | string |

### Print Events

#### PrintStartEventArgs

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **cancel** | If it is true then the print operation will not work. | boolean |
| **fileName** | File name of the currently loaded PDF document in the PDF Viewer. | string |

#### PrintEndEventArgs

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **fileName** | File name of the currently loaded PDF document in the PDF Viewer. | string |

### Usage Examples

#### Enable or Disable Print
```typescript
[enablePrint]='true'
[enablePrintRotation]='false'
```

#### Set Print Quality
```typescript
[printScaleFactor]='2.0'
```

#### Set Print Mode
```typescript
public printMode = 'NewWindow';
```
```html
<ejs-pdfviewer [printMode]='printMode'></ejs-pdfviewer>
```

#### Handle Print Events
```typescript
printStart(args: PrintStartEventArgs): void {
  console.log("Print operation started for file:", args.fileName);
  // Perform custom validation or logging
  // args.cancel = true; // Set to true to prevent print
}

printEnd(args: PrintEndEventArgs): void {
  console.log("Print operation completed for file:", args.fileName);
  // Perform post-print actions
}
```
```html
<ejs-pdfviewer (printStart)='printStart($event)' (printEnd)='printEnd($event)'></ejs-pdfviewer>
```

## Decision Guide: Choosing Print Settings

### Print Quality (printScaleFactor)

**Guide users based on document characteristics:**

| **Document Type** | **Recommended Scale** | **Why** |
|-----|-----|-----|
| Large PDFs (100+ pages) | 1.0 - 1.5 | Balances quality with processing time |
| Technical drawings | 2.0 - 3.0 | Fine lines and small text need higher quality |
| Text-heavy documents | 1.5 - 2.0 | Good readability without excessive processing |
| Image-heavy documents | 1.0 - 1.5 | Images already high-res, avoid over-processing |
| Small documents (<10 pages) | 2.0 - 5.0 | Can afford higher quality without performance hit |

**Trade-off:** Higher values = better quality but slower processing

### Print Mode Selection

**Help users choose between Default and NewWindow:**

| **Use Case** | **Recommended Mode** | **Why** |
|-----|-----|-----|
| Simple print workflow | Default | Familiar browser dialog, quick access |
| Advanced print preview | NewWindow | More control, separate preview window |
| Mobile/responsive apps | Default | Better mobile browser compatibility |
| Desktop enterprise apps | NewWindow | Professional print preview experience |

## Troubleshooting & Edge Cases

### Issue: Print Button Not Visible
**Cause:** `enablePrint` is set to false or PrintService not injected
**Solution:**
```typescript
// Ensure PrintService is injected in providers:
import { PrintService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  providers: [PrintService]  // Required for print functionality
})
```

### Issue: Landscape Pages Print Incorrectly
**Cause:** Browser auto-rotation conflicts with document orientation
**Solution:** Set `[enablePrintRotation]='false'` to preserve original orientation

### Issue: Print Quality Too Low for Detailed Documents
**Cause:** Default `printScaleFactor` of 1.0 insufficient for fine details
**Solution:** Increase to 2.0-3.0 for technical documents, CAD drawings, or small fonts

### Issue: Print Dialog Takes Too Long to Open
**Cause:** High `printScaleFactor` on large documents
**Solution:** Reduce scale factor to 1.0-1.5 or warn users about processing time

### Issue: Need to Prevent Printing Based on Conditions
**Cause:** No validation before print operation
**Solution:** Use `printStart` event and set `args.cancel = true`:
```typescript
printStart(args: PrintStartEventArgs): void {
  if (!userHasPermission) {
    args.cancel = true;
    this.showAccessDeniedMessage();
  }
}
```

## Key Implementation Notes

- **Service Injection:** The PrintService MUST be injected in component providers array for print functionality to work
- **Scale Factor Range:** Valid range is 0.5 to 5.0; values outside this range will be clamped or revert to default (1.0)
- **Performance Impact:** `printScaleFactor > 2.0` significantly increases memory usage and processing time for large documents
- **Browser Compatibility:** Print mode behavior may vary across browsers; test in target environments
- **Event Cancellation:** Only `printStart` supports cancellation via `args.cancel = true`; `printEnd` is informational only
