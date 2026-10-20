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

## Conclusão

Os testes demonstram que um agente de IA precisa de instruções claras, validação das respostas e limites bem definidos para evitar informações comerciais incorretas ou promessas que não pode cumprir.

As melhorias implementadas priorizam a confiabilidade das informações, a proteção dos dados do cliente e a transparência sobre as limitações do sistema.

**Limitação atual:** O workflow recebe mensagens por webhook e gera respostas com IA. O encaminhamento para atendimento humano e a consulta a pedidos ainda não estão integrados a sistemas reais.

**Próximas melhorias:**
- Testar novamente a consulta sobre o status de um pedido.
- Implementar uma rota de encaminhamento para atendimento humano.
- Criar uma fonte controlada de informações sobre serviços e preços.
- Ampliar os testes com diferentes mensagens e situações.
