## Common Annotation Operations

### Selecting Annotations

**Programmatic selection:**

```javascript
function selectAnnotation(annotationId) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.selectAnnotation(annotationId);
}
```

### Moving and Resizing

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

### Deleting Annotations

**Programmatic deletion:**

#### Deleting a single annotation using its Id

```javascript
function deleteAnnotation(annotationId) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.deleteAnnotation(annotationId);
}
```

#### Deleting all annotations on a single page

```javascript
// Delete all annotations on a page
function deleteAllAnnotations(pageNumber) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotationCollection.forEach(function(annotation) {
        if (annotation.pageNumber === pageNumber) {
            viewer.annotation.deleteAnnotation(annotation.annotationId);
        }
    });
}
```

### Locking Annotations

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

### Importing and Exporting

**Export annotations:**

```javascript
function exportAnnotations() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.exportAnnotation();
}
```

**Import annotations:**

```javascript
function importAnnotations(annotationData) {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.importAnnotation(annotationData);
}
```

---