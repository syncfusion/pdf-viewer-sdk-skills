# Exporting PDF Pages as Images in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports exporting PDF pages as images (JPG, PNG, TIFF, BMP) via the `ExportAsImage` API.

---

## Export a Single PDF Page as a JPEG, PNG, TIFF, or BMP Image Using ExportAsImage in Code-Behind
Exports a single PDF page to a `BitmapSource` by passing the zero-based page index to `ExportAsImage`.

```csharp
PdfViewerControl pdfViewer = new PdfViewerControl();

// Load the input PDF file.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Sample.pdf");
pdfViewer.Load(loadedDocument);

// Export the page at index 0 as a BitmapSource.
BitmapSource image = pdfViewer.ExportAsImage(0);

string output = @"..\..\Output\Image";
if (image != null)
{
    // Initialize a JPEG encoder.
    BitmapEncoder encoder = new JpegBitmapEncoder();
    encoder.Frames.Add(BitmapFrame.Create(image));

    // Save the image to the output path.
    FileStream stream = new FileStream(output + ".Jpeg", FileMode.Create);
    encoder.Save(stream);
}

loadedDocument.Dispose();
loadedDocument = null;
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Replace `output` path with the desired output directory.
- Swap `JpegBitmapEncoder` with `PngBitmapEncoder`, `TiffBitmapEncoder`, or `BmpBitmapEncoder` to export in PNG, TIFF, or BMP format respectively.

---

## Export a Contiguous Range of PDF Pages as Images into a BitmapSource Array Using ExportAsImage in Code-Behind
Exports a contiguous range of PDF pages to a `BitmapSource[]` array by passing the start and end page indexes to `ExportAsImage`.

```csharp
PdfViewerControl pdfViewer = new PdfViewerControl();

// Load the input PDF file.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Sample.pdf");
pdfViewer.Load(loadedDocument);

// Export all pages as images.
BitmapSource[] images = pdfViewer.ExportAsImage(0, loadedDocument.Pages.Count - 1);

string output = @"..\..\Output\Image";
if (images != null)
{
    for (int i = 0; i < images.Length; i++)
    {
        BitmapEncoder encoder = new JpegBitmapEncoder();
        encoder.Frames.Add(BitmapFrame.Create(images[i]));

        FileStream stream = new FileStream(output + i.ToString() + ".Jpeg", FileMode.Create);
        encoder.Save(stream);
    }
}

loadedDocument.Dispose();
loadedDocument = null;
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Replace `output` path with the desired output directory.
- Adjust the start/end page indexes to export only a subset of pages.

---

## Export a Single PDF Page as an Image at a Custom Pixel Width and Height with Optional Aspect Ratio Preservation Using ExportAsImage in Code-Behind
Exports a single PDF page as an image at a specified pixel width and height by passing a `SizeF` to `ExportAsImage`. Set `keepAspectRatio` to `true` to preserve the original page proportions.

```csharp
// Export page at index 0 with a custom size of 1836 x 2372 pixels.
BitmapSource image = pdfViewer.ExportAsImage(0, new SizeF(1836, 2372), false);

string output = @"..\..\Output\Image";
if (image != null)
{
    BitmapEncoder encoder = new JpegBitmapEncoder();
    encoder.Frames.Add(BitmapFrame.Create(image));

    FileStream stream = new FileStream(output + ".Jpeg", FileMode.Create);
    encoder.Save(stream);
}
```

### Placeholders
- Replace the `SizeF` values with the required width and height in pixels.
- Pass `true` as the third argument to maintain the aspect ratio of the output image.

---

## Export a Range of PDF Pages as Images at a Custom Horizontal and Vertical DPI Resolution Using ExportAsImage in Code-Behind
Exports a range of PDF pages as images at a specified horizontal (`DpiX`) and vertical (`DpiY`) resolution using `ExportAsImage`.

```csharp
int startPageIndex = 0;
int endPageIndex = 3;
float dpiX = 200;
float dpiY = 200;

BitmapSource[] images = pdfViewer.ExportAsImage(startPageIndex, endPageIndex, dpiX, dpiY);

string output = @"..\..\Output\Image";
if (images != null)
{
    for (int i = 0; i < images.Length; i++)
    {
        BitmapEncoder encoder = new JpegBitmapEncoder();
        encoder.Frames.Add(BitmapFrame.Create(images[i]));

        FileStream stream = new FileStream(output + i.ToString() + ".Jpeg", FileMode.Create);
        encoder.Save(stream);
    }
}
```

### Placeholders
- Adjust `startPageIndex` and `endPageIndex` to the desired page range.
- Replace `dpiX` and `dpiY` with the required resolution values.


