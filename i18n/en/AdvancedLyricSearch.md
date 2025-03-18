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
%title: chorus
```
```
%title: --rgx (verse)
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