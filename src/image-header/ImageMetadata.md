# struct `ImageMetadata`

## UNFINISHED

```
struct ImageMetadata {
    let all_default = read!(Bool);
    let extra_fields = if all_default {
        false
    } else {
        read!(Bool)
    };

    pub let orientation = if extra_fields {
        read!(U(3)) + 1
    } else {
        1
    };

    let has_intrinsic_size = if extra_fields {
        read!(Bool)
    } else {
        false
    };
    pub let intrinsic_size = if has_intrinsic_size {
        Some(read!(struct ImageSize))
    } else {
        None
    };

    let has_preview = if extra_fields {
        read!(Bool)
    } else {
        false
    };
    pub let preview_info = if has_preview {
        Some(read!(struct PreviewInfo))
    } else {
        None
    };

    let has_animation = if extra_fields {
        read!(Bool)
    } else {
        false
    };
    pub let animation_info = if has_preview {
        Some(read!(struct AnimationInfo))
    } else {
        None
    };
}
```

## Orientation

The `orientation` field describes whether the image has to be flipped / rotated and by how much.

`orientation`|Pixel order|Transformation(s)
---|---|---
1 | Top to bottom, left to right | None
2 | Top to bottom, right to left | Horizontal flip
3 | Bottom to top, right to left | 180° rotation
4 | Bottom to top, left to right | Vertical flip
5 | Left to right, top to bottom | 90° rotation clockwise then horizontal flip
6 | Right to left, top to bottom | 90° rotation clockwise
7 | Right to left, bottom to top | Horizontal flip then 90° rotation clockwise
8 | Left to right, bottom to top | 90° rotation counterclockwise

Note: The `orientation` field's value is interpreted the same as in `Exif version 2.3`.

## struct `PreviewInfo`

!TODO


## struct `AnimationInfo`

!TODO

`ImageMetadata` also uses some techniques to encode common image types, as well as to optimise for small images (e.g. icons).
- The `all_default` and `extra_fields` bools allow images with common image formats (XYZ encoded non-animated images without custom upscaling or colour transform parameters)
