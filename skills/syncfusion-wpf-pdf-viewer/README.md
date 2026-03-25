# Syncfusion WPF PDF Viewer (PdfViewerControl) Skill

## Overview
Display, load, and interact with PDF documents in WPF using Syncfusion's `PdfViewerControl` — concise, paste-ready XAML/C# examples for loading PDFs, annotations, text search, toolbar customization, printing, form filling, and many other PDF tasks.

See **[SKILL.md](SKILL.md)** for the full intent-routing guide and rules.

---

## Key Capabilities

- **PDF Loading & Display:** load from file path, stream, or `PdfLoadedDocument`; support for encrypted PDFs and MVVM binding via `ItemSource`.
- **Annotations:** ink, shapes (line, rectangle, circle, arrow, polygon, polyline), stamp, sticky note, free text, text callout, highlight, underline, strikethrough, squiggly, and file link annotations.
- **Navigation & Interaction:** page navigation, thumbnails, bookmarks, hyperlinks, zoom modes, and cursor interaction modes (Selection, Panning, Marquee Zoom).
- **Text Operations:** text search with highlight, text selection, and full text extraction with bounds.
- **Forms & Signatures:** AcroForm field management, FDF import/export, and handwritten signature support.
- **Toolbar & UI Customization:** show/hide toolbar items, disable specific buttons, customize context menus, and apply localization.
- **Document Processing:** print (silent and interactive), save PDF, export pages as images, import/export annotations (FDF/XFDF), page organize (rotate, reorder, remove), and redaction.
- **Advanced Features:** PDF layers, PDF coordinates/scroll offsets, rendering engine switching (PDFium/SfPdf), and text extraction engine switching.

---

## Getting Started

### How to Integrate the Skill

**Step 1: Checkout and copy the required skill**

Clone or download the PDF-Viewer-SDK-Skills repository and copy the **wpf-pdfviewer-code-generator** skill from the `skills/` directory.

**Step 2: Install the skill**

Place the copied skill folder in your workspace following this structure:

```
your-workspace/
├── .github/skills/          # or .claude/skills/ or .codestudio/skills/
│   └── wpf-pdfviewer-code-generator/
│       └── SKILL.md
├── your-project-files...
└── MainWindow.xaml
```

**Step 3: Verify and manage your skills**

Type `/skills` in the GitHub Copilot or Code Studio chat to quickly access the Configure Skills menu and manage your installed skills.

**Step 4: Use the skill in VS Code / Code Studio**

There are two ways to use the skill:

1. **Slash commands** – Type `/` in the GitHub Copilot chat to see available skills. For example:
   ```
   /wpf-pdfviewer How do I load an encrypted PDF?
   ```

2. **Automatic loading** – Simply describe your task naturally, and the AI Agent automatically loads the relevant skill:
   ```
   Create a WPF window with PdfViewerControl that highlights text and exports annotations to XFDF
   ```

When the wpf-pdfviewer skill is loaded, the AI Agent provides focused XAML/C# snippets and commands for `PdfViewerControl`.

---

### Prerequisites

1. **Visual Studio** 2022 or later (WPF workload installed)
2. **.NET** Framework 4.5+ or .NET Core / .NET 8+ with WPF support
3. **Syncfusion License** — register your key inside the `MainWindow` constructor:
   ```csharp
   SyncfusionLicenseProvider.RegisterLicense("Your-License-Key");
   ```
   Free license: [Syncfusion Community License](https://www.syncfusion.com/products/communitylicense)

### NuGet Package

```bash
dotnet add package Syncfusion.PdfViewer.WPF
```

---

## Example Prompts

### Loading & Display
- "Show me how to load a PDF from a file path using `PdfViewerControl`."
- "Generate code to load a password-protected PDF and suppress the built-in password dialog."
- "Provide a MVVM example where `ItemSource` is bound to a ViewModel property."

### Annotations
- "Generate C# to enable ink annotation mode with a green color and 5px thickness."
- "Show me how to add a custom stamp image programmatically at a specific page position."
- "Provide code to listen to `TextMarkupAnnotationChanged` events for highlight, underline, and strikethrough."
- "How do I lock all annotations so they can't be edited or deleted?"

### Navigation & Zoom
- "Show code to navigate to a specific page and zoom to 150%."
- "How do I switch the cursor to Panning mode programmatically?"
- "Generate code to handle bookmark navigation events."

### Text Search & Selection
- "Show me how to search for text in the PDF and highlight all matches."
- "Provide code to retrieve the selected text and its bounds from `PdfViewerControl`."

### Toolbar & UI Customization
- "How do I hide the default toolbar and scrollbar?"
- "Show me how to collapse a specific toolbar button like the text search button."
- "Generate code to add a custom item to the PdfViewer context menu."

### Printing & Saving
- "Show me how to silently print the PDF to a specific printer."
- "Generate code to save the PDF to a file path and handle the save completed event."

### Forms & Signatures
- "How do I import form data from an FDF file into the viewer?"
- "Show me how to enable handwritten signature mode and flatten signatures on save."

### Export & Extraction
- "Generate code to export page 2 as a PNG image."
- "Show me how to extract all text and bounds from every page of the loaded PDF."

### Advanced
- "How do I switch the rendering engine to PDFium?"
- "Show me how to mark a region for redaction and apply it."
- "Provide code to rotate and reorder pages using the page organizer."

---

## Reference Files

All code snippets used by the AI Agent are organized in the `references/` folder:

| File | Purpose |
|---|---|
| `Load-sample.md` | Load PDFs via stream or file path (encrypted and normal); unload document; customize loading indicator color and message. |
| `navigation.md` | Page navigation (including `GoToPageAtIndex`), page count, current page index, thumbnail panel, bookmark navigation, and hyperlink events. |
| `annotation.md` | Add and control annotations (ink, shapes, stamp, text, highlights, etc.); disable annotation selection; set current user; customize annotation selector colors. |
| `pdf-rendering.md` | Switch rendering engine (PDFium/SfPdf) and set ReferencePath. |
| `text-extraction-engine.md` | Switch text extraction engine (PDFium/SfPdf). |
| `print.md` | Print settings, silent print, paper source, and print events. |
| `export-image.md` | Export pages as images (JPG, PNG, TIFF, BMP) using `ExportAsImage`. |
| `import-export-annotations.md` | Import/export annotations in FDF or XFDF format using `ImportAnnotations` and `ExportAnnotations`. |
| `extract-text-from-pdf.md` | Extract text and bounds from pages or full document. |
| `form-filling.md` | Form field events, FDF import/export, and AcroForm field management. |
| `pdf-layers.md` | Toggle layer visibility and disable layers. |
| `redaction.md` | Enable redaction, mark regions, customize appearance, and handle events. |
| `pdf-coordinates.md` | Coordinate conversion, scroll offsets, and ZoomToRect. |
| `organize-pages.md` | Rotate, reorder, and remove pages; page organizer settings. |
| `handwritten-signature.md` | Signature mode, appearance settings, flatten on save, and events. |
| `interaction-mode.md` | Switch cursor modes (Selection, Panning, Marquee Zoom). |
| `pdf-pages.md` | Page border customization, page interaction events, and pixel-to-point coordinate conversion on page click. |
| `saving-pdf-files.md` | Save PDF, handle save events, cancel save, and check if the document has been edited. |
| `magnifying.md` | Zoom level, zoom mode, zoom limits, and ZoomChanged event. |
| `searching-text.md` | Search, highlight, navigate results, and retrieve text bounds. |
| `text-selection.md` | Detect and retrieve selected text and bounds. |
| `localization.md` | Apply .resx localization and set UI culture. |
| `customize-contextmenu.md` | Add, remove, or hide context menu items. |
| `commands.md` | Command bindings for navigation, zoom, annotations, print, and save; disable undo/redo via `UndoRedoSettings.Limit`. |
| `toolbar-items.md` | Show/hide toolbar elements and disable individual toolbar items. |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| License warning at startup | Call `SyncfusionLicenseProvider.RegisterLicense()` inside the `MainWindow` constructor before `InitializeComponent()` |
| PDF not loading | Ensure the file path is correct and the file is not locked by another process; use `Path.GetFullPath()` for relative paths |
| Missing NuGet package | Run `dotnet add package Syncfusion.PdfViewer.WPF` or install via NuGet Package Manager |
| Toolbar item not found | Verify the template part name (e.g., `PART_ButtonTextSearch`) using the Syncfusion control template |
| Encrypted PDF dialog not suppressed | Handle the `GetDocumentPassword` event and set `e.Handled = true` to bypass the built-in dialog |
| Annotations not saving | Call `pdfViewer.Save("output.pdf")` or handle `DocumentSaveInitiated` to persist annotation changes |

---

## Resources

- [WPF PdfViewer Overview](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/wpf/overview)
- [API Reference – PdfViewerControl](https://help.syncfusion.com/cr/wpf/Syncfusion.Windows.PdfViewer.PdfViewerControl.html)

---

## License

Syncfusion WPF PdfViewer requires a commercial license for production use. A [free community license](https://www.syncfusion.com/products/communitylicense) is available for qualifying organizations.
