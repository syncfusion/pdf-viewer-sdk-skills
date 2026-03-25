# Toolbar Buttons: Hide or Disable

The WinForms PDF Viewer provides a `ToolbarSettings` API that allows you to access and manage toolbar buttons. To hide a specific button, use the `IsVisible` property associated with that button. Setting `IsVisible` to `false` hides the button from the toolbar.

The following code snippet demonstrates how to hide the **Open** and **Save** buttons in the WinForms PDF Viewer control.

```csharp
// Load the document into PdfViewer control
pdfviewerControl.Load("Input.pdf");

// Change the visibility of the Open and Save buttons
pdfviewerControl.ToolbarSettings.OpenButton.IsVisible = false;
pdfViewerControl1.ToolbarSettings.SaveButton.IsVisible = false;
pdfViewerControl1.ToolbarSettings.ZoomInButton.IsVisible = false;
pdfViewerControl1.ToolbarSettings.ZoomOutButton.IsVisible = false;
pdfViewerControl1.ToolbarSettings.PanButton.IsVisible = false;
pdfViewerControl1.ToolbarSettings.PrintButton.IsVisible = false;
```