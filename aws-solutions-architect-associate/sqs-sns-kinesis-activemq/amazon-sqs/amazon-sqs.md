---
layout: home
title: Amazon SQS – Standard Queue - AWS Solutions Architect Associate
---

# Amazon SQS – Standard Queue

- É a oferta mais antiga da AWS (mais de 10 anos)
- Serviço totalmente gerenciado, usado para **desacoplar aplicações**

## Atributos

- Throughput ilimitado, quantidade ilimitada de mensagens na fila
- Retenção padrão das mensagens: 4 dias, máximo de 14 dias
- Baixa latência (<10 ms para publicar e receber)
- Limitação de 1.024 KB por mensagem enviada

## Comportamento

- Pode haver mensagens duplicadas (entrega "at least once", ocasionalmente)
- Pode haver mensagens fora de ordem (ordenação "best effort")

---

# SQS com Auto Scaling Group (ASG)

Esse diagrama mostra um padrão comum de arquitetura onde o **SQS** é usado como gatilho para escalar automaticamente instâncias **EC2** através de um **Auto Scaling Group**, com base no tamanho da fila.

## Fluxo do diagrama

1. **SQS Queue** — a fila armazena as mensagens a serem processadas.
2. **EC2 Instances** — as instâncias fazem *poll* (consultam) a fila continuamente em busca de novas mensagens para processar.
3. **CloudWatch Metric – Queue Length** — o CloudWatch monitora a métrica `ApproximateNumberOfMessages`, que indica quantas mensagens estão aguardando na fila.
4. **CloudWatch Alarm** — quando essa métrica ultrapassa um limite definido (breach), um alarme é disparado.
5. **Auto Scaling Group** — o alarme aciona o ASG, que então **escala** (aumenta) o número de instâncias EC2 para dar conta do aumento de mensagens na fila.

## Ideia central

Quanto mais mensagens se acumulam na fila, mais processamento é necessário. Em vez de manter um número fixo de instâncias EC2 rodando o tempo todo, o CloudWatch monitora o tamanho da fila e aciona o Auto Scaling Group para adicionar mais instâncias sob demanda — e, quando a fila diminui, o mesmo mecanismo pode ser usado para reduzir o número de instâncias.

Esse padrão é muito usado para processamento assíncrono e para lidar com picos de demanda de forma elástica e econômica, sem precisar de intervenção manual.

---

# Amazon SQS – Segurança

## Criptografia

- **Em trânsito (in-flight)**: usando a API via HTTPS
- **Em repouso (at-rest)**: usando chaves do KMS
- **Do lado do cliente (client-side)**: caso o cliente queira realizar a criptografia/descriptografia por conta própria

## Controle de Acesso

- Políticas do **IAM** para regular o acesso à API do SQS

## Políticas de Acesso do SQS

Semelhantes às bucket policies do S3:

- Úteis para acesso *cross-account* (entre contas diferentes) às filas do SQS
- Úteis para permitir que outros serviços (SNS, S3...) escrevam em uma fila do SQS

---

[← Voltar para SQS, SNS, Kinesis, Active MQ](../sqs-sns-kinesis-activemq.html)
