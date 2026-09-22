# ☕ Arquitetura Serverless para Relatório Automatizado de Vendas na AWS

## 📌 Visão Geral do Projeto
Este projeto consiste na implementação de uma solução **Serverless e Orientada a Eventos (Event-Driven Architecture)** na AWS para automação e geração diária de relatórios de vendas de uma empresa fictícia (Café). 

A arquitetura extrai dados de vendas de um banco de dados **MySQL** hospedado em uma instância EC2 privada, formata os dados consolidados e dispara notificações por e-mail para os gestores através do **Amazon SNS**.

---

## 📐 Arquitetura da Solução

```text
[ CloudWatch Event / Cron ]
           │
           ▼
[ Lambda Orchestrator ] ────► [ Systems Manager (Parameter Store) ]
   (salesAnalysisReport)                    │ (Busca Credenciais)
           │                                ▼
           ├──────────────────► [ Lambda Data Extractor ]
           │                       (salesAnalysisReportDataExtractor)
           │                                │ (Consulta SQL na Porta 3306)
           │                                ▼
           │                      [ EC2 / MySQL Database ]
           │                         (Cafe VPC - Private)
           ▼
[ Amazon SNS Topic ]
  (SalesReportTopic)
           │
           ▼
[ Email Administrator ]


