---
name: syncfusion-uwp-pdf-viewer
description: Implements Syncfusion UWP SfPdfViewerControl for native Windows PDF viewing, page navigation, annotations, text search/selection, ink signatures, printing, bookmark/hyperlink navigation, and toolbar/UI customization. Use when working with PDF viewer setup, document loading, annotations workflows in UWP apps.
metadata:
  author: "Syncfusion Inc"
  version: "33.1.44"
---

# Implementing UWP PDF Viewer (SfPdfViewerControl)

The Syncfusion `SfPdfViewerControl` is a native UWP control for viewing, annotating, searching, and printing PDF documents. It uses the Windows rendering engine (`Windows.Data.Pdf`) by default and supports an optional PDFium renderer.

## When to Use This Skill

Use this skill when you need to:
- View and navigate PDF documents in UWP applications
- Load PDFs from streams, StorageFile objects, or byte arrays
- Add and manage annotations (highlight, underline, strikethrough, ink, shapes, free text, popup, stamp)
- Search and select text within PDF documents
- Navigate pages, bookmarks, and hyperlinks
- Print PDF documents with custom quality and preview settings
- Create custom toolbars wired to PDF Viewer commands
- Configure zoom, view modes, scrollbar, and progress ring
- Localize the viewer UI
- Export PDF pages as images or use the PDFium custom renderer

## Component Overview

**SfPdfViewerControl** is a comprehensive PDF viewing and management control for UWP with these capabilities:

- **Document Management:** Load from PdfLoadedDocument, Stream, or StorageFile (sync and async with CancellationToken); save with annotations; unload and dispose
- **Annotations:** Text markup (highlight, underline, strikethrough), shape (rectangle, ellipse, line), ink with Windows Ink Canvas support, popup (sticky note), free text, free text callout, and custom stamp annotations
- **Text Operation:** Text selection with color customization, synchronous and asynchronous text search with next/previous navigation
- **Navigation & UI:** Page navigation commands, bookmarks, hyperlink handling, zoom/view modes, thumbnail view, separate desktop and mobile toolbar layouts, scrollbar and progress ring customization
- **Utilities & Advanced:** Export pages as images (GetPage, GetPages, ExportAsImage), vertical/horizontal offset access, PDFium custom renderer via IPdfRenderer interface, page number display

## Documentation and Navigation Guide

### Getting Started & Setup
📄 **Read:** [references/getting-started.md](references/getting-started.md)
- Covers required assemblies, NuGet packages, adding the control via XAML or code, ItemsSource binding, and the DocumentLoaded event
- Explains synchronous and asynchronous loading methods, page count access, saving (Save/SaveAsync), unloading, and disposing

### Document Operations
📄 **Read:** [references/viewing-pdf.md](references/viewing-pdf.md)
- Describes loading PDFs from PdfLoadedDocument, Stream, and StorageFile objects using both sync and async approaches
- Covers CancellationToken support for async loading, saving with annotations, and viewer unload/dispose patterns

### Page Navigation & Viewing
📄 **Read:** [references/page-navigation.md](references/page-navigation.md)
- Explains programmatic page navigation, built-in navigation commands (FirstPage, LastPage, NextPage, PreviousPage), and XAML command binding
- Covers the PageChanged event, page count, page gap, offset collection, and toggling the page number display

### Magnification & View Modes
📄 **Read:** [references/magnification.md](references/magnification.md)
- Covers zoom control via ZoomTo, increase/decrease zoom commands, and view mode options (FitWidth, Normal, OnePage)
- Explains MinimumZoomPercentage, thumbnail view toggle, and reading the current zoom value

### Text Search
📄 **Read:** [references/text-operations.md](references/text-operations.md)
- Explains synchronous and asynchronous text search, forward/backward result navigation, and SearchNextCommand/SearchPreviousCommand
- Covers GetTextCoordinates for retrieving the page positions of all text matches

### Text Selection
📄 **Read:** [references/text-operations.md](references/text-operations.md)
- Describes enabling text selection, customizing the selection highlight color, and the TextSelectionCompleted event
- Covers copying selected text to the clipboard

### Annotations
📄 **Read:** [references/annotations.md](references/annotations.md)
- Covers all supported annotation types: text markup (highlight, underline, strikethrough), shapes (rectangle, ellipse, line), ink with Windows Ink Canvas, popup, free text, free text callout, and custom stamps
- Explains annotation events (Added, Tapped, Selected, Removed, MovedOrResized), deleting annotations, AnnotationCollection, undo/redo, and the IsDocumentEdited property

### Printing
📄 **Read:** [references/printing.md](references/printing.md)
- Explains the Print method, PrintCommand, and async printing with CancellationToken support
- Covers QualityFactor, customizing or disabling the print preview dialog, and setting the document name via PrinterSettings

### Bookmarks & Hyperlinks
📄 **Read:** [references/bookmarks-and-hyperlinks.md](references/bookmarks-and-hyperlinks.md)
- Explains navigating to bookmarks via GoToBookmark and retrieving the bookmark collection from PdfLoadedDocument
- Covers AllowHyperlinkNavigation, hyperlink pointer events, HyperlinkEventArgs properties, and restricting navigation

### Localization
📄 **Read:** [references/localization.md](references/localization.md)
- Covers setting the default language in the app manifest and adding .resw resource files for UI string localization
- Explains supported resource file names and changing the context menu language

### Gesture Events & Interaction
📄 **Read:** [references/utilities.md](references/utilities.md)
- Covers pointer events on hyperlinks (HyperlinkPointerPressed, HyperlinkPointerMoved) for custom interaction handling
- Explains using the PageChanged and DocumentLoaded events to drive post-navigation and post-load workflows

### Utilities & Advanced
📄 **Read:** [references/utilities.md](references/utilities.md)
- Covers exporting PDF pages as BitmapImage objects (GetPage, GetPages) and as image streams (ExportAsImage)
- Explains accessing vertical/horizontal scroll offsets, using the PDFium custom renderer via IPdfRenderer, and the ShowPageNumber and VerticalScrollBarWidth properties
