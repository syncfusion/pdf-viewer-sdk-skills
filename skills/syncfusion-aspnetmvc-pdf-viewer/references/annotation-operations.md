# Common Annotation Operations

## Selecting Annotations

**Programmatic selection:**

Select the annotations programmatically using annotation object or annotation Id using `selectAnnotation(annotationId)`

```javascript
function selectAnnotation(annotationId) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.selectAnnotation(annotationId);
}
```

### Parameter

| Parameter | Type | Description | Optional |
|---|---|---|---|
| annotationId | `string` or `object` | The annotation Id or the whole annotation that needs to be selected | No |

### Returns

`void`

---

## Moving and Resizing

**Programmatic repositioning:**

```javascript
function moveAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    for (let i = 0; i < viewer.annotationCollection.length; i++) {
        var annotation = viewer.annotationCollection[i];
        if (annotation.annotationId === targetId) {
            annotation.bounds.x = 150;
            annotation.bounds.y = 200;
            viewer.annotation.editAnnotation(annotation);
        }
    }
}
```

---

## Deleting Annotations

Delete the annotations programmatically using the `deleteAnnotationById(annotationId)` of the `annotation` module of PDF Viewer instance.

**Programmatic deletion:**

```javascript
function deleteAnnotation(annotationId) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.deleteAnnotationById(annotationId);
}
```

### Parameter

| Parameter | Type | Description | Optional |
|---|---|---|---|
| annotationId | `string` or `object` | The annotation Id or the whole annotation that needs to be deleted | No |

### Returns

`void`

---

## Locking Annotations

Locked annotations cannot be edited or deleted by users:

```javascript
function lockAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    for (let i = 0; i < viewer.annotationCollection.length; i++) {
        var annotation = viewer.annotationCollection[i];
        if (annotation.annotationId === targetId) {
            annotation.annotationSettings.isLock = true;
            viewer.annotation.editAnnotation(annotation);
        }
    }
}
```

## Importing and Exporting

Export annotations programmatically using the `exportAnnotation(AnnotationDataFormat)` method of PDF Viewer instance.

**Export annotations:**

```javascript
function exportAnnotations() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.exportAnnotation();
}
```

### Parameter

| Parameter | Type | Description | Optional |
|---|---|---|---|
| annotationDataFormat | [`AnnotationDataFormat`](#annotationdataformat) | The annotation data that needs to be imported | Yes |

### Returns

`void`

### Returns

`void`

**Import annotations:**

Import annotations using `importAnnotation(importData, AnnotationDataFormat)` method of PDF Viewer instance

```javascript
function importAnnotations(annotationData) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.importAnnotation(annotationData);
}
```

### Parameter

| Parameter | Type | Description | Optional |
|---|---|---|---|
| importData | `any` | The annotation data that needs to be imported | No |
| annotationDataFormat | [`AnnotationDataFormat`](#annotationdataformat) | The annotation data that needs to be imported | Yes |

### Returns

`void`

---

## AnnotationDataFormat

Types for annotation file types

- `Json`
- `Xfdf`

### Type

`string`