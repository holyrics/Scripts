# InputParam

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/InputParam.md)

---


InputParam is the item used in the creation of components created in the program's windows.<br>
Various JavaScript-based functionalities can create input windows to obtain user entries.<br>
Items such as text box, checkbox, combobox, etc. can be created using the InputParam structure

Parameters that each item of type `InputParam` can contain:<br>
__id__ `string` _(mandatory)_<br>
Variable name

__name__ `string`  `default: id`<br>
Name to display in the interface.<br>
To use HTML formatting, start the string with `<html>`.<br>
`name: '<html><i>name</i>'`<br>

__type__ `string`  `default: 'string'`<br>
Parameter type. This defines the type of component displayed in the interface to set values.<br>
For example, a boolean type will display a `checkbox`.<br>
Available types: `title`  `separator`  `label (v2.22.0+)`  `string`  `textarea`  `number`  `boolean`  `password`  `date`  `time`  `datetime`  `color`  `receiver`  `song`  `holyrics_text`  `verse`  `audio`  `video`  `image`  `file`  `announcement`  `automatic_presentation`  `countdown`  `countdown_cp`  `cp_text`  `background`  `theme`  `button (v2.22.0+)`  `settings (v2.23.0+)`<br>

__description__ `string`  `default: ''`<br>
Provide a description for the parameter, so it can be displayed on the screen as "help".<br>

__default_value__ `object`  `default: '' | false | 0 | null`<br>
Set an initial value for the parameter.<br>

__onchange__ `function`  `default: null`  `v2.23.0+`<br>
Method that will be executed whenever the component's value is changed.<br>
(`only read` methods do not trigger `onchange`, for example, `type: title`)
The parameter received by the function contains the `input` with the current value of all `InputParam` items in the current window, not just the current `InputParam`.<br>
The `view` parameter (Map) was added in `v2.25.0`, allowing, for example, to change the current name (label) set for the parameter.<br>
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
Validate the content of the item when the OK button of the dialog window is pressed.<br>
Return a string with the error or `true` if the item is valid.<br>
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

### _Available only for 'string' type_<br>
__suggested_values__ `array or function`  `default: null`<br>
Displays a list of suggestions when clicking on the "arrow" available in the text box, but allows any value to be typed in the text box.<br>
It is possible to return a `function` so that the values can be updated in real time.<br>
Allows, for example, to display a list of suggested values based on the value of previous inputs.<br>

__allowed_values__ `array or function`  `default: null`<br>
Displays a list of options in `combobox` format, without the option to enter other values.<br>
It is possible to return a `function` so that the values can be updated in real time.<br>
Allows, for example, to display a list of suggested values based on the value of previous inputs.<br>

### _Available only for type 'number'_<br>
__min__ `number`  `default: 0`<br>
Minimum allowed value.<br>

__max__ `number`  `default: 100`<br>
Maximum allowed value.<br>

__component__ `string`  `default: 'spinner'`<br>
Define the type of component used.<br>
Available values: `spinner` `combobox` `slider`.<br>

__decimal__ `boolean`  `default: false`<br>
Define whether the component will accept decimal values or only integers.<br>
Available only for `spinner` and `slider`.<br>

__unit__ `string`  `default: null`<br>
Text added after the current value displayed in the component.<br>
Available only for `slider`.<br>

### _Available only for 'receiver' type_<br>
__receiver__ `string` _(mandatory)_<br>
Allows selecting the ID of a created receiver to perform communications using the `apiRequest` method, passing the receiver's ID as a parameter.<br>
For example, select a receiver of type `obs_v5` (OBS Studio WebSocket v5) to be able to send requests to this configured receiver.<br>
Starting from `v2.23.0`, it is possible to define multiple values separated by commas, for example: `receiver: 'obs_v4,obs_v5'`<br>
Available values:<br>
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

### _Available only for 'background' type_<br>
__background_type__ `string`  `default: 'all'`<br>
Available types: `all`  `theme`  `my_video`  `my_image`  `video`  `image`

### _Available only for type 'title'_ <br>
__setup__ `function`  `default: null`  `v2.24.0+`<br>
Method that will be executed when displaying a window with inputs.<br>
The parameter received by the function is an object of type `JSInputParamWindow`.<br>
Usage example: capture the reference to the `dialog` object in the current context and call `dialog.ok()` in another situation, for example, to force the window to restart.<br>
```javascript
function(dialog) {
  //simulates clicking the ok button
  //dialog.ok();

  //simulates clicking the cancel button
  //dialog.cancel();
}
```

### _Available only for 'label' type_ <br>
`v2.22.0+` <br>
__text__ `string or function` _(mandatory)_ Text that will be displayed. It can be a function that returns a string.<br>
__copyable__ `boolean` `default: false` Displays a copy icon to copy the content of `text`.<br>
__text_to_copy__ `string or function` `default: text` Text that will be copied instead of `text`.<br>
__monospaced__ `boolean` `default: false` Display the text in a monospaced font.<br>

`v2.24.0+` <br>
__hide_label__ `boolean` `default: false` To display only the text, centered, without the "label" identifying the field `name`.<br>

### _Available only for 'button' type_ <br>
`v2.22.0+` <br>
__button_label__ `string or function` _(mandatory)_ Text that will be displayed on the button. It can be a function that returns a string.<br>
__action__ `function` _(mandatory)_ Action that will be executed when clicking the button.<br>
__hide_label__ `boolean` `default: false` To display only the button, centered, without the "label" identifying the field `name`.<br>
`v2.23.0+` <br>
__button_icon__ `string` `default: null` Icon displayed on the button. Know more: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/i18n/en/Icon.md)<br>

### _Available only for type 'settings'_ <br>
Allows you to create a button that opens another input window with new items.<br>
`v2.23.0+` <br>
__button_label__ `string or function` `default: ''` Text that will be displayed on the button. It can be a function that returns a string.<br>
__settings__ `Array<InputParam>` _(mandatory)_ List of items displayed when clicking the settings button.<br>
__hide_label__ `boolean` `default: false` To display only the button, centered, without the "label" identifying the field `name`.<br>
__button_icon__ `string` `default: 'settings'` Icon displayed on the button. Know more: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/i18n/en/Icon.md)<br>

---

Some examples of input:

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
   //displays in the interface (combobox) the value of the 'label' parameter
   //but the content in the variable 'obj.input.option'
   //it will be the value of the parameter 'value'
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
                   name: 'Message',
                   type: 'string'
                 }, {
                     id: 'duration',
                   name: 'Duration',
                   type: 'number'
                 }]
}

// The fields defined in settings are within the id of the upper field
// For example
// var_name.msg
// var_name.duration
```