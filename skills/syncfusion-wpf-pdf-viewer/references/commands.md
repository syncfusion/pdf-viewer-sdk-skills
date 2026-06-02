# Commands in WPF Pdf Viewer
The Syncfusion WPF PdfViewer provides built-in commands for page navigation, zoom, text search, annotations, undo/redo, print, save, and unload operations that can be bound directly to UI elements via XAML or executed in code-behind.

## Navigate to First, Last, Previous, Next, and Specific Pages Using Button Click in XAML

```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="First Page" Command="{Binding ElementName=pdfViewerControl, Path=FirstPageCommand, Mode=OneWay}" />
<Button Content="Last Page" Command="{Binding ElementName=pdfViewerControl, Path=LastPageCommand, Mode=OneWay}" />
<Button Content="Previous Page" Command="{Binding ElementName=pdfViewerControl, Path=PreviousPageCommand, Mode=OneWay}" />
<Button Content="Next Page" Command="{Binding ElementName=pdfViewerControl, Path=NextPageCommand, Mode=OneWay}" />
<Button Content="Go to Page 2" Command="{Binding ElementName=pdfViewerControl, Path=GoToPageCommand, Mode=OneWay}" CommandParameter="2" />
```

## Navigate to a Specific Page Using GoToPageCommandParameter in XAML
The GoToPageCommandParameter specifies the target page index for navigation.
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Go to Page 5"
        Command="{Binding ElementName=pdfViewerControl, Path=GoToPageCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=GoToPageCommandParameter, Mode=
```
## Navigate to the First Page Using FirstPageCommandParameter in XAML
The FirstPageCommandParameter can be used to pass an optional parameter while executing the FirstPageCommand.
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="First Page"
        Command="{Binding ElementName=pdfViewerControl, Path=FirstPageCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=FirstPageCommandParameter, Mode=OneWay}" />
```
## Navigate to the Last Page Using LastPageCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Last Page"
        Command="{Binding ElementName=pdfViewerControl, Path=LastPageCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=LastPageCommandParameter, Mode=OneWay}" />
```

## Navigate to the Previous Page Using PreviousPageCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Previous Page"
        Command="{Binding ElementName=pdfViewerControl, Path=PreviousPageCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=PreviousPageCommandParameter, Mode=OneWay}" />
```
## Navigate to the Next Page Using NextPageCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Next Page"
        Command="{Binding ElementName=pdfViewerControl, Path=NextPageCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=NextPageCommandParameter, Mode=OneWay}" />
```
## Rotate Pages to a Specific Angle, Clockwise, or Counterclockwise Using Code-Behind

```csharp
// Rotate page 6 to 180 degrees
pdfViewer.PageOrganizer.RotatePagesCommand.Execute(new object[] { new int[] { 5 }, PdfPageRotateAngle.RotateAngle180 });

// Rotate pages 1 and 2 clockwise by 90 degrees
pdfViewer.PageOrganizer.RotatePagesClockwiseCommand.Execute(new int[] { 0, 1 });

// Rotate pages 1 and 2 counterclockwise by 90 degrees
pdfViewer.PageOrganizer.RotatePagesCounterclockwiseCommand.Execute(new int[] { 0, 1 });
```

## Remove a Specific Page by Zero-Based Index Using Code-Behind

```csharp
// Remove the 3rd page
pdfViewer.PageOrganizer.RemovePagesCommand.Execute(new int[] { 2 });
```

### Placeholders
- Replace `2` with the zero-based index of the page to remove.

## Zoom In and Zoom Out Using Button Click in XAML

```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Zoom In" Command="{Binding ElementName=pdfViewerControl, Path=IncreaseZoomCommand, Mode=OneWay}" />
<Button Content="Zoom Out" Command="{Binding ElementName=pdfViewerControl, Path=DecreaseZoomCommand, Mode=OneWay}" />
```
## Increase Zoom Level Using IncreaseZoomCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Zoom In"
        Command="{Binding ElementName=pdfViewerControl, Path=IncreaseZoomCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=Increase
```
## Decrease Zoom Level Using DecreaseZoomCommandParameter in XAML
The DecreaseZoomCommandParameter allows an optional parameter to be supplied when executing DecreaseZoomCommand.
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Zoom Out"
        Command="{Binding ElementName=pdfViewerControl, Path=DecreaseZoomCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=DecreaseZoomCommandParameter, Mode=OneWay}" />
```

## Search Next and Previous Occurrences of a Keyword Using Button Click in XAML

```xaml
<syncfusion:PdfViewerControl x:Name="PdfViewer" />
<Button Content="Search Next" Command="{Binding ElementName=PdfViewer, Path=SearchNextCommand, Mode=OneWay}" CommandParameter="keyword" />
<Button Content="Search Previous" Command="{Binding ElementName=PdfViewer, Path=SearchPreviousCommand, Mode=OneWay}" CommandParameter="keyword" />
```

### Placeholders
- Replace `keyword` with the text to search.

## Search Using SearchNextCommandParameter and SearchPreviousCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="PdfViewer" />
<Button Content="Search Next"
        Command="{Binding ElementName=PdfViewer, Path=SearchNextCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=PdfViewer, Path=SearchNextCommandParameter, Mode=OneWay}" />

<Button Content="Search Previous"
        Command="{Binding ElementName=PdfViewer, Path=SearchPreviousCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=PdfViewer, Path=SearchPreviousCommandParameter, Mode=OneWay}" />
```

## Enable Highlight, Underline, Strikethrough, Shape, and Ink Annotation Modes Using Button Click in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Highlight" CommandParameter="Highlight" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Underline" CommandParameter="Underline" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Strikethrough" CommandParameter="Strikethrough" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Line" CommandParameter="Line" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Rectangle" CommandParameter="Rectangle" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Circle" CommandParameter="Circle" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Arrow" CommandParameter="Arrow" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
<Button Content="Ink" CommandParameter="Ink" Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}" />
```
## Set Annotation Mode Using AnnotationCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Rectangle"
        Command="{Binding ElementName=pdfViewerControl, Path=AnnotationCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=AnnotationCommandParameter, Mode=OneWay}" />
```

## Undo and Redo the Last Annotation Action Using Button Click in XAML

```xaml
<syncfusion:PdfViewerControl x:Name="PdfViewer" />
<Button Content="Undo" Command="{Binding ElementName=PdfViewer, Path=UndoCommand, Mode=OneWay}" />
<Button Content="Redo" Command="{Binding ElementName=PdfViewer, Path=RedoCommand, Mode=OneWay}" />
```

## Disable Undo and Redo Functionality by Setting the History Limit to Zero
```csharp
pdfViewer.UndoRedoSettings.Limit = 0;
```

## Undo and Redo Operations Using UndoRedoSettings (Code-Behind)
The `UndoRedoSettings` property of the WPF PdfViewer provides APIs to **undo and redo user actions**.

Undo and redo actions should always be performed **only after checking their availability** using `CanUndo` and `CanRedo`.

## Undo the Most Recent Action Safely
Use `CanUndo` to determine whether an undo operation is possible before calling `PerformUndo()`.
```csharp
if (pdfViewer.UndoRedoSettings.CanUndo)
{
    pdfViewer.UndoRedoSettings.PerformUndo();
}
```
## Redo the Most Recently Undone Action Safely
Use `CanRedo` to determine whether a redo operation is possible before calling `PerformRedo()`.
```csharp
if (pdfViewer.UndoRedoSettings.CanRedo)
{
    pdfViewer.UndoRedoSettings.PerformRedo();
}
```

## Open the System Print Dialog Using Button Click in XAML

The print command opens the system print dialog, allowing the user to select a printer and configure print settings before sending the document to the printer. It can be bound to a button or menu item directly in XAML using standard WPF command binding. No additional parameters are required — invoking `PrintCommand` is sufficient to trigger the full print workflow. This command is useful for building custom toolbars where the built-in toolbar is hidden but printing functionality must still be exposed.

```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Print" Command="{Binding ElementName=pdfViewerControl, Path=PrintCommand, Mode=OneWay}" />
```
## Open Print Dialog Using PrintCommandParameter in XAML
```xaml
<syncfusion:PdfViewerControl x:Name="pdfViewerControl" />
<Button Content="Print"
        Command="{Binding ElementName=pdfViewerControl, Path=PrintCommand, Mode=OneWay}"
        CommandParameter="{Binding ElementName=pdfViewerControl, Path=PrintCommandParameter, Mode=OneWay}" />
```
## Save the Current PDF with Annotations and Form Data to a File Path Using Code-Behind

The save document command writes the current state of the loaded PDF — including any annotations, form field values, or page-level changes — to a file on disk. The target file path is passed directly as the command parameter when executing `SaveDocumentCommand` in code-behind. This is particularly important after annotation work, since all annotation types (ink, shape, text markup, stamp, sticky note, free text, etc.) are persisted into the saved file. If the path points to the same file that was loaded, the document is saved in-place; otherwise, a new file is created at the specified location.

```csharp
pdfViewerControl.SaveDocumentCommand.Execute(@"C:\Output.pdf");
```

### Placeholders
- Replace `C:\Output.pdf` with the desired output file path.

## Unload the Current PDF Document and Free Resources Using Button Click in XAML

The unload command releases the currently loaded PDF document from the viewer, clearing the display and freeing associated resources. It can be bound to a button in XAML and requires no command parameter. Unloading a document is useful when the user switches between files, closes a document explicitly, or when the application needs to free memory before loading a new PDF. After unloading, any unsaved annotation changes or edits will be lost, so it is good practice to invoke `SaveDocumentCommand` first if persistence is required.

```xaml
<syncfusion:PdfViewerControl x:Name="PdfViewer" />
<Button Content="Unload" Command="{Binding ElementName=PdfViewer, Path=UnloadCommand, Mode=OneWay}" />
```

## API Reference for All Commands, Properties, and Binding Patterns

The table below summarizes every command and related property covered in this document. Commands are bindable via XAML `Command` / `CommandParameter` attributes or executable in code-behind using the `.Execute()` method. Properties under settings objects (e.g., `UndoRedoSettings.Limit`) must be set in code-behind before or after the relevant operation.

| API | Type | Description |
|---|---|---|
| `FirstPageCommand` | Command | Navigates to the first page. |
| `FirstPageCommandParameter` | Property | Optional parameter for first-page navigation. |
| `LastPageCommand` | Command | Navigates to the last page. |
| `LastPageCommandParameter` | Property | Optional parameter for last-page navigation. |
| `PreviousPageCommand` | Command | Navigates to the previous page. |
| `PreviousPageCommandParameter` | Property | Optional parameter for previous-page navigation. |
| `NextPageCommand` | Command | Navigates to the next page. |
| `NextPageCommandParameter` | Property | Optional parameter for next-page navigation. |
| `GoToPageCommand` | Command | Navigates to the page specified by `CommandParameter`. |
| `GoToPageCommandParameter` | Property | Specifies the target page number. |
| `PageOrganizer.RotatePagesCommand` | Command | Rotates pages to a specified angle (0, 90, 180, 270). |
| `PageOrganizer.RotatePagesClockwiseCommand` | Command | Rotates pages 90° clockwise from the current angle. |
| `PageOrganizer.RotatePagesCounterclockwiseCommand` | Command | Rotates pages 90° counterclockwise from the current angle. |
| `PageOrganizer.RemovePagesCommand` | Command | Removes pages at the specified zero-based indices. |
| `IncreaseZoomCommand` | Command | Increases zoom by 25%. |
| `IncreaseZoomCommandParameter` | Property | Optional parameter for zoom-in behavior. |
| `DecreaseZoomCommand` | Command | Decreases zoom by 25%. |
| `DecreaseZoomCommandParameter` | Property | Optional parameter for zoom-out behavior. |
| `SearchNextCommand` | Command | Finds the next occurrence of the text in `CommandParameter`. |
| `SearchNextCommandParameter` | Property | Specifies the text to search. |
| `SearchPreviousCommand` | Command | Finds the previous occurrence of the text in `CommandParameter`. |
| `SearchPreviousCommandParameter` | Property | Specifies the text to search. |
| `AnnotationCommand` | Command | Sets annotation mode based on `CommandParameter` (Line, Circle, Rectangle, Arrow, Ink, Strikethrough, Highlight, Underline). |
| `UndoCommand` | Command | Reverts the most recent action. |
| `RedoCommand` | Command | Reapplies the most recently undone action. |
| `UndoRedoSettings.CanUndo` | Property | Gets a value indicating whether the most recent action can be undone. |
| `UndoRedoSettings.CanRedo` | Property | Gets a value indicating whether the most recent undone action can be redone. |
| `UndoRedoSettings.PerformUndo()` | Method | Undoes the most recent action if undo is available. |
| `UndoRedoSettings.PerformRedo()` | Method | Redoes the most recently undone action. |
| `UndoRedoSettings.Limit` | Property | Maximum number of undo/redo steps; set to `0` to disable undo/redo entirely. |
| `PrintCommand` | Command | Opens the print dialog. |
| `PrintCommandParameter` | Property | Optional parameter for print behavior. |
| `SaveDocumentCommand` | Command | Saves the PDF to the file path passed as the command parameter. |
| `UnloadCommand` | Command | Unloads the currently loaded PDF document. |
