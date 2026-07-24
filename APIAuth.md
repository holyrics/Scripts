# Fluxo de autenticação API Auth utilizando QR Code

**PT** | [EN](https://github.com/holyrics/Scripts/blob/main/i18n/en/APIAuth.md)

---


Método utilitário para receber um `payload` de um serviço externo.<br>
Útil para fazer login, recebendo um token de autenticação.<br>
É necessário uma assinatura [Holyrics Plan](https://holyrics.com.br/holyrics_plan.html) ativa para utilizar esta opção.<br>

Um QR Code é exibido contendo um `json` com as seguintes informações:
```json
{
    "type": "jslib_api_auth",
    "ts": "1779726247",
    "device": "hostname",
    "token": "ONuqkROS93wTAQgRljDQcZGg0hTCu3MADrAyzbp3YS5EN2HqebNsC0dnPTvL12xZ",
    "sig": "bca47d4a4f154c3f3be926f2e95bc9488642867706e9e3a17cf737f193ebb3ce"
}
```
`type` Tipo de autenticação (para possível identificação automática do tipo de QR Code lido)<br>
`ts` timestamp em segundos<br>
`device` Nome do computador<br>
`token` string 64 caracteres [a-zA-Z0-9] Token gerado pelo Holyrics para envio do token de autenticação pela internet<br>
`sig` Assinatura para verificação simples de autenticidade do QR Code<br>

### sig
O valor `sig` é um `HmacSHA256` da concatenação `ts;device;token`, ou seja, baseado no `json` de exemplo acima fica:<br>
```json
"1779726247;hostname;ONuqkROS93wTAQgRljDQcZGg0hTCu3MADrAyzbp3YS5EN2HqebNsC0dnPTvL12xZ"
```
É utilizado o valor definido no parâmetro `secret` para gerar o `HmacSHA256`, no exemplo acima foi utilizado o secret:<br>
```json
"EJbMZOnfEsZEal05T1OBqHnd3DqcYs1g"
```
É algo opcional, apenas caso queira validar a autenticidade do QR Code gerado.

---

### Após ler o QR Code e extrair o token, envie o payload para o endpoint do Holyrics
```bash
curl -X POST "https://holyrics.com.br/api/jslib_auth/send_payload.php" \
  -H "Content-Type: application/json" \
  -d '{
    "token":"ONuqkROS93wTAQgRljDQcZGg0hTCu3MADrAyzbp3YS5EN2HqebNsC0dnPTvL12xZ",
    "payload":"qualquer conteúdo que precisar enviar, token de autenticação, por exemplo"
  }'
```
Obs: O conteúdo enviado no payload pode ser também um objeto complexo em vez de uma string.<br>
Tamanho máximo do `payload`: 1024 caracteres

### Possíveis códigos de erro
400 token inválido ou payload inválido<br>
401 token não encontrado<br>
405 se a requisição não for POST<br>
410 prazo expirado para autenticação<br>
422 se o token já foi utilizado<br>

### Após enviar o payload para o endpoint
Caso a requisição do passo anterior retorne 200, o payload será recebido internamente pelo programa Holyrics aberto no computador (e redirecionado para a `function callback`) e a janela com o QR Code será automaticamente fechada.

Obs: A janela também exibe um botão "copiar", que copia para a área de transferência o mesmo json exibido no QR Code, porém o conteúdo fica em base64.<br>
Exemplo:
```
eyJ0eXBlIjoianNsaWJfYXBpX2F1dGgiLCJ0cyI6IjE3Nzk3MjYyNDciLCJkZXZpY2UiOiJob3N0bmFtZSIsInRva2VuIjoiT051cWtST1M5M3dUQVFnUmxqRFFjWkdnMGhUQ3UzTUFEckF5emJwM1lTNUVOMkhxZWJOc0MwZG5QVHZMMTJ4WiIsInNpZyI6ImJjYTQ3ZDRhNGYxNTRjM2YzYmU5MjZmMmU5NWJjOTQ4ODY0Mjg2NzcwNmU5ZTNhMTdjZjczN2YxOTNlYmIzY2UifQ==
```

Código de exemplo:
```javascript
function scriptAction(obj) {
    
    var header = "<html><div style='text-align:center;width:400pt'>"
                 + "Texto de ajuda para o usuário saber o que fazer para ler o QR Code";
    h.popupAPIAuth({
      window_title: 'QR Code Auth Test',
      header: header,
      callback: (payload) => {
        h.log("payload");
        h.logp(payload);
      },
      on_error: (err) => {
        h.log(err);
      },
      secret: 'EJbMZOnfEsZEal05T1OBqHnd3DqcYs1g'
    });
    
}
```