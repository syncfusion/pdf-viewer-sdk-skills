---
name: syncfusion-aspnetcore-pdf-viewer
description: Implements the Syncfusion ASP.NET Core PDFViewer for embedding, configuring, and loading PDF documents. Use this when rendering PDFs in ASP.NET Core applications, embedding viewer controls, or generating Razor page (.cshtml) code for PDF display and interaction.
compatibility: .NET Version >= 8.0, .NET Framework >= 4.6.2
metadata:
  author: "Syncfusion Inc"
  version: "33.1.44"
---

# Syncfusion ASP.NET Core Pdfviewer – UI Sample Generator

## Generate Code for the User's Project *(default)*

**Trigger keywords:** "how to", "add pdfviewer", "code sample", "show me", "example", "snippet", "integrate", "component", "create sample", "ASP.NET Core sample".

**Purpose:** Generate minimal, copy-pasteable Razor + HTML code (.cshtml) that the user can integrate directly into their ASP.NET Core project.

**Workflow:**
**⚠️ CRITICAL — Feature Support Policy (STRICT MODE):**
 
**FUNDAMENTAL RULE:** Only generate code using APIs and properties that are EXPLICITLY listed in the reference files. ANY deviation is a VIOLATION.
 
- **MANDATORY CHECKS BEFORE GENERATING ANY CODE:**
  1. Search the reference files for the exact API/property name
  2. Verify it appears in the Method Reference, Properties, or Events tables
  3. If NOT found in ANY reference file, STOP immediately
  4. Do NOT generate or suggest undocumented APIs under any circumstances
 
- **STRICT ENFORCEMENT - ZERO TOLERANCE:**
  - **NO custom properties** - Only use properties from reference file tables
  - **NO invented methods** - Only use methods from reference file tables
  - **NO workarounds with undefined APIs** - Forbidden
  - **NO assumptions** about undocumented behavior - Forbidden
  - **NO alternative implementations** using guess-work - Forbidden
  - **NO pretending support exists** - Forbidden
 
- **MANDATORY RESPONSE FOR UNSUPPORTED FEATURES:**
  - **If a requested scenario/feature/API is NOT listed in any reference file, you MUST respond with:**
    ```
    "This feature is not supported in the current Syncfusion ASP.NET Core PDF Viewer implementation."
    ```
  - **Then list what IS supported** from the appropriate reference file
  - **Never suggest alternatives** unless explicitly documented in reference files
 
- **REFERENCE FILE HIERARCHY:**
  - Each reference file contains complete, authoritative documentation for its domain
  - The tables (Method Reference, Properties, Events) are the SOURCE OF TRUTH
  - Content outside these tables in reference files is explanatory only
  - Do NOT extend beyond what appears in the reference file tables
 
- **AUDIT YOUR GENERATION:**
  - Before providing any code, verify EVERY API used appears in a reference file table
  - Document which reference file each API comes from
  - If you cannot cite a reference file table entry, DELETE that code
 
- **This is a CRITICAL REQUIREMENT.** Violations compromise the skill's integrity and reliability.
 
#### Step 1 — Generate Code from Reference Files Only *(REQUIRED)*
- Read the relevant `references/*.md` file(s) for the requested feature
- Cross-reference EVERY API, property, and method against these tables
- **MANDATORY:** Before generating ANY code, verify that reference files exist and are accessible
- **Read the appropriate reference file(s)** for the requested feature:
  - Use `read_file` tool on relevant `references/*.md` files
  - Confirm file contains Methods/Properties/Events tables
  - Verify tables are complete and readable
- **If reference file is missing or cannot be read:**
  - STOP code generation
  - Respond: "Reference file for this feature is not available. Please ensure all reference files are present in the `references/` directory."
  - List the missing reference file name
- **This is a BLOCKER step:** Cannot proceed without reference file validation
- If an API/property does NOT appear in the reference file table, DO NOT USE IT
- Do NOT invent, guess, or suggest any API, method, property, class, or namespace not explicitly present in the reference files
 
---

## ⚙️ SETTINGS CONFIGURATION BEST PRACTICES

**When generating code with settings (toolbarSettings, annotationSettings, annotationSelectorSettings, arrowSettings, rectangleSettings, etc.), follow these guidelines to prevent unnecessary imports and over-engineering:**

### Rule 1: Simple Settings → Define as Razor inline code

**Use this approach when:**
- Configuring only 1-3 properties
- Settings are straightforward without custom types

**Example (DO THIS):**
```html
<ejs-pdfviewer
    annotationSelectorSettings="@(new {
        selectionBorderColor = "blue",
        resizerBorderColor = "red",
        resizerFillColor = "#4070ff",
        resizerSize = 8,
        selectionBorderThickness = 1,
        resizerShape = "Circle",
        selectorLineDashArray = new int[] { 5, 6 },
        resizerLocation = "Corners|Edges",
        resizerCursorType = "grab"
    })">
</ejs-pdfviewer>
```

**Benefits:**
- ✅ Simple and readable
- ✅ Less code clutter
- ✅ Type checking still works

---

### Rule 2: Complex Settings → Define as Razor code blocks outside HTML

**Use this approach when:**
- Configuring 4+ properties OR multiple related settings
- Using enums or complex configurations
- Need to reuse the same configuration across multiple components
- Settings are complex enough to warrant separate definition

**Example (DO THIS ONLY FOR COMPLEX CASES):**

```html
@{
    var annotationSelectorSettings = new {
        selectionBorderColor = "blue",
        resizerBorderColor = "red",
        resizerFillColor = "#4070ff",
        resizerSize = 8,
        selectionBorderThickness = 1,
        resizerShape = "Circle",
        selectorLineDashArray = new int[] { 5, 6 },
        resizerLocation = "Corners|Edges",
        resizerCursorType = "grab"
    };
}
<ejs-pdfviewer annotationSelectorSettings="@annotationSelectorSettings">
</ejs-pdfviewer>
```

---

### Rule 3: NEVER Over-Engineer Simple Cases

**❌ DO NOT DO THIS (Over-engineered):**
```html
@{
    var toolbarSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings  { ShowTooltip = true };
}
<ejs-pdfviewer
    toolbarSettings="@toolbarSettings"
>
</ejs-pdfviewer>
```

**✅ DO THIS INSTEAD (Simple & Clean):**
```html
<ejs-pdfviewer 
    toolbarSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings  { ShowTooltip = true })">
</ejs-pdfviewer>
```

---

### Checklist Before Generating Code

- [ ] **Count the settings properties:** 1-3? → Use inline | 4+? → Use separate razor code block
- [ ] **Is the component prop simple enough?** Yes → Keep inline | No → Extract to separate razor code block
- [ ] **Are Default values set for properties explicitly?** Yes → Remove | No → Keep it 

---

### Code References

All templates and operation snippets live in `references/*.md`. Each file is a focused snippet or template the agent will combine when generating samples.

**Flow:** Always start with `references/basic-sample.md`, then merge matched features into its anchors (PROPS, EVENTS, UI_BUTTONS, HANDLERS). If no keyword matches, return only the basic sample.

---

## Reference File Routing Guide

### 🎯 Core Setup & Configuration

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **basic-sample.md** | Minimal PDFViewer with documentPath, height, and width. Base template for all samples. | "basic setup", "minimal example", "getting started", "how to load PDF" |
| **general-properties.md** | Configure core viewer properties (server URL, document path, locale, resource base path). | "configuration", "server settings", "locale", "document path setup" |

### Navigation Features
 
**Read file when:** Implementing page navigation, bookmarks, thumbnails, hyperlinks, or table of contents
- Page navigation (first, last, previous, next, go to page)
- Bookmark creation and navigation
- Thumbnail view and thumbnail navigation
- Hyperlink support (internal and external links)
- Table of contents navigation
- Programmatic navigation methods
- Navigation-related events
📄 **Read:** [references/navigation.md](references/navigation.md)  

### Core Viewing and Interaction
 
**Read file when:** Understanding interaction modes, scrolling, and core viewing features
- Interaction modes (Text Selection, Pan, None)
- Page scrolling and viewing behavior
- Panning operations
- Feature modules for modular architecture
- Enabling and disabling specific features
- Core viewing capabilities
📄 **Read:** [references/viewing-and-interaction.md](references/viewing-and-interaction.md)  

**Read file when:** Implementing zoom functionality, fit-to-page modes, or custom zoom levels
- Zoom levels and zoom percentages
- Zoom modes (fit to page, fit to width, fit to visible area, automatic)
- Custom zoom control
- Programmatic zoom operations
- Zoom toolbar configuration
- Mouse wheel zoom behavior
📄 **Read:** [references/magnification.md](references/magnification.md)  

### Toolbar Configuration
 
**Read file when:** Customizing PDF viewer toolbar, showing/hiding toolbar items, or creating custom toolbars
- Built-in toolbar overview
- Primary toolbar customization
- Annotation toolbar configuration
- Form designer toolbar setup
- Mobile toolbar adaptation
- Custom toolbar creation from scratch
- Toolbar item visibility control
- Toolbar positioning and layout
- Toolbar click events and handlers
📄 **Read:** [references/toolbar-customization.md](references/toolbar-customization.md)  

### Annotations and Markup
 
**Read file when:** Adding annotations, markup tools, signatures, measurements, or redaction to PDFs
- Annotation types overview and capabilities
- Text markup (highlight, underline, strikethrough)
- Shape annotations (line, arrow, rectangle, circle, polygon)
- Stamp annotations (built-in stamps and custom images)
- Ink/freehand drawing annotations
- Sticky notes and comment annotations
- Handwritten and digital signatures
- Measurement annotations (distance, perimeter, area, volume)
- Redaction annotations
- Annotation toolbar configuration
- Import and export annotations
- Annotation settings and customization
📄 **Read:** [references/annotations-overview.md](references/annotation-overview.md)

### Forms Management
  
**Read file when:** Filling PDF forms, designing forms, managing form fields, or validating form data
- Form filling vs form designing
- Form field types (textbox, password, checkbox, radio button, dropdown, listbox, signature)
- Creating form fields programmatically
- Form designer toolbar and UI interactions
- Form field properties and customization
- Form field validation rules
- Form constraints and settings
- Form field API methods
- Import and export form data
- Custom data in form fields
📄 **Read:** [references/forms-overview.md](references/form-fields-overview.md)

### Text Operations
 
**Read file when:** Implementing text search, finding text in PDFs, or highlighting search results
- Text search functionality
- Search options (case-sensitive, whole word matching)
- Highlighting search results
- Find next and previous occurrences
- Programmatic text search methods
- Search completion events
- Custom search highlight colors
📄 **Read:** [references/text-search.md](references/text-search.md)  
 
**Read file when:** Enabling text selection, copying text, or extracting text from PDFs
- Text selection modes and behavior
- Copying selected text to clipboard
- Text selection events
- Programmatic text selection
- Extracting text from PDF pages
- Text extraction options and settings
- Text collections and text bounds
📄 **Read:** [references/text-selection.md](references/text-selection.md)  

### Document Operations
 
**Read file when:** Loading PDF documents from various sources, handling encrypted PDFs, or managing document loading
- Loading PDF from URL (HTTP/HTTPS)
- Loading PDF from local file paths
- Loading PDF as base64 string
- Opening encrypted/password-protected PDFs
- Programmatic document loading
- Document load events and lifecycle
- Handling load failures and errors
📄 **Read:** [references/opening-pdfs.md](references/opening-pdfs.md)  
 
**Read file when:** Downloading PDFs, saving modifications, or exporting PDF data
- Downloading PDF documents
- Saving PDFs with annotations and modifications
- Download with form data included
- Retrieving PDF as base64 data
- Download events and customization
- Custom download filenames
📄 **Read:** [references/saving-and-downloading.md](references/saving-and-downloading.md)  
 
**Read file when:** Printing PDFs, organizing pages, rearranging, rotating, or extracting pages
- Printing PDF documents from browser
- Print options (page range, print quality)
- Silent printing configuration
- Print events
- Page organization overview
- Rearranging and reordering pages
- Rotating pages (90°, 180°, 270°)
- Deleting pages from PDF
- Copying and duplicating pages
- Extracting pages to new document
- Page organizer toolbar
- Programmatic page organization
- Mobile view for page organization
📄 **Read:** [references/printing-and-organizing.md](references/printing-and-organizing.md)  

### ⚙️ Advanced Features

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **api-methods.md** | Programmatic control: load documents, manage forms, annotations, extract text, undo/redo, navigation APIs. | "load PDF programmatically", "API methods", "export form data", "extract text", "undo/redo", "programmatic control" |
| **events.md** | Complete list of all PDFViewer events (document load, download, annotations, forms, search, navigation). | "event list", "all events", "available events", "event reference", "event handlers" |

---
