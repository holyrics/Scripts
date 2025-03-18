# Item Status

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/StatusView.md)

---


It is possible to apply a custom view to a Script/API item added to the favorites bar.<br>
So that the item can have a different color if there is any activated/deactivated state, for example.

Implement the method `hGetItemStatusData` in the optional methods section, on the right side of the script editing window, for example:<br>

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
`active` defines whether the item is enabled or disabled<br>
If the item is enabled, it will be displayed in green by default, unless the `background` value is returned.

`foreground` text color in hexadecimal format<br>

`background` background color in hexadecimal format<br>

`iconColor` icon color in hexadecimal format<br>

`description` (v2.21.0+) item description. The description will be added after the name/title of the item<br>

`icon` (v2.21.0+) custom item icon. Based on an existing item in the program.<br>
Know more: [Scripts > Icon](https://github.com/holyrics/Scripts/blob/main/i18n/en/Icon.md)<br>

`hint` (v2.24.0+) Tooltip text that will be displayed when the mouse hovers over the item.<br>
Available only for items of type: [ModuleAction](https://github.com/holyrics/JSCommunity/tree/main/src/modules#moduleaction)<br>

Note: All parameters are optional

If `null` is returned, the item will be displayed in the default form