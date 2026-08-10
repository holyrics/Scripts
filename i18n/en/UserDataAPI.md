# Holyrics User Data API

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/UserDataAPI.md)

---


API to list the files and data of the Holyrics program available on the computer (read-only)<br>
Available from version `2.30.0` expected on `09/15/2026`

Types of available items:<br>
| Type | Class |
| ---- | ------------|
| `song` | [Song](#song) |
| `text` | [Text](#text) |
| `audio` | [Audio](#audio) |
| `video` | [Video](#video) |
| `image` | [Image](#image) |
| `file` | [File](#file) |
| `announcement` | [Announcement](#announcement) |
| `automatic_presentation` | [AutomaticPresentation](#automaticpresentation) |
| `theme` | [Theme](#theme) |
| `background` | [Background](#background) |


This API allows third-party apps (such as volunteer management apps, for example) to make requests to search for an item directly in the user's Holyrics "database."<br>
Allowing, for example, to add audio files, video files, images, folders, etc. that are already on the computer directly into the worship order of the management app.<br>

Observation: This API does not provide direct access to files (audio, video, and images), only the listing and information of the file, as well as a preview image for compatible items, such as images, videos, themes, etc.<br>
The provision of access to the file may be implemented in the future, but for now, there is no forecast.

---

## Request
All API responses return a standard object:
| Name | Type  | Description |
| ---- | :---: | ------------|
| `status` | _String_ | It might be *'ok'* or *'error'* |
| `error` | _String (optional)_ | Error message if status equals *error* |
| `result` | _Object (optional)_ | Response content if *status* equals *ok* |

Standard endpoint
```
https://userdata.holyrics.com.br/api/v1/
```

# Available endpoints 
  - [{type}/{id}](#typeid)
  - [{type}/list](#typelist)
  - [{type}/search](#typesearch)


---

### {type}/{id}
Returns the respective item by ID.<br>
Available types: `song` `text` `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`



**Response:**

| Type  | Description |
| :---: | ------------|
| _Object_ | Object of the class corresponding to the item type |


**Example:** [` userdata.holyrics.com.br/api/v1/text/31ca678b-6ad6-4ad7-ba48-ba409bc6c783 `](https://userdata.holyrics.com.br/api/v1/text/31ca678b-6ad6-4ad7-ba48-ba409bc6c783)<br>

<details>
  <summary>Response</summary>

```json
{
  "status": "ok",
  "result": {
    "id": "31ca678b-6ad6-4ad7-ba48-ba409bc6c783",
    "title": "Text Title Example",
    "language": "",
    "folder": "",
    "theme": null,
    "transition_settings_id": null,
    "slides": [
      {
        "text": "Slide 1\nSlide 1",
        "styled_text": "Slide 1\nSlide 1",
        "background_id": null,
        "transition_settings_id": null,
        "translations": null
      },
      {
        "text": "Slide 2\nSlide 2",
        "styled_text": "Slide 2\nSlide 2",
        "background_id": null,
        "transition_settings_id": null,
        "translations": null
      },
      {
        "text": "Slide 3\nSlide 3",
        "styled_text": "Slide 3\nSlide 3",
        "background_id": null,
        "transition_settings_id": null,
        "translations": null
      }
    ],
    "formatting_type": "basic",
    "extras": {},
    "tags": [],
    "metadata": {
      "modified_time_millis": "0"
    }
  }
}
```
</details>


---

### {type}/list
Lists the available items for the respective type.<br>
Available types: `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`

**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| <br>**Available for the types:** `audio` `video` `image` `file` |  |  |
| `folder` | _String (optional)_ | If the `folder` parameter is declared, only the items from that folder will be listed.<br>If not declared, the root folder will be used as the base.<br>For a subfolder, simply provide the respective path with the separator slash, for example: `folder/subfolder` |
| `is_folder` | _Boolean (optional)_ | If the `is_folder` parameter is declared, only items that are folders (`is_folder=true`) or only items that are files (`is_folder=false`) will be listed |
| `recursive` | _Boolean (optional)_ | If `recursive=true`, then items from subfolders will also be listed `Default: false` |


**Response:**

| Type  | Description |
| :---: | ------------|
| _Array&lt;Object&gt;_ | Array of objects of the corresponding class type of the item |


**Example:** [` userdata.holyrics.com.br/api/v1/image/search?folder=example `](https://userdata.holyrics.com.br/api/v1/image/search?folder=example)<br>

<details>
  <summary>Response</summary>

```json
{
  "status": "ok",
  "result": [
    {
      "id": "0TKgGy8lGs9vvf5cebqAw",
      "name": "example/Jellyfish.jpg",
      "is_folder": false,
      "length": 775702,
      "width": 1024,
      "height": 768,
      "modified_time": "2026-08-09T15:00:00Z",
      "thumbnail_url": "",
      "preview_url": ""
    },
    {
      "id": "1dw4v1vN09JeZHFnwCBrg",
      "name": "example/Hydrangeas.jpg",
      "is_folder": false,
      "length": 595284,
      "width": 1024,
      "height": 768,
      "modified_time": "2026-08-09T15:00:00Z",
      "thumbnail_url": "",
      "preview_url": ""
    }
  ]
}
```
</details>


---

### {type}/search
Search for the available items for the respective type.<br>
Limit: 30 results<br>
Available types: `song` `text` `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`

**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| `q` | _String_ | Text to be searched. |
| <br>**Available for the types:** `audio` `video` `image` `file` |  |  |
| `folder` | _String (optional)_ | If the `folder` parameter is declared, only the items from that folder will be listed.<br>If not declared, the root folder will be used as the base.<br>For a subfolder, simply provide the respective path with the separator slash, for example: `folder/subfolder` |
| `is_folder` | _Boolean (optional)_ | If the `is_folder` parameter is declared, only items that are folders (`is_folder=true`) or only items that are files (`is_folder=false`) will be listed |
| `recursive` | _Boolean (optional)_ | If `recursive=true`, then items from subfolders will also be listed `Default: false` |


**Response:**

| Type  | Description |
| :---: | ------------|
| _Array&lt;Object&gt;_ | Array of objects of the corresponding class type of the item |


**Example:** [` userdata.holyrics.com.br/api/v1/song/search?q=example `](https://userdata.holyrics.com.br/api/v1/song/search?q=example)<br>

<details>
  <summary>Response</summary>

```json
{
  "status": "ok",
  "result": [
    {
      "id": "123",
      "title": "Title Example",
      "artist": "",
      "author": "",
      "note": "",
      "copyright": "",
      "language": "",
      "formatting_type": "basic",
      "order": "",
      "arrangements": [],
      "key": "",
      "bpm": 0,
      "time_sig": "",
      "linked_audio_file": "",
      "linked_backing_track_file": "",
      "streaming": {
        "audio": {
          "spotify": "",
          "youtube": "",
          "deezer": "",
          "apple_music": "",
          "amazon_music": ""
        },
        "backing_track": {
          "spotify": "",
          "youtube": "",
          "deezer": "",
          "apple_music": "",
          "amazon_music": ""
        }
      },
      "extras": {
        "extra": ""
      },
      "tags": [],
      "archived": false,
      "modified_time": "2026-08-08T15:00:00.000Z"
    },
    {
      "id": "456",
      "title": "Title Example",
      "artist": "",
      "author": "",
      "note": "",
      "copyright": "",
      "language": "",
      "formatting_type": "basic",
      "order": "",
      "arrangements": [],
      "key": "",
      "bpm": 0,
      "time_sig": "",
      "linked_audio_file": "",
      "linked_backing_track_file": "",
      "streaming": {
        "audio": {
          "spotify": "",
          "youtube": "",
          "deezer": "",
          "apple_music": "",
          "amazon_music": ""
        },
        "backing_track": {
          "spotify": "",
          "youtube": "",
          "deezer": "",
          "apple_music": "",
          "amazon_music": ""
        }
      },
      "extras": {
        "extra": ""
      },
      "tags": [],
      "archived": false,
      "modified_time": "2026-08-08T16:00:00.000Z"
    }
  ]
}
```
</details>


---



# Classes

## Song
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Song ID |
| `title` | _String_ | Song title |
| `artist` | _String_ | Music artist |
| `author` | _String_ | Music author |
| `note` | _String_ | Music annotation |
| `copyright` | _String_ | Music copyright |
| `slides` | _Array&lt;Object&gt;_ | **The `slides` parameter is not available in the `/list` and `/search` endpoints** |
| `slides.*.text` | _String_ | Slide text |
| `slides.*.styled_text` | _String_ | Slide text with **styled** formatting (when available) |
| `slides.*.slide_description` | _String_ | Slide description |
| `slides.*.background_id` | _String_ | ID of the theme or background saved for the slide |
| `slides.*.translations` | _Object_ | Translations for the slide.<br>Key/value pair. |
| `order` | _String_ | Order of slides (index from 1), separated by comma |
| `title_translations` | _Object_ | Translations for the title slide.<br>Key/value pair. |
| `key` | _String_ | Tone of music.<br>Can be: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number_ | BPM of the song |
| `time_sig` | _String_ | Music time.<br>Can be: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `linked_audio_file` | _String_ | Path of the audio file linked to the song |
| `linked_backing_track_file` | _String_ | Path of the audio file (backing track) linked to the song |
| `streaming` | _Object_ | URI or ID of the streamings |
| `streaming.audio` | _Object_ | Audio |
| `streaming.audio.spotify` | _String_ |  |
| `streaming.audio.youtube` | _String_ |  |
| `streaming.audio.deezer` | _String_ |  |
| `streaming.audio.apple_music` | _String_ |  |
| `streaming.audio.amazon_music` | _String_ |  |
| `streaming.backing_track` | _Object_ | Backing track |
| `streaming.backing_track.spotify` | _String_ |  |
| `streaming.backing_track.youtube` | _String_ |  |
| `streaming.backing_track.deezer` | _String_ |  |
| `streaming.backing_track.apple_music` | _String_ |  |
| `streaming.backing_track.amazon_music` | _String_ |  |
| `extras` | _Object_ | Map of extra objects (added by the user) |
| `theme` | _String_ | Saved theme ID for the song |
| `archived` | _Boolean_ | If the song is archived |
| `tags` | _Array&lt;String&gt;_ |  |
| `metadata.modified_time_millis` | _Number_ | File modification date. (timestamp) `read-only` |

## Text
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Text ID |
| `title` | _String_ | Text title |
| `folder` | _String_ | Path of the location folder |
| `theme` | _String_ | ID of the theme saved for the text |
| `slides` | _Array&lt;Object&gt;_ | **The `slides` parameter is not available in the `/list` and `/search` endpoints** |
| `slides.*.text` | _String_ | Slide text |
| `slides.*.styled_text` | _String_ | Slide text with **styled** formatting (when available) |
| `slides.*.background_id` | _String_ | ID of the theme or background saved for the slide |
| `slides.*.translations` | _Object_ | Translations for the slide.<br>Key/value pair. |
| `formatting_type` | _String_ | `basic`  `styled`  `advanced`<br> <br>When using this object in creation or editing methods, if `formatting_type=basic` is used, the value of the variable `slides.*.text` will be used; otherwise, the value of the variable `slides.*.styled_text` will be used `Default: basic` |
| `extras` | _Object_ | Map of extra objects (added by the user) |
| `tags` | _Array&lt;String&gt;_ |  |
| `metadata.modified_time_millis` | _Number_ | File modification date. (timestamp) `read-only` |

## Audio
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Full name of the item, including folder, if it is within folders and subfolders |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Number of items within the respective folder `(available only for folders)` |
| `length` | _Number_ | File size (in bytes) `(available only for files)` |
| `duration_millis` | _Number_ | Media duration in milliseconds |

## Video
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Full name of the item, including folder, if it is within folders and subfolders |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Number of items within the respective folder `(available only for folders)` |
| `length` | _Number_ | File size (in bytes) `(available only for files)` |
| `duration_millis` | _Number_ | Media duration in milliseconds |
| `width` | _Number_ | Width `px` |
| `height` | _Number_ | Height `px` |
| `preview_url` | _String_ | Preview image URL of the respective item. Maximum Resolution: `1280x720` |
| `thumbnail_url` | _String_ | Thumbnail URL of the respective item. Maximum Resolution: `320x180` |

## Image
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Full name of the item, including folder, if it is within folders and subfolders |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Number of items within the respective folder `(available only for folders)` |
| `length` | _Number_ | File size (in bytes) `(available only for files)` |
| `width` | _Number_ | Width `px` |
| `height` | _Number_ | Height `px` |
| `preview_url` | _String_ | Preview image URL of the respective item. Maximum Resolution: `1280x720` |
| `thumbnail_url` | _String_ | Thumbnail URL of the respective item. Maximum Resolution: `320x180` |

## File
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Full name of the item, including folder, if it is within folders and subfolders |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Number of items within the respective folder `(available only for folders)` |
| `length` | _Number_ | File size (in bytes) `(available only for files)` |

## Announcement
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Item name |
| `text` | _String_ | Announcement text |
| `shuffle` | _Boolean_ | Display the list of ads randomly |
| `archived` | _Boolean_ | If the item is archived |
| `preview_url` | _String_ | Preview image URL of the respective item. Maximum Resolution: `1280x720` |
| `thumbnail_url` | _String_ | Thumbnail URL of the respective item. Maximum Resolution: `320x180` |

## AutomaticPresentation
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Item name |
| `duration` | _Number_ | Duration in milliseconds |

## Theme
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `name` | _String_ | Item name |
| <br>**background** |  | <br>Background |
| `background.type` | _String_ | Type of background. Can be: `color`  `my_video`  `my_image`  `video`  `image`  `pattern`  `transparent`  `image_file`  `video_file` |
| `background.id` | _String_ | <table><tr><td><p align="right">**Type**</p></td><td>Value</td></tr><tr><td><p align="right">color</p></td><td>Color in hexadecimal format</td></tr><tr><td><p align="right">my_video</p></td><td>Item ID</td></tr><tr><td><p align="right">my_image</p></td><td>Item ID</td></tr><tr><td><p align="right">video</p></td><td>Item ID</td></tr><tr><td><p align="right">image</p></td><td>Item ID</td></tr><tr><td><p align="right">pattern</p></td><td>Item ID</td></tr><tr><td><p align="right">transparent</p></td><td>"transparent"</td></tr><tr><td><p align="right">image_file</p></td><td>File name in the library</td></tr><tr><td><p align="right">video_file</p></td><td>File name in the library</td></tr></table> |
| `background.adjust_type` | _String_ | `fill` `extend` `adjust` `side_by_side` `center`<br>Available for: **type=my_image**, **type=image** |
| `background.opacity` | _Number_ | Opacity. `0 ~ 100` |
| `background.velocity` | _Number_ | Available for: **type=my_video**, **type=video**<br>`0.25 ~ 4.0` |
| `base_color` | _String_ | Color in hexadecimal format. Base color of the background when reducing opacity. |
| <br>**font** |  | <br>Source |
| `font.name` | _String_ | Font name |
| `font.bold` | _Boolean_ | Bold |
| `font.italic` | _Boolean_ | Italic |
| `font.size` | _Number_ | Size `0 ~ 50`<br>Value in percentage, based on the slide height. |
| `font.color` | _String_ | Color in hexadecimal format |
| `font.line_spacing` | _Number_ | Line spacing. `-0.5 ~ 1.0`<br>Value in percentage based on the line height. |
| `font.char_spacing` | _Number_ | Spacing between characters. `-40 ~ 120` |
| <br>**align** |  | <br>Alignment |
| `align.horizontal` | _String_ | `left`  `center`  `right`  `justify` |
| `align.vertical` | _String_ | `top`  `middle`  `bottom` |
| `align.margin.top` | _Number_ | `0 ~ 90` |
| `align.margin.right` | _Number_ | `0 ~ 90` |
| `align.margin.bottom` | _Number_ | `0 ~ 90` |
| `align.margin.left` | _Number_ | `0 ~ 90` |
| <br>**effect** |  | <br>Font effects |
| `effect.outline_color` | _String_ | Color in hexadecimal format |
| `effect.outline_weight` | _Number_ | `0.0 ~ 100.0` |
| `effect.brightness_color` | _String_ | Color in hexadecimal format |
| `effect.brightness_weight` | _Number_ | `0.0 ~ 100.0` |
| `effect.shadow_color` | _String_ | Color in hexadecimal format |
| `effect.shadow_x_weight` | _Number_ | `-100.0 ~ 100.0` |
| `effect.shadow_y_weight` | _Number_ | `-100.0 ~ 100.0` |
| `effect.blur` | _Boolean_ | Apply 'blur' effect on brightness and shadow |
| <br>**shape_fill** |  | <br>Background color |
| `shape_fill.type` | _String_ | `box`  `line`  `line_fill`  `theme_margin` |
| `shape_fill.enabled` | _Boolean_ |  |
| `shape_fill.color` | _String_ | Color in hexadecimal format (RGBA) |
| `shape_fill.margin.top` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.right` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.bottom` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.left` | _Number_ | `0 ~ 100` |
| `shape_fill.corner` | _Number_ | `0 ~ 100` |
| <br>**shape_outline** |  | <br>Outline |
| `shape_outline.type` | _String_ | `box`  `line`  `line_fill`  `theme_margin` |
| `shape_outline.enabled` | _Boolean_ |  |
| `shape_outline.color` | _String_ | Color in hexadecimal format (RGBA) |
| `shape_outline.outline_thickness` | _Number_ | `0 ~ 25` |
| `shape_outline.margin.top` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.right` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.bottom` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.left` | _Number_ | `0 ~ 100` |
| `shape_outline.corner` | _Number_ | `0 ~ 100` |
| <br>**comment** |  | <br>Comment |
| `comment.font_name` | _String_ | Font name |
| `comment.bold` | _Boolean_ | Bold |
| `comment.italic` | _Boolean_ | Italic |
| `comment.relative_size` | _Number_ | relative font size. `40 ~ 100` |
| `comment.color` | _String_ | Color in hexadecimal format |
| <br>**settings** |  | <br>Settings |
| `settings.uppercase` | _Boolean_ | Display the text in uppercase |
| `settings.line_break` | _String_ | Apply line break. `system`  `true`  `false`<br> `Default: system` |
| <br>**metadata** |  | <br> |
| `metadata.modified_time_millis` | _Number_ | File modification date. (timestamp) `read-only` |
| `preview_url` | _String_ | Preview image URL of the respective item. Maximum Resolution: `1280x720` |
| `thumbnail_url` | _String_ | Thumbnail URL of the respective item. Maximum Resolution: `320x180` |

## Background
| Name | Type  | Description |
| ---- | :---: | ------------|
| `id` | _String_ | Item ID |
| `type` | _String_ | Type of item. Can be: `theme` `my_video` `my_image` `video` `image` |
| `name` | _String_ | Item name |
| `width` | _Number (optional)_ |  |
| `height` | _Number (optional)_ |  |
| `duration` | _Number (optional)_ | Duration in milliseconds |
| `tags` | _Array&lt;String&gt;_ | Item tag list |
| `bpm` | _Number_ | BPM value of item |
| `preview_url` | _String_ | Preview image URL of the respective item. Maximum Resolution: `1280x720` |
| `thumbnail_url` | _String_ | Thumbnail URL of the respective item. Maximum Resolution: `320x180` |