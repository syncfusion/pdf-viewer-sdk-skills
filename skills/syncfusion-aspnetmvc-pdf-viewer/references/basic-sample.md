# Basic Sample

## Overview

The Syncfusion ASP.NET MVC PDF Viewer provides a comprehensive solution for viewing, printing, and interacting with PDF documents in web applications. This guide covers the standalone PDF Viewer setup using ASP.NET MVC.

## Prerequisites

Before setting up the PDF Viewer, ensure the following requirements are met:

### System Requirements

Review the Syncfusion ASP.NET MVC system requirements including:

- **Operating System:** Windows, Linux, or macOS
- **.NET Framework:** .NET Framework 4.5.1 or later
- **Development Tools:** Visual Studio 2022, Visual Studio Code, or JetBrains Rider
- **Web Browser:** Modern browsers with HTML5 and WebAssembly support
- **License:** Register your Syncfusion license key (see [licensing documentation](https://help.syncfusion.com/common/essential-studio/licensing/license-key))

## Standalone PDF Viewer Setup

Follow these steps to integrate the standalone PDF Viewer into your ASP.NET MVC application.

**Important:** Always check if the project already has a PDF Viewer setup; if not, create it using the following steps.

### Step 1: Create ASP.NET MVC Project

1. Open Visual Studio and select **Create a new project**
2. Select **ASP.NET Web Application (.NET Framework)**
3. Enter your project name and location
4. Click **Create**
5. In the next dialog, select **MVC** as the project template
6. Click **Create**

**Visual Studio 2022 Alternative:**

1. Create a new project using **ASP.NET MVC Web Application** template
2. Select the target framework (.NET Framework 4.7.2 or later recommended)
3. Click **Create**

### Step 2: Install NuGet Packages

Install the required Syncfusion NuGet package:

**Package Manager Console:**

```powershell
Install-Package Syncfusion.EJ2.MVC5
```

**NuGet Package Manager UI:**
1. Right-click project → **Manage NuGet Packages**
2. Search for `Syncfusion.EJ2.MVC5`
3. Click **Install**

### Step 3: Add Namespace

Add the Syncfusion.EJ2 namespace to `Web.config` in the `Views` folder.

Open `~/Views/Web.config` and locate the `<namespaces>` section. Add the following namespace:

```xml
<namespaces>
    <add namespace="Syncfusion.EJ2"/>
</namespaces>
```

### Step 4: Add Styles (CDN)

Reference the Syncfusion theme in `~/Views/Shared/_Layout.cshtml` inside the `<head>` tag:

```html
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewBag.Title - PDF Viewer</title>
    
    <!-- Syncfusion ASP.NET MVC controls styles -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.1.44/fluent.css" />
</head>
```

### Step 5: Add Scripts (CDN)

Add the Syncfusion JavaScript library in `_Layout.cshtml` inside the `<head>` tag:

```html
<head>
    <!-- ... theme CSS ... -->
    
    <!-- Syncfusion ASP.NET MVC controls scripts -->
    <script src="https://cdn.syncfusion.com/ej2/dist/ej2.min.js"></script>
</head>
```

### Step 6: Register Script Manager

Register the Syncfusion script manager at the **end of the `<body>` tag** in `_Layout.cshtml`:

```html
<body>
    <!-- Other content -->
    
    <!-- Syncfusion ASP.NET MVC Script Manager -->
    @Html.EJS().ScriptManager()
</body>
```

**Important:** The `@Html.EJS().ScriptManager()` must be placed at the end of the `<body>` element to ensure proper initialization.

### Step 7: Add PDF Viewer Component

Add the PDF Viewer to `~/Views/Home/Index.cshtml`:

```cshtml
@{
    ViewBag.Title = "Home Page";
}

<div>
    <div style="height:500px;width:100%;">
        @Html.EJS().PdfViewer("pdfviewer").DocumentPath("https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf").Render()
    </div>
</div>
```

**Component Properties:**
- `PdfViewer()` - Creates a PDF Viewer component with the specified ID
- `DocumentPath()` - URL or path to the PDF document to display (required)
- `Render()` - Renders the component HTML

**Note:** The `DocumentPath` property is essential for loading a PDF file in the PDF Viewer.

### Step 8: Configure Local Resources (Standalone)

To load resources locally with the PDF Viewer, follow these steps:

**Step 8a:** Create the folder structure under `Content`:

```
Content/
├── ej2-pdfviewer-lib/
│   ├── pdfium.js
│   └── pdfium.wasm
└── pdfsuccinctly.pdf
```

**Step 8b:** Update `Index.cshtml` to use local paths:

```cshtml
@{
    ViewBag.Title = "Home Page";
    var originUrl = $"{Request.Url.Scheme}://{Request.Url.Authority}";
    var document = originUrl + "/Content/pdfsuccinctly.pdf";
    var resourceUrl = originUrl + "/Content/ej2-pdfviewer-lib";
}

<div style="height: 900px;width:100%;">
    @Html.EJS().PdfViewer("pdfviewer").ResourceUrl(@resourceUrl).DocumentPath(@document).Render()
</div>
```

**Property Explanations:**
- `DocumentPath()` - Full URL to the PDF file (must be publicly accessible)
- `ResourceUrl()` - URL to the folder containing pdfium.js and pdfium.wasm files

## Using Local Resources

For offline deployment or when CDN access is restricted, use local resources.

### Local Styles and Scripts

**Step 1:** Download Syncfusion resources:
- Download `ej2.min.js` from [Syncfusion CDN](https://cdn.syncfusion.com/ej2/)
- Download theme CSS file (e.g., `fluent.min.css`)

**Step 2:** Place files in `Content` folder:

```
Content/
├── ej2/
│   ├── fluent.min.css
│   └── ej2.min.js
└── ej2-pdfviewer-lib/
```

**Step 3:** Update `_Layout.cshtml` with local references:

```html
<head>
    <!-- Syncfusion ASP.NET MVC controls styles -->
    <link rel="stylesheet" href="~/Content/ej2/fluent.min.css" />
    
    <!-- Syncfusion ASP.NET MVC controls scripts -->
    <script src="~/Content/ej2/ej2.min.js"></script>
</head>
```

### Local PDF Files

Store PDF files in `Content` folder and reference them:

```cshtml
@{
    var originUrl = $"{Request.Url.Scheme}://{Request.Url.Authority}";
    var documentPath = originUrl + "/Content/sample.pdf";
}

<div style="height:600px;width:100%;">
    @Html.EJS().PdfViewer("pdfviewer").DocumentPath(@documentPath).Render()
</div>
```

## Running the Application

### Using Visual Studio

1. Press **Ctrl+F5** (Windows) or **⌘+F5** (macOS) to run the application without debugging
2. The PDF Viewer will render in your default browser with the specified PDF document loaded

### Using IIS Express

1. The application will start with IIS Express as the default
2. Navigate to `http://localhost:[port]` in your browser

### Using Command Line

You can also run the application from the command line:

```bash
dotnet run
```

## Configuration Options

### Component-Level Properties

```cshtml
<div style="height:600px;width:100%;">
    @Html.EJS().PdfViewer("pdfviewer").DocumentPath("sample.pdf").ResourceUrl("/Content/ej2-pdfviewer-lib").EnableTextSearch(true).EnableTextSelection(true).EnableAnnotation(true).EnableFormFields(true).EnableBookmark(true).EnableThumbnail(true).EnablePrint(true).EnableDownload(true).EnableNavigation(true).InteractionMode("TextSelection").ZoomMode("FitToPage").Render()
</div>
```

### Programmatic Configuration

Access and configure the PDF Viewer instance using JavaScript:

```javascript
// Get PDF Viewer instance
var viewer = document.getElementById('pdfviewer').ej2_instances[0];

// Load a different document
viewer.load('new-document.pdf', null);

// Enable/disable features
viewer.enableTextSearch = false;
viewer.enableAnnotation = true;
viewer.dataBind(); // Apply changes

// Navigate to specific page
viewer.navigation.goToPage(5);

// Set zoom level
viewer.magnification.zoomTo(150); // 150%
```

## Complete Basic Setup Example

Full example combining all setup steps:

**~/Views/Home/Index.cshtml**

```cshtml
@{
    ViewBag.Title = "Home Page";
}

<div style="height:500px;width:100%;">
    @Html.EJS().PdfViewer("pdfviewer").DocumentPath("https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf").Render()
</div>
```

**~/Views/Web.config** (Add to `<namespaces>` section)

```xml
<namespaces>
    <add namespace="Syncfusion.EJ2"/>
</namespaces>
```

**~/Views/Shared/_Layout.cshtml**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewBag.Title - ASP.NET MVC PDF Viewer</title>
    
    <link rel="stylesheet" href="~/Content/bootstrap.min.css" />
    <link rel="stylesheet" href="~/Content/site.css" />
    <!-- Syncfusion ASP.NET MVC controls styles -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.1.44/fluent.css" />
    <!-- Syncfusion ASP.NET MVC controls scripts -->
    <script src="https://cdn.syncfusion.com/ej2/33.1.44/dist/ej2.min.js"></script>
</head>
<body>
    <nav class="navbar navbar-inverse">
        <div class="container">
            <div class="navbar-header">
                <a class="navbar-brand" href="@Url.Action("Index", "Home")">PDF Viewer</a>
            </div>
        </div>
    </nav>

    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/Scripts/jquery-1.10.2.min.js"></script>
    <script src="~/Scripts/bootstrap.min.js"></script>
    <script src="~/Scripts/site.js"></script>

    @RenderSection("Scripts", required: false)
    
    <!-- Syncfusion ASP.NET MVC Script Manager -->
    @Html.EJS().ScriptManager()
</body>
</html>
```