# PDF Viewer Toolbar Customization - Complete Reference

This guide demonstrates how to customize PDF Viewer toolbars by toolbar type and platform, including removing, adding, hiding, and inserting toolbar items.

---

# Desktop Toolbar Items - Complete Reference

Comprehensive guide for customizing PDF Viewer toolbars on Desktop platforms.

---

## Desktop 1. Primary Toolbar Items

**Location:** Main toolbar at top  
**Toolbar Name:** `PrimaryToolbar`

### Navigation & Document Controls
| Item | Description |
|------|-------------|
| `Undo` | Undo the last action |
| `Redo` | Redo the last undone action |
| `Previous page` | Navigate to previous page |
| `Next page` | Navigate to next page |
| `Page number entry` | Enter page number to jump to |
| `Page count` | Display total number of pages |

### View & Tools
| Item | Description |
|------|-------------|
| `Zoom mode` | Adjust magnification/zoom level |
| `Annotations` | Access annotation toolbar |
| `Print` | Print the PDF document |
| `Outline` | View document outline/bookmarks |
| `Search` | Find specific text in document |
| `Page layout mode` | Customize page display and layout |

### Separators
| Item | Description |
|------|-------------|
| `PageCountSeparator` | Separator between page number and count |
| `ZoomIconSeparator` | Separator before zoom button |
| `AnnotationSeparator` | Separator before annotations button |
| `PrintSeparator` | Separator after print button |
| `MoreOptionSeparator` | Separator before page layout mode |

---

## Desktop 2. Annotations Toolbar Items

**Location:** Annotation toolbar (appears below PrimaryToolbar)  
**Toolbar Name:** `AnnotationsToolbar`

### Text Markup
| Item | Description |
|------|-------------|
| `Text markups` | Annotate text in document |
| `Highlight` | Highlight selected text |
| `Underline` | Underline selected text |
| `Strikeout` | Strike-through selected text |
| `Squiggly` | Add squiggly line under text |

### Drawing & Freehand
| Item | Description |
|------|-------------|
| `Ink` | Draw freehand annotations |
| `Ink eraser` | Erase ink annotations |
| `Free text` | Add text annotations |

### Shapes
| Item | Description |
|------|-------------|
| `Shapes` | Add shapes menu |
| `Square` | Draw a square/rectangle |
| `Circle` | Draw a circle/ellipse |
| `Line` | Draw a straight line |
| `Arrow` | Draw an arrow |
| `Polyline` | Draw multi-segment lines |
| `Polygon` | Draw a polygon |
| `Cloud` | Draw a cloud shape |

### Special Annotations
| Item | Description |
|------|-------------|
| `Stamps` | Add built-in or custom stamps |
| `Sticky note` | Add sticky notes |
| `Signature` | Create and add signature |

### Formatting & Styling
| Item | Description |
|------|-------------|
| `Color picker` | Select and apply colors |
| `Thickness` | Set line/border thickness |
| `Font size` | Change text size |
| `Sticky note icons` | Select sticky note types |

### Actions
| Item | Description |
|------|-------------|
| `Delete` | Delete selected annotation |
| `ColorPickerSeparator` | Separator before color picker |
| `Close` | Close annotation toolbar |

---

## Desktop 3. Annotation Edit Toolbars

**Location:** Edit toolbar (appears when editing annotations)  
**Used in:** All 15 annotation edit toolbars

These toolbars share items with AnnotationsToolbar:
- `HighlightAnnotationEditToolbar`
- `UnderlineAnnotationEditToolbar`
- `StrikeOutAnnotationEditToolbar`
- `SquigglyAnnotationEditToolbar`
- `LineAnnotationEditToolbar`
- `ArrowAnnotationEditToolbar`
- `RectangleAnnotationEditToolbar`
- `CircleAnnotationEditToolbar`
- `PolygonAnnotationEditToolbar`
- `PolylineAnnotationEditToolbar`
- `FreeTextAnnotationEditToolbar`
- `InkAnnotationEditToolbar`
- `EraserEditToolbar`
- `StickyNoteAnnotationEditToolbar`
- `StampAnnotationEditToolbar`

**Common items in all edit toolbars:**
```
Text markups | Highlight | Underline | Strikeout | Squiggly | Ink | Ink eraser
Free text | Shapes | Square | Circle | Line | Arrow | Polyline | Polygon | Cloud
Stamps | Sticky note | Signature | Color picker | Thickness | Font size
Sticky note icons | Delete | Close
```

---

## Desktop Quick Reference

### PrimaryToolbar
```
Undo | Redo | Previous page | Next page | Page number entry | Page count
Zoom mode | Annotations | Print | Outline | Search | Page layout mode
[Separators: PageCountSeparator, ZoomIconSeparator, AnnotationSeparator, PrintSeparator, MoreOptionSeparator]
```

### AnnotationsToolbar
```
Text markups | Highlight | Underline | Strikeout | Squiggly | Ink | Ink eraser
Free text | Shapes | Square | Circle | Line | Arrow | Polyline | Polygon | Cloud
Stamps | Sticky note | Signature | Color picker | Thickness | Font size
Sticky note icons | Delete | ColorPickerSeparator | Close
```

### Annotation Edit Toolbars (All Types)
```
All items from AnnotationsToolbar
```

---

# Mobile Toolbar Items - Complete Reference

Easy-to-understand guide for customizing PDF Viewer toolbars on Mobile platforms.

---

## Mobile 1. Top Toolbar Items

**Location:** Top of the PDF Viewer  
**Toolbar Name:** `TopToolbar`

| Item | Description |
|------|-------------|
| `Undo` | Undo the last action |
| `Redo` | Redo the last undone action |
| `ZoomMode` | Adjust magnification/zoom level |
| `PageSettings` | Customize page display and layout |
| `Search` | Find specific text in document |
| `MoreItem` | Expand additional options |

---

## Mobile 2. Bottom Toolbar Items

**Location:** Bottom of the PDF Viewer  
**Toolbar Name:** `BottomToolbar`

| Item | Description |
|------|-------------|
| `TextMarkup` | Annotate text (highlight, underline, etc.) |
| `FreeText` | Add text annotations to document |
| `Ink` | Draw freehand annotations |
| `Eraser` | Erase ink annotations |
| `Shape` | Add shapes (lines, rectangles, circles) |
| `Stamp` | Add built-in or custom stamps |
| `Signature` | Create and add signature annotations |
| `StickyNote` | Add sticky notes to document |

---

## Mobile 3. Text Markup Toolbar Items

**Location:** Appears when text markup annotation selected  
**Toolbar Name:** `TextMarkupToolbar`

| Item | Description |
|------|-------------|
| `TextMarkupToolbarBackIcon` | Navigate back from toolbar |
| `Highlight` | Highlight selected text |
| `Underline` | Underline selected text |
| `StrikeOut` | Strike-through selected text |
| `Squiggly` | Add squiggly line under text |

---

## Mobile 4. Shape Annotations Toolbar Items

**Location:** Appears when shape annotation selected  
**Toolbar Name:** `ShapeAnnotationsToolbar`

| Item | Description |
|------|-------------|
| `ShapeToolbarBackIcon` | Navigate back from toolbar |
| `Line` | Draw a straight line |
| `Arrow` | Draw an arrow line |
| `Rectangle` | Draw a rectangle |
| `Circle` | Draw a circle/ellipse |
| `Polygon` | Draw a polygon |
| `Polyline` | Draw multi-segment lines |
| `Cloud` | Draw a cloud shape |

---

## Mobile 5. Annotation Edit Toolbar Items

**Location:** Appears when editing any annotation  
**Used in:** All annotation type edit toolbars

### Navigation & Type
| Item | Description |
|------|-------------|
| `SecondaryAnnotationBackIcon` | Navigate back from edit toolbar |
| `BackIconSeparator` | Separator after back button |
| `AnnotationType` | Show/indicate annotation type |
| `BorderStyle` | Set border/cloud style |

### Text & Size
| Item | Description |
|------|-------------|
| `TextColor` | Change text color |
| `TextSize` | Change text size |
| `TextPropertySeparator` | Separator after text properties |
| `TextFillColor` | Set text box fill color |

### Color & Style
| Item | Description |
|------|-------------|
| `StokeColor` | Set stroke/outline color |
| `FillColor` | Set fill color |
| `Thickness` | Set line/border thickness |
| `Opacity` | Set annotation opacity |

### Content & Actions
| Item | Description |
|------|-------------|
| `Edit` | Edit annotation content |
| `Notes` | Show sticky note icons |
| `DeleteSeparator` | Separator before delete button |
| `Delete` | Delete the annotation |

**Used in these edit toolbars:**
- `HighlightAnnotationEditToolbar`
- `UnderlineAnnotationEditToolbar`
- `StrikeOutAnnotationEditToolbar`
- `SquigglyAnnotationEditToolbar`
- `LineAnnotationEditToolbar`
- `ArrowAnnotationEditToolbar`
- `RectangleAnnotationEditToolbar`
- `CircleAnnotationEditToolbar`
- `PolygonAnnotationEditToolbar`
- `PolylineAnnotationEditToolbar`
- `FreeTextAnnotationEditToolbar`
- `InkAnnotationEditToolbar`
- `EraserEditToolbar`
- `StickyNoteAnnotationEditToolbar`
- `StampAnnotationEditToolbar`

---

## Mobile 6. Sticky Note Icons Toolbar Items

**Location:** Sticky note type selection  
**Toolbar Name:** `StickyNoteIconsToolbarView`

| Item | Description |
|------|-------------|
| `Note` | Add a note type sticky note |
| `Insert` | Add an insert type sticky note |
| `Comment` | Add a comment type sticky note |
| `Key` | Add a key type sticky note |
| `Help` | Add a help type sticky note |
| `Paragraph` | Add a paragraph type sticky note |
| `New Paragraph` | Add a new paragraph type sticky note |

---

## Mobile 7. More Option Toolbar Items

**Location:** More options menu  
**Toolbar Name:** `MoreOptionToolbar`

| Item | Description |
|------|-------------|
| `Outline` | View document outline/bookmarks |
| `Print` | Print the PDF document |

---

## Mobile 8. Search Toolbar Items

**Location:** Search panel  
**Toolbar Name:** `SearchToolbar`

| Item | Description |
|------|-------------|
| `SearchBackIcon` | Navigate back from search toolbar |
| `SearchEntry` | Text input field for search query |
| `SearchBusyIndicator` | Shows search is in progress |
| `ClearSearch` | Clear current search text |
| `ClearSeparator` | Separator after clear button |
| `PreviousSearch` | Go to previous search result |
| `NextSearch` | Go to next search result |
| `MoreOption` | Search with case sensitivity option |

---

## Mobile Quick Reference by Toolbar

### TopToolbar
```
Undo | Redo | ZoomMode | PageSettings | Search | MoreItem
```

### BottomToolbar
```
TextMarkup | FreeText | Ink | Eraser | Shape | Stamp | Signature | StickyNote
```

### TextMarkupToolbar
```
TextMarkupToolbarBackIcon | Highlight | Underline | StrikeOut | Squiggly
```

### ShapeAnnotationsToolbar
```
ShapeToolbarBackIcon | Line | Arrow | Rectangle | Circle | Polygon | Polyline | Cloud
```

### Edit Toolbars (All Annotation Types)
```
SecondaryAnnotationBackIcon | BackIconSeparator | AnnotationType | BorderStyle
TextColor | TextSize | TextPropertySeparator | TextFillColor
StokeColor | FillColor | Thickness | Opacity
Edit | Notes | DeleteSeparator | Delete
```

### StickyNoteIconsToolbarView
```
Note | Insert | Comment | Key | Help | Paragraph | New Paragraph
```

### MoreOptionToolbar
```
Outline | Print
```

### SearchToolbar
```
SearchBackIcon | SearchEntry | SearchBusyIndicator | ClearSearch | ClearSeparator
PreviousSearch | NextSearch | MoreOption
```

---

## Code Examples - Customize Toolbar Items

### 1. Remove Item by Name
Remove a specific toolbar item by its name using the `GetByName()` method:

```csharp
// Remove the "Undo" button from TopToolbar
var item = pdfViewer.Toolbars?.GetByName("TopToolbar")?.Items?.GetByName("Undo");
if (item != null)
{
    pdfViewer.Toolbars?.GetByName("TopToolbar")?.Items?.Remove(item);
}
```

### 2. Remove Item by Index
Remove a toolbar item by accessing it through its index:

```csharp
// Get the top toolbar of the PDF Viewer
Syncfusion.Maui.PdfViewer.Toolbar? topToolbar = pdfViewer.Toolbars?.GetByName("TopToolbar");
if (topToolbar != null)
{
    // Get the first item from the toolbar
    Syncfusion.Maui.PdfViewer.ToolbarItem? firstItem = topToolbar.Items?[0];
    if (firstItem != null)
    {
        // Remove the first item from the toolbar
        topToolbar?.Items?.Remove(firstItem);
    }
}
```

### 3. Remove Item from All Toolbars
Remove a specific item from all toolbars by iterating through the toolbar collection:

```csharp
// Remove "Sticky note" item from all toolbars
for (int i = 0; i < pdfViewer?.Toolbars?.Count; i++)
{
    var item = pdfViewer.Toolbars?[i]?.Items?.GetByName("Sticky note");
    if (item != null)
    {
        pdfViewer?.Toolbars?[i]?.Items?.Remove(item);
    }
}
```

### 4. Add Custom Item to Toolbar
Add a new custom button to a toolbar:

```csharp
// Create a custom button
Button fileOpenButton = new Button
{
    Text = "Open",           
    FontSize = 14,
    FontFamily = "Helvetica",
    HorizontalOptions = LayoutOptions.Center,
    VerticalOptions = LayoutOptions.Center,
    BackgroundColor = Colors.Transparent,
    BorderColor = Colors.Transparent,
    Padding = 10,
    Margin = new Thickness(5, 0, 0, 0)
};

// Add the button to PrimaryToolbar
pdfViewer.Toolbars?.GetByName("PrimaryToolbar")?.Items?.Add(
    new Syncfusion.Maui.PdfViewer.ToolbarItem(fileOpenButton, "FileOpenButton")
);
```

### 5. Insert Item at Specific Index
Insert a toolbar item at a specific position:

```csharp
// Create a custom button
Button fileSaveButton = new Button
{
    Text = "Save",           
    FontSize = 14,
    FontFamily = "Helvetica",
    HorizontalOptions = LayoutOptions.Center,
    VerticalOptions = LayoutOptions.Center,
    BackgroundColor = Colors.Transparent,
    BorderColor = Colors.Transparent,
    Padding = 10
};

// Find the Print item in PrimaryToolbar
var printItem = pdfViewer?.Toolbars?.GetByName("PrimaryToolbar")?.Items?.GetByName("Print");
if (printItem != null)
{
    // Insert the new button after the Print button
    pdfViewer?.Toolbars?.GetByName("PrimaryToolbar")?.Items?.Insert(
        printItem.Index + 1, 
        new Syncfusion.Maui.PdfViewer.ToolbarItem(fileSaveButton, "FileSaveButton")
    );
}
```

### 6. Hide Item by Name (Keep Visible Layout)
Hide a toolbar item while keeping the toolbar visible:

```csharp
// Hide the "Search" item in PrimaryToolbar
var item = pdfViewer.Toolbars?.GetByName("PrimaryToolbar")?.Items?.GetByName("Search");
if (item != null)
{
    item.IsVisible = false;  // Hide the item
}
```

### 7. Hide Item by Index
Hide a toolbar item by its index position:

```csharp
// Hide item at index 2 in PrimaryToolbar
int indexToHide = 2;
var toolbar = pdfViewer.Toolbars?.GetByName("PrimaryToolbar");
if (toolbar != null && indexToHide >= 0 && indexToHide < toolbar.Items?.Count)
{
    var item = toolbar.Items[indexToHide];
    item.IsVisible = false;  // Hide the item
}
```

### 8. Hide Entire Toolbar
Hide an entire toolbar including all its items:

```csharp
// Hide the bottom toolbar (annotation toolbar on mobile)
var bottomToolbar = pdfViewer.Toolbars?.GetByName("BottomToolbar");
if (bottomToolbar != null)
{
    bottomToolbar.IsVisible = false;
}
```

### 9. Hide Item from All Toolbars
Hide a specific item from all toolbars:

```csharp
// Hide "Signature" item from all toolbars
for (int i = 0; i < pdfViewer?.Toolbars?.Count; i++)
{
    var item = pdfViewer.Toolbars?[i]?.Items?.GetByName("Signature");
    if (item != null)
    {
        item.IsVisible = false;  // Hide the Signature item
    }
}
```

### 10. Keep Only Specific Items
Customize toolbar to show only selected items:

```csharp
// Keep only Undo, Redo, and ZoomMode in TopToolbar
var topToolbar = pdfViewer.Toolbars?.GetByName("TopToolbar");
if (topToolbar?.Items != null)
{
    var itemsToKeep = new[] { "Undo", "Redo", "ZoomMode" };
    var itemsToRemove = topToolbar.Items
        .Where(i => !itemsToKeep.Contains(i.Name))
        .ToList();
    
    foreach (var item in itemsToRemove)
        topToolbar.Items.Remove(item);
}
```

### 11. Show/Hide All Toolbars
Control visibility of all built-in toolbars:

```csharp
// Hide all toolbars
pdfViewer.ShowToolbars = false;

// Show all toolbars
pdfViewer.ShowToolbars = true;
```

### 12. Hide Specific Toolbar by Index
Hide a toolbar by its index in the collection:

```csharp
// Hide the first and second toolbars
if (pdfViewer?.Toolbars?.Count > 1)
{
    var firstToolbar = pdfViewer?.Toolbars[0];
    if (firstToolbar != null)
        firstToolbar.IsVisible = false;  // Hide first toolbar
        
    var secondToolbar = pdfViewer?.Toolbars[1];
    if (secondToolbar != null)
        secondToolbar.IsVisible = false;  // Hide second toolbar
}
```

---

## Important Notes

✅ **Separator items** provide visual breaks between tools  
✅ **Edit toolbar items** work with all 15 annotation types  
✅ **Customize based on requirements** - not all items need to be visible  

---

---

## Desktop vs Mobile Toolbar Comparison

| Feature | Desktop | Mobile |
|---------|---------|--------|
| Primary Toolbar | PrimaryToolbar | TopToolbar |
| Annotations | AnnotationsToolbar | BottomToolbar |
| Text Markup | Built into AnnotationsToolbar | TextMarkupToolbar |
| Shapes | Built into AnnotationsToolbar | ShapeAnnotationsToolbar |
| Pages | Previous, Next, Entry, Count | None (manual scroll) |
| Outline | Built into PrimaryToolbar | MoreOptionToolbar |
| Separators | 5 separator items | 8+ separator items |
| Edit Toolbars | 15 shared toolbars | 15 separate toolbars |

---

## References

- [Syncfusion MAUI PDF Viewer Toolbar Customization](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/maui/toolbar)
