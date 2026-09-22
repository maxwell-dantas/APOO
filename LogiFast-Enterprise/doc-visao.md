## LogiFast Enterprise

## Requisitos Funcionais (RF)

| Código | Nome | Descrição | Categoria | Prioridade |
| :-----: | :--- | :-------- | :-------: | :--------: |
| RF01 | Pedido de Transporte | Permitir que clientes cadastrados solicitem o transporte de uma carga | Evidente | x |
| RF02 | Validação de Documentação MOPP | Validar documentação de Movimentação Operacional de Produtos Perigosos cadastrado no sistema | Oculto | x |
| RF03 | Identificação de Cliente Corporativo | Verificar se o cliente é corporativo | Oculto | x |
| RF04 | Validação do Limite de Crédito do Cliente Corporativo | Verificar se o valor do serviço não ultrapassa o limite de crédito disponível da conta jurídica | Oculto | x |
| RF05 | Liberação de Transporte | Permitir que **operadores de tráfego** liberem as solicitações de transporte bloqueado | Evidente | x |
| RF06 | Cálculo de Frete | Calcular frete a partir de dados fornecidos pelo RF01 e API Externa | Oculto | x |
| RF07 | Cancelamento de Pedido | Permitir que clientes cancelem suas solicitações de transporte | Evidente | x |

## Requisitos Não Funcionais (RNF)

| x | x | x | x | x |
| :----- | :--- | :-------- | :-------: | :--------: |
| x | x | x | x | x |

## Regras de Negócio (RN)

| Código | Regra | Descrição |
| :---: | :--- | :--- |
| RN01 | Atribuição de Carga | Cargas categorizadas como **perigosas** só podem ser atribuídas ou visíveis para motoristas MOPP com documentação válida e atualizada no sistema. |
| RN02 | Confirmação de Chamado do Cliente Corporativo | Bloquear solicitação caso crédito do **cliente corporativo** ultrapasse o limite disponível da conta jurídica |
| RN03 | Taxa de Cancelamento | Caso o cancelamento do pedido seja solicitado após 10 minutos da aceitação por parte do motorista, o sistema aplicará automaticamente uma taxa de retenção de 20% sobre o valor estimado do frete |
| RN04 | Limite de Rota | Caso o veículo do motorista parceiro apresente menos de 25% de autonomia restante, as rotas ofertadas não poderão ser superiores a 40km |
| RN05 | Suspensão de Tempo Limite de Entrega | Caso ocorra algum imprevisto durante o percurso (pneu furado, acidente ou avaria da carga), o tempo limite de entrega é suspendido | 