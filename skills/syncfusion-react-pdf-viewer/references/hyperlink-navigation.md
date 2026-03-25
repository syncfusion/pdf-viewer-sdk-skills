# Hyperlink Navigation

Brief: Hyperlink Navigation in PDF Viewer enables users to interact with embedded links in PDF documents. Configure hyperlink behavior including enabling/disabling links, controlling how they open, and responding to hyperlink events for custom interactions.

---

## Table of Contents
- [Enabling and Disabling Hyperlinks](#enabling-and-disabling-hyperlinks)
- [Controlling Link Open Behavior](#controlling-link-open-behavior)
- [Hyperlink Events](#hyperlink-events)
- [Complete Configuration Example](#complete-configuration-example)

---

## Enabling and Disabling Hyperlinks

Control whether hyperlinks in the PDF document are interactive or non-interactive.

### Property
`enableHyperlink`

### Type
`boolean`

### Default Value
`true`

### Description
By default, the PDF Viewer automatically detects and enables all hyperlinks present in a loaded document. When set to `false`, all hyperlinks become non-interactive and users cannot click them.

### Usage
```tsx
<PdfViewerComponent
  enableHyperlink={false}
>
</PdfViewerComponent>
```

**Note**: Disabling hyperlinks only affects the viewer's behavior and does not alter the original PDF document.

---

## Controlling Link Open Behavior

Determine how external URLs are opened when a hyperlink is clicked.

### Property
`hyperlinkOpenState`

### Type
`'CurrentTab' | 'NewTab'`

### Default Value
`'CurrentTab'`

### Description
Controls where external links open when clicked. Use `'CurrentTab'` to open in the current browser tab or `'NewTab'` to open in a new tab, preserving the user's current viewing session.

### Usage
```tsx
<PdfViewerComponent
  hyperlinkOpenState="NewTab"
>
</PdfViewerComponent>
```

---

## Hyperlink Events

Handle user interactions with hyperlinks using event handlers.

### hyperlinkClick Event

Triggered when a user clicks a hyperlink. Use this to implement custom logic like URL validation or preventing default navigation.

#### Event Arguments
- **hyperlink** (`string`): The URL of the clicked hyperlink
- **cancel** (`boolean`): Set to `true` to prevent the default navigation action

### hyperlinkMouseOver Event

Triggered when the mouse pointer hovers over a hyperlink. Use this to display custom tooltips or visual feedback.

#### Event Arguments
- **hyperlinkElement** (`HTMLAnchorElement`): The HTML anchor element corresponding to the hyperlink

### Usage
```tsx
const handleHyperlinkClick = (args: any) => {
  console.log('Hyperlink Clicked:', args.hyperlink);
  // Prevent default navigation if needed
  // args.cancel = true;
};

const handleHyperlinkMouseOver = (args: any) => {
  console.log('Mouse over hyperlink:', args.hyperlinkElement.href);
};

// Attach to PdfViewerComponent:
<PdfViewerComponent
  hyperlinkClick={handleHyperlinkClick}
  hyperlinkMouseOver={handleHyperlinkMouseOver}
>
</PdfViewerComponent>
```

---

## Complete Configuration Example

Combine all hyperlink features in a single setup:

```tsx
const onHyperlinkClick = (args: any) => {
  const url = args.hyperlink;
  console.log('User clicked link:', url);
  
  // Custom validation logic
  if (url.includes('trusted-domain.com')) {
    // Allow navigation
    args.cancel = false;
  } else {
    // Block suspicious links
    args.cancel = true;
    alert('This link is not allowed');
  }
};

const onHyperlinkMouseOver = (args: any) => {
  console.log('Preview link:', args.hyperlinkElement.href);
};

// Attach to PdfViewerComponent:
<PdfViewerComponent
  enableHyperlink={true}
  hyperlinkOpenState="NewTab"
  hyperlinkClick={onHyperlinkClick}
  hyperlinkMouseOver={onHyperlinkMouseOver}
>
</PdfViewerComponent>
```

### Configuration Summary
- Enable/disable hyperlinks with `enableHyperlink`
- Control link behavior with `hyperlinkOpenState`
- Use `hyperlinkClick` to customize link interactions
- Use `hyperlinkMouseOver` to provide visual feedback
