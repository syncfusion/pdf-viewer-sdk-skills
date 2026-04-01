# Events

Brief: The Syncfusion Vue PDF Viewer surfaces lifecycle, navigation, collaboration, signature, and text events so your Vue components can coordinate UI, analytics, and synchronization flows without resorting to DOM hacks.

## Wiring events in Vue

Attach handlers directly on `<ejs-pdfviewer>` using Vue's event syntax. Every PDF Viewer event listed below keeps its camelCase name.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :serviceUrl="serviceUrl"
    :documentPath="documentPath"
    @documentLoad="onDocumentLoad"
    @commentAdd="onCommentAdd"
    @downloadStart="onDownloadStart"
  />
</template>

<script setup>
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer'
const documentPath = 'PDF_Succinctly.pdf'

const onDocumentLoad = (args) => {
  console.log('pages ready', args.pageData.pageCount)
}

const onCommentAdd = (args) => {
  console.log('comment added', args.id, args.annotationId)
}

const onDownloadStart = (args) => {
  // push analytics, disable buttons, etc.
  console.log('download starting for', args.fileName)
}
</script>
```

Each handler receives an `args` object documented per event below. Use the same pattern inside the Composition API or Options API.

---

## Event reference (Vue)

Events are grouped for faster scanning. Every event name from the React reference is available on Vue; descriptions and property hints below are reworded for this platform.

### Viewer lifecycle

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**created**|Raised once the PDF Viewer instance finishes instantiating.|`void`|No payload; ideal for grabbing refs or wiring services.|
|**resourcesLoaded**|Emitted after internal PDFium assets download and initialize.|`void`|No payload; indicates that rendering resources are ready.|

### Document load and teardown

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**documentLoad**|Fires after a PDF is successfully loaded into the viewer.|`LoadEventArgs`|`documentName` – file being opened.<br>`pageData` – includes `pageCount` plus size data.|
|**documentLoadFailed**|Runs if loading a document throws an error.|`LoadFailedEventArgs`|`documentName` – requested file.<br>`error` – descriptive failure text.|
|**documentUnload**|Emitted when the current document is closed/unloaded.|`UnloadEventArgs`|`documentName` – file that was just closed.|

### Bookmark, navigation, and rendering

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**bookmarkClick**|Raised when the user activates a bookmark entry from the bookmark panel.|`BookmarkClickEventArgs`|`name` – bookmark caption.<br>`target` – destination within the document.|
|**pageChange**|Runs every time the current page number changes.|`PageChangeEventArgs`|`currentPageNumber` – page after navigation.<br>`previousPageNumber` – page before navigation.|
|**pageClick**|Triggered for mouse clicks directly on a rendered page.|`PageClickEventArgs`|`pageNumber` – page that was clicked.<br>`x`, `y` – click coordinates inside the page.|
|**pageMouseover**|Emitted while the pointer moves over a page surface.|`PageMouseoverEventArgs`|`name` – event label.<br>`pageX`, `pageY` – pointer coordinates relative to the page.|
|**thumbnailClick**|Raised when a thumbnail item in the thumbnail pane is chosen.|`ThumbnailClickEventArgs`|`pageNumber` – page represented by the thumbnail.|
|**pageRenderInitiate**|Published right before a page begins rendering.|`PageRenderInitiateEventArgs`|`jsonData` – serialized data for the page being rendered.|
|**pageRenderComplete**|Runs after a page finishes rendering.|`PageRenderCompleteEventArgs`|`data` – the page number that just completed rendering.|
|**pageOrganizerSaveAs**|Fires when users save a document from the Page Organizer UI.|`PageOrganizerSaveAsEventArgs`|`downloadDocument` – output document name.|
|**zoomChange**|Raised whenever the magnification factor changes.|`ZoomChangeEventArgs`|`zoomValue` – new zoom percentage.<br>`previousZoomValue` – zoom before the change.|

### Downloading and printing

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**downloadStart**|Triggered as soon as the download workflow begins.|`DownloadStartEventArgs`|`fileName` – target download name.|
|**downloadEnd**|Raised when the download request completes.|`DownloadEndEventArgs`|`fileName` – downloaded file.<br>`status` – success/failure text.|
|**printStart**|Runs when print preparation starts.|`PrintStartEventArgs`|`documentName` – file sent to print.|
|**printEnd**|Emitted after the print action finishes.|`PrintEndEventArgs`|`documentName` – file that finished printing.|

### Import, export, and extraction

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**importStart**|Raised when annotation import begins.|`ImportStartEventArgs`|`fileName` – source XFDF / JSON file.|
|**importSuccess**|Emitted after annotations import correctly.|`ImportSuccessEventArgs`|No additional fields; treat the event itself as confirmation.|
|**importFailed**|Runs if annotation import fails.|`ImportFailureEventArgs`|`name` – event identifier.<br>`errorDetails` – reason for failure.|
|**exportStart**|Fires when annotation export begins.|`ExportStartEventArgs`|`fileName` – name assigned to the export.|
|**exportSuccess**|Raised after annotations export successfully.|`ExportSuccessEventArgs`|`fileName` – generated file name.|
|**exportFailed**|Runs if annotation export fails.|`ExportFailureEventArgs`|`name` – event identifier.<br>`errorDetails` – diagnostic text.|
|**extractTextCompleted**|Emitted when text extraction finishes.|`ExtractTextCompletedEventArgs`|`documentTextCollection` – page-wise text map.<br>`pageTextContent.pageText` – text chunk.<br>`pageTextContent.pageSize` – size of the page.|

### Hyperlinks, search, and selection

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**hyperlinkClick**|Raised when a document hyperlink is clicked.|`HyperlinkClickEventArgs`|`hyperlink` – URL that was clicked.<br>`target` – window/frame target.|
|**hyperlinkMouseOver**|Runs while hovering on a hyperlink.|`HyperlinkMouseOverArgs`|`hyperlink` – URL under the pointer.<br>`name` – hyperlink label.|
|**textSearchStart**|Emitted when text search starts (Find dialog or API).|`TextSearchStartEventArgs`|`searchText` – term being searched.<br>`matchCase` – boolean for case sensitivity.|
|**textSearchHighlight**|Raised for every match highlight.|`TextSearchHighlightEventArgs`|`bounds` – highlighted rectangle info.<br>`pageIndex` – page containing the match.|
|**textSearchComplete**|Runs after search completes.|`TextSearchCompleteEventArgs`|`searchText` – term that was searched.<br>`results` – number of matches.|
|**textSelectionStart**|Fires when a text selection begins.|`TextSelectionStartEventArgs`|`pageIndex` – page where selection started.|
|**textSelectionEnd**|Raised when text selection is finalized.|`TextSelectionEndEventArgs`|`pageIndex` – page containing the selection end.<br>`textContent` – selected text.|

### Comments and review panel

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**commentAdd**|Runs when a comment gets added to the comments pane.|`CommentEventArgs`|`id` – unique comment id.<br>`pageIndex` – page of the comment.<br>`annotationId` – related annotation.|
|**commentDelete**|Raised when a comment is removed.|`CommentEventArgs`|`id` – removed comment id.<br>`pageIndex` – page that lost the comment.|
|**commentEdit**|Emitted when a comment is edited.|`CommentEventArgs`|`id` – comment id.<br>`pageIndex` – origin page.|
|**commentSelect**|Runs when a comment becomes selected.|`CommentEventArgs`|`id` – selected comment id.<br>`pageIndex` – page reference.|
|**commentStatusChanged**|Raised when a comment status value changes.|`CommentEventArgs`|`id` – comment id.<br>`status` – new status string.<br>`pageIndex` – related page.|

### Form fields and validation

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**buttonFieldClick**|Fires when a button form field is clicked.|`ButtonFieldClickEventArgs`|`name` – form field name.<br>`pageNumber` – page containing the button.|
|**validateFormFields**|Raised when required fields fail validation.|`ValidateFormFieldsArgs`|`name` – event id.<br>`documentName` – PDF name.<br>`formField` – last interacted field data.<br>`nonFillableFields` – array of missing/invalid fields.|

### Custom menus, toolbar, and keyboard

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**customContextMenuBeforeOpen**|Runs before the custom context menu shows.|`CustomContextMenuBeforeOpenEventArgs`|`name` – event id.<br>`ids` – string array of menu items that will show (you can splice to hide).|
|**customContextMenuSelect**|Raised when an item inside the custom context menu is chosen.|`CustomContextMenuSelectEventArgs`|`name` – event id.<br>`id` – clicked menu item id.|
|**toolbarClick**|Emitted for toolbar interactions.|`ClickEventArgs`|`name` – toolbar command name.<br>`id` – DOM id of the toolbar button.|
|**keyboardCustomCommands**|Runs whenever a registered keyboard shortcut fires.|`KeyboardCustomCommandsEventArgs`|`name` – event id.<br>`keyboardCommand` – metadata for the custom command.<br>`keyboardCommand.name` – shortcut name.|

### Signatures and ink objects

| Event | When it happens | Args | Useful data |
|-----|-----|-----|-----|
|**moveSignature**|Raised when a signature is moved across a page.|`MoveSignatureEventArgs`|`id` – signature id.<br>`pageNumber` – page where it moved.|
|**removeSignature**|Runs when a signature is deleted.|`RemoveSignatureEventArgs`|`bounds` – previously occupied bounds.<br>`id` – signature id.|
|**resizeSignature**|Emitted after a signature is resized.|`ResizeSignatureEventArgs`|`currentPosition` – latest size/position.<br>`id` – signature id.|
|**signaturePropertiesChange**|Runs when signature properties change.|`SignaturePropertiesChangeEventArgs`|`type` – property that changed.<br>`id` – signature id.|
|**signatureSelect**|Raised when a signature becomes selected.|`SignatureSelectEventArgs`|`signature` – selected signature object.<br>`id` – signature id.|
|**signatureUnselect**|Emitted when a signature loses selection.|`SignatureUnselectEventArgs`|`signature` – unselected signature object.<br>`id` – signature id.|

---

## PdfKeys

These constant names describe which keyboard key triggered `keyboardCustomCommands`. Use them when mapping command metadata.

| Name | Description |
|-----|-----|
|A|Represents the "A" key when pressed.|
|ArrowDown|Represents the Arrow Down key press.|
|ArrowLeft|Represents the Arrow Left key press.|
|ArrowRight|Represents the Arrow Right key press.|
|ArrowUp|Represents the Arrow Up key press.|
|B|Represents the "B" key input.|
|BackSpace|Represents the Backspace key input.|
|C|Represents the "C" key input.|
|D|Represents the "D" key input.|
|Delete|Represents the Delete key input.|
|E|Represents the "E" key input.|
|End|Represents the End key input.|
|Enter|Represents the Enter/Return key input.|
|Escape|Represents the Escape key input.|
|F|Represents the "F" key input.|
|F1|Represents the F1 function key.|
|F10|Represents the F10 function key.|
|F11|Represents the F11 function key.|
|F12|Represents the F12 function key.|
|F2|Represents the F2 function key.|
|F3|Represents the F3 function key.|
|F4|Represents the F4 function key.|
|F5|Represents the F5 function key.|
|F6|Represents the F6 function key.|
|F7|Represents the F7 function key.|
|F8|Represents the F8 function key.|
|F9|Represents the F9 function key.|
|G|Represents the "G" key input.|
|H|Represents the "H" key input.|
|Home|Represents the Home key input.|
|I|Represents the "I" key input.|
|J|Represents the "J" key input.|
|K|Represents the "K" key input.|
|L|Represents the "L" key input.|
|M|Represents the "M" key input.|
|Minus|Represents the Minus/Hyphen key input.|
|N|Represents the "N" key input.|
|None|Represents the absence of any key value.|
|Number0|Represents the numeric 0 key.|
|Number1|Represents the numeric 1 key.|
|Number2|Represents the numeric 2 key.|
|Number3|Represents the numeric 3 key.|
|Number4|Represents the numeric 4 key.|
|Number5|Represents the numeric 5 key.|
|Number6|Represents the numeric 6 key.|
|Number7|Represents the numeric 7 key.|
|Number8|Represents the numeric 8 key.|
|Number9|Represents the numeric 9 key.|
|O|Represents the "O" key input.|
|P|Represents the "P" key input.|
|PageDown|Represents the Page Down key input.|
|PageUp|Represents the Page Up key input.|
|Plus|Represents the Plus/Equals key input.|
|Q|Represents the "Q" key input.|
|R|Represents the "R" key input.|
|S|Represents the "S" key input.|
|Space|Represents the Spacebar key input.|
|Star|Represents the Asterisk key input.|
|T|Represents the "T" key input.|
|Tab|Represents the Tab key input.|
|U|Represents the "U" key input.|
|V|Represents the "V" key input.|
|W|Represents the "W" key input.|
|X|Represents the "X" key input.|
|Y|Represents the "Y" key input.|
|Z|Represents the "Z" key input.|

## PdfModifierKeys

| Name | Description |
|-----|-----|
|Alt|Indicates the Alt modifier key is held down.|
|Control|Indicates the Control modifier key is held down.|
|Meta|Indicates the Meta/Command key is held down.|
|None|Indicates no modifier keys are pressed.|
|Shift|Indicates the Shift modifier key is held down.|
