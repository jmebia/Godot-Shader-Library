# Color Manipulation

Shaders that you'd use to alter your sprite's color properties such as brightness and saturation.

## Custom Colored Flash

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

## Brightness
```
shader_type canvas_item;

uniform float brightness : hint_range(1.0, 2.0) = 1.0;

void fragment() {
    vec4 tex_color = texture(TEXTURE, UV);
    COLOR = tex_color * brightness;
}
```

## Saturation
```
shader_type canvas_item;

uniform float saturation : hint_range(0.0, 1.0, 0.1);

void fragment() {
    vec4 tex_color = texture(TEXTURE, UV);

    COLOR.rgb = mix(vec3(dot(tex_color.rgb, vec3(0.299, 0.587, 0.114))), tex_color.rgb, saturation);
	COLOR.a = tex_color.a;
}
```

## Silhoutte

This is the shader I used to draw *ghost effects* for a character dash mechanic.

```
shader_type canvas_item;

render_mode blend_mix;
uniform vec4 modulate: source_color;

void fragment() {
	COLOR = vec4(modulate.rgb, texture(TEXTURE, UV).a * modulate.a);
}
```