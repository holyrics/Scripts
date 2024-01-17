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
            icon: 'image:example.jpg'
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
Tipos disponíveis: `image`  `video`  `announcement`  `background`  `theme`<br>

Exemplo:
```javascript
icon: 'image:name.jpg' //filename
icon: 'video:name.mp4' //filename
icon: 'announcement:1234' //id
icon: 'background:1234' //id
icon: 'theme:1234' //id
```

Obs.: Todos os parâmetros são opcionais

Caso seja retornado `null`, o item será exibido na forma padrão
