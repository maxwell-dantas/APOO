## LogiFast Enterprise

## Requisitos Funcionais (RF)

| Código | Nome | Descrição | Categoria | Prioridade |
| :---: | :--- | :--- | :---: | :---: |
| RF01 | Solicitação de Transporte | Permitir que clientes cadastrados solicitem o transporte de uma carga | Evidente | Alta |
| RF02 | Agendamento de Transporte | Permitir que clientes cadastrados façam o agendamento de transporte de uma carga | Evidente | Alta |
| RF03 | Cancelamento de Pedido | Permitir que clientes cancelem suas solicitações de transporte | Evidente | Baixa |
| RF04 | Realizar Transporte | Permitir que motoristas parceiros aceitem solicitações de transporte | Evidente | Alta |
| RF05 | Registro de Incidente | Permitir que o motorista parceiro registre um incidente | Evidente | Média |
| RF06 | Inserção de Dados na Aplicação | Permitir que o motorista parceiro insira informações referentes a energia/combustível de seu automóvel | Evidente | Média |
| RF07 | Liberação de Transporte | Permitir que operadores de tráfego liberem as solicitações de transporte bloqueado | Evidente | Alta |
| RF08 | Monitoramento Global de Frotas | Permitir que operadores de tráfego monitorem as frotas do sistema | Evidente | Alta |
| RF09 | Intervenção em Falhas Operacionais | Permitir que operadores de tráfego intervenham em quaisquer falhas operacionais do sistema | Evidente | Média |
| RF10 | Enviar Veículo de Resgate | Permitir que operadores de tráfego enviem veículos de resgate para os motoristas parceiros | Evidente | Média |
| RF11 | Realizar Pagamento | Permitir que clientes realizem o pagamento de suas solicitações de transporte  | Evidente | Alta |
| RF12 | Cadastro no Sistema | Permitir que visitantes (possíveis usuários) façam cadastro na aplicação como cliente ou motorista parceiro | Evidente | Alta |
| RF13 | Autenticação no Sistema | Permitir que usuários façam cadastro na aplicação | Evidente | Alta |  
| RF14 | Informações de Tráfego Georreferenciado | Permitir que o sistema busque informações de tráfego e de geolocalização através de uma API Externa | Oculta | Alta |
| RF15 | Validação de Documentação MOPP | Validar documentação de Movimentação Operacional de Produtos Perigosos cadastrado no sistema | Oculto | Média |
| RF16 | Identificação de Cliente Corporativo | Verificar se o cliente é corporativo | Oculto | Baixa |
| RF17 | Validação do Limite de Crédito do Cliente Corporativo | Verificar se o valor do serviço não ultrapassa o limite de crédito disponível da conta jurídica | Oculto | Alta |
| RF18 | Cálculo de Frete | Calcular frete a partir de dados fornecidos pelo RF01 e RF13 | Oculto | Alta |
| RF19 | Verificação do nível de bateria/combustível do veículo | Verificar nível de bateria/combustível do veículo do motorista parceiro | Oculto | Baixa |

> Obs.: Acredito que seja necessário propor ao cliente um RF para visualizar onde o item transportado se encontra. Não coloquei, pois não está claro no texto (isso seria uma dúvida a tirar com o cliente).

## Requisitos Não Funcionais (RNF)

| Código | Nome | Descrição | Categoria | Classificação | Permanência |
| :---: | :--- | :--- | :---: | :---: | :---: |
| RNF01 | Posição Geográfica | O tempo de atualização da posição geográfica no mapa do cliente não deve exceder 2 segundos em conexões 4G/5G | Obrigatório | Desempenho | Permanente |
| RNF02 | Tempo de Atividade | O sistema deve manter um tempo de atividade (uptime) de 99,9% no período de 24/7 | Obrigatório | Confiabilidade | Permanente |
| RNF03 | Dados Sensíveis | Todos os dados sensíveis dos usuários (clientes e motoristas) devem ser armazenados com criptografia AES-256 e transmitidos sob protocolo TLS 1.3 | Obrigatório | Funcional | Permanente |
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

> **Observações**: Deixo registrado que senti falta de regras de negócios aplicadas ao tempo de limite de entrega e se haverá taxa aplicada ao motorista que registrar um incidente e for preciso enviar uma equipe de resgate.

## Matriz de Rastreabilidade Simples

| RF | RNF Associado | RN Associado |
| :--: | :--: | :--: |
| RF01 e RF02 | RNF01, RNF02 e RNF03 | RN01 e RN02 |
| RF03 | RNF01, RNF02 e RNF03 | RN03 |
| RF04 | RNF02, RNF03 e RNF04 | RN04 e RN05 |