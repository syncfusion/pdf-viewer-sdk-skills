# Viewing PDF in UWP PDF Viewer (SfPdfViewerControl)

The `SfPdfViewerControl` supports loading PDF documents from three source types — each available in both synchronous and asynchronous variants.

## 🔒 Security Considerations

**When loading PDFs from untrusted sources (user-selected files, network, etc.):**
- PDFs can contain malicious content including crafted hyperlinks and embedded scripts
- Always validate hyperlinks before allowing navigation (see [Bookmarks & Hyperlinks - Security Best Practice](bookmarks-and-hyperlinks.md#-security-best-practice-validate-hyperlinks-from-untrusted-pdfs))
- Consider disabling hyperlink navigation if not needed: `pdfViewer.AllowHyperlinkNavigation = false`
- Load PDFs from trusted sources when possible (embedded resources, verified downloads)

---

## Loading from a PdfLoadedDocument Object

### Synchronous

```csharp
Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("MyApp.Assets.sample.pdf");
byte[] buffer = new byte[fileStream.Length];
fileStream.Read(buffer, 0, buffer.Length);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(buffer);
pdfViewer.LoadDocument(loadedDocument);
```

### Asynchronous (with cancellation)

```csharp
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(buffer);
CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
await pdfViewer.LoadDocumentAsync(loadedDocument, cancellationTokenSource.Token);
```

---

## Loading from a Stream Object

### Synchronous

```csharp
Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("MyApp.Assets.sample.pdf");
pdfViewer.LoadDocument(fileStream);
```

### Asynchronous (with cancellation)

```csharp
Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("MyApp.Assets.sample.pdf");
CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
await pdfViewer.LoadDocumentAsync(fileStream, cancellationTokenSource.Token);
```

---

## Loading from a StorageFile Object

The viewer supports loading a `StorageFile` (for example, when a file is provided by the app). Use `LoadDocument(StorageFile)` or `LoadDocumentAsync(StorageFile, CancellationToken)` to load such files. Monitor load completion with the **`DocumentLoaded`** event API; concrete file-picking examples are omitted here.

---

## Cancelling Async Loading

Pass a `CancellationToken` to any `LoadDocumentAsync` call. To cancel while in progress:

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
// Start loading
await pdfViewer.LoadDocumentAsync(loadedDocument, cts.Token);

// To cancel:
cts.Cancel();
```

---

## Choosing the Right Load Method

| Scenario | Recommended Method |
|---|---|
| Embedded resource in app package | `LoadDocument(PdfLoadedDocument)` |
| File picked by user at runtime | `LoadDocument(StorageFile)` |
| Stream from network or memory | `LoadDocument(Stream)` |
| Large file needing cancellation | `LoadDocumentAsync(...)` with CancellationToken |
| XAML binding on startup | `ItemsSource="{Binding DocumentStream}"` |
