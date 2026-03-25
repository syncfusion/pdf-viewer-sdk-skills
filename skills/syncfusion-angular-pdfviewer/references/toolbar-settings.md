# Toolbar Customization in Angular PDF Viewer

Reference: Official Syncfusion Angular PDF Viewer Documentation

Brief: The Angular PDF Viewer provides comprehensive toolbar customization APIs enabling control over visibility, item selection, and arrangement across primary, annotation, form designer, page organizer, and mobile toolbars. These configurations allow tailored user experiences from simple document viewing to complex form design and annotation workflows.

---

## Table of Contents
- [Primary Toolbar Configuration](#primary-toolbar-configuration)
- [Annotation Toolbar Configuration](#annotation-toolbar-configuration)
- [Form Designer Toolbar Configuration](#form-designer-toolbar-configuration)
- [Page Organizer Toolbar Configuration](#page-organizer-toolbar-configuration)
- [Mobile Toolbar Configuration](#mobile-toolbar-configuration)
- [Custom Toolbar Implementation](#custom-toolbar-implementation)

---

## Primary Toolbar Configuration

The primary toolbar displays core document interaction controls including file operations, navigation, and magnification tools.

### Show or Hide Primary Toolbar

Control the visibility of the entire primary toolbar using the `enableToolbar` property at initialization or the `showToolbar()` method at runtime.

**Property**: `enableToolbar` (boolean, default: `true`)

**Method**: `toolbar.showToolbar(isVisible: boolean)`

**When to use**: Hide when implementing a fully custom toolbar or when the viewer should be embedded without default controls. Enable for standard document viewing workflows.

### Usage - Property Based

```typescript
import { Component } from '@angular/core';
import { PdfViewerModule } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [enableToolbar]="false"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### Usage - Method Based

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="hideToolbar()">Hide Toolbar</button>
    <ejs-pdfviewer #pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfviewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  hideToolbar(): void {
    this.pdfViewer?.toolbar.showToolbar(false);
  }
}
```

### Note

Disabling the toolbar removes all built-in controls. Ensure programmatic alternatives or custom UI elements are provided for essential operations like navigation, zoom, and download.

---

## Annotation Toolbar Configuration

The annotation toolbar provides markup tools for highlighting, commenting, drawing shapes, and adding text annotations to PDF documents.

### Show or Hide Annotation Toolbar

Control annotation toolbar visibility using the `enableAnnotationToolbar` property or the `showAnnotationToolbar()` method.

**Property**: `enableAnnotationToolbar` (boolean, default: `true`)

**Method**: `toolbar.showAnnotationToolbar(isVisible: boolean)`

**When to use**: Show when users need document markup capabilities. Hide for read-only viewing scenarios or when annotations are disabled.

### Usage - Method Based

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="toggleAnnotationToolbar()">Toggle Annotation Toolbar</button>
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  toggleAnnotationToolbar(): void {
    this.pdfViewer?.toolbar.showAnnotationToolbar(false);
  }
}
```

### Customize Annotation Toolbar Items

Specify which annotation tools appear using the `annotationToolbarItems` property within `toolbarSettings`.

**Property**: `toolbarSettings.annotationToolbarItems` (AnnotationToolbarItem[])

**Available Items**: `HighlightTool`, `UnderlineTool`, `StrikethroughTool`, `SquigglyTool`, `ColorEditTool`, `OpacityEditTool`, `AnnotationDeleteTool`, `StampAnnotationTool`, `HandWrittenSignatureTool`, `InkAnnotationTool`, `ShapeTool`, `CalibrateTool`, `StrokeColorEditTool`, `ThicknessEditTool`, `FreeTextAnnotationTool`, `FontFamilyAnnotationTool`, `FontSizeAnnotationTool`, `FontStylesAnnotationTool`, `FontAlignAnnotationTool`, `FontColorAnnotationTool`, `CommentPanelTool`

### Usage

```typescript
import { Component } from '@angular/core';
import { AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [toolbarSettings]="toolbarSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  
  public toolbarSettings = {
    annotationToolbarItems: [
      'HighlightTool',
      'UnderlineTool',
      'StrikethroughTool',
      'ColorEditTool',
      'OpacityEditTool',
      'AnnotationDeleteTool',
      'InkAnnotationTool',
      'ShapeTool',
      'FreeTextAnnotationTool',
      'CommentPanelTool'
    ]
  };
}
```

### Note

The annotation toolbar order follows the sequence in the `annotationToolbarItems` array. Items not included in the array are hidden. The toolbar adapts responsively based on available screen width.

---

## Form Designer Toolbar Configuration

The form designer toolbar enables creation and editing of interactive form fields including text boxes, checkboxes, radio buttons, dropdowns, and signature fields.

### Show or Hide Form Designer Toolbar

Control form designer toolbar visibility using the `enableFormDesigner` property or the `showFormDesignerToolbar()` method.

**Property**: `enableFormDesigner` (boolean, default: `true`)

**Method**: `toolbar.showFormDesignerToolbar(isVisible: boolean)`

**When to use**: Enable for form creation workflows. Disable when users should only fill forms or view documents without form design capabilities.

### Usage - Property Based

```typescript
import { Component } from '@angular/core';
import { FormDesignerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [enableFormDesigner]="false"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [FormDesignerService]
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/formdesigner.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### Customize Form Designer Toolbar Items

Specify which form field tools appear using the `formDesignerToolbarItems` property within `toolbarSettings`.

**Property**: `toolbarSettings.formDesignerToolbarItems` (FormDesignerToolbarItem[])

**Available Items**: `TextboxTool`, `PasswordTool`, `CheckBoxTool`, `RadioButtonTool`, `DropdownTool`, `ListboxTool`, `DrawSignatureTool`, `DeleteTool`

### Usage

```typescript
import { Component } from '@angular/core';
import { FormDesignerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [toolbarSettings]="toolbarSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [FormDesignerService]
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/formdesigner.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  
  public toolbarSettings = {
    formDesignerToolbarItems: [
      'TextboxTool',
      'PasswordTool',
      'CheckBoxTool',
      'RadioButtonTool',
      'DropdownTool',
      'ListboxTool',
      'DrawSignatureTool',
      'DeleteTool'
    ]
  };
}
```

### Note

Only the specified form designer tools will be visible. The toolbar order matches the sequence in the `formDesignerToolbarItems` array, providing a consistent form design experience across devices.

---

## Page Organizer Toolbar Configuration

The page organizer toolbar enables page manipulation operations including insert, delete, rotate, copy, import, and rearrange functionality for managing PDF document structure.

### Configure Page Operations

Control which page operations are available using the `pageOrganizerSettings` configuration object.

**Property**: `pageOrganizerSettings` (PageOrganizerSettings object)

**Available Properties**:
- `canInsert` (boolean, default: `true`) - Show/hide insert page tool
- `canDelete` (boolean, default: `true`) - Show/hide delete page tool
- `canRotate` (boolean, default: `true`) - Show/hide rotate page tool
- `canCopy` (boolean, default: `true`) - Show/hide copy page tool
- `canImport` (boolean, default: `true`) - Show/hide import pages tool
- `canRearrange` (boolean, default: `true`) - Enable/disable page rearrangement

**When to use**: Disable destructive operations (delete, import) for controlled environments. Enable all operations for full document editing workflows.

### Usage - Hide Insert Tool

```typescript
import { Component } from '@angular/core';
import { PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [pageOrganizerSettings]="{ canInsert: false }"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [PageOrganizerService]
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### Usage - Multiple Operations Control

```typescript
import { Component } from '@angular/core';
import { PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [pageOrganizerSettings]="pageOrganizerSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [PageOrganizerService]
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  
  public pageOrganizerSettings = {
    canInsert: false,
    canDelete: false,
    canRotate: true,
    canCopy: true,
    canImport: false,
    canRearrange: true
  };
}
```

### Note

Setting any property to `false` hides or disables the corresponding tool in the page organizer dialog. This provides fine-grained control over page manipulation capabilities based on user permissions and workflow requirements.

---

## Mobile Toolbar Configuration

The mobile toolbar provides an optimized interface for PDF viewing on mobile devices with touch-friendly controls and responsive layout adaptation.

### Desktop Mode on Mobile

Enable desktop toolbar features on mobile devices using the `enableDesktopMode` property to provide full desktop functionality on tablets and larger mobile screens.

**Property**: `enableDesktopMode` (boolean, default: `false`)

**When to use**: Enable for tablets with external keyboards or when mobile users require complete desktop-level features. Disable for optimized touch experience on small screens.

### Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [enableDesktopMode]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### Enable Touch Scrolling in Desktop Mode

Improve touch-based scrolling when desktop mode is enabled on mobile by disabling text selection using the `enableTextSelection` property.

**Property**: `enableTextSelection` (boolean, default: `true`)

**When to use**: Disable text selection when enabling desktop mode on mobile devices to prevent text selection gestures from interfering with touch scrolling.

### Usage

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [enableDesktopMode]="true"
      [enableTextSelection]="false"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
}
```

### Mobile Toolbar Features

The mobile toolbar includes optimized touch controls:
- **OpenOption**: Load PDF documents
- **SearchOption**: Text search within document
- **UndoRedoTool**: Undo/redo annotations
- **OrganizePagesTool**: Page organization features
- **AnnotationEditTool**: Annotation editing mode
- **DownloadOption**: Download document (in more options menu)
- **BookmarkOption**: View bookmarks (in more options menu)

### Note

Print functionality is not available in default mobile mode. To enable printing on mobile devices, set `enableDesktopMode` to `true`. The annotation toolbar displays at the bottom of the viewer in mobile mode for easier thumb access.

---

## Custom Toolbar Implementation

Create fully custom toolbars when default toolbar configurations don't meet branding, workflow, or UI requirements. Custom toolbars provide complete control over appearance, functionality, and user interactions.

### Implementation Pattern

1. **Disable default toolbar**: Set `enableToolbar="false"`
2. **Create Syncfusion Toolbar component**: Use `ejs-toolbar` with `e-items`
3. **Define toolbar items**: Add `e-item` with icon, id, tooltip, and alignment
4. **Handle click events**: Implement click handlers that call PDF Viewer APIs
5. **Inject required services**: Include ToolbarService and feature-specific services

### Custom Toolbar Structure

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, ToolbarService, MagnificationService, 
         NavigationService, PrintService } from '@syncfusion/ej2-angular-pdfviewer';
import { ToolbarModule } from '@syncfusion/ej2-angular-navigations';

@Component({
  selector: 'app-root',
  template: `
    <ejs-toolbar id='customToolbar' (clicked)='toolbarClick($event)'>
      <e-items>
        <e-item prefixIcon='e-icons e-folder' id='open' 
                tooltipText='Open' align='Left'></e-item>
        <e-item prefixIcon='e-icons e-chevron-left' id='previousPage' 
                tooltipText='Previous Page' align='Center'></e-item>
        <e-item prefixIcon='e-icons e-chevron-right' id='nextPage' 
                tooltipText='Next Page' align='Center'></e-item>
        <e-item prefixIcon='e-icons e-circle-add' id='zoomIn' 
                tooltipText='Zoom In' align='Center'></e-item>
        <e-item prefixIcon='e-icons e-circle-remove' id='zoomOut' 
                tooltipText='Zoom Out' align='Center'></e-item>
        <e-item prefixIcon='e-icons e-print' id='print' 
                tooltipText='Print' align='Right'></e-item>
        <e-item prefixIcon='e-icons e-download' id='download' 
                tooltipText='Download' align='Right'></e-item>
      </e-items>
    </ejs-toolbar>
    
    <input type="file" id="fileUpload" accept=".pdf" 
           style="display:none;" (change)="fileSelected($event)">
    
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="documentPath"
      [resourceUrl]="resourceUrl"
      [enableToolbar]="false"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [ToolbarService, MagnificationService, NavigationService, PrintService]
})
export class AppComponent {
  @ViewChild('pdfViewer') pdfViewer?: PdfViewerComponent;
  
  public documentPath: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resourceUrl: string = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

  toolbarClick(args: any): void {
    const viewer = this.pdfViewer;
    
    switch (args.item.id) {
      case 'open':
        document.getElementById('fileUpload')?.click();
        break;
      case 'previousPage':
        viewer?.navigation.goToPreviousPage();
        break;
      case 'nextPage':
        viewer?.navigation.goToNextPage();
        break;
      case 'zoomIn':
        viewer?.magnification.zoomIn();
        break;
      case 'zoomOut':
        viewer?.magnification.zoomOut();
        break;
      case 'print':
        viewer?.print.print();
        break;
      case 'download':
        viewer?.download();
        break;
    }
  }

  fileSelected(event: any): void {
    const files = event.target.files;
    if (files && files[0]) {
      const reader = new FileReader();
      reader.onload = (e: any) => {
        this.pdfViewer?.load(e.target.result, null);
      };
      reader.readAsDataURL(files[0]);
    }
  }
}
```

### API Mapping for Custom Toolbar

Map custom toolbar button actions to PDF Viewer APIs:

| Operation | API Method | Purpose |
|-----------|------------|---------|
| Open File | `load(document, password)` | Load PDF document |
| Previous Page | `navigation.goToPreviousPage()` | Navigate to previous page |
| Next Page | `navigation.goToNextPage()` | Navigate to next page |
| Go to Page | `navigation.goToPage(pageNumber)` | Jump to specific page |
| Zoom In | `magnification.zoomIn()` | Increase zoom level |
| Zoom Out | `magnification.zoomOut()` | Decrease zoom level |
| Fit to Page | `magnification.fitToPage()` | Fit page to viewer |
| Print | `print.print()` | Print document |
| Download | `download()` | Download document |

### Note

Custom toolbars require manual state management for button enabling/disabling based on viewer state (e.g., disable Previous Page on first page). Use viewer events like `pageChange` and `documentLoad` to update toolbar button states.

---
