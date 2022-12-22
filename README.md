# Currency exchange Spring Boot Microservice with AWS Fargate

- Deployment using AWS ECS (Fargate)
- Distributed tracing using AWS X Ray
- Containerization using Docker
- CI/CD integration with AWS codepipeline
- Centralized configuration using AWS SSM

## Container Images

|     Application                 |    Container                                  |
| ------------------------------- | --------------------------------------------- |
| CurrencyExchangeMicroservice-H2 | theashwinr/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT |
| CurrencyExchangeMicroSevice-MySQL| theashwinr/aws-currency-exchange-service-mysql:0.0.1-SNAPSHOT|
| CurrencyConversionMicroservice | theashwinr/aws-currency-conversion-service:0.0.1-SNAPSHOT |
| Currency Exchange - X Ray | theashwinr/aws-currency-exchange-service-h2-xray:0.0.1-SNAPSHOT|
| Currency Conversion - X Ray | theashwinr/aws-currency-conversion-service-xray:0.0.1-SNAPSHOT|

|     Utility       |     Container Image        |
| ------------- | ------------------------- |
| aws-xray-daemon| amazon/aws-xray-daemon:1|

## Microservice URLs and Details

### Currency Exchange Service

- HEALTH URL - `http://localhost:8000/api/currency-exchange-microservice/manage/health`
- Enviroment Variables
  - /dev/currency-exchange-service/RDS_DB_NAME  - exchange_db
  - /dev/currency-exchange-service/RDS_HOSTNAME 
  - /dev/currency-exchange-service/RDS_PASSWORD 
  - /dev/currency-exchange-service/RDS_PORT     - 3306
  - /dev/currency-exchange-service/RDS_USERNAME - exchange_db_user

Example:
-http://localhost:8000/api/currency-exchange-microservice/currency-exchange/from/USD/to/INR

```json
{
  "id": 10001,
  "from": "USD",
  "to": "INR",
  "conversionMultiple": 80.00,
  "environmentInfo": "NA"
}
```

### Currency Conversion Service

- HEALTH URL - `http://localhost:8100/api/currency-conversion-microservice/manage/health`
- Enviroment Variables
  - /dev/currency-conversion-service/CURRENCY_EXCHANGE_URI
  - /dev/currency-conversion-service/CURRENCY_EXCHANGE_URI
  - /dev/currency-exchange-service/RDS_DB_NAME  - exchange_db
  - /dev/currency-exchange-service/RDS_HOSTNAME 
  - /dev/currency-exchange-service/RDS_PASSWORD 
  - /dev/currency-exchange-service/RDS_PORT     - 3306
  - /dev/currency-exchange-service/RDS_USERNAME - exchange_db_user

Example:
-http://localhost:8100/api/currency-converter/from/USD/to/INR/quantity/1000

```json
{
  "id": 10001,
  "from": "USD",
  "to": "INR",
  "conversionMultiple": 80.00,
  "quantity": 1000,
  "totalCalculatedAmount": 80000.00,
  "environmentInfo": "NA"
}
```
