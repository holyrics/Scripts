# Holyrics User Data API

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/UserDataAPI.md)

---


API para listar os arquivos e dados do programa Holyrics disponíveis no computador  (somente leitura)<br>
Disponível a partir da versão `2.30.0`

Tipos de itens disponíveis:<br>
| Tipo | Classe |
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


Essa API permite que apps de terceiros (como apps de gestão de voluntários, por exemplo) façam requisições para pesquisar um item diretamente na "base de dados" do usuário Holyrics.<br>
Permitindo, por exemplo, adicionar arquivos de áudio, vídeo, imagens, pastas, etc. que já estão no computador diretamente na ordem de culto do app de gestão.<br>

Observação: Essa API não disponibiliza acesso direto aos arquivos (áudio, vídeo e imagens), apenas a listagem e informações do arquivo, e também uma imagem preview para itens compatíveis, como imagens, vídeos, temas, etc.<br>
A disponibilização de acesso ao arquivo pode ser implementada futuramente, mas por enquanto não há previsão.

---

## Request
Todas as respostas da API retornam um objeto padrão:
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `status` | _String_ | Pode ser *'ok'* ou *'error'* |
| `error` | _String (opcional)_ | Mensagem de erro se *status* for igual a *error* |
| `result` | _Object (opcional)_ | Conteúdo da resposta se *status* for igual a *ok* |

Endpoint padrão
```
https://userdata.holyrics.com.br/v1/
```

Autenticação (header)
```
'Authorization: Bearer {API_TOKEN}'
```

# Endpoints disponíveis 
  - [{type}/{id}](#typeid)
  - [{type}/list](#typelist)
  - [{type}/search](#typesearch)


---

### {type}/{id}
Retorna o respectivo item pelo ID.<br>
Tipos disponíveis: `song` `text` `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`



**Resposta:**

| Tipo  | Descrição |
| :---: | ------------|
| _Object_ | Objeto da classe correspondente ao tipo do item |


**Exemplo:** [` userdata.holyrics.com.br/v1/text/31ca678b-6ad6-4ad7-ba48-ba409bc6c783 `](https://userdata.holyrics.com.br/v1/text/31ca678b-6ad6-4ad7-ba48-ba409bc6c783)<br>

<details>
  <summary>Resposta</summary>

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
Lista os itens disponíveis para o respectivo tipo.<br>
Tipos disponíveis: `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| <br>**Disponível para os tipos:** `audio` `video` `image` `file` |  |  |
| `folder` | _String (opcional)_ | Se o parâmetro `folder` for declarado, serão listados apenas os itens a partir dessa pasta.<br>Caso não seja declarado, a pasta raiz será utilizada como base.<br>Para uma subpasta, basta informar o respectivo caminho com a barra separadora, por exemplo: `folder/subfolder` |
| `is_folder` | _Boolean (opcional)_ | Se o parâmetro `is_folder` for declarado, serão listados apenas os itens que são pasta (`is_folder=true`) ou apenas os itens que são arquivo (`is_folder=false`) |
| `recursive` | _Boolean (opcional)_ | Se `recursive=true`, então serão listados também os itens das subpastas `Padrão: false` |


**Resposta:**

| Tipo  | Descrição |
| :---: | ------------|
| _Array&lt;Object&gt;_ | Array de objetos da classe correspondente ao tipo do item |


**Exemplo:** [` userdata.holyrics.com.br/v1/image/search?folder=example `](https://userdata.holyrics.com.br/v1/image/search?folder=example)<br>

<details>
  <summary>Resposta</summary>

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
Pesquisa os itens disponíveis para o respectivo tipo.<br>
Limite: 30 resultados<br>
Tipos disponíveis: `song` `text` `audio` `video` `image` `file` `announcement` `automatic_presentation` `theme` `background`

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `q` | _String_ | Texto a ser pesquisado. |
| <br>**Disponível para os tipos:** `audio` `video` `image` `file` |  |  |
| `folder` | _String (opcional)_ | Se o parâmetro `folder` for declarado, serão listados apenas os itens a partir dessa pasta.<br>Caso não seja declarado, a pasta raiz será utilizada como base.<br>Para uma subpasta, basta informar o respectivo caminho com a barra separadora, por exemplo: `folder/subfolder` |
| `is_folder` | _Boolean (opcional)_ | Se o parâmetro `is_folder` for declarado, serão listados apenas os itens que são pasta (`is_folder=true`) ou apenas os itens que são arquivo (`is_folder=false`) |
| `recursive` | _Boolean (opcional)_ | Se `recursive=true`, então serão listados também os itens das subpastas `Padrão: false` |


**Resposta:**

| Tipo  | Descrição |
| :---: | ------------|
| _Array&lt;Object&gt;_ | Array de objetos da classe correspondente ao tipo do item |


**Exemplo:** [` userdata.holyrics.com.br/v1/song/search?q=example `](https://userdata.holyrics.com.br/v1/song/search?q=example)<br>

<details>
  <summary>Resposta</summary>

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
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID da música |
| `title` | _String_ | Título da música |
| `artist` | _String_ | Artista da música |
| `author` | _String_ | Autor da música |
| `note` | _String_ | Anotação da música |
| `copyright` | _String_ | Copyright da música |
| `slides` | _Array&lt;Object&gt;_ | **O parâmetro `slides` não está disponível nos endpoints `/list` e `/search`** |
| `slides.*.text` | _String_ | Texto do slide |
| `slides.*.styled_text` | _String_ | Texto do slide com formatação **styled** (quando disponível) |
| `slides.*.slide_description` | _String_ | Descrição do slide |
| `slides.*.background_id` | _String_ | ID do tema ou plano de fundo salvo para o slide |
| `slides.*.translations` | _Object_ | Traduções para o slide.<br>Conjunto chave/valor. |
| `order` | _String_ | Ordem dos slides (índice a partir do 1), separado por vírgula |
| `title_translations` | _Object_ | Traduções para o slide título.<br>Conjunto chave/valor. |
| `key` | _String_ | Tom da música.<br>Pode ser: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number_ | BPM da música |
| `time_sig` | _String_ | Tempo da música.<br>Pode ser: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `linked_audio_file` | _String_ | Caminho do arquivo de áudio linkado com a música |
| `linked_backing_track_file` | _String_ | Caminho do arquivo de áudio (playback) linkado com a música |
| `streaming` | _Object_ | URI ou ID dos streamings |
| `streaming.audio` | _Object_ | Áudio |
| `streaming.audio.spotify` | _String_ |  |
| `streaming.audio.youtube` | _String_ |  |
| `streaming.audio.deezer` | _String_ |  |
| `streaming.audio.apple_music` | _String_ |  |
| `streaming.audio.amazon_music` | _String_ |  |
| `streaming.backing_track` | _Object_ | Playback |
| `streaming.backing_track.spotify` | _String_ |  |
| `streaming.backing_track.youtube` | _String_ |  |
| `streaming.backing_track.deezer` | _String_ |  |
| `streaming.backing_track.apple_music` | _String_ |  |
| `streaming.backing_track.amazon_music` | _String_ |  |
| `extras` | _Object_ | Mapa de objetos extras (adicionados pelo usuário) |
| `theme` | _String_ | ID do tema salvo para a música |
| `archived` | _Boolean_ | Se a música está arquivada |
| `tags` | _Array&lt;String&gt;_ |  |
| `metadata.modified_time_millis` | _Number_ | Data de modificação do arquivo. (timestamp) `read-only` |

## Text
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do texto |
| `title` | _String_ | Título do texto |
| `folder` | _String_ | Caminho da pasta de localização |
| `theme` | _String_ | ID do tema salvo para o texto |
| `slides` | _Array&lt;Object&gt;_ | **O parâmetro `slides` não está disponível nos endpoints `/list` e `/search`** |
| `slides.*.text` | _String_ | Texto do slide |
| `slides.*.styled_text` | _String_ | Texto do slide com formatação **styled** (quanto disponível) |
| `slides.*.background_id` | _String_ | ID do tema ou plano de fundo salvo para o slide |
| `slides.*.translations` | _Object_ | Traduções para o slide.<br>Conjunto chave/valor. |
| `formatting_type` | _String_ | `basic`  `styled`  `advanced`<br> <br>Ao utilizar este objeto em métodos de criação ou edição, se `formatting_type=basic` for utilizado, o valor da variável `slides.*.text` será utilizado, caso contrário, o valor da variável `slides.*.styled_text` será utilizado `Padrão: basic` |
| `extras` | _Object_ | Mapa de objetos extras (adicionados pelo usuário) |
| `tags` | _Array&lt;String&gt;_ |  |
| `metadata.modified_time_millis` | _Number_ | Data de modificação do arquivo. (timestamp) `read-only` |

## Audio
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome completo do item, incluindo pasta, caso esteja dentro de pastas e subpastas |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Quantidade de itens dentro da respectiva pasta `(disponível somente para pastas)` |
| `length` | _Number_ | Tamanho do arquivo (em bytes) `(disponível somente para arquivos)` |
| `duration_millis` | _Number_ | Duração da mídia em milissegundos |

## Video
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome completo do item, incluindo pasta, caso esteja dentro de pastas e subpastas |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Quantidade de itens dentro da respectiva pasta `(disponível somente para pastas)` |
| `length` | _Number_ | Tamanho do arquivo (em bytes) `(disponível somente para arquivos)` |
| `duration_millis` | _Number_ | Duração da mídia em milissegundos |
| `width` | _Number_ | Largura `px` |
| `height` | _Number_ | Altura `px` |
| `preview_url` | _String_ | URL da imagem preview do respectivo item. Resolução Máxima: `1280x720` |
| `thumbnail_url` | _String_ | URL da imagem miniatura do respectivo item. Resolução Máxima: `320x180` |

## Image
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome completo do item, incluindo pasta, caso esteja dentro de pastas e subpastas |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Quantidade de itens dentro da respectiva pasta `(disponível somente para pastas)` |
| `length` | _Number_ | Tamanho do arquivo (em bytes) `(disponível somente para arquivos)` |
| `width` | _Number_ | Largura `px` |
| `height` | _Number_ | Altura `px` |
| `preview_url` | _String_ | URL da imagem preview do respectivo item. Resolução Máxima: `1280x720` |
| `thumbnail_url` | _String_ | URL da imagem miniatura do respectivo item. Resolução Máxima: `320x180` |

## File
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome completo do item, incluindo pasta, caso esteja dentro de pastas e subpastas |
| `is_folder` | _Boolean_ |  |
| `item_count` | _Number_ | Quantidade de itens dentro da respectiva pasta `(disponível somente para pastas)` |
| `length` | _Number_ | Tamanho do arquivo (em bytes) `(disponível somente para arquivos)` |

## Announcement
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome do item |
| `text` | _String_ | Texto do anúncio |
| `shuffle` | _Boolean_ | Exibir a lista de anúncios de forma aleatória |
| `archived` | _Boolean_ | Se o item está arquivado |
| `preview_url` | _String_ | URL da imagem preview do respectivo item. Resolução Máxima: `1280x720` |
| `thumbnail_url` | _String_ | URL da imagem miniatura do respectivo item. Resolução Máxima: `320x180` |

## AutomaticPresentation
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome do item |
| `duration` | _Number_ | Duração em milissegundos |

## Theme
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `name` | _String_ | Nome do item |
| <br>**background** |  | <br>Plano de fundo |
| `background.type` | _String_ | Tipo do plano de fundo. Pode ser: `color`  `my_video`  `my_image`  `video`  `image`  `pattern`  `transparent`  `image_file`  `video_file` |
| `background.id` | _String_ | <table><tr><td><p align="right">**Tipo**</p></td><td>Valor</td></tr><tr><td><p align="right">color</p></td><td>Cor no formato hexadecimal</td></tr><tr><td><p align="right">my_video</p></td><td>ID do item</td></tr><tr><td><p align="right">my_image</p></td><td>ID do item</td></tr><tr><td><p align="right">video</p></td><td>ID do item</td></tr><tr><td><p align="right">image</p></td><td>ID do item</td></tr><tr><td><p align="right">pattern</p></td><td>ID do item</td></tr><tr><td><p align="right">transparent</p></td><td>"transparent"</td></tr><tr><td><p align="right">image_file</p></td><td>Nome do arquivo na biblioteca</td></tr><tr><td><p align="right">video_file</p></td><td>Nome do arquivo na biblioteca</td></tr></table> |
| `background.adjust_type` | _String_ | `fill` `extend` `adjust` `side_by_side` `center`<br>Disponível para: **type=my_image**, **type=image** |
| `background.opacity` | _Number_ | Opacidade. `0 ~ 100` |
| `background.velocity` | _Number_ | Disponível para: **type=my_video**, **type=video**<br>`0.25 ~ 4.0` |
| `base_color` | _String_ | Cor no formato hexadecimal. Cor base do plano de fundo ao diminuir a opacidade. |
| <br>**font** |  | <br>Fonte |
| `font.name` | _String_ | Nome da fonte |
| `font.bold` | _Boolean_ | Negrito |
| `font.italic` | _Boolean_ | Itálico |
| `font.size` | _Number_ | Tamanho `0 ~ 50`<br>Valor em porcentagem, baseado na altura do slide. |
| `font.color` | _String_ | Cor no formato hexadecimal |
| `font.line_spacing` | _Number_ | Espaçamento entre linhas. `-0.5 ~ 1.0`<br>Valor em porcentagem baseado na altura da linha. |
| `font.char_spacing` | _Number_ | Espaçamento entre caracteres. `-40 ~ 120` |
| <br>**align** |  | <br>Alinhamento |
| `align.horizontal` | _String_ | `left`  `center`  `right`  `justify` |
| `align.vertical` | _String_ | `top`  `middle`  `bottom` |
| `align.margin.top` | _Number_ | `0 ~ 90` |
| `align.margin.right` | _Number_ | `0 ~ 90` |
| `align.margin.bottom` | _Number_ | `0 ~ 90` |
| `align.margin.left` | _Number_ | `0 ~ 90` |
| <br>**effect** |  | <br>Efeitos da fonte |
| `effect.outline_color` | _String_ | Cor no formato hexadecimal |
| `effect.outline_weight` | _Number_ | `0.0 ~ 100.0` |
| `effect.brightness_color` | _String_ | Cor no formato hexadecimal |
| `effect.brightness_weight` | _Number_ | `0.0 ~ 100.0` |
| `effect.shadow_color` | _String_ | Cor no formato hexadecimal |
| `effect.shadow_x_weight` | _Number_ | `-100.0 ~ 100.0` |
| `effect.shadow_y_weight` | _Number_ | `-100.0 ~ 100.0` |
| `effect.blur` | _Boolean_ | Aplicar efeito 'blur' no brilho e sombra |
| <br>**shape_fill** |  | <br>Cor de fundo |
| `shape_fill.type` | _String_ | `box`  `line`  `line_fill`  `theme_margin` |
| `shape_fill.enabled` | _Boolean_ |  |
| `shape_fill.color` | _String_ | Cor no formato hexadecimal (RGBA) |
| `shape_fill.margin.top` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.right` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.bottom` | _Number_ | `0 ~ 100` |
| `shape_fill.margin.left` | _Number_ | `0 ~ 100` |
| `shape_fill.corner` | _Number_ | `0 ~ 100` |
| <br>**shape_outline** |  | <br>Contorno |
| `shape_outline.type` | _String_ | `box`  `line`  `line_fill`  `theme_margin` |
| `shape_outline.enabled` | _Boolean_ |  |
| `shape_outline.color` | _String_ | Cor no formato hexadecimal (RGBA) |
| `shape_outline.outline_thickness` | _Number_ | `0 ~ 25` |
| `shape_outline.margin.top` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.right` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.bottom` | _Number_ | `0 ~ 100` |
| `shape_outline.margin.left` | _Number_ | `0 ~ 100` |
| `shape_outline.corner` | _Number_ | `0 ~ 100` |
| <br>**comment** |  | <br>Comentário |
| `comment.font_name` | _String_ | Nome da fonte |
| `comment.bold` | _Boolean_ | Negrito |
| `comment.italic` | _Boolean_ | Itálico |
| `comment.relative_size` | _Number_ | tamanho relativo da fonte. `40 ~ 100` |
| `comment.color` | _String_ | Cor no formato hexadecimal |
| <br>**settings** |  | <br>Configurações |
| `settings.uppercase` | _Boolean_ | Exibir o texto em maiúsculo |
| `settings.line_break` | _String_ | Aplicar quebra de linha. `system`  `true`  `false`<br> `Padrão: system` |
| <br>**metadata** |  | <br> |
| `metadata.modified_time_millis` | _Number_ | Data de modificação do arquivo. (timestamp) `read-only` |
| `preview_url` | _String_ | URL da imagem preview do respectivo item. Resolução Máxima: `1280x720` |
| `thumbnail_url` | _String_ | URL da imagem miniatura do respectivo item. Resolução Máxima: `320x180` |

## Background
| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `id` | _String_ | ID do item |
| `type` | _String_ | Tipo do item. Pode ser: `theme` `my_video` `my_image` `video` `image` |
| `name` | _String_ | Nome do item |
| `width` | _Number (opcional)_ |  |
| `height` | _Number (opcional)_ |  |
| `duration` | _Number (opcional)_ | Duração em milissegundos |
| `tags` | _Array&lt;String&gt;_ | Lista de tags do item |
| `bpm` | _Number_ | Valor BPM do item |
| `preview_url` | _String_ | URL da imagem preview do respectivo item. Resolução Máxima: `1280x720` |
| `thumbnail_url` | _String_ | URL da imagem miniatura do respectivo item. Resolução Máxima: `320x180` |