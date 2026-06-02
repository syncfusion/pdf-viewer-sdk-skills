# Syncfusion .NET MAUI PDF Viewer — Skill

## Overview

The **syncfusion-maui-pdf-viewer** skill enables AI-assisted code generation for the [Syncfusion .NET MAUI SfPdfViewer](https://help.syncfusion.com/maui/pdf-viewer/getting-started). It produces minimal, copy-pasteable C# and XAML code to embed, configure, and interact with PDF documents inside cross-platform .NET MAUI applications.

---

## Compatibility

| Requirement | Version |
|---|---|
| .NET | .NET 6, 7, 8, 9 or later |
| Target Platforms | Android, iOS, Windows, macOS |
| Visual Studio | 2022 (17.0 or later) |
| Package Manager | NuGet |

---

## Skill Structure

```
syncfusion-maui-pdf-viewer/
├── SKILL.md                              # Skill rules, routing, and code generation guidelines
├── README.md                             # This file
└── references/
    ├── basic-sample.md                   # Minimal setup, handler registration, document loading
    ├── viewing.md                        # Page layouts, zoom modes, fit modes, bookmarks, hyperlinks
    ├── document-operations.md            # Load with password, unload (memory mgmt), save, print
    ├── annotations.md                    # Ink, shapes, stamps, sticky notes, text markups, free text
    ├── form-fields.md                    # AcroForm support, validation, import/export (XFDF/FDF/JSON/XML)
    ├── text-search.md                    # Async text search, match navigation, highlighting
    ├── text-selection.md                 # Enable selection, SelectedText property, customization
    ├── electronic-signature.md           # Handwritten, image, text signatures
    ├── redaction.md                      # Text/area/page-based redaction, permanent removal
    ├── toolbar-customization.md          # Desktop/mobile layouts, add/remove/reorder items
    ├── ui-settings.md                    # Localization, RTL, liquid glass, theme customization
    ├── gesture-events.md                 # DocumentTapped event, touch handling
    └── migration-xamarin-to-maui.md      # Xamarin.Forms to MAUI migration guide
```

---

## Quick Start

### 1. Install NuGet Package

```
Syncfusion.Maui.PdfViewer
```

### 2. Register Syncfusion Core Handler (`MauiProgram.cs`)

```csharp
using Syncfusion.Maui.Core.Hosting;

builder.ConfigureSyncfusionCore();
Syncfusion.Licensing.SyncfusionLicenseProvider.RegisterLicense("YOUR_LICENSE_KEY");
```

### 3. Add SfPdfViewer to XAML (`MainPage.xaml`)

```xml
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.Maui.PdfViewer;assembly=Syncfusion.Maui.PdfViewer">
    <syncfusion:SfPdfViewer x:Name="pdfViewer" />
</ContentPage>
```

### 4. Load a PDF Document

**Option A: From Embedded Resource (Recommended)**

1. Add PDF to `Assets` folder in your project
2. Set **Build Action** to **Embedded Resource**
3. Load in code:

```csharp
using System.Reflection;

Stream stream = typeof(App).GetTypeInfo().Assembly
    .GetManifestResourceStream("PdfViewerExample.Assets.sample.pdf");
pdfViewer.DocumentSource = stream;
```

**Option B: From File Picker**

```csharp
private async Task LoadPdfFromFileSystem()
{
    var result = await FilePicker.PickAsync(new PickOptions
    {
        PickerTitle = "Select a PDF file"
    });
    
    if (result != null)
    {
        Stream stream = await result.OpenReadAsync();
        pdfViewer.DocumentSource = stream;
    }
}
```

### 5. Run the Application

Press **F5** to build and run. The PDF will be displayed with the built-in toolbar.

---

## Reference File Routing

Use the table below to find the correct reference file for any feature request.

### Core Setup & Document Loading

| Reference File | Use When … |
|---|---|
| `basic-sample.md` | Initial setup, handler registration, XAML declaration, DocumentSource binding |
| `document-operations.md` | Loading with password, unloading (memory management), saving with flattening, printing |

### Navigation & Viewing

| Reference File | Use When … |
|---|---|
| `viewing.md` | Page navigation, layout modes (Single, Continuous), bookmarks, hyperlinks, zoom, FitMode |

### Text Operations

| Reference File | Use When … |
|---|---|
| `text-search.md` | Async text search, match navigation (GoToNextMatch, GoToPreviousMatch), highlighting, custom UI |
| `text-selection.md` | Enable text selection, SelectedText property, clipboard copy, selection customization |

### Annotations

| Reference File | Use When … |
|---|---|
| `annotations.md` | Ink, shapes, stamps, sticky notes, text markups, free text, eraser; annotation properties and events |

### Forms & Signatures

| Reference File | Use When … |
|---|---|
| `form-fields.md` | Viewing, filling, validating form fields; import/export (XFDF, FDF, JSON, XML); flattening |
| `electronic-signature.md` | Handwritten, image-based, text signatures; signature field management, validation |

### Security & Redaction

| Reference File | Use When … |
|---|---|
| `redaction.md` | Redacting text, areas, or pages; permanent content removal, appearance customization |

### UI Customization

| Reference File | Use When … |
|---|---|
| `toolbar-customization.md` | Desktop vs mobile toolbars, add/remove/hide/reorder items, AnnotationToolbarItemClicked event |
| `ui-settings.md` | Localization, FlowDirection (RTL), liquid glass effect, theme customization |

### Advanced Features

| Reference File | Use When … |
|---|---|
| `gesture-events.md` | DocumentTapped event with page number and position, custom touch interactions |
| `migration-xamarin-to-maui.md` | Migrating from Xamarin.Forms to MAUI, API differences, breaking changes |

---

## Available Services

The PDF Viewer includes comprehensive features through its built-in services:

| Service | Purpose |
|---|---|
| **Viewing** | Page navigation, zoom, layout modes (Single, Continuous) |
| **Annotations** | Ink, shapes, stamps, sticky notes, text markups, free text |
| **Forms** | Fill, validate, import/export form data (XFDF, FDF, JSON, XML) |
| **Text Operations** | Async search, text selection, clipboard copy |
| **Signatures** | Handwritten, image-based, text signatures |
| **Redaction** | Permanent content removal |
| **Toolbar** | Customizable desktop/mobile layouts |

---

## Example Prompts

 "Show me how to set up SfPdfViewer in .NET MAUI"
- "How do I navigate to a specific page number?"
- "How do I search for text in a PDF asynchronously?"
- "How do I add an ink annotation to the PDF?"
- "How do I fill a form field programmatically?"
---

## Metadata

| Field | Value |
|---|---|
| **Skill Name** | `syncfusion-maui-pdf-viewer` |
| **Author** | Syncfusion Inc |
| **Version** | `1.0.0` |
| **Category** | Document Viewing |
| **Framework** | .NET MAUI (Multi-platform App UI) |
| **Target Platforms** | Android, iOS, Windows, macOS |
| **Reference Files** | 13 |

---

## License

Syncfusion .NET MAUI components require a commercial license for production use. A [free community license](https://www.syncfusion.com/products/communitylicense) is available for qualifying organizations and individuals.
