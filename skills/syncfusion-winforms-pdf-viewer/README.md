# Syncfusion WinForms PdfViewer skill

## Overview
Create WinForms applications featuring the Syncfusion WinForms PDF Viewer, customized to meet specific user requirements.

See **[SKILL.md](SKILL.md)** for the full intent-routing guide and rules.

---

## Key Capabilities

- **High-fidelity PDF rendering & navigation:** pdf viewing, bookmark navigation, hyperlink navigation, interaction modes, printing and saving pdf files.
- **Text search & extraction:** text search and extract text from pdf.


## Getting Started

### How to Integrate Skills

**Step 1: Checkout and copy the required skills**

Clone or download the PDF-Viewer-SDK-Skills repository and copy the **winforms-pdf-viewer** skill from the `skills/` directory.

**Step 2: Install the skill**

Place the copied skill folders in your workspace following this structure:

```
your-workspace/
├── .github/skills/          # or .claude/skills/ or .codestudio/skills/
│   └── winforms-pdf-viewer/
│       └── SKILL.md
├── your-project-files...
└── Program.cs
```

**Step 3: Verify and manage your skills**

Type `/skills` in the GitHub Copilot or Code Studio chat to quickly access the Configure Skills menu and manage your installed skills.

**Step 4: Use skills in VS Code**

There are two ways to use skills:

1. **Slash commands** - Type `/` in the GitHub Copilot chat to see available skills. 

2. **Automatic loading** - Simply describe your task naturally, and your AI Agent automatically loads the relevant skill:
   ```
   Create a WinForms window with WinForms PdfViewer that loads pdf document
   ```

When the winforms-pdf-viewer skill is loaded, the AI Agent provides focused C# snippets and commands for WinForms PdfViewer.

### Prerequisites

- **Visual Studio** 2019 or later
- **.NET** Framework 4.6+ or .NET 6+
- **Syncfusion License** — register your key in `Program.cs`, or set the `SYNCFUSION_LICENSE_KEY` environment variable.  
  Free license: [Syncfusion Community License](https://www.syncfusion.com/products/communitylicense)


### NuGet Packages

```bash
dotnet add package Syncfusion.PdfViewer.Windows
```

---

## Example Prompts

#### Code Generation
*Use these when you want C# code for your existing WinForms project.*

- "Create a C# WinForms Form that adds a Syncfusion PdfViewer, loads a PDF from disk, and shows zoom/print toolbar buttons."
- "Add code to extract all text from page 2 and save it to a .txt file."
- "Show how to save the currently loaded PDF to a new file programmatically"
---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| License warning at startup | Call `SyncfusionLicenseProvider.RegisterLicense()` in `Program.cs` before any control is created |
| Missing NuGet package | `dotnet add package Syncfusion.PdfViewer.Windows` |
---

## Resources

- [Syncfusion WinForms PdfViewer Docs](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/winforms/overview)
- [API Reference](https://help.syncfusion.com/cr/document-processing/Syncfusion.Windows.PdfViewer.html)

---

## License

Syncfusion WinForms PdfViewer requires a commercial license for production use. A [free community license](https://www.syncfusion.com/products/communitylicense) is available for qualifying organizations.
