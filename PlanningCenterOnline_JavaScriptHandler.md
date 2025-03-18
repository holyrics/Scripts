# Planning Center Online - JavaScript Handler

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/PlanningCenterOnline_JavaScriptHandler.md)

---


Código JavaScript intermediário que permite manipular a lista recebida do Planning Center Online.

Permite, por exemplo, corrigir alguns detalhes no objeto identificado por padrão, ou mesmo gerar itens diferentes do padrão, baseado na resposta da API.

---

## PlanningCenterOnline_JSHandler
Código JavaScript intermediário que permite manipular a lista recebida do Planning Center Online.<br> <br>Permite, por exemplo, corrigir alguns detalhes no objeto identificado por padrão, ou mesmo gerar itens diferentes do padrão, baseado na resposta da API.

### transformSong(obj)
Método que recebe o objeto `Lyrics` identificado e permite editá-lo.<br>Retorne `null` para manter o objeto original sem edições.

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |
| `obj.item` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/item> |
| `obj.arrangement` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/arrangement> |
| `obj.song` | _[Lyrics](https://github.com/holyrics/jslib#lyrics)_ |  |


**Retorno:**

| Tipo  | Descrição |
| :---: | ------------|
| _[Lyrics](https://github.com/holyrics/jslib#lyrics)_ | Objeto editado ou `null` para manter o objeto original sem edições. |


**Exemplo:**

```javascript
function transformSong(obj) {
    var song = obj.song;
    if (song.title.contains("abc")) {
        song.title = song.title.replace("abc", "xyz");
        return song;
    }
    return null;
}
```

---

### createItem(obj)
**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |
| `obj.item` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/item> |


**Retorno:**

| Tipo  | Descrição |
| :---: | ------------|
| _[AddItem](https://github.com/holyrics/jslib#additem)_ | Retorne qualquer item do tipo `AddItem???` disponível na documentação.<br>É possível retornar um array de itens.<br>Retorne `null` para utilizar o objeto padrão identificado nativamente pelo programa, que pode ser do tipo `plain_text` (texto exibido ao público) ou `cp_text` (texto exibido no painel de comunicação), depende da configuração definida na interface. |


**Exemplo:**

```javascript
function createItem(obj) {
  var attr = obj.item.attributes;
  if (attr.title.contains("#cp")) {
      return {
          type: 'cp_text',
          name: attr.title,
          text: attr.description,
          display_ahead: true
      };
  }
  return null;
}
```

---

### onload(obj)
Executado após uma lista ser carregada

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |


_Método sem retorno_

**Exemplo:**

```javascript
function onload(obj) {
  //todo
}
```

---