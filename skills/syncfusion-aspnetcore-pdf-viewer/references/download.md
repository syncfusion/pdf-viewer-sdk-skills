# Download

Brief: The Download feature enables users to save the currently loaded PDF document, including all applied changes such as annotations, form-field edits, ink drawings, comments, or page reorganizations. Downloads can be triggered via the toolbar or programmatically through the API.

## Toolbar Download

The ASP.NET Core PDF Viewer can include a download button in its toolbar when the Toolbar service is injected and the `DownloadOption` is configured.

### Requirements

To enable the toolbar download button:

1. Include `DownloadOption` in the `toolbarItems` property
2. Users can then click the download icon to save the PDF

### Usage

The toolbar automatically includes a download button.

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Programmatic Download

### Method
`download()`

### Description
Triggers a download of the currently loaded PDF document programmatically. The downloaded PDF includes all applied changes and edits.

### Usage

```javascript
var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
pdfViewer.download();
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Download with Event Interception

### Event
`downloadStart`

### Type
`DownloadStartEventArgs`

### Description
Fires before the download action begins. Can be used to intercept the download process, cancel the default download, and implement custom logic such as flattening annotations.

### Usage

```javascript
function onDownloadStart(args) {
    args.cancel = true; // Cancel default download
    // Implement custom download logic here
}
```

### Event Properties

- **cancel**: `boolean` - Set to `true` to prevent the default download action and implement custom download logic

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Save PDF as blob

### Method
`saveAsBlob()`

### Description
Retrieves the current PDF document as a `Blob` object. This can be used in conjunction with the `downloadStart` event to flatten annotations or apply custom modifications before downloading.

### Usage

```javascript
function blobToBase64(blob) {
    return new Promise(function(resolve, reject) {
        var reader = new FileReader();
        reader.onerror = function() { reject(reader.error); };
        reader.onload = function() {
            var dataUrl = reader.result;
            var data = dataUrl.split(',')[1];
            resolve(data);
        };
        reader.readAsDataURL(blob);
    });
}

function handleFlattening() {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    pdfViewer.saveAsBlob().then(function(blob) {
        blobToBase64(blob).then(function(data) {
            flattenPDF(data);
        });
    });
}

function flattenPDF(data) {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    var document = new PdfDocument(data);
    document.flatten = true;
    document.save(pdfViewer.fileName + '.pdf');
    document.destroy();
}

function onDownloadStart(args) {
    args.cancel = true;
    handleFlattening();
}
```

### Return Type

- **Blob**: The PDF document as a binary blob object

### Note

- The `saveAsBlob()` method includes all applied annotations, form-field edits, and other modifications
- Use with `FileReader` API to convert blob to base64 format when needed for further processing

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Related Services

To use the download functionality, ensure the following services are injected into the `PdfViewerComponent`:

- **Toolbar**: Enables the toolbar with download button
- **Print**: Often used alongside download functionality
- **Annotation**: For handling annotated PDFs during download
- **FormFields**: For preserving form-field data in downloaded PDFs