# Advanced Lyrics Search

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/AdvancedLyricSearch.md)

---


It is possible to perform an advanced search in the lyrics tab for a more precise filter of items, using items not available in the interface and filtering by different items simultaneously.

Search syntax:

```
%key: value   &&   %key: < value   &&   %key: value
```

Use "percentage" at the beginning of the key and a colon at the end of the key.<br>
Next, please provide the value you wish to search for.

To use multiple keys, use the "&&" sign to separate the items.

Available items:<br>
- [title](#title)
- [artist](#artist)
- [lyrics](#lyrics)
- [note](#note)
- [author](#author)
- [group](#group)
- [comment](#comment)
- [slide_description](#slide_description)
- [translation](#translation)
- [bpm](#bpm)
- [chord_key](#chord_key)
- [time_sig](#time_sig)
- [extra](#extra)
- [order](#order)
- [saved_theme](#saved_theme)
- [played_days](#played_days)
- [played_count](#played_count)

`v2.26.0`<br>
- [arrangement](#arrangement)
- [spotify_id](#streaming_id)
- [spotify_id_bt](#streaming_id_bt)
- [spotify_id_any](#streaming_id_any)
- [youtube_id](#streaming_id)
- [youtube_id_bt](#streaming_id_bt)
- [youtube_id_any](#streaming_id_any)
- [deezer_id](#streaming_id)
- [deezer_id_bt](#streaming_id_bt)
- [deezer_id_any](#streaming_id_any)
- [linked_audio](#linked_audio)
- [linked_audio_bt](#linked_audio_bt)
- [linked_audio_any](#linked_audio_any)
- [saved_theme_by_id](#saved_theme_by_id)
- [saved_theme_by_name](#saved_theme_by_name)
- [played_hour](#played_hour)
- [played_day_of_week](#played_day_of_week)
- [played_month](#played_month)
- [played_year](#played_year)
- [played_service](#played_service)

Note: Some items allow the use of the translated name, for example, "título" instead of "title".

It is also possible to use an extra item created by the user as a key for the letters.


## String

String searches, for example:<br>
Songs that contain __"estou aqui"__ in the letter and contains some author with a name __"mat..."__<br>
```%lyrics: estou aqui && %author: mat```

It is possible to use the character `*` to filter when it contains any value or `!*` to filter when it does not contain a value, for example:<br>
Songs that contain __"estou aqui"__ and the __author__ field is filled in<br>
```%lyrics: estou aqui && %author: *```

Songs that contain __"estou aqui"__ and the __author__ field is not filled in<br>
```%lyrics: estou aqui && %author: !*```

## Regex

Searches using regex, add `--regex` or `--rgx` at the beginning of the searched field, for example:<br>
Songs that contain the word __"estou"__ or the word __"aqui"__ in the letter and contains some author with a name __"mat..."__<br>
```%lyrics: --rgx (estou|aqui) && %author: mat```

## Number

Research using numbers, for example:<br>
Songs with bpm greater than or equal to 80<br>
```%bpm: >= 80```

Songs with bpm from 90 to 120<br>
```%bpm: >= 90 && %bpm: <= 120```

Songs that were last played more than 90 days ago and have been played more than 5 times in total<br>
```%played_days: > 90 && %played_count: > 5```

Accepted types of comparison:<br>
`<=` less than or equal to<br>
`>=` greater than or equal to<br>
`<>` or `!=` different from <br>
`<` less than <br>
`>` greater than <br>

## Boolean

Research using true or false, for example: <br>
Songs that contain saved theme:<br>
```%saved_theme: true```

Allowed: `true` `false` `yes` `no`

--- 

### title

`string` `regex`<br>
Song title
```
%title: abc xyz
```
```
%title: --rgx (abc|xyz)
```

--- 

### artist

`string` `regex`<br>
Music artist
```
%artist: abc xyz
```
```
%artist: --rgx (abc|xyz)
```

--- 

### lyrics

`string` `regex`<br>
Song lyrics
```
%lyrics: abc xyz
```
```
%lyrics: --rgx (abc|xyz)
```

--- 

### note

`string` `regex`<br>
Music annotation
```
%note: abc xyz
```
```
%note: --rgx (abc|xyz)
```

--- 

### author

`string` `regex`<br>
Music author
```
%author: abc xyz
```
```
%author: --rgx (abc|xyz)
```

--- 

### group

`string`<br>
Filters only songs from the specified group.<br>
It is necessary to provide the full name of the group.<br>
Does not accept regex or partial search.
```
%group: abc
```

--- 

### comment

`string` `regex`<br>
Comments on the song lyrics
```
%comment: abc xyz
```
```
%comment: --rgx (abc|xyz)
```

--- 

### slide_description

`string` `regex`<br>
Filters only songs that contain at least one slide with the specified name.<br>
Accepts partial search using only regex.<br>
The simple string search needs to provide the full name of the description
```
%slide_description: chorus
```
```
%slide_description: --rgx (verse)
```

--- 

### translation

`string` `regex`<br>
Research in the translated fields of the song lyrics
```
%translation: abc xyz
```
```
%translation: --rgx (abc|xyz)
```

--- 

### bpm

`number`<br>
Filter songs using BPM
```
%bpm: <= 90
```
```
%bpm: = 80
```

--- 

### chord_key

`string`<br>
Filter songs using the key
```
%chord_key: Em
```
```
%chord_key: A
```

--- 

### time_sig

`string`<br>
Filter songs using the time
```
%time_sig: 4/4
```
```
%time_sig: 6/8
```

--- 

### extra

`string` `regex`<br>
"Extra" field available in the song lyrics editing window
```
%extra: abc xyz
```
```
%extra: --rgx (abc|xyz)
```

--- 

### order

`boolean`<br>
Filter songs that have or do not have the slide order defined manually
```
%order: true
```
```
%order: false
```

--- 

### saved_theme

`boolean`<br>
Filter songs that have or do not have a saved theme
```
%saved_theme: yes
```
```
%saved_theme: no
```

--- 

### played_days

`number`<br>
Filter songs based on the number of days since the last display of the lyrics.<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
%played_days: >= 90
```
```
%played_days: < 90
```

--- 

### played_count

`number`<br>
Filter songs based on the total number of times the song has been played.<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
%played_count: != 0
```
```
%played_count: > 5
```

--- 

### arrangement

`string` `regex`<br>
Filter songs that contain a specific arrangement (by name)<br>
```
%arrangement: abc
```
```
%arrangement: xyz
```
--- 

### streaming_id

`spotify_id`  `youtube_id`  `deezer_id`<br>
`string`<br>
Filter songs by the link saved in the 'extras' information of the song in the respective streaming<br>
The search is conducted only on items of type **"voice"**<br>
The search can be done by providing only the **id** or the complete link<br>
```
%spotify_id: abc
```
```
%youtube_id: xyz
```
--- 

### streaming_id_bt

`spotify_id_bt`  `youtube_id_bt`  `deezer_id_bt`<br>
`string`<br>
Filter songs by the link saved in the 'extras' information of the song in the respective streaming<br>
The search is conducted only on items of type **"playback"**<br>
The search can be done by providing only the **id** or the complete link<br>
```
%spotify_id_bt: abc
```
```
%youtube_id_bt: xyz
```
--- 

### streaming_id_any

`spotify_id_any`  `youtube_id_any`  `deezer_id_any`<br>
`string`<br>
Filter songs by the link saved in the 'extras' information of the song in the respective streaming<br>
The search is made in items of type **"voice"** and **"playback"**<br>
The search can be done by providing only the **id** or the complete link<br>
```
%spotify_id_any: abc
```
```
%youtube_id_any: xyz
```
--- 

### linked_audio

`string` `regex`<br>
Filter songs by the name of the associated audio file in the song's 'extras' information<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
```
---

### linked_audio_bt

`string` `regex`<br>
Filter songs by the name of the associated audio file in the song's 'extras' information<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
```
--- 

### linked_audio_any

`string` `regex`<br>
Filter songs by the name of the associated audio file in the song's 'extras' information<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
```
--- 

### saved_theme_by_id

`string`<br>
Filter items by the **id** of the theme saved as **default theme** in the respective item<br>
```
%saved_theme_by_id: 1234
```
--- 

### saved_theme_by_name

`string` `regex`<br>
Filter items by the **name** of the theme saved as **default theme** in the respective item<br>
```
%saved_theme_by_name: abc
```
```
%saved_theme_by_name: xyz
```
--- 

### played_hour

`string`<br>
Filter songs by the number of times they were played in a specific hour of the day.<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
//was played more than 10 times at 7 PM
%played_hour: 19 > 10
```
```
//was played less than 10 times during the hours of 7 PM, 8 PM, 9 PM, and 10 PM
%played_hour: 19,20,21,22 <= 10
```
```
//was played less than 10 times in the interval of 7 PM, 8 PM, 9 PM, and 10 PM
%played_hour: 19-22
```
--- 

### played_day_of_week

`string`<br>
Filter songs by the number of times they were played on a specific day of the week.<br>
`sun` `mon` `tue` `wed` `thu` `fri` `sat`
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
//was played more than 20 times on Sunday
%played_day_of_week: sun > 20
```
```
//was played 20 times or less including Saturday and Sunday
%played_day_of_week: sat,sun <= 20
```
--- 

### played_month

`string`<br>
Filter songs by the number of times they were played in a month of the year.<br>
`1 ~ 12`<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
//was played less than 5 times in January
%played_month: 1 < 5
```
```
//was played 5 times or more counting March, April, or May
%played_month: 3,4,5 >= 5
```
```
//was played 5 times or more counting March, April, or May
%played_month: 3-5
```
--- 

### played_year

`string`<br>
Filter songs by the number of times they were played in a specific year.<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
//was played more than 10 times in 2023
%played_year: 2023 > 10
```
```
//was played 10 times or less counting 2023, 2024, and 2025
%played_year: 2023,2024,2025 <= 10
```
```
//was played 10 times or less counting 2023, 2024, and 2025
%played_year: 2023-2025
```
--- 

### played_service

`string`<br>
Filter songs by the number of times they have been played in a specific service (by the name of the service).<br>
The "history" field is used as a basis, meaning that only the displays of the option "marked as played" are considered.
```
//was played more than 20 times during the respective service time
%played_service: name of the worship > 20
```
```
//was played 10 times or less during the respective service time
%played_service: name of the worship <= 10
```