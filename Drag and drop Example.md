```HTML
<!DOCTYPE html>
<html lang="en">

<head>
	<style>
		.dz {
			width: 200px;
			height: 200px;
			border: 1px solid black;
		}

	</style>
</head>

<body>
	<div 
		ondragenter="dragEnterHandler(event)" 
		ondragleave="dragLeaveHandler(event)"
		class="dz"
		ondrop="dropHandler(event)"
		ondragover="dragOverHandler(event)"
	>
		<div
			draggable="true"
			ondragend="dragEnd(event)"
			ondragstart="dragStart(event)"
			id="draggable"
		>
			Some text
		</div>
	</div>
	<div
		ondragenter="dragEnterHandler(event)"
		ondragleave="dragLeaveHandler(event)"
		class="dz"
		ondrop="dropHandler(event)"
		ondragover="dragOverHandler(event)"
	></div>

	<script>
		function dragOverHandler(ev) {
			ev.preventDefault();
			ev.dataTransfer.dropEffect = 'move';
			ev.dataTransfer.dropEffect = 'all';
		}

		function dragLeaveHandler(ev) {
			ev.target.style.background = 'white';
		}

		function dragEnterHandler(ev) {
			ev.target.style.background = 'lightgray';
		}

		function dragStart(ev) {
			ev.dataTransfer.setData("text", ev.target.id);
			ev.dataTransfer.effectAllowed = "move";
			ev.dataTransfer.effectAllowed = "all";
			ev.target.style.border = 'dashed';
		}

		function dragEnd(ev) {
			ev.target.style.border = 'solid';
			ev.currentTarget.style.background = 'white';
		}

		function dropHandler(ev) {
			ev.preventDefault();
			const data = ev.dataTransfer.getData('text');
			ev.target.appendChild(document.getElementById(data));
			ev.target.style.background = 'white';
		}
	</script>
</body>

</html>

```
