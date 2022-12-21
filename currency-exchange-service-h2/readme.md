# Currency Exchange Micro Service - H2

## Containerization

### Creating Container

- mvn package

### Running Container

#### Basic
```
docker container run -p8000:8000 theashwinr/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT
```
#### Custom Network
```
docker run -p8000:8000 --network currency-network --name=currency-exchange-service theashwinr/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT
```

Test API 
- http://localhost:8000/api/currency-exchange-microservice/currency-exchange/from/USD/to/INR


```json output sample
{
  "id": 10001,
  "from": "USD",
  "to": "INR",
  "conversionMultiple": 65.00,
  "environmentInfo": "NA"
}
```

## H2 Console

- http://localhost:8000/api/currency-exchange-microservice/h2-console

## Tables Created
```
create table exchange_value 
(
	id bigint not null, 
	conversion_multiple decimal(19,2), 
	currency_from varchar(255), 
	currency_to varchar(255), 
	primary key (id)
)
```
