# Basic Sample

Brief: This guide covers the setup and initialization of a Syncfusion React PDF Viewer component with standalone mode configuration. It includes project setup, package installation, CSS imports, and basic component rendering with resource configuration.

> For the latest compatibility requirements, refer to the official Syncfusion documentation.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Installation](#installation)
- [CSS Configuration](#css-configuration)
- [HTML Setup](#html-setup)
- [PdfViewerComponent Configuration](#pdfviewercomponent-configuration)
- [Services Injection](#services-injection)
- [Local Resources Configuration](#local-resources-configuration)
- [Running the Application](#running-the-application)
- [Styling](#styling)
- [Next.js Configuration](#nextjs-configuration)
- [Complete Basic Example](#complete-basic-example)

## Prerequisites

Required versions and dependencies for Syncfusion React PDF Viewer:

### Requirements
- React supported version >= 15.5.4+
- Node version >= 14.0.0+ (NPM Package Manager)

---

## Project Setup

Setup a new React application using Vite for optimal development experience.

### Setup with TypeScript

```bash
npm create vite@latest my-app -- --template react-ts
cd my-app
npm run dev
```

### Setup with JavaScript

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm run dev
```

---

## Installation

Install the Syncfusion PDF Viewer package and configure required resources.

### Install Package

```bash
npm install @syncfusion/ej2-react-pdfviewer --save
```

### Copy Resources

Copy the ej2-pdfviewer-lib folder from node_modules to the public directory:

```bash
cp -R ./node_modules/@syncfusion/ej2-pdfviewer/dist/ej2-pdfviewer-lib public/ej2-pdfviewer-lib
```

### Verify Configuration

- Confirm `ej2-pdfviewer-lib` directory exists in your public folder
- Ensure your server supports `Content-Type: application/wasm` MIME type

---

## CSS Configuration

Add the PDF Viewer component CSS references to `src/index.css`:

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import "../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css";
```

---

## HTML Setup

Add the root div element to `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Syncfusion React PDF Viewer</title>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Essential JS 2 for React Components" />
  <meta name="author" content="Syncfusion" />
</head>
<body>
  <div id='sample'>
    <div id='loader'>Loading....</div>
    <script type="module" src="/src/main.tsx"></script>
  </div>
</body>
</html>
```

---

## PdfViewerComponent Configuration

The main component for rendering PDF documents with interactive features. Configure these essential properties to set up your PDF viewer instance.

### Required Properties

**Always provide these three properties when creating a PdfViewerComponent:**

| Property | Type | Purpose | Example |
|----------|------|---------|---------|
| **id** | `string` | Unique identifier for the component instance | `id="container"` |
| **documentPath** | `string` | Path to the PDF document (CDN URL or local file) | `documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"` |
| **resourceUrl** | `string` | URL folder with library resources (pdfium.js, pdfium.wasm) | `resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"` |

### Basic Implementation

```tsx
<PdfViewerComponent
  id="container"
  documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
  resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"
  style={{ 'height': '640px' }}>
</PdfViewerComponent>
```

### Property Details

#### Property: documentPath

**Type**: `string`

**Description**: Specifies the path to the PDF document to be displayed. Can be a CDN URL or local file path.

**Why it matters**: Without this, the viewer has no PDF to render. Always provide either a CDN URL or local path.

**Examples**:
- CDN: `"https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"`
- Local: `"/assets/document.pdf"` or `window.location.origin + "/assets/pdf.pdf"`

#### Property: resourceUrl

**Type**: `string`

**Description**: Specifies the URL of the folder containing the required PDF Viewer library resources, including pdfium.js and pdfium.wasm files.

**Why it matters**: The PDF Viewer needs WebAssembly files to function. This URL must point to the directory containing `pdfium.js` and `pdfium.wasm` files.

**Examples**:
- CDN: `"https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"`
- Local: `window.location.origin + "/assets/ej2-pdfviewer-lib"`

#### Property: id

**Type**: `string`

**Description**: Unique identifier for the PDF Viewer component instance.

**Why it matters**: Used to reference and control the component instance from your code. Must be unique within your application.

**Examples**:
- Simple: `id="container"`
- Descriptive: `id="pdf-viewer-main"` or `id="invoice-pdf"`

---

## Services Injection

Services enable specific features in the PDF Viewer. Inject only the services you need to optimize performance and reduce bundle size.

### Service Selection Guide

**Choose services based on user needs. This table helps you decide which services to inject:**

| Service | When to Use | Use Case | Bundle Impact |
|---------|------------|----------|---------------|
| **Toolbar** | Always (unless read-only viewer) | Display toolbar with document controls | Medium |
| **Magnification** | When users need zoom control | Zoom and magnification functionality | Small |
| **Navigation** | When document has multiple pages | Page navigation controls | Small |
| **Annotation** | For collaborative review/feedback | Annotation capabilities | Large |
| **LinkAnnotation** | For documents with hyperlinks | Enable clicking links in PDFs | Small |
| **BookmarkView** | For long documents with bookmarks | Bookmark view panel for quick navigation | Small |
| **ThumbnailView** | For visual page browsing | Thumbnail view panel | Medium |
| **Print** | When print capability needed | Print functionality | Small |
| **TextSelection** | For extracting text from PDF | Text selection capabilities | Small |
| **TextSearch** | For finding content in document | Text search functionality | Medium |
| **FormFields** | For interactive forms | Form field handling | Medium |
| **FormDesigner** | For form creation/editing | Form design mode | Large |

### Available Services

- **Toolbar**: Displays toolbar with document controls
- **Magnification**: Zoom and magnification functionality
- **Navigation**: Page navigation controls
- **Annotation**: Annotation capabilities
- **LinkAnnotation**: Link annotation support
- **BookmarkView**: Bookmark view panel
- **ThumbnailView**: Thumbnail view panel
- **Print**: Print functionality
- **TextSelection**: Text selection capabilities
- **TextSearch**: Text search functionality
- **FormFields**: Form field handling
- **FormDesigner**: Form design mode

### Usage

```tsx
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, 
         BookmarkView, ThumbnailView, Print, TextSelection, Annotation, TextSearch, 
         FormFields, FormDesigner, Inject } from '@syncfusion/ej2-react-pdfviewer';

function App() {
  return (
    <PdfViewerComponent
      id="container"
      documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
      resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"
      style={{ 'height': '640px' }}>
      <Inject services={[ 
        Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, 
        BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, 
        FormFields, FormDesigner 
      ]} />
    </PdfViewerComponent>
  );
}
```

---

## Local Resources Configuration

Load PDF Viewer with local files instead of CDN resources.

### Step 1: Resource Location

Ensure your application includes the `ej2-pdfviewer-lib` folder containing:
- `pdfium.js`
- `pdfium.wasm`
- PDF files to display

These files should be located in the `public/assets` directory.

### Step 2: Local Path Configuration

Assign local file paths to `documentPath` and `resourceUrl` properties:

```tsx
<PdfViewerComponent
  id="container"
  documentPath={window.location.origin + "/assets/pdfsuccinctly.pdf"}
  resourceUrl={window.location.origin + "/assets/ej2-pdfviewer-lib"}
  style={{ 'height': '640px' }}>
</PdfViewerComponent>
```

### Note: Resource Requirements

- `documentPath`: Should refer to your local PDF file
- `resourceUrl`: Should point to the directory containing supporting resources

---

## Running the Application

Start the development server with the following command:

```bash
npm run dev
```

This command compiles your code and serves the application locally, opening it in the browser.

---

## Styling

Configure component styling with inline CSS or CSS classes:

```tsx
<PdfViewerComponent
  id="container"
  documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
  resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"
  style={{ 'height': '640px' }}>
</PdfViewerComponent>
```

### Parameters
- **height**: CSS height value for the component container (e.g., '640px', '100%')

---

## Next.js Configuration

When deploying the PDF Viewer in a Next.js application, create a `next.config.js` file:

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: false,  // Disable React Strict Mode for compatibility
  swcMinify: false,        // Disable SWC minification for better compatibility
};

module.exports = nextConfig;
```

### Note: OpenSSL Legacy Provider

If you encounter `ERR_OSSL_EVP_UNSUPPORTED` error, run:

```bash
$env:NODE_OPTIONS = "--openssl-legacy-provider"
```

---

## Complete Basic Example

Full example combining all setup steps:

```tsx
import * as ReactDOM from 'react-dom/client';
import * as React from 'react';
import './index.css';
import { 
  PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, 
  BookmarkView, ThumbnailView, Print, TextSelection, Annotation, TextSearch, 
  FormFields, FormDesigner, Inject 
} from '@syncfusion/ej2-react-pdfviewer';

function App() {
  return (
    <div>
      <div className='control-section'>
        <PdfViewerComponent
          id="container"
          documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
          resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"
          style={{ 'height': '640px' }}>
          <Inject services={[ 
            Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, 
            BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, 
            FormFields, FormDesigner 
          ]} />
        </PdfViewerComponent>
      </div>
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('sample'));
root.render(<App />);
```