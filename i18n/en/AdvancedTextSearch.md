# Advanced Text Search

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/AdvancedTextSearch.md)

---

`v2.26.0+`

It is possible to perform an advanced search in the text tab for a more precise filter of items, using items not available in the interface and filtering by different items simultaneously.

Search syntax:

```
%key: value   &&   %key: < value   &&   %key: value
```

Use "percentage" at the beginning of the key and a colon at the end of the key.<br>
Next, please provide the value you wish to search for.

To use multiple keys, use the "&&" sign to separate the items.

Available items:<br>
- [title](#title)
- [content](#content)
- [comment](#comment)
- [translation](#translation)
- [extra](#extra)
- [saved_theme](#saved_theme)
- [saved_theme_by_id](#saved_theme_by_id)
- [saved_theme_by_name](#saved_theme_by_name)

It is also possible to use an extra item created by the user as a key for the letters.


## String

String searches, for example:<br>
Texts that contain __"estou aqui"__ in the text and the saved theme contains __"abc..."__<br>
```%content: estou aqui && %saved_theme_by_name: abc```

It is possible to use the character `*` to filter when it contains any value or `!*` to filter when it does not contain a value, for example:<br>
Texts that contain __"estou aqui"__ and the field __saved_theme_by_name__ is filled in<br>
```%content: estou aqui && %saved_theme_by_name: *```

Texts that contain __"estou aqui"__ and the field __saved_theme_by_name__ is not filled in<br>
```%content: estou aqui && %saved_theme_by_name: !*```

## Regex

Searches using regex, add `--regex` or `--rgx` at the beginning of the searched field, for example:<br>
Texts that contain the word __"estou"__ or the word __"aqui"__ in the text and contains some saved theme with name __"abc..."__<br>
```%content: --rgx (estou|aqui) && %saved_theme_by_name: abc```

## Boolean

Research using true or false, for example: <br>
Texts that contain saved theme:<br>
```%saved_theme: true```

Allowed: `true` `false` `yes` `no`

--- 

### title

`string` `regex`<br>
Title of the Text
```
%title: abc xyz
```
```
%title: --rgx (abc|xyz)
```

--- 

### content

`string` `regex`<br>
Item content Text
```
%content: abc xyz
```
```
%content: --rgx (abc|xyz)
```

--- 

### comment

`string` `regex`<br>
Comments in the paragraphs of the Text
```
%comment: abc xyz
```
```
%comment: --rgx (abc|xyz)
```

--- 

### translation

`string` `regex`<br>
Search in the translated fields of the item Text
```
%translation: abc xyz
```
```
%translation: --rgx (abc|xyz)
```

--- 

### extra

`string` `regex`<br>
"extra" field available in the edit window of a Text item
```
%extra: abc xyz
```
```
%extra: --rgx (abc|xyz)
```

--- 

### saved_theme

`boolean`<br>
Filter texts that have or do not have a saved theme
```
%saved_theme: yes
```
```
%saved_theme: no
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