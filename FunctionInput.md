# Function Input

É possível definir `inputs` (parâmetros) personalizados para a execução de um código javascript.<br>
Dessa forma é possível criar modelos de código genéricos que serão executados conforme parâmetros informados na interface.

As variáveis são passadas no objeto `obj.input` na execução do código.<br>
Criando 3 inputs com os IDs `name`, `duration` e `flag`, esses valores podem ser acessados conforme exemplo abaixo:<br>
```javascript
function example(obj) {
    obj.input.text;
    obj.input.duration;
    obj.input.repeat;
}
```

Para criar `inputs`, implemente o método `hGetItemInputParams` na parte de métodos opcionais, na parte direita da janela de edição de script, exemplo:<br>

```javascript
function hGetItemInputParams() {
  return [
    {
      id: 'text',
      name: 'Texto'
    },{
      id: 'duration',
      name: 'Duração',
      type: 'number'
    }, {
      id: 'repeat',
      name: 'Repetir',
      type: 'boolean'
    }
  ];
}
```

# Syntax

Parâmetros que cada `input` pode conter:<br>
__id__ `string` _(obrigatório)_<br>
Nome da variável

__name__ `string`<br>
Nome para exibir na interface<br>
Valor padrão: `Nome da variável`

__type__ `string`<br>
Tipo de parâmetro. Isso define o tipo de componente exibido na interface para definir valores.<br>
Por exemplo, tipo boolean irá exibir um `checkbox`.<br>
Tipos disponíveis: `title`  `separator`  `label (v2.22.0+)`  `string`  `textarea`  `number`  `boolean`  `password`  `date`  `time`  `datetime`  `color`  `receiver`  `song`  `holyrics_text`  `verse`  `audio`  `video`  `image`  `file`  `announcement`  `automatic_presentation`  `countdown`  `countdown_cp`  `cp_text`  `background`  `theme`  `button (v2.22.0+)`<br>
Valor padrão: `string`

__description__ `string`<br>
Informa uma descrição para o parâmetro, para poder ser exibido na tela como "ajuda".<br>
Valor padrão: `vazio`

__default_value__ `object`<br>
Define um valor inicial para o parâmetro.<br>
Valor padrão: `vazio | false | 0 | null`

### _Disponível apenas para tipo 'string'_<br>
__suggested_values__ `array or function`<br>
Exibe uma lista de sugestões ao clicar na "setinha" disponível na caixa de texto, mas permite que qualquer valor seja digitado na caixa de texto.<br>
É possível retornar uma `function` para que os valores possam ser atualizados em tempo real.<br>
Permite, por exemplo, exibir uma lista de valores sugeridos baseado no valor dos inputs anteriores.<br>
Valor padrão: `null`

__allowed_values__ `array or function`<br>
Exibe uma lista de opções no formato `combobox`, sem opção para inserir outros valores.<br>
É possível retornar uma `function` para que os valores possam ser atualizados em tempo real.<br>
Permite, por exemplo, exibir uma lista de valores sugeridos baseado no valor dos inputs anteriores.<br>
Valor padrão: `null`

### _Disponível apenas para tipo 'number'_<br>
__min__ `number`<br>
Valor mínimo permitido.<br>
Valor padrão: `0`

__max__ `number`<br>
Valor máximo permitido.<br>
Valor padrão: `100`

__show_as_combobox__ `boolean`<br>
Exibe os números como itens numa lista (combobox) em vez de spinner<br>
Valor padrão: `false`

### _Disponível apenas para tipo 'receiver'_<br>
__receiver__ `string`<br>
Permite selecionar o ID de um receptor criado, para realizar comunicações utilizando o método `apiRequest`, passando o ID do receptor como parâmetro.<br>
Por exemplo, selecionar um receptor do tipo `obs_v5` (OBS Studio WebSocket v5) para poder enviar requisições para este receptor configurado.<br>
Valores disponíveis:<br>
`obs_v4` OBS Studio WebSocket v4<br>
`obs_v5` OBS Studio WebSocket v5<br>
`lumikit` Lumikit WebService<br>
`vmix` vMix WebService<br>
`ha` Home Assistant<br>
`ptz` PTZ Optics<br>
`midi` receptores MIDI<br>
`tbot` Telegram Bot<br>
`openai` OpenAI API

### _Disponível apenas para tipo 'background'_<br>
__background_type__ `string`<br>
Tipos disponíveis: `all`  `theme`  `my_video`  `my_image`  `video`  `image`

### _Disponível apenas para tipo 'label'_ <br>
`v2.22.0+` <br>
__text__ `string or function` Texto que será exibido. Pode ser uma function que retorna uma string.<br>
__copyable__ `boolean` _(opcional)_ Exibe um ícone de copiar, para copiar o conteúdo de `text`.<br>
__text_to_copy__ `string or function` _(opcional)_ Texto que será copiado em vez de `text`.<br>
__monospaced__ `boolean` _(opcional)_ Exibir o texto com uma fonte monospaced.<br>

### _Disponível apenas para tipo 'button'_ <br>
`v2.22.0+` <br>
__button_label__ `string or function` Texto que será exibido no botão. Pode ser uma function que retorna uma string.<br>
__action__ `function` Ação que será executada ao clicar no botão.<br>
__hide_label__ `boolean` _(opcional)_ Para exibir somente o botão, centralizado, sem o "label" identificador do campo `name`.<br>


---

Alguns exemplos de input:

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'title'
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'separator'
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'string',
  hint: 'hint'
}
```

```javascript
{
             id: 'var_name',
           name: 'default value',
           type: 'string',
    description: 'Example',
  default_value: 'Abc'
}
```

```javascript
{
                id: 'item',
              name: 'suggested',
              type: 'string',
  suggested_values: [
    'abc', '123', 'xyz'
  ]
}
```

```javascript
{
              id: 'item',
            name: 'allowed',
            type: 'string',
  allowed_values: [
   'abc', '123', 'xyz'
 ]
}
```

```javascript
{
              id: 'option',
            name: 'allowed label',
            type: 'string',
  allowed_values: [
   //exibe na interface (combobox) o valor do parâmetro 'label'
   //mas o conteúdo na variável 'obj.input.option'
   //será o valor do parâmetro 'value'
   {value: '1', label: 'ABC'},
   {value: '2', label: 'XYZ'},
   {value: '3', label: '123'}
 ]
}
```

```javascript
{
              id: 'item',
            name: 'allowed function',
            type: 'string',
  allowed_values: function(obj) {
    var n = new Date().getSeconds();
    return [n, n + 1, n + 2];
  }
}
```

```javascript
{
             id: 'subgroup',
           name: 'Subgrupo',
           type: 'string',
 allowed_values: function(obj) {
   switch (obj.input.group) {
      case 'group_1':
        return ['A', 'B', 'C'];
      case 'group_2':
        return ['X', 'Y', 'Z'];
      case 'group_3':
        return ['0', '1', '2'];
   }
 }
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'textarea'
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'number'
}
```

```javascript
{
             id: 'duration',
           name: 'range',
           type: 'number',
            min: 1,
            max: 60,
  default_value: 5
}
```

```javascript
{
                id: 'channel',
              name: 'combobox',
              type: 'number',
               min: 1,
               max: 16,
  show_as_combobox: true
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'boolean'
}
```

```javascript
{
    id: 'var_name',
  name: 'Input name',
  type: 'password'
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'date',
  default_value: "2024-01-16" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'time',
  default_value: "20:00" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'datetime',
  default_value: "2024-01-16 20:00" //optional
}
```

```javascript
{
            id: 'var_name',
          name: 'Input name',
          type: 'color',
 default_value: '#0000FF' //optional
}
```

```javascript
{
        id: 'receiver_id',
      name: 'OBS',
      type: 'receiver',
  receiver: 'obs_v5'
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'song',
  default_value: "12345678" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'holyrics_text',
  default_value: "abcxyz" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'verse',
  default_value: "Gn 1:1" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'audio',
  default_value: "example.mp3" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'video',
  default_value: "example.mp4" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'image',
  default_value: "example.jpg" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'file',
  default_value: "example.txt" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'announcement',
  default_value: { //optional
    ids: [
      "11122233",
      "12345678"
    ]
  }
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'automatic_presentation',
  default_value: "example" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'countdown',
  default_value: { //optional
          time: "19:00",
    exact_time: true
  }
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'countdown_cp',
  default_value: { //optional
    minutes: 5,
    stop_at_zero: false
  }
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'cp_text',
  default_value: { //optional
    text: "Example",
    display_ahead: true
  }
}
```

```javascript
{
               id: 'bg',
             name: 'Input name',
             type: 'background',
  background_type: 'all'
}
```

```javascript
{
               id: 'bg',
             name: 'Input name',
             type: 'background',
  background_type: 'my_video'
}
```

```javascript
{
               id: 'bg',
             name: 'Input name',
             type: 'background',
  background_type: 'my_video',
    default_value: "12345678" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'theme',
  default_value: "123456789" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'label',
           text: " - Text - ",
           copyable: true, //optional
           text_to_copy: "Text" //optional
}
```

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'button',
   button_label: "button_label",
         action: function() {
                   //do action
                 }
}
```
