# Enable Properties in Vue Syncfusion PDFViewer Component

## Table of Contents
- [When to Use This Guide](#when-to-use-this-guide)
- [Overview](#overview)
- [Decision Workflow: Choosing Enable Properties](#decision-workflow-choosing-enable-properties)
  - [Step 1: Capture User Intent](#step-1-capture-user-intent)
  - [Step 2: Tune for Performance](#step-2-tune-for-performance)
- [Basic Usage Pattern](#basic-usage-pattern)
- [Common Configuration Scenarios](#common-configuration-scenarios)
  - [Scenario 1: Read-Only Document Viewer](#scenario-1-read-only-document-viewer)
  - [Scenario 2: Annotation-Focused Reviewer](#scenario-2-annotation-focused-reviewer)
  - [Scenario 3: Form Filling Workspace](#scenario-3-form-filling-workspace)
  - [Scenario 4: Mobile-First Viewer](#scenario-4-mobile-first-viewer)
  - [Scenario 5: Full-Featured Editor](#scenario-5-full-featured-editor)
- [Enable Properties Reference](#enable-properties-reference)
- [Property Groupings by Feature Area](#property-groupings-by-feature-area)
  - [Core Navigation & UI](#core-navigation--ui)
  - [Text Features](#text-features)
  - [Zoom & Magnification](#zoom--magnification)
  - [Annotation Features (Core)](#annotation-features-core)
  - [Annotation Types](#annotation-types)
  - [Form Features](#form-features)
  - [Document Actions](#document-actions)
  - [Advanced Editing](#advanced-editing)
  - [Accessibility & Localization](#accessibility--localization)
  - [Performance & Persistence](#performance--persistence)
  - [Import & Advanced Features](#import--advanced-features)
- [Feature Dependencies](#feature-dependencies)
  - [Annotation Dependencies](#annotation-dependencies)
  - [Form Dependencies](#form-dependencies)
- [Edge Cases & Troubleshooting](#edge-cases--troubleshooting)
- [Performance Recommendations](#performance-recommendations)
- [Related References](#related-references)

## When to Use This Guide

Point Vue teams to this reference when they need to:
- Shape the PDF Viewer surface area to match product requirements
- Ship trimmed-down viewers for performance or security goals
- Assemble role-specific viewers (reviewer, form filler, editor)
- Enforce restrictions such as no print/download/text selection
- Turn on accessibility helpers or localization support
- Double-check that every available boolean API is represented in a configuration

## Overview

Every enable property is a boolean toggle on `ejs-pdfviewer`. Use them as building blocks to craft very focused viewers instead of enabling everything by default. Begin with a lean configuration, then selectively turn features on after confirming they are truly needed.

## Decision Workflow: Choosing Enable Properties

### Step 1: Capture User Intent

- **Read-only consumption?**
  - Turn on `enableToolbar`, `enableNavigation`, `enableTextSearch`, `enableMagnification`
  - Turn off annotation, form, download, and print toggles
- **Markup and review sessions?**
  - Enable `enableAnnotation`, `enableAnnotationToolbar`, `enableCommentPanel`
  - Switch on the specific annotation families (`enableTextMarkupAnnotation`, `enableShapeAnnotation`, `enableStickyNotesAnnotation`, etc.) that reviewers will actually use
- **Form interaction?**
  - Enable `enableFormFields`, `enableFormFieldsValidation`, `enableAutoComplete`, `enableHandwrittenSignature`
  - Leave `enableFormDesigner` off unless the user needs to author fields
- **Form authoring?**
  - Enable `enableFormDesigner`, `enableFormDesignerToolbar`, and keep `enableFormFields` active for testing
- **Document restructuring or sanitizing?**
  - Use `enablePageOrganizer` for page level edits
  - Use `enableRedactionToolbar` when redacting sensitive copy
- **Touch-first UX?**
  - Enable `enablePinchZoom`, set `enableDesktopMode` to `false`, and use `enableZoomOptimization`
- **Locked-down documents?**
  - Disable `enableDownload`, `enablePrint`, `enableTextSelection`, `enableLocalStorage`

### Step 2: Tune for Performance

- Minimal viewer (no authoring or heavy UI):
```vue
<ejs-pdfviewer
  :enableAnnotation="false"
  :enableFormDesigner="false"
  :enablePageOrganizer="false"
  :enableRedactionToolbar="false"
/>
```
- Mobile tuning:
```vue
<ejs-pdfviewer
  :enablePinchZoom="true"
  :enableZoomOptimization="true"
  :enableDesktopMode="false"
/>
```

## Basic Usage Pattern

```vue
<template>
  <ejs-pdfviewer
    id="viewer"
    :documentPath="documentPath"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enableTextSearch="true"
    :enableMagnification="true"
  />
</template>

<script setup>
import { PdfViewerComponent as EjsPdfviewer } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'document.pdf';
</script>
```

## Common Configuration Scenarios

### Scenario 1: Read-Only Document Viewer
*Goal: Pure viewing experience, no edits or extraction*

```vue
<template>
  <ejs-pdfviewer
    id="readonly"
    documentPath="document.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enableTextSearch="true"
    :enableMagnification="true"
    :enableThumbnail="true"
    :enableBookmark="true"
    :enableDownload="false"
    :enablePrint="false"
    :enableTextSelection="false"
    :enableAnnotation="false"
    :enableFormDesigner="false"
  />
</template>
```

### Scenario 2: Annotation-Focused Reviewer
*Goal: Reviewers annotate with markup, sticky notes, and comments*

```vue
<template>
  <ejs-pdfviewer
    id="reviewer"
    documentPath="annotate.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enableAnnotation="true"
    :enableAnnotationToolbar="true"
    :enableCommentPanel="true"
    :enableTextMarkupAnnotation="true"
    :enableStickyNotesAnnotation="true"
    :enableShapeAnnotation="true"
    :enableFreeText="true"
    :enableDownload="true"
  />
</template>
```

### Scenario 3: Form Filling Workspace
*Goal: Users complete and validate existing forms*

```vue
<template>
  <ejs-pdfviewer
    id="forms"
    documentPath="form.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enableFormFields="true"
    :enableFormFieldsValidation="true"
    :enableAutoComplete="true"
    :enableHandwrittenSignature="true"
    :enableDownload="true"
    :enablePrint="true"
  />
</template>
```

### Scenario 4: Mobile-First Viewer
*Goal: Responsive canvas for tablets and phones*

```vue
<template>
  <ejs-pdfviewer
    id="mobile"
    documentPath="device.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enablePinchZoom="true"
    :enableZoomOptimization="true"
    :enableDesktopMode="false"
    :enableMagnification="true"
    :enableThumbnail="true"
  />
</template>
```

### Scenario 5: Full-Featured Editor
*Goal: Give power users every major editing surface*

```vue
<template>
  <ejs-pdfviewer
    id="editor"
    documentPath="workspace.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :enableToolbar="true"
    :enableNavigation="true"
    :enableAnnotation="true"
    :enableAnnotationToolbar="true"
    :enableCommentPanel="true"
    :enableFormDesigner="true"
    :enableFormDesignerToolbar="true"
    :enableFormFields="true"
    :enablePageOrganizer="true"
    :enableRedactionToolbar="true"
    :enableDownload="true"
    :enablePrint="true"
    :enableTextSearch="true"
  />
</template>
```

## Enable Properties Reference

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **enableAccessibilityTags** | Toggle accessibility tags inside the PDF for assistive tooling. | `boolean` |
| **enableAnnotation** | Master switch for the annotation subsystem. | `boolean` |
| **enableAnnotationToolbar** | Shows or hides the annotation toolbar surface. | `boolean` |
| **enableAutoComplete** | Enables form field auto-completion in the viewer. | `boolean` |
| **enableBookmark** | Controls bookmark panel visibility for outline navigation. | `boolean` |
| **enableBookmarkStyles** | Allows bookmark styling capabilities within the panel. | `boolean` |
| **enableCommentPanel** | Displays the threaded comments pane for annotations. | `boolean` |
| **enableDesktopMode** | Forces desktop-oriented interaction patterns. | `boolean` |
| **enableDownload** | Determines whether end users can download the PDF. | `boolean` |
| **enableFormDesigner** | Exposes the form designer surface for creating fields. | `boolean` |
| **enableFormDesignerToolbar** | Shows the toolset dedicated to form design actions. | `boolean` |
| **enableFormFields** | Allows interaction with existing form fields. | `boolean` |
| **enableFormFieldsValidation** | Turns on validation behavior for form fields. | `boolean` |
| **enableFreeText** | Provides the free text annotation tool. | `boolean` |
| **enableHandwrittenSignature** | Lets users sign documents with handwritten signatures. | `boolean` |
| **enableHyperlink** | Enables link activation within the PDF. | `boolean` |
| **enableImportAnnotationMeasurement** | Allows importing measurement annotations from external data. | `boolean` |
| **enableInkAnnotation** | Enables freehand ink drawing on the document. | `boolean` |
| **enableLocalStorage** | Persists viewer state locally between sessions. | `boolean` |
| **enableMagnification** | Provides zoom in/out controls. | `boolean` |
| **enableMeasureAnnotation** | Activates measurement annotations for distance/area. | `boolean` |
| **enableMultiLineOverlap** | Handles overlap scenarios for multi-line text markup. | `boolean` |
| **enableMultiPageAnnotation** | Allows annotations to span across multiple pages. | `boolean` |
| **enableNavigation** | Enables core page navigation shortcuts. | `boolean` |
| **enableNavigationToolbar** | Shows the dedicated navigation toolbar. | `boolean` |
| **enablePageOrganizer** | Turns on page insert, reorder, and delete tools. | `boolean` |
| **enablePersistence** | Persists viewer state for later restoration. | `boolean` |
| **enablePinchZoom** | Enables pinch gestures on touch hardware. | `boolean` |
| **enablePrint** | Allows printing from the viewer. | `boolean` |
| **enablePrintRotation** | Adds page rotation support inside the print flow. | `boolean` |
| **enableRedactionToolbar** | Enables the redaction toolbar for masking content. | `boolean` |
| **enableRtl** | Enables right-to-left language layout. | `boolean` |
| **enableShapeAnnotation** | Turns on geometric annotation tools. | `boolean` |
| **enableShapeLabel** | Adds label support to shape annotations. | `boolean` |
| **enableStampAnnotations** | Provides predefined stamp annotations. | `boolean` |
| **enableStickyNotesAnnotation** | Enables sticky note comment annotations. | `boolean` |
| **enableTextMarkupAnnotation** | Activates highlight, underline, and strikethrough. | `boolean` |
| **enableTextMarkupResizer** | Lets users resize text markup anchors. | `boolean` |
| **enableTextSearch** | Enables search within the PDF text layer. | `boolean` |
| **enableTextSelection** | Allows text selection and copying. | `boolean` |
| **enableThumbnail** | Shows the thumbnail pane for page previews. | `boolean` |
| **enableToolbar** | Displays the primary toolbar. | `boolean` |
| **enableZoomOptimization** | Optimizes rendering across zoom levels. | `boolean` |

## Property Groupings by Feature Area

### Core Navigation & UI
- `enableToolbar` – general command bar
- `enableNavigation` – essential navigation logic
- `enableNavigationToolbar` – pagination-focused toolbar
- `enableThumbnail` – thumbnail rail
- `enableBookmark` – bookmark outline viewer

Use these for almost every viewer. Only omit when embedding the canvas inside a tightly controlled layout.

### Text Features
- `enableTextSearch` – text lookup box
- `enableTextSelection` – highlight/copy text
- `enableHyperlink` – activate embedded links

Disable text selection for rights-managed PDFs while still allowing navigation.

### Zoom & Magnification
- `enableMagnification`
- `enablePinchZoom`
- `enableZoomOptimization`

These three properties collaborate to make zooming comfortable on both desktop and touch screens.

### Annotation Features (Core)
- `enableAnnotation`
- `enableAnnotationToolbar`
- `enableCommentPanel`

`enableAnnotation` is the critical parent toggle—leave it off and every other annotation property becomes irrelevant.

### Annotation Types
- `enableTextMarkupAnnotation`
- `enableTextMarkupResizer`
- `enableStickyNotesAnnotation`
- `enableShapeAnnotation`
- `enableShapeLabel`
- `enableFreeText`
- `enableInkAnnotation`
- `enableStampAnnotations`
- `enableMeasureAnnotation`
- `enableMultiPageAnnotation`
- `enableMultiLineOverlap`

Pick only the annotation families your reviewers require to keep the UI tidy.

### Form Features
- `enableFormFields`
- `enableFormFieldsValidation`
- `enableAutoComplete`
- `enableFormDesigner`
- `enableFormDesignerToolbar`

`enableFormFields` should be on for any workflow that interacts with form inputs. The designer toggles are exclusive to builders.

### Document Actions
- `enableDownload`
- `enablePrint`
- `enablePrintRotation`

Disable these when you need to restrict data exfiltration.

### Advanced Editing
- `enablePageOrganizer`
- `enableRedactionToolbar`
- `enableHandwrittenSignature`

These tools are heavier and should be reserved for power-user surfaces.

### Accessibility & Localization
- `enableAccessibilityTags`
- `enableRtl`
- `enableBookmarkStyles`

Turn them on for compliance or RTL experiences.

### Performance & Persistence
- `enableLocalStorage`
- `enablePersistence`
- `enableDesktopMode`

Use `enableLocalStorage` and `enablePersistence` to restore session state. Disable `enableDesktopMode` for mobile-first screens.

### Import & Advanced Features
- `enableImportAnnotationMeasurement`

This is only necessary when bringing in measurement data created elsewhere.

## Feature Dependencies

### Annotation Dependencies
```
enableAnnotation
  ├── enableAnnotationToolbar
  ├── enableCommentPanel
  ├── enableTextMarkupAnnotation
  │     └── enableTextMarkupResizer
  ├── enableStickyNotesAnnotation
  ├── enableShapeAnnotation
  │     └── enableShapeLabel
  ├── enableFreeText
  ├── enableInkAnnotation
  ├── enableStampAnnotations
  └── enableMeasureAnnotation
```

### Form Dependencies
```
enableFormFields
  ├── enableFormFieldsValidation
  └── enableAutoComplete

enableFormDesigner
  └── enableFormDesignerToolbar
```

## Edge Cases & Troubleshooting

- **Annotation toolbar missing**: Confirm both `enableAnnotation` and `enableAnnotationToolbar` are `true`.
- **Viewer feels slow with large PDFs**: Trim unused annotation types, disable `enablePageOrganizer`/`enableFormDesigner`, and allow `enableZoomOptimization`.
- **Pinch gestures inactive on tablets**: Ensure `enablePinchZoom` is enabled and `enableDesktopMode` is `false`.
- **Download intentionally unavailable**: When `enableDownload` is `false`, consider server-side workflows for delivering approved exports.

## Performance Recommendations

1. Start with the smallest possible surface area, then add toggles as requirements harden.
2. Revisit heavy properties (`enableAnnotation`, `enableFormDesigner`, `enablePageOrganizer`) on low-powered devices.
3. Test with long documents (100+ pages) while monitoring memory.
4. Combine `enableZoomOptimization` with disabled unused features to keep rendering responsive.

## Related References

- [basic-sample.md](./basic-sample.md)
- [general-properties.md](./general-properties.md)
- [annotation-settings.md](./annotation-settings.md)
- [form-field-settings.md](./form-field-settings.md)
