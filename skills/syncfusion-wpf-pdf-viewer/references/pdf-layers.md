# Working with PDF Layers in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows users to toggle the visibility of individual and group of layers in the PDF document using the `Layers` collection and the `IsVisible` property of the `Layer` class.

## APIs and Properties
| API / Property | Description |
|---|---|
| `PdfDocumentView.Layers` | Gets the `LayerCollection` of the loaded PDF. |
| `PdfViewerControl.Layers` | Gets the `LayerCollection` via the viewer control. |
| `Layer.Name` | Gets the name of the PDF layer. |
| `Layer.IsVisible` | Gets or sets the visibility of the layer. |
| `PdfViewerControl.EnableLayers` | Enables or disables the layer feature in the viewer. |

## Toggle the Visibility of a Specific PDF Layer by Name Using Code-Behind
Retrieves the `Layers` collection from `PdfDocumentView` and toggles visibility using the layer's `Name` and `IsVisible` property.

```csharp
    // Initialize the PdfDocumentView control.
     PdfDocumentView pdfDocumentView = new PdfDocumentView();
    // Load the PDF file.
    pdfDocumentView.Load(@"Sample.pdf");

     // Retrieve the layers collection.
    LayerCollection layers = pdfDocumentView.Layers;

    // Toggle visibility of a layer by name.
    for (int i = 0; i < layers.Count; i++)
    {
        if (layers[i].Name == "Layer1")
            {
                layers[i].IsVisible = !layers[i].IsVisible;
            }
    }
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Replace `"Layer1"` with the target layer name.

## Disable All PDF Layers in PdfViewerControl by Setting EnableLayers to False Using Code-Behind
Disables the display of all layers in the PDF document by setting `EnableLayers` to `false`.

```csharp
     // Disable the layers panel and layer rendering.
    pdfViewer.EnableLayers = false;

```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.

## Disable PDF Layers at Startup via EnableLayers DependencyProperty Using XAML

```xaml
<Window
    x:Class="PdfLayersDemo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    WindowState="Maximized"
    xmlns:syncfusion="clr-namespace:Syncfusion.Windows.PdfViewer;assembly=Syncfusion.PdfViewer.WPF">
    <Grid>
        <syncfusion:PdfViewerControl x:Name="pdfViewer" EnableLayers="False"></syncfusion:PdfViewerControl>
    </Grid>
</Window>
```
