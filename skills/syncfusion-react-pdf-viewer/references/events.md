# Events

Brief: The Syncfusion React PDFViewer component triggers multiple events that allow you to respond to user interactions and control the PDF viewing experience. These events include document loading, download, import/export, annotations, signatures, printing, form validation, text search, and page navigation.

### How to Use the Event in PDF Viewer

```typescript
const handleEventName = (args: EventArgs) => {
  // Event handling logic here
};

// Attach to PdfViewerComponent prop:
// eventName={handleEventName}
```

### List of Events

| **Event Name** | **Description** | **Args** | **Args Properties** |
|-----|-----|-----|------|
|**bookmarkClick**|Triggers when a bookmark item is clicked in the bookmark panel.|**BookmarkClickEventArgs**|**name** - (string) - The bookmark name that was clicked. **target** - (string) - The bookmark target/destination.|
|**buttonFieldClick**|Triggers when a button form field is clicked.|**ButtonFieldClickEventArgs**|**name** - (string) - The name of the button field. **pageNumber** - (number) - The page number where the button is located.|
|**commentAdd**|Triggers when a comment is added to the comment panel.|**CommentEventArgs**|**id** - (string) - The unique identifier of the comment. **pageIndex** - (number) - The page index where the comment was added. **annotationId** - (string) - The associated annotation ID.|
|**commentDelete**|Triggers when a comment is deleted from the comment panel.|**CommentEventArgs**|**id** - (string) - The unique identifier of the deleted comment. **pageIndex** - (number) - The page index of the deleted comment.|
|**commentEdit**|Triggers when a comment is edited in the comment panel.|**CommentEventArgs**|**id** - (string) - The unique identifier of the edited comment. **pageIndex** - (number) - The page index of the edited comment.|
|**commentSelect**|Triggers when a comment is selected in the comment panel.|**CommentEventArgs**|**id** - (string) - The unique identifier of the selected comment. **pageIndex** - (number) - The page index of the selected comment.|
|**commentStatusChanged**|Triggers when a comment's status changes in the comment panel.|**CommentEventArgs**|**id** - (string) - The comment identifier. **status** - (string) - The new status of the comment. **pageIndex** - (number) - The page index of the comment.|
|**created**|Triggers during the creation of the PDF Viewer component.|**void**|No Properties|
|**customContextMenuBeforeOpen**|Fires before the custom context menu opens.|**CustomContextMenuBeforeOpenEventArgs**|**name** - (string) - Event name. **ids** - (string[]) - Array of menu item ids that will be shown; remove ids to hide items for this open.|
|**customContextMenuSelect**|Fires when a custom context menu item is selected.|**CustomContextMenuSelectEventArgs**|**name** - (string) - Event name. **id** - (string) - The id of the clicked menu item.|
|**documentLoad**|Triggers while loading a document into the PDF Viewer.|**LoadEventArgs**|**documentName** - (string) - Name of the loaded document. **pageData** - (DocumentInfo) - Document information including page count and sizes. **pageData.pageCount** - (number) - Total page count of the document.|
|**documentLoadFailed**|Triggers when document loading fails.|**LoadFailedEventArgs**|**documentName** - (string) - Name of the document that failed to load. **error** - (string) - Error message describing the failure.|
|**documentUnload**|Triggers when the document is closed.|**UnloadEventArgs**|**documentName** - (string) - Name of the unloaded document.|
|**downloadEnd**|Triggers after a document is downloaded.|**DownloadEndEventArgs**|**fileName** - (string) - File name of the downloaded PDF document. **status** - (string) - Download completion status.|
|**downloadStart**|Triggers when the download action is initiated.|**DownloadStartEventArgs**|**fileName** - (string) - File name of the PDF document being downloaded.|
|**exportFailed**|Triggers when exporting annotations fails.|**ExportFailureEventArgs**|**name** - (string) - Event name. **errorDetails** - (string) - Details of the export failure.|
|**exportStart**|Triggers when exporting annotations starts.|**ExportStartEventArgs**|**fileName** - (string) - Name of the export file.|
|**exportSuccess**|Triggers when annotations are exported successfully.|**ExportSuccessEventArgs**|**fileName** - (string) - Name of the exported annotations file.|
|**extractTextCompleted**|Triggers when text extraction is completed.|**ExtractTextCompletedEventArgs**|**documentTextCollection** - (List<Dictionary>) - Returns the extracted text collection. **pageTextContent.pageText** - (string) - Extracted text from the page. **pageTextContent.pageSize** - (SizeF) - Dimensions of the page.|
|**hyperlinkClick**|Triggers when a hyperlink in the PDF document is clicked.|**HyperlinkClickEventArgs**|**hyperlink** - (string) - The URL of the clicked hyperlink. **target** - (string) - The target window/frame for the hyperlink.|
|**hyperlinkMouseOver**|Triggers when hovering over a hyperlink in the PDF document.|**HyperlinkMouseOverArgs**|**hyperlink** - (string) - The URL of the hovered hyperlink. **name** - (string) - Name associated with the hyperlink.|
|**importFailed**|Triggers when importing annotations fails.|**ImportFailureEventArgs**|**name** - (string) - Event name. **errorDetails** - (string) - Details of the import failure.|
|**importStart**|Triggers when importing annotations starts.|**ImportStartEventArgs**|**fileName** - (string) - Name of the import file.|
|**importSuccess**|Triggers when annotations are imported successfully.|**ImportSuccessEventArgs**|No Properties|
|**keyboardCustomCommands**|Triggers when customized keyboard command keys are pressed.|**KeyboardCustomCommandsEventArgs**|**name** - (string) - Event name. **keyboardCommand** - (object) - The command metadata raised by Command Manager. **keyboardCommand.name** - (string) - Name of the custom command.|
|**moveSignature**|Triggers when a signature is moved across the page.|**MoveSignatureEventArgs**|**id** - (string) - Signature identifier. **pageNumber** - (number) - Page number where signature was moved.|
|**pageChange**|Triggers when the current page number changes.|**PageChangeEventArgs**|**currentPageNumber** - (number) - Current page number. **previousPageNumber** - (number) - Previous page number before navigation.|
|**pageClick**|Triggers when a mouse click occurs on a page.|**PageClickEventArgs**|**pageNumber** - (number) - Page number where click occurred. **x** - (number) - X coordinate of the click. **y** - (number) - Y coordinate of the click.|
|**pageMouseover**|Triggers when moving the mouse over a page.|**PageMouseoverEventArgs**|**name** - (string) - Event name. **pageX** - (number) - Mouse X position relative to page. **pageY** - (number) - Mouse Y position relative to page.|
|**pageOrganizerSaveAs**|Triggers when a save as action is performed in the page organizer.|**PageOrganizerSaveAsEventArgs**|**downloadDocument** - (string) - Name of the document to be saved.|
|**pageRenderComplete**|Triggers after a page finishes rendering.|**PageRenderCompleteEventArgs**|**data** - (number) - Page number that completed rendering.|
|**pageRenderInitiate**|Triggers when page rendering begins.|**PageRenderInitiateEventArgs**|**jsonData** - (string) - JSON data for the page being rendered.|
|**printEnd**|Triggers when a print action is completed.|**PrintEndEventArgs**|**documentName** - (string) - Name of the printed document.|
|**printStart**|Triggers when a print action is initiated.|**PrintStartEventArgs**|**documentName** - (string) - Name of the document being printed.|
|**removeSignature**|Triggers when a signature is removed.|**RemoveSignatureEventArgs**|**bounds** - (object) - Bounds information of the removed signature. **id** - (string) - Signature identifier.|
|**resizeSignature**|Triggers when a signature is resized.|**ResizeSignatureEventArgs**|**currentPosition** - (object) - Current position and size of the resized signature. **id** - (string) - Signature identifier.|
|**resourcesLoaded**|Triggers after PDFium resources are loaded.|**void**|No Properties|
|**signaturePropertiesChange**|Triggers when signature properties are changed.|**SignaturePropertiesChangeEventArgs**|**type** - (string) - Type of property that changed. **id** - (string) - Signature identifier.|
|**signatureSelect**|Triggers when a signature is selected.|**SignatureSelectEventArgs**|**signature** - (object) - The selected signature object. **id** - (string) - Signature identifier.|
|**signatureUnselect**|Triggers when a signature is unselected.|**SignatureUnselectEventArgs**|**signature** - (object) - The unselected signature object. **id** - (string) - Signature identifier.|
|**textSearchComplete**|Triggers when a text search is completed.|**TextSearchCompleteEventArgs**|**searchText** - (string) - The text that was searched. **results** - (number) - Number of results found.|
|**textSearchHighlight**|Triggers when the searched text is highlighted.|**TextSearchHighlightEventArgs**|**bounds** - (object) - Bounds of the highlighted search result. **pageIndex** - (number) - Page index of the highlighted text.|
|**textSearchStart**|Triggers when a text search is initiated.|**TextSearchStartEventArgs**|**searchText** - (string) - The text being searched. **matchCase** - (boolean) - Whether search is case-sensitive.|
|**textSelectionEnd**|Triggers when text selection is complete.|**TextSelectionEndEventArgs**|**pageIndex** - (number) - Page index where text selection ended. **textContent** - (string) - The selected text content.|
|**textSelectionStart**|Triggers when text selection is initiated.|**TextSelectionStartEventArgs**|**pageIndex** - (number) - Page index where text selection started.|
|**thumbnailClick**|Triggers when a thumbnail is clicked in the thumbnail panel.|**ThumbnailClickEventArgs**|**pageNumber** - (number) - Page number of the clicked thumbnail.|
|**toolbarClick**|Triggers when a toolbar item is clicked.|**ClickEventArgs**|**name** - (string) - Name of the toolbar item clicked. **id** - (string) - Id of the toolbar item.|
|**validateFormFields**|Triggers when form field validation fails.|**ValidateFormFieldsArgs**|**name** - (string) - Event name. **documentName** - (string) - Name of the document. **formField** - (object) - The last interacted field's data. **nonFillableFields** - (array) - Array of required/invalid fields that failed validation.|
|**zoomChange**|Triggers when the magnification value changes.|**ZoomChangeEventArgs**|**zoomValue** - (number) - The new zoom percentage value. **previousZoomValue** - (number) - The previous zoom percentage value.|

---

## PdfKeys

|**Name**|**Description**|
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
|F10|Represents the key value F10 when the F10 key is pressed in the Keyboard|
|F11|Represents the key value F11 when the F11 key is pressed in the Keyboard|
|F12|Represents the key value F12 when the F12 key is pressed in the Keyboard|
|F2|Represents the key value F2 when the F2 key is pressed in the Keyboard|
|F3|Represents the key value F3 when the F3 key is pressed in the Keyboard|
|F4|Represents the key value F4 when the F4 key is pressed in the Keyboard|
|F5|Represents the key value F5 when the F5 key is pressed in the Keyboard|
|F6|Represents the key value F6 when the F6 key is pressed in the Keyboard|
|F7|Represents the key value F7 when the F7 key is pressed in the Keyboard|
|F8|Represents the key value F8 when the F8 key is pressed in the Keyboard|
|F9|Represents the key value F9 when the F9 key is pressed in the Keyboard|
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

## PdfModifierKeys

|**Name**|**Description**|
|-----|-----|
|Alt|Represents the Alt key is pressed in the Keyboard|
|Control|Represents the Control key is pressed in the Keyboard|
|Meta|Represents the Meta key is pressed in the Keyboard|
|None|Represents no modifiers are pressed in the Keyboard|
|Shift|Represents the Shift key is pressed in the Keyboard|


