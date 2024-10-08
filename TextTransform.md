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
         /* opcional */
         //Valor que será adicionado no início do texto do slide atual
         add_start: "", // (string)
         //
         /* opcional */
         //Valor que será adicionado no final do texto do slide atual
         add_end: "", // (string)
         //
         /* opcional */
         //Adiciona o texto com uma quebra de linha (default: true)
         line_break: true, // (boolean)
         //
         /* opcional */
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
        // o texto '♪' seja exibido
        return {
            add_end: '♪'
        };
    }
    return null;
}
```

#TextTransformInfo#
