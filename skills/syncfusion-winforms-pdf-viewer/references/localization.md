# Localization

Localization is the process of configuring the application to a specific language. PDF Viewer provides support to localize all the static text used for tooltip and context menu contents. Localization can be done by adding resource file (Resx) in the application.

## Default Localization Keys

The following table shows the default values for the common text used in the `PdfViewerControl` which is in `en-US` culture:

| Name | Value |
| --- | --- |
| Bookmarks | Bookmarks |
| Cancel | Cancel |
| CloseBookmarks | Click to close the bookmark pane |
| CloseSearchBar | Close search bar |
| CopyException | Copy exception detail to the clipboard |
| DocumentProtected | This document is password protected. Please enter a Document Open Password. |
| EnterPassword | Enter Password: |
| ErrorDocument | Essential PDF Viewer could not open the PDF document |
| EssentialPdfViewer | Essential Pdf Viewer |
| FitPage | Click to show one page at a time. |
| FitWidth | Click to fill the window with each page and scroll through pages continuously. |
| GoToFirstPage | Click to go to first page in the document. |
| GoToLastPage | Click to go to last page in the document. |
| GoToNextPage | Click to go to next page in the document. |
| GoToPreviousPage | Click to go to previous page in the document. |
| LoadingPage | Loading Page |
| LoadingSeparator | Of |
| Next | Next |
| NoMatches | Reader has finished searching the document. No more matches were found |
| Ok | Ok |
| OpenDocument | Click to open a PDF Document |
| Password | Password |
| Previous | Previous |
| PrintDocument | Click to Print this PDF file or pages from it. |
| SaveDocument | Click to save the document in the local disk |
| Searching | Searching |
| Separator | Of |
| ViewBookmarks | Click to view the bookmarks |
| Zoom | Zoom. |
| ZoomIn | Click to increase the magnification of the entire page. |
| ZoomOut | Click to decrease the magnification of the entire page. |

> Create a .resx file named Syncfusion.PdfViewer.Windows.[CultureName].resx that includes all the name–value pairs listed in the table for the corresponding culture. Add the generated .resx file to the Resources folder for reference.

## Adding Resource File

- Create a folder named `Resources` in your application.
- Add the default English (`en-US`) [Resx](https://github.com/syncfusion/winforms-controls-localization-resx-files/tree/master/Syncfusion.PdfViewer.Windows) file of `PdfViewerControl` in the `Resources` folder named as `Syncfusion.PdfViewer.Windows.resx`.
- Create a new Resx file named as `Syncfusion.PdfViewer.Windows.[Culture name].resx`. For example, `Syncfusion.PdfViewer.Windows.fr.resx` for French culture.
- Add the resource key (e.g., `OpenDocument`) and its corresponding localized value in the culture-specific Resx file.
- Execute the application in the target culture to see the changes.

## Localize Resource File with Different Assembly or Namespace

```csharp
Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("ar-AE");
Thread.CurrentThread.CurrentUICulture = new System.Globalization.CultureInfo("ar-AE");

// Set the custom assembly and namespace for the localization.
LocalizationManager.SetResources(typeof(Custom_Form).Assembly, "ClassLibrary");
InitializeComponent();
```
