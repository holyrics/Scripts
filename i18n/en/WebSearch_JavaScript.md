### createUrlToSearch(input)

**EN** | [PT](https://github.com/holyrics/Scripts/blob/main/WebSearch_JavaScript.md)

---

Method that receives input from the interface and needs to return the search URL.<br>
Example:
```javascript
function createUrlToSearch(input) {
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
            'id': json[i]['id'],
            'title': json[i]['title'],
            'artist_or_author': json[i]['author']
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
        'title': json['title'],
        'artist': json['artist'],
        'author': json['author'],
        'lyrics': json['lyrics']
    };
}
```