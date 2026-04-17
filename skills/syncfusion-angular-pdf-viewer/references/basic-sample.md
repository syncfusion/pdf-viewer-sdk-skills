# Getting Started with Angular Standalone PDF Viewer Component

Brief: This guide covers the setup and initialization of a Syncfusion Angular PDF Viewer component with standalone mode configuration. It includes project setup, package installation, CSS imports, and basic component rendering with resource configuration for Angular 21 and other recent Angular versions.

> This guide supports Angular 21 and other recent Angular versions. Starting from Angular 19, standalone components are the default, and this guide reflects that architecture.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setup Angular Environment](#setup-angular-environment)
- [Create an Angular Application](#create-an-angular-application)
- [Installation](#installation)
- [CSS Configuration](#css-configuration)
- [Component Setup](#component-setup)
- [PdfViewer Component Configuration](#pdfviewer-component-configuration)
- [Module Injection](#module-injection)
- [Local Resources Configuration](#local-resources-configuration)
- [Running the Application](#running-the-application)
- [Complete Basic Example](#complete-basic-example)

---

## Prerequisites

Ensure your development environment meets the System Requirements for Syncfusion Angular UI Components.

### Requirements
- Node.js and npm package manager
- Angular CLI installed globally
- Compatible Angular version (refer to Angular version support matrix)

---

## Setup Angular Environment

Use the Angular CLI to setup your Angular applications.

GitHub Reference: https://github.com/angular/angular-cli

```bash
npm install -g @angular/cli
```

### Angular 21 Standalone Architecture

Standalone components are the default in Angular 21. This guide uses the modern standalone architecture.



To install a particular version of Angular CLI:

```bash
npm install -g @angular/cli@21.0.0
```

---

## Create an Angular Application

Start a new Angular application using the Angular CLI command.

### Basic Creation

```bash
ng new my-app
```

This command will prompt you to configure settings:
- Enable Angular routing
- Choose a stylesheet format (CSS, SCSS, etc.)

### Create with SCSS Styles

```bash
ng new my-app --style=scss
```

### Configuration Prompts

During project setup, you will be prompted for:

1. **Server-side rendering (SSR) option**: Choose the appropriate configuration based on your requirements
2. **AI tool selection**: Select the required AI tool or 'none' if not needed

### Navigate to Project Directory

```bash
cd my-app
```

### File Structure Note

In Angular 19 and below, the CLI uses:
- `app.component.ts`
- `app.component.html`
- `app.component.css`

In Angular 20+, the CLI generates a simpler structure:
- `src/app/app.ts`
- `app.html`
- `app.css`

(no `.component.` suffixes)

---

## Installation

Install the Syncfusion PDF Viewer package and configure required resources.

### Install Package

All available Essential JS 2 packages are published in npmjs.com registry.

```bash
npm install @syncfusion/ej2-angular-pdfviewer --save
```

### Copy Resources

Copy the contents of the ej2-pdfviewer-lib folder from node_modules to the src/assets directory:

```bash
cp -R ./node_modules/@syncfusion/ej2-pdfviewer/dist/ej2-pdfviewer-lib src/assets/ej2-pdfviewer-lib
```

### Verify Configuration

- Confirm that there is an `ej2-pdfviewer-lib` directory within your `src/assets` directory, housing the assets of the PDF Viewer library
- Validate that your server has been configured to utilize the `Content-Type: application/wasm` MIME type

---

## CSS Configuration

Add the Angular PDF Viewer component's styles to `src/styles.css` file.

### CSS Imports

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
@import '../node_modules/@syncfusion/ej2-notifications/styles/material.css';
```

### Available Themes

The example above uses the `material` theme. Other available themes include:
- `bootstrap`
- `bootstrap4`
- `bootstrap5`
- `fabric`
- `tailwind`
- `fluent`
- `material3`

Replace `material` in the import paths with your preferred theme name.

---

## Component Setup

Add the Angular PDF Viewer component to your application.

### Basic Component Implementation

Add the Angular PDF Viewer by using `<ejs-pdfviewer>` selector in the template section of the `src/app/app.ts` file to render the PDF Viewer component.

```typescript
import { Component, OnInit } from '@angular/core';
import { PdfViewerModule, LinkAnnotationService, BookmarkViewService,
         MagnificationService, ThumbnailViewService, ToolbarService,
         NavigationService, TextSearchService, TextSelectionService,
         PrintService, FormDesignerService, FormFieldsService,
         AnnotationService, PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  // specifies the template string for the PDF Viewer component
  template: `<div class="content-wrapper">
                <ejs-pdfviewer id="pdfViewer"
                    [documentPath]='document'
                    [resourceUrl]='resource'
                    style="height:640px;display:block">
                </ejs-pdfviewer>
             </div>`,
  imports: [ PdfViewerModule ],
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               TextSearchService, TextSelectionService, PrintService,
               AnnotationService, FormDesignerService, FormFieldsService, PageOrganizerService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = window.location.origin + "/assets/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
}
```

---

## PdfViewer Component Configuration

The main component for rendering PDF documents with interactive features. Configure these essential properties to set up your PDF viewer instance.

### Required Properties

**Always provide these properties when creating a PdfViewerComponent:**

| Property | Type | Purpose | Example |
|----------|------|---------|---------|
| **id** | `string` | Unique identifier for the component instance | `id="pdfViewer"` |
| **documentPath** | `string` | Path to the PDF document (CDN URL or local file) | `[documentPath]='document'` where `document` is a component property |
| **resourceUrl** | `string` | URL folder with library resources (pdfium.js, pdfium.wasm) | `[resourceUrl]='resource'` where `resource` is a component property |

### Property Details

#### Property: documentPath

**Type**: `string`

**Description**: Specifies the path to the PDF document to be displayed. Can be a CDN URL or local file path.

**Why it matters**: Without this, the viewer has no PDF to render. Always provide either a CDN URL or local path.

**Examples**:
- CDN: `'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'`
- Local: `window.location.origin + "/assets/pdfsuccinctly.pdf"`

#### Property: resourceUrl

**Type**: `string`

**Description**: Specifies the URL of the folder containing the required PDF Viewer library resources, including pdfium.js and pdfium.wasm files.

**Why it matters**: The PDF Viewer needs WebAssembly files to function. This URL must point to the directory containing `pdfium.js` and `pdfium.wasm` files.

**Examples**:
- CDN: Provide the Valid CDN link of the resource url
- Local: `window.location.origin + "/assets/ej2-pdfviewer-lib"`

#### Property: id

**Type**: `string`

**Description**: Unique identifier for the PDF Viewer component instance.

**Why it matters**: Used to reference and control the component instance from your code. Must be unique within your application.

**Examples**:
- Simple: `id="pdfViewer"`
- Descriptive: `id="pdf-viewer-main"` or `id="invoice-pdf"`

---

## Module Injection

To enable additional features, inject the required modules. Services enable specific features in the PDF Viewer.

### Service Selection Guide

**Choose services based on user needs. This table helps you decide which services to inject:**

| Service | When to Use | Use Case | Bundle Impact |
|---------|------------|----------|---------------|
| **ToolbarService** | Always (unless read-only viewer) | Enables the built-in toolbar UI | Medium |
| **MagnificationService** | When users need zoom control | Provides zoom in/out operations | Small |
| **NavigationService** | When document has multiple pages | Enables page navigation | Small |
| **AnnotationService** | For collaborative review/feedback | Enables annotation features | Large |
| **LinkAnnotationService** | For documents with hyperlinks | Enables hyperlink navigation | Small |
| **BookmarkViewService** | For long documents with bookmarks | Displays and navigates document bookmarks | Small |
| **ThumbnailViewService** | For visual page browsing | Displays page thumbnails for navigation | Medium |
| **PrintService** | When print capability needed | Enables printing | Small |
| **TextSelectionService** | For extracting text from PDF | Enables text selection | Small |
| **TextSearchService** | For finding content in document | Enables text search | Medium |
| **FormFieldsService** | For interactive forms | Enables form field support | Medium |
| **FormDesignerService** | For form creation/editing | Enables designing and editing of form fields | Large |
| **PageOrganizerService** | For page manipulation | Enables page organization features | Medium |

### Available Services

- **LinkAnnotationService**: Enables hyperlink navigation
- **BookmarkViewService**: Displays and navigates document bookmarks
- **MagnificationService**: Provides zoom in/out operations
- **NavigationService**: Enables page navigation
- **TextSelectionService**: Enables text selection
- **ThumbnailViewService**: Displays page thumbnails for navigation
- **ToolbarService**: Enables the built-in toolbar UI
- **PrintService**: Enables printing
- **AnnotationService**: Enables annotation features
- **TextSearchService**: Enables text search
- **FormFieldsService**: Enables form field support
- **FormDesignerService**: Enables designing and editing of form fields
- **PageOrganizerService**: Enables page organization features

### Usage

Inject modules using the `providers` array in the component:

```typescript
import { Component, OnInit } from '@angular/core';
import { PdfViewerModule, LinkAnnotationService, BookmarkViewService,
         MagnificationService, ThumbnailViewService, ToolbarService,
         NavigationService, TextSearchService, TextSelectionService,
         PrintService, FormDesignerService, FormFieldsService,
         AnnotationService, PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<div class="content-wrapper">
                <ejs-pdfviewer id="pdfViewer"
                    [documentPath]='document'
                    style="height:640px;display:block">
                </ejs-pdfviewer>
             </div>`,
  imports: [ PdfViewerModule ],
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               TextSearchService, TextSelectionService, PrintService,
               AnnotationService, FormDesignerService, FormFieldsService, PageOrganizerService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  ngOnInit(): void {
  }
}
```

### Note: Service Optimization

Inject only the services you need to optimize performance and reduce bundle size. Each service adds functionality but also increases the application bundle size.

---

## Local Resources Configuration

Load PDF Viewer with local files instead of CDN resources.

### Step 1: Resource Location

Ensure that your application includes the `ej2-pdfviewer-lib` folder containing:
- `pdfium.js`
- `pdfium.wasm`
- PDF files to display

These files should be located in the `src/assets` directory within your project's `src` folder.

### Step 2: Register Assets Folder

Register the assets folder inside `angular.json`:

```json
"assets": [
  "src/assets"
]
```

### Step 3: Local Path Configuration

Assign local file paths to `documentPath` and `resourceUrl` properties. The `documentPath` should refer to your PDF file, while the `resourceUrl` should point to the directory containing the supporting resources.

```typescript
@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer id="pdfViewer"
                [documentPath]='document'
                [resourceUrl]='resource'
                style="height:640px;display:block">
              </ejs-pdfviewer>`,
  imports: [ PdfViewerModule ],
  providers: [ /* services */ ]
})
export class AppComponent implements OnInit {
  public document: string = window.location.origin + "/assets/pdfsuccinctly.pdf";
  public resource: string = window.location.origin + "/assets/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
}
```

---

## Running the Application

Use the following command to run the application in the browser.

### Start Development Server

```bash
ng serve --open
```

This command:
- Compiles your code
- Starts the development server
- Opens the application in your default browser

### Expected Output

The output will display a PDF Viewer component with:
- Toolbar with controls
- PDF document loaded and rendered
- Interactive features based on injected services

---

## Complete Basic Example

Full example combining all setup steps:

### app.ts

```typescript
import { Component, OnInit } from '@angular/core';
import { PdfViewerModule, LinkAnnotationService, BookmarkViewService,
         MagnificationService, ThumbnailViewService, ToolbarService,
         NavigationService, TextSearchService, TextSelectionService,
         PrintService, FormDesignerService, FormFieldsService,
         AnnotationService, PageOrganizerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  // specifies the template string for the PDF Viewer component
  template: `<div class="content-wrapper">
                <ejs-pdfviewer 
                    id="pdfViewer"
                    [documentPath]='document'
                    [resourceUrl]='resource'
                    style="height:640px;display:block">
                </ejs-pdfviewer>
             </div>`,
  imports: [ PdfViewerModule ],
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               TextSearchService, TextSelectionService, PrintService,
               AnnotationService, FormDesignerService, FormFieldsService, PageOrganizerService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = window.location.origin + "/assets/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
}
```

### Styling

Configure component styling with inline CSS or CSS classes:

```html
<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]='document'
    [resourceUrl]='resource'
    style="height:640px;display:block">
</ejs-pdfviewer>
```

**Parameters**:
- **height**: CSS height value for the component container (e.g., '640px', '100%')
- **display**: CSS display property (typically 'block' for full-width display)

---
