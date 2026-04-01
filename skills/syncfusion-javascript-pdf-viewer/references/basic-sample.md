# Basic Sample

**Description**: Complete getting started guide for setting up and using the Syncfusion PDF Viewer in a TypeScript application using Essential JS 2 quickstart seed repository. This guide covers development environment setup, package installation, and basic PDF Viewer implementation.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Set up the development environment](#set-up-the-development-environment)
- [Add Syncfusion Javascript (ES6) packages](#add-syncfusion-javascript-packages)
- [Import Syncfusion CSS styles](#import-syncfusion-css-styles)
- [Add the PDF Viewer component](#add-the-pdf-viewer-component)
- [Run the application](#run-the-application)
- [Module injection](#module-injection)
- [Version Information](#version-information)
- [Important Notes](#important-notes)


## Prerequisites

> The sample project uses a webpack configuration (`webpack.config.js`) and the latest [webpack-cli](https://webpack.js.org/api/cli#commands). Node.js `v14.15.0` or later is required. For details, see the [webpack getting started guide](https://webpack.js.org/guides/getting-started).

---

## Set up the development environment

### Step 1: Clone the quickstart project

Open a command prompt in your target directory and clone the Syncfusion Essential JS 2 quickstart project from GitHub:

```cmd
git clone https://github.com/SyncfusionExamples/ej2-quickstart-webpack ej2-quickstart
```

### Step 2: Navigate to the project folder

```cmd
cd ej2-quickstart
```

---

## Add Syncfusion Javascript (ES6) packages

Syncfusion Essential JS 2 packages are available on [npmjs.com](https://www.npmjs.com/~syncfusionorg). The quickstart project includes the [@syncfusion/ej2](https://www.npmjs.com/package/@syncfusion/ej2) meta package in `package.json`.

### Install dependencies

```npm
npm install
```

---

## Import Syncfusion CSS styles

Add the required Syncfusion CSS files to `src/styles/styles.css`:

```css
@import '../../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import "../../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css";
@import "../../node_modules/@syncfusion/ej2-notifications/styles/material.css";
```

---

## Add the PDF Viewer component

### Step 1: Configure PDF Viewer in app.ts

In `app.ts`, import and inject the required modules, then create and configure the PDF Viewer:

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, FormFields, FormDesigner);

let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.documentPath = "https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf";
pdfviewer.resourceUrl = "https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib";
pdfviewer.appendTo('#PdfViewer');
```

### Step 2: Using Local Resources (Optional)

To use local resources instead of CDN, follow these steps:

- Ensure the `ej2-pdfviewer-lib` folder (containing `pdfium.js`, `pdfium.wasm`, and the PDF file) is present in your project's `dist` directory.
- Set the `documentPath` and `resourceUrl` properties to local paths:

```typescript
pdfviewer.documentPath = window.location.origin + "/pdfsuccinctly.pdf";
pdfviewer.resourceUrl = window.location.origin + "/ej2-pdfviewer-lib";
```

**Reference Example**: For a complete example, see [load PDF Viewer with local resources](https://github.com/SyncfusionExamples/typescript-pdf-viewer-examples/tree/master/How%20to/Refer%20resource%20url%20locally).

### Step 3: Add HTML container

Add a container element for the PDF Viewer in `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Essential JS 2</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
    <meta name="description" content="Essential JS 2" />
    <meta name="author" content="Syncfusion" />
    <link rel="shortcut icon" href="resources/favicon.ico" />
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
</head>
<body>
    <!-- PDF Viewer container -->
    <div id="PdfViewer"></div>
</body>
</html>
```

---

## Run the application

The quickstart project is preconfigured to build and launch in the browser. Start the application with:

```npm
npm start
```

### Complete Output Example

**index.ts**:
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
         ThumbnailView, BookmarkView, TextSelection, TextSearch, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView,
                BookmarkView, TextSelection, TextSearch, FormFields, FormDesigner);

let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.documentPath = "https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf";
pdfviewer.resourceUrl = "https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib";
pdfviewer.appendTo('#PdfViewer');
```

**Preview Sample**: [Open in Stackblitz](https://cdn.syncfusion.com/documentation/images/StackBlitz-icon.png)

---

## Module injection

To enable additional features, inject the required modules using `PdfViewer.Inject`. The following modules extend the PDF Viewer:

- **LinkAnnotation**: Hyperlink navigation
- **BookmarkView**: Bookmark display and navigation
- **Magnification**: Zoom in/out
- **Navigation**: Page navigation
- **TextSelection**: Text selection
- **ThumbnailView**: Page thumbnails
- **Toolbar**: Built-in toolbar UI
- **Print**: Printing support
- **Annotation**: Annotation features
- **TextSearch**: Text search
- **FormFields**: Form field support
- **FormDesigner**: Form field design and editing

---

## Version Information

**Resource URL Version**: 31.1.23 (as referenced in the CDN path)

---

## Important Notes

1. Node.js `v14.15.0` or later is required
2. The sample uses webpack configuration and latest webpack-cli
3. The quickstart project includes the @syncfusion/ej2 meta package
4. All Syncfusion packages are available on npmjs.com
5. For local resources, ensure `ej2-pdfviewer-lib` folder is in the `dist` directory
