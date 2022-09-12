# SQS & SNS AWS

- Serviço de mensageria da AWS.
- Gerenciamento via console AWS e operações por cli ou sdks.
- Queues são identificáveis pela URL disponiblizada e as  mensagens são enviadas no formato texto.
- disponiblidade servida pela própria AWS.
- pelo console AWS cria-se uma fila onde pode-se enviar/consumir mensagens tb.
- é necessário configurar credenciais de acesso pelo `aws configure` com acesso de `AmazonSQSFullAccess`.
- comandos comuns:
```shell
aws sqs create-queue
aws sqs send-message
aws sqs receive-message
```
- `Long Polling`: parâmetro `wait-time-seconds` permite abrir uma conexão que só é finalizada após processar as mensagens recebidas ou quando o timeout é atingido, com isso se reduz quantidade de conexões e custo evitando-se a estratégia de short polling.
- uma vez processada as mensagens deve-se remover as mesmas ou em caso de erro de leitura enviar para uma DLQ(Dead Letter Queue).
- `Visibility Timeout`: configura o tempo de processamento de uma mensagem, permitindo que ela fique invisível a outros consumidores e garante indepotencia.
- `DLQ(Dead Letter Queue) & Poison Messages`: pode-se configurar um número X de tentativas de leitura de uma mensagem (tolerância de falha) até enviar a mesma para uma DLQ.
- Ordenação das mensagens: pode-se garantir a ordenação de mensagens criando uma fila do tipo `FIFO`, para isso é necessário adicionar o sufixo `.fifo` ao nome da fila e configurar o parâmetro `MessageGroupId`(chave de agrupamento) onde as mensagens de um grupo chegam em ordem.
- `ContentBasedDeduplication`: parâmetro que habilitado remove mensagens duplicadas dentro de um intervalo de 300 segundos.
- Cenário com N consumidores: para este cenário deve-se criar um tópico (SNS), neste tópico os consumidores são escritos e as mensagens são distribuídas(Fanout).
- os tipos de inscrições em um tópico podem ser: endpoints HTTP, filas SQS, números de telefone.