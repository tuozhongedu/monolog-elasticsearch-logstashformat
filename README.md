# Elasticsearch with logstash formatter

This handler lets you put logs into Elasticsearch in the Logstash format, 
which makes visualization with Kibana very easy.

## Recommended setup

```php
use Elasticsearch\ClientBuilder;
use Monolog\Formatter\LogstashFormatter;
use Monolog\ElasticLogstashHandler;

$client = ClientBuilder::create()->setHosts(
    [
        'http://127.0.0.1:9200'
    ]
)->build();

$formatter = new LogstashFormatter('application', null, null, '', 1);
$handler = new ElasticLogstashHandler($client, ['type' => 'invoicing-logs']);
$handler->setFormatter($formatter);


$log = new Monolog\Logger('invoicing');
$log->pushHandler($handler);
$log->warn('new sale', ['user_id' => 42, 'product_id' => 7537]);
```


Fork from https://github.com/nulpunkt/monolog-elasticsearch-logstashformat
