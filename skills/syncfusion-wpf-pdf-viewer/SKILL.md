---
name: syncfusion-wpf-pdf-viewer
description: Create sample application using Syncfusion WPF PdfViewer. Implements Syncfusion WPF PdfViewer for embedding, configuring, and customizing PDF viewing in WPF applications. Generates C# and XAML code for PDF display, navigation, zooming, text selection, search, annotations, toolbar customization, and PDF event handling using Syncfusion's WPF PDF viewing components.
compatibility: .NET Framework 4.5+ or .NET Core/NET 8+, Syncfusion.WPF.PdfViewer.
metadata:
  author: Syncfusion Inc
  version: "34.1.29"
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
| **Load-sample.md** | Load and unload PDFs using file paths, streams, or PdfLoadedDocument (encrypted or not); support async loading, MVVM binding, password handling, loading indicator customization, and theme application. |
| **navigation.md** | Navigate PDF pages using index‑ or number‑based APIs; retrieve page state information; scroll programmatically; manage thumbnails and bookmarks; and handle hyperlink navigation events. |
| **annotation.md** | Enable, customize, and manage all annotation types; handle annotation events; programmatically select, hide, lock, or delete annotations; control comments panel, authorship, hyperlinks, and selection visuals. |
| **pdf-rendering.md** | Configure the PDF rendering engine by switching between PDFium and SfPdf and setting the required ReferencePath. |
| **text-extraction-engine.md** | Select the text extraction engine (PDFium or SfPdf) to control text extraction behavior. |
| **print.md** | Print PDFs with silent or dialog options; configure printers, page size, scaling, orientation, page range, paper source, and document name; and handle print lifecycle events. |
| **export-image.md** | Export PDF pages or page ranges as images (JPG, PNG, TIFF, BMP) with control over size, DPI, aspect ratio, and transparency. |
| **import-export-annotations.md** | Import and export annotations using FDF or XFDF formats. |
| **extract-text-from-pdf.md** | Extract text content and bounding information from pages or the entire document. |
| **form-filling.md** | Handle AcroForm fields: manage form events, show or hide icons, import/export form data, and add or edit form fields programmatically. |
| **pdf-layers.md** | Access and manage PDF layers by toggling visibility, enabling or disabling layers, and controlling the Layers pane UI. |
| **redaction.md** | Apply redactions by marking regions, customizing appearance, and handling redaction events. |
| **pdf-coordinates.md** | Convert between coordinate systems, retrieve scroll offsets, and zoom into specific page regions. |
| **organize-pages.md** | Rotate, reorder, and remove pages using page organizer features. |
| **handwritten-signature.md** | Capture handwritten signatures, customize appearance, handle signature events, and flatten signatures on save. |
| **interaction-mode.md** | Switch viewer interaction modes such as text selection, panning, and marquee zoom using cursor settings. |
| **pdf-pages.md** | Customize page appearance, handle page interaction events, and convert pixel coordinates to PDF points. |
| **saving-pdf-files.md** | Save edited PDFs, detect unsaved changes, cancel save operations, handle save events, and prompt before closing with pending edits. |
| **magnifying.md** | Control zoom behavior including zoom levels, fit modes, limits, zoom-to-rectangle, toolbar visibility, and zoom change events. |
| **searching-text.md** | Search and highlight text, navigate results, retrieve match bounds and text details, support multi-line search, and control search UI and availability. |
| **text-selection.md** | Detect text selection completion, retrieve selected text and bounds, customize highlight color, enable or disable selection, and clear selections programmatically. |
| **localization.md** | Localize the PDF Viewer UI using .resx resources and culture settings. |
| **customize-contextmenu.md** | Customize context menus by adding, removing, hiding items, and handling menu click events. |
| **commands.md** | Use and bind built‑in WPF commands for navigation, zoom, search, annotations, undo/redo, printing, saving, and unloading documents. |
| **toolbar-items.md** | Customize viewer UI by showing or hiding toolbars, panels, buttons, menus, notification bars, and switching toolbar styles. |
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
