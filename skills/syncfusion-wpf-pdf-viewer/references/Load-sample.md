# Load PDF Files in WPF Pdf Viewer
Loading PDF files in the Syncfusion WPF PdfViewer is done through the `Load` API and the `ItemSource` property, which support opening both normal and encrypted documents. PDFs can be loaded from file paths, streams, or `PdfLoadedDocument` objects, and also via XAML data binding using `ItemSource`, enabling flexible integration within WPF applications.


## Add PdfViewerControl to the Main Window Using XAML

Add the `PdfViewerControl` in the `MainWindow.xaml`.

```xaml
<Window 
    x:Class="PdfViewerDemo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    WindowState="Maximized"
    xmlns:syncfusion="clr-namespace:Syncfusion.Windows.PdfViewer;assembly=Syncfusion.PdfViewer.WPF">
    <Grid>
        <syncfusion:PdfViewerControl x:Name="pdfViewer"></syncfusion:PdfViewerControl>
    </Grid>
</Window>
```

## Load a Normal PDF from a File Path Using Code-Behind
```csharp
            //Load PDF file using the file path.
            pdfViewer.Load(@"customer.pdf");
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Load a Normal PDF from a Stream Using Code-Behind
```csharp
        FileStream stream = new FileStream(@"customer.pdf", FileMode.Open);
        //Load PDF file using stream.
        pdfViewer.Load(stream);
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Load a Password-Protected PDF from a File Path Using Code-Behind
```csharp
            //Load password protected PDF file using the file path and the password.
            pdfViewer.Load(@"customer.pdf", "password");
```
### Placeholders
- Replace `customer.pdf` with the customer-given PDF file path.
- Replace `"password"` with the actual password of the PDF.

## Load a Password-Protected PDF from a Stream Using Code-Behind
```csharp
         FileStream stream = new FileStream(@"customer.pdf", FileMode.Open);
         //Load password protected PDF file using stream and the password.
        pdfViewer.Load(stream, "password");
```
### Placeholders
- Replace `customer.pdf` with the customer-given PDF file path.
- Replace `"password"` with the actual password of the PDF.

## Load a PDF Using the ItemSource Property with a File Path in Code-Behind

The `ItemSource` property of `PdfViewerControl` accepts a string file path, a `Stream`, or a `PdfLoadedDocument` object to load a PDF.

```csharp
    //Load PDF file using the ItemSource property.
    pdfViewer.ItemSource = @"customer.pdf";
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Load a PDF Using the ItemSource Property with a Stream in Code-Behind
```csharp
    //Load PDF file as Stream using the ItemSource property.
    pdfViewer.ItemSource = new FileStream(@"customer.pdf", FileMode.Open);
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Load a PDF Using the ItemSource Property with a PdfLoadedDocument Object in Code-Behind
```csharp
    //Load PDF file as PdfLoadedDocument object using the ItemSource property.
    PdfLoadedDocument pdfLoadedDocument = new PdfLoadedDocument(@"customer.pdf");
    pdfViewer.ItemSource = pdfLoadedDocument;
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Load a PDF by Binding the ItemSource Property to a ViewModel Using XAML and MVVM

You can bind the `ItemSource` property directly in XAML using a ViewModel, enabling MVVM-based PDF loading.

### MainWindow.xaml
```xaml
<Window 
    x:Class="PdfViewerDemo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    WindowState="Maximized"
    xmlns:syncfusion="clr-namespace:Syncfusion.Windows.PdfViewer;assembly=Syncfusion.PdfViewer.WPF"
    xmlns:local="clr-namespace:PdfViewerDemo">
    <Window.DataContext>
        <local:MainViewModel/>
    </Window.DataContext>
    <Grid>
        <syncfusion:PdfViewerControl x:Name="pdfViewer"
                                     ItemSource="{Binding PdfFilePath}">
        </syncfusion:PdfViewerControl>
    </Grid>
</Window>
```

### MainWindow.xaml.cs
```csharp
    public MainWindow()
    {
        InitializeComponent();
    }
```

### MainViewModel.cs
```csharp
    public class MainViewModel : INotifyPropertyChanged
    {
        private string _pdfFilePath;

        public string PdfFilePath
        {
            get { return _pdfFilePath; }
            set
            {
                _pdfFilePath = value;
                OnPropertyChanged(nameof(PdfFilePath));
            }
        }

        public MainViewModel()
        {
            //Set the PDF file path to load via binding.
            PdfFilePath = @"customer.pdf";
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
```
### Placeholders
Replace `customer.pdf` with the customer-given PDF file path.

## Unload the Current PDF Document and Free Resources Using Code-Behind
```csharp
pdfViewer.Unload(true);
```

## Change the Loading Indicator Spinner Color Using Code-Behind
```csharp
pdfViewer.LoadingIndicator.LoaderColor = System.Windows.Media.Color.FromArgb(255, 255, 0, 0);
```

## Change the Loading Indicator Message Text Using Code-Behind
```csharp
pdfViewer.LoadingIndicator.LoadingMessage = "Document loading";
```

## Suppress the Built-In Password Dialog and Supply the Password Programmatically Using Code-Behind

To suppress the built-in password prompt and supply the password programmatically, handle the `GetDocumentPassword` event and set `e.Handled = true`.

```csharp
        pdfViewer.GetDocumentPassword += PdfViewer_GetDocumentPassword;
         string filePath = Path.GetFullPath(@"customer.pdf");
        pdfViewer.Load(filePath);

        private void PdfViewer_GetDocumentPassword(object sender, GetDocumentPasswordEventArgs e)
        {
            System.Security.SecureString secureString = new System.Security.SecureString();
            foreach (char c in "password")
                secureString.AppendChar(c);

            e.Password = secureString;

            // Set Handled to true to hide the built-in password dialog.
            e.Handled = true;
        }
```
### Placeholders
- Replace `customer.pdf` with the customer-given PDF file path.
- Replace `"password"` with the actual password characters for the PDF.

## Apply a Theme to WPF PdfViewerControl Using SfSkinManager

The WPF PdfViewerControl supports built-in themes via `SfSkinManager`. To apply a theme, install the corresponding Syncfusion theme NuGet package and call `SfSkinManager.SetTheme` in code-behind.

### Required NuGet Package per Theme

| Theme Name | NuGet Package |
|---|---|
| `FluentLight` | `Syncfusion.Themes.FluentLight.WPF` |
| `FluentDark` | `Syncfusion.Themes.FluentDark.WPF` |
| `MaterialLight` | `Syncfusion.Themes.MaterialLight.WPF` |
| `MaterialDark` | `Syncfusion.Themes.MaterialDark.WPF` |
| `MaterialLight3` | `Syncfusion.Themes.MaterialLight3.WPF` |
| `MaterialDark3` | `Syncfusion.Themes.MaterialDark3.WPF` |
| `Office2019Colorful` | `Syncfusion.Themes.Office2019Colorful.WPF` |
| `Office2019Black` | `Syncfusion.Themes.Office2019Black.WPF` |
| `Office2019White` | `Syncfusion.Themes.Office2019White.WPF` |
| `Office2019DarkGray` | `Syncfusion.Themes.Office2019DarkGray.WPF` |
| `Windows11Light` | `Syncfusion.Themes.Windows11Light.WPF` |
| `Windows11Dark` | `Syncfusion.Themes.Windows11Dark.WPF` |

> **Note:** Install only the NuGet package that matches the theme the user wants to apply.

### Apply a Theme Using SfSkinManager in Code-Behind

The following example applies the `FluentLight` theme. Replace the theme name and NuGet package according to the desired theme from the table above.

**Step 1:** Install the theme NuGet package (example for FluentLight):
```
Install-Package Syncfusion.Themes.FluentLight.WPF
```

**Step 2:** Add the `SfSkinManager` namespace to `MainWindow.xaml`:
```xaml
<Window 
    x:Class="PdfViewerDemo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    WindowState="Maximized"
    xmlns:syncfusion="clr-namespace:Syncfusion.Windows.PdfViewer;assembly=Syncfusion.PdfViewer.WPF"
    xmlns:syncfusionskin="clr-namespace:Syncfusion.SfSkinManager;assembly=Syncfusion.SfSkinManager.WPF">
    <Grid x:Name="HomeGrid">
        <syncfusion:PdfViewerControl x:Name="pdfViewer"></syncfusion:PdfViewerControl>
    </Grid>
</Window>
```

**Step 3:** Apply the theme in `MainWindow.xaml.cs`:
```csharp
    // Apply the FluentLight theme to PdfViewerControl.
    // Replace "FluentLight" with your desired theme name (e.g., "FluentDark", "MaterialLight", "Windows11Light").
    SfSkinManager.SetTheme(pdfViewer, new Theme() { ThemeName = "FluentLight" });
    // Load a PDF after applying the theme.
    pdfViewer.Load(@"customer.pdf");
```
### Placeholders
- Replace `"FluentLight"` with the desired theme name from the table above.
- Replace `customer.pdf` with the customer-given PDF file path.
- Install the corresponding NuGet package for the chosen theme.

### References
- [Apply theme using SfSkinManager](https://help.syncfusion.com/wpf/themes/skin-manager)
- [Create a custom theme using ThemeStudio](https://help.syncfusion.com/wpf/themes/theme-studio#creating-custom-theme)
- [WPF PdfViewer Getting Started – Theme](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/wpf/getting-started#theme)

---

## API Reference for All Load Methods, Properties, and Events

| API | Type | Description |
|---|---|---|
| `Load(filePath)` | Method | Loads a PDF document from the given file path. |
| `Load(stream)` | Method | Loads a PDF document from a `Stream`. |
| `Load(filePath, password)` | Method | Loads a password-protected PDF from a file path. |
| `Load(stream, password)` | Method | Loads a password-protected PDF from a `Stream`. |
| `ItemSource` | Property | Accepts a file path, `Stream`, or `PdfLoadedDocument` to load a PDF; supports XAML binding. |
| `Unload(bool)` | Method | Unloads the document; pass `true` to also dispose it. |
| `GetDocumentPassword` | Event | Fires when the viewer needs the document password; set `e.Handled = true` to suppress the built-in dialog. |
| `GetDocumentPasswordEventArgs.Password` | Property | `SecureString` password to supply programmatically. |
| `GetDocumentPasswordEventArgs.Handled` | Property | Set to `true` to hide the built-in password dialog. |
| `LoadingIndicator.LoaderColor` | Property | Color of the loading spinner shown while the PDF is loading. |
| `LoadingIndicator.LoadingMessage` | Property | Text message displayed in the loading indicator. |
| `SfSkinManager.SetTheme(control, theme)` | Method | Applies a built-in theme to the PdfViewerControl using `Syncfusion.SfSkinManager`. |