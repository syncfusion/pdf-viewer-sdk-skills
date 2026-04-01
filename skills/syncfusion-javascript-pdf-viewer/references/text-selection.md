# Text Selection

**Description**: Text selection enables users to highlight and copy text from PDF documents. The TypeScript PDF Viewer provides text selection capabilities that are enabled by default, allowing users to select text with standard mouse interactions and copy to clipboard. This guide covers controlling text selection behavior, capturing selected text, and responding to selection events for custom workflows.

---

## Table of Contents

- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling and Disabling Text Selection](#enabling-and-disabling-text-selection)
- [Text Selection Events](#text-selection-events)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Text Selection Properties](#text-selection-properties)

---

## When to Use
Use text selection features when:
- Users need to copy text for notes, citations, or documentation
- Building standard PDF reading experiences
- Implementing custom text processing workflows (translate, search, analyze)
- Tracking user interactions with document content
- Enabling annotation or highlighting features based on selected text
- Creating accessible document viewers with screen reader support

Disable text selection when:
- Viewing secure or confidential documents
- Implementing presentation or kiosk mode
- Creating read-only legal documents where copying is restricted
- Forms where you want to prevent content extraction

---

## Prerequisites
Before using text selection features, ensure:
- `enableTextSelection: true` is set on the PdfViewer instance (enabled by default)
- `TextSelection` service is injected into the PdfViewer
- The PDF document is loaded and rendered

---

## Enabling and Disabling Text Selection
The TextSelection module allows users to highlight and copy text from the loaded PDF. Text selection is enabled by default and can be configured programmatically.

### Property
`enableTextSelection`

### Type
`boolean`

### Default Value
`true`

### Description
Controls whether users can select and copy text from the PDF document. When `false`, text selection is completely disabled.

### Usage

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  enableTextSelection: true  // Defaults to true
});
pdfviewer.appendTo('#PdfViewer');

// Disable text selection later if required
pdfviewer.enableTextSelection = false;
```

**When to enable (default behavior):**
- Users need to copy text for notes or citations
- Standard PDF reading experience
- Content is not sensitive or protected
- Supporting accessibility features

**When to disable:**
- Secure or confidential documents
- Presentation or kiosk mode
- Forms where you want to prevent content extraction
- Read-only legal documents

---

## Text Selection Events
Monitor user interaction with selection events to coordinate downstream actions such as showing tooltips, enabling context menus, or storing analytics.

### 1. textSelectionStart Event

**Signature:** `textSelectionStart: (args: TextSelectionStartEventArgs) => void`

Fires immediately when a user begins selecting text. Use this to initialize contextual UI, disable conflicting features during selection, or capture selection start analytics.

**Event Arguments:**
- `pageNumber` (number): The page where selection started
- `bounds` (object): Bounding box coordinates of the starting point
- `selectionBehavior` (string): Type or behavior of the selection

**Usage:**

```typescript
const handleTextSelectionStart = (args: any) => {
  console.log('Selection started on page:', args.pageNumber);
  console.log('Bounds:', args.bounds);
  console.log('Selection behavior:', args.selectionBehavior);
  
  // Show selection UI indicator or disable conflicting features
};

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  textSelectionStart: handleTextSelectionStart
});
pdfviewer.appendTo('#PdfViewer');
```

**Use Cases:**
- Show "Selecting..." indicator or highlight toolbar
- Temporarily disable keyboard shortcuts that might interfere
- Start a timer to track selection duration
- Prepare UI for displaying selection tools
- Log page numbers where users start selections

---

### 2. textSelectionEnd Event

**Signature:** `textSelectionEnd: (args: TextSelectionEndEventArgs) => void`

Fires when text selection is finalized. Provides the complete selected text and metadata, allowing you to process, display, or act on the selection.

**Event Arguments:**
- `pageNumber` (number): The page where selection occurred
- `bounds` (object): Bounding box coordinates of the completed selection
- `selectedText` (string): The actual text that was selected (key property)
- `isSelectionCopied` (boolean): Indicates if text was copied to clipboard

**Usage:**

```typescript
const handleTextSelectionEnd = (args: any) => {
  const selectedText = args.selectedText;
  const pageNum = args.pageNumber;
  
  console.log('Selected text:', selectedText);
  console.log('On page:', pageNum);
  console.log('Was copied to clipboard:', args.isSelectionCopied);
  
  // Process the selected text
  if (selectedText) {
    // Custom actions: translate, search, save, etc.
  }
};

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  textSelectionEnd: handleTextSelectionEnd
});
pdfviewer.appendTo('#PdfViewer');
```

**Use Cases:**
- Show custom context menu with "Translate", "Search", "Define" options
- Auto-save selected quotes to notes database
- Process selected text with AI (summarize, analyze)
- Enable "Highlight" or "Add Comment" buttons
- Track frequently selected text passages
- Send text to external services (translation, dictionary)

---

## API Methods

### 1. copyText()
**Signature:** `pdfviewer.textSelection.copyText(): void`
Programmatically copies the currently selected text in the PDF document to the clipboard.

**Example with Button:**
```html
<button id="copyTextBtn">Copy Selected Text</button>
```

```typescript
document.getElementById('copyTextBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.textSelection) {
    pdfviewer.textSelection.copyText();
  }
});
```

**Use Cases:**
- Programmatically copy selected text with custom UI buttons
- Automate text copying as part of a workflow
- Integrate with custom clipboard management systems
- Create keyboard shortcut alternatives
---

### 2. selectTextRegion()
**Signature:** `pdfviewer.textSelection.selectTextRegion(pageNumber: number, bounds: IRectangle[]): void`
Programmatically selects a specific text region in the PDF document based on provided page number and bounding coordinates.
**Parameters:**
- `pageNumber` (number): The page number where the text region is located (1-based index)
- `bounds` (IRectangle[]): An array of rectangle objects defining the bounding boxes

**IRectangle Interface:**
```typescript
interface IRectangle {
  x: number;      // X-coordinate of the rectangle's top-left corner
  y: number;      // Y-coordinate of the rectangle's top-left corner
  width: number;  // Width of the rectangle
  height: number; // Height of the rectangle
}
```
**Example with Button:**
```html
<button id="selectRegionBtn">Select Specific Text Region</button>
```
```typescript
document.getElementById('selectRegionBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.textSelection) {
    const bounds = [
      { x: 100, y: 150, width: 200, height: 20 }
    ];
    pdfviewer.textSelection.selectTextRegion(1, bounds);
  }
});
```

**Use Cases:**
- Highlight specific sections programmatically
- Implement search and highlight functionality
- Create automated document review workflows
- Pre-select important text regions for user attention
- Implement accessibility features for guided reading
- Automate text extraction from known layouts
---

## Complete Examples

### Example 1: Basic Text Selection Configuration

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Text Selection</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  enableTextSelection: true  // Enabled by default
});
pdfviewer.appendTo('#PdfViewer');
```

---

## Text Selection Properties
The following property is available on the `PdfViewer` component to control text selection behavior:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableTextSelection** | Enables or disables text selection functionality | `boolean` | `true` |

### Usage Example

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableTextSelection: true
});
```

**When to enable (default):**
- Standard PDF reading experience
- Users need to copy text for notes or citations
- Supporting accessibility features
- Content is not sensitive

**When to disable:**
- Secure or confidential documents
- Presentation or kiosk mode
- Read-only legal documents
- Preventing content extraction

---

## ⚠️ CRITICAL: Correct API Usage

**Text selection methods MUST be accessed via `pdfviewer.textSelection` module:**

```typescript
// ✅ CORRECT - Access via textSelection module
pdfviewer.textSelection.copyText();
pdfviewer.textSelection.selectTextRegion(pageNumber, bounds);

// ❌ WRONG - These methods DO NOT exist directly on pdfviewer
pdfviewer.copyText();             // ❌ WRONG - Missing .textSelection
pdfviewer.selectTextRegion();     // ❌ WRONG - Missing .textSelection
```

**Important Notes:**
- The `TextSelection` service must be injected for text selection to work
- Text selection is enabled by default (`enableTextSelection: true`)
- The `textSelectionEnd` event provides access to selected text via `args.selectedText`
- Use `copyText()` to programmatically copy selected text to clipboard
- Use `selectTextRegion()` to programmatically select specific text regions
- Page numbers for `selectTextRegion()` are 1-based (first page is 1, not 0)
- Standard keyboard shortcuts (Ctrl+C, Cmd+C) work automatically when text is selected

---
