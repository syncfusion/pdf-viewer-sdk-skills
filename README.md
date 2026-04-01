# PDF-Viewer-SDK-Skills

[Syncfusion PDF Viewer](https://www.syncfusion.com/pdf-viewer-sdk) Skills are specialized instruction sets that teach AI assistants how to generate code for PDF viewing applications across multiple platforms. These skills follow the [Agent Skills open standard](https://agentskills.io/) and are designed to work seamlessly across AI agents like GitHub Copilot and Code Studio.

## About This Repository

This repository contains **AI-ready skills** that empower AI agents to generate production-ready code for embedding Syncfusion PDF Viewer components into your applications. Each skill provides platform-specific code generation capabilities, enabling your AI to create code snippets for viewing, annotating, searching, and managing PDF documents across web, mobile, and desktop platforms.

## Included Platform-Specific PDF Viewer Skills

### Web Frameworks
- **Blazor PDF Viewer** - Interactive PDF viewing in Blazor Server and WebAssembly with full annotation support, form filling, text search, redaction, custom toolbar configuration, and event handling
- **React PDF Viewer** - Modern PDF viewer for React applications with TypeScript support, comprehensive annotation tools, form designer, text search/selection, bookmark navigation, thumbnail view, and print/download capabilities
- **ASP.NET Core PDF Viewer** - PDF viewing for ASP.NET Core applications with local PDF hosting, toolbar customization, text search, annotations, form filling, and event hooks.
- **ASP.NET MVC PDF Viewer** - PDF viewing for ASP.NET MVC applications with local PDF hosting, toolbar customization, text search, annotations, form filling, and event hooks.
- **Angular PDF Viewer** – Enterprise-grade PDF viewer for Angular applications with toolbar customization, annotations, form fields, text search/selection, bookmarks, thumbnails, redaction, page organization, print/download, and full API access
- **Vue PDF Viewer** – PDF viewer for Vue applications with annotations, form filling and form designer, text search/selection, toolbar customization, page organizer, magnification, navigations, redaction.
- **JavaScript PDF Viewer** – PDF viewer for JavaScript (ES6) applications with annotations, form filling and form designer, text search/selection, toolbar customization, page organizer, magnification, navigations, redaction.
- **Blazor Smart PDF Viewer** - Intelligent PDF viewer powered by AI with document summarizer, smart form filling, smart redaction with Blazor PDF Viewer.

### Mobile & Cross-Platform
- **Flutter PDF Viewer** - Native PDF viewing for iOS and Android with text search, annotations (text markup, sticky notes), form filling, signature pad integration, bookmark navigation, password-protected PDF support, and localization
- **.NET MAUI PDF Viewer** - Cross-platform PDF viewer for Android, iOS, Windows, and macOS with ink annotations, shapes, stamps, text markups, form validation, electronic signatures, redaction, and custom toolbar support

### Desktop Frameworks
- **UWP PDF Viewer** - Native Universal Windows Platform PDF viewer (`SfPdfViewerControl`) with full annotation support (text markup, shapes, ink, free text, stamp), form field interaction, text search/selection, bookmark/hyperlink navigation, printing, custom toolbar layouts for desktop and mobile, localization, page image export, and PDFium renderer support
- **WPF PDF Viewer** - Feature-rich PDF viewer for Windows desktop applications with annotation tools, magnification, text selection, search, bookmark/hyperlink navigation, printing, theming, and localization support
- **Windows Forms PDF Viewer** - Traditional Windows Forms PDF viewer with essential operations including loading, saving, printing, text extraction, search, bookmark navigation, zoom controls, and theming

## Getting Started

### How to Integrate Skills

**Step 1: Checkout and copy the required skills**

Clone or download the PDF-Viewer-SDK-Skills repository and copy the platform-specific skills you need (e.g., `syncfusion-blazor-pdf-viewer`, `syncfusion-react-pdf-viewer`, `syncfusion-maui-pdf-viewer`) from the `skills/` directory.

**Step 2: Install the skills**

Place the copied skill folders in your workspace following this structure:

```
your-workspace/
├── .github/skills/                          # or .claude/skills/ or .codestudio/skills/
│   ├── syncfusion-blazor-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-react-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-aspnetcore-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-aspnetmvc-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-angular-pdf-viewer/
│   │   └── SKILL.md
|   ├── syncfusion-vue-pdf-viewer/
│   │   └── SKILL.md
|   ├── syncfusion-javascript-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-flutter-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-maui-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-uwp-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-wpf-pdf-viewer/
│   │   └── SKILL.md
│   ├── syncfusion-winforms-pdf-viewer/
│   |   └── SKILL.md
│   └── syncfusion-blazor-smart-pdf-viewer/
│       └── SKILL.md
├── your-project-files...
└── App.tsx / Program.cs / MainPage.xaml / etc.
```

Each skill directory must contain a `SKILL.md` file that defines the skill's behavior and capabilities.

**Step 3: Verify and manage your skills**

Type `/skills` in the GitHub Copilot or Code Studio chat to quickly access the Configure Skills menu and manage your installed skills.

**Step 4: Use skills**

There are two ways to use skills:

1. **Automatic loading** - Simply describe your task naturally, and your AI Agent automatically loads the relevant skill:
   ```
   Add a PDF viewer to my Blazor app with toolbar customization
   Show me how to implement text search in React PDF viewer
   Create a MAUI PDF viewer with annotation support
   ```

2. **Slash commands** - Type `/` in the GitHub Copilot chat to mention available skills. For example:
   ```
   /syncfusion-blazor-pdf-viewer Add PDF viewer with custom toolbar
   /syncfusion-react-pdf-viewer Implement form filling features
   /syncfusion-maui-pdf-viewer Add signature support to PDF viewer
   /syncfusion-uwp-pdf-viewer Load a PDF from StorageFile with annotation support
   ```

When a skill is loaded, the AI Agent gains specialized knowledge of the platform-specific PDF Viewer component and can help you generate accurate, production-ready code.

### Prerequisites

**For .NET Platforms (Blazor, MAUI, WPF, WinForms):**
```bash
# .NET SDK 8+
dotnet --version
```

**For React:**
```bash
# Node.js 14.0.0+
node --version

# NPM or Yarn
npm --version
```

**For Flutter:**
```bash
# Flutter 3.x+
flutter --version
```

### Syncfusion License

Place your license key in `SyncfusionLicense.txt` at the workspace root, or set the environment variable:

```bash
# Windows
set SYNCFUSION_LICENSE_KEY=your_key_here

# macOS/Linux
export SYNCFUSION_LICENSE_KEY=your_key_here
```

Get a free license: [Syncfusion Community License](https://www.syncfusion.com/products/communitylicense)

### NuGet Packages & Dependencies

**Blazor PDF Viewer:**
```bash
dotnet add package Syncfusion.Blazor.SfPdfViewer
```

**React PDF Viewer:**
```bash
npm install @syncfusion/ej2-react-pdfviewer --save
```

**ASP.NET Core PDF Viewer:**
```bash
dotnet add package Syncfusion.EJ2.PdfViewer.AspNet.Core
```

**ASP.NET MVC PDF Viewer:**
```bash
dotnet add package Syncfusion.EJ2.MVC5
```

**Angular PDF Viewer:**
```bash
npm install @syncfusion/ej2-angular-pdfviewer --save
```

**Vue PDF Viewer:**
```bash
npm install @syncfusion/ej2-vue-pdfviewer --save
```

**JavaScript (ES6) PDF Viewer:**
```bash
npm install
```

**Flutter PDF Viewer:**
```yaml
# Add to pubspec.yaml
dependencies:
  syncfusion_flutter_pdfviewer: ^latest_version
```

**.NET MAUI PDF Viewer:**
```bash
dotnet add package Syncfusion.Maui.PdfViewer
```

**WPF PDF Viewer:**
```bash
dotnet add package Syncfusion.PdfViewer.WPF
```

**UWP PDF Viewer:**
```
Syncfusion.SfPdfViewer.UWP (via NuGet or manual assembly reference)
```

**WinForms PDF Viewer:**
```bash
dotnet add package Syncfusion.PdfViewer.Windows
```

**Blazor Smart PDF Viewer:**
```bash
dotnet add package Syncfusion.Blazor.SfSmartPdfViewer
```

## How it Works

### Generate Code for Your Project *(Mode 1 - default)*

All PDF Viewer skills generate **production-ready code** that you integrate directly into your application. The AI assistant produces platform-specific code snippets (C#, TypeScript/JSX, Dart, XAML) based on your requirements and inserts them into your project files.

This mode is ideal when you want to:
- Learn how to implement specific PDF viewer features
- Integrate PDF viewing capabilities into your existing application
- Customize the PDF viewer for your specific use case
- Understand the API and component structure

**Trigger keywords:** `"code"`, `"snippet"`, `"how to"`, `"show me"`, `"sample"`, `"example"`, `"integrate"`, `"add"`, `"implement"`

## Example Prompts

### Blazor PDF Viewer

```
# Basic Setup
Show me how to add a Blazor PDF viewer to my Home.razor page
Add a basic PDF viewer component with document loading

# Features
How do I implement text search with custom highlight colors in Blazor PDF viewer?
Add annotation toolbar with circle and highlight tools to the PDF viewer
Show me how to implement form filling and validation in the PDF viewer
Create a custom toolbar with only download and print buttons
```

### React PDF Viewer

```
# Basic Setup
Add a React PDF viewer component to App.tsx
Show me how to load a PDF from URL in React

# Features
Implement bookmark navigation in React PDF viewer
Add form designer functionality with text and checkbox fields
Show me how to implement text selection and copy in React PDF viewer
Create custom context menu for the PDF viewer
```

### ASP.NET Core PDF Viewer

```
# Basic Setup
Add a PDF viewer to my ASP.NET Core application
Show me how to add a PDF Viewer component to Index.cshtml

# Features
How do I implement text search with custom highlight colors in ASP.NET Core PDF viewer?
Create a custom toolbar with only navigation and magnification options
Show me how to implement form filling and validation in the PDF viewer
Disable bookmark navigation and thumbnails in the PDF viewer
```

### ASP.NET MVC PDF Viewer

```
# Basic Setup
Add a PDF viewer to my ASP.NET MVC application
Add a basic PDF Viewer component with document loading event to Index.cshtml

# Features
Show me how to add annotations programmatically in MVC PDF Viewer.
Create a customized search functionalities with MVC PDF Viewer APIs.
Disable the annotation and form designer modules from MVC PDF Viewer.
How to add open and download options only in toolbar for PDF Viewer.
```

### Angular PDF Viewer

```
# Basic Setup
Add Angular PDF viewer component to app.ts
Provide code to set up the Syncfusion Angular PDF Viewer

# Features
How do I load a PDF from a remote URL using documentPath ?
Provide code to download/save the PDF programmatically.
How do I trigger print programmatically and disable the toolbar print button ?
Provide code to add a highlight annotation programmatically
```

### Vue PDF Viewer

```
# Basic Setup
Add Vue PDF viewer component to my vue sample
Provide code to set up the Syncfusion Vue PDF Viewer in the sample

# Features
How to add the print option externally in the Vuew PDF Viewer.
Show me how to add form fields programmatically in PDF Viewer.
Provide code for annotation add and delete events triggered in PDF Viewer.
How to show shape and calibrate annotations only in annotation toolbar in PDF Viewer.
```

### JavaScript (ES6) PDF Viewer

```
# Basic Setup
Add Javscript PDF viewer component to my Javascript sample
Provide code to set up the Syncfusion JavaScript PDF Viewer in the sample

# Features
Show me how to add islock as true for all the annotation in Javascript PDF Viewer.
Provide code for add free text annotation programmtically in PDF Viewer.
How to add customized option for zoom in and zoom out in toolbar.
Implement the document loaded event with document name in PDF Viewer.
```

### Flutter PDF Viewer

```
# Basic Setup
Add SfPdfViewer widget to my Flutter app
Show me how to load a PDF from assets in Flutter

# Features
Implement text search with next/previous navigation in Flutter PDF viewer
Add signature pad for form field signing
Show me how to handle password-protected PDFs in Flutter
Implement text markup annotations (highlight, underline, strikethrough)
```

### .NET MAUI PDF Viewer

```
# Basic Setup
Add SfPdfViewer to MainPage.xaml
Show me how to load PDF from file picker in MAUI

# Features
Implement ink annotation with custom colors in MAUI PDF viewer
Add electronic signature functionality to the PDF viewer
Show me how to implement form field validation and export
Create custom toolbar for mobile and desktop platforms
```

### WPF PDF Viewer

```
# Basic Setup
Add PdfViewerControl to MainWindow.xaml
Show me how to load a PDF document in WPF

# Features
Implement magnification and zoom controls in WPF PDF viewer
Add text selection and extraction functionality
Show me how to implement bookmark and hyperlink navigation
Create custom annotation tools (circle, arrow, highlight)
```

### UWP PDF Viewer

```
# Basic Setup
Add SfPdfViewerControl to UWP MainPage
Show me how to load a PDF from a StorageFile in UWP

# Features
Implement text search with next/previous navigation in UWP PDF viewer
Add annotation toolbar with highlight and ink tools
Create a custom toolbar with print and download commands
How do I export PDF pages as images in UWP?
Implement bookmark navigation in UWP PDF viewer
```

### WinForms PDF Viewer

```
# Basic Setup
Add PdfViewerControl to Form1
Show me how to load and display a PDF in WinForms

# Features
Implement text search with highlight in WinForms PDF viewer
Add print functionality with custom page settings
Show me how to extract text with line and word bounds
Switch between selection and pan interaction modes
```

### Blazor Smart PDF Viewer

```
# Basic Setup
Add Smart PDF Viewer Component to my Home.razor page
Provide code to set up the Syncfusion Smart PDF Viewer in the sample

# Features
How to enable the smart redaction option in smart PDF Viewer.
Provide code to redact the name in the document in smart PDF Viewer.
Implement the code for summarizer option in smart PDF Viewer.
Show to how to enable the smart fill option in smart PDF Viewer.
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| License Watermark | Add key to `SyncfusionLicense.txt` or use env var `SYNCFUSION_LICENSE_KEY` |
| Missing NuGet package | Run the appropriate package installation command for your platform |
| Component not rendering | Ensure package is installed and namespace is correctly imported |
| PDF not loading | Check file path, URL accessibility, or stream validity |
| CORS error (web) | Configure server to allow cross-origin requests for PDF documents |
| Feature not working | Verify the feature is supported on your target platform |

## Resources

### Documentation
- [Blazor PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/blazor/overview)
- [React PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/react/overview)
- [ASP.NET Core PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/asp-net-core/overview)
- [ASP.NET MVC PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/asp-net-mvc/overview)
- [Angular PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/angular/overview)
- [Vue PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/vue/overview)
- [JavaScript (ES6) PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/javascript-es6/overview)
- [Flutter PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/flutter/overview)
- [.NET MAUI PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/maui/overview)
- [WPF PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/wpf/overview)
- [UWP PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/uwp/overview)
- [WinForms PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/winforms/overview)
- [Blazor Smart PDF Viewer Documentation](https://help.syncfusion.com/document-processing/pdf/smart-pdf-viewer/blazor/overview)

## License

Syncfusion PDF Viewer components require a [commercial license](https://www.syncfusion.com/sales/products) for production use. A [free Community License](https://www.syncfusion.com/products/communitylicense) is also available for individual developers and small businesses.

