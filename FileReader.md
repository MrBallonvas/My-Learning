The **`FileReader`** interface lets web applications asynchronously read the contents of files (or raw data buffers) stored on the user's computer, using [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) or [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) objects to specify the file or data to read.

File objects may be obtained from a [`FileList`](https://developer.mozilla.org/en-US/docs/Web/API/FileList) object returned as a result of a user selecting files using the `<input type="file">` element, or from a drag and drop operation's [`DataTransfer`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer) object. `FileReader` can only access the contents of files that the user has explicitly selected; it cannot be used to read a file by pathname from the user's file system. To read files on the client's file system by pathname, use the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_API). To read server-side files, use [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/fetch "fetch()"), with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) permission if reading cross-origin.

EventTargetFileReader

## Constructor

`FileReader()`
Returns a new `FileReader` object.
## Instance properties

`FileReader.error`
A [`DOMException`](https://developer.mozilla.org/en-US/docs/Web/API/DOMException) representing the error that occurred while reading the file.

`FileReader.readyState` Read only
A number indicating the state of the `FileReader`. This is one of the following:

| Name      | Value | Description                                 |
| --------- | ----- | ------------------------------------------- |
| `EMPTY`   | `0`   | No data has been loaded yet.                |
| `LOADING` | `1`   | Data is currently being loaded.             |
| `DONE`    | `2`   | The entire read request has been completed. |

`FileReader.result` Read only
The file's contents. This property is only valid after the read operation is complete, and the format of the data depends on which of the methods was used to initiate the read operation.

## Instance methods

`FileReader.abort()`
Aborts the read operation. Upon return, the `readyState` will be `DONE`.

`FileReader.readAsArrayBuffer()`
Starts reading the contents of the specified [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob), once finished, the `result` attribute contains an [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) representing the file's data.

`FileReader.readAsDataURL()`
Starts reading the contents of the specified [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob), once finished, the `result` attribute contains a `data:` URL representing the file's data.

`FileReader.readAsText()`
Starts reading the contents of the specified [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob), once finished, the `result` attribute contains the contents of the file as a text string. An optional encoding name can be specified.

## Events
Listen to these events using [`addEventListener()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener "addEventListener()") or by assigning an event listener to the `oneventname` property of this interface. Remove the event listeners with [`removeEventListener()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener "removeEventListener()"), once `FileReader` is no longer used, to avoid memory leaks.

`abort`

Fired when a read has been aborted, for example because the program called [`FileReader.abort()`](https://developer.mozilla.org/en-US/docs/Web/API/FileReader/abort).

`error`
Fired when the read failed due to an error.

`load`
Fired when a read has completed successfully.
Fired when a read has completed, successfully or not.

`loadstart`
Fired when a read has started.

`progress`
Fired periodically as data is read.

## Examples

### Using FileReader

This example reads and displays the contents of a text file directly in the browser.

#### HTML
```HTML
<h1>File Reader</h1>
<input type="file" id="file-input" />
<div id="message"></div>
<pre id="file-content"></pre>
```

#### JavaScript
```JS
const fileInput = document.getElementById("file-input");
const fileContentDisplay = document.getElementById("file-content");
const messageDisplay = document.getElementById("message");

fileInput.addEventListener("change", handleFileSelection);

function handleFileSelection(event) {
  const file = event.target.files[0];
  fileContentDisplay.textContent = ""; // Clear previous file content
  messageDisplay.textContent = ""; // Clear previous messages

  // Validate file existence and type
  if (!file) {
    showMessage("No file selected. Please choose a file.", "error");
    return;
  }

  if (!file.type.startsWith("text")) {
    showMessage("Unsupported file type. Please select a text file.", "error");
    return;
  }

  // Read the file
  const reader = new FileReader();
  reader.onload = () => {
    fileContentDisplay.textContent = reader.result;
  };
  reader.onerror = () => {
    showMessage("Error reading the file. Please try again.", "error");
  };
  reader.readAsText(file);
}

// Displays a message to the user
function showMessage(message, type) {
  messageDisplay.textContent = message;
  messageDisplay.style.color = type === "error" ? "red" : "green";
}
```