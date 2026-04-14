# 📊 Data Quality — Projeto Pedágios Federais

Este documento registra a análise inicial de qualidade dos dados utilizados no projeto, descrevendo estrutura, problemas encontrados, necessidades de tratamento e riscos associados a cada dataset.

---

## 🟦 1. Dataset: dados-dos-pracas-de-pedagio2_2026

### ✔ Descrição
Contém informações cadastrais das praças de pedágio:
- Nome da praça
- Concessionária
- Localização (cidade/UF ou coordenadas)

### ✔ Pontos verificados
- Estrutura simples e consistente
- Campos textuais bem definidos
- Não há valores numéricos críticos

### ⚠ Problemas identificados
- Possível variação nos nomes das praças entre datasets
- Possível ausência de coordenadas geográficas (dependendo da fonte)
- Necessidade de padronização dos nomes das concessionárias

### 🛠 Ações recomendadas
- Criar tabela de referência (dimensão) com nomes padronizados
- Validar se todas as praças aparecem no dataset de tráfego

---

## 🟩 2. Dataset: receita_de_pedagio

### ✔ Descrição
Contém receita anual por concessionária:
- Concessionária
- Ano
- Valor da receita (em reais)

### ✔ Pontos verificados
- Estrutura simples
- Dados anuais consolidados

### ⚠ Problemas identificados
- Coluna de valores sem formatação (ex.: 150533000)
- Necessidade de conversão para formato monetário
- Possível ausência de casas decimais explícitas

### 🛠 Ações recomendadas
- Converter valores para R$ 000.000.000,00
- Validar se o valor está em reais (confirmado pelo dicionário)
- Criar coluna formatada no Power BI ou no ETL

---

## 🟧 3. Dataset: volume-trafego-equivalente-praca-pedagio-2025_mensal_consolidado

### ✔ Descrição
Dataset mais robusto, contendo:
- Concessionária
- Praça
- Categoria de veículo (eixos)
- Tipo de cobrança (manual, TAG, OCR)
- volume_total (quantidade de veículos)
- VEQ (veículos equivalentes)

### ✔ Pontos verificados
- volume_total representa **quantidade real de veículos**
- VEQ representa impacto financeiro (multiplicador por categoria)
- Estrutura rica para análises de tráfego

### ⚠ Problemas identificados
- Dúvida sobre granularidade (mensal ou diária)
  → Nome do arquivo indica **mensal**, mas precisa confirmar no dicionário
- Possível inconsistência nos nomes das praças
- Dataset grande (pode exigir otimização no Power BI)

### 🛠 Ações recomendadas
- Confirmar granularidade no dicionário oficial
- Padronizar nomes de praças e concessionárias
- Criar tabela de relacionamento (dim_praca)
- Criar medidas DAX para:
  - Volume total por praça
  - VEQ total
  - Percentual por tipo de cobrança

---

## ⭐ 4. Riscos e Observações Gerais

### ⚠ Riscos
- Divergência de nomes entre datasets pode quebrar relacionamentos
- Valores monetários mal formatados podem gerar erros de cálculo
- Granularidade incorreta pode distorcer KPIs

### ✔ Oportunidades
- VEQ permite projeções financeiras
- Tipo de cobrança permite KPIs modernos (TAG vs manual)
- Localização das praças permite mapas e análises geográficas

---

## 🧭 5. Próximos Passos

1. Validar granularidade do dataset de tráfego  
2. Padronizar nomes de praças e concessionárias  
3. Criar modelo relacional no Power BI  
4. Criar medidas DAX para KPIs  
5. Documentar transformações no CHANGELOG

---

**Documento atualizado em:** 14/04/2026  
**Responsável:** Jefferson Soares Silva Novaes

