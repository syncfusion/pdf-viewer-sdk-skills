# Basic Sample

## Overview

The Syncfusion ASP.NET Core PDF Viewer provides a comprehensive solution for viewing, annotating, and interacting with PDF documents in web applications. This shows component setup using standalone mode.

## Prerequisites

Before setting up the PDF Viewer, ensure the following requirements are met:

### System Requirements

Review the Syncfusion ASP.NET Core system requirements including:

- **Operating System:** Windows, Linux, or macOS
- **.NET Version:** .NET 8.0 LTS or later (e.g., .NET 8.0 LTS)
- **Development Tools:** Visual Studio 2022, Visual Studio Code, Syncfusion Code studio or JetBrains Rider
- **Web Browser:** Modern browsers with HTML5 and WebAssembly support

## Standalone PDF Viewer Setup

Follow these steps to integrate the standalone PDF Viewer with client-side rendering.

**Important:** Always check if the project already has a PDF Viewer setup, if not create it on the root folder using the following steps

### Step 1: Create ASP.NET Core Project

1. Open Visual Studio and select **Create a new project**
2. Choose **ASP.NET Core Web App** template
3. Enter your project name and location
4. Select **.NET 6.0 (Long-term Support)** or later LTS version
5. Click **Create**

**Command Line Alternative:**

```bash
dotnet new webapp
```

### Step 2: Install NuGet Packages

Install the required Syncfusion package using one of these methods:

**Package Manager Console:**

```powershell
Install-Package Syncfusion.EJ2.AspNet.Core
```

**NuGet Package Manager UI:**
1. Right-click project → **Manage NuGet Packages**
2. Search for `Syncfusion.EJ2.AspNet.Core`
3. Click **Install**

**.NET CLI:**

```bash
dotnet add package Syncfusion.EJ2.AspNet.Core
```

### Step 3: Import Tag Helper

Open `~/Pages/_ViewImports.cshtml` (or `~/Views/_ViewImports.cshtml` for MVC) and add:

```csharp
@addTagHelper *, Syncfusion.EJ2
```

This makes all Syncfusion tag helpers available throughout your application.

### Step 4: Add Styles (CDN)

Reference the Syncfusion theme in `~/Pages/Shared/_Layout.cshtml` inside the `<head>` tag:

```html
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - PDF Viewer</title>
    
    <!-- Syncfusion CSS Theme -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/material.css" />
</head>
```

**Available Themes:**
- `material.css` - Material Design
- `bootstrap5.css` - Bootstrap 5
- `tailwind3.css` - Tailwind CSS
- `fluent.css` - Microsoft Fluent
- `fabric.css` - Microsoft Fabric

### Step 5: Add Scripts (CDN)

Add the Syncfusion JavaScript library in `_Layout.cshtml` inside the `<head>` tag:

```html
<head>
    <!-- ... theme CSS ... -->
    
    <!-- Syncfusion JavaScript Library -->
    <script src="https://cdn.syncfusion.com/ej2/dist/ej2.min.js"></script>
</head>
```

### Step 6: Register Script Manager

Register the Syncfusion script manager at the **end of the `<body>` tag** in `_Layout.cshtml`:

```html
<body>
    <header><!-- header content --></header>
    
    <main role="main">
        @RenderBody()
    </main>
    
    <footer><!-- footer content --></footer>
    
    <!-- Syncfusion Script Manager - MUST be at end of body -->
    <ejs-scripts></ejs-scripts>
</body>
```

**Important:** The `<ejs-scripts>` tag must be placed at the end of the `<body>` element to ensure proper initialization.

### Step 7: Add PDF Viewer Component

Add the PDF Viewer to `~/Pages/Index.cshtml`:

```cshtml
@page "{handler?}"
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
- `style` - CSS styles (height is required for proper display)
- `documentPath` - URL or path to the PDF document

### Step 8: Configure Local Resources (Standalone)

For standalone mode with local PDF files and resources:

**Step 8a:** Create the folder structure:

```
wwwroot/
├── ej2-pdfviewer-lib/
│   ├── pdfium.js
│   └── pdfium.wasm
└── pdfs/
    └── sample.pdf
```

**Step 8b:** Download pdfium files from Syncfusion GitHub repository or CDN.

**Step 8c:** Update `Index.cshtml` to use local paths:

```cshtml
@page "{handler?}"
@model IndexModel
@{
    ViewData["Title"] = "PDF Viewer";
    var originUrl = $"{Request.Scheme}://{Request.Host}{Request.PathBase}";
    var documentPath = originUrl + "/pdfs/sample.pdf";
    var resourceUrl = originUrl + "/ej2-pdfviewer-lib";
}

<div class="pdf-viewer-container">
    <ejs-pdfviewer 
        id="pdfviewer" 
        style="height:600px" 
        documentPath="@documentPath" 
        resourceUrl="@resourceUrl">
    </ejs-pdfviewer>
</div>
```

**Property Explanations:**
- `documentPath` - Full URL to the PDF file (must be publicly accessible)
- `resourceUrl` - URL to the folder containing pdfium.js and pdfium.wasm

### Step 9: Run the Application

Press **Ctrl+F5** (Windows) or **⌘+F5** (macOS) to run the application without debugging.

**.NET CLI:**

```bash
dotnet run
```

The PDF Viewer will render in your default browser with the specified PDF document loaded.

## Using Local Resources

For offline deployment or when CDN access is restricted, use local resources.

### Local Styles and Scripts

**Step 1:** Download Syncfusion resources:
- Download `ej2.min.js` from Syncfusion GitHub
- Download theme CSS file (e.g., `material.min.css`)

**Step 2:** Place files in `wwwroot`:

```
wwwroot/
├── css/
│   └── material.min.css
└── js/
    └── ej2.min.js
```

**Step 3:** Update `_Layout.cshtml` with local references:

```html
<head>
    <!-- Local Syncfusion CSS -->
    <link rel="stylesheet" href="~/css/material.min.css" />
    
    <!-- Local Syncfusion JavaScript -->
    <script src="~/js/ej2.min.js"></script>
</head>
```

### Local PDF Files

Store PDF files in `wwwroot/pdfs/` and reference them:

```cshtml
@{
    var documentPath = $"{Request.Scheme}://{Request.Host}/pdfs/sample.pdf";
}

<ejs-pdfviewer 
    id="pdfviewer" 
    style="height:600px" 
    documentPath="@documentPath">
</ejs-pdfviewer>
```

## Common Setup Steps

These steps apply to both rendering modes.

### Configuring Static Files (if needed)

If serving PDFs from custom folders, configure static file middleware in `Program.cs`:

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services
builder.Services.AddRazorPages();
builder.Services.AddMemoryCache();

var app = builder.Build();

// Configure static files
app.UseStaticFiles(); // Serves files from wwwroot by default

// Optional: Serve files from custom directory
app.UseStaticFiles(new StaticFileOptions
{
    FileProvider = new PhysicalFileProvider(
        Path.Combine(builder.Environment.ContentRootPath, "Documents")),
    RequestPath = "/documents"
});

app.UseRouting();
app.UseAuthorization();
app.MapRazorPages();

app.Run();
```

### Enabling CORS (for cross-origin requests)

If your PDF Viewer needs to access resources from different origins:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowPdfViewer",
        policy => policy
            .WithOrigins("https://yourdomain.com")
            .AllowAnyMethod()
            .AllowAnyHeader());
});

var app = builder.Build();

app.UseCors("AllowPdfViewer");
// ... other middleware
```

## Configuration Options

### Component-Level Properties

```cshtml
<ejs-pdfviewer 
    id="pdfviewer" 
    style="height:600px"
    documentPath="sample.pdf"
    serviceUrl="/Index"              <!-- Server-backed only -->
    resourceUrl="/ej2-pdfviewer-lib" <!-- Standalone only -->
    enableTextSearch="true"
    enableTextSelection="true"
    enableAnnotation="true"
    enableFormFields="true"
    enableBookmark="true"
    enableThumbnail="true"
    enablePrint="true"
    enableDownload="true"
    enableNavigation="true"
    interactionMode="TextSelection"
    zoomMode="FitToPage">
</ejs-pdfviewer>
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

### Dynamic Service URL (Server-backed)

Update the service URL at runtime:

```javascript
function updateServiceUrl() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.serviceUrl = "/NewPdfViewerService";
    viewer.dataBind();
    viewer.load('document.pdf', null);
}
```

## Complete basic setup

Full example combining all setup steps:

```cshtml
@page
@model IndexModel
@{
    ViewData["Title"] = "Home page";
}

<div class="text-center">
    <ejs-pdfviewer id="pdfviewer" style="height:600px"
        documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
        annotationAdd="annotationAdded" >
    </ejs-pdfviewer>
</div>
```

**Pages/_ViewImports.cshtml**

```cshtml
@using sample
@namespace sample.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper *, Syncfusion.EJ2
```

**Pages/Layout/_Layout.cshtml**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - sample</title>
    <script type="importmap"></script>
    <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />
    <link rel="stylesheet" href="~/css/site.css" asp-append-version="true" />
    <link rel="stylesheet" href="~/sample.styles.css" asp-append-version="true" />
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.1.44/tailwind3.css" />
    <script src="https://cdn.syncfusion.com/ej2/33.1.44/dist/ej2.min.js"></script>
</head>
<body>
    <div class="container">
        <main role="main" class="pb-3">
            @RenderBody()
        </main>
    </div>

    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/site.js" asp-append-version="true"></script>

    @await RenderSectionAsync("Scripts", required: false)
    <ejs-scripts></ejs-scripts>
</body>
</html>

```