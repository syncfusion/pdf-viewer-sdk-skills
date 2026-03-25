# Bookmark Navigation

Brief: Bookmark navigation enables users to navigate through embedded PDF bookmarks. The ASP.NET Core PDF Viewer automatically loads and presents bookmarks for easy document traversal. Use the `goToBookmark` method to navigate to specific bookmarks and `getBookmarks` to retrieve all available bookmarks in a PDF document.

## Enabling Bookmark Navigation

Enable bookmark functionality in the PDF Viewer component to display and interact with bookmarks embedded in the PDF document.

### Property
`enableBookmark="true"`

### Description
Enables the bookmark panel in the PDF Viewer, allowing users to view and navigate through document bookmarks.

### Usage
```html
<ejs-pdfviewer
  enableBookmark="true">
</ejs-pdfviewer>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### Note
- The `BookmarkView` service must be injected for bookmark functionality to work
- Bookmarks are loaded automatically from the PDF document when `enableBookmark` is set to `true`
- The bookmark panel appears in the left sidebar of the PDF Viewer

---

## Navigate to Bookmark

Use the `goToBookmark` method to programmatically navigate to a specific bookmark location within the PDF document.

### Method
`goToBookmark(x, y)`

### Description
Navigates to a specific bookmark location in the PDF document. The method throws an error if the specified bookmark does not exist in the document.

### Parameters
- **x**: (number) The zero-based page index to navigate to
- **y**: (number) The vertical Y coordinate on the target page to position the viewport

### Usage
```javascript
var onGoToBookmark = function() {
  // Navigate to page index 0 with Y coordinate 100
  var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
  if (pdfViewer) {
    pdfViewer.bookmark.goToBookmark(0, 100);
  }
};

// Button integration
<button onclick="onGoToBookmark()">Go to Specific Page</button>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### Behavior
- The method requires a valid page index (x parameter)
- The Y coordinate (y parameter) determines the vertical position on the target page
- An error is thrown if the page index is invalid or bookmark doesn't exist
- The view updates immediately upon successful navigation

---

## Retrieve All Bookmarks

Use the `getBookmarks` method to retrieve a complete list of all bookmarks available in the PDF document.

### Method
`getBookmarks()`

### Description
Retrieves a list of all bookmarks in the PDF document. Returns a collection of Bookmark objects containing information about each bookmark, including title, page references, and hierarchy.

### Return Value
- **Type**: Array of Bookmark objects
- **Contains**: Bookmark information including titles, page indices, and nested hierarchy

### Usage
```javascript
var onGetBookmarks = function() {
  var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
  var bookmarks = pdfViewer && pdfViewer.bookmark.getBookmarks();
  console.log(bookmarks);
  
  // Process bookmarks
  if (bookmarks && bookmarks.length > 0) {
    bookmarks.forEach(function(bookmark, index) {
      console.log('Bookmark ' + index + ': ' + bookmark.title);
    });
  }
};

// Button integration
<button onclick="onGetBookmarks()">Retrieve Bookmarks</button>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### Behavior
- Returns an empty array if the document contains no bookmarks
- Bookmarks maintain their hierarchical structure in the returned list
- The method is non-destructive and does not modify the PDF document
- Can be called at any time during PDF document viewing

---

## Bookmark Structure

Bookmark objects returned by `getBookmarks()` contain the following information:

### Bookmark Object Properties
- **title**: The display name of the bookmark
- **page**: The zero-based page index the bookmark references
- **y**: The Y coordinate position on the page
- **children**: Array of child bookmarks (for nested bookmarks)
- **destination**: The navigation destination details

### Example Bookmark Data Structure
```javascript
[
  {
    title: "Chapter 1",
    page: 0,
    y: 150,
    children: [
      {
        title: "Section 1.1",
        page: 2,
        y: 200,
        children: []
      },
      {
        title: "Section 1.2",
        page: 5,
        y: 100,
        children: []
      }
    ]
  },
  {
    title: "Chapter 2",
    page: 10,
    y: 50,
    children: []
  }
]
```

---

## Service Dependencies

The following services must be injected for bookmark functionality:

### Required Services
```html
<script>
var services = ['BookmarkView'];
// Optional but recommended:
// 'Toolbar', 'Navigation', 'ThumbnailView'
</script>
```

### Service Descriptions
- **BookmarkView**: Enables the bookmark panel and bookmark-related operations
- **Toolbar** (optional): Provides toolbar items for bookmark operations
- **Navigation** (optional): Enhances overall document navigation capabilities
- **ThumbnailView** (optional): Displays page thumbnails alongside bookmarks

---

## Best Practices

1. **Always check for valid references** before calling bookmark methods:
   ```javascript
   var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
   pdfViewer && pdfViewer.bookmark.goToBookmark(pageIndex, yCoordinate);
   ```

2. **Handle errors gracefully** when navigating to bookmarks:
   ```javascript
   try {
     var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
     pdfViewer.bookmark.goToBookmark(pageIndex, yCoordinate);
   } catch (error) {
     console.error('Bookmark navigation failed:', error);
   }
   ```

3. **Cache bookmark data** if accessing frequently:
   ```javascript
   var cachedBookmarks = null;
   function getAllBookmarks() {
     if (!cachedBookmarks) {
       var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
       cachedBookmarks = pdfViewer && pdfViewer.bookmark.getBookmarks();
     }
     return cachedBookmarks;
   }
   ```

4. **Use BookmarkView service** for all bookmark-related operations

5. **Test with various PDF documents** to ensure bookmark compatibility

---

## Integration Example

Complete example showing bookmark navigation with a bookmark list:

```html
<div style="display: flex; height: 100vh;">
  <div style="width: 200px; overflowY: 'auto'; borderRight: '1px solid #ccc';">
    <h3>Bookmarks</h3>
    <ul id="bookmarkList"></ul>
  </div>
  <div style="flex: 1;">
    <ejs-pdfviewer
      id="pdfViewer"
      enableBookmark="true">
    </ejs-pdfviewer>
  </div>
</div>

<script>
function populateBookmarks() {
  var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
  var allBookmarks = pdfViewer && pdfViewer.bookmark.getBookmarks();
  var bookmarkList = document.getElementById('bookmarkList');
  bookmarkList.innerHTML = '';
  
  if (allBookmarks && allBookmarks.length > 0) {
    allBookmarks.forEach(function(bookmark, index) {
      var li = document.createElement('li');
      li.textContent = bookmark.title;
      li.onclick = function() {
        handleBookmarkClick(bookmark);
      };
      bookmarkList.appendChild(li);
    });
  }
}

function handleBookmarkClick(bookmark) {
  var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
  if (pdfViewer) {
    pdfViewer.bookmark.goToBookmark(bookmark.page, bookmark.y);
  }
}

// Populate bookmarks when document loads
setTimeout(populateBookmarks, 1000);
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---