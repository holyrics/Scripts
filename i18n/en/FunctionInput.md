# Function Input

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/FunctionInput.md)

---


It is possible to define custom `inputs` (parameters) for the execution of JavaScript code.<br>
In this way, it is possible to create generic code models that will be executed according to the parameters provided in the interface.

The variables are passed in the object `obj.input` during the execution of the code.<br>
Creating 3 inputs with the IDs `name`, `duration`, and `flag`, these values can be accessed as shown in the example below:<br>
```javascript
function example(obj) {
    obj.input.text;
    obj.input.duration;
    obj.input.repeat;
}
```

To create `inputs`, implement the method `hGetItemInputParams` in the optional methods section, on the right side of the script editing window, for example:<br>

```javascript
function hGetItemInputParams() {
  return [
    {
      id: 'text',
      name: 'Text'
    },{
      id: 'duration',
      name: 'Duration',
      type: 'number'
    }, {
      id: 'repeat',
      name: 'Repeat',
      type: 'boolean'
    }
  ];
}
```

# Syntax

[InputParam](https://github.com/holyrics/Scripts/blob/main/InputParam.md)