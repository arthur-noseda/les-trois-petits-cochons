# Fluidifier l'animation

Mettre à jour le script `Tile.gd` avec le code ci-dessous, puis tester le jeu.

```python
extends Node3D

@onready var grid_map = $GridMap

var target_pos
var target_deg := 0


# Called when the node enters the scene tree for the first time.
func _ready():
	target_pos = grid_map.position


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta):
	if Input.is_action_just_pressed("move_left"):
		# translate(Vector3.LEFT)
		target_pos.x -= 1
	if Input.is_action_just_pressed("move_right"):
		# translate(Vector3.RIGHT)
		target_pos.x += 1
	if Input.is_action_just_pressed("move_up"):
		# translate(Vector3.FORWARD)
		target_pos.z -= 1
	if Input.is_action_just_pressed("move_down"):
		# translate(Vector3.BACK)
		target_pos.z += 1
	if Input.is_action_just_pressed("rotate"):
		# rotate_y(deg_to_rad(90))
		target_deg = (target_deg + 90) % 360

	if not is_zero_approx(target_pos.x - grid_map.position.x):
		var tx = lerp(0.0, 1.0, delta * 3.0)
		if tx > abs(target_pos.x - grid_map.position.x):
			grid_map.position.x = target_pos.x
		elif target_pos.x > grid_map.position.x:
			grid_map.position.x += tx
		else:
			grid_map.position.x -= tx

	if not is_zero_approx(target_pos.z - grid_map.position.z):
		var tz = lerp(0.0, 1.0, delta * 3.0)
		if tz > abs(target_pos.z - grid_map.position.z):
			grid_map.position.z = target_pos.z
		elif target_pos.z > grid_map.position.z:
			grid_map.position.z += tz
		else:
			grid_map.position.z -= tz

	var difference := angle_difference(grid_map.rotation.y, deg_to_rad(target_deg))
	if difference > 0.0:
		var rotation_y := lerp_angle(0.0, deg_to_rad(90.0), delta * 3.0)
		var effective_rotation_y = min(rotation_y, difference)
		grid_map.rotate_y(effective_rotation_y)
```
