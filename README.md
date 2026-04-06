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
* **Capacidade Mínima:** 2 | **Capacidade Máxima:** 4.
* **Política de Scaling:** Alvo de **50% de uso de CPU**.

![Definição de Tamanhos](Definindo%20os%20tamanhos.png)
![Limites Mínimos](Minimos.png)

---

## 🧪 Validação: O Teste de Stress
Para provar a resiliência da arquitetura, realizei um teste de carga real na CPU para forçar o escalonamento horizontal:

1. **O Gatilho:** Através de um script de stress, a carga de CPU foi elevada para **78%**.
2. **O Alarme:** O CloudWatch detectou que o limite de 50% foi ultrapassado e mudou o estado do alarme para **"Em Alarme"**.
3. **A Reação:** O Auto Scaling reagiu imediatamente ao sinal do CloudWatch, lançando novas instâncias (`Lab Instance`) para dividir a carga.
4. **O Resultado:** A aplicação permaneceu online e estável durante todo o processo de alta demanda.

| Status do Alarme (CPU > 50%) | Escalonamento em Tempo Real |
| :--- | :--- |
| ![Alarme CloudWatch](O%20alerta.png) | ![Load Funcionando](Load%20funcionando.png) |

> **Evidência do aumento de carga:**
> ![Teste de Carga](teste%20de%20load.png)

---

## 🎯 Conclusão e Resultados
Este laboratório validou habilidades fundamentais para a operação de infraestruturas modernas:
* ✅ **Tolerância a Falhas:** Redundância geográfica em múltiplas zonas (AZs).
* ✅ **Eficiência de Custo:** Pagamento apenas pelo recurso necessário através de Scale-in/Scale-out.
* ✅ **Segurança:** Instâncias isoladas em sub-redes privadas, protegidas do acesso direto via internet.

---
**Conecte-se comigo:**
* [LinkedIn](https://www.linkedin.com/in/thiago-barbosa-carneiro/)
* [Meu Perfil na Escola da Nuvem](https://escoladanuvem.org/)

---
*Projeto documentado por Thiago Barbosa Carneiro - 2026*
