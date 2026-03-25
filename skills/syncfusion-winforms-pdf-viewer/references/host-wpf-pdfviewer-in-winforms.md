# Host WPF PdfViewer Features in WinForms

To leverage the advanced features offered by the WPF PdfViewer — such as adding annotations, form filling, signatures, stamps, sticky notes, and more — you can integrate the WPF PdfViewer into a Windows Forms application and take advantage of its extensive feature set.

A WPF PdfViewer control can be hosted within a Windows Forms application using an `ElementHost`. By embedding the WPF PdfViewer, you can access advanced features available in the WPF control while maintaining a Windows Forms interface.

### Steps to Host the WPF PdfViewer in a WinForms Application

**Step 1:** Add a WPF UserControl and install the `Syncfusion.PdfViewer.WPF` NuGet package to your WinForms application.

**Step 2:** Add the following Syncfusion namespace in XAML to make use of the WPF `PdfViewerControl`.

```xml
<UserControl
    xmlns:PdfView="clr-namespace:Syncfusion.Windows.PdfViewer;assembly=Syncfusion.PdfViewer.WPF">
</UserControl>
```

**Step 3:** Add the following code in the XAML page to initialize the WPF PdfViewer.

```xml
<Grid>
    <PdfView:PdfViewerControl x:Name="pdfViewer"/>
</Grid>
```

**Step 4:** Load the PDF file into the PdfViewer when the UserControl is loaded in the application.

```csharp
private void UserControl_Loaded(object sender, RoutedEventArgs e)
{
    pdfViewer.Load(@"../../Data/Windows Store Apps Succinctly.pdf");
}
```

**Step 5:** Add a panel to the form. Create an `ElementHost` object in the Form and add the created UserControl's object as a child to the `ElementHost` object. Add the `ElementHost` as a child to the panel as shown below.

```csharp
// Create the ElementHost control to host the WPF PdfViewer
ElementHost elementHost = new ElementHost();
elementHost.AutoSize = true;
elementHost.Size = panel1.Size;
elementHost.Dock = DockStyle.Fill;
// Adds the ElementHost to the panel1 control
panel1.Controls.Add(elementHost);

// Create the WPF PdfViewer control and assign it as a child of ElementHost
PdfViewerUserControl pdfViewerUserControl = new PdfViewerUserControl();
// Embeds the PdfViewer into the ElementHost
elementHost.Child = pdfViewerUserControl;

// Set additional visual properties for a seamless look and feel
elementHost.Margin = new Padding(0, 0, 0, 0);
elementHost.Region = new Region();
elementHost.BackColor = System.Drawing.Color.White;
```

Hosting the WPF viewer allows using features not available in the WinForms control while keeping the rest of the app WinForms-based.