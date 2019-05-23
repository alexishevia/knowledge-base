ElasticMQ has an Amazon SQS compatible API

# List Queues
curl http://localhost:9324/?Action=ListQueues

# Receive Message
Note that receiving a message will block it from being read again during 
the visibilityTimeout period. After the period is over, the message can be 
read again.

curl http://localhost:9324/queue/myQueueName?Action=ReceiveMessage&MaxNumberOfMessages=5&VisibilityTimeout=5

# Delete Queue
curl http://localhost:9324/queue/myQueueName?Action=DeleteQueue

# Create Queue
curl http://localhost:9324/?Action=CreateQueue&QueueName=myQueueName

# Purge Queue
curl http://localhost:9324/queue/myQueueName?Action=PurgeQueue

# Send Message to Queue
export body=$(echo '
  {
    "hello": "world"
  }
' | json-minify)
curl -X POST
  --data "Action=SendMessage&MessageBody=$body" \
  --url http://localhost:9324/queue/myQueueName
