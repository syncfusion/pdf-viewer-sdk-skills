# Printing and Organizing Pages

## Table of Contents

- [Overview](#overview)
- [Printing PDF Documents](#printing-pdf-documents)
- [Print Configuration](#print-configuration)
- [Page Manipulation](#page-manipulation)
- [Programmatic Operations](#programmatic-operations)

---

## Overview

The PDF Viewer provides comprehensive printing capabilities and page organization features to support document management workflows. Users can print documents with various configurations, while developers can organize and manipulate pages programmatically for document restructuring tasks.

**Key Printing and Organization Features:**
- Print entire documents or specific page ranges
- Custom print settings (orientation, scale, quality)
- Page rearrangement and reordering
- Page deletion and insertion
- Page rotation and transformation
- Programmatic page manipulation APIs
- Batch page operations

Enable printing and organization features to give users complete document management capabilities.

---

## Printing PDF Documents

The PDF Viewer includes built-in printing functionality accessible through the toolbar and programmatic API. Printing support enables users to create physical copies and export documents to paper or PDF files.

### Enable Print in Toolbar

The print button appears in the default toolbar when enabled:

```html
<ejs-pdfviewer enablePrint="true">
</ejs-pdfviewer>
```

### Programmatic Print

Programmatically print using the `print()` method in the `print` module of PDF Viewer instance:

```html
<script>
    function printPDF () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.print.print();
    }
</script>
```

---

## Print Configuration

Customize print behavior to meet specific requirements. The PDF Viewer provides several configuration options for controlling print output.



---

## Page Manipulation

Advanced page manipulation enables complex document restructuring scenarios like page extraction, copying, and merging.

### Extract Pages

Extract specific pages to create a new document:

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Extract pages to new document
function extractPagesToNewDocument(pageIndices) {
    // Send extracted pages to server for processing
    fetch('/api/pdf/extract', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            documentId: 'doc123',
            pages: pageIndices,
            outputFileName: 'ExtractedPages.pdf'
        })
    })
    .then(response => response.blob())
    .then(blob => {
        // Download extracted document
        const url = window.URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = 'ExtractedPages.pdf';
        link.click();
        window.URL.revokeObjectURL(url);
    });
}

// Extract first 5 pages
function extractFirstPages() {
    var pages = [];
    for (let i = 0; i < 5; i++) {
        pages.push(i);
    }
    extractPagesToNewDocument(pages);
}
```

---

## Programmatic Operations

Execute page operations through APIs for integration with document management workflows.

### Page Information Retrieval

Get information about pages:

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Get total page count
function getTotalPages() {
    return pdfViewer.pageCount;
}

// Get current page number
function getCurrentPage() {
    return pdfViewer.currentPageNumber;
}

// Get page dimensions
function getPageDimensions(pageIndex) {
    var totalPages = pdfViewer.pageCount;
    
    if (pageIndex < 0 || pageIndex >= totalPages) {
        console.error('Invalid page index');
        return null;
    }
    
    // Get page size information
    return {
        width: pdfViewer.pageSize[pageIndex]?.width,
        height: pdfViewer.pageSize[pageIndex]?.height
    };
}

// Log all page information
function logPageInfo() {
    var totalPages = getTotalPages();
    var currentPage = getCurrentPage();
    
    console.log(`Total Pages: ${totalPages}`);
    console.log(`Current Page: ${currentPage}`);
    
    for (let i = 0; i < totalPages; i++) {
        var dimensions = getPageDimensions(i);
        console.log(`Page ${i + 1}: ${dimensions?.width} x ${dimensions?.height}`);
    }
}
```

---

## Best Practices

1. **Validate page ranges**: Always check page indices before manipulation operations
2. **Provide user feedback**: Show progress for batch operations on large documents
3. **Enable undo/redo**: Consider maintaining operation history for user recovery
4. **Optimize print output**: Configure print quality based on use case (draft vs final)
5. **Handle page dependencies**: Consider how page manipulations affect annotations and forms
6. **Test page operations**: Verify document integrity after page modifications
7. **Secure operations**: Validate user permissions before allowing page manipulations