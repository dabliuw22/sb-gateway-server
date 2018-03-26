# Gateway Server

Servidor gateway para microservicios.

1. Dependencias:
	* Cloud Routing: Zuul.
	* Cloud Discovery: Eureka Discovery.
	* Cloud Tracing: Sleuth, Zipkin Client.
	* Actuator.

2. Anotar con *@EnableZuulProxy* y *@EnableDiscoveryClient* la clase de configuración.

3. Crear Bean defaultSampler para trazabilidad:
	* Spring Boot 1:
		```[java]
		@Bean
		public AlwaysSampler defaultSampler() {
			return new AlwaysSampler();
		}
		```
	* Spring Boot 2:
		```[java]
		@Bean
		public Sampler defaultSampler() {
			return Sampler.ALWAYS_SAMPLE;
		}
		```

4. Renombrar *application.yml* por *bootstrap.yml* y agregar:
```[yml]
server:
  port: 8765
spring:
  application:
    name: gateway-server
eureka:
  client:
    service-url:
      default-zone: ${EUREKA_URI:http://localhost:8761/eureka}
```