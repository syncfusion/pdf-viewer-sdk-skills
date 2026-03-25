# Magnifying PDF Documents

The WinForms PDF Viewer provides built-in zoom tools in the toolbar and programmatic APIs to control the magnification of the displayed PDF document.

## Zoom to a Specific Percentage

```csharp
// Zoom to 235 percentage.
pdfViewer.ZoomTo(235);
```

## Get the Current Zoom Percentage

```csharp
// Get the current zoom percentage.
int currentZoomPercentage = pdfViewer.ZoomPercentage;
```

## Set Zoom Mode

```csharp
// To apply fit-to-page zoom mode.
pdfViewer.ZoomMode = ZoomMode.FitPage;

// To apply fit-to-width zoom mode.
pdfViewer.ZoomMode = ZoomMode.FitWidth;
```
