# Download in Angular PDF Viewer component

Brief: The Angular PDF Viewer component provides download functionality to save the currently loaded PDF document. Users can download PDFs either through the toolbar button or programmatically using the download method.

## Table of Contents
- [Enable Download](#enable-download)
- [Programmatic Download](#programmatic-download)
- [Download Filename](#download-filename)
- [Related Features](#related-features)

## Enable Download

The download feature allows users to save the currently loaded PDF document to their local system.

### Property
`enableDownload`

### Type
`boolean`

### Default Value
`true`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { LinkAnnotationService, BookmarkViewService, MagnificationService,
         ThumbnailViewService, ToolbarService, NavigationService,
         TextSearchService, AnnotationService, TextSelectionService,
         PrintService
       } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<div class="content-wrapper">
               <ejs-pdfviewer id="pdfViewer"
                        [enableDownload]='true'
                        [documentPath]='document'
                        style="height:640px;display:block">
               </ejs-pdfviewer>
            </div>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               AnnotationService, TextSearchService, TextSelectionService,
               PrintService]
})
export class AppComponent implements OnInit {
    public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
}
```

### Note
When enabled, the download button appears in the PDF Viewer toolbar. This property works for both standalone and server-backed viewer modes.

---

## Programmatic Download

Trigger a download action programmatically without user interaction with the toolbar button.

### Method
`download()`

### Usage
```typescript
<script>
    window.onload = function () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.download();
    }
</script>
```

### Note
This method initiates the download of the currently loaded PDF document. Useful for implementing custom download buttons or automated save operations in your application workflow.

---

## Download Filename

Specify the filename for the downloaded PDF document.

### Property
`downloadFileName`

### Type
`string`

### Usage
```typescript
<ejs-pdfviewer id="pdfViewer"
         [downloadFileName]='customFileName'
         [documentPath]='document'
         style="height:640px;display:block">
</ejs-pdfviewer>
```

### Note
The filename can be set to provide a meaningful name for the downloaded file. If not specified, the default filename from the document or a generic name will be used.

---

## Related Features

### Toolbar Configuration
The download button can be customized as part of the toolbar settings. Refer to the toolbar items documentation for controlling the visibility and behavior of the download button within the toolbar.

### Feature Modules
The download functionality requires specific service providers to be injected. Ensure the necessary feature modules like ToolbarService are included in your component providers for the download feature to work properly.
