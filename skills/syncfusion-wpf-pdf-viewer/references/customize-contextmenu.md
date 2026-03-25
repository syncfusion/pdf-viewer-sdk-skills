# Customize Context Menu in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports customization of the default context menu items for Annotation, Text Selection, Redaction, and Signature Field using `ContextMenuOpening` and `ContextMenuItemClickedEvent` events.

## Wire Context Menu Opening and Item Clicked Events to Handle and Customize the Context Menu Using Code-Behind
```csharp
pdfViewer.ContextMenuOpening += PdfViewer_ContextMenuOpening;
pdfViewer.ContextMenuItemClickedEvent += PdfViewer_ContextMenuItemClickedEvent;
```

## Add a Custom Menu Item to the Annotation, Redaction, Text Selection, or Signature Field Context Menu Using Code-Behind
```csharp
private void PdfViewer_ContextMenuOpening(object sender, ContextMenuOpeningEventArgs e)
{
    if (e.Source == "Annotation")
    {
        e.MenuItems.Insert(0, new ContextMenuItem { Content = "Lock Annotation" });
        e.MenuItems.Add(new ContextMenuItem { Content = "New Menu Item" });
    }
    if (e.Source == "Redaction")
        e.MenuItems.Add(new ContextMenuItem { Content = "New Menu Item" });

    if (e.Source == "Text Selection")
        e.MenuItems.Add(new ContextMenuItem { Content = "New Menu Item" });

    if (e.Source == "Signature Field")
        e.MenuItems.Add(new ContextMenuItem { Content = "New Menu Item" });
}
```

## Remove an Existing Menu Item from the Annotation or Text Selection Context Menu by Content Name Using Code-Behind
```csharp
private void PdfViewer_ContextMenuOpening(object sender, ContextMenuOpeningEventArgs e)
{
    if (e.Source == "Annotation")
    {
        var item = e.MenuItems.FirstOrDefault(i => i.Content == "Delete");
        if (item != null) e.MenuItems.Remove(item);
    }
    if (e.Source == "Text Selection")
    {
        var item = e.MenuItems.FirstOrDefault(i => i.Content == "Copy");
        if (item != null) e.MenuItems.Remove(item);
    }
}
```

## Hide the Context Menu for Annotation, Redaction, Text Selection, or Signature Field by Setting Handled to True Using Code-Behind
```csharp
private void PdfViewer_ContextMenuOpening(object sender, ContextMenuOpeningEventArgs e)
{
    if (e.Source == "Annotation")
        e.Handled = true;

    if (e.Source == "Redaction")
        e.Handled = true;

    if (e.Source == "Text Selection")
        e.Handled = true;

    if (e.Source == "Signature Field")
        e.Handled = true;
}
```

## Handle Context Menu Item Click and Suppress the Default Action to Retrieve Clicked Item Details Using Code-Behind
```csharp
private void PdfViewer_ContextMenuItemClickedEvent(object sender, ContextMenuItemClickedEventArgs e)
{
    // Suppress default action
    e.Handled = true;

    // Retrieve clicked item details
    MessageBox.Show($"Source: {e.Source}\nClicked Item: {e.MenuItem.Content}");
}
```

## API Reference for All Context Menu Events, Event Arguments, and Properties

| API | Type | Description |
|---|---|---|
| `ContextMenuOpening` | Event | Triggered before the context menu is displayed; allows dynamic modification of menu items. |
| `ContextMenuItemClickedEvent` | Event | Triggered when a context menu item is clicked. |
| `ContextMenuOpeningEventArgs.Source` | Property | Identifies the source type: `"Annotation"`, `"Redaction"`, `"Text Selection"`, or `"Signature Field"`. |
| `ContextMenuOpeningEventArgs.MenuItems` | Property | Collection of `ContextMenuItem` objects to add, remove, or reorder. |
| `ContextMenuOpeningEventArgs.Handled` | Property | Set to `true` to suppress the context menu from appearing. |
| `ContextMenuItem.Content` | Property | Text label of the context menu item. |
| `ContextMenuItemClickedEventArgs.Source` | Property | Source type of the context menu that was clicked. |
| `ContextMenuItemClickedEventArgs.MenuItem` | Property | The `ContextMenuItem` that was clicked. |
| `ContextMenuItemClickedEventArgs.Handled` | Property | Set to `true` to prevent the default click action. |
