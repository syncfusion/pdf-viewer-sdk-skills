# Common Scenarios in toolbar customization

## Scenario 1: Minimal Viewer (Read-Only)

Simple document viewer with minimal toolbar items:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
                       ShowTooltip = true,
                       ToolbarItems = new List<object> {
                           "PageNavigationTool",
                           "MagnificationTool",
                           "PrintOption",
                           "DownloadOption"
                       }
                   })">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Essential navigation and viewing controls
- Print and download capabilities
- Minimal UI clutter

## Scenario 2: Document Review with Custom Actions

Custom toolbar with application-specific functionality:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarClick="onToolbarClick">
    </ejs-pdfviewer>
</div>

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