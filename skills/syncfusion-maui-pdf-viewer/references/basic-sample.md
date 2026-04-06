# Basic PDF Viewer Setup - .NET MAUI

This guide demonstrates the minimal setup to initialize and display a PDF in SfPdfViewer.

---

## Prerequisites

- .NET 9 SDK or later
- Visual Studio 2022 (v17.3 or later)
- Syncfusion.Maui.PdfViewer NuGet package installed
- Syncfusion.Maui.Core NuGet package (installed as dependency)

---

## Step 1: Register Syncfusion Core Handler

Update `MauiProgram.cs` to register the Syncfusion core handler:

**C#:**
```csharp
using Syncfusion.Maui.Core.Hosting;

namespace PdfViewerExample
{
    public class MauiProgram 
    {
        public static MauiApp CreateMauiApp()
        {
            var builder = MauiApp.CreateBuilder();
            builder
                .UseMauiApp<App>()
                .ConfigureFonts(fonts =>
                {
                    fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
                });

            // Register Syncfusion core handler
            builder.ConfigureSyncfusionCore();
            
            return builder.Build();
        }
    }
}
```

---

## Step 2: Add PDF Viewer to XAML

Add the SfPdfViewer control to `MainPage.xaml`:

**XAML:**
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:syncfusion="clr-namespace:Syncfusion.Maui.PdfViewer;assembly=Syncfusion.Maui.PdfViewer"
             x:Class="PdfViewerExample.MainPage">

    <ContentPage.Content>
        <syncfusion:SfPdfViewer x:Name="pdfViewer" />
    </ContentPage.Content>
</ContentPage>
```

---

## Step 3: Create ViewModel for PDF Loading

Create `PdfViewerViewModel.cs` to handle PDF stream binding:

**C#:**
```csharp
using System.Reflection;
using System.ComponentModel;

namespace PdfViewerExample
{
    class PdfViewerViewModel : INotifyPropertyChanged
    {
        private Stream pdfDocumentStream;

        /// <summary>
        /// Occurs when a property value changes.
        /// </summary>
        public event PropertyChangedEventHandler? PropertyChanged;

        /// <summary>
        /// Gets or sets the stream of the currently loaded PDF document.
        /// </summary>
        public Stream PdfDocumentStream
        {
            get
            {
                return pdfDocumentStream;
            }
            set
            {
                pdfDocumentStream = value;
                OnPropertyChanged(nameof(PdfDocumentStream));
            }
        }

        /// <summary>
        /// Initializes a new instance of the PdfViewerViewModel class.
        /// </summary>
        public PdfViewerViewModel()
        {
            // Load the embedded PDF document stream
            // Make sure PDF file is added to Assets folder and Build Action is set to "Embedded Resource"
            pdfDocumentStream = typeof(App).GetTypeInfo().Assembly
                .GetManifestResourceStream("PdfViewerExample.Assets.PDF_Succinctly.pdf");
        }

        /// <summary>
        /// Raises the PropertyChanged event for the specified property name.
        /// </summary>
        /// <param name="name">The name of the property that changed.</param>
        public void OnPropertyChanged(string name)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
        } 
    }
}
```

---

## Step 4: Bind ViewModel and Load PDF

Update `MainPage.xaml` to set the BindingContext and bind DocumentSource:

**XAML:**
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:PdfViewerExample"
             xmlns:syncfusion="clr-namespace:Syncfusion.Maui.PdfViewer;assembly=Syncfusion.Maui.PdfViewer"
             x:Class="PdfViewerExample.MainPage">

    <ContentPage.BindingContext>
        <local:PdfViewerViewModel x:Name="viewModel" />
    </ContentPage.BindingContext>

    <ContentPage.Content>
        <syncfusion:SfPdfViewer x:Name="pdfViewer" 
                                DocumentSource="{Binding PdfDocumentStream}" />
    </ContentPage.Content>
</ContentPage>
```

---

## Step 5: Prepare PDF Asset

1. Create an `Assets` folder in the project root
2. Add your PDF file to the `Assets` folder (e.g., `PDF_Succinctly.pdf`)
3. Right-click the PDF file in Solution Explorer
4. Set **Build Action** to **Embedded Resource**

---

## Running the Application

1. Select your target framework, device, or emulator
2. Press `F5` to run the application
3. The PDF document will be displayed in the SfPdfViewer control

---

## Important Notes

- **Automatic Unloading:** When changing or opening different documents on the same page, the previously loaded document is automatically unloaded
- **Memory Management:** If using multiple pages, call the `UnloadDocument()` method before navigating away to release memory and resources
- **Document Source Options:** You can also load PDFs from:
  - Local file system using `FilePicker`
  - Trusted URL streams
  - Base64 encoded strings
  - Password-protected files

---

