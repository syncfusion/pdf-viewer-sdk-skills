# Syncfusion UWP PDF Viewer — Skill

## Overview

The **syncfusion-uwp-pdf-viewer** skill enables AI-assisted code generation for the [Syncfusion UWP SfPdfViewerControl](https://help.syncfusion.com/uwp/pdf-viewer/getting-started). It produces minimal, copy-pasteable C# and XAML code to embed, configure, and interact with PDF documents inside Universal Windows Platform (UWP) applications.

---

## Compatibility

| Requirement | Version |
|---|---|
| .NET Framework | UWP (Universal Windows Platform) |
| Target Platform | Windows 10 (Build 1809) or later |
| Visual Studio | Visual Studio 2017 or later |

---

## Skill Structure

```
syncfusion-uwp-pdf-viewer/
├── SKILL.md                              # Skill rules, routing, and code generation guidelines
├── README.md                             # This file
└── references/
    ├── getting-started.md                # Minimal setup, XAML declaration, document loading
    ├── viewing-pdf.md                    # Load from Stream, PdfLoadedDocument, StorageFile
    ├── page-navigation.md                # Navigate pages, commands, PageChanged event
    ├── magnification.md                  # Zoom control, view modes, thumbnail toggle
    ├── text-operations.md                # Text search/selection, clipboard operations
    ├── annotations.md                    # Text markup, shapes, ink, popup, free text, stamps
    ├── printing.md                       # Print configuration, quality settings, preview
    ├── bookmarks-and-hyperlinks.md       # Bookmark navigation, hyperlink validation (security)
    ├── localization.md                   # UI localization, resource files, language settings
    └── utilities.md                      # Export pages, scroll offset, PDFium renderer
```

---

## Quick Start

### 1. Install NuGet Package

```bash
Install-Package Syncfusion.SfPdfViewer.UWP
```

### 2. Add License Key (`App.xaml.cs`)

```csharp
public App()
{
    Syncfusion.Licensing.SyncfusionLicenseProvider.RegisterLicense("YOUR_LICENSE_KEY");
    this.InitializeComponent();
}
```

### 3. Add Control to XAML (`MainPage.xaml`)

```xaml
<Page xmlns:syncfusion="using:Syncfusion.Windows.PdfViewer">
    <Grid>
        <syncfusion:SfPdfViewerControl x:Name="pdfViewer"/>
    </Grid>
</Page>
```

### 4. Load PDF Document

**Option A: From Embedded Resource**

```csharp
using Syncfusion.Pdf.Parsing;
using System.Reflection;

Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
Stream stream = assembly.GetManifestResourceStream("PdfViewerApp.Assets.sample.pdf");
byte[] buffer = new byte[stream.Length];
stream.Read(buffer, 0, buffer.Length);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(buffer);
pdfViewer.LoadDocument(loadedDocument);
```

**Option B: From File Picker**

```csharp
private async void LoadPdfButton_Click(object sender, RoutedEventArgs e)
{
    FileOpenPicker picker = new FileOpenPicker();
    picker.ViewMode = PickerViewMode.List;
    picker.FileTypeFilter.Add(".pdf");
    
    StorageFile file = await picker.PickSingleFileAsync();
    if (file != null)
    {
        pdfViewer.LoadDocument(file);
    }
}
```

**Option C: Using Data Binding (ItemsSource)**

```xaml
<Page Loaded="Page_Loaded">
    <Page.DataContext>
        <local:PdfReportViewModel/>
    </Page.DataContext>
    <Grid>
        <syncfusion:SfPdfViewerControl x:Name="pdfViewer"
                                       ItemsSource="{Binding DocumentStream}"/>
    </Grid>
</Page>
```

### 5. Run the Application

```bash
F5
```

---

## Security Notice ⚠️

Always validate hyperlinks before allowing navigation when loading PDFs from untrusted sources.

```csharp
pdfViewer.HyperlinkPointerPressed += (sender, args) =>
{
    if (!IsUriTrusted(args.Uri))
    {
        args.Handled = true; // Block navigation
    }
};
```

See [references/bookmarks-and-hyperlinks.md](references/bookmarks-and-hyperlinks.md) for complete validation examples.

---

## Reference File Routing

Use the table below to find the correct reference file for any feature request.

### Core Setup & Document Loading

| Reference File | Use When … |
|---|---|
| `getting-started.md` | Initial setup, XAML declaration, NuGet packages, ItemsSource binding |
| `viewing-pdf.md` | Loading from Stream, PdfLoadedDocument, StorageFile; saving, unloading, disposal |

### Navigation & Viewing

| Reference File | Use When … |
|---|---|
| `page-navigation.md` | Navigate to first/last/next/previous page, page commands, PageChanged event |
| `magnification.md` | Zoom in/out, fit-to-width, fit-to-page, thumbnail view, view modes |
| `bookmarks-and-hyperlinks.md` | Navigate bookmarks, validate hyperlinks (security), GoToBookmark method |

### Text Operations

| Reference File | Use When … |
|---|---|
| `text-operations.md` | Search text (sync/async), navigate results, text selection, clipboard copy, highlight color |

### Annotations

| Reference File | Use When … |
|---|---|
| `annotations.md` | Text markup (highlight, underline, strikethrough), free text callout, shapes, ink, popup notes, free text, stamps, undo/redo |

### Document Actions

| Reference File | Use When … |
|---|---|
| `printing.md` | Print configuration, quality factor, print preview customization, async printing |

### Advanced Features

| Reference File | Use When … |
|---|---|
| `localization.md` | Change UI language, add resource files, localize context menus |
| `utilities.md` | Export pages as images, scroll offsets, PDFium renderer, page number display |

---

---

## Available Features

The UWP PDF Viewer provides comprehensive document viewing and management capabilities:

| Feature | Description |
|---|---|
| **Document Loading** | Stream, PdfLoadedDocument, async loading with CancellationToken |
| **Navigation** | Page commands, bookmarks, hyperlinks (with validation) |
| **Viewing** | Zoom controls, view modes (FitWidth, Normal, OnePage), thumbnail view |
| **Text Operations** | Sync/async search, text selection, highlight color customization |
| **Annotations** | Text markup, shapes, ink (Windows Ink Canvas), popup, free text, stamps |
| **Printing** | Quality settings, print preview customization, async printing |
| **Localization** | Multi-language UI support with resource files |
| **Advanced** | Export pages as images, PDFium custom renderer, scroll offset access |

---

## Example Prompts

- "Show me how to set up SfPdfViewerControl in UWP XAML"
- "How do I navigate to the next page in the PDF viewer?"
- "How do I search for text in a PDF document?"
- "How do I add a highlight annotation to selected text?"
- "How do I validate hyperlinks before allowing navigation?"
- "How can I customize the print preview dialog?"

---

## Metadata

| Field | Value |
|---|---|
| **Skill Name** | `syncfusion-uwp-pdf-viewer` |
| **Author** | Syncfusion Inc |
| **Version** | `1.0.0` |
| **Category** | Document Viewing |
| **Framework** | UWP (Universal Windows Platform) |
| **Reference Files** | 10 |