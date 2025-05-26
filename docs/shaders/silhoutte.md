# Silhoutte

This is the shader I used to draw *ghost effects* for a character dash mechanic.

```
shader_type canvas_item;

render_mode blend_mix;
uniform vec4 modulate: source_color;

void fragment() {
	COLOR = vec4(modulate.rgb, texture(TEXTURE, UV).a * modulate.a);
}
```