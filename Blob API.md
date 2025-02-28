The **`Blob`** interface represents a blob, which is a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) so its methods can be used for processing the data.

Blobs can represent data that isn't necessarily in a JavaScript-native format. The [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) interface is based on `Blob`, inheriting blob functionality and expanding it to support files on the user's system.
## [Instance properties](https://developer.mozilla.org/en-US/docs/Web/API/Blob#instance_properties)

[`Blob.size`](https://developer.mozilla.org/en-US/docs/Web/API/Blob/size) Read only

The size, in bytes, of the data contained in the `Blob` object.

[`Blob.type`](https://developer.mozilla.org/en-US/docs/Web/API/Blob/type) Read only

A string indicating the MIME type of the data contained in the `Blob`. If the type is unknown, this string is empty.
## Instance methods
**`Blob.arrayBuffer()`**
Returns a promise that resolves with an [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) containing the entire contents of the `Blob` as binary data.

**`Blob.bytes()`**
Returns a promise that resolves with an [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) containing the contents of the `Blob`.

**`Blob.slice()`**
Returns a new `Blob` object containing the data in the specified range of bytes of the blob on which it's called.

**`Blob.stream()`**
Returns a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) that can be used to read the contents of the `Blob`.

**`Blob.text()`**
Returns a promise that resolves with a string containing the entire contents of the `Blob` interpreted as UTF-8 text.