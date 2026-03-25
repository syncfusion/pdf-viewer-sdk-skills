# Text Selection

Brief: The TextSelection module enables users to highlight and copy text from a loaded PDF document. Selection is enabled by default and can be configured or monitored programmatically to match application workflows. Use text selection to support copy operations, contextual actions, and accessibility scenarios in Angular PDF Viewer applications.

## Table of Contents
- [Enable or Disable Text Selection](#enable-or-disable-text-selection)
- [Text Selection Events](#text-selection-events)
- [TextSelectionStart Event](#textselectionstart-event)
- [TextSelectionEnd Event](#textselectionend-event)
- [Key Implementation Details](#key-implementation-details)

## Enable or Disable Text Selection

### Property: enableTextSelection

Controls whether users can select and copy text from the PDF document. When set to `false`, text selection is completely disabled throughout the document.

**Type:** `boolean`

**Default:** `true` (selection enabled)

### Usage

```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
               <ejs-pdfviewer id="pdfViewer"
                        [enableTextSelection]='true'
                        [documentPath]="document"
                        [resourceUrl]="resource"
                        style="height:640px;display:block">
               </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService ]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### When to Enable (Default)
- Users need to copy text for notes or citations
- Standard PDF reading experience with copy functionality
- Content is not sensitive or protected
- Accessibility features requiring text selection

### When to Disable
- Secure or confidential documents where copying is restricted
- Presentation or kiosk mode requiring read-only access
- Forms where you want to prevent content extraction
- Read-only legal documents with copy protection requirements

---

## Text Selection Events

Monitor user interactions with selection events to coordinate downstream actions such as showing tooltips, enabling context menus, or recording analytics. The PDF Viewer provides two key events to track the text selection lifecycle.

---

## TextSelectionStart Event

### Event: textSelectionStart

Fires when a user begins selecting text in the PDF document. Use this event to reset temporary UI state, pause conflicting shortcuts, or capture the starting context of the selection.

**Event Arguments:** `TextSelectionStartEventArgs`
- **pageNumber**: The page number where selection started
- **bounds**: Bounding box coordinates of the starting point
- **selectionBehavior**: Type or behavior of the selection

### Usage

```typescript
import { Component, OnInit } from '@angular/core';
import { TextSelectionService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
               <ejs-pdfviewer id="pdfViewer"
                        [documentPath]="document"
                        [resourceUrl]="resource"
                        (textSelectionStart)="textSelectionStart($event)"
                        style="height:640px;display:block">
               </ejs-pdfviewer>
            </div>`,
  providers: [ TextSelectionService ]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  public textSelectionStart(args: any): void {
    console.log('Selection started on page:', args.pageNumber);
    console.log('Bounds:', args.bounds);
    // Disable keyboard shortcuts that might interfere
    // Show selection UI indicator
  }
}
```

### Use Cases
- Show a "Selecting..." indicator or highlight toolbar when selection begins
- Temporarily disable keyboard shortcuts (Ctrl+F, etc.) that might conflict
- Start a timer to track how long users take to select text
- Prepare UI for displaying selection tools (highlight, comment buttons)
- Log page numbers where users most frequently start selections
- Initialize contextual UI components for text processing

---

## TextSelectionEnd Event

### Event: textSelectionEnd

Triggers after the text selection is finalized. Use this event to access the selected text, toggle contextual commands, or record telemetry for analytics.

**Event Arguments:** `TextSelectionEndEventArgs`
- **pageNumber**: The page number where selection occurred
- **bounds**: Bounding box coordinates of the completed selection
- **selectedText**: The actual text that was selected (key property)
- **isSelectionCopied**: Boolean indicating if text was copied to clipboard

### Usage

```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService, FormFieldsService, FormDesignerService,
         PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
               <ejs-pdfviewer id="pdfViewer"
                        [documentPath]="document"
                        [resourceUrl]="resource"
                        (textSelectionEnd)="textSelectionEnd($event)"
                        style="height:640px;display:block">
               </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService, FormFieldsService, FormDesignerService,
               PageOrganizerService ]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  public textSelectionEnd(args: any): void {
    const selectedText = args.selectedText;
    const pageNum = args.pageNumber;
    
    console.log('Selected text:', selectedText);
    console.log('On page:', pageNum);
    console.log('Was copied to clipboard:', args.isSelectionCopied);
    
    // Process the selected text
    if (selectedText) {
      // Show custom context menu, save to notes, translate, etc.
    }
  }
}
```

### Use Cases
- Show custom context menu with "Translate", "Search", "Define" options
- Auto-save selected quotes to a notes database or external system
- Process selected text with AI services (summarize, analyze sentiment)
- Enable "Highlight" or "Add Comment" buttons only when text is selected
- Track which text passages users select most frequently for analytics
- Send selected text to external services (translation, dictionary lookup)
- Display selected text in a sidebar panel for annotation or review

### Complete Pattern: Coordinating Start and End Events

When implementing responsive UI that tracks selection state, coordinate both events to manage the complete selection lifecycle:

```typescript
export class AppComponent {
  public selectedText: string = '';
  public isSelecting: boolean = false;

  public textSelectionStart(args: any): void {
    this.isSelecting = true;  // Show "selecting" UI indicator
    console.log('Selection started on page:', args.pageNumber);
  }

  public textSelectionEnd(args: any): void {
    this.isSelecting = false;  // Hide "selecting" UI indicator
    this.selectedText = args.selectedText;  // Enable action buttons
    console.log('Selected text:', args.selectedText);
  }
}
```

**Template usage:**
```html
<div *ngIf="isSelecting">Selecting text...</div>

<div *ngIf="selectedText" style="padding: 10px; background-color: #f0f0f0;">
    <strong>Selected:</strong> {{ selectedText }}
    <button>Highlight</button>
    <button>Copy Quote</button>
    <button>Translate</button>
</div>
```

---

## Key Implementation Details

**Service Injection Required:**
The `TextSelectionService` must be included in the component providers array for text selection functionality to work:

```typescript
providers: [ TextSelectionService, /* other services */ ]
```

**Default Behavior:**
Text selection is enabled by default when the TextSelectionService is injected. Users can immediately select and copy text using standard mouse interactions and keyboard shortcuts (Ctrl+C, Cmd+C).

**Performance:**
Text selection is optimized for large documents and works efficiently across multiple pages. No additional performance configuration is needed for typical use cases.

**Accessibility:**
Text selection respects standard keyboard shortcuts and works seamlessly with screen readers and accessibility tools for copying selected content. The feature supports assistive technologies for improved document accessibility.

**Angular Integration:**
Use Angular event binding syntax `(textSelectionStart)` and `(textSelectionEnd)` to wire up event handlers. Event arguments provide strongly-typed data for TypeScript applications.

---
