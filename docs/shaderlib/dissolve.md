# Dissolve and Fade Effects

The following are shaders that erase or reveal using masks, noise, or alpha

## Dissolve

This dissolve shader can be used for effects like a character or object burning away, fading out, or vanishing with noise-based erosion.

<iframe width="560" height="315" src="https://www.youtube.com/embed/FHCsIK7OsU0" frameborder="0" allowfullscreen></iframe>


| Parameter          | Description                                      |
| ------------------ | ------------------------------------------------ |
| `dissolve_texture` | Noise or gradient texture to control dissolve    |
| `dissolve_amount`  | From `0.0` (fully visible) to `1.0` (fully gone) |
| `edge_color`       | Color of the dissolving edge (e.g., flame, glow) |
| `edge_thickness`   | How thick the glowing edge is                    |

```
shader_type canvas_item;

uniform sampler2D dissolve_texture; // grayscale noise/gradient
uniform float dissolve_amount : hint_range(0.0, 1.0) = 0.0;
uniform vec4 edge_color : source_color = vec4(1.0, 0.3, 0.0, 1.0); // fiery edge
uniform float edge_thickness : hint_range(0.0, 0.2) = 0.05;

void fragment() {
    vec4 tex_color = texture(TEXTURE, UV);
    float dissolve_value = texture(dissolve_texture, UV).r;

    float edge_start = dissolve_amount - edge_thickness;
    float edge_end = dissolve_amount;

    if (dissolve_value < edge_start) {
        // Fully dissolved
        discard;
    } else if (dissolve_value < edge_end) {
        // Edge glow
        COLOR = edge_color;
    } else {
        // Normal rendering
        COLOR = tex_color;
    }
}
```

