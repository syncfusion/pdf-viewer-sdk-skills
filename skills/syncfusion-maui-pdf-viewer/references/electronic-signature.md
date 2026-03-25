# Electronic Signature in .NET MAUI PDF Viewer

This guide demonstrates how to add and manage electronic signatures in PDF documents, including handwritten, text-based, and image-based signatures.

## Signature Types

1. **Handwritten Signature** - User draws a signature
2. **Text Signature** - Text-based signature
3. **Image Signature** - Image-based signature

## Add Signature via UI

Enable signature mode to allow users to add signatures through the signature dialog.

**C#:**
```csharp
// Enable signature mode - opens signature dialog
void EnableSignatureMode()
{
    PdfViewer.AnnotationMode = AnnotationMode.Signature;
}

// Disable signature mode after adding signature
void DisableSignatureMode()
{
    PdfViewer.AnnotationMode = AnnotationMode.None;
}
```

## Add Handwritten Signature Programmatically

Create and add handwritten signatures using ink annotations.

**C#:**
```csharp
int pageNumber = 1;

// Provide the points collection to draw a stroke (single stroke example)
List<List<float>> pointsCollection = new List<List<float>>()
{
    new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 }
};

// Create an ink annotation
InkAnnotation annotation = new InkAnnotation(pointsCollection, pageNumber);

// Set IsSignature as true to mark as signature
annotation.IsSignature = true;

// Add the ink annotation to the PDF page as a signature
PdfViewer.AddAnnotation(annotation);
```

## Add Image Signature Programmatically

Create and add image-based signatures using stamp annotations.

**C#:**
```csharp
int pageNumber = 1;

// Define the position and size for the stamp
RectF bounds = new RectF(50, 50, 200, 100);

// Create an image stream from the image resource
Stream imageStream = this.GetType().Assembly.GetManifestResourceStream("Annotations.Assets.Logo.png");

// Create a custom stamp annotation using the image stream
StampAnnotation customStamp = new StampAnnotation(imageStream, pageNumber, bounds);

// Set IsSignature as true to mark as signature
customStamp.IsSignature = true;

// Add the stamp annotation to the PDF page as a signature
PdfViewer.AddAnnotation(customStamp);
```

## Handle Signature Modal View Events

Handle events when the signature dialog appears or disappears.

**C#:**
```csharp
// Subscribe to events
pdfViewer.SignatureModalViewAppearing += PdfViewer_SignatureModalViewAppearing;
pdfViewer.SignatureModalViewDisappearing += PdfViewer_SignatureModalViewDisappearing;

// Event triggered when signature modal view opens
private void PdfViewer_SignatureModalViewAppearing(object? sender, FormFieldModalViewAppearingEventArgs e)
{
    // Hide unwanted UI elements like toolbars
}

// Event triggered when signature modal view closes
private void PdfViewer_SignatureModalViewDisappearing(object? sender, EventArgs e)
{
    // Show the UI elements that were hidden
}
```

## Suppress Modal View and Use Custom UI

Replace the built-in signature dialog with a custom UI.

**C#:**
```csharp
Stream signatureImageStream;

pdfViewer.SignatureModalViewAppearing += PdfViewer_SignatureModalViewAppearing;
pdfViewer.Tapped += PdfViewer_Tapped;

// Suppress the built-in signature modal
private void PdfViewer_SignatureModalViewAppearing(object? sender, FormFieldModalViewAppearingEventArgs e)
{
    e.Cancel = true;  // Prevent default signature dialog
    // Show your custom signature UI dialog
    ShowCustomDialog();
}

// When user completes drawing signature in custom dialog
private void CustomDialogOkButton_Clicked(object sender, EventArgs e)
{
    // Get the signature as an image stream
    signatureImageStream = GetSignatureImageStream();
}

// Add signature when user taps on PDF
private void PdfViewer_Tapped(object sender, GestureEventArgs e)
{
    PointF position = e.PagePosition;
    int pageNumber = e.PageNumber;
    
    // Create and add stamp annotation as signature
    StampAnnotation stamp = new StampAnnotation(signatureImageStream, pageNumber, 
                                                 new RectF(position.X, position.Y, 200, 200));
    pdfViewer.AddAnnotation(stamp);
}
```

## Customize Handwritten Signature Appearance

Use the `SignatureCreated` event to customize signature properties after creation.

**C#:**
```csharp
// Subscribe to SignatureCreated event
pdfViewer.SignatureCreated += PdfViewer_SignatureCreated;

// Event handler triggered when a signature is created
private void PdfViewer_SignatureCreated(object? sender, SignatureCreatedEventArgs e)
{
    // Check if the signature is a handwritten ink-based signature
    if (e.Signature is InkAnnotation handWrittenSignature)
    {
        // Customize the appearance of the handwritten signature
        handWrittenSignature.BorderWidth = 6;           // Set stroke thickness
        handWrittenSignature.Color = Colors.Yellow;     // Set stroke color
        handWrittenSignature.Opacity = 0.75f;           // Set transparency level
    }
}
```

## Reference

- [Electronic Signature](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/maui/signature)
