# Brightness

This shader adjusts the brightness of a 2D texture.

- `brightness` is a uniform float that controls how bright the image appears; it ranges from 1.0 (normal) to 2.0 (twice as bright).
- In the fragment function, the shader samples the texture color at the current UV coordinates.
- Then it multiplies the sampled color by the brightness value, making the texture brighter when brightness > 1.
- The result is assigned to COLOR, which is the final color output for each pixel.

```
shader_type canvas_item;

uniform float brightness : hint_range(1.0, 2.0) = 1.0;

void fragment() {
    vec4 tex_color = texture(TEXTURE, UV);
    COLOR = tex_color * brightness;
}
```