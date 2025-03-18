# Item Status

É possível aplicar uma visualização personalizada de um item Script/API adicionado na barra de favoritos.<br>
Para que o item possa ter uma cor diferente caso exista algum estado ativado/desativado, por exemplo.

Implemente o método `hGetItemStatusData` na parte de métodos opcionais, na parte direita da janela de edição de script, exemplo:<br>

```javascript
function hGetItemStatusData(obj) {
  if (isActive()) {
    return {
          active: true,
      foreground: 'E6E6E6',
      background: '556918',
       iconColor: 'E6E6E6',
     description: 'text',
            icon: 'check',
            hint: 'hint'
    };
  }
  return null;
}

```
`active` define se o item está ativado ou desativado<br>
Se o item estiver ativado, ele será exibido na cor verde por padrão, caso o valor `background` não seja retornado.

`foreground` cor do texto no formato hexadecimal<br>

`background` cor de fundo no formato hexadecimal<br>

`iconColor` cor do ícone no formato hexadecimal<br>

`description` (v2.21.0+) descrição do item. A descrição será adicionada após o nome/título do item<br>

`icon` (v2.21.0+) ícone personalizado do item. Baseado em algum item já existente no programa.<br>
Saiba mais: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/Icon.md)<br>

`hint` (v2.24.0+) Texto de dica que será exibido ao deixar o mouse parado em cima do item.<br>
Disponível apenas para itens do tipo: [ModuleAction](https://github.com/holyrics/JSCommunity/tree/main/src/modules#moduleaction)<br>

Obs.: Todos os parâmetros são opcionais

Caso seja retornado `null`, o item será exibido na forma padrão