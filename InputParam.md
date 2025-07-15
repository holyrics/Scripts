# InputParam

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/InputParam.md)

---


InputParam é o item utilizado na criação de componentes criados nas janelas do programa.<br>
Diversas funcionalidades baseadas em JavaScript podem criar janelas de input para obter entradas do usuário.<br>
Itens como caixa de texto, checkbox, combobox, etc. podem ser criados utilizando a estrutura InputParam

Parâmetros que cada item do tipo `InputParam` pode conter:<br>
__id__ `string` _(obrigatório)_<br>
Nome da variável

__name__ `string`  `default: id`<br>
Nome para exibir na interface.<br>
Para utilizar formatação HTML inicie a string com `<html>`.<br>
`name: '<html><i>nome</i>'`<br>

__type__ `string`  `default: 'string'`<br>
Tipo de parâmetro. Isso define o tipo de componente exibido na interface para definir valores.<br>
Por exemplo, tipo boolean irá exibir um `checkbox`.<br>
Tipos disponíveis: `title`  `separator`  `label (v2.22.0+)`  `string`  `textarea`  `number`  `boolean`  `password`  `date`  `time`  `datetime`  `color`  `receiver`  `song`  `holyrics_text`  `verse`  `audio`  `video`  `image`  `file`  `announcement`  `automatic_presentation`  `countdown`  `countdown_cp`  `cp_text`  `background`  `theme`  `button (v2.22.0+)`  `settings (v2.23.0+)`  <br>
 <br>
**(v2.26.0+)**  `object_model`  `object_model_manage_list`  `module`  `transition_settings`  `song_key`  `time_sig`  `icon`  `bible_verse`  `bible_verse_list`  `bible_version`  `favorite`  `rule_group`<br>
 <br>
 <br>
__description__ `string`  `default: ''`<br>
Informa uma descrição para o parâmetro, para poder ser exibido na tela como "ajuda".<br>

__default_value__ `object`  `default: '' | false | 0 | null`<br>
Define um valor inicial para o parâmetro.<br>

__onchange__ `function`  `default: null`  `v2.23.0+`<br>
Método que será executado sempre que o componente tiver seu valor alterado.<br>
(métodos `only read` não geram `onchange`, por exemplo, `type: title`)
O parâmetro recebido pela function contém o `input` com o valor atual de todos os itens `InputParam` da janela atual, não somente do `InputParam` atual.<br>
O parâmetro `view` (Map) foi adicionado na `v2.25.0`, permitindo, por exemplo, alterar o nome (label) atual definido para o parâmetro.<br>
```javascript
function(obj) {
  //obj.input.xyz

  //v2.25.0+
  //obj.view.xyz
  //obj.view.xyz.setName(string)
  //obj.view.xyz.getName()
}
```

__validator__ `function`  `default: null`  `v2.24.0+`<br>
Validar o conteúdo do item quando o botão OK da janela de diálogo for pressionado.<br>
Retorne uma string com o erro ou `true` se o item for válido.<br>
```javascript
function(value, input, inputs) {
  //value
  //input.id
  //input.name
  //input.value
  //inputs['abc'].name
  //inputs['abc'].value
  if (value.trim().isEmpty()) {
    return "Field '" + input.name + "' is empty";
  }
  return true;
}
```

### _Disponível apenas para os tipos 'string' 'textarea' 'password'_<br>
__cols__ `number`  `default: 20`<br>
Largura do componente, baseado na quantidade de colunas.<br>

__max_length__ `number`  `default: 8192`<br>
Tamanho máximo de caracteres.<br>

### _Disponível apenas para tipo 'string'_<br>
__suggested_values__ `array or function`  `default: null`<br>
Exibe uma lista de sugestões ao clicar na "setinha" disponível na caixa de texto, mas permite que qualquer valor seja digitado na caixa de texto.<br>
É possível retornar uma `function` para que os valores possam ser atualizados em tempo real.<br>
Permite, por exemplo, exibir uma lista de valores sugeridos baseado no valor dos inputs anteriores.<br>

__allowed_values__ `array or function`  `default: null`<br>
Exibe uma lista de opções no formato `combobox`, sem opção para inserir outros valores.<br>
É possível retornar uma `function` para que os valores possam ser atualizados em tempo real.<br>
Permite, por exemplo, exibir uma lista de valores sugeridos baseado no valor dos inputs anteriores.<br>

### _Disponível apenas para tipo 'textarea'_<br>
__rows__ `number`  `default: 3`<br>
Quantidade de linhas visíveis na interface.<br>

### _Disponível apenas para tipo 'number'_<br>
__min__ `number`  `default: 0`<br>
Valor mínimo permitido.<br>

__max__ `number`  `default: 100`<br>
Valor máximo permitido.<br>

__component__ `string`  `default: 'spinner'`<br>
Define o tipo de componente utilizado.<br>
Valores disponíveis: `spinner` `combobox` `slider`.<br>

__decimal__ `boolean`  `default: false`<br>
Define se o componente aceitará valores decimais ou apenas inteiros.<br>
Disponível apenas para `spinner` e `slider`.<br>

__unit__ `string`  `default: null`<br>
Texto adicionado após o valor atual exibido no componente.<br>
Disponível apenas para `slider`.<br>

### _Disponível apenas para os tipos 'audio' 'video' 'image' 'file'_<br>
__accept_file__ `boolean`  `default: true`  `v2.23.0+`<br>
Aceitar arquivos na janela de seleção de arquivo<br>

__accept_folder__ `boolean`  `default: true`  `v2.23.0+`<br>
Aceitar pastas na janela de seleção de arquivo<br>

### _Disponível apenas para tipo 'receiver'_<br>
__receiver__ `string` _(obrigatório)_<br>
Permite selecionar o ID de um receptor criado, para realizar comunicações utilizando o método `apiRequest`, passando o ID do receptor como parâmetro.<br>
Por exemplo, selecionar um receptor do tipo `obs_v5` (OBS Studio WebSocket v5) para poder enviar requisições para este receptor configurado.<br>
A partir da `v2.23.0` é possível definir múltiplos valores separados por vírgula, por exemplo: `receiver: 'obs_v4,obs_v5'`<br>
Valores disponíveis:<br>
`get` HTTP GET (Query) `v2.23.0+`<br>
`post` HTTP POST `v2.23.0+`<br>
`ws` WebSocket `v2.23.0+`<br>
`tcp` TCP `v2.23.0+`<br>
`udp` UDP `v2.23.0+`<br>
`obs_v4` OBS Studio WebSocket v4<br>
`obs_v5` OBS Studio WebSocket v5<br>
`lumikit` Lumikit WebService<br>
`vmix` vMix WebService<br>
`osc` Behringer (OSC Protocol) `v2.22.1+`<br>
`soundcraft` Soundcraft Ui Series `v2.23.0+`<br>
`ha` Home Assistant<br>
`ptz` PTZ Optics<br>
`midi` receptores MIDI<br>
`tbot` Telegram Bot<br>
`openai` OpenAI API

### _Disponível apenas para tipo 'background'_<br>
__background_type__ `string`  `default: 'all'`<br>
Tipos disponíveis: `all`  `theme`  `my_video`  `my_image`  `video`  `image`

### _Disponível apenas para tipo 'title'_ <br>
__setup__ `function`  `default: null`  `v2.24.0+`<br>
Método que será executado ao exibir uma janela com inputs.<br>
O parâmetro recebido pela function é um objeto do tipo `JSInputParamWindow`.<br>
Exemplo de uso: capturar a referência para o objeto `dialog` no contexto atual e chamar `dialog.ok()` em outra situação, por exemplo, para forçar a reinicialização da janela.<br>
```javascript
function(dialog) {
  //simula o clique no botão ok
  //dialog.ok();

  //simula o clique no botão cancel
  //dialog.cancel();
}
```

### _Disponível apenas para tipo 'label'_ <br>
`v2.22.0+` <br>
__text__ `string or function` _(obrigatório)_ Texto que será exibido. Pode ser uma function que retorna uma string.<br>
__copyable__ `boolean` `default: false` Exibe um ícone de copiar, para copiar o conteúdo de `text`.<br>
__text_to_copy__ `string or function` `default: text` Texto que será copiado em vez de `text`.<br>
__monospaced__ `boolean` `default: false` Exibir o texto com uma fonte monospaced.<br>

`v2.24.0+` <br>
__hide_label__ `boolean` `default: false` Para exibir somente o texto, centralizado, sem o "label" identificador do campo `name`.<br>

### _Disponível apenas para tipo 'button'_ <br>
`v2.22.0+` <br>
__button_label__ `string or function` _(obrigatório)_ Texto que será exibido no botão. Pode ser uma function que retorna uma string.<br>
__action__ `function` _(obrigatório)_ Ação que será executada ao clicar no botão.<br>
__hide_label__ `boolean` `default: false` Para exibir somente o botão, centralizado, sem o "label" identificador do campo `name`.<br>
`v2.23.0+` <br>
__button_icon__ `string` `default: null` Ícone exibido no botão. Saiba mais: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/Icon.md)<br>

### _Disponível apenas para tipo 'settings'_ <br>
Permite criar um botão que abre outra janela de input com novos itens.<br>
`v2.23.0+` <br>
__button_label__ `string or function` `default: ''` Texto que será exibido no botão. Pode ser uma function que retorna uma string.<br>
__settings__ `Array<InputParam>` _(obrigatório)_ Lista de itens exibidos ao clicar no botão de configuração.<br>
__hide_label__ `boolean` `default: false` Para exibir somente o botão, centralizado, sem o "label" identificador do campo `name`.<br>
__button_icon__ `string` `default: 'settings'` Ícone exibido no botão. Saiba mais: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/Icon.md)<br>

### _Disponível apenas para os tipos 'object_model' 'object_model_manage_list'_ <br>
Disponível apenas para módulos<br>
`v2.26.0+` <br>
__model__ `string` _(obrigatório)_ **id** do modelo declarado no respectivo módulo<br>

### _Disponível apenas para o tipo 'module'_ <br>
`v2.26.0+` <br>
__filter_by_info_id__ `string` Para filtrar os itens disponíveis pelo id declarado em `info()` de um módulo<br>
__jscommunity_only__ `boolean` Para filtrar somente módulos instalados pelo **JSCommunity**<br>

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
  component: 'combobox'
}
```

```javascript
{
         id: 'volume',
       name: 'Volume',
       type: 'number',
        min: 0,
        max: 100,
  component: 'slider',
    decimal: true,
       unit: '%'
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

```javascript
{
             id: 'var_name',
           name: 'Input name',
           type: 'settings',
   button_label: "button_label",
       settings: [{
                     id: 'msg',
                   name: 'Mensagem',
                   type: 'string'
                 }, {
                     id: 'duration',
                   name: 'Duração',
                   type: 'number'
                 }]
}

// Os campos definidos em settings ficam dentro do id do campo superior
// Por exemplo
// var_name.msg
// var_name.duration
```

```javascript
{
     id: 'var_name',
   name: 'Input name',
   type: 'object_model',
  model: 'object_model_id'
}
```

```javascript
{
     id: 'var_name',
   name: 'Input name',
   type: 'object_model_manage_list',
  model: 'object_model_id'
}
```

```javascript
{
                 id: 'var_name',
               name: 'Input name',
               type: 'module',
  filter_by_info_id: 'module_id',
   jscommunity_only: true
}
```