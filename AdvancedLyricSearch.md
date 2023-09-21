# Pesquisa Avançada de Letra

É possível realizar uma pesquisa avançada na aba de letras para um filtro mais preciso dos itens, utilizando itens não disponíveis na interface e filtrando por diferentes itens simultaneamente.

Sintaxe da pesquisa:

```
%key: value   &&   %key: < value   &&   %key: value
```

Utilize "porcentagem" no início da chave e dois-pontos no final da chave.<br>
Em seguida, informe o valor que deseja procurar.

Para utilizar múltiplas chaves, utilize o sinal "&&" para separar os itens.

Itens disponíveis:<br>
- [title](#title)
- [artist](#artist)
- [lyrics](#lyrics)
- [note](#note)
- [author](#author)
- [group](#group)
- [comment](#comment)
- [slide_description](#slide_description)
- [translation](#translation)
- [bpm](#bpm)
- [chord_key](#chord_key)
- [time_sig](#time_sig)
- [extra](#extra)
- [order](#order)
- [saved_theme](#saved_theme)
- [played_days](#played_days)
- [played_count](#played_count)

Obs.: Alguns itens permitem utilizar o nome traduzido, por exemplo, "título" em vez de "title".

Também é possível utilizar como chave um item extra criado pelo usuário para as letras.


## String

Pesquisas com string, exemplo:<br>
Músicas que contém __"estou aqui"__ na letra e contém algum autor com nome __"mat..."__<br>
```%lyrics: estou aqui && %author: mat```

É possível utilizar o caractere `*` para filtrar quando contém qualquer valor ou `!*` para filtrar quando não contém um valor, exemplo:<br>
Músicas que contém __"estou aqui"__ e o campo __autor__ está preenchido<br>
```%lyrics: estou aqui && %author: *```

Músicas que contém __"estou aqui"__ e o campo __autor__ não está preenchido<br>
```%lyrics: estou aqui && %author: !*```

## Regex

Pesquisas utilizando regex, adicione `--regex` ou `--rgx` no início do campo pesquisado, exemplo:<br>
Músicas que contém a palavra __"estou"__ ou a palavra __"aqui"__ na letra e contém algum autor com nome __"mat..."__<br>
```%lyrics: --rgx (estou|aqui) && %author: mat```

## Number

Pesquisas utilizando número, exemplo:<br>
Músicas com bpm maior ou igual a 80<br>
```%bpm: >= 80```

Músicas com bpm de 90 a 120<br>
```%bpm: >= 90 && %bpm: <= 120```

Músicas que foram tocadas pela última vez há mais de 90 dias e que foram tocadas mais de 5 vezes no total<br>
```%played_days: > 90 && %played_count: > 5```

Tipos de comparação aceitos:<br>
`<=` menor ou igual a<br>
`>=` maior ou igual a<br>
`<>` ou `!=` diferente de <br>
`<` menor que <br>
`>` maior que <br>

## Boolean

Pesquisas utilizando verdadeiro ou falso, exemplo: <br>
Músicas que contém tema salvo:<br>
```%saved_theme: true```

Permitido: `true` `false` `yes` `no`

--- 

### title

`string` `regex`<br>
Título da música
```
%title: abc xyz
```
```
%title: --rgx (abc|xyz)
```

--- 

### artist

`string` `regex`<br>
Artista da música
```
%artist: abc xyz
```
```
%artist: --rgx (abc|xyz)
```

--- 

### lyrics

`string` `regex`<br>
Letra da música
```
%lyrics: abc xyz
```
```
%lyrics: --rgx (abc|xyz)
```

--- 

### note

`string` `regex`<br>
Anotação da música
```
%note: abc xyz
```
```
%note: --rgx (abc|xyz)
```

--- 

### author

`string` `regex`<br>
Autor da música
```
%author: abc xyz
```
```
%author: --rgx (abc|xyz)
```

--- 

### group

`string`<br>
Filtra apenas músicas do grupo informado.<br>
É necessário informar o nome completo do grupo.<br>
Não aceita regex ou pesquisa parcial.
```
%group: abc
```

--- 

### comment

`string` `regex`<br>
Comentários na letra da música
```
%comment: abc xyz
```
```
%comment: --rgx (abc|xyz)
```

--- 

### slide_description

`string` `regex`<br>
Filtra apenas músicas que contém pelo menos um slide com o nome informado.<br>
Aceita pesquisa parcial apenas utilizando regex.<br>
A pesquisa simples por string precisa informar o nome completo da descrição
```
%title: chorus
```
```
%title: --rgx (verse)
```

--- 

### translation

`string` `regex`<br>
Pesquisa nos campos traduzidos da letra da música
```
%translation: abc xyz
```
```
%translation: --rgx (abc|xyz)
```

--- 

### bpm

`number`<br>
Filtrar músicas utilizando o BPM
```
%bpm: <= 90
```
```
%bpm: = 80
```

--- 

### chord_key

`string`<br>
Filtrar músicas utilizando a tonalidade
```
%chord_key: Em
```
```
%chord_key: A
```

--- 

### time_sig

`string`<br>
Filtrar músicas utilizando o tempo
```
%time_sig: 4/4
```
```
%time_sig: 6/8
```

--- 

### extra

`string` `regex`<br>
Campo "extra" disponível na janela de edição da letra da música
```
%extra: abc xyz
```
```
%extra: --rgx (abc|xyz)
```

--- 

### order

`boolean`<br>
Filtrar músicas que tem ou não a ordem dos slides definida manualmente
```
%order: true
```
```
%order: false
```

--- 

### saved_theme

`boolean`<br>
Filtrar músicas que tem ou não tema salvo
```
%saved_theme: yes
```
```
%saved_theme: no
```

--- 

### played_days

`number`<br>
Filtrar músicas baseado na quantidade de dias desde a última exibição da letra.<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
%played_days: >= 90
```
```
%played_days: < 90
```

--- 

### played_count

`number`<br>
Filtrar músicas baseado na quantidade (total) de vezes que a música foi exibida.<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
%played_count: != 0
```
```
%played_count: > 5
```
