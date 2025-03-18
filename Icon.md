# Icon

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/Icon.md)

---


Opções disponíveis para exibição de ícones personalizados nas funcionalidades do Holyrics que aceitam esta sintaxe.<br>

Tipos disponíveis: `image`  `video`  `announcement`  `background`  `theme`<br>
A partir de `v2.23.0+`<br>
`system`  `base64`  `svg`<br>

O valor deverá ser informado como string, sendo iniciado pelo tipo, seguido de dois-pontos e o respectivo valor correspondente ao tipo informado.<br>

Para os tipos `image` e `video`, o valor é o **nome de um arquivo** (incluindo possíveis subpastas) existente na respectiva aba Imagem ou Vídeo.<br>
Obs.: A utilização de um vídeo não significa que o ícone será animado, tipo gif. Apenas a imagem estática identificada do vídeo será utilizada.<br>

Para os tipos `announcement`, `background` e `theme`, o valor é o `id` do item.<br>
Geralmente o `id` de um item pode ser obtido clicando com o botão direito do mouse no item (menu de contexto), opção **"Script Info"**.<br>

`system`<br>
Na `v2.23.0` a biblioteca [Google Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons&icon.style=Filled) foi adicionada ao programa.<br>
Para o tipo `system`, o valor é o `nome` do ícone.<br>
Obs.: é opcional informar `system:`, para valores informados sem um `type` declarado, o valor será considerado um ícone do tipo `system` por padrão.<br>

Para o tipo `base64`, o valor é os bytes da imagem (JPG , por exemplo) em formato base64.<br>

Para o tipo `svg`, o valor é o próprio conteúdo XML do SVG

Exemplos:
```javascript
icon: 'image:name.jpg'
icon: 'image:folder/name.jpg'

icon: 'video:name.mp4'

icon: 'announcement:1234'

icon: 'background:1234'

icon: 'theme:1234'

icon: 'system:settings'
icon: 'settings'

icon: 'base64:iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAbUlEQVR42mNgGAWjAAgWA7EoLS34AcTvgDielhb8h+K9QKxESwv+Q/mVQMxEKwtg+AIQG9PSAhjuA2IeWloAwveB2IuWFjwEYg9aWdADxFy0CKJLQGxAq2RaTatkup9WGQ1UVCQP2cJuFAxxAAAPXEusG9ShJQAAAABJRU5ErkJggg=='

icon: 'svg:<?xml version="1.0" encoding="utf-8"?>\n<svg fill="#000000" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">\n    <path d="M8 5v14l11-7z"/>\n    <path d="M0 0h24v24H0z" fill="none"/>\n</svg>'
```

## HTML

Em locais onde `html` é permitido, é possível utilizar um ícone pela tag `<img>`.<br>
Sintaxe `<img src='icon:{name,size,color}'>`<br>
`size` e `color` são opcionais<br>

Exemplo:
```html
<!-- ícone 'settings' no mesmo tamanho de fonte e cor do texto atual -->
<img src='icon:settings'>

<!-- ícone 'settings' no tamanho 16px e cor do texto atual -->
<img src='icon:settings,16'>

<!-- ícone 'settings' no tamanho 16px e cor verde -->
<img src='icon:settings,16,00FF00'>
```