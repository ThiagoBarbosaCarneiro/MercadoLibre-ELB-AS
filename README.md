# AWS Case Study: Arquitetura Escalável e Resiliente (ELB & Auto Scaling) ☁️🚀

Este repositório documenta a implementação de uma infraestrutura automatizada na AWS, focada em **Alta Disponibilidade** e **Elasticidade**. O projeto demonstra como transitar de um modelo de servidor único para uma arquitetura resiliente que se autogerencia.

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

### 1. Padronização com AMI
O primeiro passo foi criar a `MercadoLibre-AMI` a partir de uma instância pré-configurada, garantindo que novos nós da frota sejam idênticos.

![Catálogo de AMI](/img/CatalogoAMI.png)

### 2. Infraestrutura de Balanceamento (ELB)
Configurei o **ALB** para distribuir o tráfego externo. O mapa de recursos abaixo mostra a integração entre o balanceador e as sub-redes.

![Mapa de Recursos](/img/MapaRecursos.png)

Os **Listeners** foram configurados para ouvir na porta 80 (HTTP) e encaminhar as requisições para o Target Group.

![Listeners](/img/Listeners.png)

### 3. Automação e Elasticidade (ASG)
Configurei o **Auto Scaling Group** com limites de capacidade e políticas de escalonamento baseadas na utilização média de CPU (alvo de 50%).

![Capacidade Mínima](/img/Minimos.png)

---

## 🧪 Validação: O Teste de Stress
Para validar a elasticidade, realizei um teste de carga forçando a utilização da CPU para **78%**.

1. **O Gatilho:** O script de stress elevou o consumo de recursos.
2. **O Alarme:** O CloudWatch detectou o pico e disparou o status **"Em Alarme"**.
3. **A Reação:** O Auto Scaling lançou novas instâncias automaticamente para equilibrar a carga.

| Status do Alarme (CPU > 50%) | Escalonamento em Tempo Real |
| :--- | :--- |
| ![Alarme CloudWatch](/img/Alerta.png) | ![Load Test](/img/LoadTest.png) |

> **Evidência do Teste de Carga:**
> ![Instâncias em Execução](/img/LoadFuncionando.png) 
---

## 🎯 Conclusão e Resultados
Este laboratório validou pilares essenciais do AWS Well-Architected Framework:
* ✅ **Confiabilidade:** Redundância em múltiplas zonas.
* ✅ **Eficiência:** Escalonamento automático (Scale-out/Scale-in).
* ✅ **Segurança:** Instâncias protegidas em sub-redes privadas.

---
**Conecte-se comigo:**
* [LinkedIn](https://www.linkedin.com/in/thiagobarbosacarneiro/)

---
*Documentação técnica por Thiago Barbosa Carneiro - 2026*
