# Common Scenarios in toolbar customization

## Scenario 1: Minimal Viewer (Read-Only)

Simple document viewer with minimal toolbar items:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).ToolbarSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings { ShowTooltip = true, ToolbarItems = new List<object> { "PageNavigationTool", "MagnificationTool", "PrintOption", "DownloadOption" }}).Render()
```

**Why this works:**
- Essential navigation and viewing controls
- Print and download capabilities
- Minimal UI clutter

## Scenario 2: Document Review with Custom Actions

Custom toolbar with application-specific functionality:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).ToolbarClick(onToolbarClick").Render()

<script>
    window.onload = function () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        var approveItem = {
            prefixIcon: 'e-icons e-check',
            id: 'approve',
            text: 'Approve',
            tooltipText: 'Approve this document',
            align: 'Right'
        };
        
        var rejectItem = {
            prefixIcon: 'e-icons e-close',
            id: 'reject',
            text: 'Reject',
            tooltipText: 'Reject this document',
            align: 'Right'
        };
        
        var commentItem = {
            prefixIcon: 'e-icons e-comment',
            id: 'add-comment',
            text: 'Comment',
            tooltipText: 'Add review comment',
            align: 'Right'
        };
        
        pdfViewer.toolbarSettings = {
            showTooltip: true,
            toolbarItems: [
                'OpenOption',
                'PageNavigationTool',
                'MagnificationTool',
                'PrintOption',
                'DownloadOption',
                'SearchOption',
                'AnnotationEditTool',
                approveItem,
                rejectItem,
                commentItem
            ]
        };
    };
    
    function onToolbarClick(args) {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        switch(args.item.id) {
            case 'approve':
                approveDocument();
                break;
            case 'reject':
                rejectDocument();
                break;
            case 'add-comment':
                openCommentDialog();
                break;
        }
    }
    
    function approveDocument() {
        console.log('Document approved');
        // Send approval to server
    }
    
    function rejectDocument() {
        console.log('Document rejected');
        // Send rejection to server
    }
    
    function openCommentDialog() {
        console.log('Comment dialog opened');
        // Open comment interface
    }
</script>
```

**Why this works:**
- Custom business logic buttons (Approve, Reject)
- Application-specific workflow integration
- Standard PDF operations still available