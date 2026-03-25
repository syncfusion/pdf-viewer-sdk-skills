# Syncfusion ASP.NET Core PDF Viewer — Skill

## Overview

The **syncfusion-aspnetcore-pdf-viewer** skill enables AI-assisted code generation for the [Syncfusion ASP.NET Core PDF Viewer](https://www.syncfusion.com/aspnet-core-components/pdf-viewer). It produces minimal, copy-pasteable Razor markup and C# code to embed, configure, and interact with PDF documents inside ASP.NET Core web applications.

---

## Compatibility

| Requirement | Version |
|---|---|
| .NET | `.NET 8.0 LTS` or later |
| .NET Framework | `4.6.2` or later |
| Operating System | Windows, Linux, or macOS |
| Development Tools | Visual Studio 2022, Visual Studio Code, or JetBrains Rider |
| Web Browser | Modern browsers with HTML5 and WebAssembly support |

---

## Skill Structure

```
syncfusion-aspnetcore-pdf-viewer/
├── SKILL.md                      # Skill rules, routing, and code generation guidelines
├── README.md                     # This file
└── references/
    ├── basic-sample.md           # Minimal setup & initialization template
    ├── opening-pdfs.md           # Load PDFs from various sources (URL, local, stream)
    ├── enable-properties.md      # Feature toggle properties (toolbar, annotation, forms, etc.)
    ├── viewing-and-interaction.md # Display modes, interaction, and user control
    ├── navigation.md             # Page navigation (first, last, next, previous, goto)
    ├── bookmark-navigation.md    # Bookmark panel and outline navigation
    ├── magnification.md          # Zoom levels, zoom modes, fit-to-page/width
    ├── text-selection.md         # Enable text select, copy, and selection events
    ├── text-search.md            # Find text in PDF with search options
    ├── toolbar-customization.md  # Customize toolbar items, visibility, and behavior
    ├── contextmenu.md            # Right-click context menu customization
    ├── annotation-overview.md    # Annotation capabilities and types
    ├── annotation-settings.md    # Annotation appearance (colors, opacity, author, styles)
    ├── annotation-events.md      # Annotation lifecycle events (add, delete, move, etc.)
    ├── annotation-operations.md  # Annotation API methods and programmatic control
    ├── annotation-use-cases.md   # Common annotation patterns and workflows
    ├── shape-annotations.md      # Rectangle, circle, line shape annotations
    ├── measurement-annotations.md # Measurement tool configurations
    ├── free-text-annotations.md  # Text annotation creation and styling
    ├── stamp-annotation.md       # Stamp annotations and presets
    ├── text-markup-annotations.md # Highlight, underline, strikethrough annotations
    ├── form-fields-overview.md   # Form field capabilities and field types
    ├── form-fields-props.md      # Form field properties and defaults
    ├── form-field-settings.md    # Configure default properties for form fields
    ├── form-field-events.md      # Form field interaction events (focus, blur, change)
    ├── form-field-validation.md  # Form field validation and constraints
    ├── form-operations.md        # Import/export form data and programmatic access
    ├── supported-form-fields.md  # List of supported form field types
    ├── import-export-form-data.md # Import and export form field values
    ├── download.md               # PDF download configuration and customization
    ├── printing-and-organizing.md # Print configuration and page organization
    ├── saving-and-downloading.md # Save and download options
    ├── api-methods.md            # Programmatic API (load, export, undo/redo, extract)
    └── events.md                 # Complete PDF Viewer event reference
```

---

## Quick Start

### 1. Create an ASP.NET Core Project

```bash
# Using .NET CLI
dotnet new webapp -n MyPdfViewerApp
cd MyPdfViewerApp

# Or using Visual Studio
# Create ASP.NET Core Web App → Select .NET 6.0 LTS or later
```

### 2. Install NuGet Package

Using Package Manager Console:
```powershell
Install-Package Syncfusion.EJ2.AspNet.Core
```

Or using .NET CLI:
```bash
dotnet add package Syncfusion.EJ2.AspNet.Core
```

### 3. Add Tag Helper

Update `~/Pages/_ViewImports.cshtml`:

```csharp
@addTagHelper *, Syncfusion.EJ2
```

### 4. Add Styles (CDN)

Add to `~/Pages/Shared/_Layout.cshtml` in the `<head>` section:

```html
<head>
    <!-- Syncfusion CSS Theme -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.1.44/material.css" />
</head>
```

**Available Themes:**
- `material.css` - Material Design
- `bootstrap5.css` - Bootstrap 5
- `tailwind3.css` - Tailwind CSS
- `fluent.css` - Microsoft Fluent
- `fabric.css` - Microsoft Fabric

### 5. Add Scripts (CDN)

Add to `_Layout.cshtml` in the `<head>` section:

```html
<head>
    <!-- ... CSS ... -->
    <!-- Syncfusion JavaScript Library -->
    <script src="https://cdn.syncfusion.com/ej2/33.1.44/dist/ej2.min.js"></script>
</head>
```

### 6. Register Script Manager

Add at the **end of the `<body>` tag** in `_Layout.cshtml`:

```html
<body>
    <!-- ... page content ... -->
    
    <!-- Syncfusion Script Manager - MUST be at end of body -->
    <ejs-scripts></ejs-scripts>
</body>
```

### 7. Add PDF Viewer Component

Add to `~/Pages/Index.cshtml`:

```cshtml
@page
@model IndexModel
@{
    ViewData["Title"] = "PDF Viewer";
}

<div class="pdf-viewer-container">
    <h2>Syncfusion PDF Viewer</h2>
    
    <ejs-pdfviewer 
        id="pdfviewer" 
        style="height:600px" 
        documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf">
    </ejs-pdfviewer>
</div>
```

**Component Properties:**
- `id` - Unique identifier for the PDF Viewer instance
- `style` - CSS styles (height is required)
- `documentPath` - URL or path to the PDF document

### 8. Run the Application

```bash
dotnet run
```

Or press **Ctrl+F5** in Visual Studio.

---

## Available Features

| Feature | Property | Description |
|---|---|---|
| **Toolbar** | `enableToolbar` | Show/hide the main toolbar |
| **Navigation** | `enableNavigation` | Enable page navigation controls |
| **Annotations** | `enableAnnotation` | Enable all annotation capabilities |
| **Form Fields** | `enableFormFields` | Support interactive form fields |
| **Bookmarks** | `enableBookmark` | Display bookmark/outline panel |
| **Thumbnails** | `enableThumbnail` | Show page thumbnail panel |
| **Text Search** | `enableTextSearch` | Enable find-in-document functionality |
| **Text Selection** | `enableTextSelection` | Allow text selection and copy |
| **Print** | `enablePrint` | Enable print functionality |
| **Download** | `enableDownload` | Enable PDF download |
| **Hyperlinks** | `enableHyperlink` | Make URLs clickable |

---

## Reference File Routing

Use the table below to find the correct reference file for any feature.

### Core Setup

| Reference File | Use When … |
|---|---|
| `basic-sample.md` | Getting started, minimal setup, loading a PDF |
| `opening-pdfs.md` | Loading PDFs from URLs, local files, or streams |
| `enable-properties.md` | Enabling/disabling toolbar, annotations, forms, download, print |

### Navigation

| Reference File | Use When … |
|---|---|
| `navigation.md` | Go to first/last/next/previous page or a specific page number |
| `bookmark-navigation.md` | Navigate via bookmarks or open/close bookmark panel |
| `viewing-and-interaction.md` | Display modes, interaction, and zoom behavior |

### Viewing & Interaction

| Reference File | Use When … |
|---|---|
| `magnification.md` | Zoom controls, fit-to-page, fit-to-width, zoom levels |
| `text-selection.md` | Enable/handle text selection and copy events |
| `text-search.md` | Implement in-document text search and result highlighting |

### Toolbar & Context Menu

| Reference File | Use When … |
|---|---|
| `toolbar-customization.md` | Customize toolbar items, visibility, and tooltip behavior |
| `contextmenu.md` | Add, remove, or handle right-click context menu items |

### Annotations

| Reference File | Use When … |
|---|---|
| `annotation-overview.md` | Overview of annotation types and capabilities |
| `annotation-settings.md` | Set default annotation colors, opacity, author, styles |
| `annotation-events.md` | Handle annotation add/delete/move/resize/select events |
| `annotation-operations.md` | Programmatic annotation API and methods |
| `annotation-use-cases.md` | Common annotation patterns and workflows |
| `shape-annotations.md` | Rectangle, circle, line shape annotations |
| `measurement-annotations.md` | Measurement tool configurations |
| `free-text-annotations.md` | Text annotation creation and styling |
| `stamp-annotation.md` | Stamp annotations and presets |
| `text-markup-annotations.md` | Highlight, underline, strikethrough annotations |

### Forms

| Reference File | Use When … |
|---|---|
| `form-fields-overview.md` | Overview of form field capabilities |
| `form-fields-props.md` | Form field properties and defaults |
| `form-field-settings.md` | Configure default properties for form fields |
| `form-field-events.md` | Handle form field focus, blur, and value-change events |
| `form-field-validation.md` | Form field validation and constraints |
| `form-operations.md` | Import/export form data and programmatic access |
| `supported-form-fields.md` | List of supported form field types |
| `import-export-form-data.md` | Import and export form field values |

### Document Actions

| Reference File | Use When … |
|---|---|
| `download.md` | Enable download and set custom filenames |
| `printing-and-organizing.md` | Configure printing and page organization |
| `saving-and-downloading.md` | Save and download options |

### Advanced / API

| Reference File | Use When … |
|---|---|
| `api-methods.md` | Load documents programmatically, export form data, undo/redo |
| `events.md` | Browse all available PDF Viewer events and signatures |

---

## Metadata

| Field | Value |
|---|---|
| **Skill Name** | `syncfusion-aspnetcore-pdf-viewer` |
| **Author** | Syncfusion Inc |
| **Version** | `1.0.0` |
| **Category** | Document Viewing |
| **Framework** | ASP.NET Core |
| **Reference Files** | 34 |
