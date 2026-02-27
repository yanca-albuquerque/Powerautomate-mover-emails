## 🚀 Fluxo: Mover e-mails no Outlook (Power Automate + Graph API)

Este fluxo automatiza a organização de caixas de e-mail compartilhadas, movendo mensagens para pastas específicas com base em suas categorias. 

### ⚙️ Passo a Passo

####  Recorrência
* Intervalo: 1 hora
* Fuso horário: (UTC-03:00) Brasília

#### Enviar uma solicitação HTTP
* Uri: concat(
  'https://graph.microsoft.com/v1.0/users/ID-CAIXA/mailFolders/inbox/messages?',
  '$top=1000',
  '&$select=id,subject,categories',
  '&$filter=receivedDateTime ge 2026-01-01T00:00:00Z and categories/any(c:c eq ''TESTE'')'
)
* Método: GET

#### Aplicar a cada
* Saída: body('Enviar_uma_solicitação_HTTP')?['value']

#### Mover email (V2)
* ID da mensagem: items('Aplicar_a_cada')?['id']
* Pasta: TESTE        // (Selecione a pasta ou coloque o ID dela para achar)
* Endereço da Caixa de Correio Original: teste@yanca.com.br         // coloque o email da caixa compartilhada aqui
