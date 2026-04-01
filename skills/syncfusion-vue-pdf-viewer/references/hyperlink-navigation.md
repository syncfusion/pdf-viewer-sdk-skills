# Hyperlink Navigation

Brief: Configure how the Syncfusion Vue PDF Viewer identifies, opens, and monitors hyperlinks inside a document. Toggle link interactivity, decide where external URLs launch, and react to hyperlink events for custom UX logic.

---

## Table of Contents
- [Enable or Disable Hyperlinks](#enable-or-disable-hyperlinks)
- [Choose the Target Tab](#choose-the-target-tab)
- [Hyperlink Events](#hyperlink-events)
- [Complete Vue Example](#complete-vue-example)

---

## Enable or Disable Hyperlinks

Stop users from following links without modifying the underlying PDF.

### Property
`enableHyperlink`

### Type
`boolean`

### Default
`true`

### Behavior
When `true`, the viewer scans loaded pages and turns every detected hyperlink into a clickable anchor. Set it to `false` to render links as plain text so that reviewers can focus on document content without accidental navigation.

### Vue Usage
```html
<template>
  <ejs-pdfviewer
    id="pdfViewer"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    :enableHyperlink="false"
    style="height: 640px">
  </ejs-pdfviewer>
</template>
```

> Disabling hyperlinks only affects the runtime behavior of the viewer instance. The PDF file itself stays unchanged.

---

## Choose the Target Tab

Tell the viewer whether to open external URLs beside or on top of the current tab.

### Property
`hyperlinkOpenState`

### Type
`'CurrentTab' | 'NewTab'`

### Default
`'CurrentTab'`

### Behavior
`'CurrentTab'` reuses the hosting browser tab. Pick `'NewTab'` when reviewers should stay inside the PDF session while inspecting external resources, such as annotation guidelines or legal references.

### Vue Usage
```html
<template>
  <ejs-pdfviewer
    id="pdfViewer"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    hyperlinkOpenState="NewTab"
    style="height: 640px">
  </ejs-pdfviewer>
</template>
```

---

## Hyperlink Events

Hook into hyperlink interactions for logging, validation, or custom tooltips.

### `hyperlinkClick`
Fires when a user activates a hyperlink.

**Event args**
- `hyperlink: string` – URL extracted from the PDF content.
- `cancel: boolean` – Assign `true` to keep the viewer from navigating to the link target.

**Usage**
```ts
const handleHyperlinkClick = (args: any) => {
  console.info('Clicked link:', args.hyperlink);

  if (!args.hyperlink.includes('trusted-domain.com')) {
    args.cancel = true; // block navigation
    alert('Navigation blocked: untrusted link');
  }
};
```

### `hyperlinkMouseOver`
Runs when the pointer hovers over a hyperlink area.

**Event args**
- `hyperlinkElement: HTMLAnchorElement` – DOM node representing the hyperlink so you can read the final URL or apply styles.

**Usage**
```ts
const handleHyperlinkMouseOver = (args: any) => {
  console.debug('Preview link:', args.hyperlinkElement.href);
};
```

Attach both handlers with standard Vue event syntax:
```html
<ejs-pdfviewer
  @hyperlinkClick="handleHyperlinkClick"
  @hyperlinkMouseOver="handleHyperlinkMouseOver"
  ...>
</ejs-pdfviewer>
```

---

## Complete Vue Example

```html
<template>
  <div class="viewer-wrapper">
    <ejs-pdfviewer
      id="pdfViewer"
      :documentPath="documentPath"
      :resourceUrl="resourceUrl"
      :enableHyperlink="true"
      hyperlinkOpenState="NewTab"
      @hyperlinkClick="onHyperlinkClick"
      @hyperlinkMouseOver="onHyperlinkMouseOver"
      style="height: 640px">
    </ejs-pdfviewer>
  </div>
</template>

<script>
import { PdfViewerComponent, LinkAnnotation, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'HyperlinkViewer',
  components: {
    'ejs-pdfviewer': PdfViewerComponent
  },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
      resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib'
    };
  },
  provide: {
    PdfViewer: [Toolbar, LinkAnnotation]
  },
  methods: {
    onHyperlinkClick(args) {
      console.log('User clicked:', args.hyperlink);
      if (!args.hyperlink.includes('trusted-domain.com')) {
        args.cancel = true;
        alert('Only trusted-domain.com links are allowed.');
      }
    },
    onHyperlinkMouseOver(args) {
      console.log('Hover:', args.hyperlinkElement.href);
    }
  }
};
</script>

<style>
.viewer-wrapper {
  max-width: 960px;
  margin: 0 auto;
}
</style>
```

### Configuration Checklist
- Use `enableHyperlink` to turn detection on or off per viewer instance.
- Set `hyperlinkOpenState` to keep readers in the same tab or spawn a new one.
- Subscribe to `hyperlinkClick` for validation or auditing and cancel unwanted destinations.
- Subscribe to `hyperlinkMouseOver` for tooltip text, status bar updates, or analytics.
