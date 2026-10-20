# Guia: Conectando o Google Sheets ao n8n com OAuth 2.0

## Objetivo

Este guia documenta como configurar as credenciais do Google Sheets no n8n utilizando OAuth 2.0, desde a criação de um projeto no Google Cloud até a conexão com uma planilha.

O procedimento foi realizado como parte do projeto de portfólio **Agente de Atendimento com IA para Criadores de Conteúdo**.

## 1. Pré-requisitos

- n8n instalado e funcionando localmente.
- Conta Google.
- Planilha criada no Google Sheets.
- Acesso ao Google Cloud Console.

## 2. Criar a planilha

1. Acesse o [Google Sheets](https://sheets.google.com/).
2. Crie uma planilha chamada `Registro de Atendimento IA`.
3. Crie os seguintes cabeçalhos na primeira linha:

| Coluna | Cabeçalho |
|---|---|
| A | Data |
| B | Mensagem do cliente |
| C | Resposta do agente |
| D | Precisa de atendimento humano |

## 3. Acessar o Google Cloud Console

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/).
2. Entre com a mesma conta Google utilizada para acessar a planilha.
3. Crie um projeto chamado `Agente Atendimento IA`.
4. Se o Google solicitar a configuração de uma organização ou recurso pai, selecione `No organization` somente se essa opção estiver disponível e for adequada à sua conta.

### Verificação em duas etapas

Se o Google bloquear o acesso ao Cloud Console, confira se a verificação em duas etapas está ativada na conta Google:

[Configurações de segurança da conta Google](https://myaccount.google.com/security)

## 4. Configurar as APIs

No projeto criado, acesse a biblioteca de APIs e habilite:

- Google Sheets API.
- Google Drive API, se necessária para localizar e selecionar documentos no n8n.

## 5. Configurar a tela de consentimento OAuth

1. Acesse **Google Auth Platform**.
2. Abra **Branding** e configure as informações solicitadas para o aplicativo.
3. Em **Audience**, configure o público adequado. Para uma conta Gmail pessoal, normalmente será necessário selecionar o tipo externo (*External*).
4. Enquanto o aplicativo estiver em teste, adicione a conta Google utilizada na conexão à lista **Test users**.
5. Salve as alterações.

### Como resolver o erro 403: access_denied

A mensagem de que o aplicativo está em teste e só pode ser acessado por usuários aprovados pode indicar que a conta não foi adicionada à lista de usuários de teste.

Confira se o endereço utilizado no login do Google está cadastrado em **Google Auth Platform → Audience → Test users**.

Não é necessário solicitar a verificação pública do aplicativo apenas para realizar um teste pessoal com um usuário autorizado, desde que o uso e os escopos solicitados permitam isso.

## 6. Criar as credenciais OAuth 2.0

1. No Google Cloud Console, acesse a área de clientes OAuth.
2. Crie um cliente OAuth do tipo **Web application**.
3. No n8n, abra as credenciais do Google Sheets e localize o campo **OAuth Redirect URL**.
4. Copie o endereço exibido pelo n8n.
5. Cole esse endereço, sem modificações, em **Authorized redirect URIs** no Google Cloud.
6. Crie o cliente OAuth.
7. Copie o **Client ID** e o **Client Secret** para os campos correspondentes nas credenciais do n8n.
8. Salve e conclua o processo de autorização com a conta Google.

**Importante:** o endereço de redirecionamento deve ser exatamente o informado pelo n8n. Não utilize um endereço presumido.

## 7. Configurar o nó Google Sheets no n8n

No workflow, adicione um nó Google Sheets e configure:

- **Credential:** a conta Google Sheets autorizada.
- **Resource:** o recurso de planilha disponível na versão do n8n.
- **Operation:** `Append Row`.
- **Document:** `Registro de Atendimento IA`.
- **Sheet:** a aba que contém os cabeçalhos.

Selecione o mapeamento manual das colunas e configure:

| Coluna | Expressão |
|---|---|
| Data | `{{ $now.toISO() }}` |
| Mensagem do cliente | `{{ $("Edit Fields").item.json.mensagem_cliente }}` |
| Resposta do agente | `{{ $("Message a model").item.json.candidates[0].content.parts[0].text }}` |
| Precisa de atendimento humano | `{{ $json.precisa_atendimento_humano }}` |

As expressões dependem dos nomes dos nós e da estrutura de dados do workflow. Se forem alterados, ajuste as referências.

## 8. Cuidados com a conexão do workflow

O registro na planilha não deve impedir que o agente devolva a resposta ao cliente.

Antes de testar:

1. Confira as conexões entre o `IF`, os nós `Edit Fields`, o Google Sheets e o `Respond to Webhook`.
2. Verifique se o ramo de atendimento humano registra a solicitação.
3. Verifique se o ramo de atendimento comum continua respondendo sem registrar solicitações desnecessárias.
4. Confirme que a resposta original não é perdida quando o Google Sheets devolve o resultado da operação.

## 9. Testar e diagnosticar erros

Envie uma mensagem que deva exigir atendimento humano e verifique:

- Se o webhook recebeu a mensagem.
- Se o agente gerou a resposta.
- Se `precisa_atendimento_humano` foi definido corretamente.
- Se uma nova linha foi adicionada à planilha.
- Se o webhook ainda devolveu a resposta esperada.

Se aparecer `Error in workflow`, abra **Executions** no n8n, selecione a execução com falha e identifique o nó e a mensagem de erro. Corrija a causa antes de considerar a integração concluída.

## 10. Segurança

- Nunca publique o Client Secret, tokens OAuth, chaves de API ou arquivos de credenciais.
- Não inclua dados pessoais reais de clientes nos exemplos do repositório.
- Utilize dados fictícios nos testes documentados.
- Conceda somente as permissões necessárias à integração.
- Não compartilhe capturas de tela que revelem segredos ou informações privadas.

## Status da implementação

A configuração das credenciais e do nó Google Sheets foi realizada durante o desenvolvimento. O teste final de gravação ainda precisa ser validado e, caso falhe, corrigido antes de declarar a integração como concluída.

## Aprendizado

A integração de serviços externos exige mais do que conectar nós: é necessário configurar APIs, permissões, OAuth 2.0, usuários de teste e tratamento de falhas. Documentar esses passos torna o processo mais reproduzível e facilita a resolução de problemas em projetos futuros.
