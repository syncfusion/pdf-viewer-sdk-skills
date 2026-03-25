# Working with Themes

PDF Viewer supports various built-in themes to customize the default appearance of the `PdfViewerControl` using its `ThemeName` property.

> **Note:** To use the Office2019Colorful or HighContrastBlack themes, install the corresponding NuGet packages:
Syncfusion.Office2019Theme.WinForms and Syncfusion.HighContrastTheme.WinForms. Other Office2016 themes do not require additional assemblies.
---

## Apply Office 2016 Theme

Supported themes: `Office2016Colorful`, `Office2016Black`, `Office2016DarkGray`, `Office2016White`.

```csharp
pdfViewerControl1.ThemeName = "Office2016DarkGray";
```

---

## Apply Office 2019 Theme

```csharp
// In Program.cs Main() method — load the assembly before Application.Run()
SkinManager.LoadAssembly(typeof(Syncfusion.WinForms.Themes.Office2019Theme).Assembly);
```

```csharp
pdfViewerControl1.ThemeName = "Office2019Colorful";
```

---

## Apply High Contrast Theme

```csharp
// In Program.cs Main() method — load the assembly before Application.Run()
SkinManager.LoadAssembly(typeof(Syncfusion.WinForms.Themes.HighContrastTheme).Assembly);
```

```csharp
pdfViewerControl1.ThemeName = "HighContrastBlack";
```

---

## Reset to Default Theme

```csharp
pdfViewerControl1.ThemeName = "Default";
```
