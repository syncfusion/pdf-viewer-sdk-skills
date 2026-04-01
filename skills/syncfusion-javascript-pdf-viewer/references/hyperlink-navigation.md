# Hyperlink Navigation

**Description**: Hyperlink Navigation in PDF Viewer enables users to interact with embedded links in PDF documents. The TypeScript PDF Viewer supports hyperlinks that point to external websites or destinations within the same document. Configure hyperlink behavior including enabling/disabling links, controlling how they open, and responding to hyperlink events for custom interactions.

---

## Table of Contents

- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling and Disabling Hyperlinks](#enabling-and-disabling-hyperlinks)
- [Controlling Link Open Behavior](#controlling-link-open-behavior)
- [Hyperlink Events](#hyperlink-events)
- [Complete Examples](#complete-examples)
- [Hyperlink Properties](#hyperlink-properties)

---

## When to Use

Use hyperlink navigation when:
- Users need to access external resources referenced in PDF documents
- Documents contain links to websites, email addresses, or external files
- Implementing URL validation or filtering for security purposes
- Providing custom link behavior (e.g., logging, analytics)
- Creating interactive documents with internal cross-references
- Building workflows that require tracking user link interactions

Disable hyperlinks when:
- Viewing sensitive documents where external links should be blocked
- Creating read-only document viewers with no external navigation
- Implementing security policies that prevent URL access
- Testing document layout without link interactions

---

## Prerequisites
Before using hyperlink navigation features, ensure:
- `enableHyperlink: true` is set on the PdfViewer instance (enabled by default)
- `LinkAnnotation` service is injected into the PdfViewer
- The PDF document contains embedded hyperlinks

---

## Enabling and Disabling Hyperlinks
Control whether hyperlinks in the PDF document are interactive or non-interactive.

### Property
`enableHyperlink`

### Type
`boolean`

### Default Value
`true`

### Description
By default, the PDF Viewer automatically detects and enables all hyperlinks present in a loaded document. When set to `false`, all hyperlinks become non-interactive and users cannot click them.

### Usage
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableHyperlink: false  // Disables all hyperlinks
});
```

**Note:** Disabling hyperlinks only affects the viewer's behavior and does not alter the original PDF document.

**When to disable:**
- Viewing sensitive documents where external access should be prevented
- Creating print-preview mode where links are not needed
- Implementing security policies
- Testing document layout without link interactions

---

## Controlling Link Open Behavior
Determine how external URLs are opened when a hyperlink is clicked.

### Property
`hyperlinkOpenState`

### Type
`'CurrentTab' | 'NewTab' | 'NewWindow'`

### Default Value
`'CurrentTab'`

### Description
Controls where external links open when clicked. Use `'CurrentTab'` to open in the current browser tab, `'NewTab'` to open in a new tab (preserving the user's current viewing session), or `'NewWindow'` to open in a new window.

### Usage

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  hyperlinkOpenState: 'NewTab'  // Opens links in a new browser tab
});
```

**Options:**
- `'CurrentTab'`: Opens link in the same tab (default)
- `'NewTab'`: Opens link in a new browser tab
- `'NewWindow'`: Opens link in a new browser window

**When to use `'NewTab'`:**
- Preserve user's current PDF viewing session
- Allow users to compare linked content with the PDF
- Implement multi-tasking workflows
- Prevent accidental navigation away from important documents

---

## Hyperlink Events
Handle user interactions with hyperlinks using event handlers.

### 1. hyperlinkClick Event
**Signature:** `hyperlinkClick: (args: HyperlinkClickEventArgs) => void`

Triggered when a user clicks a hyperlink. Use this to implement custom logic like URL validation or preventing default navigation.

**Event Arguments:**
- `hyperlink` (string): The URL of the clicked hyperlink
- `cancel` (boolean): Set to `true` to prevent the default navigation action

**Usage:**

```typescript
const handleHyperlinkClick = (args: any) => {
  console.log('Hyperlink Clicked:', args.hyperlink);
};
let pdfviewer: PdfViewer = new PdfViewer({
  hyperlinkClick: handleHyperlinkClick
});
```

**Example - URL Validation:**

```typescript
const handleHyperlinkClick = (args: any) => {
  const url = args.hyperlink;
  console.log('User clicked link:', url);
  // Block non-HTTPS links
  if (!url.startsWith('https://')) {
    args.cancel = true;
    alert('Only HTTPS links are allowed');
  }
};
```
---

### 2. hyperlinkMouseOver Event
**Signature:** `hyperlinkMouseOver: (args: HyperlinkMouseOverEventArgs) => void`

Triggered when the mouse pointer hovers over a hyperlink. Use this to display custom tooltips or visual feedback.

**Event Arguments:**
- `hyperlinkElement` (HTMLAnchorElement): The HTML anchor element corresponding to the hyperlink

**Usage:**
```typescript
const handleHyperlinkMouseOver = (args: any) => {
  console.log('Mouse over hyperlink:', args.hyperlinkElement.href);
  // Display custom tooltip or visual feedback
  args.hyperlinkElement.title = 'Click to open: ' + args.hyperlinkElement.href;
};
let pdfviewer: PdfViewer = new PdfViewer({
  hyperlinkMouseOver: handleHyperlinkMouseOver
});
```

---
## Complete Examples
### Example 1: Basic Hyperlink Configuration

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Hyperlink Navigation</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  enableHyperlink: true,
  hyperlinkOpenState: 'NewTab'
});
pdfviewer.appendTo('#PdfViewer');
```
---

### Example 2: Disable Hyperlinks Programmatically

```html
<div style="margin-bottom: 10px;">
  <button id="enableLinksBtn">Enable Hyperlinks</button>
  <button id="disableLinksBtn">Disable Hyperlinks</button>
  <span id="linkStatus">Status: Enabled</span>
</div>
<div id="PdfViewer" style="height: 640px;"></div>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  enableHyperlink: true,
  hyperlinkOpenState: 'NewTab'
});
pdfviewer.appendTo('#PdfViewer');

// Enable hyperlinks
document.getElementById('enableLinksBtn')?.addEventListener('click', () => {
  if (pdfviewer) {
    pdfviewer.enableHyperlink = true;
    updateStatus(true);
  }
});

// Disable hyperlinks
document.getElementById('disableLinksBtn')?.addEventListener('click', () => {
  if (pdfviewer) {
    pdfviewer.enableHyperlink = false;
    updateStatus(false);
  }
});

function updateStatus(enabled: boolean): void {
  const statusEl = document.getElementById('linkStatus');
  if (statusEl) {
    statusEl.textContent = `Status: ${enabled ? 'Enabled' : 'Disabled'}`;
    statusEl.style.color = enabled ? 'green' : 'red';
  }
}
```

---

## Hyperlink Properties

The following properties are available on the `PdfViewer` component to control hyperlink functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableHyperlink** | Enables or disables hyperlink navigation | `boolean` | `true` |
| **hyperlinkOpenState** | Controls how external links open (CurrentTab, NewTab, NewWindow) | `string` | `'CurrentTab'` |

### Usage Example

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  enableHyperlink: true,
  hyperlinkOpenState: 'NewTab'
});
pdfviewer.appendTo('#PdfViewer');
```

---
## ⚠️ CRITICAL: Correct API Usage

**Hyperlink configuration is done via properties and event handlers on the PdfViewer instance:**

```typescript
// ✅ CORRECT - Configure hyperlinks via PdfViewer properties
let pdfviewer: PdfViewer = new PdfViewer({
  enableHyperlink: true,
  hyperlinkOpenState: 'NewTab',
  hyperlinkClick: (args) => { /* handler */ },
  hyperlinkMouseOver: (args) => { /* handler */ }
});

// ❌ WRONG - There are no separate hyperlink methods to call
// pdfviewer.hyperlink.enable();  // NOT A VALID METHOD
// pdfviewer.openHyperlink();     // NOT A VALID METHOD
```

**Important Notes:**
- The `LinkAnnotation` service must be injected for hyperlink features to work
- `enableHyperlink` controls whether links are interactive (default: `true`)
- `hyperlinkOpenState` controls how external links open (default: `'CurrentTab'`)
- Use `args.cancel = true` in `hyperlinkClick` to prevent navigation
- The `hyperlinkMouseOver` event provides access to the anchor element for custom styling
---