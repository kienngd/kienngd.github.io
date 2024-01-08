# Working With Influxdb Data Using PhpClient

document: [https://github.com/influxdata/influxdb-php](https://github.com/influxdata/influxdb-php)

## Install via composer
```bash
composer require influxdb/influxdb-php
```

## Create client object
```php
$client = new InfluxDB\Client($host, $port);

// directly get the database object
$database = InfluxDB\Client::fromDSN(sprintf('influxdb://user:pass@%s:%s/%s', $host, $port, $dbname));

// Fetch the database using a 5 second time out
$database = InfluxDB\Client::fromDSN(sprintf('influxdb://user:pass@%s:%s/%s', $host, $port, $dbname), 5);

// get the client to retrieve other databases
$client = $database->getClient();
```
<!--more-->
## Reading data

```php
// fetch the database
$database = $client->selectDB('influx_test_db');

// executing a query will yield a resultset object
$result = $database->query('select * from test_metric LIMIT 5');

// get the points from the resultset yields an array
$points = $result->getPoints();
```

## Use the queryBuilder object
```php
// retrieve points with the query builder
$result = $database->getQueryBuilder()
	->select('cpucount')
	->from('test_metric')
	->limit(2)
	->offset(2)
	->getResultSet()
	->getPoints();

// get the query from the QueryBuilder
$query = $database->getQueryBuilder()
	->select('cpucount')
	->from('test_metric')
	->where(["region = 'us-west'"])
	->getQuery();
```

## Get the last executed query from the client
```php
// use the getLastQuery() method
$lastQuery = $client->getLastQuery();

// or access the static variable directly:
$lastQuery = Client::lastQuery;
```

## Writting data
```php
// create an array of points
$points = array(
	new Point(
		'Measurement_Name', // name of the measurement
		0.64, // the measurement value
		['tag_key_1' => 'tag_value_1', 'tag_key_2' => 'tag_value_2',], // optional tags
		['field_key_1' => 'field_value_1',], // optional additional fields
		1435255849 // Time precision has to be set to seconds!
	),
    new Point(
    	'Measurement_Name', // name of the measurement
		0.64, // the measurement value
		['tag_key_1' => 'tag_value_3', 'tag_key_2' => 'tag_value_4',], // optional tags
		['field_key_1' => 'field_value_5',], // optional additional fields
		1435256149 // Time precision has to be set to seconds!
	)
);

// we are writing unix timestamps, which have a second precision
$result = $database->writePoints($points, Database::PRECISION_SECONDS);
// You can use some other precisions
/*
    PRECISION_NANOSECONDS
    PRECISION_MICROSECONDS
    PRECISION_MILLISECONDS
    PRECISION_SECONDS
    PRECISION_MINUTES
    PRECISION_HOURS
*/
```

