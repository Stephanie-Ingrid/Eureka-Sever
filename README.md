# Service discovery com Eureka Sever 

## Eureka Server faz parte do pacote Spring Cloud Netflix

### O Eureka Server é um serviço REST que será responsável por “conhecer” todas as nossas instâncias de serviços.

### Ferramentas para executar
- Java 17
- Maven


<p>Para que esse serviço conheça as nossas instâncias, utiliza-se um padrão chamado self registration, onde cada instância 
deverá se auto-registrar no servidor Eureka Client. O registro é através das variáveis de ambiente no
application.properties exemplo:</p>

    spring.application.name=servico-ms

    eureka.client.register-with-eureka=true
    eureka.client.fetch-registry=true
    eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
    server.port=0
    
A biblioteca que foi usada para registro do serviço é:

	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
            <version>4.1.1</version>
    </dependency>

Na classe de inicialização é utilizada a anotação `@EnableDiscoveryClient` para a versão 4.1.1 exemplo:

    
    @SpringBootApplication
    @EnableDiscoveryClient
    public class ServicoApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(ServicoApplication.class, args);
        }
    
    }

E pronto! sua aplicação estará pronta para utilizar o Service Discovery.

## Conteúdo Adicional
Se quiser um ID random use essa variavel de ambiente:

    eureka.instance.instance-id=${spring.application.name}:${random.int}


_Essa aplicação foi desenvolvida para fins de estudo de load balancer, gateway e discovery service._