# Events

**Description**: The PDF Viewer component triggers events for creation, page navigation, document lifecycle, context menu interactions, comments, bookmarks, download and export, hyperlinks, annotation import/export, custom keyboard commands, printing, signatures, text search, and text selection. Use these events to integrate custom logic into application workflows.

### How to Use the Event in PDF Viewer

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, Annotation, FormDesigner, FormFields, PageOrganizer } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView,
    BookmarkView, TextSelection, Annotation, FormDesigner, FormFields, PageOrganizer);

const viewer: PdfViewer = new PdfViewer({
    documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
    resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
    eventName: function (args: EventArgs) {
        // Event handling logic here
    }
});
viewer.appendTo('#pdfViewer');
```

> **Note:** For annotation and signature-specific events and arguments, see the dedicated Annotations Events topic.

### List of Events

| **Event Name** | **Description** | **Args** | **Args Properties** |
|-----|-----|-----|------|
|**bookmarkClick**|Triggers when a bookmark item is clicked in the bookmark panel.|**BookmarkClickEventArgs**|**name** - (string) - Name of the event. **text** - (string) - Title of the bookmark. **pageNumber** - (number) - Page number of the bookmark. **position** - (number) - Position of the bookmark content. **fileName** - (string) - File name from Launch action.|
|**buttonFieldClick**|Triggers when a button form field is clicked.|**ButtonFieldClickEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Form field id. **buttonFieldName** - (string) - Form field name. **buttonFieldValue** - (string) - Form field value.|
|**commentAdd**|Triggers when a comment is added to the comment panel.|**CommentEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the annotation comment. **annotation** - (string) - Annotation for the comment. **text** - (string) - Comment text. **status** - (CommentStatus) - Status of the annotation.|
|**commentDelete**|Triggers when a comment is deleted from the comment panel.|**CommentEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the annotation comment. **annotation** - (string) - Annotation for the comment. **text** - (string) - Comment text. **status** - (CommentStatus) - Status of the annotation.|
|**commentEdit**|Triggers when a comment is edited in the comment panel.|**CommentEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the annotation comment. **annotation** - (string) - Annotation for the comment. **text** - (string) - Comment text. **status** - (CommentStatus) - Status of the annotation.|
|**commentSelect**|Triggers when a comment is selected in the comment panel.|**CommentEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the annotation comment. **annotation** - (string) - Annotation for the comment. **text** - (string) - Comment text. **status** - (CommentStatus) - Status of the annotation.|
|**commentStatusChanged**|Triggers when a comment's status changes in the comment panel.|**CommentEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the annotation comment. **annotation** - (string) - Annotation for the comment. **text** - (string) - Comment text. **status** - (CommentStatus) - Status of the annotation.|
|**created**|Triggers during the creation of the PDF Viewer component.|**void**|No event arguments.|
|**customContextMenuBeforeOpen**|Fires before the custom context menu opens.|**CustomContextMenuBeforeOpenEventArgs**|**name** - (string) - Name of the event. **ids** - (string[]) - Array of identifiers of added custom context menu items; remove ids to hide items for this open.|
|**customContextMenuSelect**|Fires when a custom context menu item is selected.|**CustomContextMenuSelectEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Identifier of the currently selected custom context menu item.|
|**documentLoad**|Triggers while loading a document into the PDF Viewer.|**LoadEventArgs**|**name** - (string) - Name of the event. **documentName** - (string) - Document name loaded. **pageData** - (any) - Page details and page count of the PDF document.|
|**documentLoadFailed**|Triggers when document loading fails.|**LoadFailedEventArgs**|**name** - (string) - Name of the event. **documentName** - (string) - Document name that failed to load. **isPasswordRequired** - (boolean) - Whether document is password protected. **password** - (string) - The incorrect password used (if applicable).|
|**documentUnload**|Triggers when the document is closed.|**UnloadEventArgs**|**name** - (string) - Name of the event. **documentName** - (string) - Name of the document unloaded.|
|**downloadEnd**|Triggers after a document is downloaded.|**DownloadEndEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - File name of the loaded PDF. **downloadDocument** - (string) - Base64 string of the PDF document data.|
|**downloadStart**|Triggers when the download action is initiated.|**DownloadStartEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - File name of the loaded PDF. **cancel** - (boolean) - Set to true to prevent downloading.|
|**exportFailed**|Triggers when exporting annotations fails.|**ExportFailureEventArgs**|**name** - (string) - Name of the event. **errorDetails** - (string) - Error details for export failure. **exportData** - (any) - Annotation data to be exported. **formFieldData** - (any) - Form field data to be exported.|
|**exportStart**|Triggers when exporting annotations starts.|**ExportStartEventArgs**|**name** - (string) - Name of the event. **cancel** - (boolean) - Set to true to prevent exporting. **exportData** - (any) - Annotation data exported. **formFieldData** - (any) - Form field data exported.|
|**exportSuccess**|Triggers when annotations are exported successfully.|**ExportSuccessEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - Exported annotations JSON file name. **exportData** - (any) - Annotation data exported. **formFieldData** - (any) - Form field data exported.|
|**extractTextCompleted**|Triggers when text extraction is completed.|**ExtractTextCompletedEventArgs**|**name** - (string) - Name of the event. **documentTextCollection** - (DocumentTextCollectionSettingsModel[][]) - Extracted text collection for all pages.|
|**hyperlinkClick**|Triggers when a hyperlink is clicked.|**HyperlinkClickEventArgs**|**name** - (string) - Name of the event. **hyperlink** - (string) - URL to navigate. **hyperlinkElement** - (HTMLAnchorElement) - Current hyperlink element. **cancel** - (boolean) - Set to true to prevent navigation.|
|**hyperlinkMouseOver**|Triggers when hovering over a hyperlink.|**HyperlinkMouseOverArgs**|**name** - (string) - Name of the event. **hyperlink** - (string) - URL being hovered over.|
|**importFailed**|Triggers when importing annotations fails.|**ImportFailureEventArgs**|**name** - (string) - Name of the event. **errorDetails** - (string) - Error details for import failure. **importData** - (any) - Annotation data to be imported. **formFieldData** - (any) - Form field data to be imported.|
|**importStart**|Triggers when importing annotations starts.|**ImportStartEventArgs**|**name** - (string) - Name of the event. **importData** - (any) - JSON annotation data to be imported. **formFieldData** - (any) - JSON form field data to be imported.|
|**importSuccess**|Triggers when annotations are imported successfully.|**ImportSuccessEventArgs**|**name** - (string) - Name of the event. **importData** - (any) - Annotation data imported. **formFieldData** - (any) - Form field data imported.|
|**keyboardCustomCommands**|Triggers when customized keyboard command keys are pressed. Fires after registering gestures in `commandManager.keyboardCommand`.|**KeyboardCustomCommandsEventArgs**|**name** - (string) - Name of the event. **keyboardCommand** - (KeyboardCommandModel) - Command and key gesture that triggered execution.|
|**moveSignature**|Triggers when a signature is moved across the page.|**MoveSignatureEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the signature. **pageIndex** - (number) - Page number. **currentPosition** - (any) - Current position. **previousPosition** - (any) - Previous position. **opacity** - (number) - Opacity. **strokeColor** - (string) - Stroke color. **thickness** - (number) - Thickness. **type** - (AnnotationType) - Type of signature.|
|**pageChange**|Triggers when the current page number changes (e.g., via scrolling or navigation controls).|**PageChangeEventArgs**|**name** - (string) - Name of the event. **currentPageNumber** - (number) - Current page number. **previousPageNumber** - (number) - Previous page number. **documentName** - (string) - Document name.|
|**pageClick**|Triggers when a mouse click occurs on a page.|**PageClickEventArgs**|**name** - (string) - Name of the event. **pageNumber** - (number) - Page number where click occurred. **x** - (number) - X coordinate. **y** - (number) - Y coordinate. **documentName** - (string) - Document name.|
|**pageMouseover**|Triggers when moving the mouse over a page.|**PageMouseoverEventArgs**|**name** - (string) - Name of the event. **x** - (number) - X coordinate. **y** - (number) - Y coordinate. **pageNumber** - (number) - Page number.|
|**pageOrganizerSaveAs**|Triggers when a save as action is performed in the page organizer.|**PageOrganizerSaveAsEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - File name of the loaded PDF. **downloadDocument** - (string) - Base64 string of the PDF data. **cancel** - (boolean) - Set to true to prevent save as.|
|**pageRenderComplete**|Triggers after a page finishes rendering.|**PageRenderCompleteEventArgs**|**name** - (string) - Name of the event. **documentName** - (string) - Loaded PDF document name. **data** - (any) - Data related to completion of page rendering.|
|**pageRenderInitiate**|Triggers when page rendering begins.|**PageRenderInitiateEventArgs**|**name** - (string) - Name of the event. **jsonData** - (any) - Data requesting page rendering.|
|**printEnd**|Triggers when a print action is completed.|**PrintEndEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - File name of the loaded PDF.|
|**printStart**|Triggers when a print action is initiated.|**PrintStartEventArgs**|**name** - (string) - Name of the event. **fileName** - (string) - File name of the loaded PDF. **cancel** - (boolean) - Set to true to prevent printing.|
|**removeSignature**|Triggers when a signature is removed.|**RemoveSignatureEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the removed signature. **pageIndex** - (number) - Page number. **bounds** - (any) - Bounds of the removed signature. **type** - (AnnotationType) - Type of the removed signature.|
|**resizeSignature**|Triggers when a signature is resized.|**ResizeSignatureEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the signature. **pageIndex** - (number) - Page number. **currentPosition** - (any) - Current position. **previousPosition** - (any) - Previous position. **opacity** - (number) - Opacity. **strokeColor** - (string) - Stroke color. **thickness** - (number) - Thickness. **type** - (AnnotationType) - Type of signature.|
|**resourcesLoaded**|Triggers after PDFium resources are loaded.|**void**|No event arguments.|
|**signaturePropertiesChange**|Triggers when signature properties are changed.|**SignaturePropertiesChangeEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the signature. **pageIndex** - (number) - Page number. **type** - (AnnotationType) - Type of signature. **newValue** - (any) - New property value. **oldValue** - (any) - Old property value. **isOpacityChanged** - (boolean) - Whether opacity changed. **isStrokeColorChanged** - (boolean) - Whether stroke color changed. **isThicknessChanged** - (boolean) - Whether thickness changed.|
|**signatureSelect**|Triggers when a signature is selected.|**SignatureSelectEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the selected signature. **pageIndex** - (number) - Page number. **signature** - (object) - Properties of the selected signature.|
|**signatureUnselect**|Triggers when a signature is unselected.|**SignatureUnselectEventArgs**|**name** - (string) - Name of the event. **id** - (string) - Id of the unselected signature. **pageIndex** - (number) - Page number. **signature** - (object) - Properties of the unselected signature.|
|**textSearchComplete**|Triggers when a text search is completed.|**TextSearchCompleteEventArgs**|**name** - (string) - Name of the event. **searchText** - (string) - The searched text content. **matchCase** - (boolean) - Whether match case was used.|
|**textSearchHighlight**|Triggers when the searched text is highlighted.|**TextSearchHighlightEventArgs**|**name** - (string) - Name of the event. **searchText** - (string) - The searched text content. **matchCase** - (boolean) - Whether match case was used. **pageNumber** - (number) - Page number of highlighted text. **bounds** - (RectangleBoundsModel) - Bounds of the highlighted text.|
|**textSearchStart**|Triggers when a text search is initiated.|**TextSearchStartEventArgs**|**name** - (string) - Name of the event. **searchText** - (string) - The searched text content. **matchCase** - (boolean) - Whether match case is used.|
|**textSelectionEnd**|Triggers when text selection is complete.|**TextSelectionEndEventArgs**|**name** - (string) - Name of the event. **pageIndex** - (number) - Page number where selection ended. **textContent** - (string) - Selected text content. **textBounds** - (any) - Bounds of selected text.|
|**textSelectionStart**|Triggers when text selection is initiated.|**TextSelectionStartEventArgs**|**name** - (string) - Name of the event. **pageIndex** - (number) - Page number where selection started.|
|**thumbnailClick**|Triggers when a thumbnail is clicked.|**ThumbnailClickEventArgs**|**name** - (string) - Name of the event. **pageNumber** - (number) - Page number of the clicked thumbnail.|
|**toolbarClick**|Triggers when a toolbar item is clicked.|**ClickEventArgs**|**name** - (string) - Name of the event.|
|**validateFormFields**|Triggers when form field validation fails (e.g., before download/submit). Requires `enableFormFieldsValidation = true`.|**ValidateFormFieldsArgs**|**name** - (string) - Name of the event. **documentName** - (string) - Current document name. **formField** - (any) - Last interacted field's data (if applicable). **nonFillableFields** - (any) - Array detailing required/invalid fields.|
|**zoomChange**|Triggers when the magnification value changes.|**ZoomChangeEventArgs**|**name** - (string) - Name of the event. **zoomValue** - (number) - Current zoom percentage. **previousZoomValue** - (number) - Zoom value before change.|

---

## PdfKeys

| **Name** | **Description** |
|-----|-----|
|A|Represents the key value A when the A key is pressed in the Keyboard|
|ArrowDown|Represents the key value ArrowDown when the ArrowDown key is pressed in the Keyboard|
|ArrowLeft|Represents the key value ArrowLeft when the ArrowLeft key is pressed in the Keyboard|
|ArrowRight|Represents the key value ArrowRight when the ArrowRight key is pressed in the Keyboard|
|ArrowUp|Represents the key value ArrowUp when the ArrowUp key is pressed in the Keyboard|
|B|Represents the key value B when the B key is pressed in the Keyboard|
|BackSpace|Represents the key value BackSpace when the BackSpace key is pressed in the Keyboard|
|C|Represents the key value C when the C key is pressed in the Keyboard|
|D|Represents the key value D when the D key is pressed in the Keyboard|
|Delete|Represents the key value Delete when the Delete key is pressed in the Keyboard|
|E|Represents the key value E when the E key is pressed in the Keyboard|
|End|Represents the key value End when the End key is pressed in the Keyboard|
|Enter|Represents the key value Enter when the Enter key is pressed in the Keyboard|
|Escape|Represents the key value Escape when the Escape key is pressed in the Keyboard|
|F|Represents the key value F when the F key is pressed in the Keyboard|
|F1|Represents the key value F1 when the F1 key is pressed in the Keyboard|
|F2|Represents the key value F2 when the F2 key is pressed in the Keyboard|
|F3|Represents the key value F3 when the F3 key is pressed in the Keyboard|
|F4|Represents the key value F4 when the F4 key is pressed in the Keyboard|
|F5|Represents the key value F5 when the F5 key is pressed in the Keyboard|
|F6|Represents the key value F6 when the F6 key is pressed in the Keyboard|
|F7|Represents the key value F7 when the F7 key is pressed in the Keyboard|
|F8|Represents the key value F8 when the F8 key is pressed in the Keyboard|
|F9|Represents the key value F9 when the F9 key is pressed in the Keyboard|
|F10|Represents the key value F10 when the F10 key is pressed in the Keyboard|
|F11|Represents the key value F11 when the F11 key is pressed in the Keyboard|
|F12|Represents the key value F12 when the F12 key is pressed in the Keyboard|
|G|Represents the key value G when the G key is pressed in the Keyboard|
|H|Represents the key value H when the H key is pressed in the Keyboard|
|Home|Represents the key value Home when the Home key is pressed in the Keyboard|
|I|Represents the key value I when the I key is pressed in the Keyboard|
|J|Represents the key value J when the J key is pressed in the Keyboard|
|K|Represents the key value K when the K key is pressed in the Keyboard|
|L|Represents the key value L when the L key is pressed in the Keyboard|
|M|Represents the key value M when the M key is pressed in the Keyboard|
|Minus|Represents the key value Minus when the Minus key is pressed in the Keyboard|
|N|Represents the key value N when the N key is pressed in the Keyboard|
|None|Represents a null key value when no keys are pressed|
|Number0|Represents the key value 0 when the 0 key is pressed in the Keyboard|
|Number1|Represents the key value 1 when the 1 key is pressed in the Keyboard|
|Number2|Represents the key value 2 when the 2 key is pressed in the Keyboard|
|Number3|Represents the key value 3 when the 3 key is pressed in the Keyboard|
|Number4|Represents the key value 4 when the 4 key is pressed in the Keyboard|
|Number5|Represents the key value 5 when the 5 key is pressed in the Keyboard|
|Number6|Represents the key value 6 when the 6 key is pressed in the Keyboard|
|Number7|Represents the key value 7 when the 7 key is pressed in the Keyboard|
|Number8|Represents the key value 8 when the 8 key is pressed in the Keyboard|
|Number9|Represents the key value 9 when the 9 key is pressed in the Keyboard|
|O|Represents the key value O when the O key is pressed in the Keyboard|
|P|Represents the key value P when the P key is pressed in the Keyboard|
|PageDown|Sets the key value as PageDown when page down key is pressed|
|PageUp|Represents the key value PageUp when the PageUp key is pressed in the Keyboard|
|Plus|Represents the key value Plus when the Plus key is pressed in the Keyboard|
|Q|Represents the key value Q when the Q key is pressed in the Keyboard|
|R|Represents the key value R when the R key is pressed in the Keyboard|
|S|Represents the key value S when the S key is pressed in the Keyboard|
|Space|Represents the key value Space when the Space key is pressed in the Keyboard|
|Star|Represents the key value Star when the Star key is pressed in the Keyboard|
|T|Represents the key value T when the T key is pressed in the Keyboard|
|Tab|Represents the key value Tab when the Tab key is pressed in the Keyboard|
|U|Represents the key value U when the U key is pressed in the Keyboard|
|V|Represents the key value V when the V key is pressed in the Keyboard|
|W|Represents the key value W when the W key is pressed in the Keyboard|
|X|Represents the key value X when the X key is pressed in the Keyboard|
|Y|Represents the key value Y when the Y key is pressed in the Keyboard|
|Z|Represents the key value Z when the Z key is pressed in the Keyboard|

---

## ModifierKeys

| **Name** | **Description** |
|-----|-----|
|Alt|Represents the Alt key is pressed in the Keyboard|
|Control|Represents the Control key is pressed in the Keyboard|
|Meta|Represents the Meta key is pressed in the Keyboard|
|None|Represents no modifiers are pressed in the Keyboard|
|Shift|Represents the Shift key is pressed in the Keyboard|
