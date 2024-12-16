# API Popup Create Song

Opção via API para criar uma nova música abrindo a janela de edição de letra. (v2.21.0+)

Isso permite que qualquer outro processo no computador possa enviar um conteúdo ao programa para abrir a janela de edição de letra.

```
curl -X 'POST' \
  'http://localhost:8091/api/popup-createsong' \
  -H 'Content-Type: application/json' \
  -d '{ "title": "...", "author": "...", "artist": "...", "lyrics": "..." }'
```

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `title` | _String_ | Título da música |
| `lyrics` | _String_ | Letra da música.<br>Opcional se `paragraphs` for declarado |
| `paragraphs` | _Array&lt;Object&gt;_ | Parâmetro alternativo para valores mais complexos.<br>Opcional se `lyrics` for declarado `v2.23.0+` |
| `paragraphs.*.text` | _String_ | Texto do parágrafo `v2.23.0+` |
| `paragraphs.*.description` | _String (opcional)_ | Descrição do parágrafo. coro, verso, ... `v2.23.0+` |
| `paragraphs.*.translations` | _Object (opcional)_ | Traduções para o slide.<br>Conjunto chave/valor. `v2.23.0+` |
| `author` | _String (opcional)_ | Autor da música |
| `artist` | _String (opcional)_ | Artista da música |
| `copyright` | _String (opcional)_ | Copyright da música `v2.23.0+` |
| `note` | _String (opcional)_ | Anotação da música |
| `key` | _String (opcional)_ | Tom da música.<br>Pode ser: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number (opcional)_ | BPM da música |
| `time_sig` | _String (opcional)_ | Tempo da música.<br>Pode ser: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `streaming` | _Object_ | URI ou ID dos streamings `v2.23.0+` |
| `streaming.audio` | _Object_ | Áudio `v2.23.0+` |
| `streaming.audio.spotify` | _String_ |  `v2.23.0+` |
| `streaming.audio.youtube` | _String_ |  `v2.23.0+` |
| `streaming.audio.deezer` | _String_ |  `v2.23.0+` |
| `streaming.backing_track` | _Object_ | Playback `v2.23.0+` |
| `streaming.backing_track.spotify` | _String_ |  `v2.23.0+` |
| `streaming.backing_track.youtube` | _String_ |  `v2.23.0+` |
| `streaming.backing_track.deezer` | _String_ |  `v2.23.0+` |
| `extras` | _Object (opcional)_ | Mapa de objetos extras (adicionados pelo usuário)<br>Permitido apenas campos já existentes. `v2.23.0+` |
| `title_translations` | _Object_ | Traduções para o slide título.<br>Conjunto chave/valor. `v2.23.0+` |


Observações:<br>
- Disponível a partir da versão 2.21.0;
- É necessário que a opção "API Server" esteja ativada nas configurações do programa;
- Aceita somente requisições da máquina local utilizando endereço loopback;
- Caso tenha sido modificada, altere a porta 8091 da requisição para a porta correspondente definida nas configurações API Server.

Modelo JSON simples
```json
{
  "title": "title",
  "lyrics": "Slide 1\nSlide 1\n\nSlide 2\nSlide 2",
  "artist": "artist",
  "author": "author",
  "copyright": "copyright",
}
```

Modelo JSON complexo
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
