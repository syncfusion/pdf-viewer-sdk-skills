# Hyperlink Navigation

Brief: Hyperlink Navigation in Angular PDF Viewer enables users to interact with embedded links in PDF documents. Configure hyperlink behavior including enabling or disabling links, controlling how they open, and responding to hyperlink events for custom interactions.

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
By default, the Angular PDF Viewer automatically detects and enables all hyperlinks present in a loaded document. When set to `false`, all hyperlinks become non-interactive and users cannot click them.

### Usage
```typescript
import { Component } from '@angular/core';
import { LinkAnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                [enableHyperlink]='false'
                [documentPath]='document'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [LinkAnnotationService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
}
```

**Note**: Disabling hyperlinks only affects the viewer's behavior and does not alter the original PDF document.

---

## Controlling Link Open Behavior

Determine how external URLs are opened when a hyperlink is clicked.

### Property
`hyperlinkOpenState`

### Type
`LinkTarget` (Enum: `CurrentTab` | `NewTab` | `NewWindow`)

### Default Value
`CurrentTab`

### Description
Controls where external links open when clicked. Use `CurrentTab` to open in the current browser tab or `NewTab` to open in a new tab, preserving the user's current viewing session.

### Usage
```typescript
import { Component } from '@angular/core';
import { LinkAnnotationService, LinkTarget } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                [hyperlinkOpenState]='linkTarget'
                [documentPath]='document'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [LinkAnnotationService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public linkTarget: LinkTarget = LinkTarget.NewTab;
}
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
```typescript
import { Component } from '@angular/core';
import { LinkAnnotationService, HyperlinkClickEventArgs, HyperlinkMouseOverArgs } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                (hyperlinkClick)='onHyperlinkClick($event)'
                (hyperlinkMouseOver)='onHyperlinkMouseOver($event)'
                [documentPath]='document'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [LinkAnnotationService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

  onHyperlinkClick(args: HyperlinkClickEventArgs): void {
    console.log('Hyperlink Clicked:', args.hyperlink);
    // Prevent default navigation if needed
    // args.cancel = true;
  }

  onHyperlinkMouseOver(args: HyperlinkMouseOverArgs): void {
    console.log('Mouse over hyperlink:', args.hyperlinkElement.href);
  }
}
```

---

## Complete Configuration Example

Combine all hyperlink features in a single setup:

```typescript
import { Component } from '@angular/core';
import { LinkAnnotationService, LinkTarget, HyperlinkClickEventArgs, HyperlinkMouseOverArgs } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                [enableHyperlink]='true'
                [hyperlinkOpenState]='linkTarget'
                (hyperlinkClick)='onHyperlinkClick($event)'
                (hyperlinkMouseOver)='onHyperlinkMouseOver($event)'
                [documentPath]='document'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [LinkAnnotationService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public linkTarget: LinkTarget = LinkTarget.NewTab;

  onHyperlinkClick(args: HyperlinkClickEventArgs): void {
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
  }

  onHyperlinkMouseOver(args: HyperlinkMouseOverArgs): void {
    console.log('Preview link:', args.hyperlinkElement.href);
  }
}
```

### Configuration Summary
- Enable or disable hyperlinks with `enableHyperlink`
- Control link behavior with `hyperlinkOpenState`
- Use `hyperlinkClick` to customize link interactions
- Use `hyperlinkMouseOver` to provide visual feedback
- LinkAnnotationService must be included in providers for hyperlink functionality
