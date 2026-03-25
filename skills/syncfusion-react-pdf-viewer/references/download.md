# Download

## Table of Contents
- [When to Use Download](#when-to-use-download)
- [Choosing Download Approach](#choosing-download-approach)
- [Toolbar Download](#toolbar-download)
- [Programmatic Download](#programmatic-download)
- [Download with Event Interception](#download-with-event-interception)
- [Flatten Annotations Before Download](#flatten-annotations-before-download)

## When to Use Download

When users need to save a PDF document with all applied changes—including annotations, form-field edits, ink drawings, comments, or page reorganizations—guide them to implement the download feature. This preserves all modifications made during the PDF viewing session.

**Common scenarios:**
- User completes form filling and wants to save the filled PDF locally
- User adds annotations/comments and needs to export the marked-up document
- User reorganizes pages and wants to save the modified structure
- Application requires generating downloadable PDFs after user edits

## Choosing Download Approach

**When user wants simple download with UI button** → Use toolbar download (easiest for end users)

**When download needs to be triggered programmatically** → Use `download()` method (e.g., "Save" button in custom UI, auto-save on form completion)

**When download requires custom processing** → Use `downloadStart` event + `saveAsBlob()` (e.g., flatten annotations, add watermarks, modify metadata)

---

## Toolbar Download

When users need a visible download button in the toolbar, guide them to enable the built-in toolbar download option. This provides the most straightforward user experience.

### Implementation

Enable the toolbar download by injecting the `Toolbar` service and including the download option:

1. Inject the `Toolbar` service into the `PdfViewerComponent`
2. Include `DownloadOption` in the `toolbarItems` property
3. Users can then click the download icon to save the PDF

The toolbar automatically includes a download button when the `Toolbar` service is injected.

---

## Programmatic Download

When users need to trigger downloads from custom UI elements or application logic (not from the built-in toolbar), guide them to use the `download()` method. This is useful for custom save buttons, auto-save features, or workflow-triggered downloads.

### API: `download()`

Triggers a download of the currently loaded PDF document programmatically. The downloaded PDF includes all applied changes and edits.

### Implementation

```tsx
const viewer = document.getElementById('container').ej2_instances[0];
viewer.download();
```

### API: `downloadFileName`

Sets the filename used when downloading the PDF document. This property controls what name the saved PDF file will have on the user's system.

**Type:** `string`

**Default Value:** `"PDF"`

### Implementation

```tsx
<PdfViewerComponent
  downloadFileName="MyDocument"
/>
```

This will save the PDF as `MyDocument.pdf` when the user clicks the download button or calls the `download()` method.

---

## Download with Event Interception

When users need to modify the PDF before download or implement custom download logic, guide them to use the `downloadStart` event. This allows intercepting the download process to apply transformations like flattening annotations, adding watermarks, or custom metadata.

**Why intercept downloads:**
- Flatten annotations to prevent editing after download (compliance, security)
- Apply custom processing before saving (watermarks, metadata, compression)
- Validate document state before allowing download
- Implement custom save locations or cloud uploads

### API: `downloadStart` Event

**Type:** `DownloadStartEventArgs`

Fires before the download action begins, allowing you to intercept the download process, cancel the default behavior, and implement custom logic.

### Implementation

```tsx
const onDownloadStart = async (args: DownloadStartEventArgs) => {
    args.cancel = true; // Cancel default download
    // Implement custom download logic here
};
```

### Event Properties

- **cancel**: `boolean` - Set to `true` to prevent the default download action and implement custom download logic

---

## Flatten Annotations Before Download

When users need annotations to be permanently embedded and non-editable in the downloaded PDF (e.g., for compliance, archival, or preventing tampering), guide them to flatten annotations using `saveAsBlob()` combined with the `downloadStart` event.

**Why flatten annotations:**
- **Compliance:** Many industries require non-editable final documents (legal, healthcare, finance)
- **Security:** Prevent recipients from modifying or removing annotations
- **Archival:** Ensure document appearance remains consistent across all PDF readers
- **Distribution:** Send "final" versions where comments/markups are permanent

### API: `saveAsBlob()`

Retrieves the current PDF document as a `Blob` object, including all applied annotations, form-field edits, and modifications. Use this with the `downloadStart` event to flatten annotations or apply custom transformations before download.

### Implementation

```tsx
const blobToBase64 = async (blob: Blob): Promise<string> => {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onerror = () => reject(reader.error);
        reader.onload = () => {
            const dataUrl: string = reader.result as string;
            const data: string = dataUrl.split(',')[1];
            resolve(data);
        };
        reader.readAsDataURL(blob);
    });
}

const flattenPDF = (data: string) => {
    let document: PdfDocument = new PdfDocument(data);
    document.flatten = true;
    document.save(`${viewerRef.current.fileName}.pdf`);
    document.destroy();
}

const handleFlattening = async () => {
    const blob: Blob = await viewerRef.current.saveAsBlob();
    const data: string = await blobToBase64(blob);
    flattenPDF(data);
}

const onDownloadStart = async (args: DownloadStartEventArgs) => {
    args.cancel = true;
    handleFlattening();
};
```

### Return Type

- **Blob**: The PDF document as a binary blob object

### Note

- The `saveAsBlob()` method includes all applied annotations, form-field edits, and other modifications
- Use with `FileReader` API to convert blob to base64 format when needed for further processing

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---
