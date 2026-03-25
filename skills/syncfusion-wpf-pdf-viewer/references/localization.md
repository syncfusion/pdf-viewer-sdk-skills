# Localization in WPF Pdf Viewer
Localization in the Syncfusion WPF PdfViewer allows configuring all static text (tooltips, context menus, toolbar labels, dialog messages) to a specific language by adding `.resx` resource files to the application. To localize the viewer, create a `Resources` folder in your project (new or existing), add the default English `.resx` file, and then add a culture-specific `.resx` file with translated values for the same keys. Set `Thread.CurrentThread.CurrentUICulture` before `InitializeComponent()` to activate the desired language at runtime.

## Add a Resources Folder and Culture-Specific Resource Files to a New or Existing Project to Enable Localized Text in WPF PdfViewer

To localize the WPF PdfViewer, a `Resources` folder must exist in the project. If the project is newly created, add this folder manually. If the project already exists and does not have a `Resources` folder, add it in the same way. Inside this folder, place the default English resource file and a culture-specific resource file containing translated values for each key.

**Steps:**
1. In **Solution Explorer**, right-click the project → **Add** → **New Folder** → name it `Resources`.
2. Right-click the `Resources` folder → **Add** → **New Item** → select **Resources File**.
3. Name the default file `Syncfusion.PdfViewer.WPF.resx` and add it. This file holds the base (English) key-value pairs.
4. Add a second Resources File named `Syncfusion.PdfViewer.WPF.[Culture].resx` (e.g., `Syncfusion.PdfViewer.WPF.fr.resx` for French, `Syncfusion.PdfViewer.WPF.de.resx` for German).
5. In the culture-specific file, add the same resource keys as the default file but replace each value with the translated text for the target language.
6. Set the **Access Modifier** of both `.resx` files to **Public** in the resource editor.

### Placeholders
- Replace `[Culture]` with the target culture code (e.g., `fr` for French, `de` for German, `ja` for Japanese).

## Default English (en-US) Resource Keys and Values for Syncfusion WPF PdfViewer

The table below lists every localizable key used by the WPF PdfViewer along with its default English value. Copy these keys into your culture-specific `.resx` file and replace the values with translations for the target language.

| Key | Default Value (en-US) |
|---|---|
| `Accepted` | Accepted |
| `AddLayer` | Click to add a layer. |
| `AddReply` | Add Reply |
| `AddSignatureLabel` | Add signature |
| `AddStampMessage` | Click to add stamp |
| `AddStickyNote` | Add sticky note |
| `After` | After |
| `Annotations` | Show Annotations |
| `Appearance` | Appearance |
| `ApplyLabel` | Apply |
| `ApplyRedactionLabel` | Apply |
| `ApplyRedactionMessage` | Click to permanently remove marked content. |
| `Arrow` | Arrow |
| `Author` | Author |
| `BackgroundColor` | Background color |
| `Before` | Before |
| `BlankPageMessage` | Blank page |
| `BlankPageText` | Blank Page |
| `BookmarkNotExists` | This bookmark destination doesn't exist |
| `BookmarkTitle` | Bookmarks |
| `BorderColor` | Border color |
| `BorderStyle` | Border Style |
| `BorderThickness` | Border thickness |
| `BrowseButtonHeaderText` | Add Stamp |
| `Butt` | Butt |
| `Cancel` | Cancel |
| `Cancelled` | Cancelled |
| `ClearLabel` | Clear |
| `CloseAnnotationsToolbarMessage` | Click to close annotations toolbar. |
| `CloseBookmark` | Click to close the bookmark pane |
| `Closed` | Closed |
| `CloseFontPopUp` | Click to close the text properties |
| `CloseFormOptionsMessage` | Close form options |
| `CloseLayer` | Click to close the layer pane |
| `ClosePageOrganizerMessage` | Click to close organize pages pane. |
| `CloseRedactionMessage` | Close redact |
| `CloseSearchBar` | Close Search Bar |
| `CloseThumbnail` | Click to close the thumbnail pane |
| `Cloud` | Cloud |
| `Color` | Color |
| `ColorPicker` | Color picker |
| `Comment` | Comment |
| `Comments` | Comments |
| `CommentsPanel` | Comments Panel |
| `Completed` | Completed |
| `ConfirmationBeforeClose` | Do you want to save changes before closing? |
| `Copy` | Copy |
| `CounterclockwiseMessage` | Rotate counterclockwise |
| `CreateSignatureLabel` | Create signature |
| `CurrentPageNumber` | Current page index |
| `CustomStampHeaderText` | Custom Stamps |
| `CustomTextLabel` | Custom text |
| `CutMessage` | Cut |
| `DecreaseMagnification` | Click to decrease the magnification of the entire page. |
| `Delete` | Delete |
| `DeleteLayer` | Click to delete a layer |
| `DeletePagesConfirmation` | Are you sure you want to delete the pages from the document? |
| `DeletePagesLimitation` | You cannot delete all pages. At least one page should remain |
| `DeletePagesMesage` | Delete pages |
| `Diamond` | Diamond |
| `DocumentProtected` | This document is protected. Please enter a document open password. |
| `DrawCircle` | Circle |
| `DrawingTools` | Drawing Tools |
| `DrawInk` | Draw free form |
| `DrawLine` | Line |
| `DrawPolygon` | Polygon |
| `DrawPolyline` | Polyline |
| `DrawRectangle` | Rectangle |
| `DrawTextCallout` | Text Callout |
| `Edit` | Edit |
| `EnableMultiplePageSelection` | Enable multiple page selection |
| `End` | End |
| `EnlargePageThumbnails` | Enlarge page thumbnails |
| `EnterPassword` | Enter password |
| `Error` | Error |
| `EssentialPdfViewer` | Essential Pdf Viewer |
| `Export annotation to JSON file` | Export annotation to JSON file |
| `Export annotation to XFDF file` | Export annotation to XFDF file |
| `ExportDataMessage` | Export data from a Form file |
| `FileAlreadyOpenedInformation` | This file is already opened. Please close it before saving |
| `FilesViewMessage` | Click to open, save and print a PDF Document |
| `FileText` | File |
| `FillColor` | Fill color |
| `FillOpacityLabel` | Fill opacity |
| `FirstText` | First |
| `FitPage` | Fit to Page |
| `FitWidth` | Fit to Width |
| `FontColorLabel` | Font color |
| `FontLabel` | Font |
| `FontSizeLabel` | Font size |
| `FormDataLabel` | Form Data |
| `FormDataMessage` | Form Data |
| `FormExportLabel` | Export |
| `FormImportLabel` | Import |
| `FormNameRequestDialogTitle` | File Name |
| `FormNameRequestText` | Enter the name of the loaded PDF file |
| `FreeText` | Free Text |
| `FreeTextBox` | Add text box |
| `FreeTextProperties` | Free text properties |
| `FromFileMessage` | From file |
| `General` | General |
| `GoToFirstPage` | Click to go to first page in the document. |
| `GoToLastPage` | Click to go to last page in the document. |
| `GoToNextPage` | Click to go to next page in the document. |
| `GoToPreviousPage` | Click to go to previous page in the document. |
| `HandwrittenSignatureMessage` | Sign document by drawing a signature. |
| `HandwrittenSignaturePropertiesLabel` | Handwritten signature properties |
| `Help` | Help |
| `Highlight` | Highlight |
| `HighlightProperties` | Highlight properties |
| `HighlightText` | Highlight text |
| `Icon` | Icon |
| `Import annotation from JSON file` | Import annotation from JSON file |
| `Import annotation from XFDF file` | Import annotation from XFDF file |
| `ImportDataMessage` | Import data into a Form file |
| `IncorrectNumericEntry` | Invalid numeric value |
| `IncorrectPassword` | Incorrect password |
| `IncreaseMagnification` | Click to increase the magnification of the entire page. |
| `Information` | Information |
| `Ink` | Ink |
| `InkEraser` | Click to erase a part of the ink annotation (freehand drawings) |
| `InkProperties` | Ink properties |
| `InsertButtonText` | Insert |
| `InsertPageMessage` | Insert pages |
| `InsertPagesTitle` | Insert Pages |
| `InsertPdfTitle` | Select PDF to insert |
| `InsertText` | Insert Text |
| `InsertTextBlock` | Insert: |
| `InvalidPasswordError` | Password is invalid |
| `Key` | Key |
| `LastText` | Last |
| `LayerTitle` | Layers |
| `LineEnding` | Line Ending |
| `LineProperties` | Line properties |
| `LoadingPage` | Loading Pages |
| `LocationText` | Location |
| `Locked` | Locked |
| `MakeDefault` | Set as default |
| `MakePropertiesDefault` | Make Properties default |
| `MarkForRedactionLabel` | Mark for Redaction |
| `MarkForRedactionMessage` | Click to mark content for permanent removal. |
| `MarqueeZoom` | Zoom Select Area |
| `MatchCase` | Match Case |
| `Message` | Message |
| `Modified` | Modified |
| `MoreActions` | Click to view more actions |
| `NewParagraph` | New Paragraph |
| `Next` | Next |
| `NoMatchesFound` | Reader has finished searching the document. No matches were found |
| `NoMoreMatchesFound` | Reader has finished searching the document. No more matches were found |
| `None` | None |
| `Note` | Note |
| `Of` | of |
| `OfText` | of |
| `Ok` | OK |
| `Opacity` | Opacity |
| `Open` | Open |
| `OpenDocument` | Click to open a PDF Document |
| `OpenHeaderText` | Open |
| `OpenPopupNote` | Open Pop-up Note |
| `OutlineColorLabel` | Outline color |
| `Oval` | Oval |
| `OvalProperties` | Oval properties |
| `OverlayTextTitleLabel` | Overlay text |
| `Page` | Page |
| `PageCount` | Total page count |
| `PageGroupTitle` | Page |
| `PageNotExists` | There is no page numbered '{0}' in this document |
| `PageOrganizerTitle` | Organize Pages |
| `PageText` | Page: |
| `Panning` | Click to pan around the document |
| `Paragraph` | Paragraph |
| `PasswordCancelButton` | Cancel |
| `PasswordOkButton` | OK |
| `PasswordRequestDialogTitle` | Password |
| `PasteMessage` | Paste |
| `PolygonalLine` | Polygonal Line |
| `PolygonLineProperties` | Polygon line properties |
| `PolygonProperties` | Polygon properties |
| `Post` | Post |
| `Previous` | Previous |
| `PrintDocument` | Click to Print this PDF file or pages from it. |
| `PrintHeaderText` | Print |
| `Properties` | Properties |
| `RectangleProperties` | Rectangle properties |
| `RedactedAreaFillLabel` | Redacted area fill color |
| `RedactionConfirmation` | Are you sure you want to continue? |
| `RedactionLabel` | Redaction |
| `RedactionMarkAppearancelabel` | Redaction mark appearance |
| `RedactionMessage` | Click to perform redaction. |
| `RedactionPropertiesLabel` | Redaction tool properties |
| `RedactionPropertiesMessage` | Click to view redaction tool properties. |
| `RedactionWarning` | You are about to permanently remove all content that has been marked for redaction. Once the document is saved, this operation cannot be undone |
| `ReducePageThumbnails` | Reduce page thumbnails |
| `Rejected` | Rejected |
| `Rename` | Rename |
| `RequestCorrectPassword` | Please open the document again and enter the correct password |
| `ReversedClose` | Closed (Reverse) |
| `ReversedOpen` | Open (Reverse) |
| `RotateClockwiseMessage` | Rotate clockwise |
| `Round` | Round |
| `SaveAsDocument` | Click to save the document in the local disk |
| `SaveAsHeaderText` | Save As |
| `SaveDocument` | Click to save the document in the local disk |
| `SaveHeaderText` | Save |
| `SearchIndicator` | Searching |
| `SearchText` | Click to search text |
| `SelectionTool` | Selection tool for text |
| `SetStatus` | Set Status |
| `Slash` | Slash |
| `Square` | Square |
| `Squiggly` | Squiggly |
| `SquigglyProperties` | Squiggly Properties |
| `Stamp` | Stamp |
| `StampPropertiesLabel` | Stamp properties |
| `StandardLabel` | Standard Business |
| `Start` | Start |
| `StickyNote` | Sticky Note |
| `StickyNoteProperties` | Sticky note properties |
| `StrikeoutProperties` | Strikethrough properties |
| `StrikeoutText` | Strikethrough text |
| `Strikethrough` | Strikethrough |
| `Subject` | Subject |
| `TextCalloutProperties` | Text callout properties |
| `TextMarkupAnnotation` | Text Markup Annotation |
| `TextProperties` | Text properties |
| `Thickness` | Thickness |
| `ThumbnailTitle` | Page Thumbnails |
| `Underline` | Underline |
| `UnderlineProperties` | Underline properties |
| `UnderlineText` | Underline text |
| `UseOverlayTextLabel` | Use overlay text |
| `ValueExceedsLimit` | The value must be between {0} and {1} |
| `ViewBookmarks` | Click to view the bookmarks |
| `ViewLayers` | Click to view the layers |
| `ViewPageOrganizerMessage` | Rotate, rearrange, insert or delete pages |
| `ViewThumbnails` | Click to view the thumbnails |
| `Warning` | Warning |
| `ZoomLevel` | Current zoom level |

## Apply Localization by Setting the Thread UI Culture Before Initializing the Window in Code-Behind

Set `Thread.CurrentThread.CurrentUICulture` to the desired culture code before calling `InitializeComponent()`. This must be done before the window initializes so that the PdfViewer picks up the correct `.resx` file from the `Resources` folder. The culture-specific `.resx` file (e.g., `Syncfusion.PdfViewer.WPF.fr.resx`) must already be present in the `Resources` folder of the project with the translated key values.

```csharp
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("fr-FR");
        InitializeComponent();
        pdfViewer.Load(@"sample.pdf");
```

### Placeholders
- Replace `fr-FR` with the target culture code (e.g., `de-DE` for German, `ja-JP` for Japanese, `ar-SA` for Arabic).
- Replace `sample.pdf` with the actual PDF file path.

## Load Localized Resources from a Custom Assembly and Namespace Using LocalizationManager in Code-Behind

When the localization resource files are stored in a separate class library or a different assembly (not the main application project), use `LocalizationManager.SetResources` to point the PdfViewer to the correct assembly and namespace. Call this method after setting the UI culture and before `InitializeComponent()`. The `Resources` folder and the culture-specific `.resx` file must exist inside that external assembly under the specified namespace.

```csharp
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("fr-FR");

        // Set custom assembly and namespace for localization
        LocalizationManager.SetResources(typeof(CustomClass).Assembly, "ClassLibrary");
        InitializeComponent();
```

### Placeholders
- Replace `CustomClass` with any class that belongs to the assembly containing the resource files.
- Replace `ClassLibrary` with the root namespace of that assembly where the `Resources` folder is located.
- Replace `fr-FR` with the desired culture code.

## API Reference for All Localization Properties and Methods

| API | Type | Description |
|---|---|---|
| `Thread.CurrentThread.CurrentUICulture` | Property | Sets the culture used to look up localized resources. Must be set before `InitializeComponent()`. |
| `LocalizationManager.SetResources(assembly, namespace)` | Method | Registers a custom assembly and namespace for resource lookup when resource files are in a separate project. |
