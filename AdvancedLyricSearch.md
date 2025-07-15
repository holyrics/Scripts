# Pesquisa Avançada de Letra

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/AdvancedLyricSearch.md)

---


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

`v2.26.0`<br>
- [arrangement](#arrangement)
- [spotify_id](#streaming_id)
- [spotify_id_bt](#streaming_id_bt)
- [spotify_id_any](#streaming_id_any)
- [youtube_id](#streaming_id)
- [youtube_id_bt](#streaming_id_bt)
- [youtube_id_any](#streaming_id_any)
- [deezer_id](#streaming_id)
- [deezer_id_bt](#streaming_id_bt)
- [deezer_id_any](#streaming_id_any)
- [linked_audio](#linked_audio)
- [linked_audio_bt](#linked_audio_bt)
- [linked_audio_any](#linked_audio_any)
- [saved_theme_by_id](#saved_theme_by_id)
- [saved_theme_by_name](#saved_theme_by_name)
- [played_hour](#played_hour)
- [played_day_of_week](#played_day_of_week)
- [played_month](#played_month)
- [played_year](#played_year)
- [played_service](#played_service)

Obs.: Alguns itens permitem utilizar o nome traduzido, por exemplo, "título" em vez de "title".

Também é possível utilizar como chave um item extra criado pelo usuário para as letras.


## String

Pesquisas com string, exemplo:<br>
Músicas que contêm __"estou aqui"__ na letra e contém algum autor com nome __"mat..."__<br>
```%lyrics: estou aqui && %author: mat```

É possível utilizar o caractere `*` para filtrar quando contém qualquer valor ou `!*` para filtrar quando não contém um valor, exemplo:<br>
Músicas que contêm __"estou aqui"__ e o campo __autor__ está preenchido<br>
```%lyrics: estou aqui && %author: *```

Músicas que contêm __"estou aqui"__ e o campo __autor__ não está preenchido<br>
```%lyrics: estou aqui && %author: !*```

## Regex

Pesquisas utilizando regex, adicione `--regex` ou `--rgx` no início do campo pesquisado, exemplo:<br>
Músicas que contêm a palavra __"estou"__ ou a palavra __"aqui"__ na letra e contém algum autor com nome __"mat..."__<br>
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
Músicas que contêm tema salvo:<br>
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
Filtra apenas músicas que contêm pelo menos um slide com o nome informado.<br>
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

--- 

### arrangement

`string` `regex`<br>
Filtrar músicas que contêm um arranjo específico (pelo nome)<br>
```
%arrangement: abc
```
```
%arrangement: xyz
```
--- 

### streaming_id

`spotify_id`  `youtube_id`  `deezer_id`<br>
`string`<br>
Filtrar músicas pelo link salvo nas informações 'extras' da música no respectivo streaming<br>
A busca é feita somente nos itens do tipo **"voz"**<br>
A pesquisa pode ser feita informando apenas o **id** ou o link completo<br>
```
%spotify_id: abc
```
```
%youtube_id: xyz
```
--- 

### streaming_id_bt

`spotify_id_bt`  `youtube_id_bt`  `deezer_id_bt`<br>
`string`<br>
Filtrar músicas pelo link salvo nas informações 'extras' da música no respectivo streaming<br>
A busca é feita somente nos itens do tipo **"playback"**<br>
A pesquisa pode ser feita informando apenas o **id** ou o link completo<br>
```
%spotify_id_bt: abc
```
```
%youtube_id_bt: xyz
```
--- 

### streaming_id_any

`spotify_id_any`  `youtube_id_any`  `deezer_id_any`<br>
`string`<br>
Filtrar músicas pelo link salvo nas informações 'extras' da música no respectivo streaming<br>
A busca é feita nos itens do tipo **"voz"** e **"playback"**<br>
A pesquisa pode ser feita informando apenas o **id** ou o link completo<br>
```
%spotify_id_any: abc
```
```
%youtube_id_any: xyz
```
--- 

### linked_audio

`string` `regex`<br>
Filtrar músicas pelo nome do arquivo de áudio associado nas informações 'extras' da música<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
```
---

### linked_audio_bt

`string` `regex`<br>
Filtrar músicas pelo nome do arquivo de áudio associado nas informações 'extras' da música<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
```
--- 

### linked_audio_any

`string` `regex`<br>
Filtrar músicas pelo nome do arquivo de áudio associado nas informações 'extras' da música<br>
```
%linked_audio: filename.mp3
```
```
%linked_audio: folder/filename.mp3
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
--- 

### played_hour

`string`<br>
Filtrar músicas pela quantidade de vezes que foram tocadas em uma hora do dia específica.<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
//foi tocada mais de 10 vezes às 19 horas
%played_hour: 19 > 10
```
```
//foi tocada menos de 10 vezes nos horários de 19, 20, 21 e 22 horas
%played_hour: 19,20,21,22 <= 10
```
```
//foi tocada menos de 10 vezes no intervalo de 19, 20, 21 e 22 horas
%played_hour: 19-22
```
--- 

### played_day_of_week

`string`<br>
Filtrar músicas pela quantidade de vezes que foram tocadas em um dia da semana específico.<br>
`sun` `mon` `tue` `wed` `thu` `fri` `sat`
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
//foi tocada mais de 20 vezes no domingo
%played_day_of_week: sun > 20
```
```
//foi tocada 20 vezes ou menos contando sábado e domingo
%played_day_of_week: sat,sun <= 20
```
--- 

### played_month

`string`<br>
Filtrar músicas pela quantidade de vezes que foram tocadas em um mês do ano.<br>
`1 ~ 12`<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
//foi tocada menos de 5 vezes em janeiro
%played_month: 1 < 5
```
```
//foi tocada 5 vezes ou mais contando março, abril ou maio
%played_month: 3,4,5 >= 5
```
```
//foi tocada 5 vezes ou mais contando março, abril ou maio
%played_month: 3-5
```
--- 

### played_year

`string`<br>
Filtrar músicas pela quantidade de vezes que foram tocadas em um ano específico.<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
//foi tocada mais de 10 vezes em 2023
%played_year: 2023 > 10
```
```
//foi tocada 10 vezes ou menos contando 2023, 2024 e 2025
%played_year: 2023,2024,2025 <= 10
```
```
//foi tocada 10 vezes ou menos contando 2023, 2024 e 2025
%played_year: 2023-2025
```
--- 

### played_service

`string`<br>
Filtrar músicas pela quantidade de vezes que foram tocadas em um culto específico (pelo nome do culto).<br>
É utilizado o campo "histórico" como base, ou seja, é considerado apenas as exibições da opção "marcada como tocada".
```
//foi tocada mais de 20 no horário do respectivo culto
%played_service: nome do culto > 20
```
```
//foi tocada 10 vezes ou menos no horário do respectivo culto
%played_service: nome do culto <= 10
```