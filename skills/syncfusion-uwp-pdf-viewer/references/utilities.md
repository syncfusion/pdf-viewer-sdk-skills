# Utilities & Advanced Features in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Export Pages as Images](#export-pages-as-images)
- [PDFium Custom Renderer](#pdfium-custom-renderer)

---

## Export Pages as Images

### Export a Single Page as Image

```csharp
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(buffer);
pdfViewer.LoadDocument(loadedDocument);

// Get page 2 as Image
Image pageImg = pdfViewer.GetPage(2);

// Get page 2 as Image at 300% zoom
Image pageImg = pdfViewer.GetPage(2, 300);
```

### Export Multiple Pages as Images

```csharp
// Export pages 0 through 5 as Image array
Image[] pageImgCollection = pdfViewer.GetPages(0, 5);

// Export with custom zoom factor
Image[] pageImgCollection = pdfViewer.GetPages(0, 5, 200);
```

### Export as Image Stream (for saving to disk)

```csharp
// Single page as Stream
Stream imageStream = pdfViewer.ExportAsImage(2);

// Single page at custom zoom
Stream imageStream = pdfViewer.ExportAsImage(2, 300);

// Multiple pages as List<Stream>
List<Stream> streamList = pdfViewer.ExportAsImage(0, 5);

// Multiple pages with zoom
List<Stream> streamList = pdfViewer.ExportAsImage(0, 5, 200);
```

---

## PDFium Custom Renderer

By default, `SfPdfViewerControl` uses the Windows rendering engine. To use the PDFium engine instead, implement the `IPdfRenderer` interface and assign it to the `Renderer` property.

### Step 1 — Load the PDFium DLL

Load from a file path:

```csharp
[DllImport("kernel32", SetLastError = true, CharSet = CharSet.Auto)]
private static extern IntPtr LoadLibrary(
    [MarshalAs(UnmanagedType.LPTStr)] string lpFileName);

string path = Path.Combine(ApplicationData.Current.LocalFolder.Path, "pdfium.dll");
LoadLibrary(path);
```

Or add `pdfium.dll` as a **Content** file in the project (no code loading needed).

### Step 2 — Implement IPdfRenderer

Create a class with required external method definitions and interface methods:

```csharp
// External PDFium method declarations
[DllImport("pdfium.dll", EntryPoint = "FPDF_InitLibrary")]
public static extern void FPDF_InitLibrary();

[DllImport("pdfium.dll")]
public static extern int FPDF_GetPageCount(IntPtr document);

// ... (other DllImport declarations for page size, bitmap, render, etc.)

public void Initialize(Stream stream, string password)
{
    fileStream = stream;
    FPDF_InitLibrary();
    FPDF_FILEACCESS access = new FPDF_FILEACCESS
    {
        m_FileLen    = (uint)fileStream.Length,
        m_GetBlock   = Marshal.GetFunctionPointerForDelegate(_getBlockDelegate),
        m_Param      = (IntPtr)2,
    };
    document = FPDF_LoadCustomDocument(access, password);
}

public int PageCount
{
    get
    {
        if (pageCount == -1)
            pageCount = FPDF_GetPageCount(document);
        return pageCount;
    }
}

public Size GetPageSize(int pageIndex)
{
    double height = 0, width = 0;
    FPDF_GetPageSizeByIndex(document, pageIndex, out width, out height);
    return new Size { Width = (int)width, Height = (int)height };
}

public SoftwareBitmap RenderPageBitmap(int pageIndex, double pageWidth, double pageHeight)
{
    var page   = FPDF_LoadPage(document, pageIndex);
    int width  = (int)pageWidth;
    int height = (int)pageHeight;
    byte[] buffer = new byte[width * height * 4];

    unsafe
    {
        fixed (byte* p = buffer)
        {
            IntPtr bitmap = FPDFBitmap_CreateEx(width, height, 4, (IntPtr)p, width * 4);
            FPDFBitmap_FillRect(bitmap, 0, 0, width, height, 0xFFFFFFFF);
            FPDF_RenderPageBitmap(bitmap, page, 0, 0, width, height, 0, FPDF.ANNOT);
            FPDFBitmap_Destroy(bitmap);
            FPDF_ClosePage(page);
        }
    }

    SoftwareBitmap softwareBitmap = new SoftwareBitmap(
        BitmapPixelFormat.Bgra8, width, height, BitmapAlphaMode.Premultiplied);
    softwareBitmap.CopyFromBuffer(buffer.AsBuffer());
    return softwareBitmap;
}

public void Close()
{
    if (document != IntPtr.Zero)
        FPDF_CloseDocument(document);
    pageCount = -1;
}
```

### Step 3 — Assign the Renderer

```csharp
sfPdfViewerControl.Renderer = new CustomerPDFRenderer();
```

> If `Renderer` is not set, the default Windows rendering engine is used. Ensure the correct architecture (x86 or x64) version of `pdfium.dll` is used.
