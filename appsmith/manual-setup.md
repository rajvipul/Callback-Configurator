
## Appsmith Callback Configurator Setup

1. Create a new app in Appsmith.
2. Add the following UI components manually:
   - Input: cbUrl
   - Dropdown: cbMethod (GET, POST, PUT)
   - Table: cbHeaders (columns: Key, Value)
   - Code Editor/Text Area: cbPayload (default with standard JSON)
   - Dropdown: cbAuthType (None, Basic Auth, OAuth2, AES Encrypted)
   - Conditional Inputs: authUsername, authPassword, authTokenUrl, oauthClientId, oauthClientSecret, aesKey, aesIv
   - Button: executeBtn -> triggers CallbackAPI.run()
   - Text: outcomeText -> shows response

3. Create API `CallbackAPI` with:
   - URL: http://n8n:5678/webhook/triggerCallback
   - Method: POST
   - Headers: Content-Type: application/json
   - Body (JSON):
```json
{
  "callbackUrl": "{{cbUrl.text}}",
  "method": "{{cbMethod.selectedOption}}",
  "headers": {{cbHeaders.tableData}},
  "payload": {{JSON.parse(cbPayload.text)}},
  "authType": "{{cbAuthType.selectedOption}}",
  "authDetails": {
    "username": "{{authUsername.text}}",
    "password": "{{authPassword.text}}",
    "tokenUrl": "{{authTokenUrl.text}}",
    "clientId": "{{oauthClientId.text}}",
    "clientSecret": "{{oauthClientSecret.text}}",
    "aesKey": "{{aesKey.text}}",
    "iv": "{{aesIv.text}}"
  }
}
```

Use this API to trigger the n8n webhook.
