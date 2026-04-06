# Toolbar Settings

## Table of Contents
- [When to Use Toolbar Configurations](#when-to-use-toolbar-configurations)
- [Primary Toolbar](#primary-toolbar)
- [Annotation Toolbar](#annotation-toolbar)
- [Form Designer Toolbar](#form-designer-toolbar)
- [Organize Pages Toolbar](#organize-pages-toolbar)
- [Mobile Toolbar](#mobile-toolbar)
- [Custom Toolbar](#custom-toolbar)
- [ToolbarSettings Configuration](#comprehensive-toolbarsettings-configuration)
- [Toolbar Events](#toolbar-events)
- [Implementation Patterns](#implementation-patterns)

---

## When to Use Toolbar Configurations

Match toolbar scope to the experience you are shipping:

**Read-only viewers** → Keep the primary toolbar enabled with the essentials (`OpenOption`, `PrintOption`, `DownloadOption`, `MagnificationTool`, `PageNavigationTool`).

**Annotation-centric flows** → Combine the primary toolbar with an annotation toolbar, trimming `annotationToolbarItems` to only the markup tools reviewers need.

**Form creation projects** → Turn on the designer surface with `:isFormDesignerToolbarVisible="true"` and add field tools such as `TextboxTool`, `CheckBoxTool`, or `DropdownTool`.

**Document curation/merge tasks** → Enable `pageOrganizerSettings` permissions (insert, delete, rotate, copy, import, rearrange) that match the user's role.

**Touch-first devices** → Use `:enableDesktopMode="true"` plus `:enableTextSelection="false"` for smoother gestures and consistent tool placement.

**Branded experiences** → Switch off the stock toolbar (`:enableToolbar="false"`) and plug in a custom EJ2 Toolbar component tied to the viewer APIs.

---

## Primary Toolbar

The primary toolbar hosts core navigation, magnification, open/print/download, and high-level editing entry points. Tailor it so only relevant controls remain.

### Controlling Toolbar Visibility

**API**: `enableToolbar: boolean` (default `true`)

Hide the toolbar up front or toggle it later by calling the toolbar module.

```vue
<template>
  <ejs-pdfviewer ref="viewer" :enableToolbar="false" />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { PdfViewerComponent as EjsPdfviewer } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);

onMounted(() => {
  viewer.value?.toolbar.showToolbar(false); // runtime toggle
});
</script>
```

### Configuring Toolbar Items

**API**: `toolbarItems: ToolbarItem[] | (ToolbarItem | CustomToolbarItem)[]`

Only the entries you list render, so arrange the array in the exact order you expect the buttons to appear.

| Item | Purpose | Include When |
|------|---------|--------------|
| `OpenOption` | Open dialog | Users load files manually |
| `DownloadOption` | Download PDF | Save-to-disk scenarios |
| `PrintOption` | Print dialog | Hard-copy workflows |
| `MagnificationTool` | Zoom slider + buttons | Detailed technical drawings |
| `PageNavigationTool` | Page number box + arrows | Multi-page files |
| `SearchOption` | Text search | Long or legal documents |
| `UndoRedoTool` | Undo/redo | Annotation or form edits |
| `PanTool` | Pan mode | Large canvases |
| `SelectionTool` | Text/object selection | Copy/paste is required |
| `CommentTool` | Comments pane | Collaborative review |
| `SubmitForm` | Submit button | Connected form workflows |
| `AnnotationEditTool` | Annotation edit switch | Advanced markup |
| `FormDesignerEditTool` | Form designer switch | Building forms |
| `FreeTextAnnotationOption` | Free text tool | Text callouts |
| `InkAnnotationOption` | Ink tool | Stylus drawing |
| `ShapeAnnotationOption` | Shape gallery | Diagramming |
| `StampAnnotation` | Stamp picker | Approval stamps |
| `SignatureOption` | Signature dialog | Signing pipelines |

**Simple viewer example**

```vue
<ejs-pdfviewer
  :toolbarSettings="{
    toolbarItems: ['OpenOption', 'PrintOption', 'DownloadOption', 'MagnificationTool', 'PageNavigationTool']
  }"
/>
```

**Editor-focused configuration**

```vue
<ejs-pdfviewer
  :toolbarSettings="{
    toolbarItems: [
      'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'SearchOption',
      'MagnificationTool', 'AnnotationEditTool', 'FormDesignerEditTool',
      'PrintOption', 'DownloadOption'
    ]
  }"
/>
```

---

## Annotation Toolbar

Launches whenever annotation mode is active. Keep it lean so reviewers only see the markup tools they recognize.

### Controlling Annotation Toolbar Visibility

**API**: `toolbar.showAnnotationToolbar(isVisible: boolean)`

```vue
<template>
  <ejs-pdfviewer ref="viewer" />
  <button @click="toggleAnnotation(true)">Annotate</button>
  <button @click="toggleAnnotation(false)">Close</button>
</template>

<script setup>
import { ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const toggleAnnotation = (show) => viewer.value?.toolbar.showAnnotationToolbar(show);
</script>
```

### Configuring Annotation Tools

**API**: `annotationToolbarItems: AnnotationToolbarItem[]`

| Tool | Purpose |
|------|---------|
| `HighlightTool` | Highlight text |
| `UnderlineTool` | Underline |
| `StrikethroughTool` | Strike edits |
| `SquigglyTool` | Wavy underline |
| `ColorEditTool` | Change color |
| `OpacityEditTool` | Adjust transparency |
| `AnnotationDeleteTool` | Remove selected markup |
| `StampAnnotationTool` | Insert stamps |
| `HandWrittenSignatureTool` | Freehand signature |
| `InkAnnotationTool` | Freehand drawing |
| `ShapeTool` | Rectangle, circle, arrow, etc. |
| `CalibrateTool` | Measurement calibration |
| `StrokeColorEditTool` | Outline color |
| `ThicknessEditTool` | Stroke thickness |
| `FreeTextAnnotationTool` | Text box |
| `FontFamilyAnnotationTool` | Font family |
| `FontSizeAnnotationTool` | Font size |
| `FontStylesAnnotationTool` | Bold/italic |
| `FontAlignAnnotationTool` | Text alignment |
| `FontColorAnnotationTool` | Text color |
| `CommentPanelTool` | Toggle comments pane |

```vue
<ejs-pdfviewer
  :toolbarSettings="{
    annotationToolbarItems: [
      'HighlightTool', 'UnderlineTool', 'StrikethroughTool',
      'ColorEditTool', 'OpacityEditTool', 'AnnotationDeleteTool', 'CommentPanelTool'
    ]
  }"
/>
```

---

## Form Designer Toolbar

Show this toolbar only while users are creating or editing interactive form fields.

### Controlling Visibility

**API**: `isFormDesignerToolbarVisible: boolean`

```vue
<ejs-pdfviewer :isFormDesignerToolbarVisible="true" />
```

At runtime toggle with `viewerRef.value.isFormDesignerToolbarVisible = false`.

### Configuring Form Field Tools

**API**: `formDesignerToolbarItems: FormDesignerToolbarItem[]`

| Tool | Purpose |
|------|---------|
| `TextboxTool` | Single-line or multiline text |
| `PasswordTool` | Obscured text |
| `CheckBoxTool` | Boolean choice |
| `RadioButtonTool` | Single selection among options |
| `DropdownTool` | Compact list |
| `ListboxTool` | Multi-select list |
| `DrawSignatureTool` | Signature box |
| `DeleteTool` | Remove selected field |

```vue
<ejs-pdfviewer
  :isFormDesignerToolbarVisible="true"
  :toolbarSettings="{ formDesignerToolbarItems: ['TextboxTool', 'CheckBoxTool', 'DeleteTool'] }"
/>
```

---

## Organize Pages Toolbar

`pageOrganizerSettings` restricts which structural actions (insert/delete/rotate/copy/import/rearrange) are exposed in the page organizer UI.

| Property | Purpose | Default |
|----------|---------|---------|
| `canInsert` | Allow inserting blank pages | `true` |
| `canDelete` | Allow removing pages | `true` |
| `canRotate` | Enable clockwise/counter rotation | `true` |
| `canCopy` | Duplicate existing pages | `true` |
| `canImport` | Pull pages from another PDF | `true` |
| `canRearrange` | Drag-and-drop reorder | `true` |
| `showImageZoomingSlider` | Thumbnail zoom slider | `true` |

```vue
<ejs-pdfviewer
  :pageOrganizerSettings="{
    canInsert: false,
    canDelete: false,
    canRotate: false,
    canCopy: false,
    canImport: false,
    canRearrange: false,
    showImageZoomingSlider: true
  }"
/>
```

---

## Mobile Toolbar

Switch between the condensed touch toolbar and the desktop ribbon.

**API**: `enableDesktopMode: boolean`

```vue
<ejs-pdfviewer
  :enableDesktopMode="true"
  :enableTextSelection="false"  
/>
```

Recommendations:
- Disabling text selection smooths out vertical scrolling on phones/tablets.
- Keep toolbar items minimal; mobile view prioritizes the first few items in the array.

---

## Custom Toolbar

Use a custom toolbar when the stock ribbon cannot represent the experience you are building:

- Product branding or accessibility rules block the default toolbar style.
- Workflows require bespoke commands such as "Send for Approval" or "Save to DMS".
- You need to merge built-in items with extra buttons or reorder beyond what `toolbarItems` allows.
- Integrations must launch external dialogs or services before calling viewer APIs.
- You want to expose only a handful of actions to keep mobile or kiosk layouts simple.

### Implementation Steps

1. **Disable the built-in toolbar** → Render `<ejs-pdfviewer :enableToolbar="false">` so the chrome disappears.
2. **Host an EJ2 Toolbar** → Place `<ejs-toolbar>` above/below the canvas and describe each button with `e-item` directives (or the `:items` prop).
3. **Inject viewer services** → Provide `Toolbar`, `Navigation`, `Magnification`, `Annotation`, `FormDesigner`, etc., so the viewer module plumbing still loads.
4. **Keep a viewer ref** → Capture `<ejs-pdfviewer ref="viewer">` to reach methods such as `navigation.goToNextPage()`, `print.print()`, or `magnification.fitToWidth()`.
5. **Handle `clicked` events** → Map every toolbar item `id` to a viewer API call or a downstream workflow, optionally cancelling the default behavior with `args.cancel = true`.

### Defining Custom Toolbar Items

Each `e-item` accepts an `id`, `prefixIcon`, optional `text`, alignment, and tooltip. Mix custom entries with built-in `ToolbarItem` values when you want to keep familiar buttons while introducing bespoke ones.

```vue
<template>
  <div class="pdf-shell">
    <ejs-toolbar @clicked="handleToolbarClick">
      <e-items>
        <e-item id="open_file" prefixIcon="e-icons e-folder" tooltipText="Open" align="Left" />
        <e-item id="previous_page" prefixIcon="e-icons e-chevron-left" align="Left" />
        <e-item id="next_page" prefixIcon="e-icons e-chevron-right" align="Left" />
        <e-item id="fit_width" text="Fit Width" align="Center" />
        <e-item id="print" prefixIcon="e-icons e-print" align="Right" />
        <e-item id="download" prefixIcon="e-icons e-download" align="Right" />
      </e-items>
    </ejs-toolbar>

    <ejs-pdfviewer ref="viewer" :enableToolbar="false" style="height: 640px" />
    <input id="fileUpload" type="file" class="hidden" />
  </div>
</template>

<script>
import { ToolbarComponent as EjsToolbar, ItemsDirective as EItems, ItemDirective as EItem } from '@syncfusion/ej2-vue-navigations';
import { PdfViewerComponent, Toolbar, Navigation, Magnification, Annotation, FormDesigner } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  components: {
    'ejs-toolbar': EjsToolbar,
    'e-items': EItems,
    'e-item': EItem,
    'ejs-pdfviewer': PdfViewerComponent
  },
  provide: {
    PdfViewer: [Toolbar, Navigation, Magnification, Annotation, FormDesigner]
  },
  methods: {
    handleToolbarClick(args) {
      const viewer = this.$refs.viewer?.ej2Instances;
      switch (args.item?.id) {
        case 'open_file':
          document.getElementById('fileUpload')?.click();
          break;
        case 'previous_page':
          viewer?.navigation.goToPreviousPage();
          break;
        case 'next_page':
          viewer?.navigation.goToNextPage();
          break;
        case 'fit_width':
          viewer?.magnification.fitToWidth();
          break;
        case 'print':
          viewer?.print.print();
          break;
        case 'download':
          viewer?.download();
          break;
      }
    }
  }
};
</script>
```

### Implementing Click Handler

`clicked` receives `args.item` for both custom ids and built-in toolbar entries. Cancel the default action when you need full control, or fall back to viewer APIs for built-ins you keep in the markup.

```javascript
const handleToolbarClick = (args) => {
  const viewer = this.$refs.viewer?.ej2Instances;
  if (args.item.id === 'approve_document') {
    args.cancel = true; // run workflow without viewer action
    launchApprovalFlow();
    return;
  }
  if (args.item.id === 'DownloadOption') {
    viewer?.download();
  }
};
```

**Key pattern**: Every toolbar item id maps to a viewer API (`navigation.*`, `print.*`, `magnification.*`, etc.) or a business workflow. Keep icon helpers like `e-icons e-folder`, `e-icons e-download`, `e-icons e-print`, `e-icons e-chevron-left`, `e-icons e-chevron-right`, `e-icons e-circle-add`, and `e-icons e-circle-remove` handy for consistent visuals.

---

## Comprehensive ToolbarSettings Configuration

`toolbarSettings` provides a single place to configure every toolbar surface.

| Property | Type | Purpose |
|----------|------|---------|
| `toolbarItems` | `ToolbarItem[]` | Primary toolbar composition |
| `showTooltip` | `boolean` | Global tooltip toggle |
| `annotationToolbarItems` | `AnnotationToolbarItem[]` | Annotation toolbar buttons |
| `formDesignerToolbarItems` | `FormDesignerToolbarItem[]` | Form field palette |
| `redactionToolbarItems` | `RedactionToolbarItem[]` | Redaction toolbar (standalone viewer) |

```vue
<ejs-pdfviewer
  :toolbarSettings="{
    toolbarItems: ['OpenOption', 'MagnificationTool', 'DownloadOption'],
    annotationToolbarItems: ['HighlightTool', 'InkAnnotationTool', 'AnnotationDeleteTool'],
    formDesignerToolbarItems: ['TextboxTool', 'RadioButtonTool'],
    redactionToolbarItems: ['TextRedactionTool', 'RectangleRedactionTool'],
    showTooltip: true
  }"
/>
```

Disable tooltips globally when hovering is not available:

```vue
<ejs-pdfviewer :toolbarSettings="{ showTooltip: false }" />
```

---

## Toolbar Events

Use `toolbarClick` to intercept button presses for auditing, confirmation dialogs, or custom routing.

```vue
<ejs-pdfviewer @toolbarClick="onToolbarClick" />
```

```javascript
const onToolbarClick = (args) => {
  if (args.item.id === 'DownloadOption') {
    trackAnalytics('pdf_download');
  }
  if (args.item.id === 'custom_action') {
    args.cancel = true; // stop default behavior
    launchWorkflow();
  }
};
```

`args.item.id` gives you the built-in button id or the id you supplied for a custom toolbar entry. Set `args.cancel = true` to block the default action.

---

## Implementation Patterns

- **Reader-Only Shell**: keep `enableToolbar` true but limit `toolbarItems` to open/print/download/navigation to maximize canvas space.
- **Markup Workbench**: preload annotation services, auto-show annotation toolbar after load, and expose color/thickness tools for reviewers.
- **Form Builder Studio**: enable `isFormDesignerToolbarVisible`, include every `formDesignerToolbarItems` entry, and listen for `toolbarClick` to log field creation.
- **Operations Dashboard**: pair page organizer permissions with a custom toolbar that fires bespoke commands (approve, reject, export) before calling viewer APIs.
- **Touch-Forward UI**: switch to desktop mode on tablets, hide seldom-used items, and disable tooltips.

---
