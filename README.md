# AWS Case Study: Arquitetura Escalável e Resiliente (ELB & Auto Scaling) ☁️🚀

Este repositório documenta a implementação de uma infraestrutura automatizada na AWS, focada em **Alta Disponibilidade** e **Elasticidade**. O projeto demonstra a transição de um servidor estático para uma arquitetura resiliente que se autogerencia conforme a demanda.

Projeto realizado como parte da minha jornada de especialização na **Escola da Nuvem**.

---

## 📌 Visão Geral
O desafio foi garantir que uma aplicação suporte picos de tráfego sem queda de performance e sem desperdício de custo em momentos ociosos. Para isso, utilizei o **Elastic Load Balancing (ELB)** para distribuir a carga e o **Amazon EC2 Auto Scaling** para gerenciar a frota de instâncias.

---

## 🛠️ Tecnologias e Serviços Utilizados
* **Computação:** Amazon EC2 (Instâncias t3.micro).
* **Imagens:** Amazon Machine Images (AMI) para padronização.
* **Rede:** VPC com Sub-redes Públicas e Privadas.
* **Escalabilidade:** AWS Auto Scaling & Application Load Balancer (ALB).
* **Monitoramento:** Amazon CloudWatch (Métricas de CPU e Alarmes).

---

## 📝 Ciclo de Implementação

### 1. Padronização e Infraestrutura Base
O primeiro passo foi a criação da `MercadoLibre-AMI` para garantir que todos os nós da frota fossem idênticos. Em seguida, configurei o **ALB** e os **Listeners** para gerenciar a porta 80 (HTTP).

![Mapa de Recursos](/img/MapaRecursos.png)
![Catálogo de AMI](/img/CatalogoAMI.png)

### 2. Provisionamento do Estado Inicial (Mínimo)
Ao configurar o Auto Scaling Group com a capacidade desejada de 2 instâncias, a AWS inicia o provisionamento automático para garantir a alta disponibilidade mínima.

| 1. Criando Instâncias Mínimas | 2. Estado Íntegro (2 Instâncias) |
| :--- | :--- |
| ![Criando Mínimo](/img/CriandoMinimo.png) | ![Mínimo Criado](/img/MinimoCriado.png) |

---

## 🧪 Validação: Teste de Stress e Escalonamento Vertical
Abaixo, a sequência real de como a infraestrutura reagiu a um cenário de alta demanda.

### Passo 01: O Gatilho (Stress Test)
Utilizei a ferramenta de teste de carga para elevar a utilização da CPU para **78%**, simulando um pico repentino de usuários.
![Load Test](/img/LoadTest.png)

### Passo 02: A Detecção (CloudWatch)
O alarme monitorado pelo CloudWatch detectou que a média de CPU ultrapassou o limite de 50%, mudando o estado para **"Em Alarme"**.
![Alerta CloudWatch](/img/Alerta.png)

### Passo 03: A Reação (Scale-Out)
O Auto Scaling Group identificou o alarme e, seguindo a política de escalabilidade, provisionou automaticamente mais instâncias para dividir o processamento. O resultado final foi a frota expandida para **4 instâncias ativas**.
![Frota Expandida](/img/LoadFuncionando.png)

---

## 🎯 Conclusão e Resultados
Este laboratório validou pilares essenciais do AWS Well-Architected Framework:
* ✅ **Confiabilidade:** Redundância geográfica em múltiplas AZs.
* ✅ **Eficiência:** Escalonamento automático (Scale-out/Scale-in) baseado em métricas reais.
* ✅ **Segurança:** Instâncias isoladas em sub-redes privadas, protegidas de acesso direto.

---
**Conecte-se comigo:**
* [LinkedIn](https://www.linkedin.com/in/thiagobarbosacarneiro/)

---
*Documentação técnica por Thiago Barbosa Carneiro - 2026*
