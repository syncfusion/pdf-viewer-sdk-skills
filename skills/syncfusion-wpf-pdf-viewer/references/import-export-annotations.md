# Importing and Exporting Annotations in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports exporting and importing annotation data in FDF or XFDF formats via the `ExportAnnotations` and `ImportAnnotations` APIs.

---

## Export All Annotations from a Loaded PDF to an FDF or XFDF File Using ExportAnnotations in Code-Behind
Exports all annotations in the loaded PDF to a file using `ExportAnnotations`. Choose `AnnotationDataFormat.fdf` or `AnnotationDataFormat.xfdf` as required.

```csharp
// Export annotations to an FDF file.
pdfViewer.ExportAnnotations("Annotation.fdf", AnnotationDataFormat.fdf);

// Export annotations to an XFDF file.
pdfViewer.ExportAnnotations("Annotation.xfdf", AnnotationDataFormat.xfdf);
```

### Placeholders
- Replace `"Annotation.fdf"` / `"Annotation.xfdf"` with the desired output file path.

---

## Export All Annotations from a Loaded PDF to a Memory Stream in FDF or XFDF Format for In-Memory Processing Using ExportAnnotations in Code-Behind
Exports all annotations in the loaded PDF to a `Stream` instead of a file, useful for in-memory processing or network transfer.

```csharp
// Export annotations to a memory stream in FDF format.
Stream stream = new MemoryStream();
pdfViewer.ExportAnnotations(stream, AnnotationDataFormat.fdf);
```

### Placeholders
- Replace `AnnotationDataFormat.fdf` with `AnnotationDataFormat.xfdf` to export in XFDF format.

---

## Import Annotations from an FDF or XFDF File and Apply Them to the Currently Loaded PDF Document Using ImportAnnotations in Code-Behind
Imports annotations from an FDF or XFDF file and applies them to the currently loaded PDF document using `ImportAnnotations`.

```csharp
// Import annotations from an FDF file.
pdfViewer.ImportAnnotations("Annotation.fdf", AnnotationDataFormat.fdf);

// Import annotations from an XFDF file.
pdfViewer.ImportAnnotations("Annotation.xfdf", AnnotationDataFormat.xfdf);
```

### Placeholders
- Replace `"Annotation.fdf"` / `"Annotation.xfdf"` with the path to the annotation file to import.

---

## Import Annotations from a Stream Containing FDF or XFDF Data and Apply Them to the Currently Loaded PDF Document Using ImportAnnotations in Code-Behind
Imports annotations from a `Stream` containing FDF or XFDF data and applies them to the currently loaded PDF document.

```csharp
// Import annotations from a stream in FDF format.
pdfViewer.ImportAnnotations(stream, AnnotationDataFormat.fdf);
```

### Placeholders
- Replace `AnnotationDataFormat.fdf` with `AnnotationDataFormat.xfdf` to import XFDF data.
- Ensure `stream` is positioned at the beginning before calling `ImportAnnotations`.
