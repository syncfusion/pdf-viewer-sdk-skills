# Syncfusion Flutter PdfViewer skill

## Overview
Create Flutter applications featuring the Syncfusion Flutter SfPdfViewer, customized to meet specific user requirements.

See **[SKILL.md](SKILL.md)** for the full intent-routing guide and rules.

---

## Key Capabilities

- **High-fidelity PDF rendering & navigation:** PDF viewing, bookmark navigation, hyperlink navigation, page navigation, scrolling, and magnification.
- **Text search & selection:** Search text, navigate results, and customise highlight colors; enable/disable text selection with custom selection color.
- **Annotation support:** Add, remove, select, and manage text markup (Highlight, Underline, Strikethrough, Squiggly) and Sticky Note annotations.
- **Form filling:** Fill, edit, save, export, import, and clear AcroForm fields (text box, checkbox, radio button, combo box, list box, signature).
- **Accessibility & localization:** Screen reader support, RTL rendering, and localization into any supported language.

---

## Getting Started

### How to Integrate Skills

**Step 1: Checkout and copy the required skills**

Clone or download the PDF-Viewer-SDK-Skills repository and copy the **flutter-pdfviewer-code-generator** skill from the `skills/` directory.

**Step 2: Install the skill**

Place the copied skill folders in your workspace following this structure:

```
your-workspace/
├── .github/skills/          # or .claude/skills/ or .codestudio/skills/
│   └── flutter-pdfviewer-code-generator/
│       └── SKILL.md
├── your-project-files...
└── lib/main.dart
```

**Step 3: Verify and manage your skills**

Type `/skills` in the GitHub Copilot or Code Studio chat to quickly access the Configure Skills menu and manage your installed skills.

**Step 4: Use skills in VS Code**

There are two ways to use skills:

1. **Slash commands** - Type `/` in the GitHub Copilot chat to see available skills.

2. **Automatic loading** - Simply describe your task naturally, and your AI Agent automatically loads the relevant skill:
   ```
   Create a Flutter app with SfPdfViewer that loads a PDF document from a URL
   ```

When the flutter-pdfviewer-code-generator skill is loaded, the AI Agent provides focused Dart snippets and commands for Syncfusion Flutter SfPdfViewer.

### Prerequisites

- **Flutter** 3.x or later
- **Dart** 3.x or later

### pub.dev Packages

```bash
flutter pub add syncfusion_flutter_pdfviewer
```

---

## Example Prompts

#### Code Generation
*Use these when you want Dart code for your existing Flutter project.*

- "Create a Flutter app that adds a Syncfusion SfPdfViewer, loads a PDF from a network URL, and shows zoom controls."
- "Add code to search for text inside the PDF and navigate between search results."
- "Show how to navigate to a specific page programmatically using PdfViewerController."
- "Add annotation support to highlight and underline text in the PDF."
- "Show how to fill and save AcroForm fields in a PDF document."
- "Enable RTL layout for the SfPdfViewer widget."
- "Add localization support for the SfPdfViewer UI in French."

---

## Code References

All templates and operation snippets live in `references/*.md`. Each file is a focused snippet the agent combines when generating samples.

| File | Purpose |
|---|---|
| **basic-sample.md** | Minimal SfPdfViewer with a network/asset URL, Scaffold, and AppBar. |
| **magnification.md** | Configure zoom level, max zoom, double-tap zoom, and zoom callbacks. |
| **page-navigation.md** | Navigate pages programmatically using controller methods. |
| **text-search.md** | Search text, navigate results, and customise highlight colors. |
| **text-selection.md** | Enable/disable text selection and handle selection callbacks. |
| **bookmark-navigation.md** | Open the built-in bookmark view and navigate programmatically. |
| **scrolling.md** | Programmatic scrolling and reading current scroll offset. |
| **pdfviewer-properties.md** | Common SfPdfViewer widget properties reference. |
| **annotation.md** | Add, remove, and manage text markup and Sticky Note annotations. |
| **signaturepad.md** | Custom signature pad dialog integration with form fields. |
| **password-protected-pdf.md** | Open encrypted PDFs using the `password` property. |
| **link-navigation.md** | Enable document link navigation and handle hyperlink taps. |
| **form-filling.md** | Fill, edit, save, export, import, and clear AcroForm fields. |
| **localization.md** | Localize SfPdfViewer static UI text to any supported language. |
| **directionality.md** | Enable RTL rendering using `Directionality` widget or RTL locale. |
| **accessibility.md** | Make SfPdfViewer accessible via `Semantics` and keyboard navigation. |
| **gesture-callback.md** | Handle tap gestures using the `onTap` callback. |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Missing package | Run `flutter pub add syncfusion_flutter_pdfviewer` |
| PDF not loading from network | Ensure internet permission is added in `AndroidManifest.xml` and `Info.plist` |
| PDF not loading from assets | Declare the asset path in `pubspec.yaml` under `flutter: assets:` |

---

## Resources

- [Syncfusion Flutter PdfViewer Docs](https://help.syncfusion.com/flutter/pdf-viewer/overview)
- [API Reference](https://pub.dev/documentation/syncfusion_flutter_pdfviewer/latest/)
- [pub.dev Package](https://pub.dev/packages/syncfusion_flutter_pdfviewer)

---
