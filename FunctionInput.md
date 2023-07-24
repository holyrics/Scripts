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

Parâmetros que cada `input` pode conter:<br>
__id__ `string` _(obrigatório)_<br>
Nome da variável

__name__ `string`<br>
Nome para exibir na interface<br>
Valor padrão: `Nome da variável`

__type__ `string`<br>
Tipo de parâmetro. Isso define o tipo de componente exibido na interface para definir valores.<br>
Por exemplo, tipo boolean irá exibir um `checkbox`.<br>
Tipos disponíveis: `string`, `textarea`, `number`, `boolean`, `password`, `color`, `receiver`<br>
Valor padrão: `string`

__description__ `string`<br>
Informa uma descrição para o parâmetro, para poder ser exibido na tela como "ajuda".<br>
Valor padrão: `vazio`

__default_value__ `object`<br>
Define um valor inicial para o parâmetro.<br>
Valor padrão: `vazio | false | 0`

_Disponível apenas para tipo 'string'_<br>
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

_Disponível apenas para tipo 'number'_<br>
__min__ `number`<br>
Valor mínimo permitido.<br>
Valor padrão: `0`

__max__ `number`<br>
Valor máximo permitido.<br>
Valor padrão: `100`

__show_as_combobox__ `boolean`<br>
Exibe os números como itens numa lista (combobox) em vez de spinner<br>
Valor padrão: `false`

__receiver__ `string`<br>
Permite selecionar o ID de um receptor criado, para realizar comunicações utilizando o método `apiRequest`, passando o ID do receptor como parâmetro.<br>
Por exemplo, selecionar um receptor do tipo `obs_v5` (OBS Studio WebSocket v5) para poder enviar requisições para este receptor configurado.<br>
Valores disponíveis:<br>
`obs_v4` OBS Studio WebSocket v4<br>
`obs_v5` OBS Studio WebSocket v5<br>
`lumikit` Lumikit WebService<br>
`vmix` vMix WebService<br>
`ha` Home Assistant<br>
`ptz` PTZ Optics

---

Alguns exemplos de input:

```javascript
{
 id: 'text',
 name: 'Text',
 type: 'string'
}
```

```javascript
{
 id: 'text',
 name: 'Text',
 type: 'textarea'
}
```

```javascript
{
 id: 'total',
 name: 'Total',
 type: 'number'
}
```

```javascript
{
 id: 'flag',
 name: 'Flag',
 type: 'boolean'
}
```

```javascript
{
 id: 'token',
 name: 'Token',
 type: 'password'
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
 type: 'string',
 description: 'Example',
 default_value: 'Abc'
}
```

```javascript
{
 id: 'duration',
 name: 'Duration',
 type: 'number',
 min: 1,
 max: 60,
 default_value: 5
}
```

```javascript
{
 id: 'item',
 name: 'Item',
 type: 'string',
 suggested_values: [
  'abc', '123', 'xyz'
 ]
}
```

```javascript
{
 id: 'item',
 name: 'Item',
 type: 'string',
 allowed_values: [
  'abc', '123', 'xyz'
 ]
}
```

```javascript
{
 id: 'option',
 name: 'Option',
 type: 'string',
 allowed_values: [
  //exibe na interface (combobox) o valor do parâmetro 'label'
  //mas o conteúdo a variável 'obj.input.option'
  //será o valor do parâmetro 'value'
  {value: '1', label: 'ABC'},
  {value: '2', label: 'XYZ'},
  {value: '3', label: '123'}
 ]
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
