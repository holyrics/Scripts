# API Popup Create Song

Opção via API para criar uma nova música abrindo a janela de edição de letra. (v2.21.0+)

Isso permite que qualquer outro processo no computador possa enviar um conteúdo ao programa para abrir a janela de edição de letra.

```
curl -X 'POST' \
  'http://localhost:8091/api/popup-createsong' \
  -H 'Content-Type: application/json' \
  -d '{ "title": "...", "author": "...", "artist": "...", "lyrics": "..."}'
```

**Parâmetros:**

| Nome | Tipo  | Descrição |
| ---- | :---: | ------------|
| `title` | _String_ | Título da música |
| `lyrics` | _String_ | Letra da música |
| `author` | _String (opcional)_ | Autor da música |
| `artist` | _String (opcional)_ | Artista da música |
| `note` | _String (opcional)_ | Anotação da música |
| `key` | _String (opcional)_ | Tom da música.<br>Pode ser: `C` `C#` `Db` `D` `D#` `Eb` `E` `F` `F#` `Gb` `G` `G#` `Ab` `A` `A#` `Bb` `B` `Cm` `C#m` `Dbm` `Dm` `D#m` `Ebm` `Em` `Fm` `F#m` `Gbm` `Gm` `G#m` `Abm` `Am` `A#m` `Bbm` `Bm` |
| `bpm` | _Number (opcional)_ | BPM da música |
| `time_sig` | _String (opcional)_ | Tempo da música.<br>Pode ser: `2/2` `2/4` `3/4` `4/4` `5/4` `6/4` `3/8` `6/8` `7/8` `9/8` `12/8` |


Observações:<br>
- Disponível a partir da versão 2.21.0;
- É necessário que a opção "API Server" esteja ativada nas configurações do programa;
- Aceita somente requisições da máquina local utilizando endereço loopback;
- Caso tenha sido modificada, altere a porta 8091 da requisição para a porta correspondente definida nas configurações API Server.
