---
name: syncfusion-winforms-pdf-viewer
description: Create WinForms applications featuring the Syncfusion WinForms PDF Viewer, customized to meet specific user requirements. It supports essential PDF operations such as loading, saving, printing, text search, text extraction, and bookmark or hyperlink navigation. Additional capabilities include zooming, interaction modes, localization, theming, rendering engine selection, and robust error handling, enabling the creation of tailored and fully functional PDF viewing solutions.
compatibility: Requires .NET Framework 4.5+ or .NET Core/NET 8+ and Syncfusion.PdfViewer.Windows.
metadata:
  author: Syncfusion Inc
  version: "33.1.44"
---

# Syncfusion WinForms PdfViewer - UI Sample generator

## Generate C# Code for the User's Project *(default)*

**Trigger keywords:** "code", "snippet", "how to write", "Program.cs", "show me", "sample", "integrate", "example code", "generate code for", "create sample", "winforms pdfviewer".

**Purpose:** Generate clean, ready-to-use C# code snippets that directly insert into their WinForms application when working with Syncfusion WinForms PdfViewer control.

**Workflow:**
1. Build the C# code using the snippets provided in the references/*.md files.
2. Before generating the sample, ask the user whether the code should be:Integrated into an existing WinForms project, or
Created as a new WinForms application.
3. If the user chooses to create a new WinForms project, ask them which target framework they want to use:
   -.NET Framework (e.g., 4.6, 4.7, 4.8) — uses Syncfusion.PdfViewer.WinForms and targets the classic .NET Framework.
   -.NET / .NET Core (e.g., .NET 8, .NET 10) — uses Syncfusion.PdfViewer.WinForms with <TargetFramework>net8.0-windows</TargetFramework> (or the selected version).
4. Based on the user's choice:
Generate the .csproj file with the correct <TargetFramework> value.
Add the required NuGet packages.
Tailor any framework-specific code, such as namespace imports, form initialization, startup code (Program.cs), and PDF Viewer setup, accordingly.
5. Add only the APIs required to satisfy the user's requested functionality. Do not include optional APIs, additional.
---

## Code References

All templates and snippets are in the `references/` folder. Each file is a focused snippet or template the agent will combine when generating sample:

| File | Contents |
|---|---|
| **view-pdfviewer.md** | NuGet setup, add PdfViewerControl/PdfDocumentView, load PDF |
| **saving-pdf-files.md** | Save PDF via toolbar, programmatic save using `LoadedDocument.Save()`, `BeginSave` and `EndSave` events |
| **printing-pdf-files.md** | Print PDF via toolbar, silent printing using `Print()`, customize print size (`ActualSize`, `Fit`, `CustomScale`), print orientation (`Auto`, `Portrait`, `Landscape`), hide print status dialog, `BeginPrint`, `PrintProgress`, and `EndPrint` events |
| **extract-text.md** | Extract text from a single page using `ExtractText(pageIndex, out textLines)`, extract text from entire file using `PageCount` loop, extract text with line bounds via `TextLines`/`TextLine`, extract words with bounds via `WordCollection`/`TextWord` |
| **pdf-rendering-engines.md** | Switch rendering engine using `RenderingEngine` property (`PDFium` default, `SfPdf` alternative), set custom PDFium binary path via `ReferencePath` for restricted-access environments |
| **searching-text.md** | Search next/previous text instance using `SearchNextText()`/`SearchPreviousText()`, find all instances with bounds using `FindText()`, count total matches, enable/disable highlight all instances via `TextSearchSettings.HighlightAllInstance`, customize highlight colors via `TextSearchSettings.CurrentInstanceColor`/`OtherInstanceColor` |
| **navigation.md** | Bookmark navigation, hyperlink handling, and page navigation (programmatic `GoToBookmark()`, `HyperlinkClicked`/`HyperlinkMouseOver`, `GoToPageAtIndex()`) |
| **localization.md** | Localize tooltip and context menu static text, default `en-US` localization keys table, add culture-specific Resx files (e.g., `Syncfusion.PdfViewer.Windows.fr.resx`), set custom assembly/namespace for localization using `LocalizationManager.SetResources()` |
| **themes.md** | Apply built-in themes using `ThemeName` property (`Office2016Colorful`, `Office2016Black`, `Office2016DarkGray`, `Office2016White`, `Office2019Colorful`, `HighContrastBlack`), load theme assemblies via `SkinManager.LoadAssembly()`, reset to default theme |
| **interaction-modes.md** | Switch cursor modes using `CursorMode` property — `PdfViewerCursorMode.SelectTool` for text selection (default), `PdfViewerCursorMode.HandTool` for panning/scrolling |
| **error-handling.md** | Subscribe to `ErrorOccurred` event, handle `ErrorOccurredEventArgs.Message` to log errors or display messages to users |
| **magnifying.md** | Zoom to a specific percentage using `ZoomTo()`, get current zoom via `ZoomPercentage`, switch zoom modes using `ZoomMode` property (`FitPage`, `FitWidth`) |
| **view-pdf-stream.md** | Load a PDF from a `FileStream` using the `Load(stream)` overload |
| **document-information.md** | Access filename and file path of the loaded PDF via `DocumentInformation.FileName` and `DocumentInformation.FilePath`; get page count via `PageCount` |
| **mouse-position.md** | Handle `PageClicked` and `PageMouseMove` events to get page index and mouse position relative to the PDF page |
| **host-wpf-pdfviewer-in-winforms.md** | Host the WPF PdfViewer inside a WinForms app using `ElementHost` to access advanced features (annotations, form filling, signatures) |
| **toolbar.md** | Show/hide individual toolbar buttons (Open, Save, Zoom, Print, Pan) using `ToolbarSettings.<Button>.IsVisible` |

---

## Prerequisites

- Development Environment:Visual Studio 2022 or Visual Studio insider 2026(recommended for .NET 10).
- .NET Framework 4.5+ or .NET Core/NET 8+
- Syncfusion WinForms NuGet Package: Syncfusion.PdfViewer.Windows

## Documentations
- [Syncfusion WinForms PdfViewer Docs](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/winforms/overview)
- [API Reference](https://help.syncfusion.com/cr/document-processing/Syncfusion.Windows.PdfViewer.html)