## Common Annotation Use Cases

### 1. Document Review and Approval Workflow

**Scenario:** Legal department reviewing contracts

```javascript
// Reviewer adds comments and stamps
function reviewDocument() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Add sticky note for clause discussion
    viewer.annotation.addAnnotation("StickyNotes", {
        offset: { x: 450, y: 200 },
        pageNumber: 2
    });
    
    // Add highlight to important section
    viewer.annotation.setAnnotationMode('Highlight');
    // User selects text, then:
    
    // Add approval stamp
    viewer.annotation.addAnnotation("Stamp", {
        offset: { x: 400, y: 700 },
        pageNumber: 5
    }, 'Approved');
}
```

### 2. Technical Drawing Markup

**Scenario:** Engineering team reviewing blueprints

```javascript
// Add measurement annotations with scale
function markupBlueprint() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Configure scale (1 inch = 10 feet)
    viewer.measurementSettings = {
        scaleRatio: 10,
        conversionUnit: ej.pdfviewer.CalibrationUnit.Ft
    };
    
    // Add distance measurement
    viewer.annotation.addAnnotation("Distance", {
        offset: { x: 100, y: 150 },
        pageNumber: 1,
        vertexPoints: [{ x: 100, y: 150 }, { x: 400, y: 150 }]
    });
    
    // Add area calculation for room
    viewer.annotation.addAnnotation("Area", {
        offset: { x: 150, y: 300 },
        pageNumber: 1,
        vertexPoints: [
            { x: 150, y: 300 },
            { x: 350, y: 300 },
            { x: 350, y: 500 },
            { x: 150, y: 500 },
            { x: 150, y: 300 }
        ]
    });
}
```

### 3. Form Filling and Signature Collection

**Scenario:** HR collecting signed employment agreements

```javascript
// Add form fields and signature placeholders
function prepareEmploymentForm() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Add free text fields for employee information
    viewer.annotation.addAnnotation("FreeText", {
        offset: { x: 200, y: 100 },
        pageNumber: 1,
        width: 200,
        height: 30,
        defaultText: "Employee Name:",
        fontSize: 12,
        fontFamily: "Arial"
    });
    
    // Add signature placeholder
    viewer.annotation.addAnnotation("FreeText", {
        offset: { x: 200, y: 650 },
        pageNumber: 3,
        width: 200,
        height: 40,
        defaultText: "Signature:",
        fontSize: 10,
        borderStyle: 'dashed',
        borderColor: 'gray'
    });
    
    // Add date stamp
    viewer.annotation.addAnnotation("Stamp", {
        offset: { x: 450, y: 650 },
        pageNumber: 3
    }, 'Final');
}
```

### 4. Collaborative Document Review

**Scenario:** Team reviewing project proposal

```javascript
// Multiple reviewers adding feedback
function collaborativeReview() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Configure author for tracking
    viewer.stickyNotesSettings = {
        author: "John Doe"
    };
    
    // Add sticky note with comment
    viewer.annotation.addAnnotation("StickyNotes", {
        offset: { x: 500, y: 250 },
        pageNumber: 1,
        author: "John Doe"
    });
    // User adds comment text via UI
    
    // Highlight key section
    viewer.annotation.setAnnotationMode('Highlight');
    // User selects text
    
    // Add strikethrough for suggested deletion
    viewer.annotation.setAnnotationMode('Strikethrough');
    // User selects text to mark
}
```

### 5. Quality Assurance Markup

**Scenario:** QA team marking defects on product diagrams

```javascript
// Add visual markers for issues
function markDefects() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Circle defect location
    viewer.annotation.addAnnotation("Circle", {
        offset: { x: 250, y: 300 },
        pageNumber: 1,
        width: 60,
        height: 60,
        strokeColor: "red",
        thickness: 3
    });
    
    // Add arrow pointing to issue
    viewer.annotation.addAnnotation("Arrow", {
        offset: { x: 280, y: 330 },
        pageNumber: 1,
        vertexPoints: [
            { x: 280, y: 330 },
            { x: 350, y: 380 }
        ],
        strokeColor: "red"
    });
    
    // Add free text note
    viewer.annotation.addAnnotation("FreeText", {
        offset: { x: 360, y: 380 },
        pageNumber: 1,
        width: 150,
        height: 60,
        defaultText: "Defect ID: QA-2024-001\nSeverity: High\nArea: Top-right corner",
        fontSize: 10,
        fillColor: "lightyellow",
        borderColor: "red"
    });
}
```

### 6. Educational Content Annotation

**Scenario:** Instructor marking up course materials

```javascript
// Add teaching annotations
function annotateCourseMaterial() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    
    // Highlight key concepts
    viewer.annotation.setAnnotationMode('Highlight');
    // Instructor selects important text
    
    // Add sticky note with additional explanation
    viewer.annotation.addAnnotation("StickyNotes", {
        offset: { x: 50, y: 200 },
        pageNumber: 3
    });
    
    // Draw attention arrow
    viewer.annotation.addAnnotation("Arrow", {
        offset: { x: 100, y: 400 },
        pageNumber: 3,
        vertexPoints: [
            { x: 100, y: 400 },
            { x: 250, y: 450 }
        ],
        strokeColor: "blue",
        thickness: 2
    });
    
    // Add text box with study tip
    viewer.annotation.addAnnotation("FreeText", {
        offset: { x: 260, y: 455 },
        pageNumber: 3,
        width: 200,
        height: 50,
        defaultText: "💡 Study Tip: Review section 3.2 before exam",
        fontSize: 11,
        fillColor: "lightgreen"
    });
}
```