# UI Settings

This guide demonstrates localization, right-to-left layout configuration, and liquid glass effect implementation.

## Localization

Translate PDF Viewer UI strings. Default culture is `en-US`.

### Setup (App.xaml.cs)

```csharp
using System.Globalization;
using System.Resources;
using Syncfusion.Maui.PdfViewer;

public partial class App : Application
{
    public App()
    {
        InitializeComponent();
        CultureInfo.CurrentUICulture = new CultureInfo("fr-FR");

        // Single control
        SfPdfViewerResources.ResourceManager = new ResourceManager(
            "PdfViewerLocalization.Resources.SfPdfViewer",
            Application.Current.GetType().Assembly);

        // Multiple Syncfusion controls  use unified resource file
        // Syncfusion.Maui.Core.Localization.LocalizationResourceAccessor.ResourceManager =
        //     new ResourceManager("Localization.Resources.SyncfusionControls",
        //         Application.Current.GetType().Assembly);

        MainPage = new AppShell();
    }
}
```

### Create Resource File

1. Add `SfPdfViewer.<culture>.resx` (e.g. `SfPdfViewer.fr.resx`) to `Resources/`
2. Set **Build Action**  **Embedded Resource**
3. Add key-value pairs (sample keys below)

| Key | Default Value |
|-----|---------------|
| Add Signature | Add Signature |
| AddBookmark | Add bookmark |
| AddFreeTextToastMessage | Tap on the page to add the free text annotation |
| AddHighlightToastMessage | Drag over a text to highlight it |
| AddReply | Add Reply |
| AddSignature | Add signature |
| AddSignatureToastMessage | Tap to add the signature |
| AddSquigglyToastMessage | Drag over a text to add a squiggly underline |
| AddStampToastMessage | Tap to add the stamp |
| AddStickyNoteToastMessage | Tap to add a sticky note |
| AddStrikeoutToastMessage | Drag over a text to strike it through |
| AddUnderlineToastMessage | Drag over a text to underline it |
| AddYourComment | Add comment |
| Annotations | Annotations |
| Apply | Apply |
| ApplyRedactionsConfirmation | You are about to permanently remove all content that has been marked for redaction. Once the document is saved, this operation cannot be undone. Are you sure you want to continue? |
| Arrow | Arrow |
| Back | Back |
| Bookmarks | Bookmarks |
| Border | Border |
| Cancel | Cancel |
| CanOpenWebPage | Do you want to open |
| Circle | Circle |
| Clear | Clear |
| Close | CLOSE |
| Cloud | Cloud |
| Color | Color |
| ColorPicker | Color picker |
| Comment | Comment |
| Comments | Comments |
| ContinuousPage | Continuous page |
| Copy | Copy |
| Create | Create |
| CreateSignature | Create Signature |
| CreateStamps | Create Stamps |
| CurrentPage | Current page |
| CustomStamps | Custom Stamps |
| CustomText | Custom text |
| Delete | Delete |
| DocumentLoadFailed | Failed to load the PDF document. |
| Drag and drop an image here | Drag and drop an image here |
| DragAndDropImage | Drag and drop an image here. |
| Draw | Draw |
| Draw your signature | Draw your signature |
| DrawArrowToastMessage | Drag to draw an arrow |
| DrawCircleToastMessage | Drag to draw a circle |
| DrawCloudToastMessage | Tap to begin drawing a cloud |
| DrawInkToastMessage | Drag to draw an ink |
| DrawLineToastMessage | Drag to draw a line |
| DrawPolygonToastMessage | Tap to begin drawing a polygon |
| DrawPolylineToastMessage | Tap to begin drawing a polyline |
| DrawSquareToastMessage | Drag to draw a square |
| Edit | Edit |
| EditYourComment | Edit comment |
| Enter | Enter |
| EnterPassword | Enter Password |
| EraseInkToastMessage | Drag over an ink to erase it |
| Error | Error |
| EvenPagesOnly | Even pages only |
| Fill | Fill |
| FillColor | Fill color |
| FillOpacity | Fill opacity |
| FitToPage | Fit to Page |
| FitToWidth | Fit to Width |
| Font | Font |
| FontColor | Font color |
| FontSize | Font size |
| FreeText | Free text |
| FreeTextEditorPlaceHolder | Text… |
| GoToPage | Go to Page |
| GuestUser | Guest User |
| Help | Help |
| Highlight | Highlight |
| Ink | Ink |
| InkEraser | Ink eraser |
| Insert | Insert |
| InvalidPageNumber | Invalid page number |
| InvalidPasswordError | Can't open an encrypted document. The password is invalid. |
| Key | Key |
| Line | Line |
| MarkForRedaction | Mark for Redaction |
| MarkPageRange | Mark page range |
| MatchCase | Match Case |
| MoreItems | More items |
| NewParagraph | New Paragraph |
| NextPage | Next page |
| NoBookmark | No Bookmark |
| NoBookmarks | No Bookmarks |
| NoColor | No Color |
| NoComments | No Comments available |
| NoMatchesWereFoundToastMessage | No matches were found. |
| NoMoreMatchesWereFoundToastMessage | No more matches were found |
| NoOutline | No outline |
| Note | Note |
| OddPagesOnly | Odd pages only |
| of | of |
| Ok | OK |
| Opacity | Opacity |
| Open | OPEN |
| OpenWebPage | Open Web Page |
| Outline | Outline |
| OutlineColor | Outline color |
| Page | Page |
| PageByPage | Page by page |
| PageCount | Page count |
| PageLayoutMode | Page layout mode |
| PageNumberEntry | Page number entry |
| PageNumberHint | Enter page number here |
| PageRange | Page range |
| Paragraph | Paragraph |
| PasswordErrorHint | Check your password |
| Polygon | Polygon |
| Polyline | Polyline |
| PreviousPage | Previous page |
| Print | Print |
| Properties | Properties |
| RedactArea | Redact area |
| RedactedAreaFillColor | Redacted area fill color |
| RedactionMarkAppearance | Redaction mark appearance |
| RedactionProperties | Redaction properties |
| RedactPages | Redact pages |
| RedactText | Redact text |
| Redo | Redo |
| Rename | Rename |
| RepeatOverlayText | Repeat overlay text |
| Replies | Replies |
| RequestPassword | This PDF file is protected. Please enter the password to open it. |
| Save | Save |
| SaveSignature | Save Signature |
| Search | Search |
| SearchPlaceholder | Find in the document |
| Shapes | Shapes |
| Signature | Signature |
| SpecificPage | Specific page |
| Square | Square |
| Squiggly | Squiggly |
| Stamps | Stamps |
| StandardStamps | Standard Stamps |
| StickyNote | Sticky note |
| StickyNoteEditorPlaceholder | Write Your Note... |
| StickyNoteIcons | Sticky note icons |
| Strikeout | Strikeout |
| Stroke | Stroke |
| Text | Text |
| TextColor | Text color |
| TextFillColor | Text fill color |
| TextMarkups | Text markups |
| Thickness | Thickness |
| Type | Type |
| Type your signature | Type your signature |
| TypeSignaturePlaceHolder | Type your signature |
| Underline | Underline |
| Undo | Undo |
| Upload | Upload |
| Upload an image | Upload an image |
| UploadImage | Upload an image |
| UseOverlayText | Use overlay text |
| XFAFormNotSupportedMessage | This PDF cannot be loaded because it contains an XFA form. |
| ZoomMode | Zoom mode |

> For the full key list refer to the [Syncfusion Localization docs](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/maui/localization).

---

## Right-to-Left Layout

```csharp
pdfViewer.FlowDirection = FlowDirection.RightToLeft;
```
XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer" FlowDirection="RightToLeft"/>
```
> All built-in controls within the viewer flow right-to-left automatically.

---

## Liquid Glass Effect

Requires iOS 26+ / macOS 26+ / .NET 10+.

XAML:
```xml
<Grid>
    <Grid.Background>
        <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
            <GradientStop Color="#0F4C75" Offset="0.0"/>
            <GradientStop Color="#3282B8" Offset="0.5"/>
            <GradientStop Color="#1B262C" Offset="1.0"/>
        </LinearGradientBrush>
    </Grid.Background>

    <core:SfGlassEffectView EffectType="Regular" CornerRadius="20">
        <syncfusion:SfPdfViewer x:Name="pdfViewer"
            Background="Transparent"
            EnableLiquidGlassEffect="True"/>
    </core:SfGlassEffectView>
</Grid>
```
