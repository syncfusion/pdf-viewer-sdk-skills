# Text Selection

Brief: Guide users to implement text selection capabilities in PDF Viewer, allowing them to highlight and copy text from loaded documents. Text selection is enabled by default—guide users to control this behavior when they need to disable selection for read-only scenarios, capture selected text for processing, or respond to selection interactions to trigger custom workflows. Use this reference when users mention selecting text, copying content from PDFs, capturing text for search or analysis, or need to track user selection behavior.

## Table of Contents
- [When User Needs to Control Text Selection](#when-user-needs-to-control-text-selection)
- [When User Needs to Track Selection Start](#when-user-needs-to-track-selection-start)
- [When User Needs to Capture Selected Text](#when-user-needs-to-capture-selected-text)
- [Complete Pattern: Coordinating Start and End Events](#complete-pattern-coordinating-start-and-end-events)
- [Key Implementation Details](#key-implementation-details)

## When User Needs to Control Text Selection

### Scenario: User wants to prevent text selection (read-only PDFs)

When a user needs to create a read-only PDF experience where text cannot be selected or copied (e.g., secure documents, presentation mode), guide them to disable text selection using the `enableTextSelection` property.

**Property:** `enableTextSelection`

**Purpose:** Controls whether users can select and copy text from the PDF document. When `false`, text selection is completely disabled.

**Default:** `true` (selection enabled)

**Implementation:**
```tsx
<PdfViewerComponent
    enableTextSelection={false}  // Disable for read-only mode
>
    <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**When to enable (default behavior):**
- Users need to copy text for notes or citations
- Standard PDF reading experience
- Content is not sensitive or protected

**When to disable:**
- Secure or confidential documents
- Presentation or kiosk mode
- Forms where you want to prevent content extraction
- Read-only legal documents

---

## When User Needs to Track Selection Start

### Scenario: User wants to know when text selection begins

When a user needs to respond the moment selection starts—to show custom UI hints, pause keyboard shortcuts that might interfere, log selection analytics, or prepare for text processing—guide them to use the `textSelectionStart` event.

**Event:** `textSelectionStart`

**Purpose:** Fires immediately when a user begins selecting text. Use this to initialize contextual UI, disable conflicting features during selection, or capture selection start analytics.

**Event Arguments:** `TextSelectionStartEventArgs`
- **pageNumber**: The page where selection started
- **bounds**: Bounding box coordinates of the starting point
- **selectionBehavior**: Type or behavior of the selection

**Implementation:**
```tsx
const textSelectionStart = (args) => {
    // Show selection UI indicator
    console.log('Selection started on page:', args.pageNumber);
    console.log('Bounds:', args.bounds);
    
    // Disable keyboard shortcuts that might interfere
    disableGlobalShortcuts();
};

<PdfViewerComponent
    textSelectionStart={textSelectionStart}
>
    <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**Use this approach when user needs to:**
- Show a "Selecting..." indicator or highlight toolbar
- Temporarily disable keyboard shortcuts (Ctrl+F, etc.) that conflict
- Start a timer to track how long users take to select text
- Prepare UI for displaying selection tools (highlight, comment, etc.)
- Log page numbers where users most frequently start selections

---

## When User Needs to Capture Selected Text

### Scenario: User wants to access the selected text for processing

When a user needs to retrieve the actual text that was selected—to show it in a custom context menu, save it for notes, process it with AI/search, or enable actions based on content—guide them to use the `textSelectionEnd` event.

**Event:** `textSelectionEnd`

**Purpose:** Fires when text selection is finalized. Provides the complete selected text and metadata, allowing you to process, display, or act on the selection.

**Event Arguments:** `TextSelectionEndEventArgs`
- **pageNumber**: The page where selection occurred
- **bounds**: Bounding box coordinates of the completed selection
- **selectedText**: The actual text that was selected (key property)
- **isSelectionCopied**: Boolean indicating if text was copied to clipboard

**Implementation:**
```tsx
const textSelectionEnd = (args) => {
    const selectedText = args.selectedText;
    const pageNum = args.pageNumber;
    
    console.log('Selected text:', selectedText);
    console.log('On page:', pageNum);
    console.log('Was copied to clipboard:', args.isSelectionCopied);
    
    // Process the selected text
    if (selectedText) {
        showCustomContextMenu(selectedText);
        // OR: saveToNotes(selectedText);
        // OR: translateText(selectedText);
        // OR: searchWithAI(selectedText);
    }
};

<PdfViewerComponent
    textSelectionEnd={textSelectionEnd}
>
    <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**Use this approach when user needs to:**
- Show custom context menu with "Translate", "Search", "Define" options
- Auto-save selected quotes to a notes database
- Process selected text with AI (summarize, analyze sentiment)
- Enable "Highlight" or "Add Comment" buttons only when text is selected
- Track which text passages users select most frequently
- Send selected text to external services (translation, dictionary lookup)
- Display selected text in a sidebar for annotation

**Common pattern—enabling actions only when text is selected:**
```tsx
const [selectedText, setSelectedText] = React.useState('');
const [showActions, setShowActions] = React.useState(false);

const handleSelectionEnd = (args) => {
    if (args.selectedText) {
        setSelectedText(args.selectedText);
        setShowActions(true);  // Enable "Highlight", "Comment" buttons
    } else {
        setShowActions(false);
    }
};
```

---

## Complete Pattern: Coordinating Start and End Events

### Scenario: User needs responsive UI that tracks selection state

When a user wants to show live feedback during selection (e.g., "Selecting..." indicator while in progress, then show action buttons when complete), guide them to coordinate both events to manage UI state.

**Pattern: Track selection lifecycle from start to completion**

```tsx
const [selectedText, setSelectedText] = React.useState('');
const [isSelecting, setIsSelecting] = React.useState(false);

const handleTextSelectionStart = (args) => {
    setIsSelecting(true);  // Show "selecting" UI
    console.log('Selection started on page:', args.pageNumber);
};

const handleTextSelectionEnd = (args) => {
    setIsSelecting(false);  // Hide "selecting" UI
    setSelectedText(args.selectedText);  // Enable action buttons
    console.log('Selected text:', args.selectedText);
};

// UI responds to selection state:
{isSelecting && <div>Selecting text...</div>}

{selectedText && (
    <div style={{ padding: '10px', backgroundColor: '#f0f0f0' }}>
        <strong>Selected:</strong> {selectedText}
        <button>Highlight</button>
        <button>Copy Quote</button>
        <button>Translate</button>
    </div>
)}

<PdfViewerComponent
    enableTextSelection={true}
    textSelectionStart={handleTextSelectionStart}
    textSelectionEnd={handleTextSelectionEnd}
>
    <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**This coordinated pattern works well for:**
- Showing selection progress indicators
- Disabling conflicting features while selection is active
- Enabling action buttons only when selection completes successfully
- Coordinating with annotation or highlighting tools
- Providing smooth user experience with clear visual feedback

---

## Key Implementation Details

**Service Injection Required:**
The `TextSelection` service must be injected for text selection to work:
```tsx
<Inject services={[TextSelection]} />
```

**Default Behavior:**
Text selection is enabled by default (`enableTextSelection={true}`). Users can immediately select and copy text with standard mouse interactions.

**Performance:**
Text selection is optimized for large documents and works efficiently across multiple pages. No performance configuration needed for typical use cases.

**Accessibility:**
Text selection respects standard keyboard shortcuts (Ctrl+C, Cmd+C) and works with screen readers and accessibility tools for copying selected content.

---

## Text Selection Properties

The following property is available on the `PdfViewerComponent` to control text selection behavior:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isMaintainSelection** | Maintain text selection when page changes. | `boolean` | `false` |

### Usage Example

```tsx
<PdfViewerComponent
  enableTextSelection={true}
  isMaintainSelection={true}
>
  <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**When to enable `isMaintainSelection`:**
- Users need to maintain text selection across page navigation
- Building features that require persistent selection state
- Implementing multi-page text operations

**When to keep disabled (default):**
- Standard text selection behavior is sufficient
- Selection should clear when navigating to different pages
- Reducing visual clutter during navigation

---

## TextSelection API Methods

The TextSelection module provides programmatic methods to control and interact with text selection functionality.

Reference: https://ej2.syncfusion.com/react/documentation/api/pdfviewer/textselection

### copyText()

Programmatically copies the currently selected text in the PDF document to the clipboard.

#### Method
`copyText()`

#### Description
This method copies any text that is currently selected in the PDF Viewer to the system clipboard. It performs the same action as if the user had used the standard copy keyboard shortcut (Ctrl+C or Cmd+C).

#### Returns
`void`

#### Usage
```tsx
import React, { useRef } from 'react';
import { PdfViewerComponent, TextSelection, Inject } from '@syncfusion/ej2-react-pdfviewer';

function App() {
    const pdfViewerRef = useRef(null);

    const handleCopyText = () => {
        // Copy the currently selected text to clipboard
        pdfViewerRef.current.textSelection.copyText();
    };

    return (
        <div>
            <button onClick={handleCopyText}>Copy Selected Text</button>
            <PdfViewerComponent
                ref={pdfViewerRef}
                enableTextSelection={true}
            >
                <Inject services={[TextSelection]} />
            </PdfViewerComponent>
        </div>
    );
}
```

#### Use Cases
- Programmatically copy selected text when custom UI buttons are clicked
- Automate text copying as part of a workflow
- Integrate with custom clipboard management systems
- Create keyboard shortcut alternatives

---

### selectTextRegion()

Programmatically selects a specific text region in the PDF document based on provided page number and bounding coordinates.

#### Method
`selectTextRegion(pageNumbers: number, bounds: IRectangle[])`

#### Description
This method allows you to programmatically select text in a specific region of the PDF document. You specify the page number and an array of rectangular bounds that define the text region to select.

#### Parameters
- **pageNumbers** (`number`): The page number where the text region is located (1-based index)
- **bounds** (`IRectangle[]`): An array of rectangle objects defining the bounding boxes of the text regions to select

#### IRectangle Interface
```typescript
interface IRectangle {
    x: number;      // X-coordinate of the rectangle's top-left corner
    y: number;      // Y-coordinate of the rectangle's top-left corner
    width: number;  // Width of the rectangle
    height: number; // Height of the rectangle
}
```

#### Returns
`void`

#### Usage
```tsx
import React, { useRef } from 'react';
import { PdfViewerComponent, TextSelection, Inject } from '@syncfusion/ej2-react-pdfviewer';

function App() {
    const pdfViewerRef = useRef(null);
    const selectSpecificRegion = () => {
        // Define the text region to select on page 1
        const bounds = [
            { x: 100, y: 150, width: 200, height: 20 },
            { x: 100, y: 170, width: 180, height: 20 }
        ];
        // Select the text region on page 1
        pdfViewerRef.current.textSelection.selectTextRegion(1, bounds);
    };

    return (
        <div>
            <button onClick={selectSpecificRegion}>Select Specific Text Region</button>
            <PdfViewerComponent
                ref={pdfViewerRef}
                enableTextSelection={true}
            >
                <Inject services={[TextSelection]} />
            </PdfViewerComponent>
        </div>
    );
}
```

#### Use Cases
- Highlight specific sections of a document programmatically
- Implement search and highlight functionality
- Create automated document review workflows
- Pre-select important text regions for user attention
- Implement accessibility features for guided reading
- Automate text extraction from known document layouts

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---
