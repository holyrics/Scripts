# API Popup Create Song

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/ApiPopupCreateSong.md)

---


API option to create a new song by opening the lyrics editing window. (v2.21.0+)

This allows any other process on the computer to send content to the program to open the text editing window.

```
curl -X 'POST' \
  'http://localhost:8091/api/popup-createsong' \
  -H 'Content-Type: application/json' \
  -d '{ "title": "...", "author": "...", "artist": "...", "lyrics": "..." }'
```

**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| `title` | _String_ | Song title |
| `lyrics` | _String_ | Song lyrics.<br>Optional if `paragraphs` is declared |
| `paragraphs` | _Array&lt;Object&gt;_ | Alternative parameter for more complex values.<br>Optional if `lyrics` is declared `v2.23.0+` |
| `paragraphs.*.text` | _String_ | Paragraph text `v2.23.0+` |
| `paragraphs.*.description` | _String (optional)_ | Description of the paragraph. chorus, verse, ... `v2.23.0+` |
| `paragraphs.*.translations` | _Object (optional)_ | Translations for the slide.<br>Key/value pair. `v2.23.0+` |
| `author` | _String (optional)_ | Music author |
| `artist` | _String (optional)_ | Music artist |
| `copyright` | _String (optional)_ | Music copyright `v2.23.0+` |
| `note` | _String (optional)_ | Music annotation |
| `key` | _String (optional)_ | Tone of music.<br>Can be: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number (optional)_ | BPM of the song |
| `time_sig` | _String (optional)_ | Music time.<br>Can be: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `streaming` | _Object_ | URI or ID of the streamings `v2.23.0+` |
| `streaming.audio` | _Object_ | Audio `v2.23.0+` |
| `streaming.audio.spotify` | _String_ |  `v2.23.0+` |
| `streaming.audio.youtube` | _String_ |  `v2.23.0+` |
| `streaming.audio.deezer` | _String_ |  `v2.23.0+` |
| `streaming.backing_track` | _Object_ | Backing track `v2.23.0+` |
| `streaming.backing_track.spotify` | _String_ |  `v2.23.0+` |
| `streaming.backing_track.youtube` | _String_ |  `v2.23.0+` |
| `streaming.backing_track.deezer` | _String_ |  `v2.23.0+` |
| `extras` | _Object (optional)_ | Map of extra objects (added by the user)<br>Allowed only for already existing fields. `v2.23.0+` |
| `title_translations` | _Object_ | Translations for the title slide.<br>Key/value pair. `v2.23.0+` |


Observations:<br>
- Available from version 2.21.0;
- The "API Server" option must be enabled in the program settings;
- Accepts only requests from the local machine using the loopback address;
- If it has been modified, change port 8091 of the request to the corresponding port defined in the API Server settings.

Simple JSON model
```json
{
  "title": "title",
  "lyrics": "Slide 1\nSlide 1\n\nSlide 2\nSlide 2",
  "artist": "artist",
  "author": "author",
  "copyright": "copyright",
}
```

Complex JSON model
```json
{
  "title": "title",
  "title_translations": {
    "key1": "value",
    "key2": "value"
  },
  "artist": "artist",
  "author": "author",
  "note": "note",
  "copyright": "copyright",
  "key": "",
  "bpm": 0.0,
  "time_sig": "",
  "paragraphs": [
    {
      "text": "Slide 1\nSlide 1",
      "description": "",
      "translations": {
        "key1": "value",
        "key2": "value"
      }
    }, {
      "text": "Slide 2\nSlide 2",
      "description": "",
      "translations": {
        "key1": "value",
        "key2": "value"
      }
    }
  ],
  "streaming": {
    "audio": {
      "spotify": "spotify_id",
      "youtube": "youtube_id",
      "deezer": "deezer_id"
    },
    "backing_track": {
      "spotify": "spotify_id",
      "youtube": "youtube_id",
      "deezer": "deezer_id"
    }
  },
  "extras": {
    "extra": "",
    "key1": "value",
    "key2": "value"
  }
}
```