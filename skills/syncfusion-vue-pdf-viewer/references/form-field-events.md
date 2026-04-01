# Form Field Events

**Goal:** Syncfusion Vue PDF Viewer exposes granular form designer events so Vue apps can react whenever a form field is created, selected, updated, moved, or validated. These hooks surface the metadata you need to drive UI rules, analytics, or custom persistence without polling the viewer state.

## Subscribing to form-field events in Vue

Attach handlers on `<ejs-pdfviewer>` by using Vue event modifiers. Each event keeps its camelCase name.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :serviceUrl="serviceUrl"
    :documentPath="documentPath"
    @formFieldAdd="onFieldAdd"
    @formFieldClick="onFieldClick"
    @formFieldPropertiesChange="onFieldPropsChange"
  />
</template>

<script setup>
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer'
const documentPath = 'FormTemplate.pdf'

const onFieldAdd = (args) => {
  console.log('Field created', args.field?.name)
}

const onFieldClick = (args) => {
  if (args.cancel) {
    return
  }
  console.log('Clicked field id', args.field?.id)
}

const onFieldPropsChange = (args) => {
    console.log('Updated props', args.changedProperties)
}
</script>
```

Every handler receives an `args` object documented below. Use the same approach inside the Options API (`methods`) if you are not on `<script setup>`.

---

## Event catalog (Vue)

| Event | When it fires | Args type | Payload highlights |
|-----|-----|-----|-----|
| **formFieldAdd** | A new field is inserted through the designer toolbar or via the API. | `formFieldAddArgs` | `cancel` (bool) lets you veto creation.<br>`field` (`FormFieldInfo`) holds the field being added. |
| **formFieldRemove** | A form element is removed from the page. | `formFieldRemoveArgs` | `cancel` (bool) to block deletion.<br>`field` (`FormFieldInfo`) describes the target.<br>`pageIndex` (number) tells which page lost the field. |
| **formFieldClick** | Users click any form field inside the viewer canvas. | `formFieldClickArgs` | `cancel` (bool) suppresses default focus behavior.<br>`field` (`FormFieldInfo`) for the clicked element. |
| **formFieldDoubleClick** | Double-click gesture occurs on a field (often to open the property pane). | `formFieldDoubleClickArgs` | `cancel` (bool) prevents the built-in editor from opening.<br>`field` (`FormFieldInfo`) references the target. |
| **formFieldSelect** | The designer highlights a field as the active selection. | `formFieldSelectArgs` | `field` (`FormFieldInfo`) for the selected item.<br>`isProgrammaticSelection` (bool) indicates API-driven selection.<br>`pageIndex` (number) shows the page hosting the field. |
| **formFieldUnselect** | A previously selected item loses focus/selection. | `formFieldUnselectArgs` | `field` (`FormFieldInfo`) for the item being cleared.<br>`pageIndex` (number) identifies the page. |
| **formFieldResize** | Drag handles resize a field. | `formFieldResizeArgs` | `field` (`FormFieldInfo`) for context.<br>`newBounds` (`PdfBounds`) capture the latest position/size.<br>`oldBounds` (`PdfBounds`) store the prior rectangle.<br>`pageIndex` (number) indicates which page was edited. |
| **formFieldMove** | A field gets dragged to a different location. | `formFieldMoveArgs` | `field` (`FormFieldInfo`) is the moved object.<br>`newPosition` (`PdfPoint`) is the updated origin.<br>`oldPosition` (`PdfPoint`) is the previous origin.<br>`pageIndex` (number) marks the page. |
| **validateFormFields** | Validation fails during download or print (required fields missing, invalid values, etc.). | `validateFormFieldsArgs` | `cancel` (bool) cancels the workflow.<br>`formField` (array) lists the invalid fields.<br>`documentName` (string) is the file under validation. |
| **formFieldFocusOut** | A field loses focus after editing. | `formFieldFocusOutEventArgs` | `field` (`FormFieldInfo`) for the element that lost focus.<br>`pageIndex` (number) indicates its page. |
| **formFieldMouseOver** | The pointer hovers over a field. | `formFieldMouseOverArgs` | `field` (`FormFieldInfo`) for the hovered element.<br>`pageIndex` (number) page reference.<br>`pageX`/`pageY` (number) coordinates relative to the page.<br>`x`/`y` (number) coordinates relative to the viewer container. |
| **formFieldMouseLeave** | Pointer exits the bounds of a field. | `formFieldMouseLeaveArgs` | `field` (`FormFieldInfo`) for the element just left.<br>`pageIndex` (number) page reference. |
| **formFieldPropertiesChange** | Any property change (style, constraint, metadata) is applied. | `formFieldPropertiesChangeArgs` | `changedProperties` (array) names of properties that changed.<br>`newValue` (`FormFieldInfo`) snapshot after the change.<br>`oldValue` (`FormFieldInfo`) snapshot before the change. |

> All event names align with the React reference so that cross-platform documentation stays consistent.

---

## FormFieldInfo schema

`FormFieldInfo` describes one form field instance and is returned by most of the events above.

| Property | What it represents | Type |
|-----|-----|-----|
| `alignment` | Horizontal text alignment (see TextAlignment values). | string |
| `backgroundColor` | Hex color string for the field background. | string |
| `bounds` | Field rectangle relative to the PDF page (see `PdfBounds`). | `PdfBounds` |
| `color` | Foreground/text color as a hex string. | string |
| `customData` | Arbitrary metadata bag for app-specific data. | object |
| `fontFamily` | Font family name used to render text. | string |
| `fontSize` | Numeric font size. | number |
| `fontStyle` | Font styling flag (see FontStyle table). | string |
| `id` | Unique identifier generated for the field. | string |
| `isReadOnly` | Marks whether the field is locked against edits. | bool |
| `isRequired` | Indicates whether validation requires the field. | bool |
| `name` | Logical field name shown in the designer. | string |
| `pageIndex` | Zero-based page index that hosts the field. | number |
| `thickness` | Border thickness. | number |
| `tooltipText` | Helper text shown as tooltip. | string |
| `type` | Field type enum (see FormFieldType list). | `FormFieldType` |
| `value` | Current value or text content. | string |

---

## PdfBounds structure

`PdfBounds` captures the rectangle used for movement and resize events.

| Property | Description | Type |
|-----|-----|-----|
| `x` | Left coordinate from the page origin. | number |
| `y` | Top coordinate from the page origin. | number |
| `width` | Width of the field. | number |
| `height` | Height of the field. | number |

---

## FormFieldType values

| Type | Meaning |
|-----|-----|
| `Textbox` | Single-line text entry. |
| `PasswordField` | Masked textbox for sensitive data. |
| `Checkbox` | Boolean toggle box. |
| `RadioButton` | Radio button that belongs to an option group. |
| `DropdownList` | Drop-down list for single selection. |
| `ListBox` | Multi-select or single-select list box. |
| `SignatureField` | Digital signature placeholder. |
| `InitialField` | Initials capture control. |

---

## FontStyle values

| Value | Effect |
|-----|-----|
| `None` | No additional style besides the default weight. |
| `Bold` | Renders text in bold weight. |
| `Italic` | Slants text. |
| `Underline` | Draws an underline beneath the text. |
| `Strikethrough` | Paints a strike through the text baseline. |

---

## TextAlignment values

| Value | Effect |
|-----|-----|
| `left` | Text anchors to the left edge of the field. |
| `center` | Text is centered horizontally. |
| `right` | Text anchors to the right edge. |
| `justify` | Text stretches to fill the width, aligning both edges. |

---

## Behavior tips

- UI actions and programmatic calls raise the same events, so a single handler covers both scenarios.
- Property-change notifications are immediate—persist your data store whenever `formFieldPropertiesChange` fires.
- `validateFormFields` only runs when print/download is initiated, letting you block those flows while keeping editing fluid.
- Every supported form field type listed above emits the same events, so you can branch using `args.field.type` when necessary.
