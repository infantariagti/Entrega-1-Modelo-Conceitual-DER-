# Entrega 1 — Modelo Conceitual (DER)
### Modelagem de um sistema de gestão de informações para uma organização de pequeno porte

## Metadados
- **Nomes dos alunos e RGM**
- Guilherme da Silva Lima RGM: 47585277
- Kaiky hamada RGM: 47210486
- Lucas Pereira Andre RGM: 46614397
- Paulo Renato sobral da Silva RGM: 46763902
- Ricardo Arakaki RGM: 46786619

---
## 1. Caracterização da Organização 

- **Nome e natureza da organização:** *Jackson Moto Peças, Oficina Mecânica*
- **Contexto e porte:** *A empresa lucra entre R$10-16k com porte pequeno com apenas 2 funcionários e por dia variando entre 10 a 20 motos para conserto e um resultado de 6 a 12 motos finalizadas por dia com problemas simples. Agendamento presencial com teste do veículo para trabalho. 
- **Problemas e necessidades identificados:** *Ausência de comunicação flexível entre funcionário e cliente, necessitando de um suporte de controle para gerenciamento da fila de espera dos clientes e seus veículos. *
- **Justificativa da escolha:** *notável que maioria dos casos a comunicação do mecânico e o cliente é limitada, devido ao excesso e escasso tempo do mecânico para manusear seu tempo com agendas, o objetivo é equilibrar o atendimento de forma que o cliente consiga fazer um autoatendimento  enquanto reduz o trabalho do mecânico de parar de trabalhar em outro veículo para prestar atenção ao novo cliente e seu problema.*
- **Evidências da organização:** Av. Primavera de Caiena, 28 - Parque Santa Madalena, São Paulo - SP, 03981-010 - 11 96067-0539 - Jackson 			
<img width="273" height="383" alt="image" src="https://github.com/user-attachments/assets/c4777c83-5072-4184-bad4-bc0c10611013" />
<img width="314" height="375" alt="image" src="https://github.com/user-attachments/assets/cd4b5832-1abc-46db-82c9-41c2809c8fa8" />


## 2. Processos de Negócio
- **Principais processos mapeados:** :** Recebe mensagens do cliente via WhatsApp, combina quando vai deixar o veículo na oficina e combina quando vai ser retirado. 
**Fluxogramas:* 

<img width="305" height="1190" alt="image" src="https://github.com/user-attachments/assets/66076bf5-f5b3-4f81-9cd6-5c6b703e1b49" />


## 3. Requisitos do Sistema

### 3.1 Requisitos Funcionais (RF)
	RF01 - Cadastro de Clientes: Registrar, editar e consultar dados de clientes (nome, telefone/WhatsApp, CPF e endereço).
	RF02 - Cadastro de Veículos (Motos): Cadastrar as motos associando-as a um cliente específico (placa, modelo, marca, ano, cor e quilometragem de entrada).
	RF03 - Abertura e Gestão de Ordem de Serviço (OS): Criar e atualizar a OS contendo data de entrada, defeito relatado, diagnóstico do mecânico, status (Ex: Aguardando Aprovação, Em Manutenção, Pronta, Entregue) e previsão de entrega.
	RF04 - Cadastro de Peças e Controle de Estoque: Registrar peças (nome, código/referência, valor de custo, valor de venda e quantidade em estoque), reduzindo o saldo automaticamente ao fechar uma OS.
	RF05 - Lançamento de Serviços (Mão de Obra): Cadastrar e vincular os serviços prestados (ex: troca de óleo, revisão geral, troca de relação) com seus respectivos valores à OS.
	RF06 - Geração de Orçamento: Calcular o valor total (peças + mão de obra) e permitir a visualização/impressão do orçamento formatado para validação com o cliente.
	RF07 - Registro de Pagamentos: Registrar a forma de pagamento (Pix, dinheiro, cartão de crédito/débito) e alterar o status financeiro da OS para Pago.
	RF08 - Histórico de Manutenções: Permitir a busca do histórico completo de OS de uma determinada moto por placa ou cliente, facilitando diagnósticos futuros pelo mecânico.
	RF09 - Alerta de Estoque Mínimo: Exibir aviso quando itens de alto giro (óleo, pastilhas de freio, velas) atingirem a quantidade mínima cadastrada.

### 3. Requisitos Não-Funcionais (RNF)
	RNF01 - Usabilidade: A interface deve ser simples e intuitiva, com formulários diretos para que o cadastro do atendimento leve menos de 2 minutos.
	RNF02 - Desempenho: As buscas por cliente ou placa do veículo devem retornar resultados instantaneamente (menos de 2 segundos).
	RNF03 - Integridade de Dados: O sistema não deve permitir a exclusão de clientes ou motos que possuam ordens de serviço ativas ou histórico registrado.
	RNF04 - Backup de Dados: O banco de dados deve possuir uma rotina periódica de backup (local ou em nuvem) para evitar perda de dados de clientes e caixa.
	RNF05 - Compatibilidade de Hardware: O sistema deve rodar em computadores de entrada (configuração básica da recepção) por meio de um navegador web padrão.
	RNF06 - Validação de Entrada: O sistema deve validar formatos de dados (máscara de CPF, padrão de telefone e formato da placa Mercosul/antiga).
	
---

## 4. Regras de Negócio
- **Regras Operacionais**
	RN01 - Execução mediante aprovação: Uma Ordem de Serviço (OS) só pode ter seu status alterado para "Em Manutenção" após a autorização e validação explícita do cliente sobre o orçamento gerado.
	RN02 - Disponibilidade e baixa de estoque: Uma peça só pode ser incluída na OS se houver saldo disponível em estoque. A baixa física/sistêmica ocorre automaticamente no momento do encerramento da OS.
	RN03 - Vinculação obrigatória: Toda OS deve estar obrigatoriamente associada a um veículo cadastrado, e todo veículo precisa ter um cliente responsável vinculado no sistema.
	RN04 - Liberação de veículo pós-quitação: O encerramento definitivo da OS e a liberação do veículo só podem ser realizados após o registro da quitação do valor total (Pix, dinheiro ou cartão).
	RN05 - Alteração de escopo do serviço: Se o mecânico identificar a necessidade de peças ou serviços adicionais durante o conserto, a OS deve entrar em status "Aguardando Nova Aprovação" até a autorização do cliente.

- **Restrições Organizacionais**
	RO01 - Operação enxuta e perfis de acesso: O sistema deve oferecer telas simplificadas e separadas por perfil (a esposa no atendimento/financeiro e o mecânico no pátio), garantindo rapidez para não travar a rotina de apenas duas pessoas.
	RO02 - Conformidade com CDC (Garantia e Validade): Por exigência legal do Código de Defesa do Consumidor, os orçamentos emitidos pelo sistema devem exibir validade padrão de 10 dias e as OS concluídas devem registrar automaticamente prazo de garantia de 90 dias.
	RO03 - Política de quitação imediata: Por diretriz da administração, a oficina não trabalha com pagamentos faturados via boleto próprio ou promissórias ("fiado"); o sistema deve restringir o fechamento a meios de pagamento de liquidação imediata ou cartão.
	RO04 - Adequação à LGPD: O armazenamento dos dados cadastrais (CPF, telefone, endereço) deve servir estritamente para emissão de comprovantes e comunicação sobre o status da moto, garantindo a privacidade do cliente.

---

  ## 5. Dicionário de Dados Conceitual (Preliminar)

- **Entidade CLIENTE:** Armazena as informações dos proprietários das motos atendidas na 
oficina.

| Atributo | Descrição | Regra de negócio associada |	
| -------- | -------- |	-------- |	
| id_cliente | Identificador único do cliente no sistema | Obrigatorio, Chave Primária (PK), Gerado automaticamente pelo sistema |	
| nome | Nome completo do cliente |	Obrigatorio. Exemplo fictício: "Carlos Eduardo Silva". |	
| cpf | Cadastro de Pessoa Física do cliente | Obrigatorio, Único, Formato válido (11 dígitos). Restrição de privacidade (RO04 - LGPD). Exemplo fictício: "123.456.789-00".|
| telefone | Número de telefone/WhatsApp para contato | Obrigatorio. Usado para validação de orçamentos e avisos de conclusão de serviço. Exemplo fictício: "(11) 98765-4321".|
| endereco | Logradouro e bairro do cliente | Opcional. Registro complementar para cadastro. Exemplo fictício: "Rua das Flores, 123 - Centro".|

- **Entidade VEICULO (Moto):**	Armazena os dados dos veículos cadastrados e vinculados aos clientes.
  
| Atributo | Descrição | Regra de negócio associada |	
| -------- | -------- |	-------- |				
|placa | Placa de identificação da moto|Obrigatorio, Chave Primária (PK). Deve seguir o padrão antigo (AAA-1234) ou Mercosul (ABC1D23). Vinculação obrigatória a um cliente (RN03). Exemplo fictício: "ABC-1D23".|
|modelo|Modelo da motocicleta|Obrigatorio. Exemplo fictício: "CG 160 Titan".|
|marca|Fabricante da moto|Obrigatorio. Exemplo fictício: "Honda".|
|ano|Ano de fabricação do veículo|Obrigatorio. Numérico inteiro de 4 dígitos. Exemplo fictício: "2021".|
|cor|Cor predominante do veículo|Obrigatorio. Exemplo fictício: "Vermelha".|
|km_atual|Quilometragem registrada no momento da entrada|Obrigatorio. Deve ser um número inteiro maior ou igual a zero.|

- **Entidade ORDEM_SERVICO:** Entidade central do sistema, responsável por registrar o ciclo de atendimento e manutenção da moto.

| Atributo | Descrição | Regra de negócio associada |	
| -------- | -------- |	-------- |				
|numero_os|Código identificador da Ordem de Serviço|Obrigatorio, Chave Primária (PK), Gerado automaticamente.|
|data_entrada|Data e hora em que a moto deu entrada na oficina|Obrigatorio. Preenchimento automático no momento do cadastro.|
|data_previsao|Data estimada para conclusão dos serviços|Obrigatorio. Deve ser igual ou posterior à data_entrada.|
|data_saida|Data e hora do encerramento e entrega da moto|Opcional na abertura. Preenchimento obrigatório no momento da quitação (RN04).|
|status_os|Estado atual da Ordem de Serviço no fluxo de trabalho|Obrigatorio. Orçamento aceito: "Aguardando Aprovação", "Aprovada", "Em Manutenção" (RN01), "Aguardando Nova Aprovação" (RN05), "Pronta", "Entregue".|
|defeito_relatado|Descrição do problema informado pelo cliente|Obrigatorio. Preenchido pela recepcionista/esposa no atendimento.|
|diagnostico_tecnico|Avaliação detalhada das causas efetuada pelo mecânico|Opcional na abertura. Obrigatorio para emissão do orçamento.|
|Preço_total|Soma do preço total das peças e dos serviços prestados|Obrigatorio, Calculado automaticamente. Deve ser maior ou igual a zero.|
|forma_pagamento|Meio utilizado para a quitação total|Preenchimento obrigatório no fechamento da OS. pagamentos permitidos: "Pix", "Dinheiro", "Cartão de Débito", "Cartão de Crédito". Proibido uso de fiado/promissórias (RO03).|
|validade_orcamento|Data limite de validade dos preços propostos|Calculado automaticamente (data_entrada + 10 dias), conforme RO02 (CDC).|
|prazo_garantia|Período legal de garantia do serviço prestado|Preenchido automaticamente com 90 dias a partir da data_saida, conforme RO02 (CDC).|
	
- **Entidade PECA:** Registra o inventário de peças e insumos mantidos na oficina.
	
| Atributo | Descrição | Regra de negócio associada |	
| -------- | -------- |	-------- |	
|id_item_peca|Código identificador do item de estoque|Obrigatorio, Chave Primária (PK), Gerado automaticamente.|
|descricao_peca|Nome ou especificação técnica da peça|Obrigatorio. Exemplo fictício: "Óleo de Motor 10W30 1L".|
|codigo_referencia|Código do fabricante ou referência comercial|Opcional. Exemplo fictício: "MOB-10W30-1L".|
|preço_custo|Preço pago pela oficina na aquisição do produto|Obrigatorio. Numérico positivo.|
|preço_venda|Preço cobrado do cliente na OS|Obrigatorio.Deve ser estritamente maior que o preço_custo.|
|qtd_estoque|Quantidade física disponível na oficina|Obrigatorio. Inteiro positivo ou zero. Inclusão na OS sujeita à disponibilidade (RN02).|

- **Entidade SERVICO:** Catálogo de mão de obra prestada pelo mecânico.

| Atributo | Descrição | Regra de negócio associada |	
| -------- | -------- |	-------- |	
|id_servico|Código identificador da modalidade de serviço|Obrigatorio, Chave Primária (PK), Gerado automaticamente.|
|nome_servico|Nome descritivo da atividade técnica|Obrigatorio. Exemplo fictício: "Troca de Kit Relação".|
|preço_padrao|Preço base sugerido para a execução do serviço|Obrigatorio. Numérico maior que zero.|

---

## 6. Modelagem Conceitual (Entidades, Atributos, Relacionamentos)
6.1. Entidades Reconhecidas e Justificativas
	CLIENTE: Entidade forte cadastral.
	Justificativa: Necessária para armazenar os dados de contato, identificação e histórico dos proprietários dos veículos, garantindo o cumprimento de exigências fiscais, contratuais e de LGPD.
	VEICULO: Entidade forte (ou de domínio).
	Justificativa: Representa a motocicleta trazida para a oficina. A separação entre CLIENTE e VEICULO permite que um mesmo cliente possua mais de uma moto cadastrada ao longo do tempo.
	ORDEM_SERVICO (OS): Entidade transacional central.
	Justificativa: Controla todo o ciclo de vida do atendimento (diagnóstico, aprovação, execução, cobrança e garantia), vinculando a moto atendida aos produtos e mão de obra empregados.
	PECA: Entidade forte cadastral.
	Justificativa: Representa o inventário físico de insumos e componentes mantidos na oficina. Essencial para controle automático de saldo de estoque e cálculo de orçamentos.
	SERVICO: Entidade forte cadastral.
	Justificativa: Mantém a tabela/catálogo de serviços de mão de obra prestados pelo mecânico, estabelecendo valores padrão para agilizar a criação de ordens de serviço.
6.2. Atributos e Classificações
A classificação dos atributos segue o padrão conceitual de modelagem de dados:
Entidade	Atributo	Classificação do Atributo
CLIENTE	id_cliente	Identificador (Chave Primária), Simples, Monovalorado
	nome	Atômico/Simples, Monovalorado, Obrigatório
	cpf	Atômico/Simples, Monovalorado, Obrigatório, Único
	telefone	Atômico/Simples, Monovalorado, Obrigatório
	endereco	Composto (Logradouro, Bairro), Opcional
VEICULO	placa	Identificador (Chave Primária), Simples, Monovalorado
	modelo	Atômico/Simples, Monovalorado, Obrigatório
	marca	Atômico/Simples, Monovalorado, Obrigatório
	ano	Atômico/Simples, Monovalorado, Obrigatório
	cor	Atômico/Simples, Monovalorado, Obrigatório
	km_atual	Atômico/Simples, Monovalorado, Obrigatório
ORDEM_SERVICO	numero_os	Identificador (Chave Primária), Simples, Monovalorado
	data_entrada	Atômico/Simples, Monovalorado, Obrigatório
	data_previsao	Atômico/Simples, Monovalorado, Obrigatório
	data_saida	Atômico/Simples, Monovalorado, Opcional (na abertura)
	status_os	Atômico/Simples, Monovalorado, Obrigatório
	defeito_relatado	Atômico/Simples, Monovalorado, Obrigatório
	diagnostico_tecnico	Atômico/Simples, Monovalorado, Opcional (na abertura)
	forma_pagamento	Atômico/Simples, Monovalorado, Opcional (no fechamento)
	preço_total	Derivado (Calculado: ∑▒"Peças" +∑▒"Serviços" )
	validade_orcamento	Derivado (Calculado: data_entrada + 10 dias)
	prazo_garantia	Derivado (Calculado: data_saida + 90 dias)
PECA	id_item_peca	Identificador (Chave Primária), Simples, Monovalorado
	descricao_peca	Atômico/Simples, Monovalorado, Obrigatório
	codigo_referencia	Atômico/Simples, Monovalorado, Opcional
	preço_custo	Atômico/Simples, Monovalorado, Obrigatório
	preço_venda	Atômico/Simples, Monovalorado, Obrigatório
	qtd_estoque	Atômico/Simples, Monovalorado, Obrigatório
	estoque_minimo	Atômico/Simples, Monovalorado, Obrigatório
SERVICO	id_servico	Identificador (Chave Primária), Simples, Monovalorado
	nome_servico	Atômico/Simples, Monovalorado, Obrigatório
	preço_padrao	Atômico/Simples, Monovalorado, Obrigatório

6.3. Relacionamentos Pertinentes e Cardinalidades

	CLIENTE possui VEICULO
	Mapeamento: Um cliente pode possuir uma ou várias motos cadastradas na oficina, mas cada moto cadastrada pertence obrigatoriamente a apenas um cliente.
	Cardinalidade: CLIENTE (0,N) <---- possui ----> (1,1) VEICULO
	VEICULO gera ORDEM_SERVICO
	Mapeamento: Uma moto cadastrada pode passar por diversas Ordens de Serviço ao longo do tempo (ou nenhuma se acabou de ser cadastrada). Toda OS refere-se obrigatoriamente a uma única moto.
	Cardinalidade: VEICULO (0,N) <---- gera ----> (1,1) ORDEM_SERVICO
	ORDEM_SERVICO contém PECA 
	Mapeamento: Uma OS pode utilizar zero ou várias peças. Uma peça cadastrada pode ser usada em várias OSs ao longo do tempo.
	Relacionamento Conceitual: N:M (Muitos para Muitos).
	ORDEM_SERVICO (0,N) <---- contém ----> (0,N) PECA
	Mapeamento: Uma Ordem de Serviço pode utilizar nenhuma, uma ou várias peças. Uma peça cadastrada pode ser utilizada em nenhuma, uma ou várias Ordens de Serviço ao longo do tempo.
	Relacionamento Conceitual: N (Muitos para Muitos).
	ORDEM_SERVICO inclui SERVICO 
	Mapeamento: Uma OS deve ter ao menos um serviço registrado (ou múltiplos). Um serviço do catálogo pode ser executado em várias OSs.
	Relacionamento Conceitual: N:M (Muitos para Muitos).
	ORDEM_SERVICO (1,N) <---- possui ----> (0,N) SERVICO
	Mapeamento: Uma Ordem de Serviço deve possuir pelo menos um serviço registrado, podendo possuir vários. Um serviço do catálogo pode ser utilizado em nenhuma, uma ou várias Ordens de Serviço.
	Relacionamento Conceitual: N (Muitos para Muitos).

6.4. Restrições e Políticas Organizacionais Aplicadas ao Modelo
	Integridade Referencial e Proteção de Dados (RN03 / RNF03):
	O modelo proíbe a exclusão física de registros de CLIENTE ou VEICULO que possuam vínculos ativos na tabela ORDEM_SERVICO, preservando a rastreabilidade fiscal e histórica da oficina.
	Prevenção de Ruína Financeira e Estoque Negativo (RN02 / RO03):
	A entidade PECA valida a quantidade solicitada contra a qtd_estoque. Se quantidade > qtd_estoque, a associação é rejeitada pelo sistema.
	O fechamento da OS exige a presença de um preço válido no atributo forma_pagamento (restringindo pagamentos a vista ou cartão).
	Conformidade Legal e Defesa do Consumidor (RO02):
	Os atributos derivados validade_orcamento e prazo_garantia são aplicados sobre as datas da ORDEM_SERVICO, garantindo que a oficina não descumpra prazos contratuais de 10 dias de orçamento e 90 dias de garantia previstos no CDC.
	Preservação de Histórico de Preços:
	Os atributos preço_unitario nas entidades associativas PECA e SERVICO gravam o valor exato cobrado na data do atendimento. Isso garante que reajustes futuros nos atributos preço_venda (da tabela PECA) ou preço_padrao (da tabela SERVICO) não alterem o valor total de ordens de serviço passadas.

## 7. Diagrama Entidade-Relacionamento (DER)
Este diagrama representa o modelo conceitual do banco de dados da oficina mecânica, estruturado para garanitir integridade referencial, histórico de transações e facilidade de expansão.

 <img width="892" height="534" alt="image" src="https://github.com/user-attachments/assets/0a114625-4481-4d8a-906b-d9c437b1694e" />


## 8. Justificativa Técnica
A. Separação entre CLIENTE e VEICULO
	Decisão: Modelar CLIENTE e VEICULO como entidades distintas conectadas por um relacionamento 1:N.
	Por que não unificar em uma única tabela? Se os dados do proprietário fossem armazenados dentro do cadastro da moto, o mesmo cliente com mais de um veículo (ex: uma moto para trabalho e outra para passeio) teria seus dados pessoais (CPF, telefone, endereço) duplicados para cada veículo. A separação garante a 3ª Forma Normal (3FN), elimina redundância cadastral e simplifica a atualização do telefone ou endereço do cliente em um único ponto do sistema.
B. Criar Entidades Associativas com Registros Históricos (PECA e SERVICO)
	Decisão: Decompor os relacionamentos N:M (Muitos-para-Muitos) em entidades associativas que armazenam quantidade e preço_unitario.
	Por que não ligar ORDEM_SERVICO diretamente a PECA e SERVICO? Uma ligação direta sem atributos de relacionamento impediria o sistema de registrar quanto foi cobrado por aquela peça no dia da manutenção. Se o valor de uma peça na tabela PECA sofresse reajuste por inflação meses depois, todas as Ordens de Serviço passadas que usaram aquela peça teriam seus totais alterados retroativamente. O uso da entidade associativa congela o preço_unitario praticado no momento da aprovação do orçamento, preservando a integridade histórica e financeira do caixa.
C. Escolha de Cardinalidades Específicas
	CLIENTE (0,N) <---> (1,1) VEICULO: A cardinalidade mínima 0 do lado do cliente permite que uma pessoa seja cadastrada antes mesmo da entrada física da moto na oficina (ex: orçamento telefônico). A cardinalidade mínima 1 e máxima 1 do lado do veículo garante integridade referencial: nenhuma moto pode existir no banco sem um proprietário responsável.
	ORDEM_SERVICO (1,N) <---> (1,1) SERVICO: Define-se cardinalidade mínima 1 para serviços, pois não existe sentido operacional em abrir uma Ordem de Serviço em uma oficina sem a prestação de ao menos uma mão de obra ou serviço de diagnóstico.
	ORDEM_SERVICO (0,N) <---> (1,1) PECA: A cardinalidade mínima é 0 do lado da peça porque existem regulagens e manutenções puramente mecânicas (ex: sangria de freio, regulagem de corrente, limpezas) que utilizam apenas mão de obra, sem consumo de estoque.
D. Adequação ao Porte do Negócio vs. Evitar Overengineering
	Por que não modelar entidades como MECANICO ou FORNECEDOR nesta etapa? O levantamento de requisitos identificou uma operação enxuta com apenas dois atores ativos (o mecânico/dono e a esposa na recepção). Criar tabelas e telas para gestão de múltiplos mecânicos ou cadastros complexos de fornecedores geraria complexidade desnecessária (overengineering) para o uso diário dos usuários. A modelagem priorizou a agilidade no atendimento sem fechar portas para o futuro: a inclusão de uma chave estrangeira id_mecanico na tabela ORDEM_SERVICO pode ser feita em etapas subsequentes sem exigir reformulação do esquema existente.
E. Persistência de Atributos Derivados e Prazos Legais
	Decisão: Armazenar preço_total, validade_orcamento e prazo_garantia na entidade ORDEM_SERVICO.
	Defesa: Embora sejam valores logicamente derivados de somatórios e datas, a persistência desses dados no banco de dados assegura a imutabilidade do orçamento aprovado pelo cliente, além de garantir compliance instantâneo com as normas do Código de Defesa do Consumidor (CDC) para emissão de comprovantes e consultas de garantia.


## 9. Uso de Inteligência Artificial

| Item | O que registrar |
| **Ferramenta e etapa** | Gemini 2.5 (3.6 flash/estendido) | Somente usado para pesquisa com algumas mínimas correções, uso de imagem e ferramentas internas.|
| **Motivação** | Porque ela faz o trabalho pesado e trabalhoso. |
| **Prompt(s) utilizados** | Sou estudante de 2 semestre de GTI, to fazendo um trabalho que tem foco usar modelagem de banco de dados em um sistema com um tema abordado de uma empresa de escolha de cada grupo. eu escolhi mecanica e tive que fazer uma entrevista com um mecanico pessoalmente e a oficina dele é pequena sendo o mecanico Dono e só ele trabalha com a esposa dele (ela n faz os reparos das motos). O que eu quero é os requisitos funcionais e nao funcionais para eu adicionar ao meu trabalho que sera usado para fazer um sistema que beneficie a oficina.
( Após este prompt foi usado apenas os critérios do esqueleto do 2 ao 8.) |
| **Resposta recebida** | Todas as respostas foram usadas no esqueleto da entrega. |
| **Fontes consultadas e verificadas** | Não houve consulta de fontes. |
| **Trechos rejeitados ou corrigidos** | O código feito em Snippet por engano no critério 7º do esqueleto, Deveria ser uma imagem mas acabou tendo um equívoco da IA e ela fez o código. |
| **Justificativa da escolha final** | houve poucos ajustes e a IA sempre foi essencial em trabalhos que manualmente levaria mais tempo para ser finalizado. |
| **Reflexão crítica** | Somente no 7º pois o prompt estava faltando oque ela deveria fazer, mas a IA foi perfeitamente usada.|
—-
