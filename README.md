# AWS Case Study: Arquitetura Escalável e Resiliente (ELB & Auto Scaling) ☁️🚀

Este repositório documenta a implementação de uma infraestrutura automatizada na AWS, focada em **Alta Disponibilidade** e **Elasticidade**. O projeto demonstra como transitar de um modelo de servidor único (ponto único de falha) para uma arquitetura resiliente que se autogerencia.

Projeto realizado como parte da minha jornada de especialização na **Escola da Nuvem**.

---

## 📌 Visão Geral
O desafio proposto foi garantir que uma aplicação suporte picos de tráfego sem queda de performance e sem desperdício de custo em momentos ociosos. Para isso, utilizei o **Elastic Load Balancing (ELB)** para distribuir a carga e o **Amazon EC2 Auto Scaling** para gerenciar a frota de instâncias.

### 🏗️ Arquitetura do Projeto
Abaixo, o arco de resiliência que sustenta a operação, integrando monitoramento e escalonamento automático:

![Arco de Resiliência](Diagrama%20de%20Arquitetura%20de%20Nuvem%20-%20visual%20selection.png)

---

## 🛠️ Tecnologias e Serviços Utilizados
* **Computação:** Amazon EC2 (Instâncias t3.micro).
* **Imagens:** Amazon Machine Images (AMI) para padronização.
* **Rede:** VPC com Sub-redes Públicas (Load Balancer) e Privadas (Instâncias).
* **Escalabilidade:** AWS Auto Scaling & Application Load Balancer (ALB).
* **Monitoramento:** Amazon CloudWatch (Métricas de CPU e Alarmes).

---

## 📝 Ciclo de Implementação

### 1. Padronização com AMI
O primeiro passo foi criar a `MercadoLibre-AMI` a partir de uma instância pré-configurada. Isso garante que o Auto Scaling sempre lance clones idênticos e prontos para produção, evitando configurações manuais e erros de ambiente.

![Catálogo de AMI](CatalogoAMI.png)

### 2. Infraestrutura de Balanceamento (ELB)
Configurei o **LabELB** em duas Zonas de Disponibilidade para eliminar qualquer ponto único de falha. O tráfego externo chega ao balanceador e é distribuído para o Target Group.
* **Target Group:** Criado para registrar dinamicamente as instâncias.
* **Listeners:** Configurados na porta 80 (HTTP) para encaminhamento eficiente.

![Mapa de Recursos](Mapa%20de%20Recursos.png)
![Listeners](Listeners.png)

### 3. Automação e Elasticidade (ASG)
Configurei o **Auto Scaling Group** utilizando um Launch Template. Defini políticas de escalabilidade para manter o equilíbrio entre performance e custo:
* **Capacidade Desejada:** 2 instâncias.
* **Cap
