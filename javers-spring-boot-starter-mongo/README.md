## Javer Spring Boot MongoDB starter configuration

### Using Spring Boot MongoDB starter settings

Spring Boot automatically configures a `MongoClient` instance.
Javers starter uses this instance by default.

```yaml
spring:
  data:
    mongodb:
      database: my-mongo-database
```
Please refer to the spring-boot-starter-data-mongodb 
[reference documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html#boot-features-mongodb) for details on how to configure MongoDB.

### Using Javers Spring Boot MongoDB starter settings

Sometimes it could be necessary to use a different MongoDB instance
for persisting Javers data.

To use a dedicated instance of MongoDB, configure Javers as shown below:

```yaml
javers:
  mongodb:
    host: localhost
    port: 27017
    database: javers-audit
    authentication-database: admin
    username: javers
    password: password
```

or:

```yaml
javers:
  mongodb:
    uri: mongodb://javers:password@localhost:27017/javers-audit&authSource=admin
```

Either `host` or `uri` has to set.

#### MongoClientOptions
If greater control is required over how Javers configures the `MongoClient` instance,
you can configure a `MongoClientOptions` bean named `javersMongoClientOptions`.
If there is no such bean, default client options are used. 

For example, to configure the MongoClient with custom parameters,
define this bean:

```java
@Bean("javersMongoClientSettings")
public MongoClientSettings clientSettings() {
    return MongoClientSetting.builder().build();
}
```