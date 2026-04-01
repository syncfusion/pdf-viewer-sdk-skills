# Annotation Events

Description: Annotation events for the Syncfusion PDF Viewer (Vue) notify your app when annotations are created, changed, moved, resized, selected, or removed. Use these hooks to implement logging, validation, custom UI updates, or backend synchronization.

Table of Contents
- When to use
- Picking the right event
- Using events in Vue
- Events reference (complete list)
- Annotation object summary
- Common usage patterns

---

When to use

- Track user edits and build audit trails.
- Run business validation before allowing annotations.
- Update custom property panes, toolbars, or lists when selection changes.
- Sync annotation changes to a server or shared session.

Picking the right event

- Need to stop an action? Use a "before" event that supports cancellation (see `beforeAddFreeText`).
- Want the final state after a user finishes an action? Use the lifecycle events (e.g., `annotationAdd`, `annotationMove`, `annotationRemove`).
- Need real-time feedback while dragging/resizing? Use the in-progress events like `annotationMoving`.

---

Using events in Vue

Example: register handlers on the PDF Viewer component using Vue event listeners.

```vue
<template>
  <ejs-pdfviewer
    @annotationAdd="handleAnnotationAdd"
    @annotationSelect="handleAnnotationSelect"
    @annotationMove="handleAnnotationMove"
  />
</template>

<script setup>
import { ref } from 'vue'

const handleAnnotationAdd = (args) => { console.log('annotation added', args) }
const handleAnnotationSelect = (args) => { console.log('selected', args) }
const handleAnnotationMove = (args) => { console.log('moved', args) }
</script>
```

Use the handler `args` to access `annotationId`, `pageIndex`, and the full `annotation` object when provided.

---

Events reference (Vue)

The following events are supported. Each entry lists when it fires and the useful properties available on the event `args` object.

- `annotationAdd` — Fires after an annotation is added. Args: `annotationId`, `pageIndex`, `annotation`, `annotationAddMode`.
- `annotationDoubleClick` — Fires on double-clicking an annotation. Args: `annotationId`, `pageIndex`, `annotation`.
- `annotationMouseLeave` — Mouse left an annotation. Args: `annotationId`, `pageIndex`.
- `annotationMouseover` — Mouse entered an annotation. Args: `annotationId`, `pageIndex`, `X`, `Y`.
- `annotationMove` — Fires after an annotation move completes. Args: `annotationId`, `pageIndex`, `annotation` (updated).
- `annotationMoving` — Fires continuously while an annotation moves. Args: `annotationId`, `pageIndex`, `currentPosition`.
- `annotationPropertiesChange` — Annotation property changes. Args include `annotationId`, `pageIndex`, boolean flags such as `isColorChanged`, `isThicknessChanged`, `isOpacityChanged`, plus `annotation`.
- `annotationRemove` — Fires when an annotation is removed. Args: `annotationId`, `pageIndex`, `annotation` (removed object).
- `annotationResize` — Fires after resize completes. Args: `annotationId`, `pageIndex`, `annotation` (with new bounds).
- `annotationSelect` — Fires when annotation(s) are selected. Args: `annotationId`, `pageIndex`, `annotation`, `annotationCollection`, `isMultiSelect`.
- `annotationUnSelect` — Fires when an annotation is unselected. Args: `annotationId`, `pageIndex`.
- `beforeAddFreeText` — Fires before a free-text annotation is created; supports cancellation via `args.cancel = true`. Args: `pageIndex`, `cancel`.
- `addSignature` — Fired when a signature is added. Args: `pageIndex`, `signature` (object).
- `removeSignature` — Fired when a signature is deleted. Args: `pageIndex`, `signature`.
- `resizeSignature` — Fires after signature resize. Args: `pageIndex`, `signature`, `previousPosition`, `currentPosition`.
- `signaturePropertiesChange` — Signature property changes. Args: `pageIndex`, `isThicknessChanged`, `isOpacityChanged`, `isStrokeColorChanged`, `signature`.
- `signatureSelect` — Signature selected. Args: `pageIndex`, `signature`.
- `signatureUnselect` — Signature unselected. Args: `pageIndex`, `signature`.

Ensure your Vue handlers inspect the `args` object to determine the annotation type and the properties that are present.

---

Annotation object summary

When handlers expose an `annotation` object, it contains both general and type-specific properties. Not every property appears on every annotation type — check `type`/`subType` first.

Core properties you can expect (commonly available):

- `annotationId` / `id` / `randomId` — identifiers.
- `author`, `creationDate`, `modifiedDate`.
- `pageNumber` / `pageIndex`.
- `type`, `subType`, `shapeAnnotationType`.
- Visual properties: `color`, `strokeColor`, `fillColor`, `opacity`, `thickness`, `isLocked`, `isPrint`.
- Geometry: `bounds` (x,y,width,height,left,top,right), `rect` (left,top,right,bottom,height,width), `vertexPoints` for polygons.
- `annotationAddMode`, `customData`, `comments`, `review`.

Type-specific highlights

- Text markup (`type: "TextMarkup"`): `textMarkupContent`, `textMarkupStartIndex`, `textMarkupEndIndex`.
- FreeText: `content`, `dynamicText`, `fontFamily`, `textAlign`, `font` object.
- Ink: `data` (path/SVG data).
- Shape/Measure: `caption`, `captionPosition`, `labelContent`, `labelBounds`, `calibrate`.
- Stamp: `icon`, `customStampName`, `isDynamicStamp`, `stampAnnotationPath`.

Nested objects you will commonly access

- Rect: `{ left, top, right, bottom, width, height }`.
- Bounds: `{ x, y, left, top, right, width, height }`.
- Review: `{ state, stateModel, author, modifiedDate }`.
- AnnotationSettings: `{ isLock, isPrint, maxHeight, maxWidth, minHeight, minWidth }`.
- AnnotationSelectorSettings: selection handle and border styling.
- LabelSettings: label `borderColor`, `fillColor`, `fontColor`, `fontSize`, `opacity`.

---

Common usage patterns (Vue examples)

1) Audit logging on add/move/remove

```js
const onAnnotationAdd = (args) => {
  sendTelemetry('annotation.add', { id: args.annotationId, page: args.pageIndex, time: new Date().toISOString() })
}

const onAnnotationMove = (args) => {
  sendTelemetry('annotation.move', { id: args.annotationId, page: args.pageIndex })
}

const onAnnotationRemove = (args) => {
  sendTelemetry('annotation.remove', { id: args.annotationId, page: args.pageIndex })
}
```

2) Preventing free-text on certain pages

```js
const onBeforeAddFreeText = (args) => {
  if (args.pageIndex === 0) { // e.g., cover page
    args.cancel = true
    // show message to user
  }
}
```

3) Properties panel for the selected annotation

```js
const onAnnotationSelect = (args) => {
  const ann = args.annotation
  // populate UI with ann.color, ann.opacity, ann.bounds, etc.
}
```

4) Bulk operations when multiple annotations are selected

```js
const onAnnotationSelect = (args) => {
  if (args.isMultiSelect) {
    args.annotationCollection.forEach(a => applyBulkChange(a.annotationId))
  }
}
```

---

Tips

- Always check the `type` before reading type-specific fields.
- For validations that must stop an action, prefer `before*` events (only `beforeAddFreeText` supports cancellation today).
- Use `annotationPropertiesChange` to react to fine-grained property edits — it includes boolean flags to indicate what changed.
