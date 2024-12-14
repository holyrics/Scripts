# ContextAction

`menu ferramentas > diversos > ações de contexto`

Cria itens no menu de contexto (botão direito do mouse) de um respectivo item, permitindo realizar ações específicas para um item.<br>
Por exemplo, criar uma ação chamada `Sem Áudio` que executa um vídeo sem áudio.<br>
Ao clicar com o botão direito em um item de vídeo no programa, no submenu `Ação de contexto`, selecionando o item `Sem Áudio`, as informações do vídeo serão redirecionadas para a respectiva `function`.<br>
E então a function pode ter a implementação de definir o player do programa para `mute = true` e depois executar o respectivo vídeo.


O parâmetro `obj.type` contém o tipo do item que gerou a ação.<br>
O parâmetro `obj.item` contém as informações do respectivo item que gerou a ação.

## Exemplo

```javascript
function scriptAction(obj) {
    if (obj.type == 'video') {
        h.getPlayer().setMute(true);
        h.playVideo(obj.item.file_fullname);
    }
}
```

## audio
```json
{
  "file_name": "file name.mp3",
  "file_fullname": "file name.mp3",
  "file_relative_path": "audio\\file name.mp3",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\audio\\file name.mp3",
  "is_dir": false,
  "extension": "mp3",
  "properties": {}
}
```

## audio_folder
```json
{
  "file_name": "folder name",
  "file_fullname": "folder name",
  "file_relative_path": "audio\\folder name",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\audio\\folder name",
  "is_dir": true,
  "extension": "",
  "properties": {}
}
```

## video
```json
{
  "file_name": "file name.mp4",
  "file_fullname": "file name.mp4",
  "file_relative_path": "video\\file name.mp4",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\video\\file name.mp4",
  "is_dir": false,
  "extension": "mp4",
  "properties": {}
}
```

## video_folder
```json
{
  "file_name": "folder name",
  "file_fullname": "folder name",
  "file_relative_path": "video\\folder name",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\video\\folder name",
  "is_dir": true,
  "extension": "",
  "properties": {}
}
```

## image
```json
{
  "file_name": "file name.jpg",
  "file_fullname": "file name.jpg",
  "file_relative_path": "image\\file name.jpg",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\image\\file name.jpg",
  "is_dir": false,
  "extension": "jpg",
  "properties": {}
}
```

## image_folder
```json
{
  "file_name": "folder name",
  "file_fullname": "folder name",
  "file_relative_path": "image\\folder name",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\image\\folder name",
  "is_dir": true,
  "extension": "",
  "properties": {}
}
```

## file
```json
{
  "file_name": "file name.txt",
  "file_fullname": "file name.txt",
  "file_relative_path": "file\\file name.txt",
  "file_path": "C:\\Holyrics\\Holyrics\\files\\media\\file\\file name.txt",
  "is_dir": false,
  "extension": "txt",
  "properties": {}
}
```

## song
```json
{
  "id": 12345,
  "title": "title",
  "artist": "artist",
  "author": "author",
  "note": "note",
  "copyright": "copyright",
  "key": "",
  "bpm": 0.0,
  "time_sig": "",
  "extra": ""
}
```

## text
```json
{
  "id": "c0598eab-00b0-4e36-b7bc-82d9b1978e24",
  "title": "title"
}
```

## announcement
```json
{
  "id": 1734201631915,
  "name": "Announcement"
}
```

## automatic_presentation
```json
{
  "name": "name.ap"
}
```

## plain_text
```json
{
  "title": "title",
  "description": "Text, actually"
}
```

## cp_text
```json
{
  "title": "title",
  "description": "Text, actually"
}
```

---

# Available only for modules
## favorite
```json
{
  "id": "zdBNPrwV7g3V7",
  "type": "favorite",
  "name": "favorite name",
  "item": {
    "id": "zdBNPrwV7g3V7",
    "type": "image",
    "name": "file name.jpg",
    "isDir": false,
    "properties": {}
  }
}
```

## paragraph_preview
```json
{
  "id": "12345",
  "type": "song",
  "text": "Chorus\nChorus",
  "slide_type": "default",
  "slide_number": 2,
  "total_slides": 3,
  "slide_description": "Chorus"
}
```

## song_history
```json
{
  "song_id": "12345",
  "date": "2024-08-28 12:00"
}
```

## theme
```json
{
  "id": "12345",
  "type": "theme",
  "name": "Theme name",
  "tags": [],
  "bpm": 0.0
}
```

## presentation_theme_footer
```json
{
  "id": "12345",
  "type": "my_video",
  "name": "name",
  "tags": [],
  "bpm": 0.0
}
```

## playlist_item
```json
{
  "item": {
    "id": "zdBNPrwV7g3V7",
    "type": "image",
    "name": "file name.jpg",
    "isDir": false,
    "properties": {}
  },
  "playlist": {
    "type": "temporary",
    "name": "Temporário",
    "datetime": "2024-08-28 12:00",
    "datetime_millis": "1734201632207"
  }
}
```

## song_playlist_item
```json
{
  "item": {
    "id": "zjrcbHzFKCxyc",
    "type": "song",
    "name": "title (artist)",
    "song_id": "12345",
    "reference_id": "12345"
  },
  "playlist": {
    "type": "temporary",
    "name": "Temporário",
    "datetime": "2024-12-14 15:40",
    "datetime_millis": "1734201632209"
  }
}
```

## chat_message
```json
{
  "id": "1734201632211",
  "datetime": 1734201632211,
  "user_id": "-1qfe9t8wtrsb6p5",
  "name": "example",
  "message": "example"
}
```


