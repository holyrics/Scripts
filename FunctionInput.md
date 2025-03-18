# Function Input

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/FunctionInput.md)

---


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

[InputParam](https://github.com/holyrics/Scripts/blob/main/InputParam.md)