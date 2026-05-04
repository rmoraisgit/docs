---
layout: home
title: Diferenças entre Scaling Up e Scaling Out
---

# Scaling: Up vs Out

## O que é Scaling?

Scaling (ou escalabilidade) é a capacidade de um sistema de aumentar sua capacidade para lidar com mais carga ou demanda. Existem duas abordagens principais: **Scaling Up** (vertical) e **Scaling Out** (horizontal).

---

## Scaling UP (Escalonamento Vertical)

O **Scaling Up** consiste em aumentar os recursos de uma **única máquina** existente, tornando-a mais poderosa.

### Como funciona

Você pega um servidor (ex: instância EC2 na AWS) com uma aplicação rodando sobre um sistema operacional Linux e substitui por uma máquina com mais:

- **CPU** — processador mais rápido ou com mais núcleos
- **Disco** — maior capacidade de armazenamento
- **Memória RAM** — mais memória disponível
- **Rede** — maior largura de banda

### Estrutura típica

```
[ APP ]
[ Linux OS ]
[ CPU | Disk | RAM | NIC ]
```

### Vantagens
- Simplicidade — não exige mudanças na arquitetura da aplicação
- Fácil de implementar inicialmente
- Sem necessidade de gerenciar múltiplos servidores

### Desvantagens
- Tem um **limite físico** — não dá para aumentar indefinidamente
- Ponto único de falha (single point of failure)
- Geralmente mais caro a longo prazo
- Downtime necessário para upgrades de hardware

---

## Scaling OUT (Escalonamento Horizontal)

O **Scaling Out** consiste em adicionar **mais máquinas** ao sistema, distribuindo a carga entre elas.

### Como funciona

Em vez de melhorar um único servidor, você replica a mesma instância várias vezes. Cada nó possui:

- A mesma aplicação (**APP**)
- O mesmo sistema operacional (**Linux**)
- Recursos de hardware similares (CPU, Disk, RAM, NIC)

### Estrutura típica

```
[ APP ]       [ APP ]       [ APP ]
[ Linux ]     [ Linux ]     [ Linux ]
[ CPU|Disk ]  [ CPU|Disk ]  [ CPU|Disk ]
    Nó 1          Nó 2          Nó 3
```

### Vantagens
- **Alta disponibilidade** — se um nó falhar, os outros continuam
- **Escalabilidade quase ilimitada** — basta adicionar mais nós
- Melhor para lidar com picos de tráfego
- Custo mais previsível (máquinas menores e mais baratas)

### Desvantagens
- Maior complexidade arquitetural
- Exige balanceamento de carga (load balancer)
- A aplicação precisa ser stateless ou suportar distribuição de estado

---

## Comparação Resumida

| Critério              | Scaling UP (Vertical) | Scaling OUT (Horizontal) |
|-----------------------|-----------------------|--------------------------|
| Estratégia            | Máquina maior         | Mais máquinas            |
| Limite                | Físico (hardware)     | Quase ilimitado          |
| Custo                 | Alto a longo prazo    | Mais previsível          |
| Disponibilidade       | Ponto único de falha  | Alta disponibilidade     |
| Complexidade          | Baixa                 | Alta                     |
| Mudança na aplicação  | Não necessária        | Pode ser necessária      |

---

## Quando usar cada um?

- **Scaling Up** → Ideal para fases iniciais, bancos de dados relacionais ou sistemas legados difíceis de distribuir.
- **Scaling Out** → Ideal para aplicações web modernas, microserviços e sistemas que precisam de alta disponibilidade e resiliência.

> 💡 **Dica:** Em ambientes de nuvem como AWS, Azure ou GCP, ambas as estratégias podem ser combinadas para obter o melhor dos dois mundos.
