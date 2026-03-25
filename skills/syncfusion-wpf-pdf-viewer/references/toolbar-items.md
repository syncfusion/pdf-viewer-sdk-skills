# Toolbar Items in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports showing, hiding, and disabling individual toolbar items using the `ShowToolbar`, `ShowScrollbar`, `EnableNotificationBar` properties and toolbar template names.

## Hide the Default Top Toolbar by Setting ShowToolbar to False in Code-Behind
```csharp
// Hide the top toolbar
pdfViewer.ShowToolbar = false;
```

## Hide the Scrollbar by Setting ShowScrollbar to False in Code-Behind
```csharp
// Hide the scrollbar
pdfViewer.ShowScrollbar = false;
```

## Hide All Icons in the Vertical Left Toolbar by Disabling Each Panel Setting in Code-Behind
```csharp
pdfViewer.ThumbnailSettings.IsVisible = false;
pdfViewer.IsBookmarkEnabled = false;
pdfViewer.EnableLayers = false;
pdfViewer.PageOrganizerSettings.IsIconVisible = false;
pdfViewer.EnableRedactionTool = false;
pdfViewer.FormSettings.IsIconVisible = false;
```

## Hide a Specific Toolbar Button by Retrieving Its Template Part and Collapsing Its Visibility in Code-Behind
```csharp
pdfViewer.Load("sample.pdf");
pdfViewer.Loaded += pdfViewer_Loaded;

private void pdfViewer_Loaded(object sender, RoutedEventArgs e)
{
    // Get the toolbar instance
    DocumentToolbar toolbar = pdfViewer.Template.FindName("PART_Toolbar", pdfViewer) as DocumentToolbar;
    // Get the text search button and hide it
    Button textSearchButton = (Button)toolbar.Template.FindName("PART_ButtonTextSearch", toolbar);
    textSearchButton.Visibility = System.Windows.Visibility.Collapsed;
}
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.
- Replace `PART_ButtonTextSearch` with the template name of the item to disable.

## Hide a Specific File Menu Item by Iterating the Context Menu and Collapsing the Matching Entry in Code-Behind
```csharp
private void pdfViewer_Loaded(object sender, RoutedEventArgs e)
{
    DocumentToolbar toolbar = pdfViewer.Template.FindName("PART_Toolbar", pdfViewer) as DocumentToolbar;
    ToggleButton fileButton = (ToggleButton)toolbar.Template.FindName("PART_FileToggleButton", toolbar);
    ContextMenu fileContextMenu = fileButton.ContextMenu;
    foreach (MenuItem item in fileContextMenu.Items)
    {
        if (item.Name == "PART_OpenMenuItem")
            item.Visibility = System.Windows.Visibility.Collapsed;
    }
}
```
### Placeholders
- Replace `PART_OpenMenuItem` with the desired file menu item template name.

## Expand the Annotation Toolbar Programmatically by Setting the Annotation Toggle Button to Checked in Code-Behind
```csharp
private void ExpandAnnotationToolbar()
{
    DocumentToolbar toolbar = pdfViewer.Template.FindName("PART_Toolbar", pdfViewer) as DocumentToolbar;
    ToggleButton annotationButton = (ToggleButton)toolbar.Template.FindName("PART_Annotations", toolbar);
    annotationButton.IsChecked = true;
}
```

## Suppress Error Notifications by Disabling the Notification Bar in Code-Behind
```csharp
// Hide the notification bar (suppresses error notifications)
pdfViewer.EnableNotificationBar = false;
```

## Switch to the Classic Toolbar Design by Applying the Legacy Control Style in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewer"
                             Style="{StaticResource SyncfusionPdfViewerCustomControlStyle}">
</syncfusion:PdfViewerControl>
```

## API Reference for All Toolbar Visibility and Notification Bar Properties

| API | Type | Description |
|---|---|---|
| `ShowToolbar` | Property | Shows or hides the top toolbar. |
| `ShowScrollbar` | Property | Shows or hides the scrollbar. |
| `ThumbnailSettings.IsVisible` | Property | Shows or hides the thumbnail icon in the vertical toolbar. |
| `IsBookmarkEnabled` | Property | Shows or hides the bookmark icon in the vertical toolbar. |
| `EnableLayers` | Property | Shows or hides the layers icon in the vertical toolbar. |
| `PageOrganizerSettings.IsIconVisible` | Property | Shows or hides the organize pages icon in the vertical toolbar. |
| `EnableRedactionTool` | Property | Shows or hides the redaction icon in the vertical toolbar. |
| `FormSettings.IsIconVisible` | Property | Shows or hides the form icon in the vertical toolbar. |
| `EnableNotificationBar` | Property | Enables or disables the notification bar that displays on unexpected errors. |

