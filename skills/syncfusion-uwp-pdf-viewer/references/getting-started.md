# Getting Started with UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Required Assemblies](#required-assemblies)
- [Add SfPdfViewerControl via XAML](#add-sfpdfviewercontrol-via-xaml)
- [Load PDF via Data Binding (ItemsSource)](#load-pdf-via-data-binding-itemssource)
- [Load PDF via FileOpenPicker](#load-pdf-via-fileopenpicker)
- [DocumentLoaded Event](#documentloaded-event)
- [Saving a PDF Document](#saving-a-pdf-document)
- [Unloading and Disposing](#unloading-and-disposing)

---

## Required Assemblies

Add the following assemblies as references to your UWP project:

- `Syncfusion.SfPdfViewer.UWP`
- `Syncfusion.Pdf.UWP`
- `Syncfusion.SfColorPickers.UWP`
- `Syncfusion.SfInput.UWP`
- `Syncfusion.SfRadialMenu.UWP`
- `Syncfusion.SfShared.UWP`

> Starting with v16.2.0.x, you must include a license key in your project when referencing Syncfusion assemblies from trial setup or NuGet.

---

## Add SfPdfViewerControl via XAML

Add the `Syncfusion.Windows.PdfViewer` namespace and declare the control:

```xaml
<Page
    x:Class="SimpleSample.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:syncfusion="using:Syncfusion.Windows.PdfViewer">
    <Grid>
        <syncfusion:SfPdfViewerControl Name="pdfViewer"/>
    </Grid>
</Page>
```

Set the DataContext to the pdfViewer for command bindings in the toolbar:

```csharp
this.DataContext = pdfViewer;
```

---

## Load PDF via Data Binding (ItemsSource)

`ItemsSource` accepts a `Stream` bound during initialization. Create a ViewModel class that loads the stream:

```csharp
class PdfReport : INotifyPropertyChanged
{
    private Stream docStream;
    public event PropertyChangedEventHandler PropertyChanged;

    public Stream DocumentStream
    {
        get { return docStream; }
        set
        {
            docStream = value;
            OnPropertyChanged(new PropertyChangedEventArgs("DocumentStream"));
        }
    }

    public PdfReport()
    {
        // Load from embedded resource
        Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
        docStream = assembly.GetManifestResourceStream("SimpleSample.Assets.sample.pdf");
    }

    public void OnPropertyChanged(PropertyChangedEventArgs e)
    {
        PropertyChanged?.Invoke(this, e);
    }
}
```

Bind in XAML:

```xaml
<Page Loaded="Page_Loaded">
    <Page.DataContext>
        <local:PdfReport/>
    </Page.DataContext>
    <Grid>
        <syncfusion:SfPdfViewerControl Name="pdfViewer"
                                       ItemsSource="{Binding DocumentStream}"/>
    </Grid>
</Page>
```

---

## Load PDF via FileOpenPicker

The `SfPdfViewerControl` supports loading documents from an embedded resource, a `Stream`, a `PdfLoadedDocument`, or a `StorageFile`. To load a document at runtime, call the appropriate viewer API such as `LoadDocument(Stream)`, `LoadDocument(PdfLoadedDocument)`, or `LoadDocument(StorageFile)`. You can monitor load completion using the **`DocumentLoaded`** event API. Example implementation details for runtime file-picking are omitted from this reference.

---

## Load PDF from Embedded Resource (Code-Behind)

```csharp
Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("MyApp.Assets.sample.pdf");
byte[] buffer = new byte[fileStream.Length];
fileStream.Read(buffer, 0, buffer.Length);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(buffer);
pdfViewer.LoadDocument(loadedDocument);
```

For async loading with cancellation support:

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
await pdfViewer.LoadDocumentAsync(loadedDocument, cts.Token);
```

---

## DocumentLoaded Event

Use `DocumentLoaded` to run logic after the PDF is fully rendered:

```csharp
SfPdfViewerControl pdfViewer = new SfPdfViewerControl();
pdfViewer.DocumentLoaded += PdfViewer_DocumentLoaded;

private void PdfViewer_DocumentLoaded(object sender, DocumentLoadedEventArgs args)
{
    // Get total page count after load
    int pageCount = pdfViewer.PageCount;
}
```

---

## Saving a PDF Document

Save the document with annotations as a stream:

```csharp
// Synchronous save (does not include stamp annotations)
Stream pdfDocumentStream = pdfViewer.Save();

// Asynchronous save (includes stamp annotations)
Task<Stream> pdfDocumentStream = pdfViewer.SaveAsync();
```

To save to a file using FileSavePicker:

```csharp
Stream stream = pdfViewer.Save();
stream.Position = 0;

FileSavePicker savePicker = new FileSavePicker();
savePicker.DefaultFileExtension = ".pdf";
savePicker.SuggestedFileName = "output.pdf";
savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
StorageFile stFile = await savePicker.PickSaveFileAsync();
if (stFile != null)
{
    var fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.SetLength(0);
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
}
```

---

## Unloading and Disposing

Unload the PDF and release associated resources when the viewer is no longer needed:

```csharp
// Unload the current PDF document
pdfViewer.Unload();

// Dispose all managed resources
pdfViewer.Dispose();
```

---
