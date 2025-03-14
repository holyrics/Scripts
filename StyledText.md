# Styled Text
Para exibir um texto com formatação avançada, inicie o texto com **&lt;styled&gt;**

Tags HTML disponíveis

```html
<styled>
<b>negrito</b>
<i>itálico</i>
<u>sublinhado</u>
<color:0000FF>Cor da fonte</color>
<font:Arial>Nome da fonte</font>
<size:70>Tamanho relativo da fonte 70%</size>

A partir da v2.23.0
<line-height:100>Altura da linha</line-height>
<valign:0>Alinhamento vertical  -200 ~ 200  </valign>
<bgcolor:000000>Cor de fundo</bgcolor>
<brightness-color:000000>Cor do brilho</brightness-color>
<brightness-weight:50>  0 ~ 100  </brightness-weight>
<outline-color:000000>Cor do contorno</outline-color>
<outline-weight:50>  0 ~ 100  </outline-weight>
<shadow-color:000000>Cor da sombra</shadow-color>
<shadow-x-weight:50>  -100 ~ 100  </shadow-x-weight>
<shadow-y-weight:-50>  -100 ~ 100  </shadow-y-weight>
<blur>Aplicar efeito blur</blur>
```

---

## v2.25.0+

É possível criar modelos de formatação (parecido como funciona um CSS) para reutilizar a respectiva formatação em textos exibidos em diferentes locais do programa compatíveis com a sintaxe &lt;styled&gt;

**Exemplo:**
```
title {
  b;
  size: 120;
}

footer {
  i;
  size: 80;
}
```

**Texto:**
```
<#:title>Exemplo</#>
 
Exemplo Exemplo Exemplo Exemplo
```

O trecho dentro da tag `<#:title>...</#>` será exibido com a formatação negrito e tamanho de fonte relativo de 120%.
