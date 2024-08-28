# TextTransform

`menu arquivo > configurações > diversos > inserir texto`

Permite inserir um texto no início ou no final de um slide ou alterar o texto atual.<br>
Esta ação é feita em tempo de execução no momento da projeção do respectivo slide e é aplicada de forma independente para cada tela, de acordo com o valor em `screen_id`.<br>
Observação: há um cachê de 30 segundo para reutilizar o último valor retornado pela function, baseado no mesmo slide e mesma tela.

O parâmetro `obj` é do tipo [TextTransformInfo](#texttransforminfo)

## Exemplo

```javascript
function getData(obj) {
    return {
         /* ${{opcional}} */
         //Valor que será adicionado no início do texto do slide atual
         add_start: "", // (string)
         //
         /* ${{opcional}} */
         //Valor que será adicionado no final do texto do slide atual
         add_end: "", // (string)
         //
         /* ${{opcional}} */
         //Adiciona o texto com uma quebra de linha (default: true)
         line_break: true, // (boolean)
         //
         /* ${{opcional}} */
         //Valor para substituir o texto do slide atual
         replace: "" // (string)
    }
}
```

```javascript
// EXTRA SLIDE
function getData(obj) {
    if (obj.screen_id == 'public' && obj.slide_type == 'blank') {
        // Isso faz com que na tela 'public'
        // quando a opção F9 (sem texto) estiver ativada
        // o texto '♪' será exibido
        return {
            add_end: '♪'
        };
    }
    return null;
}
```

## TextTransformInfo
Contém as informações da origem da requisição

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `screen_id` | _String_ | `public` `screen_2` `screen_3` `screen_?` `stream_image` `stream_html_1` `stream_html_2` `stream_html_3` |
| `source_type` | _String_ | `music` `text` `unknown` |
| `source_id` | _String_ |  |
| `slide_type` | _String_ | `default` `final_slide` `wallpaper` `blank` `black` |
| `text` | _String_ | Texto do slide |
| `slide_number` | _Number_ | Disponível se `source_type = music` ou `source_type = text`.<br>Número do slide. Começa em 1. |
| `total_slides` | _Number_ | Disponível se `source_type = music` ou `source_type = text`.<br>Total de slides. |
| `stage_view_enabled` | _Boolean_ | Verifica se a tela está com a opção **Visão do Palco** ativada |
| `stage_view_preview_mode` | _String_ | Disponível se `stage_view_enabled = true`<br>`CURRENT_SLIDE`<br>`FIRST_LINE_OF_THE_NEXT_SLIDE_WITH_SEPARATOR`<br>`FIRST_LINE_OF_THE_NEXT_SLIDE_WITHOUT_SEPARATOR`<br>`NEXT_SLIDE`<br>`CURRENT_AND_NEXT_SLIDE`<br>`ALL_SLIDES` |
| `stage_view_show_comment` | _Boolean_ | Disponível se `stage_view_enabled = true` |
| `stage_view_show_communication_panel` | _Boolean_ | Disponível se `stage_view_enabled = true` |
| <br>Disponível se **source_type=music** |  |  |
| `title` | _String_ | Título da música |
| `artist` | _String_ | Artista da música |
| `author` | _String_ | Autor da música |
| `note` | _String_ | Anotação da música |
| `copyright` | _String_ | Copyright da música |
| `key` | _String_ | Tom da música.<br>Pode ser: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number_ | BPM da música |
| `time_sig` | _String_ | Tempo da música.<br>Pode ser: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |
| `slide_description` | _String_ |  |
| <br>Disponível se **source_type=text** |  |  |
| `title` | _String_ | Título do texto |
