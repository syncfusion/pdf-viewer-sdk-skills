## Stamp Annotations

Stamp annotations add predefined or custom image stamps to PDF documents for approval workflows, status marking, and branding.

### Stamp Categories

**1. Dynamic Stamps**
- Approved
- Confidential
- Draft
- Final
- For Comment
- For Public Release
- Not Approved
- Not For Public Release
- Void

**2. Sign Here Stamps**
- Accepted
- Initial Here
- Sign Here
- Witness

**3. Standard Business Stamps**
- Approved
- Completed
- Confidential
- Draft
- Final
- For Comment
- For Public Release
- Information Only
- Not Approved
- Not For Public Release
- Void

**4. Custom Image Stamps**
- Upload JPG/JPEG images (logos, signatures, branded elements)

### Adding Stamp Annotations

```javascript
// Add dynamic stamp
function addDynamicStamp() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Stamp", {
        offset: { x: 200, y: 140 },
        pageNumber: 1
    }, 'Approved');
}

// Add sign here stamp
function addSignStamp() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Stamp", {
        offset: { x: 200, y: 240 },
        pageNumber: 1
    }, undefined, 'Witness');
}

// Add custom image stamp
function addCustomStamp() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation('Stamp', {
        offset: { x: 100, y: 440 },
        width: 46,
        height: 100,
        pageNumber: 1,
        customStamps: [{
            customStampName: "Logo",
            customStampImageSource: "data:image/jpeg;base64,..." // Base64 image data
        }]
    });
}
```