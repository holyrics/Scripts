# WebSearch (JavaScript)

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/WebSearch_JavaScript.md)

---


### settings()
**Optional**<br>
Starting from `v2.26.0`, the ability to create a settings interface that will be displayed in the window for the user has been added.<br>
The `settings` object will be globally available anywhere in the script for accessing the configurations by the respective `id`.<br>
Example:
```javascript
function settings() {
  var arr = [];
  arr.push({
    id: 'abc',
    type: 'boolean',
    name: 'Example 1'
  });
  arr.push({
    id: 'xyz',
    type: 'boolean',
    name: 'Example 2'
  });
  return arr;
}
```

```javascript
function createUrlToSearch(input) {
  if (settings.abc) {
    /* ... */
  }
  if (settings.xyz) {
    /* ... */
  }
  return /* ... */;
}
```

---
### createUrlToAuth(input) `v2.26.0+`
**Optional**<br>
Method that makes an initial request to obtain, if necessary, an authentication token to be used throughout the flow in the subsequent requests<br>
Example:
```javascript
function createUrlToAuth(input) {
  //input.text (string)
  //input.title (boolean)
  //input.artist (boolean)
  //input.lyrics (boolean)
  //
  //can return a string (url)
  //or a complex request object
  return 'https://domain.com/auth';
}
```
---
### createUrlToSearch(input)
Method that receives input from the interface and needs to return the search URL.<br>
Example:
```javascript
function createUrlToSearch(input) {
  //input.text (string)
  //input.title (boolean)
  //input.artist (boolean)
  //input.lyrics (boolean)
  //input.auth (string) nullable v2.26.0+
  //
  //can return a string (url)
  //or a complex request object
  return 'https://domain.com/search?text=' + encodeURI(input.text);
}
```
---
### parseSearchResponseToList(response)
Method to transform the response of the request made to the URL returned in the `createUrlToSearch` method into a list of objects, each object containing the fields `id`, `title`, and `artist_or_author`.<br>
Example:
```javascript
function parseSearchResponseToList(response) {
  var json = JSON.parse(response);
  var songs = [];
  for (var i = 0; i < json.length; i++) {
    songs.push({
      id: json[i].id,
      title: json[i].title,
      artist_or_author: json[i].author
    });
  }
  return songs;
}
```
---
### createUrlToGetById(id)
Method that receives the id of the selected item in the interface (in the results list) and needs to return the URL to obtain the complete data of the song (lyrics, for example).<br>
Example:
```javascript
function createUrlToGetById(id) {
  //
  //can return a string (url)
  //or a complex request object
  return 'https://domain.com/get?id=' + encodeURI(id);
}
```
---
### parseGetResponseToSong(response)
Method to transform the response of the request made to the URL returned in the `createUrlToGetById` method into a "music" object. The object needs to return the fields `title`, `artist`, `author`, and `lyrics`.<br>
Example:
```javascript
function parseGetResponseToSong(response) {
  var json = JSON.parse(response);
  return {
    title: json.title,
    artist: json.artist,
    author: json.author,
    lyrics: json.lyrics
  };
}
```
---
### Complex Request Object
To make an advanced request (for example, of type **POST** or adding **headers**), return an object instead of `string`<br>
Example:
```javascript
function createUrlToSearch(response) {
  /* ... */
  return {
    url: 'https://domain.com',
    type: 'POST', /*default GET*/
    headers: {
      Authorization: 'Bearer ...'
    },
    data: "body/raw", /* 'data' can be string or object */
  };
}
```