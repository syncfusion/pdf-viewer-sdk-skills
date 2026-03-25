# Magnification

## Table of Contents
- [Overview](#overview)
- [When to Use Magnification Features](#when-to-use-magnification-features)
- [Magnification Component Properties](#magnification-component-properties)
- [Enabling Magnification](#enabling-magnification)
- [Zoom Operations](#zoom-operations)
  - [Incremental Zoom (ZoomIn/ZoomOut)](#incremental-zoom-zoominzoomout)
  - [Custom Zoom Levels](#custom-zoom-levels)
- [Fit-to-View Operations](#fit-to-view-operations)
  - [Fit to Page](#fit-to-page)
  - [Fit to Width](#fit-to-width)
- [Choosing the Right Zoom Approach](#choosing-the-right-zoom-approach)
- [Common Scenarios](#common-scenarios)
- [API Reference](#api-reference)

## Overview

The Magnification module provides zoom and scaling capabilities for PDF Viewer, enabling users to adjust document visibility from 10% to 400%. When implementing PDF viewing features, use magnification to improve document readability, allow detailed inspection, or fit documents to different viewport sizes.

## When to Use Magnification Features

Guide users to magnification features when they need to:

- **Inspect fine details** → Use incremental zoom (`zoomIn()`) or specific zoom levels (`zoomTo()`) for examining small text, images, or diagrams
- **Read long documents comfortably** → Use `fitToWidth()` to eliminate horizontal scrolling and maximize reading area
- **Get document overview** → Use `fitToPage()` to see entire pages at once for navigation or layout review
- **Create zoom controls** → Implement custom zoom buttons or sliders that let users adjust view dynamically
- **Support accessibility** → Provide zoom options for users with vision impairments who need larger text

## Magnification Component Properties

These properties are available directly on the `PdfViewerComponent` to control zoom and magnification functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **maxZoom** | Set the maximum zoom percentage allowed. | `number` | `400` |
| **minZoom** | Set the minimum zoom percentage allowed. | `number` | `50` |
| **restrictZoomRequest** | Restrict zoom to specific values. | `boolean` | `false` |
| **zoomMode** | Set the zoom mode (fitToPage, fitToWidth, etc.). | `ZoomMode` | `FitToPage` |
| **zoomPercentage** | Get the current zoom percentage. | `number` | `100` |
| **zoomValue** | Get or set the current zoom value. | `number` | `100` |

**Usage Example:**

```tsx
<PdfViewerComponent
  minZoom={10}
  maxZoom={400}
  zoomValue={125}
  zoomMode="FitToWidth"
  restrictZoomRequest={false}
>
  <Inject services={[Magnification]} />
</PdfViewerComponent>
```

## Enabling Magnification

Before using any zoom features, enable magnification in your PDF Viewer component. This activates the zoom toolbar buttons and programmatic zoom methods.

**Property:** `enableMagnification` (boolean)

```tsx
enableMagnification={true}
```

**Key Points:**
- Set to `true` to enable zoom and magnification tools in the toolbar
- The Magnification module must be injected into the Inject component for this to work
- Without this property, zoom methods will not function

---

## Zoom Operations

### Incremental Zoom (ZoomIn/ZoomOut)

Use incremental zoom when users need to gradually adjust magnification using predefined steps. This approach provides predictable zoom behavior and matches the built-in toolbar zoom dropdown values.

**When to guide users here:**
- User wants zoom in/out buttons that increment by standard steps
- User prefers consistent zoom levels (50%, 75%, 100%, 125%, etc.)
- User is creating toolbar-like controls that mirror the default UI

#### ZoomIn Method

**Method:** `viewerRef.current.magnification.zoomIn()`  
**Returns:** void  
**Range:** 10% to 400%

```tsx
const handleZoomIn = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.zoomIn();
  }
};
```

**Behavior:**
- Increments zoom to the next predefined value in the toolbar dropdown
- Each call steps through: 50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%

#### ZoomOut Method

**Method:** `viewerRef.current.magnification.zoomOut()`  
**Returns:** void  
**Range:** 10% to 400%

```tsx
const handleZoomOut = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.zoomOut();
  }
};
```

**Behavior:**
- Decrements zoom to the previous predefined value in the toolbar dropdown
- Each call steps backward through the zoom values

### Custom Zoom Levels

Use custom zoom levels when users need precise magnification control beyond the predefined steps. This approach is ideal for zoom sliders, percentage inputs, or application-specific zoom requirements.

**When to guide users here:**
- User wants a zoom slider with arbitrary values (e.g., 87%, 134%)
- User needs to set specific zoom on document load
- User is building custom zoom input fields
- User wants to remember and restore user-specific zoom preferences

#### ZoomTo Method

**Method:** `viewerRef.current.magnification.zoomTo(zoomValue: number)`  
**Parameters:**
- `zoomValue` (number): Zoom percentage value (range: 10–400%)

**Returns:** void

```tsx
const handleCustomZoom = (zoomPercentage) => {
  if (viewerRef.current) {
    viewerRef.current.magnification.zoomTo(zoomPercentage);
  }
};

// Example usage:
// handleCustomZoom(50);   // 50%
// handleCustomZoom(100);  // 100%
// handleCustomZoom(150);  // 150%
// handleCustomZoom(200);  // 200%
```

**Key Points:**
- Zoom values must be between 10% and 400%
- Values outside this range may be rejected or clamped to valid bounds
- Can be called during document load or dynamically during user interaction
- Useful for restoring saved zoom preferences or implementing zoom sliders

---

## Fit-to-View Operations

Use fit-to-view operations when users need automatic zoom adjustment based on viewport size. These methods calculate optimal zoom levels to display content without manual zooming.

### Fit to Page

Use this when users want to see the entire page at once, ideal for getting an overview or navigating through documents visually.

**When to guide users here:**
- User wants to see full page layout (both width and height)
- User needs document overview for navigation
- User is creating presentation mode or thumbnail views
- User wants to see page boundaries and margins

#### FitToPage Method

**Method:** `viewerRef.current.magnification.fitToPage()`  
**Returns:** void

```tsx
const handleFitToPage = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.fitToPage();
  }
};
```

**Behavior:**
- Automatically adjusts zoom so the entire page fits within the viewport
- Zoom level is recalculated based on viewport size and page dimensions
- Both width and height are considered for scaling
- Useful for presentation mode or getting a complete page overview

### Fit to Width

Use this when users want to maximize reading area by spanning text across the full viewport width, eliminating horizontal scrolling.

**When to guide users here:**
- User wants to read documents without horizontal scrolling
- User prefers maximum text size while keeping text visible
- User is reading column-based layouts or forms
- User wants continuous vertical scrolling for long documents

#### FitToWidth Method

**Method:** `viewerRef.current.magnification.fitToWidth()`  
**Returns:** void

```tsx
const handleFitToWidth = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.fitToWidth();
  }
};
```

**Behavior:**
- Adjusts zoom level so page width spans the full width of the viewport
- Vertical scrolling may be needed if page height exceeds viewport height
- Zoom level is calculated based on viewport width and page width
- Ideal for continuous reading without left-right panning

---

## Choosing the Right Zoom Approach

Guide users to select the appropriate zoom method based on their requirements:

| **User Need** | **Recommended Method** | **Why** |
|---------------|------------------------|---------|
| User wants standard zoom in/out buttons | `zoomIn()` / `zoomOut()` | Provides predictable, stepped zoom behavior matching toolbar |
| User wants zoom slider or percentage input | `zoomTo(value)` | Allows precise control over any zoom level within range |
| User wants to see full page layout | `fitToPage()` | Automatically scales entire page to viewport for overview |
| User wants maximum reading area | `fitToWidth()` | Eliminates horizontal scrolling, optimizes for vertical reading |
| User wants to set default zoom on load | `zoomTo(value)` | Sets specific zoom level when document opens |
| User wants accessible zoom controls | `zoomIn()` / `zoomOut()` + keyboard | Provides keyboard-friendly incremental zoom |

---

## Common Scenarios

### Scenario 1: Creating Custom Zoom Controls

When user needs zoom buttons in a custom toolbar:

```tsx
// Incremental zoom buttons
<button onClick={() => viewerRef.current.magnification.zoomIn()}>
  Zoom In
</button>
<button onClick={() => viewerRef.current.magnification.zoomOut()}>
  Zoom Out
</button>

// Preset zoom buttons
<button onClick={() => viewerRef.current.magnification.zoomTo(100)}>
  100%
</button>
<button onClick={() => viewerRef.current.magnification.zoomTo(150)}>
  150%
</button>
```

### Scenario 2: Implementing Zoom Slider

When user wants a slider for continuous zoom control:

```tsx
const [zoomLevel, setZoomLevel] = useState(100);

const handleSliderChange = (value) => {
  setZoomLevel(value);
  viewerRef.current.magnification.zoomTo(value);
};

<input 
  type="range" 
  min={10} 
  max={400} 
  value={zoomLevel} 
  onChange={(e) => handleSliderChange(Number(e.target.value))} 
/>
<span>{zoomLevel}%</span>
```

### Scenario 3: Setting Default Zoom on Load

When user wants specific zoom level when document opens:

```tsx
const documentLoaded = () => {
  // Set to 125% for better readability
  viewerRef.current.magnification.zoomTo(125);
  
  // Or fit to width for continuous reading
  // viewerRef.current.magnification.fitToWidth();
};

<PdfViewerComponent 
  documentLoad={documentLoaded}
  // ... other props
/>
```

### Scenario 4: Responsive Zoom Behavior

When user wants adaptive zoom based on viewport size:

```tsx
useEffect(() => {
  const handleResize = () => {
    if (viewerRef.current) {
      // Adjust zoom when window resizes
      viewerRef.current.magnification.fitToWidth();
    }
  };
  
  window.addEventListener('resize', handleResize);
  return () => window.removeEventListener('resize', handleResize);
}, []);
```

---

## API Reference

### Supported Zoom Range

The PDF Viewer magnification feature supports zoom values from **10% to 400%**. Any values outside this range may be rejected or automatically adjusted to the nearest valid boundary.

### Default Zoom Values in Toolbar Dropdown
- 50%
- 75%
- 100%
- 125%
- 150%
- 200%
- 250%
- 300%
- 400%

### Complete Integration Example

```tsx
const handleZoomLevel = (level) => {
  if (viewerRef.current) {
    viewerRef.current.magnification.zoomTo(level);
  }
};

const handleFitWidth = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.fitToWidth();
  }
};

const handleFitPage = () => {
  if (viewerRef.current) {
    viewerRef.current.magnification.fitToPage();
  }
};

// Usage examples:
// handleZoomLevel(100);   // 100%
// handleZoomLevel(150);   // 150%
// handleZoomLevel(200);   // 200%
// handleFitWidth();       // Fit to width
// handleFitPage();        // Fit to page
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.
