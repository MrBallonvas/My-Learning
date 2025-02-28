The **`File`** interface provides information about files and allows JavaScript in a web page to access their content.

`File` objects are generally retrieved from a [[FileList]](https://developer.mozilla.org/en-US/docs/Web/API/FileList) object returned as a result of a user selecting files using the [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) element, or from a drag and drop operation's [`DataTransfer`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer) object.

A `File` object is a specific kind of [[Blob API]], and can be used in any context that a Blob can. In particular, the following APIs accept both `Blob`s and `File` objects:

- [`FileReader`](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)
- [`URL.createObjectURL()`](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL_static "URL.createObjectURL()")
- [`Window.createImageBitmap()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/createImageBitmap) and [`WorkerGlobalScope.createImageBitmap()`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerGlobalScope/createImageBitmap)
- the [`body`](https://developer.mozilla.org/en-US/docs/Web/API/RequestInit#body) option to [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/fetch "fetch()")
- [`XMLHttpRequest.send()`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send)
# Instance properties
_The `File` interface also inherits properties from the [[Blob API]] interface._

[`File.lastModified`](https://developer.mozilla.org/en-US/docs/Web/API/File/lastModified) Read only

Returns the last modified time of the file, in millisecond since the UNIX epoch (January 1st, 1970 at Midnight).

[`File.lastModifiedDate`](https://developer.mozilla.org/en-US/docs/Web/API/File/lastModifiedDate) Deprecated Read only Non-standard

Returns the last modified [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) of the file referenced by the `File` object.

[`File.name`](https://developer.mozilla.org/en-US/docs/Web/API/File/name) Read only

Returns the name of the file referenced by the `File` object.

[`File.webkitRelativePath`](https://developer.mozilla.org/en-US/docs/Web/API/File/webkitRelativePath) Read only

Returns the path the URL of the `File` is relative to.