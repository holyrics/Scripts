# TextTransform

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/TextTransform.md)

---


`file menu > settings > several > insert text`

Allows you to insert text at the beginning or end of a slide or change the current text.<br>
This action is performed at runtime at the moment of projecting the respective slide and is applied independently for each screen, according to the value in `screen_id`.<br>
Note: there is a 30-second cache to reuse the last value returned by the function, based on the same slide and the same screen.

The parameter `obj` is of type [TextTransformInfo](#texttransforminfo)

## Example

```javascript
function getData(obj) {
    return {
         /* optional */
         //Value that will be added at the beginning of the current slide text
         add_start: "", // (string)
         //
         /* optional */
         //Value that will be added at the end of the current slide text
         add_end: "", // (string)
         //
         /* optional */
         //Adds the text with a line break (default: true)
         line_break: true, // (boolean)
         //
         /* optional */
         //Value to replace the text of the current slide
         replace: "" // (string)
    }
}
```

```javascript
// EXTRA SLIDE
function getData(obj) {
    if (obj.screen_id == 'public' && obj.slide_type == 'blank') {
        // This causes on the 'public' screen
        // when the F9 option (without text) is enabled
        // the text '♪' should be displayed
        return {
            add_end: '♪'
        };
    }
    return null;
}
```

## TextTransformInfo
Contains information about the origin of the request

| Name | Type  | Description |
| ---- | :---: | ------------|
| `screen_id` | _String_ | `public` `screen_2` `screen_3` `screen_?` `stream_image` `stream_html_1` `stream_html_2` `stream_html_3` |
| `source_type` | _String_ | `music` `text` `unknown` |
| `source_id` | _String_ |  |
| `slide_type` | _String_ | `default` `final_slide` `wallpaper` `blank` `black` |
| `text` | _String_ | Slide text |
| `slide_number` | _Number_ | Available if `source_type = music` or `source_type = text`.<br>Slide number. Starts at 1. |
| `total_slides` | _Number_ | Available if `source_type = music` or `source_type = text`.<br>Total slides. |
| `stage_view_enabled` | _Boolean_ | Check if the **Stage View** option is enabled on the screen |
| `stage_view_preview_mode` | _String_ | Available if `stage_view_enabled = true`<br>`CURRENT_SLIDE`<br>`FIRST_LINE_OF_THE_NEXT_SLIDE_WITH_SEPARATOR`<br>`FIRST_LINE_OF_THE_NEXT_SLIDE_WITHOUT_SEPARATOR`<br>`NEXT_SLIDE`<br>`CURRENT_AND_NEXT_SLIDE`<br>`ALL_SLIDES` |
| `stage_view_show_comment` | _Boolean_ | Available if `stage_view_enabled = true` |
| `stage_view_show_communication_panel` | _Boolean_ | Available if `stage_view_enabled = true` |
| <br>Available if **source_type=music** |  |  |
| `title` | _String_ | Song title |
| `artist` | _String_ | Music artist |
| `author` | _String_ | Music author |
| `note` | _String_ | Music annotation |
| `copyright` | _String_ | Music copyright |
| `key` | _String_ | Tone of music.<br>Can be: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number_ | BPM of the song |
| `time_sig` | _String_ | Music time.<br>Can be: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `slide_description` | _String_ |  |
| <br>Available if **source_type=text** |  |  |
| `title` | _String_ | Text title |