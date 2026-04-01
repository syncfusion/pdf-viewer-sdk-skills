# Toolbar Methods in Angular PDF Viewer

## Table of Contents
- [When to Use Toolbar Methods](#when-to-use-toolbar-methods)
- [Overview](#overview)
- [Common Scenarios](#common-scenarios)
- [Toolbar Methods](#toolbar-methods)
- [Toolbar Properties](#toolbar-properties)
- [Decision Guide: Choosing the Right Method](#decision-guide-choosing-the-right-method)
- [Additional Examples](#additional-examples)
- [Edge Cases and Troubleshooting](#edge-cases-and-troubleshooting)

## When to Use Toolbar Methods

Use these methods when the user needs to:
- **Dynamically control toolbar visibility** based on application state (e.g., hide toolbars in presentation mode, show them for editing)
- **Create custom UI controls** that toggle specific PDF Viewer toolbars (primary, annotation, navigation, redaction)
- **Selectively enable/disable toolbar features** based on user permissions or document type
- **Build custom toolbar experiences** by hiding default toolbars and showing only specific items
- **Respond to user actions** (e.g., entering full-screen mode hides toolbars, exiting shows them)

## Overview

The Toolbar module provides runtime control over PDF Viewer toolbars. Unlike initialization properties (which set toolbar state at load time), these methods allow you to show or hide toolbars and enable or disable toolbar items dynamically in response to user interactions or application logic.

**Key Distinction:**
- **Properties** (`enableToolbar`, `enableNavigationToolbar`): Set initial toolbar state at component mount
- **Methods** (`showToolbar()`): Change toolbar state after component is mounted

## Common Scenarios

### Scenario 1: User wants presentation or distraction-free mode
Guide the user to hide the primary toolbar while keeping navigation controls:

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="enterPresentationMode()">Presentation Mode</button>
    <button (click)="exitPresentationMode()">Exit Presentation Mode</button>
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  enterPresentationMode(): void {
    // Hide main toolbar for clean viewing experience
    this.pdfViewer?.toolbar.showToolbar(false);
    // Keep navigation toolbar for page controls
    this.pdfViewer?.toolbar.showNavigationToolbar(true);
  }

  exitPresentationMode(): void {
    // Restore full toolbar for editing
    this.pdfViewer?.toolbar.showToolbar(true);
  }
}
```

### Scenario 2: User needs role-based toolbar access
When users have different permission levels (viewer vs. editor):

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  configureToolbarForRole(userRole: string): void {
    if (userRole === 'viewer') {
      this.pdfViewer?.toolbar.showAnnotationToolbar(true);
    }
  }
}
```

### Scenario 3: User switches between view and edit modes
Toggle annotation toolbar based on current mode:

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="toggleEditMode()">{{ isEditMode ? 'View Mode' : 'Edit Mode' }}</button>
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  public isEditMode: boolean = false;

  toggleEditMode(): void {
    this.isEditMode = !this.isEditMode;
    // Show annotation toolbar in edit mode, hide in view mode
    this.pdfViewer?.toolbar.showAnnotationToolbar(this.isEditMode);
  }
}
```

**Note**: See basic sample documentation for complete component setup and ViewChild configuration.

## Toolbar Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|-----|-----|-----|-----|
| **showAnnotationToolbar** | Shows or hides the annotation toolbar in the PDF Viewer. This method controls the visibility of the annotation toolbar that contains tools for adding and editing annotations. | `enableAnnotationToolbar: boolean` - If set to true, shows the annotation toolbar; if false, hides it. | void |
| **showNavigationToolbar** | Shows or hides the navigation toolbar in the PDF Viewer. The navigation toolbar contains tools for navigating through pages. | `enableNavigationToolbar: boolean` - If set to true, shows the navigation toolbar; if false, removes it. | void |
| **showRedactionToolbar** | Shows or hides the redaction toolbar in the PDF Viewer. This redaction customization feature is available only when the PDF Viewer is operating in Standalone Mode. Remarks: This method toggles the visibility of the redaction annotation toolbar in the PDF Viewer. | `enableRedactionToolbar: boolean` - If set to true, shows the redaction toolbar; if false, hides it. | void |
| **showToolbar** | Shows or removes the primary toolbar in the PDF Viewer. This is the main toolbar containing document operations like open, save, print, and download. | `enableToolbar: boolean` - If set to true, shows the toolbar; if false, removes it. | void |

## Toolbar Properties

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableToolbar** | Enables or disables the primary toolbar in the PDF Viewer at initialization. When set to false, the default toolbar is not displayed. | boolean | true |
| **enableFormDesigner** | Controls the visibility of the Form Designer toolbar. Set to true to show the form designer toolbar for form field interactions. | boolean | true |
| **enableNavigationToolbar** | Enables or disables the navigation toolbar at initialization. | boolean | true |
| **enableAnnotationToolbar** | Enables or disables the annotation toolbar at initialization. | boolean | true |

## Decision Guide: Choosing the Right Method

**User wants to hide or show the entire main toolbar?**
→ Use `showToolbar(boolean)`

**User needs to toggle annotation tools?**
→ Use `showAnnotationToolbar(boolean)`

**User wants page navigation controls only?**
→ Use `showNavigationToolbar(boolean)` (combine with `showToolbar(false)` to hide main toolbar)

**User needs redaction features?**
→ Use `showRedactionToolbar(boolean)` (Standalone Mode only)

## Additional Examples

### Dynamic Toolbar Visibility with State

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="toggleToolbars()">
      {{ showToolbars ? 'Hide UI' : 'Show UI' }}
    </button>
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  public showToolbars: boolean = true;

  toggleToolbars(): void {
    this.showToolbars = !this.showToolbars;
    this.pdfViewer?.toolbar.showToolbar(this.showToolbars);
    this.pdfViewer?.toolbar.showNavigationToolbar(this.showToolbars);
  }
}
```

## Edge Cases and Troubleshooting

**Toolbar methods called before component mounts:**
- Ensure the ViewChild is attached and component is rendered before calling toolbar methods
- Use lifecycle hooks like `ngAfterViewInit` or event handlers (not during constructor or ngOnInit)

**Methods not working:**
- Verify the toolbar service is imported: `import { ToolbarService } from '@syncfusion/ej2-angular-pdfviewer'`
- Check that the service is provided in the component: `providers: [ToolbarService, ...]`

**Want to customize toolbar items (not just show or hide):**
- Use `toolbarSettings` property for custom toolbar configuration
- See toolbar customization documentation for adding custom buttons

**Redaction toolbar not showing:**
- `showRedactionToolbar()` only works in Standalone Mode
- Server-backed mode does not support redaction toolbar
