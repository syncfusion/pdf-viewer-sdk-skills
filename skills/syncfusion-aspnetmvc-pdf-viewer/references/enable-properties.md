# Enable Properties in ASP.NET MVC Syncfusion PDFViewer Component

The ASP.NET MVC PDFViewer component provides a comprehensive set of enable properties to control and customize various features and functionalities of the PDF viewer. These boolean properties allow you to enable or disable specific capabilities such as annotations, form design, navigation, printing, and more.

### How to Use the Enable Properties in PDF Viewer

```cshtml
EnableToolbar(true)
EnableNavigation(true)
EnableAnnotation(true)
EnableFormDesigner(true)
EnablePrint(true)
EnableTextSearch(true)
EnableThumbnail(true)
EnableDownload(true)
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### List of Enable Properties

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **enableAccessibilityTags** | Enables or disables accessibility tags in the PDF document for improved accessibility support. | `boolean` |
| **enableAnnotation** | Enables or disables the annotation feature, allowing users to add comments, highlights, and markup annotations to PDF documents. | `boolean` |
| **enableAnnotationToolbar** | Enables or disables the annotation toolbar, which provides quick access to annotation tools like highlight, underline, and strikethrough. | `boolean` |
| **enableAutoComplete** | Enables or disables the auto-complete functionality for form fields in the PDF viewer. | `boolean` |
| **enableBookmark** | Enables or disables the bookmark feature, allowing users to navigate using document bookmarks. | `boolean` |
| **enableBookmarkStyles** | Enables or disables bookmark styling options in the PDF viewer. | `boolean` |
| **enableCommentPanel** | Enables or disables the comment panel, which displays comments and annotations added to the PDF document. | `boolean` |
| **enableDesktopMode** | Enables or disables desktop mode for optimized viewing experience on desktop devices. | `boolean` |
| **enableDownload** | Enables or disables the download functionality, allowing users to download the PDF document. | `boolean` |
| **enableFormDesigner** | Enables or disables the form designer feature, which allows users to create and edit form fields in PDF documents. | `boolean` |
| **enableFormDesignerToolbar** | Enables or disables the form designer toolbar with form field creation and editing tools. | `boolean` |
| **enableFormFields** | Enables or disables the form fields feature, allowing users to interact with fillable form fields in PDFs. | `boolean` |
| **enableFormFieldsValidation** | Enables or disables validation for form fields in the PDF viewer. | `boolean` |
| **enableFreeText** | Enables or disables the free text annotation feature for adding text comments directly on the PDF. | `boolean` |
| **enableHandwrittenSignature** | Enables or disables the handwritten signature feature for signing PDF documents. | `boolean` |
| **enableHyperlink** | Enables or disables hyperlink functionality in PDF documents. | `boolean` |
| **enableImportAnnotationMeasurement** | Enables or disables the import functionality for annotation measurements. | `boolean` |
| **enableInkAnnotation** | Enables or disables ink annotation feature for freehand drawing and annotations on the PDF. | `boolean` |
| **enableLocalStorage** | Enables or disables local storage to persist PDF viewer state and data locally. | `boolean` |
| **enableMagnification** | Enables or disables the magnification feature, allowing users to zoom in and out of the PDF document. | `boolean` |
| **enableMeasureAnnotation** | Enables or disables the measure annotation feature for measuring distances and areas in PDFs. | `boolean` |
| **enableMultiLineOverlap** | Enables or disables multi-line overlap handling in text markup annotations. | `boolean` |
| **enableMultiPageAnnotation** | Enables or disables annotations across multiple pages in the PDF document. | `boolean` |
| **enableNavigation** | Enables or disables the navigation feature, allowing users to move between pages in the PDF document. | `boolean` |
| **enableNavigationToolbar** | Enables or disables the navigation toolbar with page navigation and control buttons. | `boolean` |
| **enablePageOrganizer** | Enables or disables the page organizer feature for reordering, inserting, and deleting pages. | `boolean` |
| **enablePersistence** | Enables or disables persistence to save and restore the PDF viewer state across sessions. | `boolean` |
| **enablePinchZoom** | Enables or disables pinch zoom functionality for touch devices and mobile views. | `boolean` |
| **enablePrint** | Enables or disables the print functionality, allowing users to print the PDF document. | `boolean` |
| **enablePrintRotation** | Enables or disables page rotation during print operations. | `boolean` |
| **enableRedactionToolbar** | Enables or disables the redaction toolbar for redacting sensitive information from PDFs. | `boolean` |
| **enableRtl** | Enables or disables right-to-left (RTL) language support for proper rendering of RTL text. | `boolean` |
| **enableShapeAnnotation** | Enables or disables shape annotation features for drawing rectangles, circles, lines, and polygons. | `boolean` |
| **enableShapeLabel** | Enables or disables labels on shape annotations in the PDF viewer. | `boolean` |
| **enableStampAnnotations** | Enables or disables stamp annotations for adding pre-defined stamps like "Approved" or "Rejected". | `boolean` |
| **enableStickyNotesAnnotation** | Enables or disables sticky notes (comment) annotations for adding notes to the PDF. | `boolean` |
| **enableTextMarkupAnnotation** | Enables or disables text markup annotations including highlight, underline, and strikethrough. | `boolean` |
| **enableTextMarkupResizer** | Enables or disables the resizer for text markup annotations to adjust their size and position. | `boolean` |
| **enableTextSearch** | Enables or disables the text search feature, allowing users to search for text within the PDF document. | `boolean` |
| **enableTextSelection** | Enables or disables text selection in the PDF document for copying and highlighting. | `boolean` |
| **enableThumbnail** | Enables or disables the thumbnail panel for quick navigation and page preview. | `boolean` |
| **enableToolbar** | Enables or disables the main toolbar containing various action buttons and controls. | `boolean` |
| **enableZoomOptimization** | Enables or disables zoom optimization for better rendering performance at different zoom levels. | `boolean` |

### Usage Example with Multiple Enable Properties

```cshtml
// Set multiple enable properties on <ejs-pdfviewer>:
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).EnableNavigation(true).EnableAnnotation(true).EnableAnnotationToolbar(true).EnableBookmark(true).EnableCommentPanel(true).EnableFormDesigner(true).EnableFormDesignerToolbar(true).EnableFormFields(true).EnableFormFieldsValidation(true).EnableDownload(true).EnablePrint(true).EnableTextSearch(true).EnableTextSelection(true).EnableThumbnail(true).EnableMagnification(true).EnablePinchZoom(true).EnablePageOrganizer(true).EnableRedactionToolbar(true).EnableHandwrittenSignature(true).EnableZoomOptimization(true).Render()

```

**Important:** If a property is assigned a value that is the same as its default value, do not include that property in the output.

### Notes

- All enable properties accept boolean values (`true` or `false`)
- These properties can be set during component initialization or modified dynamically
- Disabling certain features can improve performance for specific use cases
- Some features may depend on others (e.g., enabling `enableAnnotationToolbar` requires `enableAnnotation` to be enabled)