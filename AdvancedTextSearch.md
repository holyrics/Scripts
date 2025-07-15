# Pesquisa Avançada de Texto

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/AdvancedTextSearch.md)

---

`v2.26.0+`

É possível realizar uma pesquisa avançada na aba de textos para um filtro mais preciso dos itens, utilizando itens não disponíveis na interface e filtrando por diferentes itens simultaneamente.

Sintaxe da pesquisa:

```
%key: value   &&   %key: < value   &&   %key: value
```

Utilize "porcentagem" no início da chave e dois-pontos no final da chave.<br>
Em seguida, informe o valor que deseja procurar.

Para utilizar múltiplas chaves, utilize o sinal "&&" para separar os itens.

Itens disponíveis:<br>
- [title](#title)
- [content](#content)
- [comment](#comment)
- [translation](#translation)
- [extra](#extra)
- [saved_theme](#saved_theme)
- [saved_theme_by_id](#saved_theme_by_id)
- [saved_theme_by_name](#saved_theme_by_name)

Também é possível utilizar como chave um item extra criado pelo usuário para as letras.


## String

Pesquisas com string, exemplo:<br>
Textos que contêm __"estou aqui"__ no texto e o tema salvo contém __"abc..."__<br>
```%content: estou aqui && %saved_theme_by_name: abc```

É possível utilizar o caractere `*` para filtrar quando contém qualquer valor ou `!*` para filtrar quando não contém um valor, exemplo:<br>
Textos que contêm __"estou aqui"__ e o campo __saved_theme_by_name__ está preenchido<br>
```%content: estou aqui && %saved_theme_by_name: *```

Textos que contêm __"estou aqui"__ e o campo __saved_theme_by_name__ não está preenchido<br>
```%content: estou aqui && %saved_theme_by_name: !*```

## Regex

Pesquisas utilizando regex, adicione `--regex` ou `--rgx` no início do campo pesquisado, exemplo:<br>
Textos que contêm a palavra __"estou"__ ou a palavra __"aqui"__ no texto e contém algum tema salvo com nome __"abc..."__<br>
```%content: --rgx (estou|aqui) && %saved_theme_by_name: abc```

## Boolean

Pesquisas utilizando verdadeiro ou falso, exemplo: <br>
Textos que contêm tema salvo:<br>
```%saved_theme: true```

Permitido: `true` `false` `yes` `no`

--- 

### title

`string` `regex`<br>
Título do Texto
```
%title: abc xyz
```
```
%title: --rgx (abc|xyz)
```

--- 

### content

`string` `regex`<br>
Conteúdo do item Texto
```
%content: abc xyz
```
```
%content: --rgx (abc|xyz)
```

--- 

### comment

`string` `regex`<br>
Comentários nos parágrafos do Texto
```
%comment: abc xyz
```
```
%comment: --rgx (abc|xyz)
```

--- 

### translation

`string` `regex`<br>
Pesquisa nos campos traduzidos do item Texto
```
%translation: abc xyz
```
```
%translation: --rgx (abc|xyz)
```

--- 

### extra

`string` `regex`<br>
Campo "extra" disponível na janela de edição de um item Texto
```
%extra: abc xyz
```
```
%extra: --rgx (abc|xyz)
```

--- 

### saved_theme

`boolean`<br>
Filtrar textos que tem ou não tema salvo
```
%saved_theme: yes
```
```
%saved_theme: no
```

--- 

### saved_theme_by_id

`string`<br>
Filtrar itens pelo **id** do tema salvo como **tema padrão** no respectivo item<br>
```
%saved_theme_by_id: 1234
```
--- 

### saved_theme_by_name

`string` `regex`<br>
Filtrar itens pelo **nome** do tema salvo como **tema padrão** no respectivo item<br>
```
%saved_theme_by_name: abc
```
```
%saved_theme_by_name: xyz
```