### createUrlToSearch(input)
Método que recebe o input da interface e precisa retornar a URL de pesquisa.<br>
Exemplo:
```javascript
function createUrlToSearch(input) {
    return 'https://domain.com/search?text=' + encodeURI(input.text);
}
```
---
### parseSearchResponseToList(response)
Método para transformar a resposta da requisição feita na URL retornada no método `createUrlToSearch` em uma lista de objetos, cada objeto contendo os campos `id`, `title` e `artist_or_author`.<br>
Exemplo:
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
Método que recebe o id do item selecionado na interface (na lista de resultados) e precisa retornar a URL para obter os dados completos da música (letra, por exemplo).<br>
Exemplo:
```javascript
function createUrlToGetById(id) {
    return 'https://domain.com/get?id=' + encodeURI(id);
}
```
---
### parseGetResponseToSong(response)
Método para transformar a resposta da requisição feita na URL retornada no método `createUrlToGetById` em um objeto "música". O objeto precisa retornar os campos `title`, `artist`, `author` e `lyrics`.<br>
Exemplo:
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

