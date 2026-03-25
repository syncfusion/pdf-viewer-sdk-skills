# Syncfusion Angular PDF Viewer — Skill

## Overview

The **syncfusion-angular-pdf-viewer** skill enables AI-assisted code generation for the [Syncfusion Angular PDF Viewer (`PdfViewerComponent`)](https://www.syncfusion.com/pdf-viewer-sdk/angular-pdf-viewer). It produces minimal, copy-pasteable TS/JS code to embed, configure, and interact with PDF documents inside Angular applications.

---

## Compatibility

Starting from Angular 19, standalone components are the default. Moreover in Angular 19 and below, it uses app.component.ts, app.component.html, app.component.css etc. In Angular 20+, the CLI generates a simpler structure with src/app/app.ts, app.html, and app.css (no .component. suffixes).

---

## Skill Structure

```
syncfusion-angular-pdfviewer/
├── SKILL.md                      # Skill rules, routing, and code generation guidelines
├── README.md                     # This file
└── references/
    ├── basic-sample.md           # Minimal setup & initialization template
    ├── general-properties.md     # Core viewer properties (documentPath, height, locale, etc.)
    ├── enable-properties.md      # Feature toggle properties (enableToolbar, enableAnnotation, etc.)
    ├── toolbar-settings.md       # Toolbar visibility and item customization
    ├── toolbar-methods.md        # Programmatic toolbar show/hide at runtime
    ├── contextmenu.md            # Right-click context menu customization
    ├── page-navigation.md        # Navigate between pages programmatically
    ├── bookmark-navigation.md    # Bookmark panel and navigation
    ├── thumbnail-navigation.md   # Thumbnail panel and page previews
    ├── hyperlink-navigation.md   # Hyperlink and external link behavior
    ├── magnification.md          # Zoom levels, zoom modes, fit-to-page/width
    ├── interaction-mode.md       # Selection mode vs. panning mode
    ├── text-selection.md         # Enable text select, copy, and selection events
    ├── text-search.md            # Find text in PDF with search options
    ├── annotation-settings.md    # Annotation appearance (colors, opacity, styles)
    ├── annotation-events.md      # Annotation lifecycle events (add, delete, resize, etc.)
    ├── shape-label-settings.md   # Shape/measure annotation label customization
    ├── redaction-annotation.md   # Redaction: create, configure, and apply
    ├── form-field-settings.md    # Form field default properties
    ├── form-field-events.md      # Form field interaction events (focus, blur, change)
    ├── download.md               # PDF download configuration
    ├── print.md                  # PDF print configuration
    ├── organize-pages.md         # Reorder, rotate, insert, remove, merge pages
    ├── api-methods.md            # Programmatic API (load, export, undo/redo, extract text)
    └── events.md                 # Complete PDF Viewer event reference
```

---

## Quick Start

### 1. Install the latest Angular CLI

```bash
npm install -g @angular/cli
```

### 2. Create a Angular Project

```bash
ng new my-app
cd my-app
```

### 3. Install the Package

```bash
npm install @syncfusion/ej2-angular-pdfviewer --save
```

### 4. Copy WebAssembly Resources

```bash
cp -R ./node_modules/@syncfusion/ej2-pdfviewer/dist/ej2-pdfviewer-lib  src/assets/ej2-pdfviewer-lib
```

### 5. Add CSS Imports (`src/index.css`)

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

### 6. Basic Component (`src/app/app.ts`)

```ts
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
export class App implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  ngOnInit(): void {
  }
}
```

### 7. Run the App

```bash
ng serve --open
```

---

## Available Services

Inject only the services your use-case requires to keep the bundle lean.

| Service | Purpose |
|---|---|
| `Toolbar` | Main toolbar with document controls |
| `Magnification` | Zoom and magnification |
| `Navigation` | Page navigation controls |
| `Annotation` | All annotation capabilities |
| `LinkAnnotation` | Clickable hyperlinks in PDFs |
| `BookmarkView` | Bookmark/outline panel |
| `ThumbnailView` | Page thumbnail panel |
| `Print` | Print functionality |
| `TextSelection` | Select and copy text |
| `TextSearch` | Find text in document |
| `FormFields` | Interactive form field support |
| `FormDesigner` | Create and edit form fields |

---

## Reference File Routing

Use the table below to find the correct reference file for any feature request.

### Core Setup

| Reference File | Use When … |
|---|---|
| `basic-sample.md` | Getting started, minimal setup, loading a PDF |
| `general-properties.md` | Configuring server URL, locale, width/height, resourceUrl |
| `enable-properties.md` | Enabling/disabling toolbar, annotations, forms, download, print |

### Navigation

| Reference File | Use When … |
|---|---|
| `page-navigation.md` | Go to first/last/next/previous page or a specific page number |
| `bookmark-navigation.md` | Navigate via bookmarks or open/close bookmark panel |
| `thumbnail-navigation.md` | Display or navigate with the thumbnail panel |
| `hyperlink-navigation.md` | Configure clickable hyperlinks and external URL behavior |

### Viewing & Interaction

| Reference File | Use When … |
|---|---|
| `magnification.md` | Zoom controls, fit-to-page, fit-to-width, zoom levels |
| `interaction-mode.md` | Switch between text-selection and panning modes |
| `text-selection.md` | Enable/handle text selection and copy events |
| `text-search.md` | Implement in-document text search and result highlighting |

### Toolbar & Context Menu

| Reference File | Use When … |
|---|---|
| `toolbar-settings.md` | Customize toolbar items, visibility, and tooltip behavior |
| `toolbar-methods.md` | Show/hide toolbars programmatically at runtime |
| `contextmenu.md` | Add, remove, or handle right-click context menu items |

### Annotations

| Reference File | Use When … |
|---|---|
| `annotation-settings.md` | Set default annotation colors, opacity, author, styles |
| `annotation-events.md` | Handle annotation add/delete/move/resize/select events |
| `shape-label-settings.md` | Customize labels on shape and measure annotations |
| `redaction-annotation.md` | Create and apply redactions to remove sensitive content |

### Forms

| Reference File | Use When … |
|---|---|
| `form-field-settings.md` | Configure default properties for text, checkbox, radio, dropdown, signature fields |
| `form-field-events.md` | Handle form field focus, blur, and value-change events |

### Document Actions

| Reference File | Use When … |
|---|---|
| `download.md` | Enable download and set custom filenames |
| `print.md` | Configure and trigger printing |
| `organize-pages.md` | Reorder, rotate, insert, remove, or merge pages |

### Advanced / API

| Reference File | Use When … |
|---|---|
| `api-methods.md` | Load documents programmatically, export form data, undo/redo, extract text |
| `events.md` | Browse all available PDF Viewer events and their signatures |

---

## Metadata

| Field | Value |
|---|---|
| **Skill Name** | `syncfusion-angular-pdf-viewer` |
| **Author** | Syncfusion Inc |
| **Version** | `1.0.0` |
| **Category** | Document Viewing |
| **Framework** | Angular |
| **Reference Files** | 25 |
