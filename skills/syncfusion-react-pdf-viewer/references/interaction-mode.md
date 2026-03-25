# Interaction Mode

## Table of Contents
- [When to Use Interaction Modes](#when-to-use-interaction-modes)
- [Selection Mode](#selection-mode)
- [Panning Mode](#panning-mode)
- [Decision Guide: Choosing the Right Mode](#decision-guide-choosing-the-right-mode)
- [Switching Between Modes](#switching-between-modes)
- [Required Services](#required-services)
- [Edge Cases and Troubleshooting](#edge-cases-and-troubleshooting)
- [Key Implementation Notes](#key-implementation-notes)

## When to Use Interaction Modes

Guide users to configure interaction modes when they need to:
- **Enable text selection and copying** for document review, quotation, or content extraction workflows
- **Enable touch-based scrolling** for mobile or tablet PDF viewing experiences
- **Switch between modes dynamically** based on user actions (e.g., toggle button, toolbar selection)
- **Optimize for specific use cases**: Reading mode (panning) vs. editing/review mode (selection)
- **Control user interactions** in restricted environments (view-only vs. interactive documents)

**Why this matters:** The interaction mode directly affects how users engage with PDF content. Selection mode supports text-based workflows (copying, highlighting, searching), while Panning mode provides fluid navigation for quick document browsing.

---

## Selection Mode

**User Need:** Users need to select and copy text from the loaded PDF document for quotations, citations, or documentation.

**When to use:** Document review workflows, research applications, content extraction tasks, or any scenario where users need to interact with PDF text.

### Property
`enableTextSelection`

### Description
A boolean property that controls whether text selection is enabled in the PDF Viewer. When set to `true`, users can select and copy text from the document.

### Usage
```tsx
<PdfViewerComponent
  enableTextSelection={true}
>
  <Inject services={[TextSelection]} />
</PdfViewerComponent>
```

**Result:** Users can click and drag to select text, then copy it to the clipboard. Panning is disabled to prevent accidental scrolling during text selection.

### Behavior
- When `enableTextSelection` is `true`, text selection mode is active
- Users can select text by clicking and dragging across content
- Text can be copied to clipboard
- Panning and touch scrolling are disabled to prevent selection interference

### Note
Text selection requires the `TextSelection` service to be injected in the component.

---

## Panning Mode

**User Need:** Users need to navigate through PDF documents quickly using drag gestures or touch scrolling, especially on mobile/tablet devices.

**When to use:** Mobile-friendly reading experiences, presentation mode, quick document browsing, or touch-enabled kiosks where text selection is not required.

### Property
`interactionMode`

### Description
Controls the interaction mode of the PDF Viewer. This property determines whether the viewer should be in panning mode or selection mode for document interaction.

### Usage
```tsx
<PdfViewerComponent
  enableTextSelection={false}
  interactionMode="Pan"
>
</PdfViewerComponent>
```

**Result:** Users can drag the document to scroll through pages. Touch gestures work smoothly on mobile devices. Text selection is disabled.

### Behavior
- When `enableTextSelection` is `false`, panning mode is active
- Users can drag the document to navigate through pages
- Touch scrolling is enabled for mobile and tablet devices
- Text selection is disabled to enable smooth panning

---

## Decision Guide: Choosing the Right Mode

**User wants to copy text or highlight content?**
→ Use Selection Mode (`enableTextSelection={true}`)

**User needs fluid scrolling on touch devices?**
→ Use Panning Mode (`enableTextSelection={false}`)

**User switches between reading and annotation tasks?**
→ Implement dynamic mode switching with state management (see example below)

**Application is mobile-first or kiosk-style?**
→ Default to Panning Mode for better touch UX

**Application is for research, legal review, or documentation?**
→ Default to Selection Mode for text interaction

---

## Switching Between Modes

**User Need:** Users need to switch between reading mode (panning) and review mode (text selection) without reloading the document.

**When to use:** Applications that support both casual browsing and detailed review workflows (e.g., document management systems, legal review tools).

### Implementation Strategy

To switch between modes, adjust the `enableTextSelection` property dynamically:

- **Selection Mode**: Set `enableTextSelection={true}` - Enables text selection, disables panning
- **Panning Mode**: Set `enableTextSelection={false}` - Enables panning, disables text selection

### Complete Example: Dynamic Mode Switching
```tsx
const [enableSelection, setEnableSelection] = React.useState(true);

const toggleMode = () => {
  setEnableSelection(!enableSelection);
};

// Button and component integration:
<button onClick={toggleMode}>
  Toggle Mode: {enableSelection ? 'Selection' : 'Panning'}
</button>

<PdfViewerComponent
  enableTextSelection={enableSelection}
>
</PdfViewerComponent>
```

---

## Required Services

Both interaction modes require specific services to be injected:

- **TextSelection Service**: Required for text selection functionality
- **Toolbar Service**: Recommended for user interface controls

### Service Injection
```typescript
<Inject services={[ Toolbar, TextSelection, TextSearch, Annotation, Magnification, 
                    Navigation, LinkAnnotation, BookmarkView, ThumbnailView, Print ]} />
```

---

## Edge Cases and Troubleshooting

**Text selection not working:**
- Verify `TextSelection` service is injected: `<Inject services={[TextSelection]} />`
- Ensure `enableTextSelection={true}` is set
- Check that the PDF contains selectable text (not scanned images)

**Panning feels unresponsive:**
- Confirm `enableTextSelection={false}` is set (text selection blocks panning)
- On mobile devices, ensure touch events aren't blocked by other UI elements
- Test on actual devices, not just browser emulators

**Mode switching doesn't take effect:**
- Verify state updates trigger re-render
- Check that prop value is actually changing in React DevTools
- Ensure no conflicting props override the mode setting

**Users accidentally select text when trying to scroll:**
- This indicates Selection Mode is active when Panning Mode is needed
- Set `enableTextSelection={false}` for reading-focused UX
- Provide a clear toggle button so users can switch modes intentionally

---

## Key Implementation Notes

- **Default Behavior**: By default, `enableTextSelection` is typically `true`, enabling text interaction
- **Performance**: Panning mode provides better scroll performance on lower-end devices when text selection is not needed
- **User Experience**: Selection mode is ideal for document review and text extraction; Panning mode is ideal for quick navigation and mobile browsing
- **Touch Devices**: Both modes support touch gestures, but Panning mode provides more intuitive touch scrolling
- **Service Dependencies**: TextSelection service is required for Selection Mode functionality
