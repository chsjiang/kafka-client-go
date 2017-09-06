# kafka-client-go

Library for producing and consuming messages directly from Kafka.


## To use
To import:
```
import "github.com/Financial-Times/kafka-client-go/kafka"
```

### Producer
To set up, create your producer:
```
kp, err := kafka.NewProducer(*kafkaAddresses, *kafkaTopic)
```

You can then send an FT Message:
```
message := kafka.NewFTMessage(map[string]string{}, string(concept))
err = kp.SendMessage(message)
```


### Consumer
Create the consumer and start listening:
```
kc, err := kafka.NewConsumer(*zookeeperConnectionString, *groupName, []string{*topic})
kc.StartListening(handler.ProcessKafkaMessage)
```

Make sure to close it when the app is shutting down.
```
kc.Shutdown()
```


## Testing
Some tests in this project require a local Zookeeper/Kafka. To omit these tests, use the `-short` option.
