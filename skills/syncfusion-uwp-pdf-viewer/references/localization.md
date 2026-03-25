# Localization in UWP PDF Viewer (SfPdfViewerControl)

Localization lets you translate the PDF Viewer's context menu and UI strings to any language by providing `.resw` resource files.

---

## Step 1: Set Default Language in App Manifest

1. Open `Package.appxmanifest` in the manifest designer.
2. On the **Application** tab, set the **Default language** (e.g., `en-US`, `fr-FR`).
3. Save the manifest.

---

## Step 2: Add Resource Files

Create this folder structure in your project:

```
Resources/
├── en-US/
│   ├── Syncfusion.SfPdfViewerControl.UWP.Resources.resw
│   ├── Syncfusion.SfColorPickers.WinRT.Resources.resw
│   └── Localization.Resources.resw
└── fr-FR/
    ├── Syncfusion.SfPdfViewerControl.UWP.Resources.resw
    ├── Syncfusion.SfColorPickers.WinRT.Resources.resw
    └── Localization.Resources.resw
```

- Add the resource key names and their translated string values in the Resource Designer for each `.resw` file.
- The `en-US` files serve as the fallback/default.

---

## Supported Resource File Names

| File | Purpose |
|---|---|
| `Syncfusion.SfPdfViewerControl.UWP.Resources.resw` | PDF Viewer context menu and UI strings |
| `Syncfusion.SfColorPickers.WinRT.Resources.resw` | Color picker strings |
| `Localization.Resources.resw` | App-level localization strings |

---

## Resource Keys and Translated Values

The following table lists the supported resource key names and their French (`fr-FR`) translated values for `Syncfusion.SfPdfViewerControl.UWP.Resources.resw`:

| Name | Value (fr-FR) |
|------|--------------|
| Color | Couleur |
| Delete | effacer |
| Edit | Éditer |
| FillColor | Remplir Couleur |
| Opacity | opacité |
| Open Pop-Up Note | ouvrir la note contextuelle |
| Properties | Propriétés |
| Text Size | taille du texte |
| Thickness | épaisseur |
| Type your text | Tapez votre texte |

> These keys must be added to the `.resw` resource file under the matching locale folder (e.g., `Resources/fr-FR/Syncfusion.SfPdfViewerControl.UWP.Resources.resw`).

---

## Result

After adding the resource files with the correct keys and translations, the PDF Viewer's context menus and UI elements will display in the configured language automatically at runtime.
