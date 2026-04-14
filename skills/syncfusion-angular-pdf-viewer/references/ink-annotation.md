# Ink Annotations in Angular PdfViewer Component

**Description**: Implement ink annotations (freehand drawing) in the Angular PdfViewer component using point-based path data. Add signatures, handwritten notes, sketches, and custom drawings programmatically by converting coordinate points to SVG path commands. This reference covers the correct path format, bounds calculation, and complete implementation patterns to avoid JSON parsing errors.

## Table of Contents
- [Overview](#overview)
- [Critical Implementation Details](#critical-implementation-details)
- [Path Data Format](#path-data-format)
- [Quick Start](#quick-start)
- [Complete Implementation](#complete-implementation)
- [Configuration Settings](#configuration-settings)
- [Common Use Cases](#common-use-cases)
- [Troubleshooting](#troubleshooting)

---

## Overview

Ink annotations enable freehand drawing on PDF documents by defining a series of coordinate points that form strokes. Each stroke is a continuous line connecting multiple points, and multiple strokes can be combined to create complex drawings.

**When to use:**
- Adding signatures to documents
- Creating handwritten notes or sketches
- Drawing custom markings or symbols
- Implementing approval marks (checkmarks, X marks)
- Adding freehand highlights or underlines

---

## Critical Implementation Details

### ⚠️ CRITICAL: Path Data Must Be SVG Commands as JSON String

**DO NOT** pass raw point arrays directly to the `path` property. The API expects SVG path commands in JSON string format.

**❌ INCORRECT - Will Cause JSON Parse Error:**
```typescript
// This will fail with "Unexpected non-whitespace character after JSON"
this.pdfViewer.annotation.addAnnotation('Ink', {
  path: [[100, 400], [110, 395], [120, 390]], // Raw array - WRONG!
  pageNumber: 1
});
```

**✅ CORRECT - SVG Path Commands as JSON String:**
```typescript
// Convert points to SVG path commands first
const pathCommands = [
  {"command":"M","x":100,"y":400},  // M = Move to (first point)
  {"command":"L","x":110,"y":395},  // L = Line to (subsequent points)
  {"command":"L","x":120,"y":390}
];
const pathData = JSON.stringify(pathCommands);

this.pdfViewer.annotation.addAnnotation('Ink', {
  path: pathData,  // JSON string - CORRECT!
  pageNumber: 1
});
```

---

## Path Data Format

### SVG Path Command Structure

Ink annotations use SVG path commands to define the drawing path:

| **Command** | **Meaning** | **When to Use** |
|------------|-------------|-----------------|
| **M** | Move To | First point of each stroke |
| **L** | Line To | All subsequent points in the stroke |

### Point-to-Path Conversion Algorithm

```typescript
// Input: Array of strokes, each stroke is an array of [x, y] points
const pointsList = [
  [[100, 400], [110, 395], [120, 390]],  // Stroke 1
  [[150, 420], [160, 425], [170, 430]]   // Stroke 2
];

// Step 1: Convert to SVG path commands
const pathCommands: any[] = [];

pointsList.forEach((stroke: any[]) => {
  if (stroke.length > 0) {
    // First point: Move To
    pathCommands.push({
      command: "M",
      x: stroke[0][0],
      y: stroke[0][1]
    });
    
    // Remaining points: Line To
    for (let i = 1; i < stroke.length; i++) {
      pathCommands.push({
        command: "L",
        x: stroke[i][0],
        y: stroke[i][1]
      });
    }
  }
});

// Step 2: Convert to JSON string
const pathData = JSON.stringify(pathCommands);
// Result: '[{"command":"M","x":100,"y":400},{"command":"L","x":110,"y":395},...]'
```

### Bounds Calculation

Calculate bounds automatically from all points to position the annotation correctly:

```typescript
// Flatten all points from all strokes
const allPoints = pointsList.flat();

// Extract x and y coordinates
const xValues = allPoints.map((p: number[]) => p[0]);
const yValues = allPoints.map((p: number[]) => p[1]);

// Calculate bounding box
const minX = Math.min(...xValues);
const minY = Math.min(...yValues);
const maxX = Math.max(...xValues);
const maxY = Math.max(...yValues);

// Use in annotation
const bounds = {
  offset: { x: minX, y: minY },
  width: maxX - minX,
  height: maxY - minY
};
```

---

## Quick Start

### Minimal Example

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="addInkSignature()">Add Signature</button>
    <ejs-pdfviewer 
      #pdfviewer
      [documentPath]="document"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent {
  @ViewChild('pdfviewer') pdfViewer!: PdfViewerComponent;
  
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

  addInkSignature(): void {
    // Define signature as points
    const points = [
      [100, 400], [110, 395], [120, 390], [130, 388],
      [140, 387], [150, 388], [160, 390], [170, 395]
    ];

    // Convert to SVG path commands
    const pathCommands = points.map((point, index) => ({
      command: index === 0 ? "M" : "L",
      x: point[0],
      y: point[1]
    }));

    // Add ink annotation
    this.pdfViewer.annotation.addAnnotation('Ink', {
      offset: { x: 100, y: 387 },
      width: 70,
      height: 13,
      pageNumber: 1,
      strokeColor: '#000080',
      thickness: 2,
      opacity: 1.0,
      path: JSON.stringify(pathCommands)
    } as any);
  }
}
```

---

## Complete Implementation

### Reusable Helper Method

Create a utility method to handle point conversion and annotation creation:

```typescript
/**
 * Adds an ink annotation from a list of coordinate points
 * @param pointsList Array of strokes (each stroke is an array of [x, y] points)
 * @param strokeColor Hex color code for the ink
 * @param thickness Line thickness (1-10)
 * @param opacity Transparency level (0-1)
 * @param pageNumber Target page number
 */
addInkAnnotation(
  pointsList: number[][][],
  strokeColor: string = '#FF0000',
  thickness: number = 2,
  opacity: number = 0.9,
  pageNumber: number = 1
): void {
  // Convert point arrays to SVG path command format
  const pathCommands: any[] = [];
  
  pointsList.forEach((stroke: number[][]) => {
    if (stroke.length > 0) {
      // First point uses "M" (move to)
      pathCommands.push({
        command: "M",
        x: stroke[0][0],
        y: stroke[0][1]
      });
      
      // Subsequent points use "L" (line to)
      for (let i = 1; i < stroke.length; i++) {
        pathCommands.push({
          command: "L",
          x: stroke[i][0],
          y: stroke[i][1]
        });
      }
    }
  });

  // Convert to JSON string
  const pathData = JSON.stringify(pathCommands);

  // Calculate bounds from all points
  const allPoints = pointsList.flat();
  const xValues = allPoints.map((p: number[]) => p[0]);
  const yValues = allPoints.map((p: number[]) => p[1]);
  const minX = Math.min(...xValues);
  const minY = Math.min(...yValues);
  const maxX = Math.max(...xValues);
  const maxY = Math.max(...yValues);

  // Add the ink annotation
  this.pdfViewer.annotation.addAnnotation('Ink', {
    offset: { x: minX, y: minY },
    width: maxX - minX,
    height: maxY - minY,
    pageNumber: pageNumber,
    strokeColor: strokeColor,
    thickness: thickness,
    opacity: opacity,
    path: pathData,
    author: 'Ink Reviewer'
  } as any);
}
```

### Usage Examples

```typescript
// Single stroke signature
addSimpleSignature(): void {
  const signature = [
    [100, 400], [110, 395], [120, 390], [130, 388], [140, 387],
    [150, 388], [160, 390], [170, 395], [180, 402], [190, 410]
  ];
  this.addInkAnnotation([signature], '#000080', 3, 1.0, 1);
}

// Multi-stroke drawing
addComplexDrawing(): void {
  const stroke1 = [[150, 350], [160, 345], [170, 342], [180, 340]];
  const stroke2 = [[150, 370], [160, 378], [170, 384], [180, 388]];
  const stroke3 = [[145, 350], [155, 360], [165, 370], [175, 380]];
  
  this.addInkAnnotation([stroke1, stroke2, stroke3], '#008000', 2, 0.9, 1);
}

// Checkmark
addCheckmark(): void {
  const stroke1 = [[300, 320], [310, 330], [320, 340]];
  const stroke2 = [[320, 340], [340, 310], [360, 280], [380, 250]];
  
  this.addInkAnnotation([stroke1, stroke2], '#00AA00', 3, 1.0, 1);
}
```

---

## Configuration Settings

### Ink Annotation Settings Property

Configure default ink annotation properties using `inkAnnotationSettings`:

```typescript
public inkAnnotationSettings = {
  strokeColor: '#FF0000',      // Default ink color
  thickness: 2,                // Default pen thickness (1-10)
  opacity: 0.9,                // Default opacity (0-1)
  author: 'Ink Reviewer'       // Default author name
};
```

### Binding to Component

```html
<ejs-pdfviewer 
  #pdfviewer
  [documentPath]="document"
  [resourceUrl]="resource"
  [inkAnnotationSettings]="inkAnnotationSettings"
  style="height:640px;display:block">
</ejs-pdfviewer>
```

### Available Settings Properties

| **Property** | **Description** | **Type** | **Default** |
|-------------|-----------------|----------|-------------|
| `strokeColor` | Ink path color | `string` | `"#FF0000"` |
| `thickness` | Line thickness (1-10) | `number` | `2` |
| `opacity` | Transparency (0-1) | `number` | `0.9` |
| `author` | Author name | `string` | `"Guest"` |
| `subject` | Annotation subject | `string` | `""` |
| `customData` | Custom metadata | `object` | `null` |
| `isLock` | Lock annotation | `boolean` | `false` |
| `annotationSelectorSettings` | Resize handle styling | `object` | Default settings |

---

## Common Use Cases

### Use Case 1: E-Signature Implementation

```typescript
addESignature(): void {
  // Realistic signature curve
  const signature = [
    [100, 400], [105, 398], [110, 396], [115, 394], [120, 393],
    [125, 392], [130, 392], [135, 393], [140, 395], [145, 398],
    [150, 402], [155, 407], [160, 413], [165, 419], [170, 425]
  ];
  
  this.addInkAnnotation(
    [signature],
    '#000080',  // Navy blue for formal documents
    3,          // Medium thickness
    1.0,        // Fully opaque
    1           // First page
  );
}
```

### Use Case 2: Approval Marks

```typescript
addApprovalCheckmark(): void {
  const checkStroke1 = [[300, 320], [310, 330], [320, 340]];
  const checkStroke2 = [[320, 340], [340, 310], [360, 280], [380, 250]];
  
  this.addInkAnnotation(
    [checkStroke1, checkStroke2],
    '#00AA00',  // Green for approval
    4,          // Thick for visibility
    1.0,
    1
  );
}

addRejectionX(): void {
  const xStroke1 = [[400, 250], [420, 270], [440, 290], [460, 310]];
  const xStroke2 = [[460, 250], [440, 270], [420, 290], [400, 310]];
  
  this.addInkAnnotation(
    [xStroke1, xStroke2],
    '#FF0000',  // Red for rejection
    4,
    1.0,
    1
  );
}
```

### Use Case 3: Handwritten Initials

```typescript
addInitials(): void {
  // Letter 'J'
  const letterJ = [
    [100, 300], [100, 310], [100, 320], [100, 330], [100, 340],
    [105, 345], [110, 348], [120, 350], [130, 348]
  ];

  // Letter 'D'
  const letterD = [
    [150, 300], [150, 310], [150, 320], [150, 330], [150, 340], [150, 350],
    [155, 350], [165, 348], [175, 343], [180, 335], [182, 325],
    [180, 315], [175, 307], [165, 302], [155, 300], [150, 300]
  ];

  this.addInkAnnotation([letterJ, letterD], '#0000FF', 2, 1.0, 1);
}
```

### Use Case 4: Freehand Highlight

```typescript
addHighlightUnderline(): void {
  // Wavy underline beneath text
  const wavyLine = [
    [50, 450], [60, 445], [70, 442], [80, 445], [90, 450],
    [100, 455], [110, 458], [120, 455], [130, 450], [140, 445],
    [150, 442], [160, 445], [170, 450], [180, 455], [190, 458]
  ];
  
  this.addInkAnnotation(
    [wavyLine],
    '#FF00FF',  // Bright color
    3,
    0.6,        // Semi-transparent
    1
  );
}
```

### Use Case 5: Custom Stamps/Symbols

```typescript
addStarSymbol(): void {
  // Create a star shape with multiple strokes
  const stroke1 = [[200, 200], [220, 250], [240, 200]];
  const stroke2 = [[200, 230], [240, 230]];
  const stroke3 = [[210, 250], [220, 200], [230, 250]];
  
  this.addInkAnnotation([stroke1, stroke2, stroke3], '#FFD700', 2, 1.0, 1);
}
```

---

## Troubleshooting

### Error: "Unexpected non-whitespace character after JSON"

**Cause:** Passing raw point arrays instead of JSON string with SVG path commands.

**Solution:**
```typescript
// ❌ WRONG
path: [[100, 400], [110, 395]]

// ✅ CORRECT
const pathCommands = [
  {"command":"M","x":100,"y":400},
  {"command":"L","x":110,"y":395}
];
path: JSON.stringify(pathCommands)
```

### Error: Ink not appearing on PDF

**Possible causes and solutions:**

1. **Points outside page bounds**
   - Solution: Verify coordinates are within page dimensions (typically 0-600 for x, 0-800 for y)

2. **Empty stroke array**
   - Solution: Ensure each stroke has at least 2 points

3. **Incorrect page number**
   - Solution: Use 1-based page numbering (first page = 1, not 0)

### Jagged or Angular Lines

**Cause:** Insufficient points between coordinates.

**Solution:** Add more intermediate points for smooth curves:

```typescript
// ❌ Jagged - only 3 points
const jagged = [[100, 100], [200, 150], [300, 100]];

// ✅ Smooth - many intermediate points
const smooth = [
  [100, 100], [110, 105], [120, 110], [130, 115], [140, 120],
  [150, 125], [160, 130], [170, 135], [180, 140], [190, 145],
  [200, 150], [210, 145], [220, 140], [230, 135], [240, 130],
  [250, 125], [260, 120], [270, 115], [280, 110], [290, 105],
  [300, 100]
];
```

### Poor Performance with Complex Drawings

**Cause:** Too many points or strokes.

**Solution:** Optimize point density:
- Target 5-15 pixels between points
- Simplify complex paths using curve-fitting algorithms
- Split very complex drawings into multiple annotations

---

## Best Practices

### 1. Point Density Guidelines

| **Use Case** | **Recommended Spacing** | **Example** |
|--------------|------------------------|-------------|
| Signatures | 5-10 pixels | Natural handwriting flow |
| Simple lines | 10-20 pixels | Clean, straight lines |
| Curves | 3-8 pixels | Smooth arcs and circles |
| Detailed drawings | 2-5 pixels | Complex shapes |

### 2. Color Selection

```typescript
// Document type-specific colors
const SIGNATURE_BLUE = '#000080';    // Formal documents
const APPROVAL_GREEN = '#00AA00';    // Approvals
const REJECTION_RED = '#FF0000';     // Rejections
const NOTE_PURPLE = '#800080';       // Comments
const HIGHLIGHT_YELLOW = '#FFFF00';  // Emphasis
```

### 3. Thickness Standards

```typescript
// Thickness guidelines
const FINE_LINE = 1;        // Detailed annotations
const STANDARD = 2;         // Normal signatures
const MEDIUM = 3;           // Visible markings
const BOLD = 4;             // Emphasis
const VERY_BOLD = 6-10;     // Highlights/stamps
```

### 4. Opacity Recommendations

```typescript
// Opacity by purpose
const SIGNATURE = 1.0;      // Fully opaque
const MARKUP = 0.8-0.9;     // Semi-opaque
const HIGHLIGHT = 0.3-0.6;  // Transparent overlay
```

### 5. Performance Optimization

```typescript
// Limit complexity
const MAX_POINTS_PER_STROKE = 1000;
const MAX_STROKES_PER_ANNOTATION = 50;

// Batch operations
function addMultipleInkAnnotations(annotations: any[]): void {
  annotations.forEach(anno => {
    this.addInkAnnotation(anno.points, anno.color, anno.thickness, anno.opacity, anno.page);
  });
}
```

---

## Advanced Techniques

### Programmatic Curve Generation

```typescript
// Generate smooth Bezier curve points
generateBezierCurve(
  start: [number, number],
  control1: [number, number],
  control2: [number, number],
  end: [number, number],
  steps: number = 20
): number[][] {
  const points: number[][] = [];
  for (let t = 0; t <= 1; t += 1/steps) {
    const x = Math.pow(1-t, 3) * start[0] + 
              3 * Math.pow(1-t, 2) * t * control1[0] +
              3 * (1-t) * Math.pow(t, 2) * control2[0] +
              Math.pow(t, 3) * end[0];
    const y = Math.pow(1-t, 3) * start[1] + 
              3 * Math.pow(1-t, 2) * t * control1[1] +
              3 * (1-t) * Math.pow(t, 2) * control2[1] +
              Math.pow(t, 3) * end[1];
    points.push([Math.round(x), Math.round(y)]);
  }
  return points;
}

// Usage
const curvePoints = this.generateBezierCurve(
  [100, 400], [150, 350], [200, 350], [250, 400], 30
);
this.addInkAnnotation([curvePoints], '#000080', 2, 1.0, 1);
```

### Touch/Mouse Drawing Capture

```typescript
// Capture user drawing input
private isDrawing = false;
private currentStroke: number[][] = [];

@HostListener('mousedown', ['$event'])
onMouseDown(event: MouseEvent): void {
  this.isDrawing = true;
  this.currentStroke = [];
  const point = this.getPagePoint(event);
  this.currentStroke.push(point);
}

@HostListener('mousemove', ['$event'])
onMouseMove(event: MouseEvent): void {
  if (this.isDrawing) {
    const point = this.getPagePoint(event);
    this.currentStroke.push(point);
  }
}

@HostListener('mouseup', ['$event'])
onMouseUp(event: MouseEvent): void {
  if (this.isDrawing) {
    this.isDrawing = false;
    if (this.currentStroke.length > 1) {
      this.addInkAnnotation([this.currentStroke], '#000000', 2, 1.0, 1);
    }
  }
}

private getPagePoint(event: MouseEvent): [number, number] {
  const clientPoint = { x: event.clientX, y: event.clientY };
  const pagePoint = this.pdfViewer.convertClientPointToPagePoint(clientPoint);
  return [pagePoint.x, pagePoint.y];
}
```

---

## Summary

**Key Takeaways:**
1. ✅ Always convert points to SVG path commands as JSON string
2. ✅ Use "M" for first point, "L" for subsequent points
3. ✅ Calculate bounds automatically from all points
4. ✅ Test with different stroke counts and point densities
5. ✅ Use appropriate colors, thickness, and opacity for the use case

**Common Mistakes to Avoid:**
- ❌ Passing raw point arrays to `path` property
- ❌ Forgetting to stringify SVG path commands
- ❌ Using incorrect command types
- ❌ Not calculating proper bounds
- ❌ Using page index 0 (use 1-based numbering)

**Quick Reference:**
```typescript
// Complete pattern
const points = [[[x1,y1], [x2,y2], [x3,y3]]];
const commands = points[0].map((p, i) => ({
  command: i === 0 ? "M" : "L",
  x: p[0],
  y: p[1]
}));

this.pdfViewer.annotation.addAnnotation('Ink', {
  offset: { x: minX, y: minY },
  width: maxX - minX,
  height: maxY - minY,
  pageNumber: 1,
  strokeColor: '#000080',
  thickness: 2,
  opacity: 1.0,
  path: JSON.stringify(commands)
} as any);
```
