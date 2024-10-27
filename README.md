# StepFunction

# Passo a passo no fluxo de pedidos usando Amazon Step Functions
- Recepção do Pedido (Lambda + API Gateway):
Usar o API Gateway para expor um endpoint HTTP que receba os pedidos de delivery. Configurar uma função Lambda para processar a entrada e armazenar os dados iniciais, como informações do cliente e do pedido, em uma tabela DynamoDB.

- Validação de Pedido (Step Function + Lambda):
Em uma máquina de estados do Step Functions, criar um passo para validar o pedido. Esta validação pode incluir verificação de dados (como endereço) e disponibilidade dos produtos.

- Integração com Serviços de Pagamento (Step Function + Lambda):
Configurar um passo para realizar a integração com um serviço de pagamento, como o Stripe ou o AWS Payment Cryptography. A função Lambda correspondente deve realizar a transação e verificar a confirmação do pagamento. Dependendo do resultado, definir transições de sucesso ou falha no Step Functions.

- Confirmação de Pedido (SNS + Lambda):
Uma vez confirmado o pagamento, enviar uma notificação para o cliente via SNS (Simple Notification Service). Configurar uma Lambda para publicar uma mensagem no SNS, confirmando o pedido.

- Atualização do Status de Pedido (Step Function + Lambda):
Atualizar o status do pedido em uma tabela DynamoDB para refletir que o pagamento foi processado e o pedido está em preparação. utlizar função Lambda para essa atualização.

- Gerenciamento de Preparação e Entrega (Step Function + Lambda + IoT Core):
Criar passos para gerenciar a preparação e a entrega. 

- Monitoramento e Log (CloudWatch):
 CloudWatch para monitorar métricas e logs de cada função Lambda e das Step Functions. Utlizar alarmes para detectar falhas, como validação de pedido falhada, erro de pagamento ou problemas de atualização de status.

- Gerenciamento de Erros e Compensações (Step Function):
Incluir passos de fallback e de compensação para lidar com falhas em qualquer ponto. Por exemplo, se o pagamento falhar, reverter atualizações de status ou enviar notificações de erro ao cliente.
