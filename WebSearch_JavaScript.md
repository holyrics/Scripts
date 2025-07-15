# WebSearch (JavaScript)

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/WebSearch_JavaScript.md)

---


### settings()
**Opcional**<br>
A partir da `v2.26.0` foi adicionada possibilidade de criar uma interface de configurações que será exibida na janela para o usuário.<br>
O objeto `settings` estará disponível globalmente em qualquer local do script para acesso às configurações pelo respectivo `id`.<br>
Exemplo:
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
**Opcional**<br>
Método que faz uma requisição inicial para obter, se necessário, algum token de autenticação para ser utilizado no decorrer do fluxo nas próximas requisições<br>
Exemplo:
```javascript
function createUrlToAuth(input) {
  //input.text (string)
  //input.title (boolean)
  //input.artist (boolean)
  //input.lyrics (boolean)
  //
  //pode retornar uma string (url)
  //ou um objeto complexo de requisição
  return 'https://domain.com/auth';
}
```
---
### createUrlToSearch(input)
Método que recebe o input da interface e precisa retornar a URL de pesquisa.<br>
Exemplo:
```javascript
function createUrlToSearch(input) {
  //input.text (string)
  //input.title (boolean)
  //input.artist (boolean)
  //input.lyrics (boolean)
  //input.auth (string) nullable v2.26.0+
  //
  //pode retornar uma string (url)
  //ou um objeto complexo de requisição
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
Método que recebe o id do item selecionado na interface (na lista de resultados) e precisa retornar a URL para obter os dados completos da música (letra, por exemplo).<br>
Exemplo:
```javascript
function createUrlToGetById(id) {
  //
  //pode retornar uma string (url)
  //ou um objeto complexo de requisição
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
    title: json.title,
    artist: json.artist,
    author: json.author,
    lyrics: json.lyrics
  };
}
```
---
### Complex Request Object
Para realizar uma requisição avançada (por exemplo, do tipo **POST** ou adicionando **headers**), retorne um objeto em vez de `string`<br>
Exemplo:
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