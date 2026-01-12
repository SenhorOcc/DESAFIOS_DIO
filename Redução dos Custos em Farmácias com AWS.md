# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

**Data:** 12 de janeiro de 2026

**Empresa:** Farmácia Revendedora Saúde Ltda.

**Responsável:** Pedro

---

## 1. Introdução

Este relatório descreve a proposta de implementação de serviços AWS para a Farmácia Revendedora Saúde Ltda., com o objetivo principal de reduzir custos operacionais e de infraestrutura, aumentar a resiliência e melhorar a agilidade na entrega de serviços para clientes (farmácias revendedoras). O escopo foca em soluções de armazenamento, computação sem servidor e banco de dados escalável, priorizando redução de custo por consumo, automação e eliminação de infraestrutura ociosa.

## 2. Objetivo do projeto

Selecionar e justificar três serviços AWS que promovam redução imediata e contínua de custos, além de identificar ganhos operacionais e impactos esperados sobre processos de negócio (vendas, inventário, faturamento e distribuição).

## 3. Descrição do Projeto — Etapas

### Etapa 1 — Amazon S3 (Simple Storage Service)

**Foco da ferramenta:** Armazenamento escalável, durável, com políticas de ciclo de vida e classes de custo para otimização financeira.

**Descrição de caso de uso:**

* Migrar backups, arquivos de notas fiscais eletrônicas (XML), relatórios de vendas e arquivos de integração para buckets S3.
* Aplicar políticas de lifecycle (transição para S3 Intelligent‑Tiering e S3 Glacier) para dados históricos e backups.
* Utilizar S3 como repositório de entrega dos resultados de processamento (CSV, relatórios, artefatos) para clientes.

**Redução de custos:**

* Eliminam-se custos fixos de armazenamento on‑premise (energia, manutenção, reposição de hardware).
* Paga‑se apenas pelo uso (GB armazenado + requests/egress) e reduz custo com classes de armazenamento otimizadas para dados frios.

**Principal ganho para a empresa:** Armazenamento acessível, seguro e resiliente com políticas que minimizam custo do dado ao longo do tempo e facilitam recuperação de desastres.

---

### Etapa 2 — AWS Lambda (computação serverless) + Amazon EventBridge / Step Functions

**Foco da ferramenta:** Execução de código sob demanda, sem gerenciamento de servidores. Orquestração de processos event‑driven.

**Descrição de caso de uso:**

* Automatizar processamento de pedidos, transformações de arquivos (ex.: gerar PDF de notas fiscais), integração entre sistemas (ERP das farmácias clientes) e envio de notificações.
* Executar processos de faturamento noturno e rotinas de conciliação apenas quando eventos ocorram (push para S3, fila SNS/SQS, eventos do banco).

**Redução de custos:**

* Remoção de servidores dedicados para tarefas esporádicas (sem custos de instância ociosa). Pagamento por tempo de execução e memória.
* Melhor utilização de recursos em picos e vales sem provisionamento excessivo.

**Principal ganho para a empresa:** Agilidade na automação, menor custo operacional e manutenção, escalabilidade automática para picos de processamento.

---

### Etapa 3 — Amazon Aurora Serverless v2 (ou Amazon RDS com opções serverless)

**Foco da ferramenta:** Banco de dados relacional totalmente gerenciado com escalabilidade automática e cobrança por capacidade efetivamente utilizada.

**Descrição de caso de uso:**

* Substituir bancos on‑premise ou instâncias RDS super‑dimensionadas que ficam ociosas na maior parte do tempo.
* Utilizar Aurora Serverless para o banco de pedidos, inventário e relatórios analíticos que têm variações sazonais e picos de demanda.

**Redução de custos:**

* Paga‑se por capacidade em uso (ACUs) em vez de manter instâncias provisionadas 24/7.
* Menos despesas com administração, backups gerenciados e alto SLA de disponibilidade.

**Principal ganho para a empresa:** Custos otimizados para cargas variáveis, alta disponibilidade e simplificação da operação do banco de dados.

---

## 4. Conclusão e recomendações

A adoção do Amazon S3, AWS Lambda (com EventBridge/Step Functions) e Amazon Aurora Serverless v2 alinha-se ao objetivo de reduzir custos imediatos e sustentáveis para a farmácia revendedora. Recomenda‑se:

1. Realizar um PoC (prova de conceito) migrando um conjunto de dados e uma rotina batch para S3 + Lambda.
2. Configurar orçamentos e alertas no AWS Cost Explorer e AWS Budgets antes da migração em produção.
3. Aplicar políticas de IAM (princípio do menor privilégio) e criptografia de dados em repouso e trânsito.
4. Avaliar o uso complementar de EC2 Spot para jobs de processamento em lote e CloudFront para aceleração de entregas estáticas.

---

## 5. Anexos

* Plano de migração de arquivos para Amazon S3 (scripts, lifecycle policies e regras de versionamento).
* Exemplo de função Lambda (pseudocódigo) para processamento de arquivo gerado por uma faturação diária.
* Estrutura de escalabilidade e configuração sugerida para Aurora Serverless v2.

---

**Assinatura do Responsável pelo Projeto:**

Pedro
