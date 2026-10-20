# Caso 1 — Agente de Atendimento com IA para Criadores de Conteúdo

## Objetivo

Desenvolver e testar um workflow de atendimento com inteligência artificial para criadores de conteúdo do TikTok, Instagram e YouTube, priorizando respostas confiáveis, transparência e identificação de solicitações que precisam de análise humana.

## Tecnologias e ferramentas

- **n8n:** automação do workflow.
- **Google Gemini:** geração de respostas com IA.
- **Google Sheets:** registro de solicitações que precisam de atendimento humano.
- **Google Cloud e OAuth 2.0:** autenticação para integração com o Google Sheets.
- **GitHub:** versionamento e documentação do projeto.
- **Engenharia de prompts:** definição de regras, limites e comportamento do agente.

## Como funciona

1. O webhook recebe a mensagem do cliente.
2. O workflow prepara os dados e envia a mensagem ao modelo de IA.
3. O agente gera uma resposta seguindo instruções para evitar informações comerciais inventadas e promessas não confirmadas.
4. O workflow classifica se a solicitação precisa de atendimento humano.
5. Quando necessário, os dados são registrados em uma planilha Google Sheets.
6. A resposta é devolvida pelo webhook.

## Testes realizados

Foram avaliados os seguintes cenários:

- Perguntas sobre serviços.
- Perguntas sobre preços.
- Consultas sobre status de pedidos.
- Reclamações e solicitações de reembolso.
- Classificação de solicitações para atendimento humano.
- Saudações e interações comuns.
- Registro condicional de solicitações no Google Sheets.

## Resultados alcançados

- Respostas orientadas por regras explícitas e limites de atuação.
- Classificação das solicitações nos cenários testados.
- Registro de solicitações de reembolso na planilha.
- Confirmação de que saudações comuns não geram registros desnecessários.
- Documentação dos testes, melhorias e configuração OAuth 2.0.

## Limitações atuais

O projeto funciona como um protótipo acessível por webhook. Ainda não possui integração com WhatsApp, consulta a uma base real de pedidos ou encaminhamento automático para um atendente humano. O registro na planilha documenta a solicitação, mas não significa que um atendente tenha sido notificado.

## Próximas melhorias

- Implementar encaminhamento efetivo para atendimento humano.
- Criar uma fonte controlada de informações sobre serviços e preços.
- Integrar uma fonte segura para consulta de pedidos.
- Ampliar os testes de classificação e tratamento de falhas.

## Conclusão

O projeto demonstra a aplicação prática de engenharia de prompts e automação com n8n para criar um fluxo de atendimento com IA. A integração com o Google Sheets acrescenta um mecanismo de registro condicional, enquanto os testes documentados ajudam a avaliar o comportamento do agente e identificar limitações antes de uma futura implementação real.
