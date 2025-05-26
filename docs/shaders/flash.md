# Custom Colored Flash

This little shader is my go-to for making quick hit or flash effects in Godot. Whenever something gets damaged or you want to grab the player’s attention, this shader makes the sprite flash a bright color — super simple but really effective!

<iframe width="560" height="315" src="https://www.youtube.com/embed/071m2ErCFl4" frameborder="0" allowfullscreen></iframe>

| Parameter        | Description                                                         | 
| ---------------- | ------------------------------------------------------------------- | 
| `flash_color`    | The color used to “flash” the sprite.                               |
| `flash_modifier` | Controls the intensity of the flash (0 = no flash, 1 = full flash). |


```
shader_type canvas_item;

uniform vec4 flash_color: source_color = vec4(1.0);
uniform float flash_modifier: hint_range(0.0,1.0) = 1;

void fragment() {
	vec4 color = texture(TEXTURE, UV);
	color.rgb = mix(color.rgb, flash_color.rgb, flash_modifier);
	COLOR = color;
}
```