# Migrate from Xamarin.Forms SfPdfViewer to .NET MAUI SfPdfViewer

**Xamarin Namespace:** `Syncfusion.SfPdfViewer.XForms` → **MAUI Namespace:** `Syncfusion.Maui.PdfViewer`

> **Breaking Changes:**
> - Search method is now async: `SearchText()` → `await SearchTextAsync()`
> - Multiple annotation events consolidated into single events (e.g., `InkAdded` + `ShapeAnnotationAdded` → `AnnotationAdded`)
> - Boolean inversion: `FormField.CanEdit = false` → `FormField.ReadOnly = true`
> - `ExportAsImageAsync()` removed — use the PDF to Image Converter library instead
> - `AnnotationSettings.HandwrittenSignature` removed — use `SignatureCreated` event

---

## Namespaces

| Xamarin SfPdfViewer | .NET MAUI SfPdfViewer |
|---|---|
| Syncfusion.SfPdfViewer.XForms | Syncfusion.Maui.PdfViewer |

## Properties

| Xamarin SfPdfViewer | .NET MAUI SfPdfViewer | Description |
|---|---|---|
| InputFileStream | DocumentSource | Load PDF from stream or byte array |
| ZoomPercentage | ZoomFactor | Set zoom level (1-4, default: 1) |
| MinimumZoomPercentage | MinZoomFactor | Minimum zoom factor (default: 0.25) |
| MaximumZoomPercentage | MaxZoomFactor | Maximum zoom factor (default: 4) |
| EnableScrollHead | ShowScrollHead | Show/hide scroll head |
| BookmarkPaneVisible | IsOutlineViewVisible | Show/hide outline view |
| EnableDocumentLinkAnnotation | EnableDocumentLinkNavigation | Enable TOC interaction |
| AllowHyperlinkNavigation | EnableHyperlinkNavigation | Enable hyperlink navigation |
| Bookmarks | DocumentOutline | Get document outline |
| IsTextSelectionEnabled | EnableTextSelection | Enable text selection |
| TextSelectionColor | HighlightColor | Selected text highlight color |
| CurrentInstanceColor | CurrentMatchHighlightColor | Current search match color |
| OtherInstanceColor | OtherMatchesHighlightColor | Other matches highlight color |
| AnnotationMode | AnnotationMode | Annotation type to draw |
| Annotations | Annotations | Get list of annotations |
| AnnotationSettings | AnnotationSettings | Default annotation settings |
| ClearAllAnnotationsCommand | RemoveAllAnnotationsCommand | Remove all annotations command |
| PerformUndoCommand | UndoCommand | Undo command |
| PerformRedoCommand | RedoCommand | Redo command |
| InkPointsCollection | PointsCollection | Ink annotation points |
| InkAnnotationSettings.Thickness | InkAnnotationSettings.BorderWidth | Ink border thickness |
| ShapeAnnotationSettings.Thickness | ShapeAnnotationSettings.BorderWidth | Shape border thickness |
| InkAnnotationSettings.EnableSeparateAttributesForEachStroke | InkAnnotationSettings.AggregateInkStrokes | Treat each stroke separately |
| ShapeAnnotationSettings.StrokeColor | ShapeAnnotationSettings.Color | Shape stroke color |
| SelectorSettings.StrokeColor | AnnotationSelectorSettings.Color | Selector color |
| LockedStrokeColor | LockedColor | Locked annotation selector color |
| LinePoints | LineAnnotation.Points | Line annotation coordinates |
| Rectangle | ShapeAnnotationSettings.Square | Square annotation settings |
| Circle | AnnotationSettings.Circle | Circle annotation settings |
| Line | AnnotationSettings.Line | Line annotation settings |
| Arrow | AnnotationSettings.Arrow | Arrow annotation settings |
| Ink | AnnotationSettings.Ink | Ink annotation settings |
| Stamp | AnnotationSettings.Stamp | Stamp annotation settings |
| AnnotationMode.HandwrittenSignature | AnnotationMode.Signature | Signature dialog |
| Selector | AnnotationSettings.Selector | Selector settings |
| FormField.CanEdit | FormField.ReadOnly | Set form field editable |
| SignatureFormField.HandwrittenSignature | SignatureFormField.Signature | Signature in field |
| PageViewMode | PageLayoutMode | Page display layout |
| InkAnnotationSettings.TouchMode | InkAnnotationSettings.TouchScreenInputMode | Ink input mode |
| TouchMode.Direct | TouchScreenInputMode.FingerAndStylus | Finger and stylus input |
| IsToolbarVisible | ShowToolbars | Show/hide toolbars |
| AnnotationSettings.HandwrittenSignature | API Unavailable | Use SignatureCreated event |

## Events

| Xamarin SfPdfViewer | .NET MAUI SfPdfViewer | Description |
|---|---|---|
| UnhandledConditionOccurred | DocumentLoadFailed | PDF load failed |
| SearchInitiated, SearchCompleted | TextSearchProgress | Text search in progress |
| TextSelectionCompleted | TextSelectionChanged | Text selection changed |
| InkAdded, ShapeAnnotationAdded, StampAnnotationAdded, PopupAnnotationAdded, FreeTextAnnotationAdded, TextMarkupAdded | AnnotationAdded | Annotation added |
| InkDeselected, ShapeAnnotationDeselected, StampAnnotationDeselected, PopupAnnotationDeselected, FreeTextAnnotationDeselected, TextMarkupDeselected | AnnotationDeselected | Annotation deselected |
| InkEdited, ShapeAnnotationEdited, StampAnnotationMovedOrResized, PopupAnnotationEdited, FreeTextAnnotationEdited, TextMarkupEdited | AnnotationEdited | Annotation edited |
| InkRemoved, ShapeAnnotationRemoved, StampAnnotationRemoved, PopupAnnotationRemoved, FreeTextAnnotationRemoved, TextMarkupRemoved | AnnotationRemoved | Annotation removed |
| InkSelected, ShapeAnnotationSelected, StampAnnotationSelected, PopupAnnotationSelected, FreeTextAnnotationSelected, TextMarkupSelected | AnnotationSelected | Annotation selected |
| PageChanged | PropertyChanged | Property modified |
| DocumentSaveInitiated | API Unavailable | Use SaveDocument method |
| CanUndoModified, CanRedoModified, CanRedoInkModified, CanUndoInkModified | API Unavailable | Use annotation/form events |

## Methods

| Xamarin SfPdfViewer | .NET MAUI SfPdfViewer | Description |
|---|---|---|
| Unload | UnloadDocument | Unload PDF document |
| GoToBookmark | GoToOutlineElement | Go to outline element |
| SearchText | SearchTextAsync | Search text asynchronously |
| CancelSearch | Clear | Clear search and highlights |
| SearchNext | GoToNextMatch | Next search match |
| SearchPrevious | GoToPreviousMatch | Previous search match |
| ClearAllAnnotations | RemoveAllAnnotations | Remove all annotations |
| AddAnnotation, AddStamp | AddAnnotation | Add annotation |
| DeselectAnnotation | DeselectAnnotation | Deselect annotation |
| ExportAnnotations | ExportAnnotations | Export annotations |
| ExportAnnotationsAsync | ExportAnnotationsAsync | Export annotations async |
| ImportAnnotations | ImportAnnotations | Import annotations |
| RemoveAnnotation | RemoveAnnotation | Remove annotation |
| SaveDocument | SaveDocument | Save PDF document |
| SaveDocumentAsync | SaveDocumentAsync | Save PDF async |
| SelectAnnotation | SelectAnnotation | Select annotation |
| Print | PrintDocument | Print PDF |
| SaveDocument(bool flattenForm) | FormField.FlattenOnSave | Flatten form fields on save |
| ExportAsImageAsync | API Unavailable | Use PDF to Image Converter |

## Classes

| Xamarin SfPdfViewer | .NET MAUI SfPdfViewer | Description |
|---|---|---|
| CustomBookmark | Bookmark | Custom bookmark class |
| TouchMode | TouchScreenInputMode | Input mode enumeration |
| TextSelectionCompletedEventArgs | TextSelectionChangedEventArgs | Text selection event args |
| UnhandledConditionEventArgs | DocumentLoadFailedEventArgs | Load failed event args |
| TextMarkupAnnotation | HighlightAnnotation, SquigglyAnnotation, StrikeOutAnnotation, UnderlineAnnotation | Text markup annotations |
| ShapeAnnotation | CircleAnnotation, LineAnnotation, SquareAnnotation | Shape annotations |
| PopupAnnotation | StickyNoteAnnotation | Sticky note annotation |
| AnnotationMovedOrResizedEventArgs, InkAddedEventArgs, InkDeselectedEventArgs, InkEditedEventArgs, InkRemovedEventArgs, InkSelectedEventArgs, ShapeAnnotationAddedEventArgs, ShapeAnnotationDeselectedEventArgs, ShapeAnnotationEditedEventArgs, ShapeAnnotationRemovedEventArgs, ShapeAnnotationSelectedEventArgs, StampAnnotationAddedEventArgs, StampAnnotationDeselectedEventArgs, StampAnnotationMovedOrResizedEventArgs, StampAnnotationRemovedEventArgs, StampAnnotationSelectedEventArgs, TextMarkupAddedEventArgs, TextMarkupDeselectedEventArgs, TextMarkupEditedEventArgs, TextMarkupRemovedEventArgs | AnnotationEventArgs | Annotation event args |


