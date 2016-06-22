# no-kafka

__no-kafka__ is [Apache Kafka](https://kafka.apache.org) 0.9 client for Node.js with [new unified consumer API](#groupconsumer-new-unified-consumer-api) support.

It's a fork [from] https://github.com/oleksiyk/kafka. This version has 'just' the ssl-capabilities of kafka 0.9 included. 
To connect to a kafka >0.9 server just pass a ssl attribute within the option parameter of the producer or consumer. E.g:



```json
    "dependencies" : {
        "no-kafka": "git+https://github.com/amocoma/kafka.git"
    },
```


```javascript
var Kafka = require('no-kafka');
var zkOptions = {connectionString:'kafka+ssl://abc1.com:9096,kafka+ssl://abc2.com:9096', 
       ssl: {
              key:env.KAFKA_CLIENT_CERT_KEY, 
              cert:env.KAFKA_CLIENT_CERT, 
              ca:env.KAFKA_TRUSTED_CERT, 
              checkServerIdentity: function (host, cert) {return undefined;}
       }
};
var producer = new Kafka.Producer(zkOptions);

producer.init().then(function(){
 return producer.send({
  topic: 'test',
  partition: 0,
  message: {
   value: 'Hello!'
  }
 });
}).then(function (result) {
 node.log(' xxxxxx result : ' + JSON.stringify(result));
});
```

--dirk
