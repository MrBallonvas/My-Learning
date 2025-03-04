The **`DataTransfer`** object is used to hold any data transferred between contexts, such as a drag and drop operation, or clipboard read/write. It may hold one or more data items, each of one or more data types.

`DataTransfer` was primarily designed for the [HTML Drag and Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API), as the [`DragEvent.dataTransfer`](https://developer.mozilla.org/en-US/docs/Web/API/DragEvent/dataTransfer) property, and is still specified in the HTML drag-and-drop section, but it is now also used by other APIs, such as [`ClipboardEvent.clipboardData`](https://developer.mozilla.org/en-US/docs/Web/API/ClipboardEvent/clipboardData) and [`InputEvent.dataTransfer`](https://developer.mozilla.org/en-US/docs/Web/API/InputEvent/dataTransfer). However, other APIs only use certain parts of its interface, ignoring properties such as `dropEffect`. Documentation of `DataTransfer` will primarily discuss its usage in drag-and-drop operations, and you should refer to the other APIs' documentation for usage of `DataTransfer` in those contexts.
## Instance properties

`DataTransfer.dropEffect`
Gets the type of drag-and-drop operation currently selected or sets the operation to a new type. The value must be `none`, `copy`, `link` or `move`.

`DataTransfer.effectAllowed`
Provides all of the types of operations that are possible. Must be one of `none`, `copy`, `copyLink`, `copyMove`, `link`, `linkMove`, `move`, `all` or `uninitialized`.

`DataTransfer.files`
Contains a list of all the local files available on the data transfer. If the drag operation doesn't involve dragging files, this property is an empty list.

`DataTransfer.items`
Gives a [`DataTransferItemList`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransferItemList) object which is a list of all of the drag data.

`DataTransfer.types`
An array of strings giving the formats that were set in the [`dragstart`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragstart_event "dragstart") event.

## Instance methods
`DataTransfer.addElement()` Experimental Non-standard
Sets the drag source for the given element. This will be the element on which [`drag`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/drag_event "drag") and [`dragend`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragend_event "dragend") events are fired, and not the default target (the node that was dragged). Firefox-specific.

`DataTransfer.clearData()`
Remove the data associated with a given type. The type argument is optional. If the type is empty or not specified, the data associated with all types is removed. If data for the specified type does not exist, or the data transfer contains no data, this method will have no effect.

`DataTransfer.getData()`
Retrieves the data for a given type, or an empty string if data for that type does not exist or the data transfer contains no data.

`DataTransfer.setData()`
Set the data for a given type. If data for the type does not exist, it is added at the end, such that the last item in the types list will be the new format. If data for the type already exists, the existing data is replaced in the same position.

`DataTransfer.setDragImage()`
Set the image to be used for dragging if a custom one is desired.
