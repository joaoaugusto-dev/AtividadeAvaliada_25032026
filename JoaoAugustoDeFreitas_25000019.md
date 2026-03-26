# Avaliação — Engenharia de Software
**Sistema Integrado de Gestao de Farmácia**

- Aluno: João Augusto de Freitas  
- RA: 25000019
- Data: 25/03/2026  

---

# 1. Definição do MVP
O MVP cobre os processos de venda, controle de estoque, cadastro de clientes, compras, contas a pagar/receber e geração de relatórios. Incluí:
- Venda de produtos (à vista e a prazo)
- Atualização automática de estoque
- Cadastro e consulta de clientes
- Registro de compras e atualização de estoque
- Controle de contas a pagar e a receber
- Relatórios básicos para gestão

Ficam fora (muito avançado, por iso não faz sentido estar em um MVP):
- Integração com sistemas externos
- Funcionalidades avançadas de auditoria
- Customização de perfis de usuário além dos básicos

---

# 2. Regras de Negócio (mínimo: 5)

- **RN01 —** Produtos sem estoque não podem ser vendidos.
- **RN02 —** Vendas a prazo só podem ser realizadas para clientes cadastrados.
- **RN03 —** Compras de produtos devem atualizar automaticamente o estoque da unidade.
- **RN04 —** Contas a pagar e a receber devem ter controle de status (Aberta, Paga/Recebida, Atrasada).
- **RN05 —** Apenas gerentes podem cadastrar ou atualizar produtos.
- **RN06 —** Produtos controlados só podem ser vendidos mediante receita válida.
- **RN07 —** Não é permitido cadastrar dois produtos com o mesmo código de barras.
- **RN08 —** O sistema deve impedir vendas para clientes que estão devendo.
- **RN09 —** Relatórios financeiros só podem ser acessados por usuários autorizados (Administradores).
- **RN10 —** Transferências de estoque entre unidades devem ser registradas por gerente.

---

# 3. Requisitos Funcionais (mínimo: 8)

- **RF01 —** Permitir venda de produtos à vista e a prazo.
- **RF02 —** Consultar produtos por nome, código de barras ou fabricante.
- **RF03 —** Registrar e atualizar estoque automaticamente após vendas, compras, devoluções e perdas.
- **RF04 —** Cadastrar e consultar clientes.
- **RF05 —** Registrar compras de produtos e atualizar estoque.
- **RF06 —** Gerar contas a pagar e a receber com controle de vencimento e status.
- **RF07 —** Emitir comprovante de venda.
- **RF08 —** Gerar relatórios de vendas, estoque e contas.
- **RF09 —** Permitir cadastro e consulta de fornecedores.
- **RF10 —** Permitir transferência de estoque entre unidades.
- **RF11 —** Alertar gerente sobre produtos com estoque abaixo do mínimo.
- **RF12 —** Permitir cadastro e consulta de receitas médicas.
- **RF13 —** Permitir bloqueio de clientes "devedores".

---

# 🛡 4. Requisitos Não Funcionais (mínimo: 4)

- **RNF01 —** O sistema deve ser acessível via web para todas as unidades.
- **RNF02 —** O tempo de resposta para consultas de produtos deve ser menos que 1 segundo.
- **RNF03 —** O sistema deve garantir integridade dos dados em operações críticas (venda, compra, financeiro). Uma boa opção é a redundância de dados.
- **RNF04 —** O acesso às funcionalidades deve ser restrito conforme o perfil do usuário.
- **RNF05 —** O sistema deve ser compatível com dispositivos móveis.
- **RNF06 —** O backup dos dados deve ser realizado diariamente.
- **RNF07 —** O sistema deve estar disponível pelo menos 99,5% do tempo.

---

# 5. Casos de Uso (mínimo: 10)

## Diagrama de Casos de Uso

<img width="834" height="357" alt="uc_relatorios_administracao" src="https://github.com/user-attachments/assets/c43b8d87-0bfb-49bf-8f8d-833815229677" />
<img width="647" height="473" alt="uc_operacoes_venda" src="https://github.com/user-attachments/assets/adeeed21-29d6-4798-bb14-d9d8843393a0" />
<img width="718" height="353" alt="uc_gestao_estoque_compras" src="https://github.com/user-attachments/assets/279420b5-4251-42ef-9c45-6cfe0d5064f9" />
<img width="623" height="325" alt="uc_financeiro" src="https://github.com/user-attachments/assets/3000ba28-ca7f-47e8-a078-c11ed682d01b" />
<img width="190" height="315" alt="uc_controle_especial" src="https://github.com/user-attachments/assets/04a35c85-c32a-4752-9d37-b96b16aa9214" />

---

# 6. Documentação dos Casos de Uso

## UC01 — Realizar Venda
**Ator(es):** Atendente
**Descrição:** Registra a venda de produtos ao cliente, verifica estoque e emite comprovante.
**Pré-condições:** Produto cadastrado e disponível em estoque.
**Pós-condições:** Estoque atualizado, venda registrada, comprovante emitido.

### Fluxo Principal
1. Atendente identifica/cadastra cliente.
2. Consulta produto e verifica estoque.
3. Informa quantidade e tipo de pagamento.
4. Se necessário, valida receita médica.
5. Finaliza venda e emite comprovante.

### Fluxos Alternativos / Exceções
- FA01 — Estoque insuficiente: venda não realizada.
- FA02 — Cliente não cadastrado: realiza cadastro rápido.
- FA03 — Receita inválida: venda não autorizada.
- FA04 — Cliente inadimplente: venda bloqueada.

### Relacionamentos
- **Include:** Consultar Produto, Identificar Cliente
- **Extend:** Venda a Prazo, Validar Receita

### Diagrama de Atividades
<img width="938" height="716" alt="uc01_realizar_venda" src="https://github.com/user-attachments/assets/3ab4ba8e-e46a-4765-a907-d0218fe376cb" />

---

## UC02 — Consultar Produto
**Ator(es):** Atendente, Gerente
**Descrição:** Permite buscar produtos por nome, código de barras ou fabricante.
**Pré-condições:** Produto cadastrado.
**Pós-condições:** Produto localizado e exibido.

### Fluxo Principal
1. Usuário informa critério de busca.
2. Sistema exibe lista de produtos encontrados.

### Fluxos Alternativos / Exceções
- FA01 — Produto não encontrado: exibe mensagem.

### Relacionamentos
- **Extend:** Realizar Venda

### Diagrama de Atividades
<img width="522" height="361" alt="uc02_consultar_produto" src="https://github.com/user-attachments/assets/6aa87757-3160-42eb-b638-5fae2547ddf5" />

---

## UC03 — Identificar/Cadastrar Cliente
**Ator(es):** Atendente
**Descrição:** Identifica cliente existente ou realiza cadastro rápido.
**Pré-condições:** Cliente não identificado.
**Pós-condições:** Cliente identificado ou cadastrado.

### Fluxo Principal
1. Atendente solicita identificação do cliente.
2. Se não cadastrado, realiza cadastro rápido.

### Fluxos Alternativos / Exceções
- FA01 — Dados insuficientes: cadastro não realizado.

### Relacionamentos
- **Extend:** Realizar Venda

### Diagrama de Atividades
<img width="515" height="371" alt="uc03_identificar_cadastrar_cliente" src="https://github.com/user-attachments/assets/2260b625-c5c3-4339-8372-06ebef5611a2" />

---

## UC04 — Registrar Compra de Produtos
**Ator(es):** Gerente
**Descrição:** Registra compra de produtos junto a fornecedores e atualiza estoque.
**Pré-condições:** Produto cadastrado, fornecedor cadastrado.
**Pós-condições:** Estoque atualizado, conta a pagar criada.

### Fluxo Principal
1. Gerente seleciona fornecedor e produtos.
2. Informa quantidade e valor.
3. Confirma compra.
4. Sistema atualiza estoque e gera conta a pagar.

### Fluxos Alternativos / Exceções
- FA01 — Produto não cadastrado: impede compra.

### Relacionamentos
- **Include:** Atualizar Estoque
- **Extend:** Gerar Conta a Pagar

### Diagrama de Atividades
<img width="354" height="415" alt="uc04_registrar_compra_produtos" src="https://github.com/user-attachments/assets/dbf02a07-3def-45fa-b3ac-98f75c609716" />

---

## UC05 — Atualizar Estoque
**Ator(es):** Gerente
**Descrição:** Atualiza estoque após vendas, compras, devoluções ou perdas.
**Pré-condições:** Operação registrada.
**Pós-condições:** Estoque atualizado.

### Fluxo Principal
1. Sistema identifica operação (venda, compra, devolução, perda).
2. Atualiza quantidade em estoque.

### Fluxos Alternativos / Exceções
- FA01 — Produto não cadastrado: operação não realizada.

### Relacionamentos
- **Extend:** Registrar Compra de Produtos, Realizar Venda

### Diagrama de Atividades
<img width="450" height="253" alt="uc05_atualizar_estoque" src="https://github.com/user-attachments/assets/0dd38933-cad8-4268-a5c0-334a33fe954f" />

---

## UC06 — Gerar Conta a Pagar
**Ator(es):** Financeiro
**Descrição:** Gera lançamento de contas a pagar após compras ou despesas.
**Pré-condições:** Compra ou despesa registrada.
**Pós-condições:** Conta a pagar criada.

### Fluxo Principal
1. Sistema registra valor, data de vencimento e status.
2. Exibe conta a pagar em aberto.

### Fluxos Alternativos / Exceções
- FA01 — Dados incompletos: não gera conta.

### Relacionamentos
- **Include:** Registrar Compra de Produtos

### Diagrama de Atividades
<img width="394" height="253" alt="uc06_gerar_conta_pagar" src="https://github.com/user-attachments/assets/655ef8e6-fc2f-4cf5-a93c-cdb356916e51" />

---

## UC07 — Gerar Conta a Receber
**Ator(es):** Financeiro
**Descrição:** Gera lançamento de contas a receber após vendas a prazo.
**Pré-condições:** Venda a prazo realizada.
**Pós-condições:** Conta a receber criada.

### Fluxo Principal
1. Sistema registra valor, data de vencimento e status.
2. Exibe conta a receber em aberto.

### Fluxos Alternativos / Exceções
- FA01 — Dados incompletos: não gera conta.

### Relacionamentos
- **Include:** Realizar Venda

### Diagrama de Atividades
<img width="403" height="253" alt="uc07_gerar_conta_receber" src="https://github.com/user-attachments/assets/eb8158da-8625-4ac2-b534-745215f732d7" />

---

## UC08 — Emitir Comprovante de Venda
**Ator(es):** Atendente
**Descrição:** Emite comprovante detalhado após finalização da venda.
**Pré-condições:** Venda realizada.
**Pós-condições:** Comprovante emitido.

### Fluxo Principal
1. Sistema gera comprovante com detalhes da venda.
2. Entrega ao cliente.

### Fluxos Alternativos / Exceções
- FA01 — Falha na impressão: reemite comprovante.

### Relacionamentos
- **Include:** Realizar Venda

### Diagrama de Atividades
<img width="361" height="336" alt="uc08_emitir_comprovante_venda" src="https://github.com/user-attachments/assets/22f453a1-4bc0-486b-8f8e-25bd49a59af6" />

---

## UC09 — Gerar Relatórios
**Ator(es):** Gerente, Financeiro
**Descrição:** Gera relatórios de vendas, estoque e contas.
**Pré-condições:** Dados disponíveis.
**Pós-condições:** Relatório gerado.

### Fluxo Principal
1. Usuário seleciona tipo de relatório.
2. Sistema gera e exibe relatório.

### Fluxos Alternativos / Exceções
- FA01 — Falha na geração: exibe mensagem.

### Relacionamentos
- **Extend:** Todas as operações principais

### Diagrama de Atividades
<img width="327" height="307" alt="uc09_gerar_relatorios" src="https://github.com/user-attachments/assets/0bc9d432-cfb1-4d8e-bcc2-ab216890516b" />

---

## UC10 — Gerenciar Usuários e Permissões
**Ator(es):** Administrador
**Descrição:** Cadastra, edita e remove usuários e define permissões.
**Pré-condições:** Usuário autenticado como administrador.
**Pós-condições:** Usuários e permissões atualizados.

### Fluxo Principal
1. Administrador acessa módulo de usuários.
2. Cadastra, edita ou remove usuários.
3. Define permissões por perfil.

### Fluxos Alternativos / Exceções
- FA01 — Permissão insuficiente: operação negada.

### Relacionamentos
- **Extend:** Todas as operações restritas

### Diagrama de Atividades
<img width="447" height="361" alt="uc10_gerenciar_usuarios_permissoes" src="https://github.com/user-attachments/assets/e7df644b-d38a-4996-a5ea-28b37a039bea" />

---

## UC11 — Transferir Estoque
**Ator(es):** Gerente
**Descrição:** Permite transferir produtos entre unidades da farmácia.
**Pré-condições:** Estoque disponível na unidade de origem.
**Pós-condições:** Estoque atualizado nas duas unidades.

### Fluxo Principal
1. Gerente seleciona unidade de origem e destino.
2. Informa produtos e quantidades.
3. Confirma transferência.
4. Sistema atualiza estoques.

### Fluxos Alternativos / Exceções
- FA01 — Estoque insuficiente: operação não realizada.
- FA02 — Unidade de destino inválida: operação não realizada.

### Relacionamentos
- **Include:** Atualizar Estoque

### Diagrama de Atividades
<img width="390" height="415" alt="uc11_transferir_estoque" src="https://github.com/user-attachments/assets/4794b895-d9f7-4d19-922a-e9324346e1de" />

---

## UC12 — Validar Receita
**Ator(es):** Farmacêutico
**Descrição:** Valida receitas médicas para venda de produtos controlados.
**Pré-condições:** Receita apresentada pelo cliente.
**Pós-condições:** Venda autorizada ou negada.

### Fluxo Principal
1. Farmacêutico recebe receita.
2. Verifica autenticidade e validade.
3. Autoriza ou nega venda.

### Fluxos Alternativos / Exceções
- FA01 — Receita inválida: venda negada.
- FA02 — Produto não controlado: validação não necessária.

### Relacionamentos
- **Extend:** Realizar Venda

### Diagrama de Atividades
<img width="258" height="307" alt="uc12_validar_receita" src="https://github.com/user-attachments/assets/7fb43fe4-686d-477e-b8f5-ac33e87cfab2" />

---
