# Planning Center Online - JavaScript Handler

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/PlanningCenterOnline_JavaScriptHandler.md)

---


Intermediate JavaScript code that allows manipulation of the list received from Planning Center Online.<br> <br>Allows, for example, to correct some details in the object identified by default, or even generate different items from the default, based on the API response.

### transformSong(obj)
Method that receives the identified `Lyrics` object and allows it to be edited.<br>Return `null` to keep the original object unchanged.

**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| `obj.folder` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/folder> |
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |
| `obj.item` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/item> |
| `obj.arrangement` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/arrangement> |
| `obj.song` | _[Lyrics](https://github.com/holyrics/jslib/blob/main/README-en.md#lyrics)_ |  |


**Return:**

| Type  | Description |
| :---: | ------------|
| _[Lyrics](https://github.com/holyrics/jslib/blob/main/README-en.md#lyrics)_ | Edited object or `null` to keep the original object without edits. |


**Example:**

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
**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| `obj.folder` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/folder> |
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |
| `obj.item` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/item> |


**Return:**

| Type  | Description |
| :---: | ------------|
| _[AddItem](https://github.com/holyrics/jslib/blob/main/README-en.md#additem)_ | Return any item of type `AddItem???` available in the documentation.<br>It is possible to return an array of items.<br>Return `null` to use the default object natively identified by the program, which can be of type `plain_text` (text displayed to the public) or `cp_text` (text displayed in the communication panel), depending on the configuration set in the interface. |


**Example:**

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
Executed after a list is loaded

**Parameters:**

| Name | Type  | Description |
| ---- | :---: | ------------|
| `obj.folder` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/folder> |
| `obj.service_type` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/service_type> |
| `obj.plan` | _Object_ | <https://developer.planning.center/docs/#/apps/services/2018-11-01/vertices/plan> |


_Method does not return value_

**Example:**

```javascript
function onload(obj) {
  //todo
}
```

---