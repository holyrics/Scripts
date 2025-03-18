# Icon

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/Icon.md)

---


Available options for displaying custom icons in the Holyrics features that accept this syntax.<br>

Available types: `image`  `video`  `announcement`  `background`  `theme`<br>
Starting from `v2.23.0+`<br>
`system`  `base64`  `svg`<br>

The value should be provided as a string, starting with the type, followed by a colon and the corresponding value for the specified type.<br>

For the `image` and `video` types, the value is the **name of a file** (including possible subfolders) that exists in the respective Image or Video tab.<br>
Note: The use of a video does not mean that the icon will be animated, like a gif. Only the static image identified from the video will be used.<br>

For the types `announcement`, `background`, and `theme`, the value is the `id` of the item.<br>
Generally, the `id` of an item can be obtained by right-clicking on the item (context menu), option **"Script Info"**.<br>

`system`<br>
In `v2.23.0`, the [Google Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons&icon.style=Filled) library was added to the program.<br>
For the `system` type, the value is the `name` of the icon.<br>
Note: it is optional to specify `system:`, for values provided without a declared `type`, the value will be considered a `system` type icon by default.<br>

For the `base64` type, the value is the bytes of the image (JPG, for example) in base64 format.<br>

For the `svg` type, the value is the XML content of the SVG itself

Examples:
```javascript
icon: 'image:name.jpg'
icon: 'image:folder/name.jpg'

icon: 'video:name.mp4'

icon: 'announcement:1234'

icon: 'background:1234'

icon: 'theme:1234'

icon: 'system:settings'
icon: 'settings'

icon: 'base64:iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAbUlEQVR42mNgGAWjAAgWA7EoLS34AcTvgDielhb8h+K9QKxESwv+Q/mVQMxEKwtg+AIQG9PSAhjuA2IeWloAwveB2IuWFjwEYg9aWdADxFy0CKJLQGxAq2RaTatkup9WGQ1UVCQP2cJuFAxxAAAPXEusG9ShJQAAAABJRU5ErkJggg=='

icon: 'svg:<?xml version="1.0" encoding="utf-8"?>\n<svg fill="#000000" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">\n    <path d="M8 5v14l11-7z"/>\n    <path d="M0 0h24v24H0z" fill="none"/>\n</svg>'
```

## HTML

In places where `html` is allowed, it is possible to use an icon with the `<img>` tag.<br>
Syntax `<img src='icon:{name,size,color}'>`<br>
`size` and `color` are optional<br>

Example:
```html
<!-- 'settings' icon in the same font size and color as the current text -->
<img src='icon:settings'>

<!-- 'settings' icon in size 16px and current text color -->
<img src='icon:settings,16'>

<!-- 'settings' icon in size 16px and green color -->
<img src='icon:settings,16,00FF00'>
```