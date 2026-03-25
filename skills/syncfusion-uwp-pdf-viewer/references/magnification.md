# Magnification in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Zoom Commands](#zoom-commands)
- [Set Custom Zoom Percentage](#set-custom-zoom-percentage)
- [Get Current Zoom Value](#get-current-zoom-value)
- [View Modes](#view-modes)
- [Minimum Zoom Percentage](#minimum-zoom-percentage)
- [Disable Thumbnail View](#disable-thumbnail-view)

---

## Zoom Commands

Bind zoom commands to buttons when `DataContext` is `pdfViewer`:

```xaml
<Button Content="Zoom In"  Command="{Binding ElementName=pdfViewer, Path=IncreaseZoomCommand}"/>
<Button Content="Zoom Out" Command="{Binding ElementName=pdfViewer, Path=DecreaseZoomCommand}"/>
```

---

## Set Custom Zoom Percentage

Set a specific zoom level between 100 and 300:

```csharp
// Zoom to 140%
pdfViewer.ZoomTo(140);
```

---

## Get Current Zoom Value

```csharp
int currentZoom = pdfViewer.Zoom;
```

---

## View Modes

Three view modes are available via `PageViewMode`:

| Mode | Description |
|---|---|
| `PageViewMode.FitWidth` | Fits the page width to the viewer |
| `PageViewMode.Normal` | Default multi-page scrolling view |
| `PageViewMode.OnePage` | Single page view (flip mode, mobile only) |

```csharp
// Set to Fit Width
pdfViewer.ViewMode = PageViewMode.FitWidth;

// Set to Normal
pdfViewer.ViewMode = PageViewMode.Normal;

// Set to Single Page (mobile only)
pdfViewer.ViewMode = PageViewMode.OnePage;
```

From XAML buttons in a custom toolbar:

```csharp
private void FitWidthButtonClicked(object sender, RoutedEventArgs e)
{
    pdfViewer.ViewMode = PageViewMode.FitWidth;
}

private void OnePageButtonClicked(object sender, RoutedEventArgs e)
{
    pdfViewer.ViewMode = PageViewMode.OnePage;
}
```

> In Desktop view, when zoom drops below 100%, the view automatically switches to thumbnail mode.
> One page view is supported only in mobile view (flip view).

---

## Minimum Zoom Percentage

Set the minimum zoom level (accepted range: 10–100%):

```csharp
pdfViewer.MinimumZoomPercentage = 30;
```

> Values below 10% are treated as 10%, values above 100% are treated as 100%. Default is the fit-page zoom computed at runtime.

---

## Disable Thumbnail View

Prevent the automatic thumbnail view when zoom drops below 100%:

```csharp
pdfViewer.IsThumbnailViewEnabled = false;
```
