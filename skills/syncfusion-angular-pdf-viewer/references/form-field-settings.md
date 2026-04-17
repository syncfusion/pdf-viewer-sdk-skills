# FormField Settings

Brief: Configure default properties for form fields in Angular PDF Viewer. These settings define appearance, behavior, and validation when adding new form fields programmatically or through the Form Designer UI.

## Table of Contents

- [Form Field Component Properties](#form-field-component-properties)
- [Common Properties](#common-properties)
- [TextField Settings](#textfield-settings)
- [Password Field Settings](#password-field-settings)
- [CheckBox Field Settings](#checkbox-field-settings)
- [RadioButton Field Settings](#radiobutton-field-settings)
- [Dropdown Field Settings](#dropdown-field-settings)
- [ListBox Field Settings](#listbox-field-settings)
- [Signature Field Settings](#signature-field-settings)
- [Initial Field Settings](#initial-field-settings)
- [Property Naming Convention](#property-naming-convention-critical---case-sensitive)
- [FormField API Properties](#formfield-api-properties)
- [Usage Examples](#usage-examples)
- [Usage Notes](#usage-notes)

## Form Field Component Properties

These properties are available directly on the `PdfViewerComponent` to control form field-related functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **designerMode** | Enable or disable the interaction of form fields in the PDF Viewer. | boolean | `false` |
| **formFieldCollections** | Get the collection of form fields in the PDF document. | `FormFieldCollection[]` | `null` |
| **enableFormFieldsValidation** | Enable validation when downloading or submitting forms with required fields. | `boolean` | `false` |
| **enableFormDesigner** | Show or hide the Form Designer option in the main toolbar. | `boolean` | `true` |
| **hideSaveSignature** | Hide or show the save button in signature dialog. | `boolean` | `false` |
| **initialDialogSettings** | Configure initial dialog settings for PDF Viewer. | `InitialDialogSettings` | `null` |
| **isFormDesignerToolbarVisible** | Show or hide the form designer toolbar. | `boolean` | `true` |
| **isFormFieldDocument** | Get whether the document contains form fields. | `boolean` | `false` |
| **signatureFitMode** | Set how signatures fit in the signature field. | [`SignatureFitMode`](./annotation-settings.md#signaturefitmode) | `Default` |

## Common Properties

Properties shared across multiple form field types:

| **Property** | **Description** | **Type** | **Default** | **Applies To** |
|-----|-----|-----|-----|-----|
| **name** | Default field name | string | Varies | All |
| **value** | Default field value | string | '' | Text-based fields |
| **fontFamily** | Font family | string | Helvetica | Text-based fields |
| **fontSize** | Font size | number | 10 | Text-based fields |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | None | Text-based fields |
| **color** | Font color (hex format) | string | #000000 | Text-based fields |
| **backgroundColor** | Background color | string | #daeaf7ff | All |
| **borderColor** | Border color | string | #303030 | All |
| **thickness** | Border thickness (pixels) | number | 1 | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | TextAlignment | Left | Text-based fields |
| **isReadOnly** | Read-only state | boolean | false | All |
| **visibility** | Visibility (visible, hidden) | string | visible | All |
| **isRequired** | Required field | boolean | false | All |
| **isPrint** | Printable | boolean | true | All |
| **tooltip** | Tooltip text | string | Field type | All |
| **maxLength** | Maximum character length (0 = unlimited) | number | 0 | Text, Password |
| **isMultiline** | Allow multiline input | boolean | false | TextField |
| **isChecked** | Checked state | boolean | false | CheckBox |
| **isSelected** | Selected state | boolean | false | RadioButton |
| **options** | Dropdown/ListBox items | ItemModel[] | [] | Dropdown, ListBox |

## TextField Settings

Property: `textFieldSettings` | Default name: Textbox | Supports: All common text-based properties + `isMultiline`

```typescript
import { PdfViewerModule } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  template: `
    <ejs-pdfviewer
      [textFieldSettings]="textFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public textFieldSettings = {
    fontFamily: 'Arial',
    fontSize: 12,
    backgroundColor: '#FFFF00',
    maxLength: 100,
    isMultiline: false
  };
}
```

## Password Field Settings

Property: `passwordFieldSettings` | Default name: Password | Supports: All common text-based properties (text displays masked)

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [passwordFieldSettings]="passwordFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public passwordFieldSettings = {
    fontFamily: 'Courier',
    fontSize: 12,
    backgroundColor: '#FFE6E6',
    maxLength: 20,
    isRequired: true
  };
}
```

## CheckBox Field Settings

Property: `checkBoxFieldSettings` | Default name: CheckBox | Specific property: `isChecked`

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [checkBoxFieldSettings]="checkBoxFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public checkBoxFieldSettings = {
    isChecked: false,
    backgroundColor: '#FFFFFF',
    borderColor: '#000000',
    thickness: 1
  };
}
```

## RadioButton Field Settings

Property: `radioButtonFieldSettings` | Default name: RadioButton | Specific property: `isSelected`

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [radioButtonFieldSettings]="radioButtonFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public radioButtonFieldSettings = {
    isSelected: false,
    backgroundColor: '#FFFFFF',
    borderColor: '#0000FF',
    thickness: 1
  };
}
```

## Dropdown Field Settings

Property: `dropdownFieldSettings` | Default name: Dropdown | Supports: Text-based properties + `options`

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [dropdownFieldSettings]="dropdownFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public dropdownFieldSettings = {
    fontFamily: 'Arial',
    fontSize: 11,
    options: [
      { itemName: 'Option 1', itemValue: 'opt1' },
      { itemName: 'Option 2', itemValue: 'opt2' }
    ]
  };
}
```

## ListBox Field Settings

Property: `listBoxFieldSettings` | Default name: ListBox | Supports: Text-based properties + `options`

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [listBoxFieldSettings]="listBoxFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public listBoxFieldSettings = {
    fontFamily: 'Verdana',
    fontSize: 10,
    options: [
      { itemName: 'Item 1', itemValue: 'item1' },
      { itemName: 'Item 2', itemValue: 'item2' }
    ]
  };
}
```

## Signature Field Settings

Property: `signatureFieldSettings` | Default name: SignatureField | Specific properties: `signatureIndicatorSettings`

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [signatureFieldSettings]="signatureFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public signatureFieldSettings = {
    isRequired: true,
    thickness: 2,
    tooltip: 'Sign here'
  };
}
```

## Initial Field Settings

Property: `initialFieldSettings` | Default name: Initial | For user initials

```typescript
@Component({
  template: `
    <ejs-pdfviewer
      [initialFieldSettings]="initialFieldSettings">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  public initialFieldSettings = {
    thickness: 1,
    tooltip: 'Add your initials'
  };
}
```

## Property Naming Convention (CRITICAL - Case Sensitive)

### ⚠️ IMPORTANT: Form Fields Use CAPITALIZED Bounds Properties

**Form field bounds MUST use capitalized property names (NOT lowercase):**

### Correct Format ✅ - Form Fields
```typescript
bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
```

### Incorrect Formats ❌
```typescript
bounds: { x: 100, y: 100, width: 200, height: 30 }  // WRONG - lowercase (for annotations, not form fields)
bounds: { x: 100, y: 100, WIDTH: 200, HEIGHT: 30 }  // WRONG - Mixed case
```

**Why this matters:** TypeScript is case-sensitive. Using the wrong case will result in undefined properties and the bounds will not be applied correctly.

### Bounds Property Format for Form Fields
Always use these CAPITALIZED property names for the `bounds` object:
- `X` (not `x`) - X-coordinate of top-left corner
- `Y` (not `y`) - Y-coordinate of top-left corner
- `Width` (not `width`) - Width of rectangle
- `Height` (not `height`) - Height of rectangle

### Difference from Annotations
**CRITICAL DISTINCTION:** Form fields and annotations use DIFFERENT bounds formats:
- **Form Fields:** Use capitalized bounds `{ X: 100, Y: 100, Width: 200, Height: 30 }`
- **Annotations:** Use lowercase bounds `{ x: 100, y: 100, width: 200, height: 50 }`

Do NOT mix these formats. Using lowercase bounds with form fields or capitalized bounds with annotations will cause errors.

### Form Field Settings Properties Follow camelCase Convention
All other form field setting properties use camelCase (lowercase first letter, uppercase for subsequent words):
- `name` (not `Name`)
- `value` (not `Value`)
- `backgroundColor` (not `BackgroundColor`)
- `borderColor` (not `BorderColor`)
- `fontSize` (not `FontSize`)
- `fontFamily` (not `FontFamily`)
- `fontStyle` (not `FontStyle`)
- `isReadOnly` (not `IsReadOnly`)
- `isRequired` (not `IsRequired`)
- `isMultiline` (not `IsMultiline`)
- `maxLength` (not `MaxLength`)
- `pageNumber` (not `PageNumber`)

**Exception:** Only the `bounds` object itself uses capitalized property names (X, Y, Width, Height), while all other settings use camelCase.

---

## FormField API Properties

Access and modify existing form fields using `retrieveFormFields()`. These properties are available on individual field instances (not settings).

| **Property** | **Description** | **Type** | **Applies To** |
|-----|-----|-----|-----|
| **id** | Unique identifier assigned by PDF viewer | string | All |
| **name** | Field name from PDF document | string | All |
| **type** | Field type (Textbox, Password, CheckBox, RadioButton, DropDown, ListBox, SignatureField, InitialField) | string | All |
| **value** | Current field value | string | All |
| **backgroundColor** | Background color (hex format) | string | All |
| **borderColor** | Border color | string | All |
| **color** | Font color (text-based fields) | string | Text-based |
| **fontFamily** | Font family | string | Text-based |
| **fontSize** | Font size | number | Text-based |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | string | Text-based |
| **thickness** | Border thickness (0 = hidden) | number | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | string | Text-based |
| **maxLength** | Maximum character length | number | Text, Password |
| **isReadOnly** | Read-only state | boolean | All |
| **isRequired** | Required field | boolean | All |
| **isMultiline** | Multiline input allowed | boolean | Textbox |
| **isChecked** | Checked state | boolean | CheckBox |
| **isSelected** | Selected state | boolean | RadioButton |
| **isPrint** | Printable | boolean | All |
| **visibility** | Visibility state (visible, hidden) | string | All |
| **tooltip** | Tooltip text | string | All |
| **bounds** | Position and size (X, Y, Width, Height) | object | All |
| **pageNumber** | Page number (1-based) | number | All |
| **options** | Dropdown/ListBox items | ItemModel[] | Dropdown, ListBox |

## Usage Examples

### Configure All Field Settings

```typescript
import { Component } from '@angular/core';
import { PdfViewerModule, FormFieldsService, FormDesignerService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [PdfViewerModule],
  template: `
    <ejs-pdfviewer
      [textFieldSettings]="textFieldSettings"
      [passwordFieldSettings]="passwordFieldSettings"
      [checkBoxFieldSettings]="checkBoxFieldSettings"
      [radioButtonFieldSettings]="radioButtonFieldSettings"
      [dropdownFieldSettings]="dropdownFieldSettings"
      [listBoxFieldSettings]="listBoxFieldSettings"
      [signatureFieldSettings]="signatureFieldSettings"
      [initialFieldSettings]="initialFieldSettings">
    </ejs-pdfviewer>
  `,
  providers: [FormFieldsService, FormDesignerService]
})
export class AppComponent {
  public textFieldSettings = {
    fontFamily: 'Arial',
    fontSize: 12,
    backgroundColor: '#FFFACD',
    maxLength: 200
  };

  public passwordFieldSettings = {
    fontFamily: 'Courier',
    fontSize: 11,
    backgroundColor: '#FFE6E6',
    maxLength: 50
  };

  public checkBoxFieldSettings = {
    backgroundColor: '#E8F5E9',
    borderColor: '#4CAF50',
    thickness: 2
  };

  public radioButtonFieldSettings = {
    backgroundColor: '#E3F2FD',
    borderColor: '#2196F3',
    thickness: 2
  };

  public dropdownFieldSettings = {
    fontFamily: 'Verdana',
    backgroundColor: '#FFF3E0',
    borderColor: '#FF9800'
  };

  public listBoxFieldSettings = {
    fontFamily: 'Verdana',
    backgroundColor: '#F3E5F5',
    borderColor: '#9C27B0'
  };

  public signatureFieldSettings = {
    isRequired: true,
    thickness: 2
  };

  public initialFieldSettings = {
    thickness: 1
  };
}
```

### Add Form Fields Programmatically

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  template: `
    <ejs-pdfviewer #pdfViewer (documentLoad)="onDocumentLoad()">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfviewer!: PdfViewerComponent;

  onDocumentLoad(): void {
    this.pdfviewer.formDesignerModule.addFormField('Textbox', {
      name: 'FirstName',
      bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
      pageNumber: 1,
      isRequired: true,
      tooltip: 'Enter your first name',
      maxLength: 40
    } as any);
  }
}
```

### Modify Existing Form Fields

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  template: `
    <button (click)="customizeFormFields()">Customize Fields</button>
    <ejs-pdfviewer #pdfViewer></ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfviewer!: PdfViewerComponent;

  customizeFormFields(): void {
    const formFields = this.pdfviewer.retrieveFormFields();
    formFields.forEach((field: any) => {
      this.pdfviewer.formDesignerModule.updateFormField(field, {
        backgroundColor: '#FFFF00',
        borderColor: '#000000',
        thickness: 1
      } as any);
    });
  }
}
```

### Get Form Field Values

```typescript
getFormFieldValues(): void {
  const formFields = this.pdfviewer.retrieveFormFields();
  formFields.forEach((field: any) => {
    console.log(`${field.name}: ${field.value}`);
  });
}
```

### Validate Required Fields

```typescript
validateRequiredFields(): boolean {
  const formFields = this.pdfviewer.retrieveFormFields();
  const emptyFields = formFields.filter((field: any) => 
    field.isRequired && !field.value
  );
  
  if (emptyFields.length > 0) {
    console.log('Please fill all required fields');
    return false;
  }
  return true;
}
```

### Handle Form Validation Event

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  template: `
    <ejs-pdfviewer #pdfViewer
      [enableFormFieldsValidation]="true"
      (validateFormFields)="onValidateFormFields($event)">
    </ejs-pdfviewer>
  `
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfviewer!: PdfViewerComponent;

  onValidateFormFields(args: any): void {
    const fields = this.pdfviewer.retrieveFormFields();
    fields.forEach((field: any) => {
      if (field.isRequired && !field.value) {
        alert(`${field.name} field cannot be empty.`);
        args.isFormSubmitCancelled = true;
      }
    });
  }
}
```

## Usage Notes

**Field Settings vs FormField API:**
- **Field Settings** (textFieldSettings, etc.): Default properties for NEW fields added programmatically or via UI
- **FormField API** (retrieveFormFields()): Access/modify EXISTING fields in PDF

**Colors:**
- Hex format: `#RRGGBB` or `#RRGGBBAA` (with alpha/opacity)
- CSS names supported: `red`, `blue`, `transparent`

**Fonts:**
- Apply to text-based fields: Textbox, Password, Dropdown, ListBox
- fontStyle can combine values: `Bold | Italic`
- If font unavailable, browser uses fallback

**Selection Fields:**
- `isChecked`: CheckBox only
- `isSelected`: RadioButton only
- RadioButtons with same name = mutually exclusive group

**Field Positioning:**
- `bounds`: Object with capitalized properties `X, Y, Width, Height` (in points, 1 point = 1/72 inch)
- `pageNumber`: 1-based page index

**Behavior:**
- `isReadOnly`: Non-editable but focusable/copyable
- `isRequired`: Mandatory field for validation (requires `enableFormFieldsValidation: true`)
- `isMultiline`: Textbox only, enables line breaks
- `maxLength`: Textbox/Password only, 0 = unlimited
- `isPrint`: Controls visibility in print output

**Visibility:**
- `visible`: Displayed and interactive
- `hidden`: Invisible, space retained, data preserved

**Validation:**
- Use `enableFormFieldsValidation: true` on component
- Handle `validateFormFields` event to cancel submit/download when required fields are missing
- Set `backgroundColor` to highlight required fields

**Options (Dropdown/ListBox):**
- Format: `{ itemName: 'Display Text', itemValue: 'value' }`
- `itemName`: Shown to user
- `itemValue`: Submitted value

**Form Designer:**
- Inject `FormDesignerService` to enable form design mode
- Use `enableFormDesigner: true` to show designer in toolbar
- Use `isFormDesignerToolbarVisible: true` to show designer toolbar
