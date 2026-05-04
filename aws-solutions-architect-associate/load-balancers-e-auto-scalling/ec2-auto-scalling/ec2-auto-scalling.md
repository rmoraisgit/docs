---
layout: home
title: EC2 Auto Scaling
---

# 🚀 EC2 Auto Scaling

# EC2 Auto Scaling — AWS

## O que é Auto Scaling?

O **EC2 Auto Scaling** é um serviço da AWS que ajusta automaticamente o número de instâncias EC2 em execução de acordo com a demanda da aplicação. Ele garante que você tenha a quantidade certa de recursos disponíveis — nem de mais (custo desnecessário), nem de menos (queda de performance).

O Auto Scaling atua no eixo **OUT** (horizontal): adiciona ou remove instâncias conforme necessário.

---

## Componentes principais

### 1. EC2 Launch Template (Template de Lançamento)

É o "molde" que define como cada nova instância EC2 deve ser criada. Nele você configura:

- AMI (imagem do sistema operacional)
- Tipo de instância (ex: t3.micro, m5.large)
- Par de chaves SSH
- Security Groups
- Scripts de inicialização (User Data)

> Toda vez que o Auto Scaling precisar subir uma nova instância, ele seguirá as definições do Launch Template.

---

### 2. Auto Scaling Group (ASG)

É o grupo que gerencia o conjunto de instâncias. Você define:

- **Capacidade mínima** — número mínimo de instâncias sempre ativas
- **Capacidade desejada** — número ideal em condições normais
- **Capacidade máxima** — limite superior de instâncias permitidas

O ASG distribui as instâncias entre diferentes **sub-redes (subnets)** para garantir alta disponibilidade.

---

### 3. Subnets / Zonas de Disponibilidade

O Auto Scaling distribui as instâncias entre múltiplas subnets em zonas de disponibilidade distintas:

```
Sub_A (us-east-1a)         Sub_B (us-east-1b)
┌──────────────────┐       ┌──────────────────┐
│  [1A] [1B] [1C]  │       │  [2A] [2B] [  ]  │
│       ↑ 3x       │       │       ↑ 2x        │
└──────────────────┘       └──────────────────┘
```

Isso garante que, se uma zona falhar, as instâncias na outra zona continuam atendendo.

---

### 4. Amazon CloudWatch

O **CloudWatch** é o serviço de monitoramento que "escuta" as métricas das instâncias (CPU, memória, rede, etc.) e dispara os eventos de scaling.

Exemplos de políticas baseadas em CPU:

| Condição        | Ação                          |
|-----------------|-------------------------------|
| CPU **≥ 70%**   | **Scale Out** — adiciona instâncias |
| CPU **< 70%**   | **Scale In** — remove instâncias   |

---

## Fluxo de funcionamento

```
┌─────────────────────────────────────────────────────────┐
│                    AUTO SCALING GROUP                    │
│                                                         │
│  Sub_A                         Sub_B                    │
│  ┌──────────────┐              ┌──────────────┐         │
│  │ [1A][1B][1C] │              │ [2A][2B][  ] │         │
│  └──────────────┘              └──────────────┘         │
│           ↑                           ↑                  │
│           └──────────────┬────────────┘                  │
│                          │                               │
│               ┌──────────────────┐                      │
│               │   CloudWatch     │                      │
│               │  CPU ≥ 70% → +1  │                      │
│               │  CPU < 70% → -1  │                      │
│               └──────────────────┘                      │
│                          ↑                               │
│               ┌──────────────────┐                      │
│               │  Launch Template │                      │
│               │  (EC2 config)    │                      │
│               └──────────────────┘                      │
└─────────────────────────────────────────────────────────┘
```

**Passo a passo:**

1. O CloudWatch monitora continuamente as métricas das instâncias no ASG
2. Quando a CPU ultrapassa 70%, o CloudWatch dispara um alarme
3. O ASG recebe o alarme e aciona o **Scale Out** — cria novas instâncias usando o Launch Template
4. As novas instâncias são distribuídas entre Sub_A e Sub_B
5. Quando a CPU cai abaixo de 70%, o ASG realiza **Scale In** — termina instâncias excedentes

---

## Tipos de Scaling

| Tipo                     | Descrição                                                                 |
|--------------------------|---------------------------------------------------------------------------|
| **Scale Out**            | Aumenta o número de instâncias (mais performance/capacidade)              |
| **Scale In**             | Diminui o número de instâncias (redução de custo)                        |
| **Scaling por Política** | Baseado em métricas do CloudWatch (CPU, latência, etc.)                  |
| **Scaling Programado**   | Ajuste em horários específicos (ex: mais instâncias de manhã)             |
| **Scaling Preditivo**    | Usa ML para prever demanda e escalar antecipadamente                      |

---

## Benefícios do Auto Scaling

- ✅ **Alta disponibilidade** — instâncias em múltiplas zonas
- ✅ **Elasticidade** — adapta-se automaticamente à demanda
- ✅ **Redução de custos** — paga apenas pelo que usa
- ✅ **Tolerância a falhas** — substitui instâncias com problemas automaticamente
- ✅ **Sem intervenção manual** — tudo gerenciado pelo CloudWatch + ASG

---

## Resumo Visual

```
Baixa demanda:    [1A][1B]          → 2 instâncias ativas
Alta demanda:     [1A][1B][1C][2A][2B] → 5 instâncias ativas
CPU volta ao normal → ASG remove as excedentes
```

> 💡 **Dica:** Combine o Auto Scaling com um **Elastic Load Balancer (ELB)** para distribuir o tráfego igualmente entre todas as instâncias do grupo.
