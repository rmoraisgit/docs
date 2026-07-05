---
layout: home
title: Message Visibility Timeout - AWS Solutions Architect Associate
---

# SQS - Message Visibility Timeout

- Depois que uma mensagem é consultada (*polled*) por um consumidor, ela se torna **invisível** para os demais consumidores
- Por padrão, o "message visibility timeout" é de **30 segundos**
- Isso significa que a mensagem tem 30 segundos para ser processada
- Após o fim do visibility timeout, a mensagem volta a ficar "visível" no SQS

## Linha do tempo (diagrama)

1. Um consumidor faz um `ReceiveMessage Request` e a mensagem entra no período de **visibility timeout**
2. Enquanto o timeout está ativo, novas requisições de `ReceiveMessage` feitas por outros consumidores **não recebem** essa mensagem ("Not returned")
3. Se o consumidor original não processar (e não deletar) a mensagem dentro do timeout, ao expirar o prazo a mensagem é **devolvida** à fila ("Message returned")
4. Uma nova requisição de `ReceiveMessage` pode então buscar essa mensagem novamente ("Message returned (again)")

## Pontos importantes

- Se uma mensagem não for processada dentro do visibility timeout, ela **será processada duas vezes**
- Um consumidor pode chamar a API `ChangeMessageVisibility` para obter mais tempo de processamento
- Se o visibility timeout for **muito alto** (horas) e o consumidor falhar (crash), o reprocessamento vai demorar bastante para acontecer
- Se o visibility timeout for **muito baixo** (segundos), podemos acabar tendo mensagens duplicadas
---

[← Voltar para SQS, SNS, Kinesis, Active MQ](../sqs-sns-kinesis-activemq.html)
