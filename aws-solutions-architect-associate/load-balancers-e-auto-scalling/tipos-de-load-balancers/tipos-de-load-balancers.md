---
layout: home
title: Tipos de Load Balancers - AWS Solutions Architect Associate
---

# 🔀 Tipos de Load Balancers

Nesta seção, exploramos os diferentes tipos de Load Balancers disponíveis na AWS e suas características específicas.

## 📚 Conteúdo

# ALB vs NLB na AWS

## Camada de operação

**ALB (Application Load Balancer)** opera na **camada 7** (aplicação) — entende HTTP/HTTPS, cabeçalhos, paths, cookies e host headers.

**NLB (Network Load Balancer)** opera na **camada 4** (transporte) — trabalha com TCP/UDP/TLS, sem inspecionar o conteúdo da requisição.

---

## Comparativo direto

| Característica | ALB | NLB |
|---|---|---|
| Camada OSI | 7 (HTTP/HTTPS) | 4 (TCP/UDP/TLS) |
| Performance | Alta, mas com latência maior | Latência ultrabaixa (~microsegundos) |
| IP estático | ❌ (IP muda) | ✅ (IP fixo por AZ) |
| Roteamento | Path, host, headers, query string | Porta + protocolo |
| WebSocket | ✅ | ✅ |
| gRPC | ✅ | ❌ |
| Preserve client IP | Via X-Forwarded-For | ✅ nativo |
| Targets | EC2, ECS, Lambda, IPs | EC2, ECS, IPs, ALB |
| Preço | Maior | Menor |

---

## Casos de uso

### Use ALB quando:
- Aplicações web com múltiplos serviços/microserviços (roteamento por `/api`, `/auth`, etc.)
- Hospedar vários domínios no mesmo load balancer (host-based routing)
- Autenticação integrada com Cognito ou OIDC
- Aplicações que usam gRPC
- Quando precisar de regras de roteamento complexas
- Redirects HTTP → HTTPS nativos

### Use NLB quando:
- Precisa de **IP fixo** (ex: parceiros que fazem whitelist de IP)
- Aplicações que exigem latência mínima (jogos, trading, streaming)
- Protocolos não-HTTP: TCP puro, UDP, FTP, SMTP
- Preservar o IP real do cliente na camada de rede
- Tráfego muito alto com necessidade de escala extrema
- Expor um ALB com IP estático (NLB na frente do ALB)

---

## Regra geral

> Se é tráfego **web/HTTP** → **ALB**
> Se precisa de **velocidade, IP fixo ou protocolo não-HTTP** → **NLB**


---

[← Voltar para Load Balancers e Auto Scaling](../load-balancers-e-auto-scalling.html)
