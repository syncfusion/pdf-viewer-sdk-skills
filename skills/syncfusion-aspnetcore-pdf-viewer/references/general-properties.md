# General Properties in ASP.NET Core PDF Viewer Component

## Table of Contents
- [When to Use General Properties](#when-to-use-general-properties)
- [Property Reference Table](#property-reference-table)

---

## When to Use General Properties

Guide users to configure general properties when they need to:
- **Control document display**: Set width, height, document path, and basic page rendering
- **Customize viewer behavior**: Set locale, date/time formats for annotations
- **Optimize performance**: Configure initial render pages, retry settings, and zoom optimization
- **Integrate with servers**: Set service URLs, AJAX request headers, and server action settings
- **Configure resource loading**: Set resource URLs and custom fonts

**When NOT to use this reference:**
- **Feature enablement**: See [enable-properties.md](./enable-properties.md) for feature toggles like `enableAnnotation`, `enableFormFields`, `enableDownload`, etc.
- **Annotation customization**: See [annotation-settings.md](./annotation-settings.md) for annotation appearance (colors, opacity, author)
- **Form field configuration**: See [form-field-settings.md](./form-field-settings.md) for form field appearance and validation
- **Other specific features**: See the feature-specific references below

**Why this matters:** General properties provide core configuration for document display, server communication, and basic behavior. Other properties have been organized by feature area for easier discovery and management.

**Related References:**
- [enable-properties.md](./enable-properties.md) - Feature toggles for annotations, forms, toolbar, etc.
- [annotation-settings.md](./annotation-settings.md) - Annotation appearance and behavior customization
- [form-field-settings.md](./form-field-settings.md) - Form field appearance and validation
- [events.md](./events.md) - Event handlers for document interactions

---

## Property Reference Table

The React PDF Viewer component provides a comprehensive set of general properties to configure document display, interaction, and behavior. These properties control aspects such as page rendering, zoom settings, annotation visibility, form field handling, and customization options.

### How to Use Properties in PDF Viewer

```tsx
<ejs-pdfviewer
  zoomValue="150"
  pageCount="10"
  width="100%"
  height="100%"
  locale="en-US"
>
</ejs-pdfviewer>
```

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
| **isCommandPanelOpen** | Get or set whether the command panel is open. | `boolean` | `false` |
| **isDocumentEdited** | Get whether the document has been edited. | `boolean` | `false` |
| **locale** | Set the locale for UI strings and date/time formats. | `string` | `"en-US"` |
| **pageCount** | Get the total page count of the loaded PDF document. | `number` | `0` |
| **resourceUrl** | Set the resource URL for loading PDF Viewer scripts and styles. | `string` | `"https://cdn.syncfusion.com/react/syncfusion-react-pdfviewer-23.1.50/"` |
| **retryCount** | Set the number of retries for failed requests. | `number` | `3` |
| **retryStatusCodes** | Set the HTTP status codes to retry on. | `number[]` | `[408, 429, 500, 502, 503, 504]` |
| **retryTimeout** | Set the timeout in milliseconds between retries. | `number` | `3000` |
| **scrollSettings** | Configure scroll behavior and settings. | [`ScrollSettings`](#scrollsettings) | `null` |
| **selectedItems** | Get or set the selected annotations and form fields. | `IPageAnnotations[]` | `null` |
| **serverActionSettings** | Configure server action URLs and settings. | `ServerActionSettings` | `null` |
| **serviceUrl** | Set the service URL for server-side operations. | `string` | `"https://document.syncfusion.com/web-services/pdf-viewer/api/pdfviewer"` |
| **showNotificationDialog** | Show or hide notification dialogs. | `boolean` | `true` |
| **width** | Set the width of the PDF Viewer container. | `string \| number` | `"100%"` |


### CommandManager Configuration

The `commandManager` property allows you to define custom keyboard commands and their key gestures. It accepts a `CommandManager` object containing a `keyboardCommand` array.

**Structure:**
```cs
@{
    var commandManagerConfig = new
    {
        keyboardCommand = new[]
        {
            new
            {
                name = "customCopy",
                gesture = new
                {
                    pdfKeys = "G",
                    modifierKeys = "Shift|Alt"
                }
            },
            new
            {
                name = "customPaste",
                gesture = new
                {
                    pdfKeys = "H",
                    modifierKeys = "Shift|Alt"
                }
            }
        }
    };
    
    var commandManagerConfigJson =
        JsonSerializer.Serialize(commandManagerConfig);
}

<ejs-pdfviewer
    commandManager="@commandManagerConfig" >
</ejs-pdfviewer>
```

**KeyboardCommandModel Properties:**
| **Property** | **Type** | **Description** |
|---|---|---|
| **name** | `string` | The name of the custom command |
| **gesture** | `KeyboardEventArgs` | The key gesture configuration (pdfKeys and modifierKeys combination) |

**Default:** Empty array `[]`

### ScrollSettings

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **delayPageRequestTimeOnScroll** | Increase or decrease the delay time. | number |

