# General Properties in TypeScript PDF Viewer Component

**Description**: General properties provide core configuration for document display, server communication, and basic behavior in the Syncfusion TypeScript PDF Viewer. These properties control aspects such as width, height, document path, locale settings, resource loading, AJAX configuration, and performance optimization.

## Table of Contents
- [When to Use General Properties](#when-to-use-general-properties)
- [Property Reference Table](#property-reference-table)
- [CommandManager Configuration](#commandmanager-configuration)

---

## When to Use General Properties

Guide users to configure general properties when they need to:
- **Control document display**: Set width, height, document path, and basic page rendering
- **Customize viewer behavior**: Set locale, date/time formats for annotations
- **Optimize performance**: Configure initial render pages, retry settings, and zoom optimization
- **Integrate with servers**: Set service URLs, AJAX request headers, and server action settings
- **Configure resource loading**: Set resource URLs and custom fonts

**When NOT to use this reference:**
- **Feature enablement**: See enable-properties reference for feature toggles like `enableAnnotation`, `enableFormFields`, `enableDownload`, etc.
- **Annotation customization**: See annotation-settings reference for annotation appearance (colors, opacity, author)
- **Form field configuration**: See form-field-settings reference for form field appearance and validation
- **Other specific features**: See the feature-specific references

**Why this matters:** General properties provide core configuration for document display, server communication, and basic behavior. Other properties have been organized by feature area for easier discovery and management.

---

## Property Reference Table
The TypeScript PDF Viewer component provides a comprehensive set of general properties to configure document display, interaction, and behavior. These properties control aspects such as page rendering, zoom settings, annotation visibility, form field handling, and customization options.

### List of General Properties
| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **accessibilityTags** | Enable or disable the accessibility tags in PDF. | `boolean` | `false` |
| **ajaxRequestSettings** | Configure AJAX request headers and credentials for server communication. | `AjaxRequestSettings` | `null` |
| **commandManager** | Defines the collection of custom keyboard commands and their corresponding key gestures. See [CommandManager Configuration](#commandmanager-configuration) section below for usage and structure details. | `CommandManager` | `null` |
| **currentPageNumber** | Get or set the current page number displayed in the PDF Viewer. | `number` | `1` |
| **customFonts** | Add custom fonts for text rendering. | `string[]` | `null` |
| **documentPath** | Set the path of the PDF document to be displayed. | `string` | `null` |
| **fileName** | Get or set the filename of the loaded PDF document. | `string` | `null` |
| **height** | Set the height of the PDF Viewer container. | `string \| number` | `"100%"` |
| **initialRenderPages** | Set the number of pages to render initially for performance. | `number` | `3` |
| **interactionMode** | Set the interaction mode (text selection or panning). | `InteractionMode` | `InteractionMode.TextSelection` |
| **isCommandPanelOpen** | Get or set whether the command panel is open. | `boolean` | `false` |
| **isDocumentEdited** | Get whether the document has been edited. | `boolean` | `false` |
| **locale** | Set the locale for UI strings and date/time formats. | `string` | `"en-US"` |
| **pageCount** | Get the total page count of the loaded PDF document. | `number` | `0` |
| **resourceUrl** | Set the resource URL for loading PDF Viewer scripts and styles. | `string` | `"https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib"` |
| **retryCount** | Set the number of retries for failed requests. | `number` | `3` |
| **retryStatusCodes** | Set the HTTP status codes to retry on. | `number[]` | `[408, 429, 500, 502, 503, 504]` |
| **retryTimeout** | Set the timeout in milliseconds between retries. | `number` | `3000` |
| **scrollSettings** | Configure scroll behavior and settings. | `ScrollSettings` | `null` |
| **selectedItems** | Get or set the selected annotations and form fields. | `AnnotationBaseModel[]` | `null` |
| **serverActionSettings** | Configure server action URLs and settings. | `ServerActionSettings` | `null` |
| **serviceUrl** | Set the service URL for server-side operations. | `string` | `""` |
| **showNotificationDialog** | Show or hide notification dialogs. | `boolean` | `true` |
| **width** | Set the width of the PDF Viewer container. | `string \| number` | `"100%"` |

### Usage Examples

#### Setting Basic Properties
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  width: '1200px',
  height: '800px',
  currentPageNumber: 5,
  locale: 'en-US',
  showNotificationDialog: true
});
viewer.appendTo('#PdfViewer');
```

#### Configuring Performance Settings
```typescript
let viewer: PdfViewer = new PdfViewer({
  initialRenderPages: 5,
  retryCount: 5,
  retryTimeout: 5000,
  retryStatusCodes: [408, 429, 500, 502, 503, 504]
});

viewer.appendTo('#PdfViewer');
```

#### Setting AJAX Request Settings

```typescript
let viewer: PdfViewer = new PdfViewer({
  ajaxRequestSettings: {
    ajaxHeaders: [
      { headerName: 'Authorization', headerValue: 'Bearer token' }
    ],
    withCredentials: false
  }
});
```

#### Configuring Custom Fonts
```typescript
let viewer: PdfViewer = new PdfViewer({
  customFonts: ['Arial', 'Helvetica', 'Times New Roman', 'Courier']
});
```

#### Setting Scroll Settings
```typescript
let viewer: PdfViewer = new PdfViewer({
  scrollSettings: {
    delayPageRequestTimeOnScroll: 150
  }
});
```

#### Configuring Server Action Settings
```typescript
let viewer: PdfViewer = new PdfViewer({
  serverActionSettings: {
    load: 'Load',
    download: 'Download',
    renderPages: 'RenderPdfPages',
    print: 'PrintImages',
    renderThumbnail: 'RenderThumbnailImages'
  }
});
```

#### Dynamic Property Updates

```typescript
// Update current page
viewer.currentPageNumber = 10;
// Get page count
console.log('Total pages:', viewer.pageCount);
// Check if document is edited
console.log('Document edited:', viewer.isDocumentEdited);
// Get filename
console.log('Filename:', viewer.fileName);
```

#### Controlling Command Panel (Comments Panel)
Show or hide the command panel (comments/annotations panel) dynamically:

```typescript
import { PdfViewer, Toolbar, Annotation, CommentPanel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Annotation);
let viewer: PdfViewer = new PdfViewer({
  enableAnnotation: true
});
viewer.appendTo('#PdfViewer');
// Show command panel
viewer.isCommandPanelOpen = true;
// Hide command panel
viewer.isCommandPanelOpen = false;
// Toggle command panel
document.getElementById('toggleCommentPanel')?.addEventListener('click', () => {
  viewer.isCommandPanelOpen = !viewer.isCommandPanelOpen;
});
```

**Reference:** [isCommandPanelOpen Documentation](https://ej2.syncfusion.com/documentation/api/pdfviewer/index-default#iscommandpanelopen)

**Key Points:**
- `isCommandPanelOpen` is a read/write boolean property
- Returns `true` if the command panel is open, `false` if closed
- Can be set to show/hide the panel programmatically
- Requires `enableAnnotation: true` for the command panel to be functional
- This is more reliable than using `enableCommentPanel` for dynamic control

---

## CommandManager Configuration
The `commandManager` property allows you to define custom keyboard commands and their key gestures. It accepts a `CommandManager` object containing a `keyboardCommand` array.

### Usage

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, PdfKeys, ModifierKeys } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let viewer: PdfViewer = new PdfViewer({
  commandManager: {
    keyboardCommand: [
      {
        name: 'customCopy',
        gesture: {
          pdfKeys: PdfKeys.G,
          modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
        }
      },
      {
        name: 'customPaste',
        gesture: {
          pdfKeys: PdfKeys.H,
          modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
        }
      },
      {
        name: 'customCut',
        gesture: {
          pdfKeys: PdfKeys.Z,
          modifierKeys: ModifierKeys.Control
        }
      },
      {
        name: 'customSelectAll',
        gesture: {
          pdfKeys: PdfKeys.E,
          modifierKeys: ModifierKeys.Control
        }
      }
    ]
  }
});

viewer.appendTo('#PdfViewer');
```

### KeyboardCommandModel Properties

| **Property** | **Type** | **Description** |
|---|---|---|
| **name** | `string` | The name of the custom command |
| **gesture** | `KeyGesture` | The key gesture configuration (pdfKeys and modifierKeys combination) |

### KeyGesture Properties

| **Property** | **Type** | **Description** |
|---|---|---|
| **pdfKeys** | `PdfKeys` | The primary key for the gesture (e.g., `PdfKeys.G`, `PdfKeys.H`) |
| **modifierKeys** | `ModifierKeys` | The modifier keys (Shift, Alt, Control, Meta) combined using bitwise OR |

### Modifier Keys

Key modifiers used in gestures:

- **Control** corresponds to the Control key (value `1`) - `ModifierKeys.Control`
- **Alt** corresponds to the Alt key (value `2`) - `ModifierKeys.Alt`
- **Shift** corresponds to the Shift key (value `4`) - `ModifierKeys.Shift`
- **Meta** corresponds to the Command key on macOS or the Windows key on Windows (value `8`) - `ModifierKeys.Meta`

### Combining Modifier Keys

Use the bitwise OR operator (`|`) to combine multiple modifier keys:

```typescript
// Shift + Alt
modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
// Control + Shift
modifierKeys: ModifierKeys.Control | ModifierKeys.Shift
// Control + Alt + Shift
modifierKeys: ModifierKeys.Control | ModifierKeys.Alt | ModifierKeys.Shift
```

### Common PdfKeys
Common key values available in the `PdfKeys` enum:

- Letter keys: `PdfKeys.A` through `PdfKeys.Z`
- Number keys: `PdfKeys.Number0` through `PdfKeys.Number9`
- Function keys: `PdfKeys.F1` through `PdfKeys.F12`
- Navigation keys: `PdfKeys.Left`, `PdfKeys.Right`, `PdfKeys.Up`, `PdfKeys.Down`
- Special keys: `PdfKeys.Space`, `PdfKeys.Enter`, `PdfKeys.Delete`, `PdfKeys.Backspace`

### Default Value

By default, the `commandManager` is `null`, and the PDF Viewer uses standard keyboard shortcuts.

### Complete Example with Event Handling

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, PdfKeys, ModifierKeys } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib',
  commandManager: {
    keyboardCommand: [
      {
        name: 'customCopy',
        gesture: {
          pdfKeys: PdfKeys.G,
          modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
        }
      },
      {
        name: 'customPaste',
        gesture: {
          pdfKeys: PdfKeys.H,
          modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
        }
      },
      {
        name: 'customCut',
        gesture: {
          pdfKeys: PdfKeys.Z,
          modifierKeys: ModifierKeys.Control
        }
      },
      {
        name: 'customSelectAll',
        gesture: {
          pdfKeys: PdfKeys.E,
          modifierKeys: ModifierKeys.Control
        }
      }
    ]
  }
});
viewer.appendTo('#PdfViewer');
// Handle custom keyboard commands
document.addEventListener('keydown', (event: KeyboardEvent) => {
  // Check for custom copy command (Shift + Alt + G)
  if (event.shiftKey && event.altKey && event.key === 'g') {
    console.log('Custom copy command triggered');
    event.preventDefault();
  }
  // Check for custom paste command (Shift + Alt + H)
  if (event.shiftKey && event.altKey && event.key === 'h') {
    console.log('Custom paste command triggered');
    event.preventDefault();
  }
  // Check for custom cut command (Control + Z)
  if (event.ctrlKey && event.key === 'z') {
    console.log('Custom cut command triggered');
    event.preventDefault();
  }
  // Check for custom select all command (Control + E)
  if (event.ctrlKey && event.key === 'e') {
    console.log('Custom select all command triggered');
    event.preventDefault();
  }
});
```

### Why Use Custom Commands

Custom keyboard commands enable:
- **Workflow optimization**: Define shortcuts that match your application's specific workflow
- **Accessibility improvements**: Create alternative keyboard shortcuts for users with different accessibility needs
- **Integration**: Align PDF Viewer shortcuts with other parts of your application
- **Localization**: Adapt keyboard shortcuts to different regional keyboard layouts

### Notes
- Custom commands override default keyboard shortcuts for the same key combination
- Ensure custom shortcuts don't conflict with browser or OS shortcuts
- Test custom commands across different browsers and platforms
- Document custom shortcuts for end users
- The `commandManager` setup enables users to perform custom actions within the PDF Viewer by pressing specific key combinations, improving navigation and interaction efficiency

---

## Property Categories

### Document Configuration
- `documentPath`: Path to PDF document
- `fileName`: Document filename
- `resourceUrl`: Resource URL for scripts/styles

### Display Configuration
- `width`: Container width
- `height`: Container height
- `currentPageNumber`: Active page number
- `pageCount`: Total page count (read-only)

### Performance Configuration
- `initialRenderPages`: Initial page render count
- `retryCount`: Request retry attempts
- `retryTimeout`: Retry timeout duration
- `retryStatusCodes`: HTTP codes to retry

### Localization Configuration
- `locale`: UI locale setting
- `customFonts`: Custom font list

### Server Configuration
- `serviceUrl`: Server endpoint URL
- `serverActionSettings`: Server action mapping
- `ajaxRequestSettings`: AJAX headers/credentials

### Interaction Configuration
- `interactionMode`: Text selection or panning
- `scrollSettings`: Scroll behavior
- `commandManager`: Custom keyboard commands

### State Configuration
- `isDocumentEdited`: Document edit state (read-only)
- `isCommandPanelOpen`: Command panel state
- `selectedItems`: Selected annotations/fields
- `showNotificationDialog`: Notification visibility

### Accessibility Configuration
- `accessibilityTags`: Enable accessibility tags
- `commandManager`: Custom keyboard shortcuts

---

## Best Practices

### Performance Optimization
```typescript
let viewer: PdfViewer = new PdfViewer({
  documentPath: 'large-document.pdf',
  initialRenderPages: 5,  // Render 5 pages initially
  retryCount: 3,          // Retry failed requests 3 times
  retryTimeout: 3000      // Wait 3 seconds between retries
});
```

### Server Integration
```typescript
let viewer: PdfViewer = new PdfViewer({
  serviceUrl: 'https://your-server.com/api/pdfviewer',
  ajaxRequestSettings: {
    ajaxHeaders: [
      { headerName: 'Authorization', headerValue: 'Bearer YOUR_TOKEN' }
    ],
    withCredentials: true
  }
});
```

### Responsive Design
```typescript
let viewer: PdfViewer = new PdfViewer({
  width: '100%',    // Responsive width
  height: '100vh',  // Full viewport height
  locale: 'en-US'
});
```

### Custom Font Support
```typescript
let viewer: PdfViewer = new PdfViewer({
  customFonts: [
    'Arial',
    'Helvetica',
    'Times New Roman',
    'Courier New',
    'Georgia'
  ]
});
```

---

## Troubleshooting

### Document Not Loading
- Verify `documentPath` is correct and accessible
- Check `resourceUrl` points to valid library resources
- Ensure `serviceUrl` is reachable (for server-backed mode)
- Check browser console for CORS or network errors

### Poor Performance
- Reduce `initialRenderPages` value for faster initial load
- Increase `retryTimeout` if network is slow
- Check `retryStatusCodes` includes relevant error codes

### Keyboard Shortcuts Not Working
- Verify `commandManager` is properly configured
- Check for conflicts with browser shortcuts
- Ensure modifier keys are correctly combined with bitwise OR
- Test across different browsers and platforms

### AJAX Requests Failing
- Verify `ajaxRequestSettings` headers are correct
- Check `withCredentials` setting for cross-origin requests
- Ensure server accepts custom headers
- Verify authentication tokens are valid

### Custom Fonts Not Rendering
- Ensure fonts in `customFonts` array are installed on the system
- Check font names match exactly (case-sensitive)
- Verify fonts are accessible to the browser
- Test with standard fonts first before adding custom fonts
