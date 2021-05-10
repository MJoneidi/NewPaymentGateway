# NewPaymentGateway
This is a payment gateway, a mediator between Bank and Merchant

# Technology Stack
. Dotnet core 5
. Asynchronous Request-Reply pattern.
. Uses JWT Authentication
. Uses Command Query Responsibility Segregation (CQRS) with Event Sourcing.
. Uses RabbitMQ for write-to-read messaging.
. Uses MongoDB for read database, Dapper, Dotnet EF core with SQL Server in write database.
. Uses NLog.
. Uses Ocelot as gateway.
. Uses Docker & Docker Compose to deploy & run all services. 
