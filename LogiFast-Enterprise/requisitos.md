## LogiFast Enterprise

## Requisitos Funcionais (RF)

| Código | Nome | Descrição | Categoria | Prioridade |
| :---: | :--- | :--- | :---: | :---: |
| RF01 | Pedido de Transporte | Permitir que clientes cadastrados solicitem o transporte de uma carga | Evidente | Alta |
| RF02 | Validação de Documentação MOPP | Validar documentação de Movimentação Operacional de Produtos Perigosos cadastrado no sistema | Oculto | Média |
| RF03 | Identificação de Cliente Corporativo | Verificar se o cliente é corporativo | Oculto | Baixa |
| RF04 | Validação do Limite de Crédito do Cliente Corporativo | Verificar se o valor do serviço não ultrapassa o limite de crédito disponível da conta jurídica | Oculto | Alta |
| RF05 | Liberação de Transporte | Permitir que operadores de tráfego liberem as solicitações de transporte bloqueado | Evidente | Alta |
| RF06 | Cálculo de Frete | Calcular frete a partir de dados fornecidos pelo RF01 e API Externa | Oculto | Alta |
| RF07 | Cancelamento de Pedido | Permitir que clientes cancelem suas solicitações de transporte | Evidente | Baixa |
| RF08 | Verificação do nível de bateria/combustível do veículo | Verificar nível de bateria/combustível do veículo do motorista parceiro | Oculto | Baixa |
| RF09 | Registro de Incidente | Permitir que o motorista parceiro registre um incidente | Evidente | Baixa |
| RF10 | Veículo de Resgate | Permitir que operadores de tráfego enviem veículos de resgate para os motoristas parceiros | Evidente | Baixa |

## Requisitos Não Funcionais (RNF)

| Código | Nome | Descrição | Categoria | Classificação | Permanência |
| :---: | :--- | :--- | :---: | :---: | :---: |
| RNF01 | Posição Geográfica | O tempo de atualização da posição geográfica no mapa do cliente não deve exceder 2 segundos em conexões 4G/5G | Obrigatório | Desempenho | Permanente |
| RNF02 | Tempo de Atividade | O sistema deve manter um tempo de atividade (uptime) de 99,9% no período de 24/7 | Obrigatório | Confiabilidade | Permanente |
| RNF03 | Dados Sensíveis | Todos os dados sensíveis dos usuários (clientes e motoristas) devem ser armazenados com criptografia AES-256 e transmitidos sob protocolo TLS 1.3 | Obrigatório | Funcional | Transitório |
| RNF04 | Trajeto do transporte | O módulo do motorista deve ser executado nativamente em Android (versão 10 ou superior) e continuar gravando as coordenadas do trajeto em modo offline caso haja perda momentânea de sinal de celular, sincronizando os dados assim que a rede for restabelecida | Obrigatório | Confiabilidade | Transitório |
| RNF05 | Capacidade de requisições | A arquitetura deve suportar até 30.000 requisições simultâneas por minuto nos horários de pico sem ultrapassar a taxa de erro de 0,1% | Obrigatório | Funcional | Transitório | 

## Regras de Negócio (RN)

| Código | Regra | Descrição |
| :---: | :--- | :--- |
| RN01 | Atribuição de Carga | Cargas categorizadas como perigosas só podem ser atribuídas ou visíveis para motoristas MOPP com documentação válida e atualizada no sistema. |
| RN02 | Confirmação de Chamado do Cliente Corporativo | Bloquear solicitação caso crédito do cliente corporativo ultrapasse o limite disponível da conta jurídica |
| RN03 | Taxa de Cancelamento | Caso o cancelamento do pedido seja solicitado após 10 minutos da aceitação por parte do motorista, o sistema aplicará automaticamente uma taxa de retenção de 20% sobre o valor estimado do frete |
| RN04 | Limite de Rota | Caso o veículo do motorista parceiro apresente menos de 25% de autonomia restante, as rotas ofertadas não poderão ser superiores a 40km |
| RN05 | Suspensão de Tempo do Limite de Entrega | Caso ocorra algum imprevisto durante o percurso (pneu furado, acidente ou avaria da carga), o tempo limite de entrega é suspendido | 