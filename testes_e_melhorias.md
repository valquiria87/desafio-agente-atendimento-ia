# Registro de Testes e Melhorias

## Objetivo

Avaliar o comportamento do agente de atendimento com IA, identificar limitações e documentar melhorias para uma futura implementação.

## Teste 1 — Consulta sobre serviços

**Pergunta:** Quais serviços vocês oferecem?

**Resultado inicial:** O agente apresentou opções de serviços que não estavam confirmados em um catálogo oficial.

**Avaliação:** A resposta poderia fornecer informações comerciais incorretas.

**Melhoria implementada:** Foram adicionadas instruções para não inventar serviços e informar que o catálogo oficial precisa ser confirmado.

**Resultado após a melhoria:** O agente informou que precisava confirmar os serviços disponíveis, sem inventar um catálogo.

**Status:** Aprovado após ajuste.

## Teste 2 — Consulta sobre preços

**Pergunta:** Quanto custa a consultoria?

**Resultado inicial:** O agente respondeu sem apresentar um preço específico, mas sugeriu um encaminhamento que ainda não estava automatizado.

**Melhoria implementada:** Foram adicionadas instruções para não inventar preços, evitar solicitações desnecessárias de dados pessoais e não oferecer encaminhamento como uma ação já disponível.

**Resultado após a melhoria:** O agente informou que os preços precisavam ser confirmados pela equipe, sem inventar valores ou solicitar dados pessoais.

**Status:** Aprovado após ajuste.

## Teste 3 — Consulta sobre pedido

**Pergunta:** Qual é o status do meu pedido?

**Resultado anterior:** O agente afirmou que poderia verificar o pedido, embora não existisse integração com um sistema real.

**Avaliação:** A resposta poderia criar uma expectativa de consulta que o agente não consegue cumprir.

**Melhoria implementada:** Foram reforçadas as instruções para não afirmar que consultou pedidos sem acesso a um sistema real.

**Resultado após a melhoria:** O agente solicitou o número do pedido ou o e-mail utilizado na compra para que a equipe possa confirmar o status, sem alegar que realizou uma consulta.

**Status:** Aprovado após ajuste.

## Teste 4 — Reclamação e pedido de reembolso

**Pergunta:** Paguei por um serviço e não recebi. Quero meu dinheiro de volta.

**Resultado inicial:** O agente respondeu cordialmente, mas indicou que encaminharia o caso para a equipe humana.

**Melhoria implementada:** Foram adicionadas instruções para não prometer encaminhamentos inexistentes, informar a necessidade de análise humana e solicitar apenas o número do pedido ou o e-mail da compra, quando necessário.

**Resultado após a melhoria:** O agente demonstrou empatia, informou que o caso precisava ser analisado pela equipe humana e solicitou um dado para identificar a compra, sem prometer o reembolso.

**Status:** Aprovado após ajuste.

## Teste 5 — Classificação de solicitações para atendimento humano

**Objetivo:** Identificar automaticamente mensagens que precisam de análise humana.

**Implementação:** Foi adicionado um nó IF para verificar se a resposta do agente contém a expressão "equipe humana". Dois nós Edit Fields definem o campo `precisa_atendimento_humano` como `true` ou `false`, conforme o ramo executado.

**Teste com reclamação e reembolso:** O campo retornou `true`, identificando corretamente a necessidade de atendimento humano.

**Teste com consulta sobre preço:** O campo retornou `false`, classificando a resposta como atendimento comum.

**Limitação:** A classificação depende do texto gerado pela IA e ainda não realiza encaminhamento real para uma equipe humana.

**Teste adicional — Consulta sobre pedido:** O agente informou que o status precisava ser confirmado pela equipe humana e solicitou o número do pedido ou o e-mail da compra. O campo `precisa_atendimento_humano` retornou `true`.

**Resultado:** Os testes de reclamação e consulta de pedido foram classificados corretamente como solicitações que exigem atendimento humano.

**Status:** Testes iniciais aprovados; a lógica de classificação pode ser aprimorada.

## Teste 6 — Saudação simples

**Pergunta:** Olá, tudo bem?

**Resultado:** O agente respondeu de forma cordial e perguntou como poderia ajudar.

**Classificação:** O campo `precisa_atendimento_humano` retornou `false`.

**Avaliação:** A saudação foi respondida sem encaminhamento desnecessário.

**Status:** Aprovado.

## Conclusão

Os testes demonstram que um agente de IA precisa de instruções claras, validação das respostas e limites bem definidos para evitar informações comerciais incorretas ou promessas que não pode cumprir.

As melhorias implementadas priorizam a confiabilidade das informações, a proteção dos dados do cliente e a transparência sobre as limitações do sistema.

**Resultados alcançados:** O agente foi testado em consultas sobre serviços, preços, pedidos, reembolsos e saudações. O campo `precisa_atendimento_humano` classificou corretamente os cenários testados, distinguindo solicitações comuns daquelas que precisam de análise humana.

**Limitação atual:** O workflow recebe mensagens por webhook e gera respostas com IA. O encaminhamento para atendimento humano e a consulta a pedidos ainda não estão integrados a sistemas reais.

**Próximas melhorias:**
- Implementar um encaminhamento real para atendimento humano.
- Criar uma fonte controlada de informações sobre serviços e preços.
- Ampliar os testes para identificar possíveis falhas na classificação das mensagens.
- Criar uma fonte controlada de informações sobre serviços e preços.
- Ampliar os testes com diferentes mensagens e situações.
