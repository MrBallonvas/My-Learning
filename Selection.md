## Notes

### String representation of a selection
Calling the [`Selection.toString()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/toString) method returns the text contained within the selection, e.g.:

```JS
const selObj = window.getSelection();
window.alert(selObj);
```

Note that using a selection object as the argument to `window.alert` will call the object's `toString` method.

### Multiple ranges in a selection
A selection object represents the [`Range`](https://developer.mozilla.org/en-US/docs/Web/API/Range)s that the user has selected. Typically, it holds only one range, accessed as follows:

```JS
const selObj = window.getSelection();
const range = selObj.getRangeAt(0);
```

- `selObj` is a Selection object
- `range` is a [`Range`](https://developer.mozilla.org/en-US/docs/Web/API/Range) object

As the [Selection API specification notes](https://www.w3.org/TR/selection-api/#h_note_15), the Selection API was initially created by Netscape and allowed multiple ranges (for instance, to allow the user to select a column from a [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)). However, browsers other than Gecko did not implement multiple ranges, and the specification also requires the selection to always have a single range.

### Selection and input focus
Selection and input focus (indicated by [`Document.activeElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/activeElement)) have a complex relationship that varies by browser. In cross-browser compatible code, it's better to handle them separately.

Safari and Chrome (unlike Firefox) currently focus the element containing selection when modifying the selection programmatically; it's possible that this may change in the future (see [W3C bug 14383](https://www.w3.org/Bugs/Public/show_bug.cgi?id=14383) and [WebKit bug 38696](https://webkit.org/b/38696)).

### Behavior of Selection API in terms of editing host focus changes
The Selection API has a common behavior (i.e., shared between browsers) that governs how focus behavior changes for _editing hosts_ after certain methods are called.

The behavior is as follows:

1. An editing host gains focus if the previous selection was outside of it.
2. A Selection API method is called, causing a new selection to be made with the selection range inside the editing host.
3. Focus then moves to the editing host.

**Note:** The Selection API methods may only move focus to an editing host, not to other focusable elements (e.g., [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)).

The above behavior applies to selections made using the following methods:

- [`Selection.collapse()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/collapse)
- [`Selection.collapseToStart()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/collapseToStart)
- [`Selection.collapseToEnd()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/collapseToEnd)
- [`Selection.extend()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/extend)
- [`Selection.selectAllChildren()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/selectAllChildren)
- [`Selection.addRange()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/addRange)
- [`Selection.setBaseAndExtent()`](https://developer.mozilla.org/en-US/docs/Web/API/Selection/setBaseAndExtent)

And when the [`Range`](https://developer.mozilla.org/en-US/docs/Web/API/Range) is modified using the following methods:

- [`Range.setStart()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setStart)
- [`Range.setEnd()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setEnd)
- [`Range.setStartBefore()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setStartBefore)
- [`Range.setStartAfter()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setStartAfter)
- [`Range.setEndBefore()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setEndBefore)
- [`Range.setEndAfter()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/setEndAfter)
- [`Range.collapse()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/collapse)
- [`Range.selectNode()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/selectNode)
- [`Range.selectNodeContents()`](https://developer.mozilla.org/en-US/docs/Web/API/Range/selectNodeContents)
- 
## Example
```HTML
<style>
	*::selection {
	    background-color: gray;
	    color: white;
	}
</style>

<p>
Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptatum sapiente numquam magni corporis consequuntur quidem? Sed ut libero voluptates possimus necessitatibus. Error molestiae velit cupiditate, necessitatibus excepturi iure atque eos.
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequatur consectetur minus laboriosam ea sed maiores debitis totam temporibus blanditiis dicta?
</p>
<p>
Lorem ipsum dolor sit amet consectetur adipisicing elit. Vero, omnis!
</p>
<p id='output'></p>

<script>
	const data = document.getSelection()
	document.addEventListener('mouseup', (e) => {
	const body = document.body
	const selObj = window.getSelection()
	let text = selObj.toString();
	out.textContent = "Output: " + text;
	// delete selection from document
	selObj.deleteFromDocument()
	// collapse selection
	selObj.collapse(body)
})
</script>
```