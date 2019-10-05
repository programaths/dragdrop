# Use

1. Add the `DragDropController` node in your scene.
2. In the inspector, fill in Drag Group with the name of the group containing nodes you want to be draggable, by default, the group is named "draggable".
3. (optional) In the node that can be dragged, you can create two methods : `on_drop` and `on_drag_start`

## on_drop

Called when the node is dropped. 
Return "false" to prevent drop.
Do not return anything (no `return` in your function) or return `true` to allow drop.

Here is an example of implementation to check if you are dropping in a free space:

```godot
onready var previous_position = position
func on_drop():
	position = position.snapped(Vector2(64,64))
	yield(get_tree(),"idle_frame")
	yield(get_tree(),"idle_frame")
	if get_overlapping_areas().size()>0:
		print("col!")
		position = previous_position
	else:
		print("no col")
		previous_position = position
```

## on_drag_start

Called when the node begin to be dragged. (if multiple nodes are stacked, only the topmost node will be dragged)
