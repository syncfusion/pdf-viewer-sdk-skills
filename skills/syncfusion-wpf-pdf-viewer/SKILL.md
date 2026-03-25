---
name: syncfusion-wpf-pdf-viewer
description: Create sample application using Syncfusion WPF PdfViewer. Implements Syncfusion WPF PdfViewer for embedding, configuring, and customizing PDF viewing in WPF applications. Generates C# and XAML code for PDF display, navigation, zooming, text selection, search, annotations, toolbar customization, and PDF event handling using Syncfusion's WPF PDF viewing components.
compatibility: .NET Framework 4.5+ or .NET Core/NET 8+, Syncfusion.WPF.PdfViewer.
metadata:
  author: Syncfusion Inc
  version: "33.1.44"
---

# Syncfusion WPF PDFViewer – UI Sample Generator

## Generate C# Code for the User's Project *(default)*

**Trigger keywords:** "how to", "code sample", "show me", "example", "snippet", "integrate", "wpf PdfViewer", "create sample".

**Purpose:** Generate clean, ready-to-use C# and XAML code snippets that users can directly insert into their WPF applications when working with the Syncfusion WPF PdfViewer control.

**Workflow:**
1. Build the C# code using snippets provided in the `references/*.md` files.
2. Before generating the sample, ask the user whether the code should be inserted into an existing XAML file in their WPF project or created as a new WPF project application.
3. If the user chooses to create a **new WPF project**, ask them which target framework they want to use:
   - **.NET Framework** (e.g. 4.6, 4.7, 4.8) — uses `Syncfusion.PdfViewer.WPF` and targets classic .NET Framework.
   - **.NET Core / .NET** (e.g., .NET 8, .NET 10) — uses `Syncfusion.PdfViewer.WPF` with `<TargetFramework>net8.0-windows</TargetFramework>` (or the selected version).
   - Based on the user's choice, generate the `.csproj` file with the correct `<TargetFramework>` value, and tailor any framework-specific code (e.g., namespace imports, NuGet package versions, startup code) accordingly.
4. **XAML generation rules — MANDATORY: analyze the reference files BEFORE writing any XAML:**

   > ⚠️ **STRICT RULE — NO EXCEPTIONS:**
   > Open and read the relevant `references/*.md` file(s) for the requested feature **before** producing any XAML.
   > Ask yourself: *"Does the reference file contain any XAML markup for this feature?"*
   > - **YES → XAML exists in reference** → include only those exact XAML elements shown in the snippet.
   > - **NO → reference is C# only** → `MainWindow.xaml` MUST contain **only** `<syncfusion:PdfViewerControl>` inside a `<Grid>`. Stop. Do not add anything else.

   **Checklist to run before every XAML output:**
   - [ ] I have opened the relevant `references/*.md` file.
   - [ ] I have confirmed whether it contains XAML or is C#-only.
   - [ ] If C#-only: my XAML contains nothing beyond `<syncfusion:PdfViewerControl x:Name="pdfViewer"/>` inside `<Grid>`.
   - [ ] If XAML exists in reference: I am copying only those elements — not inventing new ones.

   **Forbidden (when reference has no XAML):** `<Button>`, `<ComboBox>`, `<Slider>`, `<StackPanel>`, `<TextBlock>`, `<Grid.RowDefinitions>`, or any UI element that does not appear verbatim in the reference snippet.

   **Known C#-only features (no XAML must be generated):**
   - Ink / shape / stamp / text / highlight annotations (`annotation.md`) — all settings are C# only.
   - Magnifying / zoom level (`magnifying.md`) — C# only.
   - Interaction mode (`interaction-mode.md`) — C# only.
   - Text selection (`text-selection.md`) — C# only.
   - PDF layers (`pdf-layers.md`) — C# only.
   - Redaction (`redaction.md`) — C# only.
   - Print (`print.md`) — C# only.
   - Export image (`export-image.md`) — C# only.
   - Saving PDF (`saving-pdf-files.md`) — C# only.

   **Known features that DO require XAML (sourced from references):**
   - **Commands** (`commands.md`): navigation/zoom/annotation/undo/redo/print/unload buttons use `Command="{Binding ElementName=..., Path=...}"`.
   - **Toolbar items** (`toolbar-items.md`): classic style requires `Style="{StaticResource SyncfusionPdfViewerCustomControlStyle}"` on `<syncfusion:PdfViewerControl>`.

   All XAML additions must be placed inside the same `<Grid>` that hosts `<syncfusion:PdfViewerControl>`, using a `<StackPanel>` or `<Grid>` sub-layout **only when the reference snippet implies it**.
5. Add only the APIs required to satisfy the user's requested functionality. Do not include optional APIs, additional.
6. **C# language version compatibility:** When the target framework is **.NET Framework** (e.g., 4.6, 4.7, 4.8), the default C# language version is **7.3**. The generated C# code **MUST NOT** use any C# 8.0+ language features. Specifically, do **NOT** use:
   - Switch expressions (`x switch { ... }`)
   - Nullable reference types (`string?`, `#nullable enable`, `object?`)
   - Default interface implementations
   - Ranges and indices (`^1`, `1..^1`)
   - `??=` null-coalescing assignment
   Use `if/else` or traditional `switch` statements instead of switch expressions. Use regular null checks (`if (x != null)`) instead of nullable reference type syntax.
---

### Code References

All templates and operation snippets live in `references/*.md`. Each file is a focused snippet or template the agent will combine when generating samples.

| File | Purpose |
|---|---|
| **Load-sample.md** | Load PDFs via stream or file path (encrypted and normal); unload document; customize loading indicator color and message. |
| **navigation.md** | Page navigation (including `GoToPageAtIndex`), page count, current page index, thumbnail panel, bookmark navigation, and hyperlink events. |
| **annotation.md** | Add and control annotations (ink, shapes, stamp, text, highlights, etc.); disable annotation selection; set current user; customize annotation selector colors. |
| **pdf-rendering.md** | Switch rendering engine (PDFium/SfPdf) and set ReferencePath. |
| **text-extraction-engine.md** | Switch text extraction engine (PDFium/SfPdf). |
| **print.md** | Print settings, silent print, paper source, and print events. |
| **export-image.md** | Export pages as images (JPG, PNG, TIFF, BMP) using `ExportAsImage`. |
| **import-export-annotations.md** | Import/export annotations in FDF or XFDF format using `ImportAnnotations` and `ExportAnnotations`. |
| **extract-text-from-pdf.md** | Extract text and bounds from pages or full document. |
| **form-filling.md** | Form field events, FDF import/export, and AcroForm field management. |
| **pdf-layers.md** | Toggle layer visibility and disable layers. |
| **redaction.md** | Enable redaction, mark regions, customize appearance, and handle events. |
| **pdf-coordinates.md** | Coordinate conversion, scroll offsets, and ZoomToRect. |
| **organize-pages.md** | Rotate, reorder, and remove pages; page organizer settings. |
| **handwritten-signature.md** | Signature mode, appearance settings, flatten on save, and events. |
| **interaction-mode.md** | Switch cursor modes (Selection, Panning, Marquee Zoom). |
| **pdf-pages.md** | Page border customization, page interaction events, and pixel-to-point coordinate conversion on page click. |
| **saving-pdf-files.md** | Save PDF, handle save events, cancel save, and check if the document has been edited. |
| **magnifying.md** | Zoom level, zoom mode, zoom limits, and ZoomChanged event. |
| **searching-text.md** | Search, highlight, navigate results, and retrieve text bounds. |
| **text-selection.md** | Detect and retrieve selected text and bounds. |
| **localization.md** | Apply .resx localization and set UI culture. |
| **customize-contextmenu.md** | Add, remove, or hide context menu items. |
| **commands.md** | Command bindings for navigation, zoom, annotations, print, and save; disable undo/redo via `UndoRedoSettings.Limit`. |
| **toolbar-items.md** | Show/hide toolbar elements and disable individual toolbar items. |
---


### Prerequisites
1. Development Environment: Visual Studio 2022 or Visual Studio Insider 2026 (recommended for .NET 10).
2. NET Framework 4.5+ or .NET Core/.NET 8+ with WPF support.
3. Syncfusion WPF NuGet Packages: `Syncfusion.PdfViewer.WPF`

### Theme NuGet Packages

To apply a built-in theme to the WPF PdfViewerControl using `SfSkinManager`, install the NuGet package that matches the desired theme:

| Theme Name | Required NuGet Package |
|---|---|
| `FluentLight` | `Syncfusion.Themes.FluentLight.WPF` |
| `FluentDark` | `Syncfusion.Themes.FluentDark.WPF` |
| `MaterialLight` | `Syncfusion.Themes.MaterialLight.WPF` |
| `MaterialDark` | `Syncfusion.Themes.MaterialDark.WPF` |
| `MaterialLight3` | `Syncfusion.Themes.MaterialLight3.WPF` |
| `MaterialDark3` | `Syncfusion.Themes.MaterialDark3.WPF` |
| `Office2019Colorful` | `Syncfusion.Themes.Office2019Colorful.WPF` |
| `Office2019Black` | `Syncfusion.Themes.Office2019Black.WPF` |
| `Office2019White` | `Syncfusion.Themes.Office2019White.WPF` |
| `Office2019DarkGray` | `Syncfusion.Themes.Office2019DarkGray.WPF` |
| `Windows11Light` | `Syncfusion.Themes.Windows11Light.WPF` |
| `Windows11Dark` | `Syncfusion.Themes.Windows11Dark.WPF` |

> **Note:** Install only the NuGet package corresponding to the theme the user wants to apply. Theme support requires `Syncfusion.SfSkinManager.WPF`, which is included as a dependency of the theme packages.
>
> Refer to: [Apply theme using SfSkinManager](https://help.syncfusion.com/wpf/themes/skin-manager) | [WPF PdfViewer Theme](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/wpf/getting-started#theme)

### Documentations
[WPF PdfViewer overview](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/wpf/overview)
